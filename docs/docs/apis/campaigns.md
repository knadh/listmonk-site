# API / Campaigns

Method |   Endpoint                                                                | Description                  
-------|---------------------------------------------------------------------------|-----------------------------
`GET`  | [/api/campaigns](#get-apicampaigns)                                       |  Gets all campaigns.
`GET`  | [/api/campaigns/:`campaign_id`](#get-apicampaignscampaign_id)                |  Gets a single campaign.
`GET`  | [/api/campaigns/:`campaign_id`/preview](#get-apicampaignscampaign_idpreview)  |  Gets the HTML preview of a campaign body.
`GET`  | [/api/campaigns/running/stats](#get-apicampaignsrunningstats)              |  Gets the stats of a given set of campaigns.
`POST` | /api/campaigns/:`campaign_id`/test                         |  Posts campaign message to arbitrary subscribers for testing.
`POST` | /api/campaigns                                                             |  Creates a new campaign.
`PUT`  | /api/campaigns/:`campaign_id`                                                |  Modifies a campaign.
`PUT`  | [/api/campaigns/:`campaign_id`/status](#put-apicampaignscampaign_idstatus)   |  Modifies a campaign status.
`DELETE`  | [/api/campaigns/:`campaign_id`](#delete-apicampaignscampaign_id)          |  Deletes a campaign. 

#### ```GET``` /api/campaigns

Gets all campaigns.

##### Example Request

```shell
 curl -u "username:password" -X GET 'http://localhost:9000/api/campaigns?page=1&per_page=100'
```

To skip pagination and retrieve all records, pass `per_page=all`.

##### Example Response

``` json
{
    "data": {
        "results": [
            {
                "id": 1,
                "created_at": "2020-03-14T17:36:41.29451+01:00",
                "updated_at": "2020-03-14T17:36:41.29451+01:00",
                "CampaignID": 0,
                "views": 0,
                "clicks": 0,
                "lists": [
                    {
                        "id": 1,
                        "name": "Default list"
                    }
                ],
                "started_at": null,
                "to_send": 0,
                "sent": 0,
                "uuid": "57702beb-6fae-4355-a324-c2fd5b59a549",
                "type": "regular",
                "name": "Test campaign",
                "subject": "Welcome to listmonk",
                "from_email": "No Reply <noreply@yoursite.com>",
                "body": "<h3>Hi {{ .Subscriber.FirstName }}!</h3>\n\t\t\tThis is a test e-mail campaign. Your second name is {{ .Subscriber.LastName }} and you are from {{ .Subscriber.Attribs.city }}.",
                "send_at": "2020-03-15T17:36:41.293233+01:00",
                "status": "draft",
                "content_type": "richtext",
                "tags": [
                    "test-campaign"
                ],
                "template_id": 1,
                "messenger": "email"
            }
        ],
        "query": "",
        "total": 1,
        "per_page": 20,
        "page": 1
    }
}
```

#### ```GET``` /api/campaigns/:`campaign_id`

Gets a single campaign.

##### Parameters 
Name        | Parameter Type    | Data Type    | Required/Optional    | Description
------------|-------------------|--------------|----------------------|-----------------------------
`campaign_id` | Path Parameter    | Number       | Required             | The id  value of the campaign you want to get.


##### Example Request

``` shell
curl -u "username:password" -X GET 'http://localhost:9000/api/campaigns/1'
```

##### Example Response

``` json
{
    "data": {
        "id": 1,
        "created_at": "2020-03-14T17:36:41.29451+01:00",
        "updated_at": "2020-03-14T17:36:41.29451+01:00",
        "CampaignID": 0,
        "views": 0,
        "clicks": 0,
        "lists": [
            {
                "id": 1,
                "name": "Default list"
            }
        ],
        "started_at": null,
        "to_send": 0,
        "sent": 0,
        "uuid": "57702beb-6fae-4355-a324-c2fd5b59a549",
        "type": "regular",
        "name": "Test campaign",
        "subject": "Welcome to listmonk",
        "from_email": "No Reply <noreply@yoursite.com>",
        "body": "<h3>Hi {{ .Subscriber.FirstName }}!</h3>\n\t\t\tThis is a test e-mail campaign. Your second name is {{ .Subscriber.LastName }} and you are from {{ .Subscriber.Attribs.city }}.",
        "send_at": "2020-03-15T17:36:41.293233+01:00",
        "status": "draft",
        "content_type": "richtext",
        "tags": [
            "test-campaign"
        ],
        "template_id": 1,
        "messenger": "email"
    }
}
```


 


#### ```GET``` /api/campaigns/:`campaign_id`/preview 

Gets the html preview of a campaign body.

##### Parameters 

Name        | Parameter Type    | Data Type    | Required/Optional    | Description
------------|-------------------|--------------|----------------------|-----------------------------
`campaign_id` | Path Parameter    | Number       | Required             | The id value of the campaign to be previewed.


##### Example Request

```shell
curl -u "username:password" -X GET 'http://localhost:9000/api/campaigns/1/preview'
```

##### Example Response

``` html
<h3>Hi John!</h3>
This is a test e-mail campaign. Your second name is Doe and you are from Bengaluru.
```

#### ```GET``` /api/campaigns/running/stats

Gets the running stat of a given set of campaigns.

##### Parameters

Name        | Parameter Type   | Data Type  | Required/Optional   | Description
------------|------------------|------------|---------------------|--------------------------------
campaign_id | Query Parameters | Number     | Required            | The id values of the campaigns whose stat you want to get.


##### Example Request

``` shell
curl -u "username:password" -X GET 'http://localhost:9000/api/campaigns/running/stats?campaign_id=1'
```

##### Example Response

``` json
{
    "data": []
}
```

#### ```PUT``` /api/campaigns/:`campaign_id`/status

Modifies a campaign status. 

##### Parameters 

Name              |  Parameter Type         | Data Type                 |    Required/Optional | Description
------------------|-------------------------|---------------------------|----------------------|-----------------------------
`campaign_id`      | Path Parameter          | Number                    | Required             | The id value of the campaign whose status is to be modified.
status            | Request Body            | String                    | Required             | The new status value, can be set to "draft", "scheduled", "running", "paused", "finished", "cancelled".                        


###### Note: 
 > * Only "scheduled" campaigns can be saved as "draft".
  * Only "draft" campaigns can be "scheduled".
  * Only "paused" campaigns and "draft" campaigns can be started.
  * Only "running" campaigns can be "cancelled" and "paused".


##### Example Request

```shell
curl -u "username:password" -X PUT 'http://localhost:9000/api/campaigns/1/status' \
--header 'Content-Type: multipart/form-data; boundary=--------------------------047372886665819311890787' \
--form 'status=scheduled'
```

##### Example Response

```json
{
    "data": {
        "id": 1,
        "created_at": "2020-03-14T17:36:41.29451+01:00",
        "updated_at": "2020-04-08T19:35:17.331867+01:00",
        "CampaignID": 0,
        "views": 0,
        "clicks": 0,
        "lists": [
            {
                "id": 1,
                "name": "Default list"
            }
        ],
        "started_at": null,
        "to_send": 0,
        "sent": 0,
        "uuid": "57702beb-6fae-4355-a324-c2fd5b59a549",
        "type": "regular",
        "name": "Test campaign",
        "subject": "Welcome to listmonk",
        "from_email": "No Reply <noreply@yoursite.com>",
        "body": "<h3>Hi {{ .Subscriber.FirstName }}!</h3>\n\t\t\tThis is a test e-mail campaign. Your second name is {{ .Subscriber.LastName }} and you are from {{ .Subscriber.Attribs.city }}.",
        "send_at": "2020-03-15T17:36:41.293233+01:00",
        "status": "scheduled",
        "content_type": "richtext",
        "tags": [
            "test-campaign"
        ],
        "template_id": 1,
        "messenger": "email"
    }
}
```

#### ```DELETE``` /api/campaigns/:`campaign_id`

Deletes a campaign, only scheduled campaigns that have not yet been started can be deleted.  

##### Parameters

Name     |  Parameter Type    | Data Type      | Required/Optional   | Description
---------|--------------------|----------------|---------------------|------------------------------
`campaign_id`| Path Parameter   | Number         | Required            | The id value of the campaign you want to delete.


##### Example Request

```shell
curl -u "username:password" -X DELETE 'http://localhost:9000/api/campaigns/34'
```

##### Example Response

```json
{
    "data": true
}
```
