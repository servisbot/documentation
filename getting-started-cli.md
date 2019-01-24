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
sb-cli login --org=[YOUR ORG]
```

then provide email & pass
Congrats, your CLI is all set up and you can now build bots

## Creating Your First Bot: Maker-Based

### Creating the Bot
Creating a bot using a pre-existing bot template
Each bot template will contain at least one worker, and possibly some BaaS dependencies
You can see a list of templates using the CLI tool

```
sb-cli list-blueprints
```

Use the CLI to to create a password reset maker BOT

```
sb-cli create-bot -b password-reset-bot --name passwordreset-demo-[yourname]
```

### Test your Bot
Your Bot will now be available for testing. You can either go to the preview URL provided by the cli, or view the bot using the portal.
Navigate to http://portal.servisbot.com .
Log in with the same credentials, and go to "Bot Designer"
Click on your bot from the list
Click on the "test" button at the bottom of the screen
Ask the bot "I would like to reset my password"

## Create Your Second Bot: Flow-Based Programming
### Setup and Test Bot
Creating a bot using a pre-existing bot template
```
sb-cli create-bot -b=k4-avalanche-bot --name flowbasedbot-[yourname]
```

Navigate to http://portal.servisbot.com.
Log in with the same credentials, and go to "Bot Designer". ( https://portal.servisbot.com/#/bot-designer/ )
Select the bot that you just created.
On the bot detail page, cClick on the "test" button at the bottom of the screen.

## Connect the two bots together
Now we're going to add the first password reset bot to the flow we created using the flow-based programming by using the portal.
Log in to the portal
Navigate to http://portal.servisbot.com .
Log in with the same credentials, and go to "Bot Designer"
Click on the k4-avalanche-bot
Scroll to the bottom and click the "Design" button
Double click the "What would you like to do" node.
Add an entry to the list of options to "reset your password", with "reset" as the value.
A new output port (grey box) will appear below the linked Dialog.
Add a new Dialogue box to the canvas
Drag a line from the third output port to the new Dialogue block.
Add a new input block and connect the dialogue block to it.
Add a “Transfer” block and connect the previous input block to it
Doubleclick on the transerblick and select your password reset block
Your flow should now look like this

Deploy your changes, then click publish.
Go back to the tab  where you originally tested the bot
with the messenger and click the "Reset" button.

## Dig Deeper
Using the CLI, it is possible to explore and configure your bot and settings.

Describe a bot
```
$ sb-cli describe-bot --name=testname
Describing Bot name: testname,  correlationId: EOSn-znvb
{
  "Workers": [
    {
      "Type": "r2-businessintent-worker",
      "Id": "srn.worker._1WckDZsy"
    }
  ],
  "State": "RUNNING",
  "SecureSession": false,
  "QuietTimeEnabled": false,
  "Organization": "trollin",
  "Updated": 1545073734937,
  "Created": 1545073734937,
  "Name": "testname"
}
```
You can make adjustments as needed, and then update the bot using a JSON file
```
sb-cli update-bot --file=<file>
```
This bot only has one worker, the details of the worker can be seen by using the CLI to describe it.
```
sb-cli describe-worker --id=srn.worker._1WckDZsy --type=r2-businessintent-worker --status=RUNNING
```

You can create, describe, update and delete the following objects using the CLI
Bots
Workers
Endpoints
BaaS Endpoints
