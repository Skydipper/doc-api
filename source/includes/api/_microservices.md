# Microservices

A list of information related to the microservices

<aside class="notice">
    These services are only available to ADMIN users.
</aside>

## List all registered microservices

To obtain a list of all the registered microservices:

```shell
curl -X GET https://api.skydipper.com/api/v1/microservice \
-H "Authorization: Bearer <your-token>"
```

> Example response:

```json
[
    {
        "infoStatus": {
            "numRetries": 0,
            "error": null,
            "lastCheck": "2019-02-04T14:05:30.748Z"
        },
        "pathInfo": "/info",
        "pathLive": "/ping",
        "status": "active",
        "cache": [],
        "uncache": ["dataset"],
        "tags": [
            "dataset"
          
        ],
        "_id": "id",
        "name": "Dataset",
        "url": "http://dataset.default.svc.cluster.local:3000",
        "version": 1,
        "endpoints": [
            {
                "redirect": {
                    "method": "GET",
                    "path": "/api/v1/dataset"
                },
                "path": "/v1/dataset",
                "method": "GET"
            },
            {
                "redirect": {
                    "method": "POST",
                    "path": "/api/v1/dataset/find-by-ids"
                },
                "path": "/v1/dataset/find-by-ids",
                "method": "POST"
            },
            ...
        ],
        "updatedAt": "2019-01-24T13:04:46.728Z",
        "swagger": "{}"
    },
    ...
  }
}
```

## Delete microservice

To remove a microservice:

```shell
curl -X DELETE https://api.skydipper.com/api/v1/microservice/:id \
-H "Authorization: Bearer <your-token>"
```

#### Notes

Keep in mind that this does not actually delete the microservice, instead it schedules it for being removed. 
There's a cron task that does the actual deleting, so the process is async.
