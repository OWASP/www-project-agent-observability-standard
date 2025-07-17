### Resubscribe To Task Request (Client)
#### 1. Description
This hook is called when the observed client agent resubscirbes to server agent's notifications for delegated task updates through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`tasks/resubscribe`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant message to the target agent and resubsribe to the task. |
| `deny` | The A2A-compliant set config message should be blocked and not sent to the server agent. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 65,
     "method": "tasks/resubscribe",
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
    "id": "f8fbc956-4a0b-4b24-821f-991b80fe8531",
    "method" : "tasks/resubscribe",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 65,
            "method": "tasks/resubscribe",
            "params": {
            "id": "2232321",
            "metadata": {}
            }
        },
        "reasoning": "Connection was lost. I need to resubscribe to get task's artifacts.",
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


### Resubscribe To Task Request (Server)
#### 1. Description
This hook is called when the observed server agent receives a notification resubscription request for delegated task updates through A2A protocol.<br>
This hook **must** be used before the observed agent processes the A2A-compliant.

#### 2. Method
[`tasks/resubscribe`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant message. |
| `deny` | The A2A-compliant set config message should be blocked and not processed by the server agent. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 65,
     "method": "tasks/resubscribe",
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
    "id": "f8fbc956-4a0b-4b24-821f-991b80fe8531",
    "method" : "tasks/resubscribe",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 65,
            "method": "tasks/resubscribe",
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
