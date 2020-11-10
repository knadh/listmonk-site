# Concepts

## Subscriber

A subscriber is a recipient identified by an e-mail address and name. Subscribers receive e-mails that are sent from listmonk.

### Attributes

Attributes are arbitrary properties attached to a subscriber in addition to their e-mail and name. They are represented as a JSON map. It is not necessary for all subscribers to have the same attributes. Subscribers can be [queried and segmented](../querying-and-segmentation) into lists based on their attributes, and the attributes can be inserted into the e-mails sent to them. For example:

```json
{
  "city": "Bengaluru",
  "likes_tea": true,
  "spoken_languages": ["English", "Malayalam"],
  "projects": 3,
  "stack": {
    "frameworks": ["echo", "go"],
    "languages": ["go", "python"],
    "preferred_language": "go"
  }
}
```

### Segmentation

Segmentation is the process of filtering a large list of subscribers into a smaller group based on arbitrary conditions, primarily based on their attributes. For instance, if an e-mail needs to be sent subscribers who live in a particular city, given their city is described in their attributes, it's possible to quickly filter them out into a new list and e-mail them. [Learn more](../querying-and-segmentation).

## List

A list (or a _mailing list_) is a collection of subscribers grouped under a name, for instance, _clients_. Lists are used to organise subscribers and send e-mails to specific groups.

### Subscription status

Subscribers in a list will have one of these subscription statuses.

| Status        | Description                                                                       |
| ------------- | --------------------------------------------------------------------------------- |
| `unconfirmed` | The subscriber was added to the list directly without their explicit confirmation |
| `confirmed`   | The subscriber added themselves to the list                                       |
| `blocklisted` | The subscriber unsubscribed from the list permanently                             |

## Campaign

A campaign is an e-mail that is sent to one or more lists.

## Template

A template is a re-usable HTML design that can be used across various campaigns. Most commonly, templates have standard header and footer areas with logos and branding elements, where campaign content is inserted in the middle. listmonk supports [Go template](https://gowebexamples.com/templates/) expressions that lets you create powerful, dynamic HTML templates. [Learn more](templating).

## Messenger

listmonk supports multiple custom messaging backends in additional to the default SMTP e-mail backend, enabling not just e-mail campaigns, but arbitrary message campaigns such as SMS, FCM notifications etc. A *Messenger* is a web service that accepts a campaign message pushed to it as a JSON request, which the service can in turn broadcast as SMS, FCM etc. [Learn more](../messengers).

## Tracking pixel

The tracking pixel is a tiny, invisible image that is inserted into an e-mail body to track e-mail views. This allows measuring the read rate of e-mails. While this is exceedingly common in e-mail campaigns, it carries privacy implications and should be used in compliance with rules and regulations such as GDPR.

## Click tracking

It is possible to track the clicks on every link that is sent in an e-mail. This allows measuring the clickthrough rates of links in e-mails. While this is exceedingly common in e-mail campaigns, it carries privacy implications and should be used in compliance with rules and regulations such as GDPR.
