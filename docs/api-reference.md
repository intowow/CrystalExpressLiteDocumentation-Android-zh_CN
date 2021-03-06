### I2WAPI

The interface for initializing CrystalExpress SDK and handle activity life-cycle callbacks.

*** Class Methods ***
```
/**
 * Initialize SDK.
 *
 * @param context Android context
 */
void init (Context context)
```

```
/**
 * Initialize SDK.
 * 
 * @param context Android context
 * @param isTestMode Set to true if you want to initialize SDK
 *        in test mode. Test mode means the SDK can only fetch
 *        the ads marked as test mode.
 */
void init (Context context, boolean isTestMode)
```

```
/**
 * Call this method when Activity.onResume is called to report activity status.
 * 
 * @param context Android context
 */
void onActivityResume(Context context)
```

```
/**
 * Call this method when Activity.onPause is called to report activity status.
 * 
 * @param context Android context
 */
void onActivityPause(Context context)
```

-------------------------------

### NativeAd

NativeAd provides ad creatives for apps to render in your own custom layout.

*** Constructor ***
```
/**
 * Constructs a NativeAd using the given context and placement.
 *
 * @param context Android context
 * @param placement Placement name
 */
NativeAd (Context context, String placement)
```

*** Class Methods ***

```
/**
 * Downloads the given image and display it in the given imageView. 
 * Note that this method will always return immediately (Image has 
 * been downloaded asynchronously).
 *
 * @param image Image creative for this NativeAd
 * @param imageView Image view to display this image
 */
void downloadAndDisplayImage (Image image, ImageView imageView)
```

*** Instance Methods ***

```
 /**
  * Sets ad event callback listener.
  *
  * @param listener Ad event callback listener
  */
void setAdListener (AdListener listener)
```

```
 /**
  * Loads an ad.
  */
void loadAd()
```

```
 /**
  * Loads an ad.
  * @param timeout request timeout in millisecond, if timeout is zero, we will use blocking call in the main thread
  */
void loadAd (long timeout)
```

```
 /**
  * Registers the given view as the container for the NativeAd 
  * to handle impressions and clicks. Applies a click handler 
  * to the entire unit.
  *
  * @param view View containing the NativeAd for display
  */
void registerViewForInteraction (View view)
```

```
 /**
  * Registers the given view as the container for the NativeAd to 
  * handle impressions and clicks. Applies a click handler to all 
  * views provided in clickableViews.
  *
  * @param view View containing the NativeAd for display
  * @param clickableViews A list of view elements that would tap on this unit
  */
void registerViewForInteraction (View view, List clickableViews)
```

```
 /**
  * Unregisters interaction set previously.
  */
void unregisterView ()
```

```
 /**
  * @return The ad title.
  */
String getAdTitle ()
```

```
 /**
  * @return The ad icon.
  */
Image getAdIcon ()
```

```
 /**
  * @return The call to action phrase.
  */
String getAdCallToAction ()
```

```
 /**
  * @return The body, usually a description of the ad.
  */
String getAdBody ()
```

```
 /**
  * @retrn Returns true if this NativeAd contains video content.
  */
boolean hasVideoContent ()
```

-------------------------------

### NativeAd.AdListener (Deprecated)

The AdListener interface is notified of events in the ad control life-cycle.

*** Instance Methods ***

```
 /**
  * Called when an error happened while the ad control is attempting to load an ad.
  * 
  * @param ad The native ad control
  * @param error Error
  */
void onError (NativeAd ad, AdError error)
```

```
 /**
  * Called when the ad control has loaded an ad
  *
  * @param ad The native ad control
  */
void onAdLoaded (NativeAd ad)
```

```
 /**
  * Called when the ad control is clicked and user is 
  * redirected to the link in the ad.
  *
  * @param ad The native ad control
  */
void onAdClicked (NativeAd ad)
```

-------------------------------

### NativeAd.FullScreenMode

Enumeration for full screen modes.

*** Constants ***

  - NONE
  - RIGHT_SIDE_UP
  - LEFT_SIDE_UP
  
-------------------------------
  
### NativeAd.Image

