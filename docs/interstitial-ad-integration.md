<h3 id='opensplash' style='color:red'>開機蓋屏</h3>

- 開機蓋屏廣告指進入應用程式時，所出現的蓋屏廣告。
- 出現時機為首次啟動應用程式(`launch flow`)

<img style="display:block; margin:auto;" src="https://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/img/splash2-demo.png" alt="splash demo" width="250">

<a target="_blank" href="http://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/globe_slideup.html">效果預覽</a>

---------------------------------------


<h4 id='opensplash-1' style='color:green'>整合步驟</h4>

<span style='font-weight: bold;color:red'>
註:
</span>
<br/>
<span style='font-weight: bold;color:red'>
整合前請先移除手機上的Demo App，一支手機上不可有相同的crystal id。
</span>
<br/>
<span style='font-weight: bold;color:red'>
若整合後看不到廣告，請參考<a target="_blank" href="../faq">問題集</a>
</span>
<br/>

<h3 id='opensplash-launch' style='color:blue'>1.  修改起始流程</h3>

<p/>

- 請參考範例APP，讓起始Activity繼承BaseActivity，BaseActivity內已處理SDK初始化大部分的邏輯<p/>
<p/>

- 為了讓廣告有轉場效果，可下載[slide_in_from_bottom.xml][slide_in_from_bottom]與[no_animation.xml][no_animation]，複製到應用程式的res/anim/目錄底下

<p/>

<p/>

- Activity宣告成員變數

```java
  private final static String KEY_HAS_INTERSTITIAL_AD = "KEY_HAS_INTERSTITIAL_AD";
  protected InterstitialAd mInterstitialAd = null;
  private boolean mHasInterstitialAd = false;
  private boolean mIsFinishInterstitialAd = false;
```

- 向SDK請求廣告

```java
      //  若主流程已呼叫過廣告，就不再向SDK請求廣告。
      //
      //  當開機廣告是橫式廣告時，APP的activity會因為轉向而重新執行onCreate()
      //  若不特別宣告旗標來紀錄要求廣告的狀態，
      //  會導致橫式廣告出現後，直接又再向SDK請求一次廣告。
      //
      //  此旗標需在onSaveInstanceState(Bundle)裡儲存起來
      //
      if(hasRequestedInterstitialAd()) {
        return;
      }

      //  實例化開機蓋屏，並帶入廣告版位"OPEN_SPLASH"
      //
      mInterstitialAd = new InterstitialAd(InterstitialAdActivity.this, "OPEN_SPLASH");
      
      //  若要設定點擊開機蓋屏，開啟網頁後，同時關閉開機蓋屏，
      //  可呼叫API setAutoCloseWhenEngaged(true)
      //
      //  mInterstitialAd.setAutoCloseWhenEngaged(true);
      
      //  設定回調
      //
      mInterstitialAd.setAdListener(new InterstitialAdListener() {

        @Override
        public void onError(Ad ad, AdError error) {
          //  當下無可投放的廣告
          //  或其他錯誤
          //

          //  釋放mInterstitialAd
          //
          onInterstitialAdFinish();
        }

        @Override
        public void onAdLoaded(Ad ad) {
          //  當廣告讀取完成後，可在此回調裡呼叫show()
          //  啟動開機蓋屏的Activity。
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
          //  開機蓋屏展示成功
          //
        }

        @Override
        public void onInterstitialDismissed(Ad ad) {
          //  開機蓋屏已被關閉
          //  其呼叫時機有
          //    1.用戶點擊關閉按鈕
          //    2.用戶點擊退回按鈕(onBackpress())
          //    3.後台設定自動關閉
          //
          //  釋放mInterstitialAd
          //
          onInterstitialAdFinish();
          
          //  APP可在此時機進入主頁面
          //
          ...
          ...
        }

        @Override
        public void onAdClicked(Ad ad) {
          //  用戶點擊開機蓋屏
          //
        }
        
      });
      
      //  向SDK請求廣告
      //  當呼叫loadAd()之後，
      //  SDK會以線程阻塞的方式(blocking call)
      //  直接呼叫廣告回調，APP可直接得知廣告是
      //  onAdLoaded()或是onError()。
      //  此時SDK會直接讀取已預載好的廣告
      //  並無任何網路行為
      //
      mInterstitialAd.loadAd();
```
<p/>

