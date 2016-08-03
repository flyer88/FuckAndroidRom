## 权限适配问题
### 问题描述
    6.0 以后如果不请求权限，直接运行，会导致崩溃
### 解决方案
先检查权限，如果没有则请求权限
```
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.READ_CONTACTS)
        != PackageManager.PERMISSION_GRANTED) {
}else{
    //
    ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.READ_CONTACTS},
                MY_PERMISSIONS_REQUEST_READ_CONTACTS);
}
```
然后在`onRequestPermissionsResult`中获取请求的回调
```
@Override
public void onRequestPermissionsResult(int requestCode,
        String permissions[], int[] grantResults) {
    switch (requestCode) {
        case MY_PERMISSIONS_REQUEST_READ_CONTACTS: {
            // If request is cancelled, the result arrays are empty.
            if (grantResults.length > 0
                && grantResults[0] == PackageManager.PERMISSION_GRANTED) {

                // permission was granted, yay! Do the
                // contacts-related task you need to do.

            } else {

                // permission denied, boo! Disable the
                // functionality that depends on this permission.
            }
            return;
        }
    }
}
```
后续详细的解决方案可以参考鸿洋大神的这篇文字[Android 6.0 运行时权限处理完全解析](http://blog.csdn.net/lmj623565791/article/details/50709663)

