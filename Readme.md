# Chrome Extension Generator - API Documentation

## Overview
The Chrome Extension Generator allows users to generate pre-configured Chrome extensions that connect to specific agents.
It creates custom browser extensions that integrate their AI agents directly into Chrome.

## API Endpoint

### Step 1: Generate & Download Chrome Extension

Generates a downloadable Chrome extension ZIP file pre-configured with the specified agent details.

#### Extension Creation Details
- Choose a unique name for your Chrome extension
- Select an agent ID to associate with the extension
- The extension will be pre-configured with your agent
- You'll get a downloadable ZIP file ready for installation

-------------------------------------------------------------------

**POST** `/chrome-extension/generate-extension`

### Request:

#### Headers
```
Content-Type: application/x-www-form-urlencoded
```

#### Body Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `extension_name` | string | Yes | Unique name for the Chrome extension |
| `agent_id` | string | Yes | ID of the agent the extension should connect to (format: `agnt_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`) |
| `api_key` | string | Yes | Personal AGX API key for usage tracking and billing (Platform Token)|

#### cURL Example
```bash
curl -X POST "https://your-domain.com/chrome-extension/generate-extension" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "extension_name=chrome_extension_name" \
  -d "agent_id=agent_id" \
  -d "api_key=your_agx_api_key_here"
  --output test_output.zip
```

### Response:

#### Success Response
- **Content-Type**: `application/zip`

The response will be a binary ZIP file that users can download and install immediately.

### Step 2: Setup Chrome Extension

#### Installation steps:

1. Download and extract ZIP file
2. Navigate to `chrome://extensions/`
3. Enable "Developer mode" (toggle in top right)
4. Click "Load unpacked" and select extracted folder
5. Extension appears in toolbar - click to start chatting

