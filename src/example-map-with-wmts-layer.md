---
title: Example Map with WTMS Layer
toc: false
---
# Example Map with WTMS Layer

```js
const div = display(document.createElement("div"));
div.style = "height: 400px;";

const map = L.map(div)
  .setView([46.55, 6.632273], 12);

// Base layer
var baseLayer = L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
  attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
})
  .addTo(map);

var tmsLayer = L.tileLayer('https://geo-timemachine.epfl.ch/geoserver/gwc/service/wmts/rest/TimeMachine:1831_Berney/{style}/{TileMatrixSet}/{TileMatrixSet}:{z}/{y}/{x}?format=image/png', {
    tms: false,
    style: 'raster',
    format: 'image/png',
    TileMatrixSet: 'EPSG:900913x2',
    attribution: '&copy; <a href="https://www.epfl.ch/schools/cdh/time-machine-unit/">EPFL Time Machine Unit</a>'
}).addTo(map);

// Crate a control to switch between layers
const layerControl = L.control.layers().addTo(map);

layerControl.addBaseLayer(baseLayer, "OSM");
layerControl.addBaseLayer(tmsLayer, "TMS Layer");
```
