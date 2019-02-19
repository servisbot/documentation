Last Updated 22/10/2018

Integrating the ServisBOT web messenger with your web application couldn’t be simpler. Just follow the quick steps below and have our AI powered chatbots handle your customer queries in no time!
Embeddable Messenger Code

Add the following script to any web page within your web application which you would like to include the ServisBOT web messenger.

<script src="https://servisbotcdn.com/messenger/latest/bundle-messenger.js"></script>
<script>
    ServisBOT.init({
      organization: '{yourOrganization}',
      endpoint: '{yourBotId-within-Organization}',
      displayWidget: true,
      alwaysOpen: true,
      context : { // context can be used for custom properties
        phone: "+17811234567",
        address: "3250 Airport Blvd, Mobile, AL 36606, USA"
      }
    });
</script>

Assuming an identity in messenger

When a conversation is created, an identity for that conversation is also created linking the conversationId to the cognitoId. If you are running within an incognito environment, running messenger on another machine, or you have cleared your local/session storage for whatever reason – it is possible to re-hydrate that conversation and resume where you left off. This can be achieved by using the following 2 methods in lightning.
Query Params

You can pass the identity as a quary param when accessing your messenger url.

https://messenger.servisbot.com/?organization="yourorganization"&identity="youridentity"

ServisBOT SDK init

You can also pass the identity as an optional parameter when initializing the ServisBOT SDK.

<script>
    ServisBOT.init({
        ...otherParameters,
        "identity": "youridentity"  //  Previously created identity
    });
</script>

How to Use Our Code

Simply copy and paste the above code into your web page’s main tag. The code snippet must be inserted before the main closing body tag. You must include the code snippet in all pages that require the ServisBOT web messenger.
ServisBOT Configuration Options

        organization: the organizational code this bot is related to – provided to you by ServisBOT
        shortBotId: <Optional> – the 9 character reference for a specific bot, i.e. 0dloyEMnyA
        displayWidget: <Optional> This option determines whether or not the ServisBOT widget is displayed. The ServisBOT widget is displayed on the bottom right hand corner of your web page, and toggles the view of the ServisBOT web messenger.
        displayHeader: <Optional> This option determines whether or not the header is displayed. If not specified by the user it will be displayed by default.
        displayRoundel: <Optional> This option determines whether or not the roundel is displayed. If not specified by the user it will be displayed by default.
        alwaysOpen: <Optional> This field specifies whether the ServisBOT web messenger is permanently displayed or not.
        context: extra information to send into the bot.
            userToken: value used to verify user is within a secureSession.

How to use this code

    Simply copy and paste the above code into your web page’s main tag.
    The code snippet must be inserted before the main closing body tag ie.
    You must include the code snippet in all pages that require the ServisBOT web messenger
    IMPORTANT: Replace ‘{yourOrganization}’ with the name in which you registered with ServisBOT.

Updating the context

A rewriteContext method is available if you wish to replace the content that was passed to the embeddable messenger at init time:

ServisBOT.rewriteContext({
  organization: '{yourOrganization}',
  shortBotId: '{yourBotId-within-Organization}',
  displayWidget: true,
  alwaysOpen: false,
  context : {
    firstName: 'Michael',
    lastName: 'Schumacher',
  },
});

Managing Conversations via Sherpa

If you have a use case where the conversation needs to be managed by your backend system, for example:

    You have secure information to share between your Sherpa Account and your servers that should not be present in the conversation.
    You want to manage the lifecycle of a conversation, e.g. an end customer may have multiple separate conversations on a single machine and each conversation will have a different context

    Use the ServisBOT API to create the conversation from your server (link)
    Pass the correct Identity and Conversation ID back to your page
    Set the Identity in LocalStorage prior to calling ServisBOT.init()

ServisBOT will provide you with the API Keys, Organisation ID and User Pool ID for your organisation.

/*
  The identity is passed into the page from your backend
*/

localStorage.setItem('{user pool id provided by ServsiBOT}', identity)

Notes:

    You do not need to pass the secure properties via the ServisBOT.init function. (They are passed in the context from the backend)

R2 Conversation creation and Routing

Although conversation creation is entirely handled using the UserRuntime module (previously known as the ConversationsSDK), it is worth noting how lightning signals that it is using R2 components of the UserRuntime module.

When talking to a R2 endpoint, you must provide the endpoint in the query param of the url.

eg. https://messenger.servisbot.com?endpoint=flowit-BotOne

With this url, lightning detects that an endpoint has been provided, and will attach V2 within the config supplied to the UserRunTime module.
Notifications

The host webpage of lightning can receive notifications from our server when using R2 bots. To listen for these notifications you can do the following.

const ServisBOTApi = ServisBOT.init({ ... });
ServisBOTApi.on('notification', (message) => {
    //  At the moment the message is just a simple string notification
    console.log(message);
});
