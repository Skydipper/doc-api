# Composite Imagery

## What is the Composite Imagery service?

CI is blah.


## Call the Composite Imagery Service

You can use it in

> To obtain a recent imagery, you have to do a POST query with the following body:

```shell
curl -X POST https://api.skydipper.com/v1/geodescriber \
-H "Content-Type: application/json"  -d \
 '{
   "geojson": <yourGeoJSONObject>
  }'
```

## Obtaining DEM data

You can get Digital Elevation Model data for your service by...