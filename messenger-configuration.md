
# ServisBot Messenger Configuration Options
   - **url:** This is the URL that you registered with ServisBot. eg. eg. If you registered your company name as 'Hooli', your url would look like the following - 'https://hooli.servisbot.com'. This option is required.
   - **organization:** the organizational code this bot is related to, i.e. `flowit`
   - **shortBotId:** the 9 character reference for a bot, i.e. `0dloyEMnyA`
   - **dir:** This option determines the direction of text in the messenger. The options are `ltr` and `rtl`. The default option is `ltr`.
   - **displayAvatar:** This option determines whether or not the avatar is shown for the bot in the conversation. This field is optional. If not specified by the user it will not be displayed by default.
   - **displayWidget:** This option determines whether or not the ServisBot widget is displayed. The ServisBot widget is displayed on the bottom right hand corner of your web page, and toggles the view of the ServisBot web messenger. This field is optional.
   - **displayHeader:** This option determines whether or not the header is displayed. This field is optional. If not specified by the user it will be displayed by default.
   - **displayRoundel:** This option determines whether or not the roundel is displayed. This field is optional. If not specified by the user it will be displayed by default.
   - **alwaysOpen:** This field specifies whether the ServisBot web messenger is permanently displayed or not. This field is optional.
   - **context:** extra information to send into the bot.
     - userToken: value used to verify user is within a secureSession.
   - **expiredEvent:** This field specifies a callback to alert parent app with secureSession failures.
   - **googleApiKey:** This field is for the Google API key to be used to display maps in the messenger
   - **WIP!** If you would like to open the messenger from a link on the page instead of opening from the roundel, just add the data attribute `data-servisbot-organization` with your orgnaization name to the anchor tag in your HTML. E.g. `<a data-servisbot-organization='flowit3'>launch a bot</a>`.
