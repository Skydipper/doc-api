# Dataset

## What is a Dataset?

A dataset abstracts the data that can be obtained from several sources into a common interface. There are several data providers supported in the API, and each of those has a different provider. Datasets can belong to several applications.

## Supported dataset sources

### Third party Dataset connectors

For data stored on third party services.

#### Carto

**`(connectorType: 'rest', provider: 'cartodb')`**<br>
[CARTO](https://www.carto.com) is an open, powerful, and intuitive map platform for discovering and predicting the key insights underlying the location data in our world.

### ArcGIS Feature service

**`(connectorType: 'rest', provider: 'featureservice')`** <br>
[ArcGIS](https://www.arcgis.com/features/index.html) for server is a Complete, Cloud-Based Mapping Platform.

### Google Earth Engine

**`(connectorType: 'rest', provider: 'gee')`** <br>
[Google Earth Engine](https://earthengine.google.com/) combines a multi-petabyte catalog of satellite imagery and geospatial datasets with planetary-scale analysis capabilities and makes it available for scientists, researchers, and developers to detect changes, map trends, and quantify differences on the Earth's surface.

## Getting all datasets

This endpoint will allow to get all datasets available in the API:


```shell
curl -X GET https://api.skydipper.com/v1/dataset
```

> Response:

```json
{
    "data": [
    {
      "id": "098b33df-6871-4e53-a5ff-b56a7d989f9a",
      "type": "dataset",
      "attributes": {
        "name": "Subnational Political Boundaries",
        "slug": "Politcial-Boundaries-GADM-adminitrative-level-1-1490086842541",
        "type": "tabular",
        "subtitle": "GADM",
        "application": ["skydipper"],
        "dataPath": null,
        "attributesPath": null,
        "connectorType": "rest",
        "provider": "cartodb",
        "userId": "57a0aa1071e394dd32ffe137",
        "connectorUrl": "https://wri-01.carto.com/tables/gadm28_adm1/public",
        "tableName": "gadm28_adm1",
        "status": "saved",
        "published": true,
        "overwrite": false,
        "verified": false,
        "blockchain": null,
        "subscribable": null,
        "mainDateField": null,
        "env": "production",
        "geoInfo": true,
        "protected": true,
        "legend": {
          "date": [],
          "region": [],
          "country": [],
          "nested": []
        },
        "clonedHost": null,
        "errorMessage": null,
        "taskId": null,
        "updatedAt": "2018-11-21T13:54:56.285Z",
        "dataLastUpdated": null
      }
    },
    ...
  ],
  "links": {
    "self": "http://api.skydipper.com/v1/dataset?page[number]=1&page[size]=10",
    "first": "http://api.skydipper.com/v1/dataset?page[number]=1&page[size]=10",
    "last": "http://api.skydipper.com/v1/dataset?page[number]=99&page[size]=10",
    "prev": "http://api.skydipper.com/v1/dataset?page[number]=1&page[size]=10",
    "next": "http://api.skydipper.com/v1/dataset?page[number]=2&page[size]=10"
  },
  "meta": {
    "total-pages": 99,
    "total-items": 990,
    "size": 10
  }
}
```

### Slug & dataset-id

Datasets have an auto-generated and unique slug and id that allows the user to get, create, update, query or clone that dataset.

The dataset slug and the id cannot be updated even if the name changes.

### Error Message

When a dataset is created the status is set to "pending" by default. Once the adapter validates the dataset, the status is changed to "saved". If the validation fails, the status will be set to "failed" and the adapter will also set an error message indicating the reason.

### Filters

The dataset list provided by the endpoint can be filtered with the following attributes:

Filter        | Description                                                                  | Accepted values
------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
name          | Allow us to filter by name                                                   | any valid text
type          | Allow us to distinguish between tabular and raster datasets                  | `raster` or `tabular`
app           | Aplications to which this dataset is being used                              | Available Aplications like: `["skydipper"]`
connectorType |                                                                              | `rest` (placeholder for future connectors not based in rest)
provider      | Dataset provider this include inner connectors and 3rd party ones            | [A valid dataset provider](##supported-dataset-sources)
userId        | the user who registered the dataset                                          | valid id
status        | the internal dataset status at connection time                               | `pending`, `saved` or `failed`
published     |                                                                              | `true`or `false`
env           | If the dataset is in preproduction envirenment or in production one          | `production`or `preproduction`
overwritted   | If the data can be overwritten (only for being able to make dataset updates) | `true`or `false`
verify        | If this dataset contains data that is verified using blockchain              | `true`or `false`
protected     | If it's a protected layer                                                    | `true`or `false`
geoInfo       | If it contains intersectable geographical info                               | `true`or `false`

> Filtering datasets

```shell
curl -X GET https://api.skydipper.com/v1/dataset?name=birds&provider=cartodb
```

> For inclusive filtering with array props use '@'

```shell
curl -X GET https://api.skydipper.com/v1/dataset?provider=cartodb@gee
```

### Sorting

#### Basics of sorting

The API currently supports sorting by means of the `sort` parameter. 

> Sorting datasets

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=name
```

Multiple sorting criteria can be used, separating them by commas.

> Sorting datasets by multiple criteria

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=name,description
```

You can specify the sorting order by prepending the criteria with either `-` or `+`. By default, `asc` order is assumed.

> Explicit order of sorting

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=-name,+description
```

#### Special sorting criteria

There are two special sorting criteria:

- `metadata`: delegates sorting to the metadata component, sorting by the name field of the metadata.
- `relevance`: delegates sorting to the metadata component, sorting by the datasets which metadata better match the search criteria. Can only be used in conjunction with a `search` parameter. Does not support ascending order. 

Special search criteria must be used as sole sorting criteria, as it's not possible to combine any of them with any other search criteria.

> Sorting datasets with special criteria

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=relevance&status=saved&search=agriculture
```

### Relationships

Available relationships: Any dataset relationship ['metadata']

> Including relationships

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=slug,-provider,userId&status=saved&includes=metadata
```

### Pagination

Field        |         Description          |   Type
------------ | :--------------------------: | -----:
page[size]   | The number elements per page | Number
page[number] |       The page number        | Number

> Paginating the output

```shell
curl -X GET https://api.skydipper.com/v1/dataset?sort=slug,-provider,userId&status=saved&includes=metadata&page[number]=1
curl -X GET https://api.skydipper.com/v1/dataset?sort=slug,-provider,userId&status=saved&includes=metadata&page[number]=2
```

## How to get a specific dataset

> To get a dataset:

```shell
curl -X GET https://api.skydipper.com/v1/dataset/51943691-eebc-4cb4-bdfb-057ad4fc2145
```

> Response:

```shell
{
    "data": {
      "id": "098b33df-6871-4e53-a5ff-b56a7d989f9a",
      "type": "dataset",
      "attributes": {
        "name": "Subnational Political Boundaries",
        "slug": "Politcial-Boundaries-GADM-adminitrative-level-1-1490086842541",
        "type": "tabular",
        "subtitle": "GADM",
        "application": ["skydipper"],
        "dataPath": null,
        "attributesPath": null,
        "connectorType": "rest",
        "provider": "cartodb",
        "userId": "57a0aa1071e394dd32ffe137",
        "connectorUrl": "https://wri-01.carto.com/tables/gadm28_adm1/public",
        "tableName": "gadm28_adm1",
        "status": "saved",
        "published": true,
        "overwrite": false,
        "verified": false,
        "blockchain": null,
        "subscribable": null,
        "mainDateField": null,
        "env": "production",
        "geoInfo": true,
        "protected": true,
        "legend": {
          "date": [],
          "region": [],
          "country": [],
          "nested": []
        },
        "clonedHost": null,
        "errorMessage": null,
        "taskId": null,
        "updatedAt": "2018-11-21T13:54:56.285Z",
        "dataLastUpdated": null
      }
    }
}
```

> To get the dataset including its relationships:

```shell
curl -X GET https://api.skydipper.com/v1/dataset/06c44f9a-aae7-401e-874c-de13b7764959?includes=metadata
```

## Creating a Dataset

To create a dataset, you will need an authorization token. Follow the steps of this [guide](#generate-your-own-oauth-token) to get yours.

To create a dataset, you need to define all of the required fields in the request body. The fields that compose a dataset are:

Field               |                                                      Description                                                       |    Type |                                                                                                                Values |                                          Required
------------------- | :--------------------------------------------------------------------------------------------------------------------: | ------: | --------------------------------------------------------------------------------------------------------------------: | ------------------------------------------------:
name                |                                                      Dataset name                                                      |    Text |                                                                                                              Any Text |                                               Yes
type                |                                                      Dataset type                                                      |    Text |                                                                                                              Any Text |                                                No
subtitle            |                                                    Dataset subtitle                                                    |    Text |                                                                                                              Any Text |                                                No
application         |                                          Applications the dataset belongs to                                           |   Array |                                                                                         Any valid application name(s) |                                               Yes
connectorType       |                                                     Connector type                                                     |    Text |                                                                                                   rest, document, wms |                                               Yes
provider            |                                               The connectorType provider                                               |    Text |                                                           cartodb, feature service, gee |                                               Yes
connectorUrl        |                                                 Url of the data source                                                 |     Url |                                                                                                               Any url |    Yes (except for gee)
tableName           |                                                       Table name                                                       |    Text |                                                                                                  Any valid table name |            No (just for GEE datasets)
data                |                             JSON DATA only for json connector if connectorUrl not present                              |    JSON |                                                                                                            [{},{},{}] | No (just for json if connectorUrl is not present)
dataPath            |                                           Path to the data in a json dataset                                           |    Text |                                                                                                    Any valid JSON key | No (just for json if connectorUrl is not present)
dataAttributes      |                                    Data fields - for json connector if data present                                    |  Object |                                                                                     {"key1": {"type": "string"},... } | No (just for json if connectorUrl is not present)
legend              |                                      Legend for dataset. Keys for special fields                                       |  Object | "legend": {"long": "123", "lat": "123", "country": ["pais"], "region": ["barrio"], "date": ["startDate", "endDate"]}} |                                                No
overwrite           |                                          It allows to overwrite dataset data                                           | Boolean |                                                                                                            true/false |                                                No
published           |                                           To set a public or private dataset                                           | Boolean |                                                                                                            true/false |                                                No
protected           |                           If it's a protected layer (not possible to delete if it's true)                           | Boolean |                                                                                                            true/false |                                                No
verified            |                                    To generate a verified blockchain of the dataset                                    | Boolean |                                                                                                            true/false |                                                No


There are some differences between datasets types.

### Rest-Carto datasets

```shell
curl -X POST https://api.skydipper.com/v1/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
    "connectorType":"rest",
    "provider":"cartodb",
    "connectorUrl":"<cartoUrl>",
    "application":[
     "your", "apps"
    ],
    "name":"Example Carto Dataset"
}'
```

> A real example:

```shell
curl -X POST https://api.skydipper.com/v1/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{
    "connectorType":"rest",
    "provider":"cartodb",
    "connectorUrl":"https://wri-01.carto.com/tables/wdpa_protected_areas/table",
    "application":[
	"skydipper"
    ],
    "name":"World Database on Protected Areas -- Global"
}'
```

<aside class="notice">
    This is an authenticated endpoint!
</aside>

### Rest-ArcGIS feature Service

```shell
curl -X POST https://api.skydipper.com/v1/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{
    "connectorType":"rest",
    "provider":"featureservice",
    "connectorUrl":"https://services.arcgis.com/uDTUpUPbk8X8mXwl/arcgis/rest/services/Public_Schools_in_Onondaga_County/FeatureServer/0?f=json",
    "application":[
	"skydipper"
    ],
    "name":"Uncontrolled Public-Use Airports -- U.S."
}'
```

<aside class="notice">
    This is an authenticated endpoint!
</aside>

### Rest-GEE

```shell
curl -X POST https://api.skydipper.com/v1/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{
    "connectorType":"rest",
    "provider":"gee",
    "tableName": "JRC/GSW1_0/GlobalSurfaceWater"
    "application":[
     "skydipper"
    ],
    "name":"Water occurrence"
}'
```



## Updating a Dataset

In order to modify the dataset, you can PATCH a request. It accepts the same parameters as the _create dataset_ endpoint, and you will need an authentication token.

> An example update request:

```shell
curl -X PATCH https://api.skydipper.com/v1/dataset/<dataset-id> \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json" -d \
'{
    "name": "Another name for the dataset"
}'
```

<aside class="notice">
    This is an authenticated endpoint!
</aside>

## Deleting a Dataset

**When a dataset is deleted the user's applications that were present on the dataset will be removed from it. If this results in a dataset without applications, the dataset itself will be then deleted.**

Datasets can be deleted either by any user with role ADMIN or by the user with role MANAGER that created them. Note that the deletion process cascades; deleting a dataset will also remove all layer, vocabularies, and metadata entities associated with it.

<aside class="warning">
Deleting a dataset removes it permanently! It is recommended that you save a local copy before doing so.
</aside>

```shell
curl -X DELETE https://api.skydipper.com/v1/dataset/<dataset-id> \
-H "Authorization: Bearer <your-token>"
-H "Content-Type: application/json"
```

<aside class="notice">
    This is an authenticated endpoint!
</aside>

## Cloning a Dataset

```shell
curl -X POST https://api.skydipper.com/v1/dataset/5306fd54-df71-4e20-8b34-2ff464ab28be/clone \
-H "Authorization: Bearer <your-token>"
-H "Content-Type: application/json" -d \
'{
  "dataset": {
    "datasetUrl": "/query/5306fd54-df71-4e20-8b34-2ff464ab28be?sql=select%20%2A%20from%20data%20limit%2010",
    "application": [
      "your",
      "apps"
    ]
  }
}'
```

<aside class="notice">
    This is an authenticated endpoint!
</aside>

