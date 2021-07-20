# Woosmap geofencing Cordova Plugin 
### _Class `Woosmap`_

`Woosmap` class will contain methods to moniter location, POIs, regions and visits. 

* **Initializing Woosmap Object**

```javascript
var woosmapSetting = {
        privateKeyWoosmapAPI: "<<WOOSMAP_KEY>>", 
        privateKeyGMPStatic: "<<GOOGLE_KEY>>",
        trackingEnable: true,
        searchAPIEnable: true,
        distanceAPIEnable: true,
        modeHighFrequencyLocation: true,
        modeDistance: "driving"
};

Woosmap.initialize(onSuccess,onError,woosmapSetting);

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
var watchId = Woosmap.watchLocation(locationCallback,errorCallback);

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
Woosmap.clearLocationWatch(onSuccess, onError, watchId);
```

* **Track search API**: Call `watchSearchApi` method to track search API. Method will invoke a callback with `POI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchSearchAPI(searchCallback,errorCallback);

var searchCallback = function(poi) {
   console.log(poi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearSearchApiWatch(onSuccess, onError, watchId);
```


* **Track Distance API**: Call `watchDistanceApi` method to track distance API. Method will invoke a callback with `DistanceAPI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchDistanceApi(distanceApiCallback,errorCallback);

var distanceApiCallback = function(distanceApi) {
   console.log(distanceApi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearDisatnceApiWatch(onSuccess, onError, watchId);
```

* **Track Distance API**: Call `watchDistanceApi` method to track distance API. Method will invoke a callback with `DistanceAPI` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchDistanceApi(distanceApiCallback,errorCallback);

var distanceApiCallback = function(distanceApi) {
   console.log(distanceApi);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearDisatnceApiWatch(onSuccess, onError, watchId);
```


* **Track Visits**: Call `watchVisits` method to track Visits. Method will invoke a callback with `Visit` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchVisits(visitCallback,errorCallback);

var visitCallback = function(visit) {
   console.log(visit);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearVisitsWatch(onSuccess, onError, watchId);
```


* **Track Regions**: Call `watchRegions` method to track Regions. Method will invoke a callback with `Region` object. Method will return a watch id which can be used later to remove the callback.

```javascript
var watchId = Woosmap.watchRegions(regionCallback,errorCallback);

var regionCallback = function(region) {
   console.log(visit);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

//Stop watching
Woosmap.clearRegionsWatch(onSuccess, onError, watchId);
```

* **Add Regions**: Call `addRegion` method to add region that you want to monitor. Method will accept following parameter.
	* `regionId` - Id of the region
	* `lat` - Latitude
	* `lng` - Longitude
	* `radius` - Radius in meters

```javascript
Woosmap.addRegion(addRegionCallback,errorCallback,"rue_tolbiac",48.82862170908377, 2.3729680825540838,10);

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
Woosmap.removeRegion(removeRegionCallback,errorCallback,"rue_tolbiac");

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
Woosmap.db.getPois(getPoisCallback,errorCallback);

var getPoisCallback = function(pois) {
   console.log(pois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Locations**: Call `getLocations` method to get an array of Locations from the local db.

```javascript
Woosmap.db.getLocations(getLocationsCallback,errorCallback);

var getLocationCallback = function(locations) {
   console.log(locations.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```


* **Get Visits**: Call `getVisits` method to get an array of Visits from the local db.

```javascript
Woosmap.db.getVisits(getVisitsCallback,errorCallback);

var getVisitsCallback = function(visits) {
   console.log(visits.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Regions**: Call `getRegions` method to get an array of Regions from the local db.

```javascript
Woosmap.db.getRegions(getRegionsCallback,errorCallback);

var getRegionsCallback = function(regions) {
   console.log(regions.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

* **Get Zones of Interests**: Call `getZois` method to get an array of ZOIs from the local db.

```javascript
Woosmap.db.getZois(getZoisCallback,errorCallback);

var getZoisCallback = function(zois) {
   console.log(zois.length);
};

var errorCallback = function(error) {
    alert('message: ' + error.message);
};

```

