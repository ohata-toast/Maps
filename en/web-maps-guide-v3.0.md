## Application Service > Maps > Guide for Web Maps

This guide describes JavaScript-based web APIs required to use web maps of Maps.


## Common API Information

### Prerequisites
- Appkey is required to use APIs.
- To check your appkey, go to **URL & Appkey** on top of the **NHN Cloud Console**.

### Common Request Information

#### URL Information

| Item | URL                              |
| ---- | -------------------------------- |
| Map | https://kr1-maps.api.nhncloudservice.com |


## Web Maps

### 1. Web Maps

The following describes how to show maps on the web browser by using Javascript-based NHN Cloud Maps API.
NHN Cloud Maps API uses WGS84 (EPSG:4326) coordinates.


#### Guide for Maps API
##### For more details on Maps API, see <a href="http://imapsapi.inavi.com/" target="_blank" rel="nofollow">iNavi Maps API Center</a>. <p>


| API Name                                | Parameter                        | Returns                                  | Description                            |
| ---------------------------------------- | -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| new inavi.maps.Map(options)  | options.container : string                 | inavi.maps.Map map object | ID of the DOM element to display the map |
|                                          | options.center : LngLatLike       |                                          | Central coordinates of the map |
|                                          | options.zoom : number            |                                          | Level of the map        |
|                                          | options.heading : number             |                                          | Angle rotated counterclockwise from the north |
|                                          | options.tilt : number             |                                          | Tilt of the map when it is laid flat |
|                                          | options.maxZoom : number             |                                          | Maximum zoom-in level |
|                                          | options.hash : boolean             |                                          | Whether to display map information on the address bar |
|                                          | options.zoomable : boolean             |                                          | Whether the map is zoomable |
|                                          | options.draggable : boolean             |                                          | Whether the map is zoomable |
|                                          | options.rotatable : boolean             |                                          | Whether the map is rotatable |
|                                          | options.keyboard : boolean             |                                          | Whether the map can be moved using the keyboard |
|                                          | options.disableDefaultUI : boolean             |                                          | Whether to hide the default control |
|                                          | options.logoScaleControl : LogoScaleControlOptions             |                                          | Log and scale display control option |
|                                          | options.compassControl : CompassControlOptions             |                                          | Compass display control option |
|                                          | options.zoomControl : ZoomControlOptions             |                                          | Zoom-in/out display control option |
| on(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener to register        |
| once(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener to register   |
| off(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | Listener to remove        |
| new inavi.maps.Marker(option)        | option.map : Map              | inavi.maps.Marker marker object | Map object                         |
|                                          | option.icon : string         |                                          | Icon URL                               |
|                                          | option.position : LngLatLike     |                                          | Coordinates where a marker will be created |
|                                          | option.anchor : string      |                                          | Position where coordinates will be located<br> top-left, top, top-right,<br>left, center, right,<br>bottom-left, bottom, bottom-right |
|                                          | option.title : string            |                                          | Character strings for tool-tips   |
|                                          | option.offset : Array       |                                          | Offset in pixel unit                    |
|                                          | option.draggable : boolean       |                                          | Whether the marker is draggable   |
|                                          | option.zIndex : number           |                                          | z-index value                           |
|                                          | option.opacity : number          |                                          | Opacity level                |
| inavi.maps.LngLat.convertToPixel(lngLat) | lngLat.lng : number               | Screen pixel coordinates | WGS84 longitude                        |
|                                          | lngLat.lat : number               |                                          | WGS84 latitude                         |
| inavi.maps.Pixel.convertToLngLat(pixel) | pixel.x : number               | Longitude/latitude coordinates | Screen pixel x coordinates               |
|                                          | pixel.y : number               |                                          | Screen pixel y coordinates               |


#### Enable the Maps API
```html
<script type="text/javascript" src="https://kr1-maps.api.nhncloudservice.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap"></script>
<div id="div_map" style="width:500px; height:500px;"></div>
<script type="text/javascript">
    var map;
    
    function initMap() {
        //Display the map on the declared DIV.
        map = new inavi.maps.Map({
            container: "div_map",
            center: {
                lng: 127.11,
                lat: 37.40
            },
            zoom: 12,
            type: "NORMAL"
        });
    }
</script>
```

#### Change the Map Mode
```html
<script type="text/javascript">
    // Change the map type of the created map object.
    // General: NORMAL, Aerial background: SATELLITE
    // Change to a aerial background map.
    window.onload = function (){
        map.setType("SATELLITE");
    };
</script>
```

#### Register a Map Event
```html
<script type="text/javascript">
    //Register the move event to the map.
    window.onload = function (){
        map.on("move", moveHandler);
    }

    function moveHandler(event){
        console.log("event callback!");
    }
</script>
```

#### Remove the Map Event
```html
<script type="text/javascript">
    //Remove the move event from the map.
    window.onload = function (){
        map.off("move", moveHandler)
    }
</script>
```

#### Add a Map Marker
```html
<script type="text/javascript">
    // Add a marker object to the map.
    window.onload = function (){
        var marker = new inavi.maps.Marker({
            map: map,
            position: {
                lng: 127.11,
                lat: 37.40
            }
        });

        // Move the marker object.
        marker.setPosition({lng: 127.110513, lat: 37.402027});
    }
</script>
```

#### Convert Screen Pixel Coordinates to WGS Coordinates
```html
<script type="text/javascript">
    window.onload = function (){
        // Convert screen pixel coordinates to WGS coordinates.
        var screen_pixel = {
            x: 100,
            y: 100
        };

        var wgs84 = inavi.maps.Pixel.convertToLngLat(map,screen_pixel);
        console.log(wgs84.lng);
        console.log(wgs84.lat);
    }
</script>
```

#### Convert WGS Coordinates to Screen Pixel Coordinates
```html
<script type="text/javascript">
    window.onload = function (){
        // Convert WGS coordinates to screen pixel coordinates.
        var wgs84 = {
            lng: 127.11074994024005,
            lat: 37.40215870673785
        };

        var screen_pixel = inavi.maps.LngLat.convertToPixel(map,wgs84);
        console.log(screen_pixel.x);
        console.log(screen_pixel.y);
    }
</script>
```

#### Change the Map Style
```html
// Change the map style of the created map object to the style created with Map Studio.
<script type="text/javascript">
    window.onload = function (){
        //For StyleJsonUrl, refer to the deployment code when deploying styles in Map Studio
        map.setStyle("{StyleJsonUrl}");
    }
</script>

// When applying styles while initializing the map, use the script below instead of the existing script.
<script type="text/javascript" src="https://kr1-maps.api.nhncloudservice.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap&styleID={styleID}"></script>
```
