### 引用 SDK  函式庫
``` java
import com.intowow.sdk.*;
```

### 初始化 SDK

- APP需呼叫3個API來初始SDKI2WAPI
    - I2WAPI.init(Context);
    - I2WAPI.onActivityResume(Context);
    - I2WAPI.onActivityPause(Context);

<p/>

- I2WAPI.init
    - 此API啟動SDK主程式
    - 若要特別使用測試廣告，可呼叫I2WAPI.init(Context, true);
    - `APP發佈前，請確認使用I2WAPI.init(Context);而非I2WAPI.init(Context, true);`

<p/>

- I2WAPI.onActivityResume與I2WAPI.onActivityPause
    - 功能:
        - 回報SDK目前APP處在前景或背景
    - 目的:
        - SDK為了使用正確的廣告預載策略，需要知道當下APP處在前景或背景
        - 當APP在前景時，SDK的預載策略就會優先抓取用戶瀏覽的廣告版位
        - 當APP在背景時，SDK的預載策略就會調整為只在WIFY環境下載
    - 此API在SDK內單純只切換旗標，若有狀態切換，SDK會使用另外一個線程處理，`不會占用主線程任何時間與資源`

---------------------------------------

- APP可選擇三種方式初始化SDK
    1. 使用範例程式的BaseApplication.java (需只支援Android 4.0以上)
    2. 使用範例程式的BaseActivity.java
    3. 設定每一隻Activity.java
- `若整合上有遇到困難，可隨時聯絡intowow窗口討論解決辦法`

方式1. 使用範例程式的BaseApplication.java

- 若APP本身可支援4.0之前的手機，請跳過此步驟，參考方式2或方式3

- 初始SDK
``` java
  @Override
  public void onCreate() {
    super.onCreate();

    //...
    //...
    
    //  要求正式廣告
    //
    I2WAPI.init(getApplicationContext());

    //  或要求測試廣告(發佈前請改用正式廣告)
    //
    //  I2WAPI.init(getApplicationContext(), true);
  }
```
- Android自4.0開始，提供了ActivityLifecycle回調，APP可在此回調內，回報APP狀態給SDK
``` java
    if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.ICE_CREAM_SANDWICH) {
      mInstance.registerActivityLifecycleCallbacks(new ActivityLifecycleCallbacks() {

        @Override
        public void onActivityCreated(Activity activity,
            Bundle savedInstanceState) {
        }

        @Override
        public void onActivityStarted(Activity activity) {
        }

        @Override
        public void onActivityResumed(Activity activity) {
          //  回報SDK Activity為Resume狀態
          //
          I2WAPI.onActivityResume(activity);
        }

        @Override
        public void onActivityPaused(Activity activity) {
          //  回報SDK Activity為Pause狀態
          //
          I2WAPI.onActivityPause(activity);
        }

        @Override
        public void onActivityStopped(Activity activity) {
        }

        @Override
        public void onActivitySaveInstanceState(Activity activity,
            Bundle outState) {
        }

        @Override
        public void onActivityDestroyed(Activity activity) {
        }});
    }
```

- activity內調用
```java
  getApplicationContext();
```

<p/>

方式2. 使用範例程式的BaseActivity.java

- 可參考範例程式的BaseActivity.java，讓所有的Activity繼承
- BaseActivity.java內已處理SDK init與其他回報APP狀態給SDK的所有邏輯
- 若APP本身已有類似BaseActivity.java，可讓其實作範例程式BaseActivity.java的邏輯，或是直接讓其繼承BaseActivity.java
- 若此部分整合有難度，可再考慮方式3


方式3. 設定每一隻Activity.java

- `若整合上有遇到困難，可隨時聯絡intowow窗口討論解決辦法`

- 在 App 起始 Activity 的 onCreate 函數中調用 I2WAPI.init(Context) API。
``` java
  //  要求正式廣告
  //
  I2WAPI.init(this);
```

- 若想使用測試廣告，可改為
``` java
  //  要求測試廣告(發佈前請改用正式廣告)
  //
  I2WAPI.init(this, true);
```
- 在 App 所有 Activity 的 onResume 函數中調用 I2WAPI.onActivityResume(Activity) API。
``` java
@Override
public void onResume() {
  // ... 其他App邏輯
  
  I2WAPI.onActivityResume(this);
}
```

- 在 App 所有 Activity 的 onPause 函數中調用 I2WAPI.onActivityPause(Activity) API。
``` java
@Override
public void onPause() {
  // ... 其他App邏輯
  
  I2WAPI.onActivityPause(this);
}
```
