## Application Service > Maps > 웹 지도 가이드

Maps 웹 지도를 사용하는 데 필요한 JavaScript 기반 웹 API를 설명합니다.


## 공통 정보

### 사전 준비
- API를 사용하려면 Appkey가 필요합니다.
- Appkey는 **NHN Cloud Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

### 요청 공통 정보

#### URL 정보

| Item       | URL                                      |
| --------- | ---------------------------------------- |
| Map        | https://kr1-maps.api.nhncloudservice.com |


## 웹 지도

### 1. 웹 지도

JavaScript 기반 NHN Cloud Maps API를 이용해 웹 브라우저에 지도를 표시하는 방법을 설명합니다.
NHN Cloud Maps API는 WGS84(EPSG:4326) 좌표를 사용합니다.


#### 주요 Maps API 안내
##### 추가 Maps API 상세 사용법은 <a href="http://imapsapi.inavi.com/" target="_blank" rel="nofollow">iNavi Maps API Center</a>를 참고하시기 바랍니다. <p>


| API 명                                    | Parameter                        | Returns                                  | 설명                                       |
| ---------------------------------------- | -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| new inavi.maps.Map(options)  | options.container : string                 | inavi.maps.Map 지도 객체 | 지도를 표시할 DOM 엘리먼트의 ID             |
|                                          | options.center : LngLatLike       |                                          | 지도의 중심 좌표                  |
|                                          | options.zoom : number            |                                          | 지도의 레벨                                   |
|                                          | options.heading : number             |                                          | 북쪽을 기준으로 반시계 방향으로 회전한 각도 |
|                                          | options.tilt : number             |                                          | 지도를 눕혔을 때의 기울기 |
|                                          | options.maxZoom : number             |                                          | 최대 확대 레벨 |
|                                          | options.hash : boolean             |                                          | 주소 표시줄에 지도 정보 표시 여부 |
|                                          | options.zoomable : boolean             |                                          | 확대 가능 여부 |
|                                          | options.draggable : boolean             |                                          | 드래그 가능 여부 |
|                                          | options.rotatable : boolean             |                                          | 회전 가능 여부 |
|                                          | options.keyboard : boolean             |                                          | 키보드를 사용한 지도 이동 가능 여부 |
|                                          | options.disableDefaultUI : boolean             |                                          | 기본 컨트롤 숨김 여부 |
|                                          | options.logoScaleControl : LogoScaleControlOptions             |                                          | 로고 및 스케일 표시 컨트롤 옵션 |
|                                          | options.compassControl : CompassControlOptions             |                                          | 나침반 표시 컨트롤 옵션 |
|                                          | options.zoomControl : ZoomControlOptions             |                                          | 확대 축소 표시 컨트롤 옵션 |
| on(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 등록할 리스너                                  |
| once(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 등록할 리스너                                  |
| off(eventType, listener) | eventType : string              |                                          | load,<br>zoomstart, zoom, zoomend,<br>rotatestart, rotate, rotateend,<br>tiltstart, tilt, tiltend,<br>click, dblclick,<br>mousedown, mouseup, mousemove,<br>mouseenter, mouseleave, mouseover, mouseout,<br>contextmenu,<br>wheel,<br>touchstart, touchend, touchcancel, touchmove,<br>movestart, move, moveend,<br>dragstart, drag, dragend|
|                                          | listener : Function             |                                          | 제거할 리스너                                  |
| new inavi.maps.Marker(option)        | option.map : Map              | inavi.maps.Marker 마커 객체 | 지도 객체                                    |
|                                          | option.icon : string         |                                          | 아이콘 URL                                   |
|                                          | option.position : LngLatLike     |                                          | 마커 생성 좌표                    |
|                                          | option.anchor : string      |                                          | 좌표가 위치할 곳<br> top-left, top, top-right,<br>left, center, right,<br>bottom-left, bottom, bottom-right |
|                                          | option.title : string            |                                          | 툴팁 문자열                                   |
|                                          | option.offset : Array       |                                          | 픽셀 단위 오프셋                                    |
|                                          | option.draggable : boolean       |                                          | 드래그 가능 여부                                |
|                                          | option.zIndex : number           |                                          | z-index 값                                |
|                                          | option.opacity : number          |                                          | 투명도                                      |
| inavi.maps.LngLat.convertToPixel(lngLat) | lngLat.lng : number               | 화면 픽셀 좌표 | WGS84 경도                                 |
|                                          | lngLat.lat : number               |                                          | WGS84 위도                                 |
| inavi.maps.Pixel.convertToLngLat(pixel) | pixel.x : number               | 경위도 좌표 | 화면 픽셀 x 좌표                                       |
|                                          | pixel.y : number               |                                          | 화면 픽셀 y 좌표                                       |


#### Maps API 사용
```html
<script type="text/javascript" src="https://kr1-maps.api.nhncloudservice.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap"></script>
<div id="div_map" style="width:500px; height:500px;"></div>
<script type="text/javascript">
    var map;
    
    function initMap() {
        //선언한 DIV에 지도를 표출합니다.
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

#### 지도 모드 변경
```html
<script type="text/javascript">
    // 생성된 지도 객체의 지도 Type을 변경합니다.
    // 일반: NORMAL, 항공배경: SATELLITE
    // 항공배경지도로 변경합니다.
    window.onload = function (){
        map.setType("SATELLITE");
    };
</script>
```

#### 지도 이벤트 등록
```html
<script type="text/javascript">
    //지도에 move 이벤트를 등록합니다.
    window.onload = function (){
        map.on("move", moveHandler);
    }

    function moveHandler(event){
        console.log("event callback!");
    }
</script>
```

#### 지도 이벤트 제거
```html
<script type="text/javascript">
    //지도에 move 이벤트를 제거합니다.
    window.onload = function (){
        map.off("move", moveHandler)
    }
</script>
```

#### 지도 마커 추가
```html
<script type="text/javascript">
    // 지도에 마커 객체를 추가합니다.
    window.onload = function (){
        var marker = new inavi.maps.Marker({
            map: map,
            position: {
                lng: 127.11,
                lat: 37.40
            }
        });

        // 마커 객체를 이동시킵니다.
        marker.setPosition({lng: 127.110513, lat: 37.402027});
    }
</script>
```

#### 화면 픽셀 좌표를 WGS 좌표로 변환
```html
<script type="text/javascript">
    window.onload = function (){
        // 화면 픽셀 좌표를 WGS 좌표로 변환합니다.
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

#### WGS 좌표를 화면 픽셀 좌표로 변환
```html
<script type="text/javascript">
    window.onload = function (){
        // WGS 좌표를 화면 픽셀 좌표로 변환합니다.
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

#### 지도 스타일 변경
```html
// 생성된 지도 객체의 지도 스타일을 Map Studio로 작성한 스타일로 변경합니다.
<script type="text/javascript">
    window.onload = function (){
        // StyleJsonUrl은 Map Studio에서 스타일 배포 시 배포 코드 참조
        map.setStyle("{StyleJsonUrl}");
    }
</script>

// 지도 초기화 시 스타일을 적용 할 경우에는 기존 스크립트 대신 아래 스크립트를 사용합니다.
<script type="text/javascript" src="https://kr1-maps.api.nhncloudservice.com/maps/v3.0/appkeys/{appkey}/maps?callback=initMap&styleID={styleID}"></script>
```
