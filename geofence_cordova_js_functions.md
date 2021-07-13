### Class `WoosmapSettings`

**Properties/methods**

`boolean modeHighFrequencyLocation = false;`

Enable/disable Location
`boolean trackingEnable = true;`

filter time to refresh user location
`int currentLocationTimeFilter = 0;`

filter distance to refresh user location
`int currentLocationDistanceFilter = 0;`

Enable/disable VisitEnable
`boolean visitEnable = true;`

Enable/disable SearchAPI
`boolean searchAPIEnable = true;`

Enable/disable Creation region on SearchAPI
`boolean searchAPICreationRegionEnable = true;`

Radius region From SearchAPI (m)
`int firstSearchAPIRegionRadius = 100;`
`int secondSearchAPIRegionRadius = 200;`
`int thirdSearchAPIRegionRadius = 300;`

filter time to request Search API
`int searchAPITimeFilter = 0;`

filter distance to request Search API
`int searchAPIDistanceFilter = 0;`

Enable/disable DistanceAPI
`boolean distanceAPIEnable = true;`

Mode transportation DistanceAPI
`private String drivingMode  = "driving";`
`private final String walkingMode  = "walking";`
`private final String cyclingMode  = "cycling";`
`String modeDistance = drivingMode;`

Filter Accuracy of the location
`int accuracyFilter = 100;`

 delay for outdated notification
`int outOfTimeDelay = 300;`

 Distance detection threshold for visits
`double distanceDetectionThresholdVisits = 25.0;`

 Distance detection threshold for visits
`long minDurationVisitDisplay = 60 * 5;`
`long durationVisitFilter = 1000 * minDurationVisitDisplay;`

Delay of Duration data
`long numberOfDayDataDuration = 30; number of day`
`long dataDurationDelay = numberOfDayDataDuration * 1000 * 86400;`

Active Classification
`boolean classificationEnable = true;`

 Distance detection threshold for a ZOI classified
`int radiusDetectionClassifiedZOI = 50;`

 Key for APIs
`String privateKeyGMP= "";`
`String privateKeyWoosmapAPI = "";`

Checking Position is inside a region
`boolean checkIfPositionIsInsideGeofencingRegionsEnable = true;`

Notification ForegroundService
`boolean foregroundLocationServiceEnable = false;`
`String updateServiceNotificationTitle = "Location updated";`
`String updateServiceNotificationText = "This app use your location";`

---

### Class `Woosmap`

**Properties/methods**

* `void addGeofence(String id, LatLng latLng, float radius, String idStore)`
* `void createWoosmapNotifChannel()` **This is specific to Android. Will this need to be included**
* `void enableModeHighFrequencyLocation(boolean modeHighFrequencyLocationEnable)`
* `Boolean enableTracking(boolean trackingEnable)`
* `void getLastRegionState()`
* `void trackRegion()`
* `void trackDistanceAPI()`
* `void trackLocation()`
* `void trackRegionLog()`
* `void trackSearchAPI()`
* `void trackVisit()`
* `void removeGeofence(String id)`
* `void removeGeofence()`
* `void trackAirshipEvent(Object event)`

