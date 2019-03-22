# Backend as a Service

- [Backend as a Service](#backend-as-a-service)
  - [Overview](#overview)
  - [Getting started with the BaaS](#getting-started-with-the-baas)
  - [Baas Types](#baas-types)
  - [Request/response parameters](#requestresponse-parameters)
    - [Request body](#request-body)
    - [Request URL](#request-url)
    - [Request header](#request-header)
    - [Response body](#response-body)
    - [Response header](#response-header)

## Overview

With the ServisBot BaaS you can set up API connectors for your Bots. The ServisBot BaaS gives you an interface for configuring all your external APIs.

## Getting started with the BaaS

* Make sure the [CLI](getting-started-cli.md) is installed on your machine
* Create a JSON file called `baas-countries.json` containing a **BaaS Payload**:

```json
{
	"Alias": "countries",                         
	"Type": "api-connector",              
	"Endpoint": "https://restcountries.eu/rest/v2/name/${country}",            
	"RequestMapping": {
    "country": {
      "type": "requestURL",
      "inputPath": "$.country",
      "requestParameter": "country"
  }
  },         
	"ResponseMapping": {},        
	"Headers": {},                
	"Method": "GET",                                
	"Body": {}                                       
}

```

* Run the command `sb-cli baas create baas-countries.json`

This will create an API connector to the `restcountries.eu` website, which is a public API that returns a list of Countries.

* Create a JSON file called `countries-exec-payload.json` with the following content:

```json
{
  "Alias": "countries",
  "country": "switzerland"
}
```

* Run the command `sb-cli baas execute countries-exec-payload.json`

You should get a response that looks like this: 

```
{
  "response": [
    {
      "name": "Switzerland",
      "topLevelDomain": [
        ".ch"
      ],
      // ... more content
    }
  ]
}
```

You now have your first BaaS connector working! Following the same procedure, you can create/update as many BaaS endpoints as you wish. 

For details on how to use the [`RequestMapping`](#requestresponse-parameters) and the [`ResponseMapping`](#requestresponse-parameters), have a look at the respective sections below.


## Baas Types

There are currently 2 types of BaaS: the api-connector and the aws-sdk

The api-connector is used to hit HTTP endpoints. For example:

```javascript
{
  "Alias": "phoneNumberValidate",
  "Body": {},
  "Endpoint": "https://password-reset.herokuapp.com/validatePhoneNumber",
  "Headers": {
    "Authorization": "************************",
    "Content-Type": "application/json"
  },
  "Method": "POST",
  "RequestMapping": {
    "telephoneNumber": {
      "inputPath": "$.telephoneNumber",
      "requestBodyPath": "$.telephoneNumber",
      "type": "requestBody"
    }
  },
  "ResponseMapping": {
    "telephoneNumber": {
      "outputPath": "$.telephoneNumber",
      "responseBodyPath": "$.telephoneNumber",
      "type": "responseBody"
    }
  }
}
```

This BAAS will hit the endpoint called out in the Endpoint parameter with a POST from the Method parameter. The `Authorization` and `Content-Type` headers will be added to the request and the `RequestMapping` and `ResponseMapping` will work per the next section of this document.

The aws-sdk BaaS connector allows you to directly call a functionality within the [AWS SDK](https://aws.amazon.com/tools/).

```javascript
{
  "Alias": "detectSentiment",
  "Body": {},
  "Credentials": "srn:vault::goes::here",
  "Type": "aws-sdk",
  "Endpoint": "Comprehend",
  "Method": "detectSentiment",
  "RequestMapping": {
    "LanguageCode": {
      "inputPath": "$.LanguageCode",
      "requestBodyPath": "$.LanguageCode",
      "type": "requestBody"
    },
    "Text": {
      "inputPath": "$.Text",
      "requestBodyPath": "$.Text",
      "type": "requestBody"
    }
  },
}
```

aws-sdk BaaS entries require your AWS credentials in order to function. They should be saved a Secret, and then referenced by the `Credentials` property.

The `Endpoint` is the AWS service to talk to according to the AWS SDK. In this example, we're using the *Comprehend* service; the `Method` is the function to call in that service, which is *detectSentiment* in this case.

## Request/response parameters

There are 5 different parameter types that can be passed:

* Request body
* Request URL
* Request header
* Response body
* Response header

You can see the examples below for an idea of what each one does.

**Terminology**

To fully understand the various properties that belong to each parameter type, it can be helpful to know about the meaning of the terms used:

* *Input*: content that is sent to the BaaS service from the outside world (e.g. a bot)
* *Output*: content that the BaaS service returns back to the outside world
* *Request*: content that the BaaS service sends to the specified API endpoint
* *Response*: content that the API endpoint returns to the BaaS after being called

### Request body

```javascript
new BaaS.API({
    "RequestMapping": {
        "convId": {
            "type": "requestBody",
            "inputPath": "$.token.contents.public.${convoId}.jwt",
            "requestBodyPath": "$.users.${convoId}.jwt"
        }
    },
    // every other field ...
});
// context
{
  token: { contents: { public: { myconv: { jwt: 'theJwt' } } } },
  convoId: 'myconv'
}
// outputs request body
{ users: { myconv: { jwt: "theJwt" } } }
```

The Request body also supports encoding of files that are stored within s3. Currently only files uploaded via messenger into the gossip attachment folder are support.


```javascript
new BaaS.API({
    "RequestMapping": {
        "policyDoc": {
            "encoding": "Base64", // type of encoding, currently only Base64 is supported 
            "inputPath": "$.fileUrl", // location of the image in the bucket
            "requestBodyPath": "$.policyDoc",
            "type": "requestBody"
    }
  },
    // every other field ...
});
// context
{
  fileUrl: 'https://servisbot-heupper-gossip.s3.eu-west-1.amazonaws.com/attachments/flowit/eu-west-1:123/7YCU-2qCF.jpg?'
}
// outputs request body
{ 
    policyDoc: '<Base64 encoded string of the file>' 
}
```
If for any reason you want to send some important info in the body, you can supply an SRN secret for this too

```javascript
new BaaS.API({
    "body":{
        "importantToken":"srn:vault:global:myorg:secret:my-secret-name:78",
    },
    "RequestMapping": {
  },
    // every other field ...
});

```

### Request URL

```javascript
new BaaS.API({
    "RequestMapping": {
        "jwt": {
            "type": "requestURL",
            "inputPath": "$.token.contents.public.type",
            "requestParameter": "type"
        }
    },
    Endpoint: "http://www.servisbot.com/widgets/${type}"
    // every other field ...
});
// context
{
  token: { contents: { public: { type: 'myType'} } },
  convoId: 'myconv'
}
// outputs
'http://www.servisbot.com/widgets/myType'
```

### Request header

```javascript
new BaaS.API({
    "RequestMapping": {
        "jwt": {
            "type": "requestHeader",
            "inputPath": "$.token.contents.public.jwt",
            "requestParameter": "jwt"
        }
    },
    "Headers": {
        "Authorization": "Bearer ${jwt}",
        "X-AMZ-Auth-${jwt}": "${jwt}"
        //Headers can also contain an SRN now to hide Authorization tokens, i.e.
        "Authorization": "srn:vault:global:myorg:secret:my-secret-name:78"
    }
    // every other field ...
});
// context
{
  token: { contents: { public: { jwt: '1a2b3c'} } },
  convoId: 'myconv'
}
// outputs headers
{ "Authorization": "Bearer 1a2b3c", "X-AMZ-Auth-1a2b3c": "1a2b3c" }
```

### Response body

```javascript
new BaaS.API({
    "ResponseMapping": {
        "jwt": {
            "type": "responseBody",
            "responseBodyPath": "$.token.contents.${somevalue}.jwt",
            "outputPath": "$.users.jwt"
        }
    }),
    // every other field ...
});
// output from the API
{ 
    somevalue: 'public', // $.token.contents.${somevalue}.jwt gets replaced with $.token.contents.public.jwt
    token: { contents: { public: { jwt: '1a2b3c'} } },
}

// outputs response body
{ 
    "users": { "jwt": "1a2b3c" }
}
```

### Response header

```javascript
new BaaS.API({
    "ResponseMapping": {
        "jwt": {
            "type": "responseHeader",
            "responseHeaderKey": "content-type",
            "outputPath": "$.contentType"
        }
    }),
    // every other field ...
});
// response has header
`'content-type', 'application/json; charset=utf-8'`

// outputs
{
    response: { ... },
    status: 200,
    headers: { contentType: "application/json; charset=utf-8" }
}
```
