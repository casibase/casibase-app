# casibase-app

A UniApp wrapper for [Casibase](https://github.com/casibase/casibase), the open-source RAG knowledge base platform. This app embeds the Casibase H5 web interface and can be published as a WeChat miniprogram or other mobile platforms.

## Features

- 📱 Cross-platform support (WeChat miniprogram, H5, App, etc.)
- 🔧 Configurable Casibase instance URL
- 🌐 WebView-based integration with Casibase web interface
- 🎨 Loading and error handling
- ⚡ Built with uni-app framework

## Configuration

The Casibase URL can be configured in `src/config.js`:

```javascript
export const config = {
  // The URL of the Casibase H5 page to be embedded
  casibaseUrl: 'https://ai-admin.casibase.com/',
  
  // App information
  appName: 'Casibase',
  appDescription: 'Open-source RAG knowledge base platform'
}
```

To use a different Casibase instance, simply update the `casibaseUrl` value.

## Development

### Install Dependencies

```bash
npm install
```

### Run in Development Mode

For H5:
```bash
npm run dev:h5
```

For WeChat Miniprogram:
```bash
npm run dev:mp-weixin
```

For other platforms, see available scripts in `package.json`.

### Build for Production

For H5:
```bash
npm run build:h5
```

For WeChat Miniprogram:
```bash
npm run build:mp-weixin
```

## WeChat Miniprogram Configuration

Before publishing to WeChat:

1. Update the `appid` in `src/manifest.json` with your WeChat miniprogram AppID
2. Ensure the domain `ai-admin.casibase.com` (or your configured domain) is added to the whitelist in WeChat miniprogram settings
3. Set `urlCheck: false` in `mp-weixin.setting` for development, or configure the business domain properly for production

## Project Structure

```
├── src/
│   ├── pages/
│   │   └── index/
│   │       └── index.vue       # Main page with webview
│   ├── static/                 # Static assets
│   ├── App.vue                 # App entry component
│   ├── main.js                 # App entry file
│   ├── manifest.json           # App configuration
│   ├── pages.json              # Page routing configuration
│   └── config.js               # Casibase URL configuration
├── package.json
└── vite.config.js
```

## License

See [LICENSE](LICENSE) file for details.