Stores the image creative metadata.

*** Instance Methods ***

```
 /**
  * @return The url of the image.
  */
String getUrl ()
```

```
 /**
  * @return The width of the image.
  */
int getWidth ()
```

```
 /**
  * @return The height of the image.
  */
int getHeight ()
```

-------------------------------

### NativeAd.MediaView

MediaView displays native ad media content and can be declared and added to view.

*** Constructor ***

```
 /**
  * Constructs a MediaView using the giving context.
  *
  * @param context Android context
  */
MediaView (Context context)
```

*** Instance Methods ***

```
 /**
  * Destroys the media view.
  */
void destroy ()
```

```
 /**
  * Sets native ad for displaying
  *
  * @param ad The native ad for displaying
  */
void setNativeAd (NativeAd ad)
```

```
 /**
  * Sets auto play flag for media view
  *
  * @param autoplay Auto play flag for media view
  */
void setAutoplay (boolean autoplay)
```

```
 /**
  * Plays the creative of media view.
  */
void play ()
```

```
 /**
  * Stops the creative of media view.
  */
void stop ()
```

```
 /**
  * Mutes the creative of media view.
  */
void mute ()
```

```
 /**
  * Unmutes the creative of media view.
  */
void unmute ()
```

```
 /**
  * @return True if media view is in full screen mode; false otherwise.
  */
boolean isFullScreen ()
```

```
 /**
  * Changes the media view to the given full screen mode.
  *
  * @param mode Full screen mode
  */
void setFullScreenMode (FullScreenMode mode)
```

-------------------------------

### InterstitialAd

An interstitial ad is a full screen ad that you can show in your app.

*** Constructor ***
```
/**
 * Constructs a InterstitialAd using the given context and placement.
 *
 * @param context Android context
 * @param placement Placement name
 */
InterstitialAd (Context context, String placement)
```

*** Instance Methods ***

```
 /**
  * Sets ad event callback listener.
  *
  * @param listener Interstitial Ad event callback listener
  */
void setAdListener (InterstitialAdListener listener)
```

```
 /**
  * Loads an ad.
  */
void loadAd ()
```

```
 /**
  * Loads an ad.
  * @param timeout request timeout in millisecond, if timeout is zero, we will use blocking call in the main thread
  */
void loadAd (long timeout)
```

```
 /**
  * If your interstitial ad has been loaded successfully, 
  * then you can call this method to pop-up the intersitital ad
  */
void show ()
```

```
 /**
  * If your interstitial ad has been loaded successfully, you can call this method
  * to show the interstitial ad.
  * 
  * the overridePendingTransition is only support single-offer and portrait
  * ad
  * 
  * @param enterAnim A resource ID of the animation resource to use for the incoming activity. Use 0 for no animation.
  * @param exitAnim A resource ID of the animation resource to use for the outgoing activity. Use 0 for no animation.
  **/
void show (int enterAnim, int exitAnim)
```

```
 /**
  * Sets interstitial ad auto close after engaged
  * @param isAutoClose 
  */
void setAutoCloseWhenEngaged (boolean isAutoClose)
```

```
 /**
  * Destroy and release memory
  */
void void destroy ()
```

```
 /**
  * To close the interstitial ad directly
  */
void close ()
```

```
 /**
  * @return The ad id.
  */
int getAdId ()
```

```
 /**
  * @return The engage url.
  */
String getEngageUrl ()
```

-------------------------------

### InterstitialAd.InterstitialAdListener

The InterstitialAdListener interface is notified of events in the ad control life-cycle.

*** Instance Methods ***

```
 /**
  * Called when an error happened while the ad control is attempting to load an ad.
  * 
  * @param ad The ad control
  * @param error Error
  */
void onError (Ad ad, AdError error)
```

```
 /**
  * Called when the ad control has loaded an ad
  *
  * @param ad The ad control
  */
void onAdLoaded (Ad ad)
```

```
 /**
  * Called when the ad control is clicked and user is 
  * redirected to the link in the ad.
  *
  * @param ad The ad control
  */
void onAdClicked (Ad ad)
```

