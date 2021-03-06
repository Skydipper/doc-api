# Widget

## What is a Widget?

A widget is a graphic representation of a Dataset's data. Most of them are defined with [Vega grammar](#what-is-vega) but we can also find other custom definitions.

Widgets contain the following fields:

Field        |                         Description                          |    Type
------------ | :----------------------------------------------------------: | ------:
userId       |                       Id of the owner                        |    Text
application  |           Application to which the dataset belongs           |   Array
slug         |               Unique identifier of the widget                |    Text
name         |                      Name of the widget                      |     Url
description  |                  Description of the widget                   |   Array
source       |                Publisher of the original code                |    Text
sourceUrl    |                    Link to publisher page                    |     Url
layerId      |             UuId of the relationship with layer              |  String
dataset      |         UuId of the dataset that the widget belongs          |    Text
authors      |                     Name of the authors                      |    Text
queryUrl     |             Url with the data of the chart shows             |    Text
widgetConfig |                     Custom configuration                     |  Object
template     |   If it's a template (base schema to create other widgets)   | Boolean
default      |   If it's a default widget for the dataset that it belongs   | Boolean
protected    |  If it's a protected widget (not is possible to delete if it's true)   | Boolean
status       |                     Status of the Widget                     |    Text
published    |                   If it's available to use                   |    Text
freeze       |                   If the data is freezed                     |    Boolean
verified     |                If it's verified by other user                |    Text
env          |  Environment can be one of `production` or `preproduction`. _By default, it's set to "production" unless specified otherwise on creation/update_   |    Text
thumbnailUrl |             Url of the widget's thumbnail, if one exists     |    Text
createdAt    |             Date in which the widget was created             |    Date
updatedAt    |             Date in which the widget was last updated        |    Date


### What is Vega?

