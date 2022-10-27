# Bounce processing

Enable bounce processing in Settings -> Bounces. POP3 bounce scanning and APIs only become available once the setting is enabled.

### POP3 bounce mailbox
Configure the bounce mailbox in Settings -> Bounces. Either the "From" e-mail that is set on a campaign (or in settings) should have a POP3 mailbox behind it to receive bounce e-mails, or you should configure a dedicated POP3 mailbox and add that address as the `Return-Path` (envelope sender) header in Settings -> SMTP -> Custom headers box. For example:

```
[
	{"Return-Path": "your-bounce-inbox@site.com"}
]

```

Some mail servers may also return the bounce to the `Reply-To` address, which can also be added to the header settings.

### Webhook API
The bounce webhook API can be used to record bounce events with custom scripting. This could be by reading a mailbox, a database, or mail server logs.

| Method | Endpoint         | Description            |
|--------|------------------|------------------------|
| `POST` | /webhooks/bounce | Record a bounce event. |


| Name              | Data type | Required/Optional | Description                                                                          |
|-------------------|-----------|-------------------|--------------------------------------------------------------------------------------|
| `subscriber_uuid` | String    | Optional          | The UUID of the subscriber. Either this or `email` is required.                      |
| `email`           | String    | Optional          | The e-mail of the subscriber. Either this or `subscriber_uuid` is required.          |
| `campaign_uuid`   | String    | Optional          | UUID of the campaign for which the bounce happened.                                  |
| `source`          | String    | Required          | A string indicating the source, eg: `api`, `my_script` etc.                          |
| `type`            | String    | Required          | `hard` or `soft` bounce. Currently, this has no effect on how the bounce is treated. |
| `meta`            | String    | Optional          | An optional escaped JSON string with arbitrary metadata about the bounce event.      |
 

```shell
curl -u 'username:password' -X POST localhost:9000/webhooks/bounce \
	-H "Content-Type: application/json" \
	--data '{"email": "user1@mail.com", "campaign_uuid": "9f86b50d-5711-41c8-ab03-bc91c43d711b", "source": "api", "type": "hard", "meta": "{\"additional\": \"info\"}}'

```

### External webhooks
listmonk supports receiving bounce webhook events from the following SMTP providers.

| Endpoint                    | Description      |           |
|-----------------------------|------------------|-----------|
| `https://listmonk.yoursite.com/webhooks/service/ses`      | Amazon (AWS) SES | [More info](https://docs.mautic.org/en/channels/emails/bounce-management#amazon-webhook). Follow the same steps as Mautic but use your listmonk's endpoint instead. |
| `https://listmonk.yoursite.com/webhooks/service/sendgrid` | Sendgrid / Twilio Signed event webhook         | [More info](https://docs.sendgrid.com/for-developers/tracking-events/getting-started-event-webhook-security-features) |
