# Bot Blueprints
Blueprints are the starting point for most bot experiences. Much of the ServisBOT definitions and settings are already taken care of so that you can get into the system and start playing with a bot. In the case of blueprints that integrate with external services, you will have limited ability to modify the bot experience if you use the default settings. Getting more advanced will required you [get your hands dirty with the CLI](getting-started-cli.md) or create bots in Dialogflow/Lex.

## Generic Lex Bot
A bot capable of replying to queries configured in Lex bot.

## Password Reset
An example Business Intent Bot using Lex and a Baas integrated with twilio for a password reset. 

## Rosetta Stone
Performs language detection and translation within flow via BaaS calls.

## Lex + Classic Flow
Performs intent detection with Lex. If a match is found, the Lex response is sent onwards. Otherwise, the message routes to a Classic Flow.

## Dialogflow + Classic Flow
Performs intent detection with Dialogflow. If a match is found, the Dialogflow resopnse is sent onwards. Otherwise, the message routes to a Classic Flow.

## Dialogflow + Classic Flow
Performs intent detection with Dialogflow and the Dialogflow resopnse is sent onwards.

## Classic Flow
The message is routed to a Classic Flow. Illustrates flow-based conversation techniques.

## Claims Bot FAQ
A bot capable of anserwing questions related to insurance policy.

## Claims Bot
A bot capable of performing an accident claim for an insurance company.
