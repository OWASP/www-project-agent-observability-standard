### Stream Message Request (Client)
#### 1. Description
This hook is called when the observed client agent sends a message to server agent to initiate a new interaction or to continue an existing one AND subsribes to real-time updates for the task through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`message/stream`](specification.md#48-a2a-protocol-methods)


#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant message to the target agent. |
| `deny` | The A2A-compliant message should be blocked and not sent to the target agent. |
| `modify` | The observed agent should send the A2A message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "message/stream",
  "params": {
    "message": {
      "role": "user",
      "parts": [
        {
          "kind": "text",
          "text": "write a long paper describing the attached pictures"
        },
        {
          "kind": "file",
          "file": {
            "mimeType": "image/png",
            "data": "<base64-encoded-content>"
          }
        }
      ],
      "messageId": "bbb7dee1-cf5c-4683-8a6f-4114529da5eb"
    },
    "configuration": {
        "acceptedOutputModes": [],
        "pushNotificationConfig": {
            "url": "https://agent.notifications.com/webhooks/1234567"
        }
    },
    "metadata": {}
  }
}
   ```
#### 5. AOS payload
   ```json
{
    "jsonrpc": "2.0",
    "id": "56e55ffd-fe11-4c64-b7c9-ddc936dbaed2",
    "method": "message/stream",
    "params": {
        "payload":{
            "jsonrpc": "2.0",
            "id": 2,
            "method": "message/stream",
            "params": {
                "message": {
                    "role": "user",
                    "parts": [
                        {
                        "kind": "text",
                        "text": "write a long paper describing the attached pictures"
                        },
                        {
                        "kind": "file",
                        "file": {
                            "mimeType": "image/png",
                            "data": "<base64-encoded-content>"
                        }
                        }
                    ],
                    "messageId": "bbb7dee1-cf5c-4683-8a6f-4114529da5eb"
                },
                "configuration": {
                    "acceptedOutputModes": [],
                    "pushNotificationConfig": {
                        "url": "https://agent.notifications.com/webhooks/1234567"
                    }
                },
                "metadata": {}
            }
        },
        "reasoning": "I will deelegate this request to the specialized agent.",
        "context": {
            "from": {
                "agent": {
                    "name": "Content generator",
                    "url": "https://cooking-assistant.openai.com/api/v1",
                    "instructions": "You are a helpful assistant that can answer questions and help with tasks.",
                    "version": "1.0.0",
                    "provider": {
                        "name": "OpenAI",
                        "url": "https://openai.com"
                    },
                    "identity": {
                        "signatures": [{
                            "header": {
                                "kid": "agent-key-12345",
                                "alg": "RS256"
                            },
                            "protected": "eyJhbGciOiJSUzI1NiIsImtpZCI6ImFnZW50LWtleS0xMjM0NSJ9",
                            "signature": "hJtXIZ2uSN5kbQfbtTNWbp5A0L9FZo1zq08ne-XY2_Ij8jWQkQxCWuAZN3dLr9YkO6cP5n2hY7pQ6D3ZdH9L3JzGb9rQlXyUpz7U8pF8xKXucE2kM5mO-lHT5Fnjz9Z8"
                        }]
                    }
                },
                "role": "client"
            },
            "to": {
                "agent": {
                    "url": "https://api.story.com/v1",
                    "name": "Story teller",
                    "version": "1.0.0",
                    "identity": {
                        "signatures": [{
                            "header": {
                                "alg": "ES256",
                                "kid": "agent-key-789"
                            },
                            "protected": "eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Im1hY2hpbmUtaWRlbnRpdHkta2V5LTc4OSJ9",
                            "signature": "MEUCIQD1ZT2VwBZ2BbnRrNQkzksYoP2KsbO8GqLxQ3-BUQqFdgIgOR9XhyXUsYMBk0yPyeyG_0Sl4vw4H8K9uN2f6nlm4LU"
                        }]
                    }
                },
                "role": "server"
            }
        }
    }
}
   ```


### Stream Message Request (Server)
#### 1. Description
This hook is called when the observed server agent receves stream message request from a client agent.<br>
This hook **must** be used before the observed agent processes the A2A-compliant message.

#### 2. Method
[`message/stream`](specification.md#48-a2a-protocol-methods)


#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant message. |
| `deny` | The A2A-compliant message should be ignored and not processed by the server agent. |
| `modify` | The observed agent should process the A2A message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "message/stream",
  "params": {
    "message": {
      "role": "user",
      "parts": [
        {
          "kind": "text",
          "text": "write a long paper describing the attached pictures"
        },
        {
          "kind": "file",
          "file": {
            "mimeType": "image/png",
            "data": "<base64-encoded-content>"
          }
        }
      ],
      "messageId": "bbb7dee1-cf5c-4683-8a6f-4114529da5eb"
    },
    "configuration": {
        "acceptedOutputModes": [],
        "pushNotificationConfig": {
            "url": "https://agent.notifications.com/webhooks/1234567"
        }
    },
    "metadata": {}
  }
}
   ```
