# Woosmap geofencing Cordova Plugin

### Cordova Plugin Structure

![N|Solid](https://cordova.apache.org/static/img/guide/cordovaapparchitecture.png)

---# Woosmap geofencing Cordova Plugin

### Cordova Plugin Structure

![N|Solid](https://cordova.apache.org/static/img/guide/cordovaapparchitecture.png)

---

### _Class `Woosmap`_

`Woosmap` class will contain methods to monitor location, POIs, regions and visits. 

* **Initializing Woosmap Object**

```javascript
var woosmapSettings = {
        privateKeyWoosmapAPI: "<<WOOSMAP_KEY>>", 
        privateKeyGMPStatic: "<<GOOGLE_KEY>>",
        trackingProfile: "liveTracking"
};

Woosmap.initialize(woosmapSettings, onSuccess, onError);

var onSuccess = function() {
    console.log("success");
};

var onError = function(error) {
    alert('message: ' + error.message);
};
```

Tracking profile can be either of the following
* `liveTracking`
* `passiveTracking`
* `visitsTracking`

* **Check for permissions (User Story 1.1)**: Call `Woosmap.getPermissionsStatus` method to check if the app is granted required permissions to track the location.

```javascript
Woosmap.getPermissionsStatus(success, errorCallback);

var success = function(status) {
   console.log(status);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};    
```

Parameter `status` will be a string, one of:

* `GRANTED_BACKGROUND`
* `GRANTED_FOREGROUND`
* `DENIED`


* **Request permissions (User Story 1.2)**: Call `Woosmap.requestPermissions` method to request the required permissions. Request for background location permission will depend on the `profile` configuration. 

```javascript
Woosmap.requestPermissions(success, errorCallback);

var success = function() {
   console.log("success");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};    
```



* **Track location (User Story 2.1, 2.6)**: Call `watchLocation` method. Method will invoke callback and pass a location object as a parameter. Method will return a `watchId`. This id can be used to remove a callback.

```javascript

//Start tracking locations
var watchId = Woosmap.watchLocation(locationCallback, errorCallback);

var locationCallback = function(location) {
    alert('Latitude: '          + location.lat          + '\n' +
          'Longitude: '         + location.lng         	+ '\n' +
          'Accuracy: '          + location.accuracy     + '\n' +
          'Speed: '             + location.speed        + '\n' +
          'Timestamp: '         + location.timestamp    + '\n');
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Stop tracking location (User Story 2.5)**: Call `clearLocationWatch` method to stop tracking location for a specified watch. Method will accept `watchId` parameter. If `watchId` is `null` or `undefined` then plugin will clear all watches.

```javascript

//Stop watching location
Woosmap.clearLocationWatch(watchId, onSuccess, onError);

```

* **Track search API**: Call `watchSearchApi` method to track search API. Method will invoke a callback with `POI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchSearchAPI(searchCallback, errorCallback);

var searchCallback = function(poi) {
   console.log(poi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearSearchApiWatch(watchId, onSuccess, onError);
```


* **Track Distance API (User Story 3.7)**: Call `watchDistanceApi` method to track distance API. Method will invoke a callback with `DistanceAPI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchDistanceApi(distanceApiCallback, errorCallback);

var distanceApiCallback = function(distanceApi) {
   console.log(distanceApi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearDistanceApiWatch(watchId, onSuccess, onError);
```

* **Track Visits (User Story 4.1)**: Call `watchVisits` method to track Visits. Method will invoke a callback with `Visit` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchVisits(visitCallback, errorCallback);

var visitCallback = function(visit) {
   console.log(visit);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearVisitsWatch(watchId, onSuccess, onError);
```


* **Track Regions (User Story 3.2, 3.3)**: Call `watchRegions` method to track Regions. Method will invoke a callback with `Region` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchRegions(regionCallback, errorCallback);

var regionCallback = function(region) {
   if (region.didEnter){
		console.log("Region entered");
   }
   else{
		console.log("Region exited");
   }
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearRegionsWatch(watchId, onSuccess, onError);
```

* **Add Regions (User Story 3.1)**: Call `addRegion` method to add region that you want to monitor. Method will accept an object following attributes.
	* `regionId` - Id of the region
	* `lat` - Latitude
	* `lng` - Longitude
	* `radius` - Radius in meters

```javascript

var regionInfo = {
	"regionId": "rue_tolbiac",
	"lat": 48.82862170908377,
	"lng": 2.3729680825540838,
	"radius": 10,
};

Woosmap.addRegion(regionInfo, addRegionCallback, errorCallback);

var addRegionCallback = function() {
   console.log("success");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```


* **Remove Region (User Story 3.5)**: Call `removeRegion` method to add region that you want to monitor. Method will accept following parameter. Passing null value to `regionId` will remove all the regions.
	* `regionId` - Id of the region
	
```javascript
Woosmap.removeRegion("rue_tolbiac", removeRegionCallback, errorCallback);

var removeRegionCallback = function() {
   console.log("success");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

---

### _Class `Woosmap.db`_

`Woosmap.db` class will contain methods to fetch POIs, regions and visits from the local device DB. 


* **Get POIs**: Call `getPois` method to get an array of POIs from the local db.

```javascript
Woosmap.db.getPois(getPoisCallback, errorCallback);

var getPoisCallback = function(pois) {
   console.log(pois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Locations (User Story 2.2)**: Call `getLocations` method to get an array of Locations from the local db.

```javascript
Woosmap.db.getLocations(getLocationsCallback, errorCallback);

var getLocationCallback = function(locations) {
   console.log(locations.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```


* **Get Visits (User Story 4.2)**: Call `getVisits` method to get an array of Visits from the local db.

```javascript
Woosmap.db.getVisits(getVisitsCallback, errorCallback);

var getVisitsCallback = function(visits) {
   console.log(visits.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Delete Visit (User Story 4.3)**: Call `deleteVisit` method to remove all or a single visit from the local DB. If the `visit` parameter is null or undefined then all the visits will be deleted.

```javascript

var visit = {
	"uuid":"123434-2323-23223-6767",
	"lat": 42,
	"lng": 19
};

Woosmap.db.deleteVisit(visit, deleteCallback, errorCallback);

var deleteCallback = function() {
   console.log("deleted");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Regions (User Story 3.4)**: Call `getRegions` method to get an array of Regions from the local db.

```javascript
Woosmap.db.getRegions(getRegionsCallback, errorCallback);

var getRegionsCallback = function(regions) {
   console.log(regions.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Zones of Interests (User Story 4.4)**: Call `getZois` method to get an array of ZOIs from the local db.

```javascript
Woosmap.db.getZois(getZoisCallback, errorCallback);

var getZoisCallback = function(zois) {
   console.log(zois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Delete Zone of Interests (User Story 4.5)**: Call `deleteZoi` method to remove all or a single ZOI from the local DB. If the `zoi` parameter is null or undefined then all the ZOIs will be deleted.

```javascript

var zoi = {
	"uuid":"123434-2323-23223-6767"
};

Woosmap.db.deleteZoi(zoi, deleteCallback, errorCallback);

var deleteCallback = function() {
   console.log("deleted");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

**Note:** Android SDK as of now does not expose any method to delete a single ZOI.



### _Class `Woosmap`_

`Woosmap` class will contain methods to monitor location, POIs, regions and visits. 

* **Initializing Woosmap Object**

```javascript
var woosmapSettings = {
        privateKeyWoosmapAPI: "<<WOOSMAP_KEY>>", 
        privateKeyGMPStatic: "<<GOOGLE_KEY>>",
        trackingEnable: true,
        searchAPIEnable: true,
        distanceAPIEnable: true,
        modeHighFrequencyLocation: true,
        modeDistance: "driving"
};

Woosmap.initialize(woosmapSettings, onSuccess, onError);

var onSuccess = function() {
    console.log("success");
};

var onError = function(error) {
    alert('message: ' + error.message);
};

```

* **Track location**: Call `watchLocation` method. Method will invoke callback and pass a location object as a parameter. Method will return a `watchId`. This id can be used to remove a callback.

```javascript

//Start tracking locations
var watchId = Woosmap.watchLocation(locationCallback, errorCallback);

var locationCallback = function(location) {
    alert('Latitude: '          + location.lat          + '\n' +
          'Longitude: '         + location.lng         	+ '\n' +
          'Accuracy: '          + location.accuracy     + '\n' +
          'Speed: '             + location.speed        + '\n' +
          'Timestamp: '         + location.timestamp    + '\n');
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching location
Woosmap.clearLocationWatch(watchId, onSuccess, onError);
```

* **Track search API**: Call `watchSearchApi` method to track search API. Method will invoke a callback with `POI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchSearchAPI(searchCallback, errorCallback);

var searchCallback = function(poi) {
   console.log(poi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearSearchApiWatch(watchId, onSuccess, onError);
```


* **Track Distance API**: Call `watchDistanceApi` method to track distance API. Method will invoke a callback with `DistanceAPI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchDistanceApi(distanceApiCallback, errorCallback);

var distanceApiCallback = function(distanceApi) {
   console.log(distanceApi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearDistanceApiWatch(watchId, onSuccess, onError);
```

* **Track Distance API**: Call `watchDistanceApi` method to track distance API. Method will invoke a callback with `DistanceAPI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchDistanceApi(distanceApiCallback, errorCallback);

var distanceApiCallback = function(distanceApi) {
   console.log(distanceApi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearDistanceApiWatch(watchId, onSuccess, onError);
```


* **Track Visits**: Call `watchVisits` method to track Visits. Method will invoke a callback with `Visit` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchVisits(visitCallback, errorCallback);

var visitCallback = function(visit) {
   console.log(visit);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearVisitsWatch(watchId, onSuccess, onError);
```


* **Track Regions**: Call `watchRegions` method to track Regions. Method will invoke a callback with `Region` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchRegions(regionCallback, errorCallback);

var regionCallback = function(region) {
   console.log(visit);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearRegionsWatch(watchId, onSuccess, onError);
```

* **Add Regions**: Call `addRegion` method to add region that you want to monitor. Method will accept an object following attributes.
	* `regionId` - Id of the region
	* `lat` - Latitude
	* `lng` - Longitude
	* `radius` - Radius in meters

```javascript

var regionInfo = {
	"regionId": "rue_tolbiac",
	"lat": 48.82862170908377,
	"lng": 2.3729680825540838,
	"radius": 10,
};

Woosmap.addRegion(regionInfo, addRegionCallback, errorCallback);

var addRegionCallback = function() {
   console.log("success");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```


* **Remove Region**: Call `removeRegion` method to add region that you want to monitor. Method will accept following parameter. Passing null value to `regionId` will remove all the regions.
	* `regionId` - Id of the region
	
```javascript
Woosmap.removeRegion("rue_tolbiac", removeRegionCallback, errorCallback);

var removeRegionCallback = function() {
   console.log("success");
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

---

### _Class `Woosmap.db`_

`Woosmap.db` class will contain methods to fetch POIs, regions and visits from the local device DB. 


* **Get POIs**: Call `getPois` method to get an array of POIs from the local db.

```javascript
Woosmap.db.getPois(getPoisCallback, errorCallback);

var getPoisCallback = function(pois) {
   console.log(pois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Locations**: Call `getLocations` method to get an array of Locations from the local db.

```javascript
Woosmap.db.getLocations(getLocationsCallback, errorCallback);

var getLocationCallback = function(locations) {
   console.log(locations.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```


* **Get Visits**: Call `getVisits` method to get an array of Visits from the local db.

```javascript
Woosmap.db.getVisits(getVisitsCallback, errorCallback);

var getVisitsCallback = function(visits) {
   console.log(visits.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Regions**: Call `getRegions` method to get an array of Regions from the local db.

```javascript
Woosmap.db.getRegions(getRegionsCallback, errorCallback);

var getRegionsCallback = function(regions) {
   console.log(regions.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Zones of Interests**: Call `getZois` method to get an array of ZOIs from the local db.

```javascript
Woosmap.db.getZois(getZoisCallback, errorCallback);

var getZoisCallback = function(zois) {
   console.log(zois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

