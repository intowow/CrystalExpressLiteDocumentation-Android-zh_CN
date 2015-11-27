### 廣告特性

- 廣告寬高佔據螢幕全版面，用戶需與其互動或關閉廣告，方可回到APP頁面

- 支援直式與橫式

- 支援圖片與視頻

- 視頻廣告預設為靜音播放

- [效果預覽](http://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/globe_slideup.html)

### 廣告要求方式

- 實例化`InterstitialAd`類別，並帶入廣告版位名稱，如`OPEN_SPLASH`

```java
  InterstitialAd mInterstitialAd = new InterstitialAd(mActivity, "OPEN_SPLASH");
```

- 設定`InterstitialAdListener`回調

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
          //  當廣告讀取完成後，可在此回調裡呼叫show()
          //  啟動蓋屏廣告的Activity。
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
        
      });
```

- 向SDK請求廣告
    - 當呼叫loadAd()之後，SDK會以線程阻塞的方式(blocking call)，直接呼叫廣告回調，APP可直接得知廣告是onAdLoaded()或是onError()
    - 此時SDK會直接讀取已預載好的廣告，並無任何網路行為

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

- `橫式廣告處理`
    - 當APP向SDK要求到橫式廣告後，因畫面轉向，會讓Activity被重新實例，執行onCreate流程。此時APP若不記住曾經要求廣告的狀態，會造成橫式廣告開啟後，APP又馬上向SDK要求一次廣告
    - 解決方式有兩種
        - 在AndroidManifest.xml設定該Activity參數`android:configChanges="orientation|screenSize"`，避免Activity被重新實例

        - 在APP內記住要求狀態，避免同時要求廣告兩次
            - [參考範例](./interstitial-ad-integration.md)



### 版位整合範例

- [開機蓋屏](./interstitial-ad-integration.md)