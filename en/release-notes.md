## Application Service > Maps > Release Notes

### October 26, 2023
#### Added Features
* [API] Added Search for W3W Suggestions API
* [API] Added Search for W3W coordinates (coordinates -> address) API
* [API] Added Search for W3W best point API
* [SDK] Support -> AndroidX Migration (Android)
* [SDK] Change play-services-location library runtime dependency (Android)

#### Bug Fixes
* [SDK] Fixed touch event error in INVShape overlap state (iOS)

### September 12, 2023
#### Added Features
* [API] Added parameters to APIs for navigation
    * useStartDirection: Whether to specify navigation direction based on departure coordinates
    * APIs to which parameters are added
        * Route Navigation
        * Summary of Route Navigation
        * Search of Estimated Routes
        * Added multi-stops 100
        * Summarize path information between stopovers

### October 4, 2022
#### Added Features
* [API] Added parameters to APIs for navigation 
    * carHeight: Car height
    * carWeight: Car weight
    * APIs to which parameters are added
        * Route Navigation
        * Summary of Route Navigation
        * Search of Estimated Routes
        * Added multi-stops 100
        * Summarize path information between stopovers
* [SDK] Added an API that sets hybrid and aerial map type
* [SDK] Added Conversion of Coordinates API

### August 23, 2022
#### Added Features
* [API] Added parameters to the address validation API
    * posx: X coordinates
    * posy: Y coordinates
    * Improved so that, when posx and posy are entered, the results are ordered from closest to farthest from the entered coordinates

### July 26, 2022
#### Added Features
* [Console] Added the excel extraction feature for statistics pages
    * Hourly, daily, monthly

### June 30, 2022
#### Added Features
* [API] Added the address validation API

### December 28, 2021
#### Feature Updates
* [API] Improved so that a request is processed normally even if the 'User-Agent' header value is unavailable

### October 26, 2021
#### Added Features
* [API] Added parameters to Route Navigation API
    * usageType: Vehicle usage type
    * searchByAddress: Whether to use address-based route navigation
* [API] Added parameters to Added Multi-Stops 100 API
    * usageType: Vehicle usage type
    * searchByAddress: Whether to use address-based route navigation
* [API] Added parameters to Summarize Path Information Between Stopovers API
    * usageType: Vehicle usage type
    * searchByAddress: Whether to use address-based route navigation
    
### September 28, 2021
#### Added Features
* [API] Added an API for querying building group entry points

### May 11, 2021
#### Added Features
* [API] Added an API that changes the style of web map
* [API] Added an API that supports custom map style created with web map Map Studio service
* [Console] Added Map Studio introduction page
* [SDK] Added an API that supports custom map style created with Map Studio service

### April 13, 2021
#### Added Features
* [API] Added the API that searches for administrative/legal-status neighborhoods within polygons
* [API] Added the API that searches for space
* [API] Added the API that summarizes path information between stopovers

### March 23, 2021
#### Added Features
* [API] Added options for sorting local category search and showing the number of search results

#### Feature Updates
* [SDK] Improved SDK stability
* [SDK] Changed Android SDK deployment Repository

### February 23, 2021
#### Added Features
* [SDK] Added API to set sizes of map symbols
* [SDK] Supports 3D effect for buildings when setting map tilt angle

### January 26, 2021
#### Added Features
* [API] “Added multi-stops 100” API added

### December 29, 2020
#### Bug Fixes
* [API] ReverseGeocoding TW coordinate request bug fixed

### November 24, 2020
#### Added Features
- [API] Expected taxi fare added to the normal path navigation response
- [API] Expected taxi fare added to the path prediction navigation response

#### Feature Updates
- [SDK] Fixed an abnormal termination error that used to occur intermittently when launched in the background

### October 27, 2020
#### Added Features
* [SDK] Initial map option property added
* [SDK] Setup for initial map options supported through XML attributes (Android)
* [SDK] Setup for initial map options supported through Interface Builder (iOS)

#### Feature Updates
* [SDK] Fixed the error where marker's icon image often fails to update (iOS)
* [SDK] Fixed the error where the previous marker is often left on the map when calling INVClusterManager#invalidate (iOS)

### August 25, 2020
#### Added Features
* [SDK] Added API sharing the same symbols on the marker from the map
* [SDK] Add API for patterned images on the path shape
* [SDK] Supports the TextureView mode for the map rendering view (Android)

### July 28, 2020
#### Feature Updates
* [SDK] Fixed infrequent error of failed display of marker (Android)

