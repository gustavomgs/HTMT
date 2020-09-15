# HT-MT

Welcome Gilsberty Boscolo.

## Getting Started

>install Flutter/Dart in your IDE i recommend VSCODE.

 https://flutter.dev/docs/get-started/editor?tab=vscode

>After the install vscode, go to extensions and install this extension:
```
Pubspec Assist
```

Pubspec is helpful to install packages in your project.

> After install the extension open a terminal in vscode and insert this command:

```
$ fluter create projectname
```

> In your selected project press Ctrl+Shift+P and type it:
```
Pubspec
```

> And enter the package name: 
```
async
```
And
```
webview
```

> After this replace the main and class of FlutterProject for this code:

```
void main() => runApp(
    MaterialApp(debugShowCheckedModeBanner: false, home: WebViewExample()));

const String kNavigationExamplePage = '''
''';Gisl

class WebViewExample extends StatefulWidget {
  @override
  _WebViewExampleState createState() => _WebViewExampleState();
}

class _WebViewExampleState extends State<WebViewExample> {
  final Completer<WebViewController> _controller =
      Completer<WebViewController>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: Builder(builder: (BuildContext context) {
        return WebView(
          initialUrl: 'https://ht-mt.org/',
          javascriptMode: JavascriptMode.unrestricted,
          onWebViewCreated: (WebViewController webViewController) {
            _controller.complete(webViewController);
          },
          javascriptChannels: <JavascriptChannel>[
            _toasterJavascriptChannel(context),
          ].toSet(),
          onPageStarted: (String url) {
            print('Página iniciada carregando: $url');
          },
          onPageFinished: (String url) {
            print('Página finalizada carregando: $url');
          },
          gestureNavigationEnabled: true,
        );
      }),
    );
  }

  JavascriptChannel _toasterJavascriptChannel(BuildContext context) {
    return JavascriptChannel(
        name: 'Toaster',
        onMessageReceived: (JavascriptMessage message) {
          Scaffold.of(context).showSnackBar(
            SnackBar(content: Text(message.message)),
          );
        });
  }
}
``` 
