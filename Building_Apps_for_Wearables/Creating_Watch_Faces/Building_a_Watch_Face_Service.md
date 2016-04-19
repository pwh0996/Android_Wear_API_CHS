# 创建表盘服务 [Building a Watch Face Service]

标签（空格分隔）： Wear

---

表盘是作为一个服务打包安装在Android Wear中,当用户安装一个包含Watch app 和表盘的手机APP时，表盘将会同时出现在手机伴侣应用中和手表变盘选择器中。当用户选择需要显示的表盘时候，根据需要回调方法。

这节课将向你展示如何配置一个Android工程包括表盘和表盘服务。

---

### 创建和配置你的工程
在你的Android studio中创建Android Wear工程

1. 打开 Android Studio
2. 创建新工程
    * 如果你没有打开过工程，在欢迎界面点击 New Project
    * 如果你打开过工程，在 File 中选择 New Project
3. 提供一个应用名称，然后点击 Next
4. 选择这 Phone And Tablet 模式
5. 在 Minimum SDK 下选择 API 18
6. 选择 Wear 模式
7. 在 Minimum SDK 下选择 API 21 然后点击 Next
8. 选择 Add No Activity 然后点击 Next 在后面的两个界面
9. 点击 Finish
10. 点击 View > ToolWindows > Project 在这个窗口
Android Studio 创建 手表 和 电话工程，更多信息可以参考创建一个工程[创建一个工程][1]

### 依赖关系 
Wearable Support Library 库提供了一些必须的类，你可以继承这些类去实现表盘。Google play services 客户端库(play-services 和 play-services-wearable)库是用来同步手机APP和手表APP之间数据。可以参见
 [Wearable Data Layer API][2]
 
### 穿戴支持库API参考
以下参考信息将告诉你实现表盘所需要的一些类的信息，详细穿戴库信息可以参考[API reference documentation][3]

> Note:欢迎使用Android studio 去构建你的项目，它提供了工程设置，包含库，方便打包。

#### 权限申明
表盘需要 PROVIDE_BACKGROUND 和 WAKE_LOCK 权限, 同时在你的手机APP中和穿戴设备APP工程中的manifest文件中添加以下权限。

```
<manifest ...>
    <uses-permission
        android:name="com.google.android.permission.PROVIDE_BACKGROUND" />
    <uses-permission
        android:name="android.permission.WAKE_LOCK" />
    ...
</manifest>
```
> 注意：手机APP中必须包含穿戴设备APP中的所有权限。

----

### 实现服务和回调函数
表盘在Android Wear 中是一个被实现的Services。当表盘活动时，每当时间改变，或者有事件触发(像进入豆子模式，或者受到一个通知)系统都会去调用在Services中的这些回调方法。Services用于实现绘制表盘、更新时间和其他相关的事情。为了实现表盘，你需要继承[CanvaWatchFaceService][4]和[CanvasWatchFaceService.Engine][5]类,然后复写CanvasWatchFaceService.Engine中的回调方法，这些类属于[Wearable Support Library][6]库

下面列出的你需要实现的回调方法
```
public class AnalogWatchFaceService extends CanvasWatchFaceService {

    @Override
    public Engine onCreateEngine() {
        /* provide your watch face implementation */
        return new Engine();
    }

    /* implement service callback methods */
    private class Engine extends CanvasWatchFaceService.Engine {

        @Override
        public void onCreate(SurfaceHolder holder) {
            super.onCreate(holder);
            /* initialize your watch face */
        }

        @Override
        public void onPropertiesChanged(Bundle properties) {
            super.onPropertiesChanged(properties);
            /* get device features (burn-in, low-bit ambient) */
        }

        @Override
        public void onTimeTick() {
            super.onTimeTick();
            /* the time changed */
        }

        @Override
        public void onAmbientModeChanged(boolean inAmbientMode) {
            super.onAmbientModeChanged(inAmbientMode);
            /* the wearable switched between modes */
        }

        @Override
        public void onDraw(Canvas canvas, Rect bounds) {
            /* draw your watch face */
        }

        @Override
        public void onVisibilityChanged(boolean visible) {
            super.onVisibilityChanged(visible);
            /* the watch face became visible or invisible */
        }
    }
}
```
CanvasWatchFaceService 类提供了一个View.invalidate()方法,你可以调用你的实现类中的 invalidate()方法,让系统重新绘制表盘，你只能在主UI线程中使用此方法.对于没有界面的其他线程，你可调用postInvalidate()方法。

对于CanvasWatchFaceService.Engine 类中跟多回调方法的介绍 请参考[Drawing Watch Faces][7]

----

### 注册表盘服务
在你实现了表盘服务之后，你应该在Mainifest文件中注册你的表盘Services.当用户安装APP.系统会根据Services信息在手机伴侣程序和手表表盘选择器中显示表盘。
下面代码将向你展示在 application 标签中如何注册表盘Services
```
<service
    android:name=".AnalogWatchFaceService"
    android:label="@string/analog_name"
    android:permission="android.permission.BIND_WALLPAPER" >
    <meta-data
        android:name="android.service.wallpaper"
        android:resource="@xml/watch_face" />
    <meta-data
        android:name="com.google.android.wearable.watchface.preview"
        android:resource="@drawable/preview_analog" />
    <meta-data
        android:name="com.google.android.wearable.watchface.preview_circular"
        android:resource="@drawable/preview_analog_circular" />
    <intent-filter>
        <action android:name="android.service.wallpaper.WallpaperService" />
        <category
            android:name=
            "com.google.android.wearable.watchface.category.WATCH_FACE" />
    </intent-filter>
</service>
```
> Note：这里的注册只在手表工程中

com.google.android.wearable.watchface.preview 该定义用来指定表盘预览图,这个预览图将被用在手机伴侣程序和手边表盘选择器中展示。对于这张图片，你可以把表盘运行在手表上或者模拟器上然后截个图。在手表hdpi屏幕设备上,这张预览图尺寸是 320x320 pixels

不起来不同的表盘能同时提供圆形和方形的预览图片，你可以指定提供圆形图片，使用com.google.android.wearable.watchface.preview_circular 参数值。如果一个表盘包含两个预览图片，在手机伴侣和手表表盘选择器上将会显示适当的那个，如果再圆的表盘上，但是没有提供圆形预览图，那么将会把方形预览图裁剪作为圆形表盘的预览图。

android.service.wallpaper 的条目指定了资源文件watch_face.xml,它包含wallpaper元素
你的手表APP能包含多个表盘，你必须在Manifest文件中添加表盘实现的服务。


  


  [1]: http://developer.android.com/sdk/installing/create-project.html
  [2]: http://developer.android.com/training/wearables/data-layer/index.html
  [3]: http://developer.android.com/reference/android/support/wearable/watchface/package-summary.html
  [4]: http://developer.android.com/reference/android/support/wearable/watchface/CanvasWatchFaceService.html
  [5]: http://developer.android.com/reference/android/support/wearable/watchface/CanvasWatchFaceService.Engine.html
  [6]: http://developer.android.com/reference/android/support/wearable/watchface/package-summary.html
  [7]: http://developer.android.com/training/wearables/watch-faces/drawing.html