### 整合重點

- 內文廣告指文章內所加入的廣告
- 為了在適當時機向SDK要求與啟動內文廣告，應用程式可加上範例程式所提供的`CrystalExpressScrollView`類別
- `CrystalExpressScrollView`類別可設定`ScrollViewListener`，
當滑動頁面時，會發出`onScrollChanged`回調，我們可在此回調判斷廣告位置，進一步向SDK要求與啟動廣告
- 考量到一般內文的操作特性，是由上往下閱讀，本範例以`ScrollView`為主，若您使用的是`WebView`，可調整應用程式的布局xml檔，將`WebView`包入`ScrollView`，如下示意
```xml
  <CrystalExpressScrollView>
    <ViewGroup>
      <WebView/>
      <ContentAd/>
    <ViewGroup/>
  <CrystalExpressScrollView/>
```

- `ScrollView`布局排列方式，可參考範例程式`activity_display.xml`

- 整合時可參考範例程式`DisplayActivity.java`

### 整合步驟

- 加入`CrystalExpressScrollView.java`至代碼裡


- 宣告變數
```java
  /**客製化scroll view, 可監聽滑動事件*/
  private CrystalExpressScrollView mScrollView = null;
  /**卡片廣告類別*/
  private DisplayAd mDisplayAd = null;
  /**定義於XML佈局裡，可載入卡片廣告*/
  private RelativeLayout mDisplayAdLayout = null;
```

- 初始化UI
```java
    mScrollView = (CrystalExpressScrollView) findViewById(R.id.scrollview);
    mDisplayAdLayout = (RelativeLayout) findViewById(R.id.displayad);

    mScrollView.setScrollViewListener(new ScrollViewListener() {

      @Override
      public void onScrollChanged(CrystalExpressScrollView scrollView, int x,
          int y, int oldX, int oldY) {
        //  檢查廣告是否在螢幕內，執行mDisplayAd.play();或mDisplayAd.stop();
        //
        ...
        ...
        ...
      }

      @Override
      public void onScrollViewIdle() {
      }
  });
```
檢查廣告是否在螢幕內的實作，可參考範例程式`DisplayActivity.java`

- 實例化DisplayAd類別
```java
  mDisplayAd = new DisplayAd(this, 廣告版位名稱);
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

- 控制廣告播放
``` java
@Override
public void onPause() {
  // 其他應用程式邏輯
	
  // 暫停播放廣告內容
  if (mDisplayAd != null) {
    mDisplayAd.stop();
  }
}
  
@Override
public void onResume() {
  // 其他應用程式邏輯
	
  // 若廣告在螢幕可視範圍內
  // 自動播放廣告內容
  if (mDisplayAd != null && adVisable()) {
    mDisplayAd.play();
  }
}
```

  - 清除廣告資源
``` android
@Override
public void onDestroy() {
  if (mDisplayAd != null) {
    mDisplayAd.destroy();
    mDisplayAd = null;
  }

  super.onDestroy();
}
```  
