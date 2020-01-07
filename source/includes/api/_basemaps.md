# Basemaps

The Basemap microservice serves pre-calculated and dynamic tiles for Layer objects and several pre-built styles.
The code for this service can be found [here](https://github.com/Skydipper/Basemaps).

## Annual Landsat Basemaps

We have created satellite basemaps based off of the NASA/USGS Landsat satellite collection. These are avaiable as [slippy map tiles](https://wiki.openstreetmap.org/wiki/Slippy_map_tilenames).
We are continuing to add years of coverage to our Landsat Basemap collection. The collection we have currently processed
is avaiable via `https://api.skydipper.com/v1/landsat/<year>/<z>/<x>/<y>`.

The service mixes pre-cached and dynamic tiles. The dynamic tiles kick-in at z>11.


```python
import requests
url = "http://api.skydipper.com/v1/basemaps/landsat/2016/14/8473/7643"
r = requests.get(url)

print(r.status_code)
with open('./image_test.jpg', 'wb') as handler:
    handler.write(r.content)
```

## Layer Basemaps

Appropriate layers in Skydipper (i.e. geospatial data, with either the EE or CartoDB provider and visulisation properties)
can be visulised as map tiles by calling `https://api.skydipper.com/v1/basemaps/layer/<layer_id>/<z>/<x>/<y>`.

<aside class="notice">
Rember, you can set the styles that control how the layer will appear using inside the Layer object. The style you set
should use either CartoCSS, mapbox vector styels, or the open standard SLD method (for rasters) depending on the data.
</aside>

```python
import requests
url = "http://api.skydipper.com/v1/basemaps/layer/e7070d5f-3d38-46b1-86eb-e98782da55dd/14/8473/7643"
r = requests.get(url)

print(r.status_code)
with open('./image_test.jpg', 'wb') as handler:
    handler.write(r.content)
```

## Movie tiles

Coming soon.