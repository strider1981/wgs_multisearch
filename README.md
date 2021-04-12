<!-- # Woosmap lib -->

<!-- ![Woosmap logo](https://www.webgeoservices.com/wp-content/uploads/2019/10/woosmap_logo-bleu-e1570096219142.png) -->
<img style="display: block; margin: 0 auto;" src="https://www.webgeoservices.com/wp-content/uploads/2019/10/woosmap_logo-bleu-e1570096219142.png">


# Introduction

Multisearch makes it easy to query geographical data by combining [Woosmap Localities](https://developers.woosmap.com/products/localities/search-city-postcode/), [Woosmap Address](https://developers.woosmap.com/products/address-api/get-started/), [Woosmap Store](https://developers.woosmap.com/products/search-api/get-started/) and [Google Places Autocomplete](https://developers.google.com/maps/documentation/javascript/places-autocomplete) APIs in a single lightweight and easy to use library.

+ Supports **callbacks** and **promises**
+ Compatible with **IE11**


# Table of contents
* [Installation](#installation)
* [Getting started](#getting-started)
* [Usage](#usage)
* [Options](#options)
* [Examples](#examples)


# Installation

**93KB** all-in-one browser bundle (dependencies included):

``` html
<script type="text/javascript" src="https://sdk.woosmap.com/multisearch/multisearch.js"></script>
```

You can then instantiate the library with the global `woosmap.multisearch()` function.

### Dependencies:
+ [Fuse.js](https://github.com/krisk/fuse)

# Getting started

``` javascript
const {
  autocompleteMulti,
	autocompleteLocalities,
	autocompleteAddress,
  autocompleteStore,
  autocompletePlaces
	detailsMulti,
	detailsLocalities,
	detailsAddress,
  detailsStore,
  detailsPlaces
} = woosmap.multisearch({
  debounceTime: 100,
  localities: {
    key: 'YOUR_WOOSMAP_API_KEY',
    params: { ... },
  },
  address: {
    key: 'YOUR_WOOSMAP_API_KEY',
    params: { ... },
  },
  store: {
    key: 'YOUR_WOOSMAP_API_KEY',
    params: { ... },
  },
  places: {
    key: 'YOUR_GOOGLE_API_KEY',
    params: { ... },
  },
});
const input = '12 rue de Paris';
const options = {
  apiOrder: ['localities', 'address', 'places'],
  localities: { ... },
  address: { ... },
  store: { ... },
  places: { ... },
};

// Using Promises
autocompleteMulti(input, options).then((results) => console.log(results), (error) => {});
// Using Callbacks
autocompleteMulti(input, options, (error, results) => console.log(results));
```


# Usage

## autocompleteXXX
Requesting autocomplete search. XXX may be:
+ **Localities** : querying [Woosmap Localities](https://developers.woosmap.com/products/localities/search-city-postcode/) autocomplete
+ **Address** : querying [Woosmap Address](https://developers.woosmap.com/products/address-api/autocomplete/) autocomplete
+ **Store** : querying [Woosmap Store](https://developers.woosmap.com/products/search-api/autocomplete/) autocomplete
+ **Places** : querying [Google Places](https://developers.google.com/maps/documentation/places/web-service/autocomplete?hl=id) autocomplete
+ **Multi** : querying the different APIs autocomplete defined in the `apiOrder` list. Depending on the `fallbackBreakpoint` defined for each API, if the first API does not send revelant enough results, it will query the next one, until results are relevant or no other API is in the list.

`woosmap.autocompleteXXX(input, options, callback)`

+ **input** `string` *Required*:  the input to autocomplete on
+ **options** `Object` *Optional*:  Options of each API. The `options`object contains the API key and a `params` attribute of the API
+ **callback** `Function` *Optional*: `function(error, results)`

<details>
  <summary style="font-weight: bold;">Response</summary>

  ```json
[{
    "api": "localities",
    "description": "M0M 2N0, North Middlesex, Canada",
    "matched_substrings": [
        {
            "offset": 0,
            "length": 1
        },
        {
            "offset": 15,
            "length": 1
        }
    ],
    "types": [
        "postal_code"
    ],
    "id": "rm7TVFwp0w1gIcNl8kxaDPsxqyU=",
    "highlight": "<mark>M</mark>0M 2N0, North <mark>M</mark>iddlesex, Canada",
    "item": {
        // Item as it is sent by the corresponding API
        ...
    },
    "score": 0.001
},
  ...
]
  ```
</details>

## detailsXXX

Retrieve details of an item. XXX may be:
+ **Localities** : querying [Woosmap Localities](https://developers.woosmap.com/products/address-api/geocode/) autocomplete
+ **Address** : querying [Woosmap Address](https://developers.woosmap.com/products/address-api/geocode/) autocomplete
+ **Store** : querying [Woosmap Store](https://developers.woosmap.com/products/search-api/search-query/) autocomplete
+ **Places** : querying [Google Places](https://developers.google.com/maps/documentation/places/web-service/details) autocomplete
+ **Multi** : querying the different APIs autocomplete defined in the `apiOrder` list. Depending on the `fallbackBreakpoint` defined for each API, if the first API does not give revelant enough results, it will query the next one, until results are relevant or no other API is in the list.

`detailsXXX(id, api, callback)`

+ **id** `string` *Required*:  Id of the item to retrieve details from
+ **api** `string` *Required*:  Api name to retrieve details from. Values may be `localities`, `address`, `store`, `places`.
+ **callback** `Function`:  *Optional* `function(error, results)`

<details>
  <summary style="font-weight: bold;">Response</summary>

 ```json
  {
    "geometry": {
        "location": {
            "lat": 42.70863,
            "lng": 19.293745
        }
    },
    "formatted_address": "Montenegro",
    "types": [
        "country"
    ],
    "id": "/2IKUQ2lsZ++AhLu05De9TJa6dU=",
    "name": "Montenegro",
    "item": {
      // Item as it is sent by the corresponding API
       ...
    }
}
}
  ```
</details>

# Options
## Global options

You can globally customize the behavior of the differents APIs, each service has a corresponding key where you can specify its behavior with the `options` object.

You must define a `fallbackBreakpoint` being either `false`or a value from `0` to `1` on each service, which sets the threshold where the service's results will be discarded and another call to the fallback service will be made. A value of `0` indicates that the results must contain at least one perfect match while `1` will match anything. 
If the value is `false`, the API will be always queried and its results merged with the other fallbacking APIs. It may be useful if, for instance, we want to create a fallback between localities, address and places but we always want the matching stores.

Availables options:
+ **debounceTime** `integer` *Optional* (detault 100ms): The amount of time you want the autocomplete function to wait after the last received call before executing the next one.
+ **apiOrder** `array` *Required*: List of the APIs to be called.
+ **localities** `ApiOptions` *Optional*: configuration for Woosmap Localities
+ **address** `ApiOptions` *Optional*: configuration for Woosmap Address
+ **store** `ApiOptions` *Optional*: configuration for Woosmap Store
+ **places** `ApiOptions` *Optional*: configuration for Google Places

`ApiOptions` is an object which allows to specify the options for each API:
+ **key** `string` *Required*: Authentication key to be able to call the API.
+ **fallbackBreakpoint** `bool or float` *Required*: either `false` to prevent the API from being fallbacked or a number between 0 and 1 corresponding to the threashold of fallback.
+ **minInputLength** `integer` *Optional*: Empty result will be sent by the API and no fallback will be triggered if the input length does not reach the minInputLength value.
+ **params** `object` *Optional*: List of the API params to send (for [Woosmap Localities](https://developers.woosmap.com/products/localities/localities-autocomplete/#optional-parameters), [Woosmao Address](https://developers.woosmap.com/products/address-api/autocomplete/#optional-parameters), [Woosmap Store](https://developers.woosmap.com/products/search-api/search-query/#fields), [Google Places](https://developers.google.com/maps/documentation/places/web-service/autocomplete?hl=id#place_autocomplete_requests))


``` javascript
const multisearch = woosmap.multisearch({
        debounceTime: 100,
        apiOrder:['localities', 'address', 'places', 'store'],
        localities: {
          key: 'key',
          fallbackBreakpoint: 0.3,
          minInputLength: 3,
          params: {
            types: ['country', 'postal_code'],
          },
        },
        address: {
          key: 'key',
          fallbackBreakpoint: 0.5,
          minInputLength: 6,
          params: {
            components: {
              country: ['FRA'],
            },
          },
        },
        places: {
          key: 'key',
          fallbackBreakpoint: 1,
        },
        store: {
          fallbackBreakpoint: false,
          key: 'key',
        }
      });
```

## autocompleteMulti options

Each time autocompleteMulti is called, options can be passed. The format of this parameter is the same as the global options.
**Per call options is merged with global `options`**: global options, and the options parameter will be merged so that you can overwrite some values.

```javascript
const results = multisearch.autocompleteMulti('12 rue de Paris', {
  apiOrder:['address'],
  address: {
    params: {
      components: {
        country: ['FRA'],
      },
    },
  }
});
```

## autocompleteLocalities, autocompleteAddress, autocompleteStore, autocompletePlaces options

You can customize the calls to the different autocomplete apis on a per call basis with the `options` parameter.
**Per call options is merged with global `options[api]`**: global options of a specific api, and the options parameter will be merged so that you can overwrite some values when calling this API.

```javascript
const results = multisearch.autocompleteLocalities('12 rue de Paris', {
  params: {
    types: ['country', 'postal_code'],
  },
});
```

