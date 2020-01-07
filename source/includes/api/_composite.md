# Composite Imagery

The Composite service enables the creation of on-the-fly composites based on either Landsat-8, or Sentinel-2
and a Geostore geometry ID. Composites can be returned in a variety of formats, either as url links to
thumbnail and slippy map (z/x/y) tile assets, or as a zip folder containing image assets.

Band visulisations can be given as argument to visulise any bands of interest in RGB space.
Digital Elevation Model (DEM) image assets can also be returned with the `get_dem`=True flag.

Code for the Composite service is [hosted on Github](https://github.com/Skydipper/Composite).


## Thumbnails and slippy maps

By default, the service accepts a Gestore id hash as an argument via the `geostore` param in a *GET* request.
The response is JSON containing urls (with tokens valid for 2 days), linking to Z/X/Y type (slippy) maps, as well as
a thumbnail, and a greyscale Digital Elevation Model (DEM) output (if `get_dem` is set to *True*).


```python
params = {"geostore": "<geostore_id>",
          "get_dem": True,
          "date_range": "[2018-01-01, 2018-12-01]",
          "thumb_size": "[500, 500]",
          "instrument": "landsat",
          "cloudscore_thresh": 5,
          "band_vizz": "{'bands': ['B4', 'B3', 'B2'], 'min': 0, 'max': 0.4}",
          "get_files": False}

r = requests.get(f"https://api.skydipper.com/v1/composite-service", params=params)
print(r.json())

```

> Response

```json
{
  "attributes": {"dem": "https://earthengine.googleapis.com/api/thumb?thumbid=6162ac5f8444eed070b537732711b688&token=XXXX",
  "thumb_url": "https://earthengine.googleapis.com/api/thumb?thumbid=580652e722a7660ab7137ffb21ce664e&token=XXXXX",
  "tile_url": "https://earthengine.googleapis.com/map/1eaa150375fa8c9b1e00aa78f754f9d1/{z}/{x}/{y}?token=XXXXX",
  "zonal_stats": "None"},
  "id": "None",
  "type": "composite_service"
}
```




## Downloading Image Assets

Sometimes you want more than a thumnail and web map tiles. If you want to build 3D models with these assets you will
need to download the composite as a surface texture and apply that texture to a surface (ideally using the DEM
to deform the surface to show height also). To do this you will need to hit the service with `get_files`=*True*, and then
unzip the assets folder that is returned in the response.



```python
params = {"geostore": "<geostore_id>",
          "get_dem": True,
          "date_range": "[2019-01-01, 2019-12-01]",
          "thumb_size": "[250, 250]",
          "instrument": "landsat",
          "get_files": True}

r = requests.get(f"https://api.skydipper.com/v1/composite-service", params=params)
print(r.json())
```

<aside class="notice">
The resolution of the downloaded images can be controled via the thumb_size parameter. E.g. if a 500x500 pixel image is required, pass the argument
thumb_size=[500,500].
</aside>