## June 23, 2020
#### Feature Updates
* [SDK] Updated not to cause an exception when it is requested to move camera to an invalid location
* [SDK] Fixed infrequent blinks when the location icon is relocated
* [SDK] Enhanced stability of SDKs

### May 26, 2020
#### Feature Updates
* [SDK] Changed to disable animation for changing information window display state by default
* [SDK] Added API to set animation for changing information window display state
* [SDK] Added API to set the control point for zooming or rotating gestures to the center of the map

### April 28, 2020
#### Added Features
* [SDK] Added API for configuring minimum/maximum tilting angle of a map

#### Feature Updates
* [SDK] Stability enhanced for SDK
* [SDK] Response available for Swift 5.2 (iOS)
* [API] Updated error logs from failed request of StaticMap

### March 24, 2020
#### Added Features
* [SDK] Added API returning the location data of a camera taking up the entire view of a particular area
* [SDK] Added API removing all shapes registered on a map from the map
* [SDK] Changed map logo image

#### Feature Updates
* [API] Changed the search engine
* [API] Improved Reverse Geocoding Validation Check
* [SDK] Improved usability of tilt gestures (Android)

#### Bug Fixes
* [SDK] Fixed an error where, when some shape objects are created before map initialization, such shape objects were displayed abnormally on the map (Android)
* [SDK]  Fixed the error of abnormal closure when Proguard obfuscation is applied (Android)
* [SDK]  Fixed error in which map does not show up on a low version OS (Android)

### February 25, 2020
#### Added Features
* [SDK] Added Marker Clustering

#### Feature Updates
* [Console] Added Japanese fonts

#### Bug Fixes
* [SDK] Fixed an error where the outline was displayed abnormally intermittently when displaying INVRoute
* [SDK] Fixed an error where the InvRoute#strokeWidth property was not applied properly (Android)
* [SDK] Fixed the error of abnormal display of an icon location when the icon size is changed (Android)
* [SDK] Fixed the error of abnormal closure, when INVShape is added/removed (iOS)

### January 21, 2020
#### Added Features
* [API] Added Search Nearby Categories API
	* Added the search of base coordinates X and Y, space and radius categories

#### Feature Updates
* [API] Added building names and zip codes for reverse geocoding
* [API] Deleted catecode for integrated search
* [SDK] Default animation value to be disabled when marker display status is changed
* [SDK] Set Animation API to be added when marker display status is changed
* [SDK] Changed the INVMarker#infoWindow attribute to nullable (iOS)

#### Bug fixes
* [API] Updated validation check on day 2 of spopt for integrated search
* [API] Updated validation check for the query of POI sub-facilities
* [SDK] Fixed mistaken line changes when "^" is included to marker titles
* [SDK] Fixed unnatural camera movement for the fly animation type (iOS)
* [SDK] Fixed failed application of map padding to zoom controller

### December 24, 2019
#### Feature Updates
* [API] Fixed the bug in which numbers exceeding the 8th digit are broken
* [API] Changed the ReverseGeocoding engine
* [API] Fixed the StaticMap IE bug
* [SDK] Added an interface restricting the area for map movement
* [SDK] Added I/F for enabling/disabling logo-click events
* [SDK] Added the intent interface calling open-source license, or legal announcement activity (Android)
* [SDK] Added the Call ViewController interface for open-source license or legal announcement (iOS)
* [SDK] Added the feature of setting space between marker icon and title
* [SDK] Changed the property of INVLatLng and INVLatLngBounds as readonly (iOS)
* [SDK] Applied Deprecated for INVCameraUpdateParams#scrollTo  (replaced by targetTo) (iOS)
* [SDK] Applied Deprecated for INVCameraUpdateParams#scrollBy  (replaced by targetBy) (iOS)
* [SDK] Applied Deprecated for INVLatLngBounds#latLngBoundsSouthWest (replaced by boundsWithSouthWest) (iOS)

### November 26, 2019
#### Added Features
* [API] Added estimated search of general routes
	* Added the search navigation for estimated departure/arrival time based on statistics
* [SDK] Added estimated navigation of general routes
	* Added the LocationIcon feature (changing the shape and position of location icons)
	* Added InvRoute (to expose routes on the map)
	* Applied Deprecated for InvMultiLine (replaced by InvRoute)

