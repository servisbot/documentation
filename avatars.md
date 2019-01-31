# Messenger Avatars
Avatars images are set on a per organization basis and displayed based on messenger configuration.

## To set the image used as an avatar
Log into portal and go to the "Configure Messenger" section. The image can be uploaded to the "Messenger Avatar URL" field in the "Customize Messenger Section"

## To display the avatar in a messenger
The avatar is shown based on a parameter passed to the Servisbot.init call when the messenger is being setup.

You can pass "displayAvatar: true|false" in your Servisbot script.

```
https://messenger.servisbot.com/preview.html?endpoint=organization-botname&displayAvatar=true
```
