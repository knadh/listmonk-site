# API / Subscribers

| Method   | Endpoint                                                      | Description                                             |
| -------- | ------------------------------------------------------------- | ------------------------------------------------------- |
| `GET`    | /api/subscribers                                              | Get subscribers                                         |
| `GET`    | /api/subscribers/:id                                          | Get a subscriber by ID                                   |
| `GET`    | /api/subscribers/lists/:id                                    | Get subscribers in a list by the list ID                |
| `GET`    | [/api/subscribers/lists](#get-subscribers-in-lists)           | Get subscribers in one or more lists by the list IDs    |
| `GET`    | [/api/subscribers](#query-subscribers-with-an-sql-expression) | Get subscribers filtered by an arbitrary SQL expression |
| `POST`   | [/api/subscribers](#add-a-new-subscriber)                     | Add a new subscriber                                    |
| `PUT`    | /api/subscribers/:id                                          | Update a subscriber by ID                               |
| `PUT`    | /api/subscribers/:id/blacklist                                | Blacklist a single subscriber by ID                     |
| `PUT`    | /api/subscribers/blacklist                                    | Blacklist one or more subscribers by their IDs          |
| `PUT`    | /api/subscribers/query/blacklist                              | Blacklist subscribers with an arbitrary SQL expression  |
| `DELETE` | /api/subscribers/:id                                          | Delete a single subscriber                              |
| `DELETE` | /api/subscribers                                              | Delete one or more subscribers by their IDs             |
| `DELETE` | /api/subscribers/query/delete                                 | Delete subscribers with an arbitrary SQL expression     |

#### Get subscribers in lists

```shell
curl 'http://localhost:9000/api/subscribers?list_id=1&list_id=2&page=1'
```

Response

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

#### Query subscribers with an SQL expression

```shell
curl -X GET  'http://localhost:9001/api/subscribers' \
    -d 'page=1' \
    -d "query=subscribers.name LIKE 'Test%' AND subscribers.attribs->>'city' = 'Bengaluru'"
```

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

#### Add a new subscriber

```shell
curl 'http://localhost:9000/api/subscribers' -H 'Content-Type: application/json' \
    --data '{"email":"subsriber@domain.com","name":"The Subscriber","status":"enabled","lists":[1],"attribs":{"city":"Bengaluru","projects":3,,"stack":{"languages":["go","python"]}}}'
```

Response

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
