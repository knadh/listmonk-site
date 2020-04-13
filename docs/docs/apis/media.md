# API/MEDIA
Method        |         Endpoint                                             |       Description
--------------|--------------------------------------------------------------|----------------------------------------------
`GET`         | [/api/media](#get-apimedia)                                  | Gets a uploaded media file.
`POST`        | [/api/media](#post-apimedia)                                 | Uploads a media file.
`DELETE`      | [/api/media/:`media_id`](#delete-apimediamedia_id)             | Deletes uploaded media files. 

#### **`GET`** /api/media
Gets a uploaded media file.

##### Example Request
```shell
curl --location --request GET 'http://localhost:9000/api/media' \
--header 'Content-Type: multipart/form-data; boundary=--------------------------093715978792575906250298'
```

##### Example Response
```json
{
    "data": [
        {
            "id": 1,
            "uuid": "ec7b45ce-1408-4e5c-924e-965326a20287",
            "filename": "Media file",
            "width": 0,
            "height": 0,
            "created_at": "2020-04-08T22:43:45.080058+01:00",
            "thumb_uri": "/uploads/thumb_Media file",
            "uri": "/uploads/Media filE"
        }
    ]
}
```

#### **`POST`** /api/media
Uploads a media file.

##### Parameters
Nam        |  Parameter Type       |  Data Type        |     Required/Optional   |   Description
-----------|-----------------------|-------------------|-------------------------|---------------------------------
file       |  Request body         |  Media file       |     Required            | The media file to be uploaded.


##### Example Request
```shell 
curl --location --request POST 'http://localhost:9000/api/media' \
--header 'Content-Type: multipart/form-data; boundary=--------------------------183679989870526937212428' \
--form 'file=@/Users/username/Desktop/Media file'
```

##### Example Response
``` json
{
    "data": true
}
```

#### **`DELETE`** /api/media/:`media_id`
Deletes a uploaded media file.

##### Parameters
Name            |   Parameter Type        | Data Type          | Required/Optional       | Description
----------------|-------------------------|--------------------|-------------------------|--------------------------
`Media_id`       | Path Parameter          | Number             | Required                | The id of the media file you want to delete.


##### Example Request
```shell
curl --location --request DELETE 'http://localhost:9000/api/media/1'
```


##### Example Response
```json
{
    "data": true
}
```