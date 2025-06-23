### Get Task Push Notification Config Request (Client)
#### 1. Description
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`tasks/pushNotificationConfig/get`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant get config message to the target agent. |
| `deny` | The A2A-compliant get config message should be blocked and not sent to the server agent. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 89,
     "method": "tasks/pushNotificationConfig/get",
     "params": {
       "id": "2232321",
       "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "ac7127f4-822b-4f65-a52e-4024635b7971",
    "method" : "tasks/pushNotificationConfig/get",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 89,
            "method": "tasks/pushNotificationConfig/get",
            "params": {
            "id": "2232321",
            "metadata": {}
            }
        },
        "reasoning": "This task is taking too long when it should not. I need to verify the notification config correctness.",
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
                    }
                },
                "role": "client"
            },
            "to": {
                "agent": {
                    "url": "https://api.story.com/v1",
                    "name": "Story teller",
                    "version": "1.0.0"
                },
                "role": "server"
            }
        }
    }
   }
   ```


### Get Task Push Notification Config Request (Server)
#### 1. Description
This hook **must** be used before the observed server agent receives the A2A-compliant message.

#### 2. Method
[`tasks/pushNotificationConfig/get`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant get config message. |
| `deny` | The A2A-compliant get config message should be blocked and not processed by the server agent. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 89,
     "method": "tasks/pushNotificationConfig/get",
     "params": {
       "id": "2232321",
       "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "ac7127f4-822b-4f65-a52e-4024635b7971",
    "method" : "tasks/pushNotificationConfig/get",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 89,
            "method": "tasks/pushNotificationConfig/get",
            "params": {
            "id": "2232321",
            "metadata": {}
            }
        },
        "context": {
            "from": {
                "agent": {
                    "name": "Content generator",
                    "url": "https://cooking-assistant.openai.com/api/v1",
                    "version": "1.0.0",
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
                    "version": "1.0.0"
                },
                "role": "server"
            }
        }
    }
   }
   ```