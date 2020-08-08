# API / Subscribers

 Method   | Endpoint                                                              | Description                                             |
 -------- | ----------------------------------------------------------------------| ---------------------------------
 `GET`    | [/api/subscribers](#get-apisubscribers)                               | Gets all subscribers.                     
 `GET`    | [/api/subscribers/:`id`](#get-apisubscribersid)                         | Gets a single subscriber.
 `GET`    | /api/subscribers/lists/:`id`                                            | Gets subscribers in a list.                
 `GET`    | [/api/subscribers/:`list_id`](#get-apisubscriberslist_id)                | Gets subscribers in one or more list.   
 `GET`    | [/api/subscribers](#get-apisubscribers_1)                             | Gets subscribers filtered by an arbitrary SQL expression. 
 `POST`   | [/api/subscribers](#post-apisubscribers)                              | Creates a new subscriber.                        
 `PUT`    | /api/subscribers/:`id`                                                 | Updates a subscriber by ID.                    
 `PUT`    | [/api/subscribers/:`id`/blocklist](#put-apisubscribersidblocklist)      | Blocklists a single subscriber.               
 `PUT`    | /api/subscribers/blocklist                                            | Blocklists one or more subscribers.     
 `PUT`    | [/api/subscribers/query/blocklist](#put-apisubscribersqueryblocklist) | Blocklists subscribers with an arbitrary SQL expression.  
 `DELETE` | [/api/subscribers/:`id`](#delete-apisubscribersid)                      | Deletes a single subscriber.                   
 `DELETE` | [/api/subscribers](#delete-apisubscribers)                            | Deletes one or more subscribers .            
 `POST` | [/api/subscribers/query/delete](#post-apisubscribersquerydelete)        | Deletes subscribers with an arbitrary SQL expression .    




#### **`GET`** /api/subscribers
Gets all subscribers. 

##### Example Request
```shell
curl 'http://localhost:9000/api/subscribers' 
```
##### Example Response
```json
{
    "data": {
        "results": [
            {
                "id": 1,
                "created_at": "2020-02-10T23:07:16.199433+01:00",
                "updated_at": "2020-02-10T23:07:16.199433+01:00",
                "uuid": "ea06b2e7-4b08-4697-bcfc-2a5c6dde8f1c",
                "email": "john@example.com",
                "name": "John Doe",
                "attribs": {
                    "city": "Bengaluru",
                    "good": true,
                    "type": "known"
                },
                "status": "enabled",
                "lists": [
                    {
                        "subscription_status": "unconfirmed",
                        "id": 1,
                        "uuid": "ce13e971-c2ed-4069-bd0c-240e9a9f56f9",
                        "name": "Default list",
                        "type": "public",
                        "tags": [
                            "test"
                        ],
                        "created_at": "2020-02-10T23:07:16.194843+01:00",
                        "updated_at": "2020-02-10T23:07:16.194843+01:00"
                    }
                ]
            },
            {
                "id": 2,
                "created_at": "2020-02-18T21:10:17.218979+01:00",
                "updated_at": "2020-02-18T21:10:17.218979+01:00",
                "uuid": "ccf66172-f87f-4509-b7af-e8716f739860",
                "email": "quadri@example.com",
                "name": "quadri",
                "attribs": {},
                "status": "enabled",
                "lists": [
                    {
                        "subscription_status": "unconfirmed",
                        "id": 1,
                        "uuid": "ce13e971-c2ed-4069-bd0c-240e9a9f56f9",
                        "name": "Default list",
                        "type": "public",
                        "tags": [
                            "test"
                        ],
                        "created_at": "2020-02-10T23:07:16.194843+01:00",
                        "updated_at": "2020-02-10T23:07:16.194843+01:00"
                    }
                ]
            },
            {
                "id": 3,
                "created_at": "2020-02-19T19:10:49.36636+01:00",
                "updated_at": "2020-02-19T19:10:49.36636+01:00",
                "uuid": "5d940585-3cc8-4add-b9c5-76efba3c6edd",
                "email": "sugar@example.com",
                "name": "sugar",
                "attribs": {},
                "status": "enabled",
                "lists": []
            }
        ],
        "query": "",
        "total": 3,
        "per_page": 20,
        "page": 1
    }
}
```






#### **`GET`** /api/subscribers/:`id`
 Gets a single subscriber. 

##### Parameters

Name     | Parameter type |Data type       | Required/Optional |  Description
---------|----------------|----------------|-------------------|-----------------------
`id`       | Path parameter | Number         | Required          | The id value of the subscriber you want to get.

##### Example Request
```shell
curl 'http://localhost:9000/api/subscribers/1' 
```

##### Example Response
```json
{
    "data": {
        "id": 1,
        "created_at": "2020-02-10T23:07:16.199433+01:00",
        "updated_at": "2020-02-10T23:07:16.199433+01:00",
        "uuid": "ea06b2e7-4b08-4697-bcfc-2a5c6dde8f1c",
        "email": "john@example.com",
        "name": "John Doe",
        "attribs": {
            "city": "Bengaluru",
            "good": true,
            "type": "known"
        },
        "status": "enabled",
        "lists": [
            {
                "subscription_status": "unconfirmed",
                "id": 1,
                "uuid": "ce13e971-c2ed-4069-bd0c-240e9a9f56f9",
                "name": "Default list",
                "type": "public",
                "tags": [
                    "test"
                ],
                "created_at": "2020-02-10T23:07:16.194843+01:00",
                "updated_at": "2020-02-10T23:07:16.194843+01:00"
            }
        ]
    }
}
```





#### **`GET`** /api/subscribers/:`list_id`
Gets subscribers in one or more lists. 

##### Parameters

Name    | Parameter type  | Data type   |  Required/Optional  | Description
------- |-----------------|-------------|---------------------|---------------
`List_id` | Request body    | Number      | Required            |  The id value of the list whose subcribers you want to get.

##### Example Request
```shell
curl 'http://localhost:9000/api/subscribers?list_id=1&list_id=2&page=1'
```

##### Example Response

```json
{
  "data": {
    "results": [
      {
        "id": 1,
        "created_at": "2019-06-26T16:51:54.37065+05:30",
        "updated_at": "2019-07-03T11:53:53.839692+05:30",
        "uuid": "5e91dda1-1c16-467d-9bf9-2a21bf22ae21",
        "email": "test@test.com",
        "name": "Test Subscriber",
        "attribs": {
          "city": "Bengaluru",
          "projects": 3,
          "stack": {
            "languages": ["go", "python"]
          }
        },
        "status": "enabled",
        "lists": [
          {
            "subscription_status": "unconfirmed",
            "id": 1,
            "uuid": "41badaf2-7905-4116-8eac-e8817c6613e4",
            "name": "Default list",
            "type": "public",
            "tags": ["test"],
            "created_at": "2019-06-26T16:51:54.367719+05:30",
            "updated_at": "2019-06-26T16:51:54.367719+05:30"
          }
        ]
      }
    ],
    "query": "",
    "total": 1,
    "per_page": 20,
    "page": 1
  }
}
```

#### **`GET`** /api/subscribers
Gets subscribers with an SQL expression.

##### Example Request
```shell
curl -X GET  'http://localhost:9000/api/subscribers' \
    -d 'page=1' \
    -d "query=subscribers.name LIKE 'Test%' AND subscribers.attribs->>'city' = 'Bengaluru'"
```

>Refer to the [querying and segmentation](/querying-and-segmentation#querying-and-segmenting-subscribers) section for more information on how to query subscribers with SQL expressions.

##### Example Response 
```json
{
  "data": {
    "results": [
      {
        "id": 1,
        "created_at": "2019-06-26T16:51:54.37065+05:30",
        "updated_at": "2019-07-03T11:53:53.839692+05:30",
        "uuid": "5e91dda1-1c16-467d-9bf9-2a21bf22ae21",
        "email": "test@test.com",
        "name": "Test Subscriber",
        "attribs": {
          "city": "Bengaluru",
          "projects": 3,
          "stack": {
            "frameworks": ["echo", "go"],
            "languages": ["go", "python"]
          }
        },
        "status": "enabled",
        "lists": [
          {
            "subscription_status": "unconfirmed",
            "id": 1,
            "uuid": "41badaf2-7905-4116-8eac-e8817c6613e4",
            "name": "Default list",
            "type": "public",
            "tags": ["test"],
            "created_at": "2019-06-26T16:51:54.367719+05:30",
            "updated_at": "2019-06-26T16:51:54.367719+05:30"
          }
        ]
      }
    ],
    "query": "subscribers.name LIKE 'Test%' AND subscribers.attribs-\u003e\u003e'city' = 'Bengaluru'",
    "total": 1,
    "per_page": 20,
    "page": 1
  }
}
```


#### **`POST`** /api/subscribers

Creates a new subscriber.

##### Parameters 

Name   | Parameter type   | Data type             | Required/Optional                 | Description
-------|------------------|-----------------------|-----------------------------------|----------------------------
email  | Request body     | String                | Required                          | The email address of the new susbcriber.
name   | Request body     | String                | Required                          | The name of the new subscriber. 
status | Request body     | String                | Required                          | The status of the new subscriber. Can be enabled, disabled or blocklisted. 
list   | Request body     | Numbers               | Optional                         | The id value of list to which new subscriber will be added.
attribs | Request body  | json                    | Optional                         | JSON list containing new subscriber's attributes.

##### Example Request
```shell
curl 'http://localhost:9000/api/subscribers' -H 'Content-Type: application/json' \
    --data '{"email":"subsriber@domain.com","name":"The Subscriber","status":"enabled","lists":[1],"attribs":{"city":"Bengaluru","projects":3,,"stack":{"languages":["go","python"]}}}'
```

##### Example Response

```json
{
  "data": {
    "id": 3,
    "created_at": "2019-07-03T12:17:29.735507+05:30",
    "updated_at": "2019-07-03T12:17:29.735507+05:30",
    "uuid": "eb420c55-4cfb-4972-92ba-c93c34ba475d",
    "email": "subsriber@domain.com",
    "name": "The Subscriber",
    "attribs": {
      "city": "Bengaluru",
      "projects": 3,
      "stack": { "languages": ["go", "python"] }
    },
    "status": "enabled",
    "lists": [1]
  }
}
```


#### **`PUT`** /api/subscribers/:`id`/blocklist
Blocklists a single subscriber.

##### Parameters 

Name  | Parameter type | Data type  | Required/Optional | Description 
------|----------------|------------|-------------------|-------------
`id`    | Path parameter | Number     | Required          | The id value of the subscriber you want to blocklist.

##### Example Request 

```shell
curl --location --request PUT 'http://localhost:9000/api/subscribers/9/blocklist'
```

##### Example Response 

``` json
{
    "data": true
} 
```

#### **`PUT`** /api/subscribers/query/blocklist 
Blocklists subscribers with an arbitrary sql expression.

##### Example Request
``` shell
curl --location --request PUT 'http://localhost:9000/api/subscribers/query/blocklist' \
--data-raw '"query=subscribers.name LIKE '\''John Doe'\'' AND subscribers.attribs->>'\''city'\'' = '\''Bengaluru'\''"'
```

>Refer to the [querying and segmentation](/querying-and-segmentation#querying-and-segmenting-subscribers) section for more information on how to query subscribers with SQL expressions.


##### Example Response

``` json
{
    "data": true
}
```

#### **`DELETE`** /api/subscribers/:`id`
Deletes a single subscriber. 

##### Parameters 

name    | Parameter type   | Data type   |   Required/Optional    |  Description
--------|------------------|-------------|------------------------|------------------
`id`      | Path parameter   | Number      | Required               | The id of the subscriber you want to delete.

##### Example  Request 

``` shell
curl --location --request DELETE 'http://localhost:9000/api/subscribers/9'
```

##### Example Response 

``` json
{
    "data": true
}
```

#### **`DELETE`** /api/subscribers 
Deletes one or more subscribers.

##### Parameters 

Name    |   Parameter type    | Data type      |   Required/Optional   | Description
--------|---------------------|----------------|-----------------------|--------------
id      | Query parameters    | Number         |  Required             | The id of the subscribers you want to delete.

##### Example Request

``` shell
curl --location --request DELETE 'http://localhost:9000/api/subscribers?id=10&id=11'
```

##### Example Response 

``` json 
{
    "data": true
}
```



#### **`POST`** /api/subscribers/query/delete 
Deletes subscribers with an arbitrary SQL expression.

##### Example Request
``` shell
curl --location --request POST 'http://localhost:9000/api/subscribers/query/delete' \
--data-raw '"query=subscribers.name LIKE '\''John Doe'\'' AND subscribers.attribs->>'\''city'\'' = '\''Bengaluru'\''"'
```

>Refer to the [querying and segmentation](/querying-and-segmentation#querying-and-segmenting-subscribers) section for more information on how to query subscribers with SQL expressions.



##### Example Response
``` json
{
    "data": true
}
```