```
 /**
  * Where relevant, use this function to pause your app's flow
  *
  * @param ad The ad control
  */
void onInterstitialDisplayed (Ad ad)
```

```
 /**
  * Use this function to resume your app's flow
  *
  * @param ad The ad control
  */
void onInterstitialDismissed (Ad ad)
```

```
 /**
  * Called when the ad control has impressioned an ad
  *
  * @param ad The ad control
  */
void onAdImpression (Ad ad)
```

```
 /**
  * Called when the ad control has muted an ad
  *
  * @param ad The ad control
  */
void onAdMute (Ad ad)
```

```
 /**
  * Called when the ad control has unmuted an ad
  *
  * @param ad The ad control
  */
void onAdUnmute (Ad ad)
```

```
 /**
  * Called when the video ad start
  *
  * @param ad The ad control
  */
void onVideoStart(Ad ad);
```

```
 /**
  * Called when the video ad play complete
  *
  * @param ad The ad control
  */
void onVideoEnd(Ad ad);
```

```
 /**
  * Called when the video ad play in progress
  *
  * @param ad The ad control
  * @param totoalDuration The totoal duration of the video ad
  * @param currentPosition The current play position of the video ad
  */
void onVideoProgress(Ad ad, int totoalDuration, int currentPosition);
```

-------------------------------

### DisplayAd

An display ad is a card ad that you can show in your app. App has to control AD's behavior.

*** Constructor ***
```
/**
* Constructs a DisplayAd using the given context and placement.
*
* @param context Android context
* @param placement Placement name
*/
DisplayAd (Context context, String placement)
```

*** Instance Methods ***

```
/**
* Sets ad event callback listener.
*
* @param listener Ad event callback listener
*/
void setAdListener (AdListener listener)
```

```
/**
* Loads an ad.
*/
void loadAd ()
```

```
/**
* Loads an ad.
* @param timeout request timeout in millisecond, if timeout is zero, we will use blocking call in the main thread
*/
void loadAd (long timeout)
```

```
/**
* If you has multi display ad that you can control the ad display order, 
* @param place display ad order
*/
void setPlace (int place)
```

```
/**
* Sets display ad view width. 
* SDK will adjust the ad view height when you set width.
* 
* @param width display ad width
**/
void setWidth (int width)
```

```
/**
* Gets display ad view.
*/
void getView ()
```

```
/**
* Enable video format display ad auto playback when ad view is showing on screen. 
* @param autoplay enable display ad view auto playback
*/
void void setAutoplay (boolean autoplay)
```

```
/**
* To play video format display ad.
*/
void play ()
```

```
/**
* To stop playback video format display ad.
*/
void stop ()
```

```
/**
* To control video format display ad volume mute.
*/
void mute ()
```

```
/**
* To control video format display ad volume unmute.
*/
void unmute ()
```

```
/**
* To check video format display ad volume mute.
*/
boolean isMute ()
```

```
/**
* Destroy and release memory
*/
void void destroy ()
```

```
/**
* @return The ad id.
*/
int getAdId ()
```

```
/**
* @return The engage url.
*/
String getEngageUrl ()
```
-------------------------------

### AdListener

The AdListener interface is notified of events in the ad control life-cycle.

*** Instance Methods ***

```
/**
* Called when an error happened while the ad control is attempting to load an ad.
* 
* @param ad The ad control
* @param error Error
*/
void onError (Ad ad, AdError error)
```

```
/**
* Called when the ad control has loaded an ad
*
* @param ad The ad control
*/
void onAdLoaded (Ad ad)
```

```
/**
* Called when the ad control is clicked and user is 
* redirected to the link in the ad.
*
* @param ad The ad control
*/
void onAdClicked (Ad ad)
```

```
/**
* Called when the ad control has impressioned an ad
*
* @param ad The ad control
*/
void onAdImpression (Ad ad)
```

```
/**
* Called when the ad control has muted an ad
*
* @param ad The ad control
*/
void onAdMute (Ad ad)
```

```
/**
* Called when the ad control has unmuted an ad
*
* @param ad The ad control
*/
void onAdUnmute (Ad ad)
```


