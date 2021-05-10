## Application Service > Maps > SDK User Guide for iOS Maps
Describes the basic project configuration method to enable iNavi maps on iOS. 

### Prerequisites 
- To enable iNavi maps, **Appkey** is required for authentication. 

#### Enable Service 
- Go to **[NHN Cloud Console]**, select a service and click Application Service > Maps. 

#### Check Appkey 
- To check your appkey, go to **URL & Appkey** on top of the **NHN Cloud Console**. 


### Project Configuration 
To enable iNavi maps SDK, a project must be configured in the following order.

#### Install Git LFS
Due to heavy volume of SDK, [Git Large File Storage(LFS)](https://git-lfs.github.com/) must be installed before pod dependency is installed.  
> Without `git-lfs, SDK dependency is not properly installed which may result in build error.'

```
brew install git-lfs
git lfs install
```

#### Configure Podfile
Since iNavi Maps SDK is deployed via CocoaPods, add dependency on iNavi Maps SDK to Podfiles of the project.

```ruby
# Podfile
target 'iNaviMapsDemo' do
  use_frameworks!
  ...
  pod 'inavi-maps-sdk'
  ...
end
```

#### Install SDK 
After dependency setting, go to protect path at the terminal, execute the command as below and install iNavi maps SDK. 
> `When SDK dependency is completely installed, the framework volume reaches around 100MB.`
```
pod install --repo-update
```

#### Delete CocoaPods Cache
Infrequently, cache from previously downloaded SDK dependency may remain, causing a build error.\
Follow the commands as below to delete CocoaPods cache of iNavi maps SDK. 
```
pod cache clean inavi-maps-sdk
pod update inavi-maps-sdk
```

### Setting Appkey 
Appkeys can be set in two methods as below: 

> Without appkey setup, authentication error may occur during map initialization. 

#### 1. Set on Project info.plist  
An appkey can be set within the `info.plist` file. 
```xml
<!-- info.plist -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	...
	<key>iNaviAppKey</key>
	<string>YOUR_APP_KEY</string>
	...
</dict>
</plist>
```

#### 2. Call INVMapSdk API 
To set appkey, call function of the [INVMapSdk] singleton object dynamically at the time when application is created.  

```swift
// Swift
INVMapSdk.sharedInstance().appKey = "YOUR_APP_KEY"
```

#### Authentication Failure 
If authentication fails for map initialization, the error code and message is delivered via callback registered within SDK. To receive callbacks on failure, set [INVMapSdkDelegate] for the [INVMapSdk] singleton object as below: 
```swift
// Swift
INVMapSdk.sharedInstance().delegate = self

func authFailure(_ errorCode: Int, message: String) {
    // Process failure in authentication 
}

```
Unless callback for authentication failure is set, error codes and messages are displayed on popups by default. 

#### Authentication Error Codes 
| Code | Description |
| ------ | ------ |
| 300 | Appkey is invalid |
| 401 | Appkey is not set |
| 503 | Server connection failed |
| 504 | Exceeded server connection time  |
| 500 | Unknown error |
| Others | Server error  (to be updated with definition) |


### Creating Maps 
Describes how to display iNavi on the app. 

#### Display Maps
Create and add [InaviMapView] on the UIViewController, like the example shows. 
```swift
// Swift
import iNaviMaps

override func viewDidLoad() {
    super.viewDidLoad()

    let mapView = InaviMapView(frame: view.bounds)
    view.addSubview(mapView)
}
```
To add maps by using Interface Builder, add UIview to XIB or Storyboard, and set [InaviMapView] for Custom Class of the Identity Inspector panel. 

#### Set Map Events
With [INVMapViewDelegate] implemented and  `delegate` is set for [InaviMapView], events can be set for interactions between map and user, such as clicks on the map, double-clicks, or long-clicks. 
```swift
// Swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    mapView.delegate = self
}

func didTapMapView(_ point: CGPoint, latLng latlng: INVLatLng) {
    // point: Coordinates on screen of clicked point
    // latlng: Coordinates on map of clicked point 
}
```

#### Expose Markers
Create a marker object, and set `position` and `map` attributes, and the marker is displayed. 
```swift
// Swift
let marker = INVMarker(position: INVLatLng(lat: 37.40219, lng : 127.11077))
marker.title = "Title"
marker.mapView = mapView
```

#### Remove Markers 
Set `nil` for the map attribute of the marker object, and the marker is removed. 
```swift
// Swift
marker.mapView = nil
```

#### Move Cameras 
Create the [INVCameraUpdate] object via factory method or [INVCameraUpdateParams], and deliver parameters to the [moveCamera()] function and call, then you can move the camera.  

Since callback is supported for animation and camera events, you can implement camera movement as much as you need. 
```swift
// Swift
let camUpdate = INVCameraUpdate.init(targetTo: INVLatLng(lat: 36.99473, lng : 127.81832))
camUpdate.animation = .fly
camUpdate.animationDuration = 3
mapView.moveCamera(camUpdate)
```

#### Create your own map style
`Map Studio` serves you to create your own unique map by allowing you to modify not only fonts but also map colors and legends icons as you want. Also, with the APIs from the latest SDK version, you can apply your own custom style to your map.
```swift
// Swift
INVMapSdk.sharedInstance().delegate = self
func authSuccess(_ customMapStyles: [INVMapStyle]) {
    // Delivers the array of map styles as a callback upon completion of map initialization authentication
}
// Applies the first custom style from the array of the saved custom styles to the map
mapView.customMapStyle = INVMapSdk.sharedInstance().savedCustomMapStyles.first
```

### Guide for Main Maps SDK 
For more details on Maps SDK, see [API Center for iNavi Maps](http://imapsapi.inavi.com/).

[INVMapSdk] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVMapSdk.html)
[INVMapSdkDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapSdkDelegate.html)

[InaviMapView] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html)

[INVMapViewDelegate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Protocols/INVMapViewDelegate.html)

[INVCameraUpdate] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdate.html)
[INVCameraUpdateParams] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/INVCameraUpdateParams.html)

[moveCamera()] : [https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:](https://inavi-systems.github.io/inavi-maps-sdk-reference/ios/Classes/InaviMapView.html#/c:objc(cs)InaviMapView(im)moveCamera:)

[NHN Cloud Console] : [https://console.toast.com/](https://console.toast.com/)
