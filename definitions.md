# Definitions
Before you get started, we need to understand the different components to a bot and how they work together:

* *Worker:*  An instance of NLP strategy or process, that responds to a request. Users never see or hear from workers, and you manage them through the capabilities you add to your bot. We have two kinds of workers
** Maker Worker: A type of worker that takes a user intent, aligns it to a business intent and interacts with APIs to carry out a set of steps
** Classic Flow Worker: Uses flow based programing to configure the interaction of the bot
* *Bot:* A collection of workers that come together to meet a set of customer use cases (could be just one worker)
* *Endpoints:* Custom Styling, channel, or customization of a bot. These can be used to display different styling for bots on different domains, or for sub brands. They can also be used to customize a bot for specific channels such as Alexa, or Whatsapp. Not to be confused with API endpoints.
* *ServisBOT BaaS:* mappings between Servisbot and your apis
* *Organization:* A customer account in which bots are created. One organization can have many endpoints, many bots.
* *Virtual Assistant (or VA):* Orchestrator of the bot army. Predicts a user’s intent, getting their messages to the relevant place. Enables intent switching mid conversation flow, translation, redaction, and many more broad conversational features.
