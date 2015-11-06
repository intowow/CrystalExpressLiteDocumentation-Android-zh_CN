### Crystal ID 設定
確認 AndroidManifest.xml 中所使用的 Crystal ID 設定正確，與 CrystalExpress 平台中設定吻合。

### SDK 運行環境
確認 SDK 非初使化為測試環境。

### Activity 生命週期回報
確認所有 Activity 都有調用 onActivityResume 與 onActivityPause 。