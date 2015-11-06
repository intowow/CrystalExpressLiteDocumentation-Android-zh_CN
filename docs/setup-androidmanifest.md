### AndroidManifest.xml 相關設定

#### 設定 SDK 所需權限

``` xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
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
<meta-data android:name="CRYSTAL_ID" android:value="Intowow提供的CRYSTAL_ID" />
```