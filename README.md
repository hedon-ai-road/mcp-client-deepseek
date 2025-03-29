# MCP Client with DeepSeek

## Requirements

- Python 3.10+
- DeepSeek API Key
- uv

## Quick Start

### Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Make directory and clone current repository

```bash
mkdir mcp-client-deepseek
git clone git@github.com:hedon-ai-road/mcp-client-deepseek.git
```

### Install the MCP Server `weather`

```bash
git clone git@github.com:hedon-ai-road/mcp-weather.git
```

### Prepare DeepSeek API Key

- Go to [DeepSeek Platform](https://platform.deepseek.com/api_keys)
- Create a new API key
- Save the API key to the `.env` file as `DEEPSEEK_API_KEY`

```bash
echo "DEEPSEEK_API_KEY=<your_api_key>" >> .env
```

### Run the client

```bash
cd mcp-client-deepseek
uv run client.py ../mcp-weather/weather.py
```

### Ask the weather

The output may look like this:

```shell
Processing request of type ListToolsRequest

Connected to server with tools: ['get_alerts', 'get_forecast']

MCP Client Started!
Type your queries or 'quit' to exit.

Query: What's the weather in LA today?
Processing request of type ListToolsRequest

Available tools: ['get_alerts', 'get_forecast']

DeepSeek Response: [Choice(finish_reason='tool_calls', index=0, logprobs=None, message=ChatCompletionMessage(content='', refusal=None, role='assistant', annotations=None, audio=None, function_call=None, tool_calls=[ChatCompletionMessageToolCall(id='call_0_3c4d5f7d-6ed9-47e6-ae3c-67ced88d5c80', function=Function(arguments='{"latitude":34.0522,"longitude":-118.2437}', name='get_forecast'), type='function', index=0)]))]
Processing request of type CallToolRequest
HTTP Request: GET https://api.weather.gov/points/34.0522,-118.2437 "HTTP/1.1 200 OK"
HTTP Request: GET https://api.weather.gov/gridpoints/LOX/155,45/forecast "HTTP/1.1 200 OK"

DeepSeek Response after tools: [Choice(finish_reason='stop', index=0, logprobs=None, message=ChatCompletionMessage(content='Here’s a concise summary of the weather in Los Angeles (LA) for today and the next few days:  \n\n### **Today (Current Conditions)**  \n- **Temperature:** 67°F (mild)  \n- **Conditions:** Mostly sunny  \n- **Wind:** 5–10 mph WSW (gusts up to 20 mph)  \n\n### **Tonight**  \n- **Low:** 51°F  \n- **Conditions:** Mostly cloudy  \n- **Wind:** 5–10 mph S  \n\n### **Sunday**  \n- **High:** 64°F  \n- **Conditions:** Mostly cloudy, 30% chance of rain (after 11 AM)  \n- **Wind:** 5–15 mph S  \n\n### **Sunday Night**  \n- **Low:** 54°F  \n- **Conditions:** 40% chance of rain, mostly cloudy  \n\n### **Monday**  \n- **High:** 64°F  \n- **Conditions:** 40% chance of rain (before 5 PM), mostly cloudy  \n\n### **Key Notes:**  \n- Light rain possible Sunday and Monday (low accumulation).  \n- Mild temperatures, with lows in the 50s and highs in the mid-60s.  \n\nWould you like hourly details or extended forecasts?', refusal=None, role='assistant', annotations=None, audio=None, function_call=None, tool_calls=None))]

[Calling tool get_forecast with args {'latitude': 34.0522, 'longitude': -118.2437}]
Here’s a concise summary of the weather in Los Angeles (LA) for today and the next few days:

### **Today (Current Conditions)**
- **Temperature:** 67°F (mild)
- **Conditions:** Mostly sunny
- **Wind:** 5–10 mph WSW (gusts up to 20 mph)

### **Tonight**
- **Low:** 51°F
- **Conditions:** Mostly cloudy
- **Wind:** 5–10 mph S

### **Sunday**
- **High:** 64°F
- **Conditions:** Mostly cloudy, 30% chance of rain (after 11 AM)
- **Wind:** 5–15 mph S

### **Sunday Night**
- **Low:** 54°F
- **Conditions:** 40% chance of rain, mostly cloudy

### **Monday**
- **High:** 64°F
- **Conditions:** 40% chance of rain (before 5 PM), mostly cloudy

### **Key Notes:**
- Light rain possible Sunday and Monday (low accumulation).
- Mild temperatures, with lows in the 50s and highs in the mid-60s.

Would you like hourly details or extended forecasts?
```