Vega is a visualization grammar; a declarative format for creating, saving and sharing interactive visualization designs. This wiki contains documentation and learning materials for getting up and running with Vega. [More info](https://github.com/vega/vega/wiki)

## How obtain a single widget

```shell
curl -X GET https://api.skydipper.com/v1/widget/51851e22-1eda-4bf5-bbcc-cde3f9a3a943
```

> Example response:

```json
{
    "data": {
        "id": "51851e22-1eda-4bf5-bbcc-cde3f9a3a943",
        "type": "widget",
        "attributes": {
            "name": "Example Carto Dataset6",
            "dataset": "be76f130-ed4e-4972-827d-aef8e0dc6b18",
            "slug": "example-carto-dataset6",
            "userId": "5820ad9469a0287982f4cd18",
            "description": null,
            "source": null,
            "sourceUrl": null,
            "authors": null,
            "application": [
                "skydipper"
            ],
            "verified": false,
            "default": false,
            "protected": false,
            "defaultEditableWidget": false,
            "published": true,
            "freeze": false,
            "env": "production",
            "queryUrl": null,
            "widgetConfig": "{}",
            "template": false,
            "layerId": null,
            "createdAt": "2017-02-08T15:30:34.505Z",
            "updatedAt": "2017-02-08T15:30:34.505Z"
        }
    }
}
```

### Customize the query url of a widget

The `queryUrl` query parameter can be set if the user needs to modify the final url that will be requested. All parameters indicated in the `queryUrl` will be pass to the microservice.

```shell
curl -X GET https://api.skydipper.com/v1/widget/049f074a-3528-427d-922b-3c2320e9caf6?queryUrl=/v1/query?sql=Select%20*%20from%20data&geostore=ungeostore
```

## How to obtain all widgets

To obtain all widgets:

```shell
curl -X GET https://api.skydipper.com/v1/widget
```

<aside class="success">
Remember — the response is jsonapi format
</aside>

<aside class="success">
Remember — <strong>the resulting list is filtered by env=production</strong> unless another env is explicitly provided as a query param. <i>A list of environments can also be provided such as e.g. "env=production,preproduction"</i>.
</aside>

> Example response:

```json
{
   "data":[
      {
         "id":"8f67fadd-d8df-4a28-82dd-a22a337d71b9",
         "type":"widget",
         "attributes":{
            "userId":"5858f37140621f11066fb2f7",
            "application":[
               "aqueduct"
            ],
            "slug":"percentage-of-country-s-population-is-at-high-risk-of-hunger",
            "name":"Percentage of country's population at high risk of hunger.",
            "description":"",
            "source":"",
            "sourceUrl":"",
            "layerId":null,
            "dataset":"f1d24950-c764-4f90-950a-4541f798eb95",
            "authors":"",
            "queryUrl":"query/f1d24950-c764-4f90-950a-4541f798eb95?sql=select * from crops",
            "widgetConfig":{
                ...
            },
            "template":false,
            "default":true,
            "status":"saved",
            "published":true,
            "freeze": false,
            "verified":false
         }
      }
   ],
   "links":{
      "first":"https://api.skydipper.com/v1/widget?page%5Bnumber%5D=1",
      "prev":"https://api.skydipper.com/v1/widget?page%5Bnumber%5D=1",
      "next":"https://api.skydipper.com/v1/widget?page%5Bnumber%5D=2&page%5Bsize%5D=10",
      "last":"https://api.skydipper.com/v1/widget?page%5Bnumber%5D=64&page%5Bsize%5D=10",
      "self":"https://api.skydipper.com/v1/widget?page%5Bnumber%5D=1&page%5Bsize%5D=10"
   },
   "meta": {
      "total-pages": 38,
      "total-items": 372,
      "size": 10
   }
}
```

Available filters parameters:

Field     |                         Description                          |    Type
--------- | :----------------------------------------------------------: | ------:
name      |    Filter the widgets whose name contains the filter text    |    Text
dataset   |              Filter the widgets by dataset uuid              |    Text
sort      |          Sort json response by specific attributes           |    Text
status    |    Filter widgets on status (pending, saved, failed, all)    |    Text
published |       Filter widgets on published status (true, false)       | Boolean
published |       Filter widgets on freeze status (true, false)          | Boolean
verified  |           Filter by verified status (true, false)            | Boolean
template  |           Filter by template status (true, false)            | Boolean
default   |            Filter by default status (true, false)            | Boolean
app       |       Filter widgets on application (prep, gfw, etc..)       |    Text
env       |   Environment can be one of `production` or `preproduction`  |    Text

> Return the widgets filtered whose name contains glad

```shell
curl -X GET https://api.skydipper.com/v1/widget?name=glad
```

> Return the widgets filtered by dataset

```shell
curl -X GET https://api.skydipper.com/v1/widget?dataset=d02df2f6-d80c-4274-bb6f-f062061655c4
curl -X GET https://api.skydipper.com/v1/dataset/d02df2f6-d80c-4274-bb6f-f062061655c4/widget
```

> Sort by name

```shell
curl -X GET https://api.skydipper.com/v1/widget?sort=name
```

> Filter widgets by status

```shell
curl -X GET https://api.skydipper.com/v1/widget?status=failed
```

> Filter widgets by published status

```shell
curl -X GET https://api.skydipper.com/v1/widget?published=false
```

> Filter widgets by verified status

```shell
curl -X GET https://api.skydipper.com/v1/widget?verified=false
```

> Return the widgets filtered by template

```shell
curl -X GET https://api.skydipper.com/v1/widget?template=true
```

> Filter widgets by default option

```shell
curl -X GET https://api.skydipper.com/v1/widget?default=true
```

> Return widgets whose applications contain skydipper

```shell
curl -X GET https://api.skydipper.com/v1/widget?app=skydipper
```

### Pagination params

Field        |       Description        |   Type
------------ | :----------------------: | -----:
page[size]   | Number elements per page | Number
page[number] |      Number of page      | Number

> Return the widgets from page 2, with 5 elements per page

```shell
curl -X GET https://api.skydipper.com/v1/widget?page[size]=5&page[number]=2
```

## How to obtain a widget for a specific dataset

To obtain the widget:

```shell
curl -X GET https://api.skydipper.com/v1/dataset/d02df2f6-d80c-4274-bb6f-f062061655c4/widget/20ec7861-5251-40a7-9503-5ee3686a66a3
curl -X GET https://api.skydipper.com/v1/widget/20ec7861-5251-40a7-9503-5ee3686a66a3
```

<aside class="success">
Remember — the response is jsonapi format
</aside>

> Example response:

```json
{
  "data": {
    "id": "20ec7861-5251-40a7-9503-5ee3686a66a3",
    "type": "widget",
    "attributes": {
      "userId": "57a0693b49c36b265ba3bec8",
      "application": [
        "skydipper"
      ],
      "slug": "estimated-c02-emission",
      "name": "Estimated C02 emission",
      "description": null,
      "source": "",
      "sourceUrl": null,
      "layerId": null,
      "dataset": "d02df2f6-d80c-4274-bb6f-f062061655c4",
      "authors": null,
      "queryUrl": "query/d02df2f6-d80c-4274-bb6f-f062061655c4?sql=select country, rank, iso3, total from estimated_co2_emission_filtered",
      "widgetConfig": {
        "data": [ ... ],
        "marks": [ ... ],
        "scales": [ ... ],
        "padding": {
          "top": 40,
          "left": 20,
          "right": 20,
          "bottom": 0
        }
      },
      "template": false,
      "default": false,
      "status": "saved",
      "published": true,
      "verified": false
    }
  },
  "meta": {
    "status": "saved",
    "published": true,
    "verified": false,
    "updated_at": "2017-01-17T17:50:45.655Z",
    "created_at": "2016-06-06T15:12:38.749Z"
  }
}
```

## Create a Widget

To create a widget, you need to define all of the required fields in the request body. The fields that compose a widget are:

Field        |               Description               |    Type |                                          Values | Required
------------ | :-------------------------------------: | ------: | ----------------------------------------------: | -------:
name         |           Name of the widget            |    Text |                                        Any Text |      Yes
description  |       Description of the dataset        |    Text |                                        Any text |       No
source       |     Publisher of the original code      |    Text |                                        Any text |       No
sourceUrl    |         Link to publisher page          |    Text |                                         Any url |       No
application  | Application to which the widget belongs |   Array | skydipper |      Yes
authors      |           Name of the authors           |    Text |                                        Any text |       No
queryUrl     |  Url with the data of the chart shows   |    Text |                                 Any valid query |       No
widgetConfig |           Vega configuration            |  Object |                                    Valid object |       No
status       |          Status of the Widget           |  Number |                                               1 |       No
published    |        If it's available to use         | Boolean |                                    true - false |       No
freeze       |        If the data is frozen            | Boolean |                                    true - false |       No
protected    |        If it's a protected widget (not is possible to delete if it's true)         | Boolean |   true - false |       No
verified     |     If it's verified by other user      | Boolean |                                    true - false |       No
template     |           If it's a template            | Boolean |                                    true - false |       No
default      |       If it's default for dataset       | Boolean |                                    true - false |       No
layerId      |   UuId of the relationship with layer   |    Text |                                   Uuid of layer |       No
dataset      |           UuId of the dataset           |    Text |                                 Uuid of Dataset |       No

