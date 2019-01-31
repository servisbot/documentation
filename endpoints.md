
# Endpoints
Endpoints custom styling, channel, or customization of a bot specific to an omnichannel entrypoint. These can be used to display different styling for bots on different domains, or for sub brands. They can also be used to customize a bot for specific channels such as Alexa, or Whatsapp. Not to be confused with API endpoints.

Each bot gets created with an default endpoint when it is created.

### Find a the bot's endpoint in bot url
You can find out what a bot's endpoint using the the CLI.

```
https://messenger.servisbot.com/preview.html?endpoint=organization-botname
```

Endpoint name is organization-botname

### Endpoint through the CLI
You can find the a bot endpoint and its settings through the CLI

```
sb-cli endpoint list
```
it will return the bot settings including the endpoint currently set.

```
{
  "Address": "organization-botname",
  "AllowedDomains": [
    "*.production.helium.servismatrix.com",
    "*.production.helium.servismatrixcdn.com",
    "*.servisbot.com",
    "https://servisbot.com"
  ],
  "Created": 1545043630304,
  "Name": "Organization Bot default endpoint",
  "Organization": "organization",
  "Status": "online",
  "TargetBotReference": "Bottname",
  "Updated": 1545043630304,
  "Useragent": "useragent"
  "Style" : {}
}
```

Styles live inside the "Style" object.

*Example styling*
```
        "name": "name",
        "avatar": "https://s3-eu-west-1.amazonaws.com/sborg-heupper-chillinsurance/forge/settings/6o4MqCMzL",
        "subtitle": "Helping You Complete Your Insurance",
        "background": "https://s3-eu-west-1.amazonaws.com/sborg-heupper-chillinsurance/forge/settings/CKBOJWq1Q",
        "messengerBackgroundColor": "#ffffff",
        "headerBackgroundColor": "#4a2783",
        "headerTextColor": "#ffffff",
        "roundelBackgroundColor": "#4a2783",
        "roundelIconColor": "#ffffff",
        "inboundMessageBackgroundColor": "#FFFFFF",
        "inboundMessageTextColor": "#3B3E3F",
        "inboundMessageTextColorSecondary": "#713f98",
        "outboundMessageBackgroundColor": "#713f98",
        "outboundMessageTextColor": "#ffffff",
        "promptHeaderBackgroundColor": "#a7c539",
        "promptHeaderTextColor": "#FFFFFF",
        "promptTextColor": "#a7c539",
        "footerBackgroundColor": "#FFFFFF",
        "footerTextColor": "#999999"
```
