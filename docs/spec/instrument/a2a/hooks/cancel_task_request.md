###  Cancel Task Request (Client)
#### 1. Description
This hook is called when the observed client agent sends task cancellation message through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`tasks/cancel`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant cancellation message to the target agent. |
| `deny` | The A2A-compliant cancellation message should be blocked. Task should not be cancelled. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 100,
     "method": "tasks/cancel",
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
    "id": "2b10e2fd-f89c-4ff7-b972-5513cd2daeb4",
    "method" : "tasks/cancel",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 100,
            "method": "tasks/cancel",
            "params": {
            "id": "2232321",
            "metadata": {}
            }
        },
        "reasoning": "This task is taking too long when it should not.",
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


###  Cancel Task Request (Server)
#### 1. Description
This hook is called when the observed server agent receives task cancellation message through A2A protocol.<br>
This hook **must** be used before the observed agent receives the A2A-compliant message.

#### 2. Method
[`tasks/cancel`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant cancellation message. |
| `deny` | The A2A-compliant cancellation message should be blocked. Task should not be cancelled. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 100,
     "method": "tasks/cancel",
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
    "id": "2b10e2fd-f89c-4ff7-b972-5513cd2daeb4",
    "method" : "tasks/cancel",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 100,
            "method": "tasks/cancel",
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