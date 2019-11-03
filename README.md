# koop-provider-geojson

This project can be used to transform GeoJSON files into ArcGIS Feature Services on the fly.

[Live demo](http://www.arcgis.com/home/webmap/viewer.html?source=sd&panel=gallery&suggestField=true&url=https://esri-es-etl-crgjcqnzug.now.sh/koop-provider-geojson/aHR0cDovL2dlb3NlcnZlci52aWxsYW51ZXZhZGVsYXNlcmVuYS5lcy9nZW9zZXJ2ZXIvd2ZzL293cz9zZXJ2aWNlPVdGUyZ2ZXJzaW9uPTEuMC4wJnJlcXVlc3Q9R2V0RmVhdHVyZSZ0eXBlTmFtZT1MRzNfV1NfTWFwUHVibGlzaF9wdWJsaWMlM0F2dmFfY29tZXJjaW9fY29tZXJjaW9zXzEwNSZzcnNOYW1lPUVQU0clM0E0MjU4Jm91dHB1dEZvcm1hdD1hcHBsaWNhdGlvbiUyRmpzb24=/FeatureServer/0) with a dataset of [City Shops](http://geoserver.villanuevadelaserena.es/geoserver/wfs/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=LG3_WS_MapPublish_public%3Avva_comercio_comercios_105&srsName=EPSG%3A4258&outputFormat=application%2Fjson) from [opendata.villanuevadelaserena.es](http://opendata.villanuevadelaserena.es/).

> Note in case it doesn't work try with [this local copy](./data/City_Shops_Villa_nueva_de_la_serena.geojson): [live demo](http://www.arcgis.com/home/webmap/viewer.html?source=sd&panel=gallery&suggestField=true&url=https://esri-es-etl-crgjcqnzug.now.sh/koop-provider-geojson/aHR0cDovL2VzcmktZXMuZ2l0aHViLmlvL2dlb2pzb24yZnMtc2VydmljZS9kYXRhL0NpdHlfU2hvcHNfVmlsbGFfbnVldmFfZGVfbGFfc2VyZW5hLmdlb2pzb24=/FeatureServer/0) using a copy of the dataset

# How does it works?

1. You need a geojson dataset accesible though a public URL, for example: [the City Shops](http://esri-es.github.io/koop-provider-geojson-service/data/City_Shops_Villa_nueva_de_la_serena.geojson)

2. Then, you need to do a Base64 encode of the URL and replace any remaining character '/' for '_'. With JavaScript it can be done using the [btoa function](https://developer.mozilla.org/en-US/docs/Web/API/WindowBase64/Base64_encoding_and_decoding) ([check this JS snippet](#snippet-js-to-encode-the-url)).

3. Then you just need to replace the result of the encoding here: `https://esri-es-etl-crgjcqnzug.now.sh/koop-provider-geojson/<ENCODED_URL>/FeatureServer/0`

4. Now you are ready to load it using the [ArcGIS Web Map Viewer](https://www.arcgis.com/home/webmap/viewer.html) it allows you to "[Add Layer from Web](https://doc.arcgis.com/en/arcgis-online/create-maps/add-layers.htm)"

# Why did we did this?

"Add Layer from Web" allow you to reference and load layers of types: WMS, WMTS, WFS, Tile layers, KML files, GeoRSS files, CSV and Bing Maps, but it still doesn't support to load GeoJSON directly inside a [Web Map](https://developers.arcgis.com/web-map-specification/) without hosting and transforming it on ArcGIS. So this way you can do it.

> **Note**: we are aware that the JavaScript 4.x already support [GeoJSON layers](https://developers.arcgis.com/javascript/latest/api-reference/esri-layers-GeoJSONLayer.html), but this is not the same use case because we are trying to load the data **on a Web Map**.

## Snippet JS to encode the URL

You can run this within the JS console to

```js
// Change set a value for `targetUrl` or leave it blank to use location.href
let targetUrl = '';

String.prototype.replaceAll = function(search, replacement) {
    var target = this;
    return target.replace(new RegExp(search, 'g'), replacement);
};

(function(targetUrl){
    url = targetUrl? targetUrl: location.href;
    url = btoa(url)
    path = `${url.replaceAll('/','_')}/FeatureServer/0`

    console.log(`https://esri-es-etl-crgjcqnzug.now.sh/koop-provider-geojson/${path}`)
    console.log(`http://localhost:8080/koop-provider-geojson/${path}`)
})(targetUrl)


```

# Contributions

This is only a sketch of how to solve this issue, we would love to improve this project adding support to other formats like Shapefiles, so any issues and pull requests are more than welcome.

# Credits
Original code base on the [koop-provider-sample](https://github.com/koopjs/koop-provider-sample)
