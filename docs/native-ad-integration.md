您可以透過以下步驟為 Android App 添加原生廣告。

### 整合步驟
  - 請求一個原生廣告
``` android
private NativeAd  nativeAd;
private MediaView mediaView;

private void showNativeAd() {

  // 步驟一 : 請求原生廣告
  nativeAd = new NativeAd(this, “廣告版位名稱”);
  nativeAd.setAdListener(new AdListener) {
    @Override
    public void onError(NativeAd ad, AdError error) {}

    @Override
    public void OnAdClicked(NativeAd ad) {}

    @Override
    public void onAdLoaded(NativeAd ad) {}
  }
  nativeAd.loadAd();
}
```
  - 使用回傳的廣告參數來創建客制化廣告呈現
``` android
@Override
private void onAdLoaded(NativeAd ad) {
  // 步驟二 : 創建客制化廣告呈現
  String titleForAd = nativeAd.getAdTitle();
  NativeAd.Image iconForAd = nativeAd.getAdIcon();
  String titleForCallToAction = nativeAd.getAdCallToAction();
  String textForAd = nativeAd.getAdBody();

  // 利用原生廣告建立客製化版面 例如：
  // (1) 產生廣告元件
  LinearLayout nativeAdContainer = new LinearLayout(this);
  TextView titleLabel = new TextView(this);
  titleLabel.setText(titleForAd);

  // (2) 銷毀之前的MediaView
  if (mediaView != null) {
    mediaView.destroy();
    mediaView = null;
  }
			
  // (3) 建立MediaView
  mediaView = new MediaView(this);
  mediaView.setNativeAd(nativeAd);
  mediaView.setAutoplay(true);
      
  nativeAdContainer.addView(titleLabel);
  nativeAdContainer.addView(mediaView);
      
  // (4) 制定原生廣告版面
  // ...
  // ...
      
  // (5) 將廣告元件加入至頁面佈局裡
  LinearLayout mainContainer = (LinearLayout) findViewById(R.id.MainContainer);
  mainContainer.addView(nativeAdContainer);
}
```
  - 註冊可互動廣告子元件
  
``` android

@Override
public void onAdLoaded(NativeAd ad) {
  if (ad != nativeAd) { 
    return; 
  }
      
  // 步驟二 : 創建客制化廣告呈現
  // ...

  // 步驟三 : 註冊可互動廣告子元件
  nativeAd.registerViewForInteraction(nativeAdContainer);
}

```

  - 控制原生廣告播放
``` java
@Override
public void onPause() {
  // 其他應用程式邏輯
	
  // 暫停播放廣告內容
  if (mediaView != null) {
    mediaView.stop();
  }
}
  
@Override
public void onResume() {
  // 其他應用程式邏輯
	
  // 自動播放廣告內容
  if (mediaView != null) {
    mediaView.play();
  }
}
```

  - 清除廣告資源
``` android
@Override
public void onDestroy() {
  if (mediaView != null) {
    mediaView.destroy();
    mediaView = null;
  }
}
```  
