###  Send Message Request (Client)

#### 1. Description
This hook is called when the observed client agent sends a message to server agent to initiate a new interaction or to continue an existing one through A2A protocol.<br>
This hook **must** be used before the observed agent sends the A2A-compliant message to server agent.

#### 2. Method
[`message/send`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should send the A2A-compliant to the target agent. |
| `deny` | The A2A-compliant message should be blocked and not sent to the target agent. |
| `modify` | The observed agent should send the A2A message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 1,
     "method": "message/send",
     "params": {
       "message": {
         "role": "agent",
         "parts": [
           {
             "kind": "text",
             "text": "how to prepare a cheese cake?"
           }
         ],
         "messageId": "9229e770-767c-417b-a0b0-f0741243c589"
       },
       "metadata": {}
     }
   }
   ```

#### 5. AOS payload
   ```json
   {
        "jsonrpc": "2.0",
        "id": "03c5db45-6455-4081-897a-4225267113ce",
        "method": "message/send",
        "params": {
            "payload": {
                "jsonrpc": "2.0",
                "id": 1,
                "method": "message/send",
                "params": {
                    "message": {
                        "role": "agent",
                        "parts": [
                        {
                            "kind": "text",
                            "text": "how to prepare a cheese cake?"
                        }
                        ],
                        "messageId": "9229e770-767c-417b-a0b0-f0741243c589"
                    },
                    "metadata": {}
                }
            },
            "reasoning": "Best to complete the task is to delegate it to the agent that specializes in cakes.",
            "context": {
                "from": {
                    "agent": {
                        "name": "Cooking assistant",
                        "url": "https://cooking-assistant.openai.com/api/v1",
                        "instructions": "You are a helpful assistant that can answer questions and help with tasks related to cooking.",
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
                        "url": "https://api.cakebaker.com/v1",
                        "name": "Cake Baker",
                        "version": "1.0.0"
                    },
                    "role": "server"
                }
            }
        }
    }
   ```


###  Send Message Request (Server)

#### 1. Description
This hook is called when the observed server agent received send message request.<br>
This hook **must** be used before the observed agent processes the A2A-compliant message.

#### 2. Method
[`message/send`](specification.md#48-a2a-protocol-methods)

#### 3. Reponse
The response is an [`AOSSuccessResponse`](specification.md#51-aossuccessresponse-object) object.

| Decision | Behavior |
| :--------- | :---------- |
| `allow` | The observed agent should process the A2A-compliant. |
| `deny` | The A2A-compliant message should be ignored and not processed by the server agent. |
| `modify` | The observed agent should process the A2A message with the modified content found in `modifiedRequest` field. |

#### 4. A2A payload
   ```json
   {
     "jsonrpc": "2.0",
     "id": 1,
     "method": "message/send",
     "params": {
       "message": {
         "role": "agent",
         "parts": [
           {
             "kind": "text",
             "text": "how to prepare a cheese cake?"
           }
         ],
         "messageId": "9229e770-767c-417b-a0b0-f0741243c589"
       },
       "metadata": {}
     }
   }
   ```
#### 5. AOS payload
   ```json
   {
        "jsonrpc": "2.0",
        "id": "03c5db45-6455-4081-897a-4225267113ce",
        "method": "message/send",
        "params": {
            "payload": {
                "jsonrpc": "2.0",
                "id": 1,
                "method": "message/send",
                "params": {
                    "message": {
                        "role": "agent",
                        "parts": [
                        {
                            "kind": "text",
                            "text": "how to prepare a cheese cake?"
                        }
                        ],
                        "messageId": "9229e770-767c-417b-a0b0-f0741243c589"
                    },
                    "metadata": {}
                }
            },
            "context": {
                "from": {
                    "agent": {
                        "url": "https://cooking-assistant.openai.com/api/v1",
                        "name": "Cooking assistant",
                        "version": "1.0.0"
                    },
                    "role": "client"
                },
                "to": {
                    "agent": {
                        "name": "Cake Bake",
                        "url": "https://api.cakebaker.com/v1",
                        "instructions": "You are a helpful assistant that specializies in answering questions and tasks related to cake baking.",
                        "version": "1.0.0",
                        "provider": {
                            "name": "AzureAIFoundry",
                            "url": "https://ai.azure.com"
                        }
                    },
                    "role": "server"
                }
            }
        }
    }
   ```