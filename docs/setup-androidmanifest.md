### AndroidManifest.xml 相關設定

#### 設定 SDK 所需權限

``` xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

#### 設定 Activity
CrystalExpress&trade; SDK Lite 支援 In-App 瀏覽，您必須在 Activity 裏新增以下的設定。
``` xml
<activity
  android:name="com.intowow.sdk.WebViewActivity"
  android:configChanges="orientation|screenSize"
  android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
</activity>
```

若需要整合開機蓋屏，可加入下面設定
``` xml
<activity
  android:name="com.intowow.sdk.InterstitialAdActivity"
  android:configChanges="orientation|screenSize"
  android:launchMode="singleTask"
  android:screenOrientation="portrait"
  android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen" >
</activity>
```

#### 設定 Receiver
``` xml
<receiver android:name="com.intowow.sdk.ScheduleReceiver" android:exported="false">
    <intent-filter >
    <action android:name="com.intowow.sdk.prefetch"/>
    </intent-filter>
</receiver>
```

#### 設定 Crystal ID
``` xml
<meta-data android:name="CRYSTAL_ID" android:value="intowow提供的CRYSTAL_ID" />
```
