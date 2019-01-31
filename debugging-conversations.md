# Debugging Conversations
This article assumes some knowledge of the servisbot-cli, a getting started guide to the CLI can be found here: [Getting Started with the CLI](https://github.com/servisbot/documentation/blob/master/getting-started-cli.md)

## Creating a Conversation
It is possible to create a conversation with a bot using its endpoint through the CLI. After the conversation is created it will begin listening to events for that conversation and open the conversation is your default web browser.

To start a conversation with a given bot use ```sb-cli conversation create <endpoint>```
Further options for this command can be found using ```sb-cli conversation create --help```

### Watching a conversation
It is possible to watch an existing conversation if you have the conversation identifier available.

To start a conversation with a given bot use ```sb-cli conversation watch <conversation_identifier>```
Further options for this command can be found using ```sb-cli conversation watch --help```

### Examples

Example showing output for a simple PING, PONG conversation.
```
# Run the command
sb-cli conversation create ENDPOINT
Starting Create Conversation command

# After creating the event, we are listening
Listening to events for identity eu-west-1:35b871ec-ad65-47a4-95fd-9d7484a9e70d & conversation SkmIdrgNE

# After sending ping to the bot we get a notification to say it was received and routed
{"data":{"event":"Event of type TimelineMessage arrived. Routing to worker: srn.worker.YP5EHpGVr:::r2-ping-worker:::published"}}
```

Example showing output for a simple DING, ?? conversation.
``` 
# Run the command
sb-cli conversation create ENDPOINT
Starting Create Conversation command

# After creating the event, we are listening
Listening to events for identity eu-west-1:35b871ec-ad65-47a4-95fd-9d7484a9e70d & conversation SkmIdrgNE

# After sending ping to the bot we get a notification to say it was received and routed
{"data":{"event":"Event of type TimelineMessage arrived. Routing to worker: srn.worker.YP5EHpGVr:::r2-ping-worker:::published"}}

# After the ping worker decided it cant handle 'ding' we got a new event which showed the workers are empty.
# We have exhausted all our workers in this bot trying to handle the 'ding' message. 
# However we can see that the workers array only has one worker
{  
   "data":{  
      "action":"workersEmpty",
      "payload":{  
         "workers":[  
            {  
               "id":"srn.worker.YP5EHpGVr:::r2-ping-worker:::published",
            }
         ],
         "event":{  
            "version":"v2",
            "type":"TimelineMessage",
            "contentType":"message",
            "contents":{  
               "message":"ding"
            },
            "correlationId":"OJO94vscr",
            "conversationId":"SkmIdrgNE",
            "id":"0KGt51Fsl",
            "to":"server",
            "timestamp":1548929200018,
            "organization":"flowit",
            "identity":"eu-west-1:35b871ec-ad65-47a4-95fd-9d7484a9e70d",
            },
            "currentBotName":"PingBot"
         },
         "workerAction":"workersEmpty"
      }
   }
}

```
