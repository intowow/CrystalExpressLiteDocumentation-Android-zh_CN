### 配置步驟
要啟用預覽模式，您必須在 AndroidManifest.xml 裡的起始 `Activity` 中加入 `深度連結 (Deeplink)` 設定

``` xml
<intent-filter>
    <actionandroid:name="android.intent.action.VIEW"/>
    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="android.intent.category.BROWSABLE"/>
    <data android:scheme="{APP_URL_SCHEME}"android:host="crystalexpress"/>
    <data android:scheme="{APP_URL_SCHEME}"android:host="activate"android:pathPattern=".*"/>
</intent-filter>
```

- `APP_URL_SCHEME` 只能是小寫英數字，通常是您的 App 名稱。
- 將 `APP_URL_SCHEME` 告知您的 intowow 聯絡窗口，待 CrystalExpress&trade; 平台設定完成後方可進行預覽測試。

### 預覽測試步驟
1. 透過 CrystalExpress™ 後台上稿後，每個廣告都會產生一組 QRCode。
2. 開發人員用實體手機掃瞄此 QRCode 後將開起 SDK 預覽模式，並且可以看到所要求的廣告。
3. 測試完成後需強制停止 App，此時 SDK 將離開預覽模式。
