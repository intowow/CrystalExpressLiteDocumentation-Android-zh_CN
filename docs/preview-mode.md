### 配置步驟
在 AndroidManifest.xml 裡的起始 `Activity` 中加入新的 `深度連結 (Deeplink)` 設定

``` xml
<intent-filter>
    <actionandroid:name="android.intent.action.VIEW"/>
    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="android.intent.category.BROWSABLE"/>
    <data android:scheme="{APP_URL_SCHEME}"android:host="crystalexpress"/>
    <data android:scheme="{APP_URL_SCHEME}"android:host="activate"android:pathPattern=".*"/>
</intent-filter>
```

再將此 `APP_URL_SCHEME` 告知 intowow 相關負責人員，等 CrystalExpress 平台設定完成後方可進行預覽測試。

### 預覽測試步驟
1. intowow 相關負責人員將提供一組 `QRCode`，開發人員用實體手機掃瞄此 `QRCode` 後將開起 SDK 預覽模式
2. 當 SDK 設定為預覽模式，開發人員將看到一則由 intowow 負責人員所設定的測試廣告
3. 測試完成後需強制停止應用程式，此時 SDK 將離開測試模式