#### Feature Updates
* [API] Changed to WGS84, which is the default coordinates of v3.0 API
* Added StaticMap API Image files
* [SDK] Fixed the error in which color is not properly displayed, with the setup of colors, including the alpha value. (Android)
* [SDK] Fixed the error in which shape disappears from a particular map level (iOS)
* [SDK] Fixed the error of infrequently abnormal exposure of distance on a scale bar (iOS)
* [SDK] Improved the overlapped map cycle icons when the map level is fast changed
* [SDK] Fixed the error in which it is abnormally closed with a click of the log on iOS 10 or lower versions  (iOS)
* [SDK] Fixed the error in which it is abnormally closed with the creation of InvShape before map initialization. (Android)

### October 29, 2019
#### Release of v3.0

* Service the most updated iNavi technology with APIs on the new Maps version
* Clear and fast map service is available due to vector-based map configuration, regardless of resolution
* By using both WebGL and vector files, flawless zooming on high-resolution, as well as a variety of visualization, are supported between background maps and data layer

* Quality Upgraded for Map Background/Cycle
    * Improved the overall color and style of the map background
    * Added the North Korean region on the map, and improved the configuration data of roads, buildings, and facilities on each map level
    * Selectively show cycle data based on big data analysis and statistics by using destination information from the on-vehicle navigation system
    * Conduct on-site nationwide investigation so as to update map data on a regular basis and provide the most updated data precisely and fast

* Added Web Maps API
    * Available to change engine for vector map rendering, set map rotation, rotation angle/tilting level, and return boundary coordinates on the map
    * Set/Undo map events (e.g. clicks, double-clicks, mouse-over, right-clicks, and dragging)
    * APIs provided for marker, marker clustering, information window, polyline/polygon/circle, and coordinate conversion

* Added API v3.0
    * Added an API integrating with iNavi's new route navigation engine
    * Guide for optimized routes and fast search of directions based on real-time traffic data
    * Added an API which navigates multiple destinations, allowing the query of each navigation time and distance data from one-time navigation.
    * Added an API for multiple departure navigation, allowing the query of each navigation time and distance data from one-time navigation.
    * Added Static Maps API
    * Added API creating static map images with the map size in need and marker images.
    * As part of vector map characteristics, map rotation, angle setting, and double zoom-ins are available, hence creating a brighter map.

* Added development guides for Maps SDK and Sample Apps for Android and iOS
    * Allows creating/setting map object, coordinates object, camera movement, zoom-in/out, tilting and rotation
    * Features of marker (creating, specifying icons or locations, and etc.), caption (text exposed along with a marker), style setting (color, size, opacity, overlapping, and Z-index)
    * Allows creating/setting information window (tool-tips), setting adapter or events, creating polyline/polygon/circle, and setting styles.

### November 27, 2018
#### Added Features
* [API] Added Coordinates Conversion API
	* Added conversion API between coordinates (WGS84 coordinates <-> TM coordinates)

### April 24, 2018
#### Feature Updates
* [Batch] Changed the mechanism for the operations of statistics batch
    * Changed the Log Creation Time: Changed from 00 sec 00 minute of every hour, into 30 sec 00 min of every hour
    * Changed the method of creating base date and time on column: On batch server time

#### Guide Updates
* Deleted Android and iOS User Guides
    * Integrated into Mobile Web Map within User Guide of Web Maps

### March 22, 2018
#### Added Features
* [API] Added Web Maps v.2.0 API
    * Main map features based on HTML5
    * Map rotation is available
        * Mobile: Use two fingers
        * PC : Shift+alt+drag or set an angle in need
    * Provides Overview which displays more than one map on the screen
    * Added the effects of map loading events and animation
    * Preload Tiles
        * Mark by caching once-confirmed area images
    * Processing KML/GPX File Type
        * Load KML/GPX files and mark onto the map; map data can be returned into KML/GPX types
* [Console] Added Web Maps v2.0
    * Added example script for Web Maps v2.0
    * Added Web Maps v2.0 for the statistics item

### June 22, 2017
#### Bug Fixes
* [Console] Fixed the bug in which the search result of Execution-Integrated Search example is not properly queried

### April 20, 2017
#### Feature Updates
* [API] Search of coordinates (coordinates -> address)
	* Added a type of coordinates available for query (TW coordinates only -> TW and WGS84 coordinates)

### March 23, 2017
#### New Product Release
* The API service is an optimized web map solution based on the web map service, providing web maps, integrated search, and route navigation.
    * All API services are available at once, including iNavi's specialized maps, search, and getting directions.
    * Various map features are available via web maps API, including movement, zoom-in/out, and aerial maps.
    * Integrated search is available for building name, phone number, land-lot number-based address (old address system), and road name-based address (new address system).
    * With traffic data reflected on route navigation, getting a direction becomes faster and easier.
