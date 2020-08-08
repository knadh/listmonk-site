# Templating

A template is a re-usable HTML design that can be used across various campaigns. Most commonly, templates have standard header and footer areas with logos and branding elements, where campaign content is inserted in the middle. listmonk supports Go template expressions that lets you create powerful, dynamic HTML templates.

listmonk supports [Go template](https://gowebexamples.com/templates/) expressions that lets you create powerful, dynamic HTML templates.

## Template functions and expressions

There are several template functions and expressions that can be used in campaign and template bodies. They are written in the form `{{ .Subscriber.Email }}`, that is, the expression between double curly braces `{{` and `}}`.

### Subscriber fields

| Expression              | Description                                                                                  |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| `.Subscriber.UUID`      | The randomly generated unique ID of the subscriber                                           |
| `.Subscriber.Email`     | E-mail ID of the subscriber                                                                  |
| `.Subscriber.Name`      | Name of the subscriber                                                                       |
| `.Subscriber.FirstName` | First name of the subscriber (automatically extracted from the name)                         |
| `.Subscriber.LastName`  | Last name of the subscriber (automatically extracted from the name)                          |
| `.Subscriber.Status`    | Status of the subscriber (enabled, disabled, blocklisted)                                    |
| `.Subscriber.Attribs`   | Map of arbitrary attributes. Fields can be accessed with `.`, eg: `.Subscriber.Attribs.city` |
| `.Subscriber.CreatedAt` | Timestamp when the subscriber was first added                                                |
| `.Subscriber.UpdatedAt` | Timestamp when the subscriber was modified                                                   |

| Expression            | Description                                              |
| --------------------- | -------------------------------------------------------- |
| `.Campaign.UUID`      | The randomly generated unique ID of the campaign         |
| `.Campaign.Name`      | Internal name of the campaign                            |
| `.Campaign.Subject`   | E-mail subject of the campaign                           |
| `.Campaign.FromEmail` | The e-mail address from which the campaign is being sent |

### Functions

| Function                                    | Description                                                                                                                                                    |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `{{ Date "2006-01-01" }}`                   | Prints the current datetime for the given format expressed as a [Go date layout](https://medium.com/@Martynas/formatting-date-and-time-in-golang-5816112bf098) |
| `{{ TrackLink "https://actual-link.com" }}` | Takes a URL and generates a tracking URL over it. For use in campaign bodies and templates.                                                                    |
| `{{ TrackView }}`                           | Inserts a single tracking pixel. Should only be used once, ideally in the template footer.                                                                     |
| `{{ UnsubscribeURL }}`                      | Unsubscription URL. Ideal for use in the template footer.                                                                                                      |
| `{{ MessageURL }}`                          | URL to view the hosted version of an e-mail message.                                                                                                           |
| `{{ OptinURL }}`                            | URL to the double-optin confirmation page.                                                                                                                     |

### Example template

The expression `{{ template "content" . }}` should appear exactly once in every template denoting the spot where an e-mail's content is inserted. Here's a sample HTML e-mail that has a fixed header and footer that inserts the content in the middle.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body {
        background: #eee;
        font-family: Arial, sans-serif;
        font-size: 6px;
        color: #111;
      }
      header {
        border-bottom: 1px solid #ddd;
        padding-bottom: 30px;
        margin-bottom: 30px;
      }
      .container {
        background: #fff;
        width: 450px;
        margin: 0 auto;
        padding: 30px;
      }
    </style>
  </head>
  <body>
    <section class="container">
      <header>
        <!-- This will appear in the header of all e-mails.
             The subscriber's name will be automatically inserted here. //-->
        Hi {{ .Subscriber.FirstName }}!
      </header>

      <!-- This is where the e-mail body will be inserted //-->
      <div class="content">
        {{ template "content" . }}
      </div>

      <footer>
        Copyright 2019. All rights Reserved.
      </footer>

      <!-- The tracking pixel will be inserted here //-->
      {{ TrackView }}
    </section>
  </body>
</html>
```

### Example campaign body

Campaign bodies can be composed using the built-in WYSIWYG editor or as raw HTML documents. Assuming that the subscriber has a set of [attributes defined](../querying-and-segmentation#sample-attributes), this example shows how to render those values in a campaign.

```
Hey, did you notice how the template showed your first name?
Your last name is {{.Subscriber.LastName }}.

You have done {{ .Subscriber.Attribs.projects }} projects.


{{ if eq .Subscriber.Attribs.city "Bengaluru" }}
  You live in Bangalore!
{{ else }}
  Where do you live?
{{ end }}


Here is a link for you to click that will be tracked.
<a href="{{ TrackLink "https://google.com" }}">Google</a>

```

The above example uses an `if` condition to show one of two messages depending on the value of a subscriber attribute. Many such dynamic expressions are possible with Go templating expressions.