#### 5. AOS payload
   ```json
{
    "jsonrpc": "2.0",
    "id": "56e55ffd-fe11-4c64-b7c9-ddc936dbaed2",
    "method": "message/stream",
    "params": {
        "payload":{
            "jsonrpc": "2.0",
            "id": 2,
            "method": "message/stream",
            "params": {
                "message": {
                    "role": "user",
                    "parts": [
                        {
                        "kind": "text",
                        "text": "write a long paper describing the attached pictures"
                        },
                        {
                        "kind": "file",
                        "file": {
                            "mimeType": "image/png",
                            "data": "<base64-encoded-content>"
                        }
                        }
                    ],
                    "messageId": "bbb7dee1-cf5c-4683-8a6f-4114529da5eb"
                },
                "configuration": {
                    "acceptedOutputModes": [],
                    "pushNotificationConfig": {
                        "url": "https://agent.notifications.com/webhooks/1234567"
                    }
                },
                "metadata": {}
            }
        },
        "context": {
            "from": {
                "agent": {
                    "name": "Content generator",
                    "url": "https://cooking-assistant.openai.com/api/v1",
                    "version": "1.0.0",
                    "identity": {
                        "signatures": [{
                            "header": {
                                "kid": "agent-key-12345",
                                "alg": "RS256"
                            },
                            "protected": "eyJhbGciOiJSUzI1NiIsImtpZCI6ImFnZW50LWtleS0xMjM0NSJ9",
                            "signature": "hJtXIZ2uSN5kbQfbtTNWbp5A0L9FZo1zq08ne-XY2_Ij8jWQkQxCWuAZN3dLr9YkO6cP5n2hY7pQ6D3ZdH9L3JzGb9rQlXyUpz7U8pF8xKXucE2kM5mO-lHT5Fnjz9Z8"
                        }]
                    }
                },
                "role": "client"
            },
            "to": {
                "agent": {
                    "url": "https://api.story.com/v1",
                    "name": "Story teller",
                    "instruction": "You are a very creative story teller.",
                    "provider": {
                        "name": "AzureAIFoundry",
                        "url": "https://ai.azure.com"
                    },
                    "version": "1.0.0",
                    "identity": {
                        "signatures": [{
                            "header": {
                                "alg": "ES256",
                                "kid": "agent-key-789"
                            },
                            "protected": "eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Im1hY2hpbmUtaWRlbnRpdHkta2V5LTc4OSJ9",
                            "signature": "MEUCIQD1ZT2VwBZ2BbnRrNQkzksYoP2KsbO8GqLxQ3-BUQqFdgIgOR9XhyXUsYMBk0yPyeyG_0Sl4vw4H8K9uN2f6nlm4LU"
                        }]
                    }
                },
                "role": "server"
            }
        }
    }
}
   ```