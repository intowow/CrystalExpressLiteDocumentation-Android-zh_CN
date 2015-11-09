如果 App 有使用程式碼混淆機制 (proguard)，請在設定檔裡加上
``` java
-keep class com.intowow.sdk.* { *; }
-keep interface android.support.v4.app.** { *; }
-keep class android.support.v4.** { *; }
```
