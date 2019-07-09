# # 学习途径
   ### 1.Effevtive Dart
   >http://dart.goodev.org/guides/language/effective-dart/
# # FLutter-Tips 开发中遇到的点点滴滴记录
### 1.iOS 'Flutter/Flutter.h' file not found
    In file included from /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.m:1:
    /Users/mt/.pub-cache/hosted/pub.flutter-io.cn/flutter_webview_plugin-0.2.1+2/ios/Classes/FlutterWebviewPlugin.h:1:9: fatal error: 'Flutter/Flutter.h' file not found
    #import <Flutter/Flutter.h>
            ^~~~~~~~~~~~~~~~~~~
    1 error generated.
   
这个解决了 大家如果也遇到了 可以尝试
* 在项目根目录运行 flutter clean  
*  删除ios/podfile.lock 再运行

### 2.目前这个版本还存在编译问题，flutter官方也在积极解决
真机运行报错couldn't find "libflutter.so"

暂时的解决方法有：

build.gradle设置

```
ndk{
     abiFilters 'armeabi', 'armeabi-v7a'//, 'arm64-v8a'
}
```

或者可以增加编译选项：

```
--target-platform android-arm64 或者 --target-platform android-arm
```

```
注意~~~~~~~~~~~~~~~~~~~~~~~~~~~了
app/build.gradle文件
defaultConfig节点下

打正式包(加入NDK限制)
        ndk {
            abiFilters 'armeabi-v7a'//'armeabi', 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64', 'mips', 'mips64'
        }
打测试包(注释掉NDK代码)
```
### 3.'_InternalLinkedHashMap<dynamic, dynamic>' is not a subtype of type 'Map<String, dynamic>' 
解决办法: ``new Map<String, dynamic>.from(snapshot.value);``

> 引用自:https://github.com/flutter/flutter/issues/16589

### 4.TextField限制字数
如果需要字数提示框 就用``maxLength:11``
如果不需要字数提示框就用 

```
inputFormatters: <TextInputFormatter>[
    WhitelistingTextInputFormatter.digitsOnly, //限制输入格式
    LengthLimitingTextInputFormatter(11),// 限制字数
]
```
### 5.继承key  :super(key:key)的意义
widget绑定key时，如果没有继承就会找不到这个widget

### 6.页面保持状态
   继承AutomaticKeepAliveClientMixin，并实现
   ```
   @override
   bool get wantKeepAlive => true;
   ```
   重点注意: 使用AutomaticKeepAliveClientMixin还要在build函数里写``super.build()``
   ```
   @override
   Widget build(BuildContext context) {
      super.build(context);
      return Container();
   }
   ```
### 7.Android WebView无法在https下加载http资源 (表现为某些http视频资源无法播放)
   在webview加载页面之前，设置加载模式为MIXED_CONTENT_ALWAYS_ALLOW
   ```
   if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
      webView.getSettings().setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW);
   }
   ```
### 8.Navigator pop to root
   ```
   Navigator.popUntil(context, (Route<dynamic> route) => route.isFirst)
   ```
### 9.ListView foreach如何获取index
```
List _sample = ['a','b','c'];
_sample.asMap().forEach((index, value) => f);
```
> 引用自:https://stackoverflow.com/questions/54898767/enumerate-or-map-through-a-list-with-index-and-value-in-dart

```
移除__MAXOSX文件夹
zip -d filename.zip __MACOSX/\*
```