<span style='font-weight: bold;color:red'>
註:
</span>
<br/>
<span style='font-weight: bold;color:red'>
1.呼叫mInterstitialAd.loadAd()的時機點，請在用戶看到應用程式LOGO之後
</span>
<br/>
<span style='font-weight: bold;color:red'>
2.建議讓LOGO等待約1秒再開啟廣告，以達較佳用戶體驗，
效果如下
</span>
<br/><br/>
<a target="_blank" href="http://s3.cn-north-1.amazonaws.com.cn/intowow-common/preview/globe_slideup.html">效果預覽</a>

- 宣告控制廣告狀態的方法

```java
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    //...
    //...
    //...
    
    //  當開機廣告是橫式廣告時，APP的activity會因為轉向而重新執行onCreate()
    //  若不特別宣告旗標來紀錄要求廣告的狀態，
    //  會導致橫式廣告出現後，直接又再向SDK請求一次廣告。
    if(savedInstanceState != null) {
      if(savedInstanceState.containsKey(KEY_HAS_INTERSTITIAL_AD)) {
        mHasInterstitialAd = savedInstanceState.getBoolean(KEY_HAS_INTERSTITIAL_AD);
        savedInstanceState.remove(KEY_HAS_INTERSTITIAL_AD);
      }
    }
    
  }
  @Override
  protected void onSaveInstanceState(Bundle outState) {
    //  儲存要求廣告的狀態
    //
    outState.putBoolean(KEY_HAS_INTERSTITIAL_AD, mInterstitialAd != null);
    super.onSaveInstanceState(outState);
  }
  
  /**
  *
  * 查詢Activity是否曾經向SDK要求廣告
  */
  private boolean hasRequestedInterstitialAd() {
    return mHasInterstitialAd;
  }

  /**
  *
  * 釋放廣告資源
  */
  private void onInterstitialAdFinish() {
    mIsFinishInterstitialAd = true;
    releaseInterstitialAd();
  }

  /**
  *
  * 釋放廣告資源
  */
  private void releaseInterstitialAd() {
    if(mIsFinishInterstitialAd) {
      
      if(mInterstitialAd != null) {
        mInterstitialAd.destroy();
        mInterstitialAd = null;
      }
      
      mIsFinishInterstitialAd = false;
      mHasInterstitialAd = false;
    }
  }
```

 
- 在onDestroy()釋放廣告
<br/>

```java
@Override
protected void onDestroy() {
  releaseSplashAd();

  //...
  //...

  super.onDestroy();
}
```
<p/>

---------------------------------------

<span style='font-weight: bold;color:red'>
註:
</span>
<br/>
<span style='font-weight: bold;color:red'>
1.頁面轉場效果只支援直式廣告
</span>
<br/>
<span style='font-weight: bold;color:red'>
2.可自行使用res/anim/底下的xml來客製
</span>
<br/>
<span style='font-weight: bold;color:red'>
3.範例APP的res/anim也提供了阻尼特效，可供應用程式參考使用
</span>
<br/>
<span style='font-weight: bold;color:red'>
    res/anim/damping_in.xml
</span>
<br/>
<span style='font-weight: bold;color:red'>
    res/anim/damping_out.xml
</span>
<p/>


[slide_in_from_bottom]:https://github.com/ddad-daniel/CrystalExpressSDK-CN-Demo/blob/master/res/anim/slide_in_from_bottom.xml
[no_animation]:https://github.com/ddad-daniel/CrystalExpressSDK-CN-Demo/blob/master/res/anim/no_animation.xml