# ServisBOT: Getting Started with the CLI
This documentation covers getting your first two bots created using the CLI, and then connects them together into one experience using our portal.

It includes:
Getting access to an organization and portal.
Setting up the ServisBOT CLI (sb-cli)
Setting up two bots
Connecting the bots together.


Setup the CLI
Our CLI is available directly on NPM. https://www.npmjs.com/package/@servisbot/servisbot-cli
```
npm install -g @servisbot/servisbot-cli
```

The installation should run with no errors.
you can validate your installation by running the cli.

```
$ sb-cli
```

If installation was a success you will get the manpage for the cli
Login to your organization with the cli

Replace [YOUR ORG] and run the command

```
$ sb-cli login <organization>
```

Then provide email & password. Congrats, your CLI is all set up and you can now build bots

## Creating Your First Bot: Maker-Based

### Creating the Bot
Create a bot using a pre-existing bot template

Each bot template will contain at least one worker, and possibly some BaaS dependencies

You can see a list of templates using the CLI tool

```
$ sb-cli blueprints list
```

Use the CLI to to create a password reset maker BOT

```
$ sb-cli blueprint build-interactive PasswordReset
```
you will be asked some questions to help configure your Bot
```
Starting Build Blueprint Interactively command
? What value would you like to set for botName {{ YOUR_BOT_NAME }}
? What value would you like to set for botDescription getting started bot
? What value would you like to set for botPersona default-bot
```
press Enter and wait for your bot URL to show

e.g. `https://messenger.servisbot.com/preview.html?endpoint={{YOUR_ORG}}-{{YOUR_BOT_NAME}}`


### Test your Bot in portal (optional)
Your Bot will now be available for testing. You can either go to the preview URL provided by the cli, or view the bot using the portal.

* Navigate to http://portal.servisbot.com .
* Log in with the same credentials, and go to "Bot Designer"
* Click on your bot from the list
* Click on the "test" button at the bottom of the screen
* Ask the bot "I would like to reset my password"

### Adjusting your bot
It is simple to add additional utterances to kick off the bot.

You can get worker details by using `describe` command, and using Worker Id you received from `bot describe` command.
  - `sb-cli worker describe <worker srn> --quiet > my-bot-worker.json`
  - within the file, find `UserIntents` Business Slot
```
"userIntents": [
{
  "name": "passwordReset",
  "utterances": [
    "I need to reset my password"
  ],
  "description": "Intent for a user to reset their password"
}
```
- change the message strings within  `utterances` array e.g.
  ```
  "utterances": [
    "I need to reset my password",
    "I would like to reset my password"
  ],
  ```
- update your Bot's worker using `my-bot-worker.json` definition file
  - `sb-cli worker update my-bot-worker.json`
- now you will have to synchronise your Bot with its updated worker
  - `sb-cli bot sync {{YOUR_BOT_NAME}}`

Open the messenger again or click `Reset` in currently opened one and type in the `I had an accident` message and your Bot should reply with the modified message.


## Create Your Second Bot: Classic Flow
Setup and Test Bot

Creating a bot using a pre-existing bot template

```
$ sb-cli blueprint build-interactive classic-flow
```
### View bot designer
* Navigate to http://portal.servisbot.com.
* Log in with the same credentials, and go to "Bot Designer". ( https://portal.servisbot.com/#/bot-designer/ )
* Select the bot that you just created.
* On the bot detail page, cClick on the "test" button at the bottom of the screen.
