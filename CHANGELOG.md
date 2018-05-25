## react-native-photo-view-ex

Fork of [react-native-photo-view](https://github.com/alwx/react-native-photo-view)

#### v1.0.2
* Allows you to configure the SDK versions using variables from [ExtraPropertiesExtension](https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ExtraPropertiesExtension.html).

#### v1.0.1
* Fixes error en typings.

#### Conversion to react-native-photo-view-ex v1.0.0 from react-native-photo-view v1.5.4
* Adds typings.
* Renames `androidZoomTransitionDuration` to `zoomTransitionDuration`
* Removes `androidScaleType` property.
* Adds `resizeMode` property supporting 'center', 'contain', 'cover', 'fitEnd', 'fitStart', 'stretch'. The default is 'cover'.
* Using the `Image.resolveAssetSource` method instead of requiring the module directly.
* Updated README.md

#### v1.5.3

* Apply "Fixing initialZoomScaleWithMinScale when image is larger than the screen #86" by @douglasjunior
* Updated build.gradle to get settings from root project.
* Updated gradle plugin to v3.1.0
* Updated facebook fresco to v1.3.0
* Updated photodraweeview to v1.1.3
* Minor fixes, makes some Java methods private.
