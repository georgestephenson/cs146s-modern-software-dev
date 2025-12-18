# Week 2: The Anatomy of Coding Agents

## Article: MCP Introduction [(link)](https://stytch.com/blog/model-context-protocol-introduction/)

- MCP - LLMs making consistent API calls
- Universal connectivity between LLMs and tools/APIs
- Built on JSON-RPC 2.0 messages

Request

``` JSON
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/list",
  "params": {}
}
```

Response

``` JSON
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    { "name": "get_weather", "description": "Retrieves weather data.", "schema": { "location": "string" } }
  ]
}
```

- Benefits from more standardisation than custom integrations, OpenAI plugins, or LangChain
- Standardised authentication with OAuth