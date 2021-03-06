# gps-scramble

[![npm version](http://img.shields.io/npm/v/gps-scramble.svg?style=flat)](https://npmjs.org/package/gps-scramble "View this project on npm")
[![Status](https://travis-ci.org/scharkee/gps-scramble.svg?branch=master)](https://travis-ci.org/scharkee/gps-scramble)
[![Coverage Status](https://coveralls.io/repos/github/Scharkee/gps-scramble/badge.svg?branch=master)](https://coveralls.io/github/Scharkee/gps-scramble?branch=master)
[![David](https://img.shields.io/david/scharkee/gps-scramble.svg)](https://david-dm.org/scharkee/gps-scramble)

A tool for controlled randomization/spoofing of GPS coordinates.

## Features

- Generate similar coordinates within a distance of given coordinates
- Location name based coordinate generation (geocoding), resolve coordinates by location name
- Generate the coordinates of a random establishment near the given coordinates

## Install

```bash
$ npm install gps-scramble
```

## Usage

```js
const { Scrambler } = require("gps-scramble");
let scrambler = new Scrambler([40.758896, -73.98513]);
console.log(scrambler.within(100, "m")); // randomized location within 100 meters from given coordinates.
console.log(scrambler.near()); // randomized location near given coordinates.
```

## Advanced usage (Geocoding)

```js
const { ScramblerAsync } = require("gps-scramble");
let scrambler = new ScramblerAsync("Times Square");

let location = await scrambler.within(100, "m");
console.log(location.x, location.y); // randomized location within 100 meters from Times Square

location = await scrambler.near();
console.log(location.x, location.y); // randomized location near Times Square

location = await scrambler.nearbyEstablishment();
console.log(location.x, location.y); // randomized location of a business near Times Square
```

## Geocoding support

To enable geocoding support (powered by Bing Maps Geocoding API), you must get an API key.
The process of getting a key is described [here](https://docs.microsoft.com/en-us/bingmaps/getting-started/bing-maps-dev-center-help/getting-a-bing-maps-key)

The key must be loaded as an enviromental variable named `BING_API_KEY`.

## Units

Supported units are: "mm" - milimeters, "cm" - centimeters, "m" - meters (default), "dm" - decimeters, "km" - kilometers.

## API

[API reference docs.](https://scharkee.github.io/gps-scramble/)

All gps-scrambler methods return Location objects, which contain coordinates.

They can be accessed like this:

```js
const { Scrambler } = require("gps-scramble");
let scrambler = new Scrambler([40.758896, -73.98513]);
let location = scrambler.near();

location.x; // X coordinate
location.y; // Y coordinate
location[0]; // X coordinate alternative
location[1]; // Y coordinate alternative
```

The same method for access works with scramblers themselves. Their initial states can be accessed like so:

```js
const { Scrambler } = require("gps-scramble");
let scrambler = new Scrambler([40.758896, -73.98513]);

scrambler.x; // initial X coordinate
scrambler.y; // initial Y coordinate
// ...
```

### Support

Submit bugs and requests through the project's issue tracker:

[![Issues](http://img.shields.io/github/issues/Scharkee/gps-scramble.svg)](https://github.com/Scharkee/gps-scramble/issues)
