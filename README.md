# FLutter-Tips 开发中遇到的点点滴滴记录

    In file included from /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.m:1:
    /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.h:1:9: fatal error: 'Flutter/Flutter.h' file not found
    #import <Flutter/Flutter.h>
            ^~~~~~~~~~~~~~~~~~~
    1 error generated.
   
这个解决了 大家如果也遇到了 可以尝试
1.在项目根目录运行 flutter clean  
2.删除ios/podfile.lock 再运行
