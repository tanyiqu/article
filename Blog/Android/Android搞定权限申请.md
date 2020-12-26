## 0x00 前言

使用EasyPermissions库进行申请权限

打开App时就申请权限，如果用户拒绝权限后，会循环申请

如果永久拒绝后，会跳转到设置里继续申请

效果图：

![效果图](https://img2020.cnblogs.com/blog/2034131/202012/2034131-20201222131043500-1253789423.gif)

注：不讲原理，先教你怎么实现

<br>

## 0x01 引入依赖

在**app**的**build.gradle**里面，添加EasyPermissions的依赖

```gradle
implementation 'pub.devrel:easypermissions:2.0.0'
```

添加后点击 File -> Sync Project with Gradle Files 重新构建一些项目

<br>

## 0x02 创建PermissionActivity

创建一个PermissionActivity用于获取权限，布局随意

可以把它设为启动Activity，也可以由SplashActivity转至PermissionActivity

<br>

创建完成后，让PermissionActivity实现**EasyPermissions.PermissionCallbacks**，并重新下面三个方法

PermissionActivity复制下面的内容即可

```java
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

import java.util.List;

import pub.devrel.easypermissions.EasyPermissions;

public class PermissionActivity extends AppCompatActivity implements EasyPermissions.PermissionCallbacks {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_permission);
    }

    // 重新下面三个方法
    
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        EasyPermissions.onRequestPermissionsResult(requestCode, permissions, grantResults, this);
    }

    @Override
    public void onPermissionsGranted(int requestCode, @NonNull List<String> perms) {

    }

    @Override
    public void onPermissionsDenied(int requestCode, @NonNull List<String> perms) {

    }
}
```



<br>

## 0x03 三个方法

其中**onRequestPermissionsResult**是权限申请后执行的方法，默认就写成上面那样就行

**onPermissionsGranted**是权限授权时的回调

**onPermissionsDenied**是权限被拒绝时的回调

<br>

## 0x04 申请权限

假如要申请存储权限

首先在**AndroidManifest.xml**里面加上这两行

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```



然后，在**PermissionActivity**里定义两个常量

```java
// 指定申请存储权限时，一个标识符，用于在成功或失败回调中判断申请成功的或失败的是哪几个权限
static final int STORAGE_CALL_BACK_CODE = 0;
// 存储权限
static final String[] perms_storage = new String[]{Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE};
```



在**onCreate**里面加上申请权限的代码

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_permission);

    if (EasyPermissions.hasPermissions(this, perms_storage)) {
        Toast.makeText(this, "已经有存储权限", Toast.LENGTH_SHORT).show();
    } else {
        EasyPermissions.requestPermissions(this, "请给我权限", STORAGE_CALL_BACK_CODE, perms_storage);
    }
}
```

<br>



## 0x05 处理授权成功 

**onPermissionsGranted**方法

```java
@Override
public void onPermissionsGranted(int requestCode, @NonNull List<String> perms) {
    //noinspection SwitchStatementWithTooFewBranches
    switch (requestCode) {
        // 如果存储权限申请通过
        case STORAGE_CALL_BACK_CODE:
            Toast.makeText(this, "已同意存储权限", Toast.LENGTH_SHORT).show();
            // pass为通过后执行的方法，注意下面有个finish()，pass()中就不要再加finish()了
            pass();
            finish();
            break;
    }
}
```



<br>

## 0x06 处理授权失败

**onPermissionsDenied**方法

```java
@Override
public void onPermissionsDenied(int requestCode, @NonNull List<String> perms) {
    //noinspection SwitchStatementWithTooFewBranches
    switch (requestCode) {
        case STORAGE_CALL_BACK_CODE:
            Toast.makeText(this, "已拒绝存储权限", Toast.LENGTH_SHORT).show();
            ActivityCompat.requestPermissions(this, perms_storage, STORAGE_CALL_BACK_CODE);
            break;
    }
    // 如果权限被永久拒绝，就提示到设置页面中开启
    if (EasyPermissions.somePermissionPermanentlyDenied(this, perms)) {
        Toast.makeText(this, "权限已被永久拒绝", Toast.LENGTH_SHORT).show();
        new AppSettingsDialog
            .Builder(this)
            .setTitle("权限已被永久拒绝")
            .setRationale("该应用需要此权限，否则无法正常使用，是否打开设置")
            .setPositiveButton("确定")
            .setNegativeButton("取消")
            .build()
            .show();
    }
}
```

<br>

## 0x07 完整代码

**PermissionActivity**

```java
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;

import android.Manifest;
import android.content.Intent;
import android.os.Bundle;
import android.widget.Toast;

import java.util.List;

import pub.devrel.easypermissions.AppSettingsDialog;
import pub.devrel.easypermissions.EasyPermissions;

public class PermissionActivity extends AppCompatActivity implements EasyPermissions.PermissionCallbacks {

    static final int STORAGE_CALL_BACK_CODE = 0;
    static final String[] perms_storage = new String[]{Manifest.permission.READ_EXTERNAL_STORAGE, Manifest.permission.WRITE_EXTERNAL_STORAGE};


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_permission);

        if (EasyPermissions.hasPermissions(this, perms_storage)) {
            Toast.makeText(this, "已经有存储权限", Toast.LENGTH_SHORT).show();
        } else {
            EasyPermissions.requestPermissions(this, "请给我权限", STORAGE_CALL_BACK_CODE, perms_storage);
        }
    }

    void pass() {
        startActivity(new Intent(this, MainActivity.class));
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        EasyPermissions.onRequestPermissionsResult(requestCode, permissions, grantResults, this);
    }

    @Override
    public void onPermissionsGranted(int requestCode, @NonNull List<String> perms) {
        //noinspection SwitchStatementWithTooFewBranches
        switch (requestCode) {
            // 如果存储权限申请通过
            case STORAGE_CALL_BACK_CODE:
                Toast.makeText(this, "已同意存储权限", Toast.LENGTH_SHORT).show();
                // pass为通过后执行的方法，注意下面有个finish()，pass()中就不要再加finish()了
                pass();
                finish();
                break;
        }
    }

    @Override
    public void onPermissionsDenied(int requestCode, @NonNull List<String> perms) {
        //noinspection SwitchStatementWithTooFewBranches
        switch (requestCode) {
            case STORAGE_CALL_BACK_CODE:
                Toast.makeText(this, "已拒绝存储权限", Toast.LENGTH_SHORT).show();
                ActivityCompat.requestPermissions(this, perms_storage, STORAGE_CALL_BACK_CODE);
                break;
        }
        // 如果权限被永久拒绝，就提示到设置页面中开启
        if (EasyPermissions.somePermissionPermanentlyDenied(this, perms)) {
            Toast.makeText(this, "权限已被永久拒绝", Toast.LENGTH_SHORT).show();
            new AppSettingsDialog
                    .Builder(this)
                    .setTitle("权限已被永久拒绝")
                    .setRationale("该应用需要此权限，否则无法正常使用，是否打开设置")
                    .setPositiveButton("确定")
                    .setNegativeButton("取消")
                    .build()
                    .show();
        }
    }
}
```

<br>

## 0x08 项目代码

项目在github上面，有用的话，可以给一个star

https://github.com/tanyiqu/android-permission-demo