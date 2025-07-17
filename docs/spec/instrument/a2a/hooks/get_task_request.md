### Get Task Request (Client)
#### 1. Description
This hook is called when the observed client agent incquiry about a delegated task through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`tasks/get`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant get task message to the target agent. |
| `deny` | The A2A-compliant get task message should be blocked and not sent to the server agent. |
| `modify` | The observed agent should send the A2A message with the modified content found in `modifiedRequest` field. |


#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 43,
     "method": "tasks/get",
     "params": {
       "id": "2232321",
       "historyLength": 4, 
       "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "b5ac0ae4-ed6a-4d9f-9e21-9ce110d1ee65",
    "method" : "tasks/get",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 43,
            "method": "tasks/get",
            "params": {
            "id": "2232321",
            "historyLength": 4, 
            "metadata": {}
            }
        },
        "reasoning": "This task is taking too long when it should not. Checking on status.",
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


### Get Task Request (Server)
#### 1. Description
This hook is called when the observed server agent receives an incquiry message about a delegated task through A2A protocol.<br>
This hook **must** be used before the observed agent processes the A2A-compliant message.

#### 2. Method
[`tasks/get`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant get task message. |
| `deny` | The A2A-compliant get task message should be blocked and not processed by the server agent. |
| `modify` | The observed agent should process the A2A message with the modified content found in `modifiedRequest` field. |


#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 43,
     "method": "tasks/get",
     "params": {
       "id": "2232321",
       "historyLength": 4, 
       "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
    "jsonrpc": "2.0",
    "id": "b5ac0ae4-ed6a-4d9f-9e21-9ce110d1ee65",
    "method" : "tasks/get",
    "params": {
        "payload": {
            "jsonrpc": "2.0",
            "id": 43,
            "method": "tasks/get",
            "params": {
            "id": "2232321",
            "historyLength": 4, 
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