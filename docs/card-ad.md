### 廣告特性

- 支援圖片與視頻

- 視頻廣告預設為靜音播放

- [效果預覽](http://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/STREAM_VIDEO_BRANDCARD.html?video=http://s3.cn-north-1.amazonaws.com.cn/intowow-common/demo/video/Stream-Video-BrandCard.mp4?icon=http://s3.cn-north-1.amazonaws.com.cn/intowow-common/demo/img/Stream-Video-BrandCard.png)

### 廣告要求方式

- 實例化`DisplayAd`類別，並帶入廣告版位名稱

```java
  DisplayAd mDisplayAd = new DisplayAd(mActivity, 廣告版位名稱);
```

- 設定`AdListener`回調
```java
    mDisplayAd.setAdListener(new AdListener() {
      
      @Override
      public void onError(Ad ad, AdError error) {
        //  當下無可投放的廣告
        //  或其他錯誤
        //
      }

      @Override
      public void onAdLoaded(Ad ad) {

        if(mDisplayAd != ad) {
          return;
        }

        //  當廣告讀取完成後，可呼叫mDisplayAd.getView()取得廣告
        //
        View adView = mDisplayAd.getView();
        if(adView != null) { 
          
          //  將adView加載至UI佈局裡
          //
          ...
          ...
          ...

          
          //  若APP在前景，且廣告在螢幕可視範圍內
          //  可呼叫mDisplayAd.play();啟動廣告
          //
          if(advisable) {
            mDisplayAd.play();
          }
          
        }
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

### 廣告控制方式

- 播放廣告
    - 請在APP在前景，且廣告在螢幕可視範圍內呼叫
```java
  mDisplayAd.play();
``` 

- 暫停廣告
    - 請在`onPause()`,或是廣告移出螢幕後呼叫
```java
  mDisplayAd.stop();
```

- 釋放廣告資源

```java
  @Override
  protected void onDestroy() {
    if(mDisplayAd != null) {
      mDisplayAd.destroy();
      mDisplayAd = null;
    }

    //...
    //...

    super.onDestroy();
  }

``` 

### 進階整合

- 若廣告在onAdLoad()內，載入UI佈局後，希望直接播放，請在呼叫loadAd()之前，設定setAutoPlay()
```java
  mDisplayAd.setAutoplay(true);

  ...
  ...
  ...

  mDisplayAd.loadAd();
``` 
- 若需要縮放廣告寬高，請在呼叫loadAd()之前，設定setWidth()
    - 設定寬度之後，SDK會自動調整廣告的寬高比
```java
  mDisplayAd.setWidth(int 廣告寬度);

  ...
  ...
  ...

  mDisplayAd.loadAd();
``` 


### 版位整合範例

- [內文廣告](./card-ad-integration.md)