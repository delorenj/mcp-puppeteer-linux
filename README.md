# MCP-Puppeteer-Linux

[![smithery badge](https://smithery.ai/badge/@PhialsBasement/mcp-puppeteer-linux)](https://smithery.ai/server/@PhialsBasement/mcp-puppeteer-linux)
A Model Context Protocol server that provides browser automation capabilities using Puppeteer, with full support for Linux display servers (X11 and Wayland). This server enables LLMs to interact with web pages, take screenshots, and execute JavaScript in a real browser environment.

## Display Server Support

This fork adds automatic detection and configuration for Linux display servers:

- Automatic X11/Wayland detection
- Dynamic environment variable configuration
- Support for various desktop environments (GNOME, KDE, etc.)
- Fallback mechanisms and robust error handling
- XWayland compatibility

## Components

### Tools

- **puppeteer_navigate**
  - Navigate to any URL in the browser
  - Input: `url` (string)
- **puppeteer_screenshot**
  - Capture screenshots of the entire page or specific elements
  - Inputs:
    - `name` (string, required): Name for the screenshot
    - `selector` (string, optional): CSS selector for element to screenshot
    - `width` (number, optional, default: 800): Screenshot width
    - `height` (number, optional, default: 600): Screenshot height
- **puppeteer_click**
  - Click elements on the page
  - Input: `selector` (string): CSS selector for element to click
- **puppeteer_hover**
  - Hover elements on the page
  - Input: `selector` (string): CSS selector for element to hover
- **puppeteer_fill**
  - Fill out input fields
  - Inputs:
    - `selector` (string): CSS selector for input field
    - `value` (string): Value to fill
- **puppeteer_select**
  - Select an element with SELECT tag
  - Inputs:
    - `selector` (string): CSS selector for element to select
    - `value` (string): Value to select
- **puppeteer_evaluate**
  - Execute JavaScript in the browser console
  - Input: `script` (string): JavaScript code to execute

### Resources

The server provides access to two types of resources:

1. **Console Logs** (`console://logs`)
   - Browser console output in text format
   - Includes all console messages from the browser
2. **Screenshots** (`screenshot://<name>`)
   - PNG images of captured screenshots
   - Accessible via the screenshot name specified during capture

## Key Features

- Browser automation with Linux display server support
- Automatic X11/Wayland detection and configuration
- Console log monitoring
- Screenshot capabilities
- JavaScript execution
- Basic web interaction (navigation, clicking, form filling)

## Configuration

### Claude Desktop Configuration

```json
{
  "mcpServers": {
    "puppeteer": {
      "command": "pnpm",
      "args": ["start"]
    }
  }
}
```

## Installation

### Automated Installation
1. Clone this repository
2. Run `pnpm install` (or `npm install`)
3. Start the server with `pnpm start` (or `npm start`)

### Manual Installation
1. Clone this repository
2. Install dependencies:
   ```bash
   pnpm install
   ```
3. Start the server:
   ```bash
   pnpm start
   # or if you prefer to use tsx directly:
   pnpm tsx index.ts
   ```

## Configuration

The server can be started with:
```bash
pnpm start
```

This will start a Model Context Protocol server that communicates over stdio. The server is meant to be used as a subprocess by MCP clients.

## Display Server Details

The server automatically detects and configures the appropriate display environment:

### Wayland Support

- Detects Wayland sessions via `WAYLAND_DISPLAY`
- Configures necessary environment variables:
  - `WAYLAND_DISPLAY`
  - `QT_QPA_PLATFORM`
  - `GDK_BACKEND`
  - `MOZ_ENABLE_WAYLAND`
  - `XDG_SESSION_TYPE`

### X11 Support

- Fallback for traditional X11 sessions
- Handles X11-specific variables:
  - `DISPLAY`
  - `XAUTHORITY`
- Supports various desktop environments and window managers

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