> To create a widget, you have to do a POST request with the following body:

```shell
curl -X POST https://api.skydipper.com/v1/dataset/<dataset_id>/widget \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "widget": {
      "application":[
         "your", "apps"
      ],
      "name":"Example Carto Dataset"
      "status": 1,
      "published": true
   }
}'
```

<aside class="notice">
Creating a widget will cause a thumbnail to be generated in the background for the new widget. As it is generated asyncronously, the newly generated thumbnail url may only become available on subsequent requests.
</aside>


## Update a Widget

To update a widget, you need to define all of the required fields in the request body. The fields that compose a widget are:

Field        |               Description               |    Type |                                          Values | Required
------------ | :-------------------------------------: | ------: | ----------------------------------------------: | -------:
name         |           Name of the widget            |    Text |                                        Any Text |      Yes
description  |       Description of the dataset        |    Text |                                        Any text |       No
source       |     Publisher of the original code      |    Text |                                        Any text |       No
sourceUrl    |         Link to publisher page          |    Text |                                         Any url |       No
application  | Application to which the widget belongs |   Array | skydipper |      Yes
authors      |           Name of the authors           |    Text |                                        Any text |       No
queryUrl     |  Url with the data of the chart shows   |    Text |                                 Any valid query |       No
widgetConfig |           Vega configuration            |  Object |                                    Valid object |       No
status       |          Status of the Widget           |  Number |                                               1 |       No
published    |        If it's available to use         | Boolean |                                    true - false |       No
freeze       |        If the data is freezed           | Boolean |                                    true - false |       No
verified     |     If it's verified by other user      | Boolean |                                    true - false |       No
template     |           If it's a template            | Boolean |                                    true - false |       No
default      |       If it's default for dataset       | Boolean |                                    true - false |       No
layerId      |   UuId of the relationship with layer   |    Text |                                   Uuid of layer |       No
dataset      |           UuId of the dataset           |    Text |                                 Uuid of Dataset |       No
env          |               Environment               |    Text |                 `production` or `preproduction` |      Yes

