### 整合步驟
  - 請求一個原生廣告
  - 使用回傳的廣告參數來創建客制化廣告呈現
  - 註冊可互動廣告子元件
  
``` android
private NativeAd nativeAd;
private void showNativeAd() {
    nativeAd = new NativeAd(this, “YOUR_PLACEMENT_NAME”);
    nativeAd.setAdListener(new AdListener() {
        @Override
        public void onError(NativeAd ad, AdError error) {}
        @Override
        public void OnAdClicked(NativeAd ad) { }

        @Override
        public void onAdLoaded(NativeAd ad) {
            if (ad !== nativeAd) { 
                return; 
            }
      
			// 步驟二 : 創建客制化廣告呈現
            String titleForAd = nativeAd.getAdTitle();
            NativeAd.Image iconForAd = nativeAd.getAdIcon();
            String titleForCallToAction = nativeAd.getAdCallToAction();
            String textForAd = nativeAd.getAdBody();

            // Create you custom view in a ad view. For example :
            LinearLayout nativeAdContainer = new LinearLayout(this);
            TextView titleLabel = new TextView(this);
            titleLabel.setText(titleForAd);

            NativeAd.MediaView mediaView = new MediaView(this);
            mediaView.setNativeAd(nativeAd);
            mediaView.setAutoplay(true);
      
            nativeAdContainer.addView(titleLabel);
            nativeAdContainer.addView(mediaView);
      
            // … Layout your own native ad components
      
            // Add Ad to your layout
            LinearLayout mainContainer = (LinearLayout) findViewById(R.id.MainContainer);
            mainContainer.addView(nativeAdContainer);

            // 步驟三 : 註冊可互動廣告子元件
            List<View> clickableList = new ArrayList<View>();
            clickableList.add(callToActionButton);

            nativeAd.registerViewForInteraction(nativeAdContainer, clickableList);
        }
    });
	
	// 步驟一 : 請求原生廣告
    nativeAd.loadAd();
}

```