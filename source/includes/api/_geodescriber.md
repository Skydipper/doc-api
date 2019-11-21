# Geodescriber

## What is Geodescriber?

Geodesriber is blah.


<aside class="notice">
Remember — All endpoint of geostore don't need that you are authenticated.
</aside>

## Call Geodescriber

You can use it in

> To create a Geostore, you have to do a POST query with the following body:

```shell
curl -X POST https://api.skydipper.com/v1/geodescriber \
-H "Content-Type: application/json"  -d \
 '{
   "geojson": <yourGeoJSONObject>
  }'
```

> Real example

```shell
curl -X POST https://api.skydipper.com/v1/geostore \
-H "Content-Type: application/json"  -d \
 '{
   "geojson":{
      "type":"FeatureCollection",
      "features":[
         {
            "type":"Feature",
            "properties":{

            },
            "geometry":{
               "type":"LineString",
               "coordinates":[
                  [
                     -3.9942169189453125,
                     41.044922165782175
                  ],
                  [
                     -3.995418548583985,
                     41.03767166215326
                  ],
                  [
                     -3.9842605590820312,
                     41.03844854003296
                  ],
                  [
                     -3.9844322204589844,
                     41.04589315472392
                  ],
                  [
                     -3.9942169189453125,
                     41.044922165782175
                  ]
               ]
            }
         },
         {
            "type":"Feature",
            "properties":{

            },
            "geometry":{
               "type":"Polygon",
               "coordinates":[
                  [
                     [
                        -4.4549560546875,
                        40.84706035607122
                     ],
                     [
                        -4.4549560546875,
                        41.30257109430557
                     ],
                     [
                        -3.5211181640624996,
                        41.30257109430557
                     ],
                     [
                        -3.5211181640624996,
                        40.84706035607122
                     ],
                     [
                        -4.4549560546875,
                        40.84706035607122
                     ]
                  ]
               ]
            }
         }
      ]
   }
}'
```

The response will be 200 if the geostore saves correctly and returns the geostore object with all information:

> Example response

```json
{
   "data":{
      "type":"geoStore",
      "id":"c9bacccfb9c3fe225dc67545bb93a5cb",
      "attributes":{
         "geojson":{
            "features":[
               {
                  "type":"Feature",
                  "geometry":{
                     "type":"Polygon",
                     "coordinates":[
                        [
                           [
                              -4.4549560546875,
                              40.84706035607122
                           ],
                           [
                              -4.4549560546875,
                              41.30257109430557
                           ],
                           [
                              -3.5211181640624996,
                              41.30257109430557
                           ],
                           [
                              -3.5211181640624996,
                              40.84706035607122
                           ],
                           [
                              -4.4549560546875,
                              40.84706035607122
                           ]
                        ]
                     ]
                  }
               }
            ],
            "crs":{

            },
            "type":"FeatureCollection"
         },
         "hash":"c9bacccfb9c3fe225dc67545bb93a5cb",
         "provider":{

         },
         "areaHa":397372.34122605197,
         "bbox":[
            -4.4549560546875,
            40.84706035607122,
            -3.5211181640624996,
            41.30257109430557
         ]
      }
   }
}
```
