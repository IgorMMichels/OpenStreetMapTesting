# My OSM Map

Simple Leaflet + OpenStreetMap starter with geolocation.

## What this does

- Shows a fullscreen map
- Loads OpenStreetMap tiles
- Finds your location and puts a marker there

## How to run

### Option 1: Open directly
Double-click index.html and open in your browser.

### Option 2: Local server
```
npx serve .
```
Then go to http://localhost:3000

### Option 3: Python
```
python -m http.server 8000
```
Then go to http://localhost:8000

## Allow location access

When the browser asks, click "Allow" to let the map find you.

If you deny or geolocation fails, it shows Lisbon (Portugal) as fallback.

## Files

- index.html - the map (everything in one file)