> To update a widget, you have to do a PATCH request with the following body:

```shell
curl -X PATCH https://api.skydipper.com/v1/dataset/<dataset_id>/widget/<widget_id> \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "widget": {
      "application":[
         "your", "apps"
      ],
      "name":"New Example Carto Dataset Name",
      "widgetConfig": {}
   }
}'
```

<aside class="notice">
Updating a widget will cause a thumbnail to be generated in the background for the new widget. As it is generated asyncronously, the newly generated thumbnail url may only become available on subsequent requests.
</aside>


## Clone a Widget

You can clone an existing widget as long as you have permissions to the applications associated with it. Basic usage requires no body params, but you can optionally pass a new `name` or `description` to be used in the creation of the new widget.


> To clone a widget, you should use one of the following POST requests:

```shell
curl -X POST https://api.skydipper.com/v1/widget/<widget_id>/clone \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"
```

```shell
curl -X POST https://api.skydipper.com/v1/dataset/<dataset_id>/widget/<widget_id>/clone \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"
```

> You can optionally set a new name or description:


```shell
curl -X POST https://api.skydipper.com/v1/widget/<widget_id>/clone \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "name": "name for the cloned widget",
   "description": "
   "name": "name for the cloned widget", for the cloned widget",
}'
```

```shell
curl -X POST https://api.skydipper.com/v1/dataset/<dataset_id>/widget/<widget_id>/clone \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "name": "name for the cloned widget",
   "description": "
   "name": "name for the cloned widget", for the cloned widget",
}'
```

### Cloning widgets from other microservices

When cloning a widget, the newly created clone will take the `userId` of the originating request. If you call this endpoint as an authenticated user from your custom application, that means it will get that authenticated user's `userId`. However, if invoked from another API microservice, that `userId` is no longer available. In this scenario, when the request to clone is originated internally, you can optionally pass a `userÌd` body value that will be set as the `userId` of the newly created widget.

<aside class="warning">
User IDs provided this way are not validated.
</aside>

```shell
curl -X POST https://api.skydipper.com/v1/widget/<widget_id>/clone \
-H "Authorization: Bearer <microservice-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "userID": "123456789",
}'
```

<aside class="notice">
Cloning a widget will cause a thumbnail to be generated in the background for the new widget. As it is generated asyncronously, the newly generated thumbnail url may only become available on subsequent requests.
</aside>


## Delete a Widget

```shell
curl -X DELETE https://api.skydipper.com/v1/dataset/<dataset_id>/widget/<widget_id> \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"
```
