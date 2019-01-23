

## Native Language Support
| Language               | Language Code            | DialogFlow | Lex | Watson* | Alexa | Luis |
|------------------------|--------------------------|------------|-----|---------|-------|------|
| Arabic                 | ar                       |            |     | YES     |       |      |
| Chinese                |                          |            |     |         |       |      |
| ↳ Cantonese            | zh-HK                    | YES        |     |         |       |      |
| ↳ Simplified           | zh-CN                    | YES        |     | YES     |       | YES  |
| ↳ Traditional          | zh-TW                    | YES        |     | YES     |       |      |
| Czech                  | cs                       |            |     | YES     |       |      |
| Danish                 | da                       | YES        |     |         |       |      |
| Dutch                  | nl                       | YES        |     | YES     |       | YES  |
| English                | en                       | YES        | YES | YES     | YES   |      |
| ↳ Australian locale    | en-AU                    | YES        |     |         | YES   |      |
| ↳ Canadian locale      | en-CA                    | YES        |     |         | YES   |      |
| ↳ Great Britain locale | en-GB                    | YES        |     |         | YES   |      |
| ↳ Indian locale        | en-IN                    | YES        |     |         | YES   |      |
| ↳ US locale            | en-US (equivalent to en) | YES        |     |         | YES   | YES  |
| French                 | fr                       | YES        |     | YES     |       |      |
| ↳ Canadian locale      | fr-CA                    | YES        |     |         | YES   | YES  |
| ↳ France locale        | fr-FR (equivalent to fr) | YES        |     |         | YES   | YES  |
| German                 | de                       | YES        |     | YES     | YES   | YES  |
| Hindi                  | hi                       | YES        |     |         |       |      |
| Indonesian             | id                       | YES        |     |         |       |      |
| Italian                | it                       | YES        |     | YES     | YES   | YES  |
| Japanese               | ja                       | YES        |     | YES     | YES   | YES  |
| Korean                 | ko                       | YES        |     | YES     |       | YES  |
| Norwegian              | no                       | YES        |     |         |       |      |
| Polish                 | pl                       | YES        |     |         |       |      |
| Portuguese             | pt                       | YES        |     |         |       | YES  |
| ↳ Brazilian            | pt-BR                    | YES        |     | YES     |       |      |
| Russian                | ru                       | YES        |     |         |       |      |
| Spanish                | es                       | YES        |     | YES     |       |      |
| ↳ Latin America locale | es-419                   | YES        |     |         |       |      |
| ↳Mexico locale         | es-MX                    |            |     |         | YES   | YES  |
| ↳ Spain locale         | es-ES (equivalent to es) | YES        |     |         | YES   | YES  |
| Swedish                | sv                       | YES        |     |         |       |      |
| Thai                   | th                       | YES        |     |         |       |      |
| Turkish                | tr                       | YES        |     |         |       | YES  |
| Ukranian               | uk                       | YES        |     |         |       |      |


Requires an account with the public AI vendor of choice - AWS Lex, Google Dialogflow or IBM Watson.
* Google's text to speech and speech to text features are released separately
** Watson separately launches support for understanding intents and entities,
Supports intent detection only - slot filling will always elicit for slot values.
( E.g. “I would like to send $12” will detect intent as sendMoney, but still ask “How much”)

Table created with
https://www.tablesgenerator.com/markdown_tables


### References: 
https://cloud.google.com/translate/
https://cloud.google.com/translate/docs/languages (over 100 languages)
https://console.bluemix.net/docs/services/assistant/lang-support.html#supported-languages
https://developer.amazon.com/docs/custom-skills/develop-skills-in-multiple-languages.html
https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-language-support