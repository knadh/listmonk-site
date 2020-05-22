# API / Import

Method     |  Endpoint                                                            |  Description 
-----------|----------------------------------------------------------------------|--------------
`GET`      | [api/import/subscribers](#get-apiimportsubscribers)                  | Gets a import statistics. 
`GET`      | [api/import/subscribers/logs](#get-apiimportsubscriberslogs)         | Get a import statistics .
`POST`     | api/import/subscribers                                               | Upload a ZIP file or CSV files to bulk import subscribers. 
`DELETE`   | [api/import/subscribers](#delete-apiimportsubscribers)               | Stops and deletes a import.


#### **`GET`** api/import/subscribers
Gets a import statistics.

##### Example Request 
```shell 
curl --location --request GET 'http://localhost:9000/api/import/subscribers'
```

##### Example Response 
```json
{
    "data": {
        "name": "",
        "total": 0,
        "imported": 0,
        "status": "none"
    }
}
```

#### **`GET`** api/import/subscribers/logs
Gets a import statistics.

##### Example Request 
```shell
curl --location --request GET 'http://localhost:9000/api/import/subscribers/logs'
```

##### Example Response
```json
{
    "data": "2020/04/08 21:55:20 processing 'import.csv'\n2020/04/08 21:55:21 imported finished\n"
}
```



#### **`DELETE`** api/import/subscribers
Stops and deletes a import.

##### Example Request
```shell
curl --location --request DELETE 'http://localhost:9000/api/import/subscribers' 
```

##### Example Response
```json
{
    "data": {
        "name": "",
        "total": 0,
        "imported": 0,
        "status": "none"
    }
}
```