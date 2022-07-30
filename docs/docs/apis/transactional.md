# API / Transactional

| Method | Endpoint | Description |
|:-------|:---------|:------------|
| `POST` | /api/tx  |             |


## POST /api/tx
Send a transactional message to a subscriber using a predefined transactional template.


##### Parameters
| Name               | Data Type | Optional | Description                                                                       |
|:-------------------|:----------|:---------|:----------------------------------------------------------------------------------|
| `subscriber_email` | String    | Optional | E-mail of the subscriber. Either this or `subscriber_id` should be passed.        |
| `subscriber_id`    | Number    | Optional | ID of the subscriber. Either this or `subscriber_email` should be passed.         |
| `template_id`      | Number    | Required | ID of the transactional template to use in the message.                           |
| `data`             | Map       | Optional | Optional data in `{}` nested map. Available in the template as `{{ .Tx.Data.* }}` |
| `headers`          | []Map     | Optional | Optional array of mail headers. `[{"key": "value"}, {"key": "value"}]`            |
| `content_type`     | string    | Optional | `html`, `markdown`, `plain`                                                       |


##### Request
```shell
curl -u "username:password" "http://localhost:9000/api/tx" -X POST \
     -H 'Content-Type: application/json; charset=utf-8' \
     --data-binary @- << EOF
    {
        "subscriber_email": "user@test.com",
        "template_id": 2,
        "data": {"order_id": "1234", "date": "2022-07-30", "items": [1, 2, 3]},
        "content_type": "html"
    }
EOF
```

##### Response
``` json
{
    "data": true
}
```


