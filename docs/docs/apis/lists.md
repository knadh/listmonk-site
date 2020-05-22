# API / Lists
Method                   | Endpoint                                             | Description
-------------------------|------------------------------------------------------|----------------------------------------------
`GET`                    | [/api/lists](#get-apilists)                          | Gets all lists.
`GET`                    | [/api/lists/:`list_id`](#get-apilistslist_id)          | Gets a single list.
`POST`                   | [/api/lists](#post-apilists)                         | Creates a new list.
`PUT`                    | /api/lists/:`list_id`                                  | Modifies a list.
`DELETE`                 | [/api/lists/:`list_id`](#put-apilistslist_id)          | Deletes a list.


#### **`GET`** /api/lists
Gets all lists.

##### Example Request
```shell
curl --location --request GET 'http://localhost:9000/api/lists'
```

##### Example Response
```json
{
    "data": {
        "results": [
            {
                "id": 1,
                "created_at": "2020-02-10T23:07:16.194843+01:00",
                "updated_at": "2020-03-06T22:32:01.118327+01:00",
                "uuid": "ce13e971-c2ed-4069-bd0c-240e9a9f56f9",
                "name": "Default list",
                "type": "public",
                "tags": [
                    "test"
                ],
                "subscriber_count": 2
            },
            {
                "id": 2,
                "created_at": "2020-03-04T21:12:09.555013+01:00",
                "updated_at": "2020-03-06T22:34:46.405031+01:00",
                "uuid": "f20a2308-dfb5-4420-a56d-ecf0618a102d",
                "name": "get",
                "type": "private",
                "tags": [],
                "subscriber_count": 0
            },
            {
                "id": 3,
                "created_at": "2020-03-04T21:12:39.702639+01:00",
                "updated_at": "2020-03-04T21:12:39.702639+01:00",
                "uuid": "414c4d67-1262-4884-bdac-cb7447d0b952",
                "name": "list2\n",
                "type": "public",
                "tags": [],
                "subscriber_count": 0
            },
            {
                "id": 4,
                "created_at": "2020-03-04T21:13:14.830035+01:00",
                "updated_at": "2020-03-04T21:13:14.830035+01:00",
                "uuid": "da21f558-ae1c-4235-bebb-f770a8d95a34",
                "name": "single\n",
                "type": "public",
                "tags": [],
                "subscriber_count": 0
            },
            {
                "id": 5,
                "created_at": "2020-03-07T06:31:06.072483+01:00",
                "updated_at": "2020-03-07T06:31:06.072483+01:00",
                "uuid": "1bb246ab-7417-4cef-bddc-8fc8fc941d3a",
                "name": "Test list",
                "type": "public",
                "tags": [],
                "subscriber_count": 0
            }
        ],
        "total": 5,
        "per_page": 20,
        "page": 1
    }
}
```

#### **`GET`** /api/lists/:`list_id`
Gets a single list.

##### Parameters
Name    | Parameter type     | Data type   | Required/Optional   | Description
--------|--------------------|-------------|---------------------|---------------------
`list_id` | Path parameter     | number      | Required            |  The id value of the list you want to get.

##### Example Request
``` shell
curl --location --request GET 'http://localhost:9000/api/lists/5'
```

##### Example Response
```json
{
    "data": {
        "id": 5,
        "created_at": "2020-03-07T06:31:06.072483+01:00",
        "updated_at": "2020-03-07T06:31:06.072483+01:00",
        "uuid": "1bb246ab-7417-4cef-bddc-8fc8fc941d3a",
        "name": "Test list",
        "type": "public",
        "tags": [],
        "subscriber_count": 0
    }
}
```

#### **`POST`** /api/lists
Creates a new list.

##### Parameters
Name    | Parameter type  | Data type   | Required/Optional  | Description
--------|-----------------|-------------|--------------------|----------------
name    | Request body    | string      | Required           | The new list name.  
type    | Request body    | string      | Required           | List type, can be set to Private or Public.

##### Example Request
``` shell
curl --location --request POST 'http://localhost:9000/api/lists'
```

##### Example Response
```json
{
    "data": {
        "id": 5,
        "created_at": "2020-03-07T06:31:06.072483+01:00",
        "updated_at": "2020-03-07T06:31:06.072483+01:00",
        "uuid": "1bb246ab-7417-4cef-bddc-8fc8fc941d3a",
        "name": "Test list",
        "type": "public",
        "tags": [],
        "subscriber_count": 0
    }
}
null
```

#### **`PUT`** /api/lists/`list_id`
Modifies a list.

##### Parameters
Name      |  Parameter type    | Data type    | Required/Optional     | Description
----------|--------------------|--------------|-----------------------|-------------------------
`list_id`   | Path parameter     | number       | Required              | The id of the list to be modified.
name      | Request body       | string       | Optional              | The name which the old name will be modified to.
type      | Request body       | string       | Optional              | List type, can be set to Private or Public.


##### Example Request
```shell
curl --location --request PUT 'http://localhost:9000/api/lists/5' \
--form 'name=modified test list' \
--form 'Type=private'
```

##### Example Response
``` json
{
    "data": {
        "id": 5,
        "created_at": "2020-03-07T06:31:06.072483+01:00",
        "updated_at": "2020-03-07T06:52:15.208075+01:00",
        "uuid": "1bb246ab-7417-4cef-bddc-8fc8fc941d3a",
        "name": "modified test list",
        "type": "private",
        "tags": [],
        "subscriber_count": 0
    }
}
```

