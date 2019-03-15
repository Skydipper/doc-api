# Fields

## What are fields?

Fields can be defined as the dataset properties. These fields are automatically generated when a dataset is created.

## How to get the dataset fields

Once the dataset is properly created and saved, it is possible to access to its fields as well as getting some information about them.

To do that, it is necessary to use of the following endpoint:

```shell
curl -X GET https://api.skydipper.com/v1/fields/<dataset-id>
```

> Real example

```shell
curl -X GET https://api.skydipper.com/v1/fields/1170030b-9725-4bfe-8fb4-1b0eb81020d2
```

> Response

```json
{
	"tableName": "public.cait_2_0_country_ghg_emissions_toplow2011",
	"fields": {
		"cartodb_id": {
			"type": "number"
		},
		"the_geom": {
			"type": "geometry"
		},
		"the_geom_webmercator": {
			"type": "geometry"
		},
		"x": {
			"type": "string"
		},
		"y": {
			"type": "number"
		},
		"z": {
			"type": "string"
		}
	}
}
```

