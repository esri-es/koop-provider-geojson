# geojson2fs-service

This project can be used to transform GeoJSON files into ArcGIS Feature Services on the fly.

[Live demo](http://www.arcgis.com/home/webmap/viewer.html?source=sd&panel=gallery&suggestField=true&url=https://esri-es-etl-crgjcqnzug.now.sh/geojson2fs/aHR0cDovL2dlb3NlcnZlci52aWxsYW51ZXZhZGVsYXNlcmVuYS5lcy9nZW9zZXJ2ZXIvd2ZzL293cz9zZXJ2aWNlPVdGUyZ2ZXJzaW9uPTEuMC4wJnJlcXVlc3Q9R2V0RmVhdHVyZSZ0eXBlTmFtZT1MRzNfV1NfTWFwUHVibGlzaF9wdWJsaWMlM0F2dmFfY29tZXJjaW9fY29tZXJjaW9zXzEwNSZzcnNOYW1lPUVQU0clM0E0MjU4Jm91dHB1dEZvcm1hdD1hcHBsaWNhdGlvbiUyRmpzb24=/FeatureServer/0) with a dataset of [City Shops](http://geoserver.villanuevadelaserena.es/geoserver/wfs/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=LG3_WS_MapPublish_public%3Avva_comercio_comercios_105&srsName=EPSG%3A4258&outputFormat=application%2Fjson) from [opendata.villanuevadelaserena.es](http://opendata.villanuevadelaserena.es/).

> Note in case it doesn't work try with [this local copy](./data/City_Shops_Villa_nueva_de_la_serena.geojson): [live demo](http://www.arcgis.com/home/webmap/viewer.html?source=sd&panel=gallery&suggestField=true&url=https://esri-es-etl-crgjcqnzug.now.sh/geojson2fs/aHR0cDovL2VzcmktZXMuZ2l0aHViLmlvL2dlb2pzb24yZnMtc2VydmljZS9kYXRhL0NpdHlfU2hvcHNfVmlsbGFfbnVldmFfZGVfbGFfc2VyZW5hLmdlb2pzb24=/FeatureServer/0) using a copy of the dataset

# How does it works?

1. You need a geojson dataset accesible though a public URL, for example: [the City Shops](http://esri-es.github.io/geojson2fs-service/data/City_Shops_Villa_nueva_de_la_serena.geojson)
2. Then, you need to do a Base64 encode of the URL
2.1. With JavaScript can be done with the [btoa](https://developer.mozilla.org/en-US/docs/Web/API/WindowBase64/Base64_encoding_and_decoding) function
2.2. You can also use online free encoders like [base64encode.net](https://www.base64encode.net/)
3. Then you just need to replace the result of the encoding here: `https://esri-es-etl-crgjcqnzug.now.sh/geojson2fs/<ENCODED_URL>/FeatureServer/0`

# When to use it

When you are using the [ArcGIS Web Map Viewers](https://www.arcgis.com/home/webmap/viewer.html) it allows you to "Add Layer from Web" of types: WMS, WMTS, WFS, Tile layers, KML files, GeoRSS files, CSV and Bing Maps, but it still doesn't support to load GeoJSON directly in a [Web Map](https://developers.arcgis.com/web-map-specification/) without hosting and transforming it on ArcGIS. So this way you can reference and load a GeoJSON hosted and maintained by a third party into a Web Map.

> Note: we are aware that the JavaScript 4.x already support [GeoJSON layers](https://developers.arcgis.com/javascript/latest/api-reference/esri-layers-GeoJSONLayer.html), but this is not the same use case.

# Contributions

This is only a sketch

# Credits
Original code base on the [koop-provider-sample](https://github.com/koopjs/koop-provider-sample)
