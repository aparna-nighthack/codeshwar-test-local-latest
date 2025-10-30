# Chrome Extension Generator - API Documentation

## Overview
This documentation describes the API endpoint for generating pre-configured Chrome extensions that connect to specific agents. Frontend developers can use this API to build a UI for extension generation.

## API Endpoint

### Generate Chrome Extension
**POST** `/chrome-extension/generate-extension`

Generates a downloadable Chrome extension ZIP file pre-configured with the specified agent details.

### Request

#### Headers
```
Content-Type: application/x-www-form-urlencoded
```

#### Body Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `extension_name` | string | Yes | Unique name for the Chrome extension |
| `agent_id` | string | Yes | ID of the agent the extension should connect to (format: `agnt_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`) |
| `api_key` | string | Yes | AGX API key for usage tracking and billing |

#### cURL Example
```bash
curl -X POST "https://your-domain.com/chrome-extension/generate-extension" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "extension_name=MyAgentExtension" \
  -d "agent_id=agnt_7704717d-31dd-4ce6-a07c-cd489e63aee3" \
  -d "api_key=your_agx_api_key_here"
```

### Response

#### Success Response
- **Status Code**: `200 OK`
- **Content-Type**: `application/zip`
- **Body**: ZIP file containing the pre-configured Chrome extension

The response will be a binary ZIP file that users can download and install immediately.

#### Error Responses
- **Status Code**: `400 Bad Request` - Invalid or missing parameters
- **Status Code**: `401 Unauthorized` - Invalid API key
- **Status Code**: `500 Internal Server Error` - Server-side error during extension generation

## Required UI Components

### Form Fields
Your UI should include these three required input fields:

1. **Extension Name**
   - Type: Text input
   - Required: Yes
   - Purpose: Unique identifier for the Chrome extension

2. **Agent ID**
   - Type: Text input  
   - Required: Yes
   - Purpose: Specifies which agent the extension connects to
   - Format: UUID format (e.g., `agnt_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`)

3. **Platform Token (AGX API Key)**
   - Type: Password input
   - Required: Yes
   - Purpose: Authentication and billing for API usage

### Informational Sections
Include these help sections in your UI:

#### How It Works
Brief description explaining that users can generate pre-configured Chrome extensions that connect immediately to their agents after installation.

#### Extension Creation Details
- Choose unique extension name
- Select agent ID to associate
- Extension comes pre-configured
- Downloadable ZIP file provided

#### Installation Steps
1. Download and extract ZIP file
2. Navigate to `chrome://extensions/`
3. Enable "Developer mode"
4. Click "Load unpacked" and select extracted folder
5. Extension appears in toolbar - click to start chatting

## Implementation Notes

- The endpoint expects form-urlencoded data
- Successful requests return a binary ZIP file for download
- Ensure proper validation of Agent ID format on the frontend
- The API key should be treated as sensitive information (use password input)
- The extension name should be unique to avoid conflicts

## Error Handling
Implement appropriate user feedback for:
- Invalid API keys
- Missing required fields
- Network errors
- Server errors

This endpoint provides everything needed to generate functional Chrome extensions without exposing backend implementation details.
