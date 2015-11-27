### 廣告特性

- 支援圖片與視頻

- 視頻廣告預設為靜音播放

- APP可取得廣告標題與描述，創建客製化廣告呈現

### 廣告要求方式

- 實例化`NativeAd`類別，並帶入廣告版位名稱

```java
  NativeAd mNativeAd = new NativeAd(mActivity, 廣告版位名稱);
```

- 宣告`MediaView`類別

```java
  private MediaView mMediaView = null;
```

- 設定`AdListener`回調
```java
    mNativeAd.setAdListener(new AdListener() {
      
      @Override
      public void onError(Ad ad, AdError error) {
        //  當下無可投放的廣告
        //  或其他錯誤
        //
      }

      @Override
      public void onAdLoaded(Ad ad) {

        if(mNativeAd != ad) {
          return;
        }

        //   取得廣告的標題
        //
        String title = mNativeAd.getAdTitle()

        //  取得廣告描述
        //
        String adBody = mNativeAd.getAdBody();

        //  取得廣告點擊說明文字
        //
        String callToAction = mNativeAd.getAdCallToAction();

        //  實例化MediaView
        //
        mMediaView = new MediaView(this);
        mMediaView.setNativeAd(mNativeAd);

        //  將標題、描述、點擊說明文字與MediaView
        //  加載至UI佈局裡
        ...
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

### 廣告控制方式

- 播放廣告
    - 請在APP在前景，且廣告進入螢幕可視範圍後呼叫
```java
    if (mMediaView != null) {
      mMediaView.play();
    }
``` 

- 暫停廣告
    - 請在`onPause()`,或是廣告移出螢幕後呼叫
```java
    if (mMediaView != null) {
      mMediaView.stop();
    }
```

- 釋放廣告資源

```java
  @Override
  protected void onDestroy() {
    if(mMediaView != null) {
      mMediaView.destroy();
      mMediaView = null;
    }

    //...
    //...

    super.onDestroy();
  }

``` 

### 進階整合

- 若廣告在onAdLoad()時，希望直接播放，請在實例化MediaView後，設定setAutoPlay()
```java
  mMediaView.setAutoplay(true);
``` 
### 版位整合範例

- [原生廣告](./native-ad-integration.md)