### 廣告特性

- 廣告寬高佔據螢幕全版面，用戶需與其互動或關閉廣告，方可回到 App 頁面

- 支援直式與橫式

- 支援圖片與視頻

- 視頻廣告預設為靜音播放，待點擊後可開啟聲音

- [效果預覽](http://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/globe_slideup.html)

### 廣告要求方式

- 實例化 `InterstitialAd` 類別，並帶入廣告版位名稱，如 `OPEN_SPLASH`

```java
  InterstitialAd mInterstitialAd = new InterstitialAd(mActivity, "OPEN_SPLASH");
```

- 設定 `InterstitialAdListener` 回調

```java
      mInterstitialAd.setAdListener(new InterstitialAdListener() {

        @Override
        public void onError(Ad ad, AdError error) {
          //  當下無可投放的廣告
          //  或其他錯誤
          //
        }

        @Override
        public void onAdLoaded(Ad ad) {
          //  當廣告讀取完成後，可在此回調裡呼叫 show()
          //  啟動蓋屏廣告的 Activity。
          //  開啟方式有兩種:
          //    1.系統預設Activity轉場效果
          //        show()
          //    2.自訂Activity轉場效果
          //        show(進場動畫的res Id, 離場動畫的res Id)
          //
          mInterstitialAd.show(
              R.anim.slide_in_from_bottom, 
              R.anim.no_animation);
        }

        @Override
        public void onInterstitialDisplayed(Ad ad) {
          //  蓋屏廣告展示成功
          //
        }

        @Override
        public void onInterstitialDismissed(Ad ad) {
          //  蓋屏廣告已被關閉
          //  其呼叫時機有
          //    1.用戶點擊關閉按鈕
          //    2.用戶點擊退回按鈕(onBackpress())
          //    3.後台設定自動關閉
          //
          //  釋放蓋屏廣告
          //
          if(mInterstitialAd != null) {
            mInterstitialAd.destroy();
          }
          
          //  APP可在此時機進入主頁面
          //
          ...
          ...
        }

        @Override
        public void onAdClicked(Ad ad) {
          //  用戶點擊廣告
          //
        }

        @Override
        public void onAdImpression(Ad ad) {
          //  廣告曝光
          //
        }

        @Override
        public void onAdMute(Ad ad) {
          //  若廣告為視頻廣告時，SDK可回傳靜音事件
          //
        }

        @Override
        public void onAdUnmute(Ad ad) {
          //  若廣告為視頻廣告時，SDK可回傳開啟聲音事件
          //
        }

        @Override
        public void onVideoStart(Ad ad) {
          //  若廣告為視頻廣告時，SDK可回傳視頻啟動事件
          //
        }

        @Override
        public void onVideoProgress(Ad ad, int totoalDuration, int currentPosition) {
          //  若廣告為視頻廣告時，SDK可回傳視頻進行事件
          //
        }

        @Override
        public void onVideoEnd(Ad ad) {
          //  若廣告為視頻廣告時，SDK可回傳視頻結束事件
          //
        }
        
      });
```

- 向 SDK 請求廣告
    - 當呼叫 loadAd() 之後，SDK 會以線程阻塞的方式 (blocking call)，直接呼叫廣告回調，App 可直接得知廣告是 onAdLoaded() 或是 onError()
    - 此時 SDK 會直接讀取已預載好的廣告，並無任何網路行為

```java
    mInterstitialAd.loadAd();
```

### 廣告控制方式

- 釋放廣告資源

```java
  @Override
  protected void onDestroy() {
    if(mInterstitialAd != null) {
      mInterstitialAd.destroy();
      mInterstitialAd = null;
    }

    //...
    //...

    super.onDestroy();
  }

```

- 橫式廣告處理
    - 當 App 向 SDK 要求到橫式廣告後，因畫面轉向，會讓 Activity 被重新實例，執行 onCreate() 流程。此時 App 若不記住曾經要求廣告的狀態，會造成橫式廣告開啟後，App 又馬上向 SDK 要求一次廣告
    - 解決方式有兩種
        - 在 AndroidManifest.xml 設定該 Activity 參數 `android:configChanges="orientation|screenSize"`，避免 Activity 被重新實例

        - 在 App 內記住要求狀態，避免同時要求廣告兩次
            - [參考範例](./interstitial-ad-integration.md)



### 版位整合範例

- [開機蓋屏](./interstitial-ad-integration.md)
