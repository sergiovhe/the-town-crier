# The Town Crier

[![Build Status](https://travis-ci.com/sergiovhe/the-town-crier.svg?branch=master)](https://travis-ci.com/sergiovhe/the-town-crier)

<p align="center">
  <img src="https://raw.githubusercontent.com/sergiovhe/warriors-webhooks-app/master/img/ttc.jpg" alt="The Town Crier" width="380">
  <br><br>
</p>

This app just post an actionable message card to an Office 365 group, it is intended to be used to manage events from TFS service hooks, for example when a pull request is created.

The following code represent the structure of the body to create an actionable message card:

```json
{
  "@context": "http://schema.org/extensions",
  "@type": "MessageCard",
  "themeColor": "0072C6",
  "title": "Visit the Outlook Dev Portal",
  "text": "Click **Learn More** to learn more about Actionable Messages!",
  "potentialAction": [
    {
      "@type": "ActionCard",
      "name": "Send Feedback",
      "inputs": [
        {
          "@type": "TextInput",
          "id": "feedback",
          "isMultiline": true,
          "title": "Let us know what you think about Actionable Messages"
        }
      ],
      "actions": [
        {
          "@type": "HttpPOST",
          "name": "Send Feedback",
          "isPrimary": true,
          "target": "http://..."
        }
      ]
    },
    {
      "@type": "OpenUri",
      "name": "Learn More",
      "targets": [
        { "os": "default", "uri": "https://docs.microsoft.com/en-us/outlook/actionable-messages" }
      ]
    }
  ]
}
```

To create a new service hook in VSTS go to Settings > Service Hooks and trigger the action with the desired event from TFS

More info: https://docs.microsoft.com/en-us/outlook/actionable-messages/actionable-messages-via-connectors

## Pull requests

#### Configuring a new pull requests notification subscription

1. Trigger on 'Pull request created' event
2. Add the URL to which the HTTP POST will be sent
3. Add 'incoming-webhook-url' HTTP header key with the desired Office 365 Incoming Webhook URL

![VSTS Service Hook creation](https://raw.githubusercontent.com/sergiovhe/warriors-webhooks-app/master/img/vsts-webhook-creation.gif)

Resulting card posted in our channel:

<p align="center">
  <img src="https://raw.githubusercontent.com/sergiovhe/warriors-webhooks-app/master/img/actionable-card.png" alt="actionable-card" width="800">
  <br><br>
</p>
