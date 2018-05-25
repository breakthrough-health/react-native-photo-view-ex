# react-native-photo-view-ex

Provides custom Image view for React Native that allows to perform pinch-to-zoom on images. Works on both iOS and Android.

This component uses [PhotoDraweeView](https://github.com/ongakuer/PhotoDraweeView) for Android and [MWPhotobrowser](https://github.com/mwaterfall/MWPhotoBrowser) on iOS.

## About this fork

This fork is based on the great work of @alwx (Alexander Pantyuhov) and has this changes:

* Android minSDKVersion 21 and targetSdkVersion 26 ([configurable](#configure-sdk-versions)).
* Peer dependent on react-native v0.54 and above.
* Using the same version of [fresco](https://github.com/facebook/fresco) included by react-native.
* Updated dependencies
  - [Relex photodraweeview](https://github.com/ongakuer/PhotoDraweeView) v1.1.3
  - Android plugin for Gradle v3.1.1 and Gradle v4.4.x
* Changes to gradle config to support the new version.
* Changes to some properties, mainly `androidScaleType` replaced by `resizeMode`.
* PhotoView as PureComponent
* Minor fixes.
* Typescript definitions.

All this is to adapt it better to my current project (it is not tested on iOS), but feel free to use it.

## Usage

```javascript
import PhotoView from 'react-native-photo-view-ex';
```

Basics:

```jsx
  <PhotoView
    source={{uri: 'https://facebook.github.io/react/img/logo_og.png'}}
    minimumZoomScale={0.5}
    maximumZoomScale={3}
    resizeMode="center"
    onLoad={() => console.log("Image loaded!")}
    style={{width: 300, height: 300}}
  />
```

### Properties

| Property | Type | Description |
|-----------------|----------|--------------------------------------------------------------|
| source | Object | The same as `source` for other React images, except that it does not handle arrays. |
| loadingIndicatorSource | Object | Similarly to `source`, but used to render the loading indicator.<br>__NOTE:__ Must be a local image. |
| fadeDuration | int | Duration of the fade, in milliseconds. |
| scale | float | Zoom scale |
| maximumZoomScale | float | The maximum allowed zoom scale. The default value is 3.0 |
| minimumZoomScale | float | The minimum allowed zoom scale. The default value is 1.0 |
| resizeMode | String | **Android only**: One of "center", "contain", "cover", "fitStart", "fitEnd", "stretch". The default is "cover" |
| style | Array or Object | Subset of react-native style. See [index.d.ts](https://github.com/aMarCruz/react-native-photo-view/blob/dev/index.d.ts) |
| showsHorizontalScrollIndicator | bool | **iOS only**: When true, shows a horizontal scroll indicator. The default value is `true`. |
| showsVerticalScrollIndicator | bool | **iOS only**: When true, shows a vertical scroll indicator. The default value is `true`. |
| zoomTransitionDuration | int | **Android only**: Double-tap zoom transition duration, in milliseconds |

### Events

| Name | Parameter \* | Description |
|-----------------|----------|--------------------------------------------------------------|
| onError | - | Invoked on load error.
| onLayout | `layout: {x, y, width, height}` | Invoked on mount and layout changes.
| onLoad | - | Invoked when load completes successfully.
| onLoadEnd | - | Invoked when load either succeeds or fails.
| onLoadStart | - | Invoked on load start.
| onProgress | `loaded, total` | **iOS only**: Invoked on download progress. |
| onScale | `scale, scaleFactor, focusX, focusY` | Callback function called on scale changes.
| onTap | `scale, x, y` | Callback function called on image tap.
| onViewTap | `x, y` | Callback function called on tap outside of the image.

\* In the `nativeEvent` property.

## Compared to [react-native-image-zoom](https://github.com/Anthonyzou/react-native-image-zoom)

react-native-image-zoom functionality is similar, but there are several major differencies:

* PhotoView is based on PhotoDraweeView which is the "PhotoView For Fresco". It works better, it supports several
important callbacks out-of-box and it is, actually, recommended by Chris Banes, because his
[PhotoView](https://github.com/chrisbanes/PhotoView) (base for react-native-image-zoom) doesn't completely
support Facebook Fresco;
* PhotoView has more options like fadeDuration and minimumZoomScale/maximumZoomScale and more important callbacks;
* PhotoView is written in the same manner as default React Image, and it supports most of the
features Image has (the goal is to be fully compaitable with Image and support absolutely everything);
* It is possible to use PhotoView as a container (currently iOS only)!

## Automatic installation

Just two simple steps:

```bash
$ yarn add react-native-photo-view-ex
$ react-native link react-native-photo-view-ex
```

## Manual installation

### Android

1. Add these lines to `android/settings.gradle`

```groovy
include ':react-native-photo-view-ex'
project(':react-native-photo-view-ex').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-photo-view-ex/android')
```

2. Add the dependency to `android/app/build.gradle`

```groovy
dependencies {
    implementation project(':react-native-photo-view-ex')
}
```

3. Register `PhotoViewPackage` in your `MainApplication.java`:

```java
import io.amarcruz.photoview.PhotoViewPackage;

// ...

public class MainActivity extends ReactActivity {
    // ...

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new PhotoViewPackage() // add this manager
      );
    }

    // ...
}
```

### iOS
1. Add this line to your podfile
```
  pod 'react-native-photo-view-ex', path: './node_modules/react-native-photo-view-ex'
```

2. Run `pod install`

### Configure SDK Versions

You can configure the SDK versions by using variables from [ExtraPropertiesExtension](https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ExtraPropertiesExtension.html).

In your android/build.gradle file, set the SDK versions that your app is using.

This is an example using the predefined values:
```groovy
ext {
    def buildToolsVersion  = '27.0.3'
    def minSdkVersion      = 21
    def compileSdkVersion  = 27
    def targetSdkVersion   = 27
}
```
