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

### NativeAd.AdListener

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