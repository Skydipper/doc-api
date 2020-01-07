# Geodescriber

Geodescriber returns a text description of any Geostore or valid geojson area, in any langunage, dynamically.
Responses from Geodescriber have been tailored to different purposes. The (optional) argument `app` controls which flavour
description you will return.

The code for Geodescriber is [hosted on Github](https://github.com/Skydipper/Geodescriber).

## Call Geodescriber with a Geostore ID

You can return a response from the Geodescriber by providing a `geostore` paramter in your *GET* request.
You can change the language of the response via the `lang` flag, using the [ISO-2 codes](https://www.sitepoint.com/iso-2-letter-language-codes/).

```bash
curl --location --request GET 'https://api.skydipper.com/api/v1/geodescriber?geostore=<ID_HASH>&template=False&app=skydipper&lang=en'
```

> Example Response

```json
{
   "data":{
      "description":"The region's habitat is comprised of Cantabrian mixed forests. This region has no Intact Forest. The area has a predominantly warm and temperate climate with dry summers. It is part of the Temperate Broadleaf and Mixed Forests biome. The location is mostly land area with a large proportion of marine area. Area of 12,387km² located in a predominanty lowland area.",
      "description_params":{},
      "lang":"en",
      "stats":{
         "biome":{"4":1082227.4941176388},
         "ecoregion":{"648":1082227.4941176388},
         "intact2016":{"0":1666560.2431372453},
         "isMountain":{"0":1603363.7882352876,
                       "1":63196.454901960824},
         "koppen":{"32":222131.647058824,
                   "35":1222652.1764705782},
         "seaLandFreshwater":{"0":1094287.9294117563,
                              "1":572272.3137254902}
               },
      "title":"Area in Galicia, Spain",
      "title_params":{}
      }
}
```

## Geodescriber from valid GeoJSON

If the geometry does not correspond to a Geostore object, and you do not wish to create one, you can post a valid
geojson directly to the Geodescriber service and return a response.

```bash
curl --location --request POST 'https://api.skydipper.com/v1/geodescriber/geom?lang=en&app=skydipper' \
--header 'Content-Type: application/json' \
--data-raw '{"geojson":{"type":"FeatureCollection","features":[{"type":"Feature","properties":{},"geometry":{"type":"Polygon","coordinates":[[[-8.749999866114031,43.86562279054269],[-8.500000104532665,43.86562279054269],[-8.2500003429513,43.86562279054269],[-8.000000581369934,43.86562279054269],[-8.000000581369934,42.49423975448128],[-8.2500003429513,42.49423975448128],[-8.500000104532665,42.49423975448128],[-8.749999866114031,42.49423975448128],[-8.999999627695365,42.49423975448128],[-8.999999627695365,43.86562279054269],[-8.749999866114031,43.86562279054269]]]}}]}}'

```

> Example Response

```json
{
   "data":{
      "description":"The region's habitat is comprised of Cantabrian mixed forests. This region has no Intact Forest. The area has a predominantly warm and temperate climate with dry summers. It is part of the Temperate Broadleaf and Mixed Forests biome. The location is mostly land area with a large proportion of marine area. Area of 12,387km² located in a predominanty lowland area.",
      "description_params":{},
      "lang":"en",
      "stats":{
         "biome":{"4":1082227.4941176388},
         "ecoregion":{"648":1082227.4941176388},
         "intact2016":{"0":1666560.2431372453},
         "isMountain":{"0":1603363.7882352876,
                       "1":63196.454901960824},
         "koppen":{"32":222131.647058824,
                   "35":1222652.1764705782},
         "seaLandFreshwater":{"0":1094287.9294117563,
                              "1":572272.3137254902}
               },
      "title":"Area in Galicia, Spain",
      "title_params":{}
      }
}
```