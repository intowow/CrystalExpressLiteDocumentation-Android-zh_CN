### 引用 SDK  函式庫
``` java
import com.intowow.sdk.*;
```

### 初始化 SDK
- (**正常模式**) : 在 App 起始 Activity 的 onCreate 函數中調用 I2WSDK.init(Context) API。
``` java
@Override
public void onCreate() {
  // ... 其他App邏輯
  
  I2WSDK.init(this);
}
```

- (**測試模式**) : 在 App 起始 Activity 的 onCreate 函數中調用 I2WSDK.init(Context, true) API。
``` java
@Override
public void onCreate() {
  // ... 其他App邏輯
  
  I2WSDK.init(this, true);
}
```

### 回報 Activity 生命週期
- 在 App 所有 Activity 的 onResume 函數中調用 I2WSDK.onActivityResume(Activity) API。
``` java
@Override
public void onResume() {
  // ... 其他App邏輯
  
  I2WSDK.onActivityResume(this);
}
```

- 在 App 所有 Activity 的 onPause 函數中調用 I2WSDK.onActivityPause(Activity) API。
``` java
@Override
public void onPause() {
  // ... 其他App邏輯
  
  I2WSDK.onActivityPause(this);
}
```
