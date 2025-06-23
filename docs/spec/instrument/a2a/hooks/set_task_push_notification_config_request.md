### Set Task Push Notification Config Request (Client)
#### 1. Description
This hook is called when the observed client agent sets or updates notification configuration of a delegated task through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`tasks/pushNotificationConfig/get`](specification.md#48-a2a-protocol-methods)

#### 6.3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant set config message to the target agent. |
| `deny` | The A2A-compliant set config message should be blocked and not sent to the server agent. |
| `modify` | The observed agent should send the A2A update config message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 34,
     "method": "tasks/pushNotificationConfig/set",
     "params": {
        "pushNotificationConfig": {
            "url": "https://agent.notifications.com/webhooks/7767"
        },
        "taskId": "2232321",
        "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "3dbc7111-e6a4-4a18-a005-6ffaa40f7d08",
    "method" : "tasks/pushNotificationConfig/set",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 34,
            "method": "tasks/pushNotificationConfig/set",
            "params": {
                "pushNotificationConfig": {
                    "url": "https://agent.notifications.com/webhooks/7767"
                },
                "taskId": "2232321",
                "metadata": {}
            }
        },
        "reasoning": "I understand why task is taking too long. The url configured is wrong. I will fix it !",
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


### Set Task Push Notification Config Request (Server)
#### 1. Description
This hook is called when the observed server client agent receives a notification configuration update of a delegated task through A2A protocol.<br>
This hook **must** be used before the observed agent processes the A2A-compliant message.

#### 2. Method
[`tasks/pushNotificationConfig/get`](specification.md#48-a2a-protocol-methods)

#### 6.3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant set config message. |
| `deny` | The A2A-compliant set config message should be blocked and not processed by the server agent. |
| `modify` | The observed agent should process the A2A update config message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 34,
     "method": "tasks/pushNotificationConfig/set",
     "params": {
        "pushNotificationConfig": {
            "url": "https://agent.notifications.com/webhooks/7767"
        },
        "taskId": "2232321",
        "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "3dbc7111-e6a4-4a18-a005-6ffaa40f7d08",
    "method" : "tasks/pushNotificationConfig/set",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 34,
            "method": "tasks/pushNotificationConfig/set",
            "params": {
                "pushNotificationConfig": {
                    "url": "https://agent.notifications.com/webhooks/7767"
                },
                "taskId": "2232321",
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