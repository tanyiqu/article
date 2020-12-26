## 0x01 创建SplashActivity

新建一个Activity，取名为**SplashActivity**

<br>

## 0x02 新建资源

在**res/drawable**下新建一个**splash.xml**文件和名为**ig_splash**的图片

splash.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <!-- 图片 -->
        <!-- gravity也可以为“center”，具体看效果而定 -->
        <bitmap
            android:gravity="fill"
            android:src="@drawable/ig_splash" />
    </item>
</layer-list>
```

<br>

## 0x03 设置主题

设置主题

在**values/styles**里面添加如下

```xml
<style name="SplashTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <item name="android:windowBackground">@drawable/splash</item>
    <item name="android:windowFullscreen">true</item>
</style>
```

<br>

## 0x04 修改AndroidManifest.xml

在**AndroidManifest.xml**中，修改**SplashActivity**的theme为**SplashTheme**，并把它设为启动activity（同时记得取消**MainActivity**为启动activity）

```xml
<activity
          android:name=".activity.SplashActivity"
          android:theme="@style/SplashTheme">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <!-- 加下面这句可以消除一些警告 -->
        <action android:name="android.intent.action.VIEW" />

        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

<br>

## 0x05 修改SplashActivity.java

修改**SplashActivity.java**

```java
public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        startActivity(new Intent(this, MainActivity.class));//启动完主Activity就finish
        finish();
    }
}
```

<br>

## 0x06 验证效果

这时候启动app就有秒开启动图的效果