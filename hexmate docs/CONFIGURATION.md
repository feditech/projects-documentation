# Configuration Guide

This guide explains all configuration options available in HexMate.

## Table of Contents

- [Environment Variables](#environment-variables)
- [Application Configuration](#application-configuration)
- [Module Configuration](#module-configuration)
- [Internationalization](#internationalization)
- [Theme Customization](#theme-customization)
- [API Configuration](#api-configuration)
- [Build Configuration](#build-configuration)

## Environment Variables

Environment variables are defined in the `.env` file in the project root.

### Available Variables

#### REACT_APP_BASE_API

**Type:** String (URL)  
**Required:** Yes  
**Description:** Base URL for the backend API server

```env
REACT_APP_BASE_API=https://api.hexmate.example.com/api/
```

**Important Notes:**
- Must end with a trailing slash
- Must include `/api/` path
- Supports both HTTP and HTTPS
- Can point to localhost for development

**Examples:**
```env
# Production
REACT_APP_BASE_API=https://api.hexmate.example.com/api/

# Staging
REACT_APP_BASE_API=https://staging-api.hexmate.example.com/api/

# Local Development
REACT_APP_BASE_API=https://localhost:7067/api/

# Development Server
REACT_APP_BASE_API=http://localhost:5000/api/
```

#### PUBLIC_URL

**Type:** String (Path)  
**Required:** No  
**Default:** `/`  
**Description:** Base path for the application when deployed to a subdirectory

```env
PUBLIC_URL=/hexmate
```

**Use Cases:**
- Deploying to a subdirectory: `PUBLIC_URL=/apps/hexmate`
- Using a CDN: `PUBLIC_URL=https://cdn.example.com/hexmate`
- Default (root): `PUBLIC_URL=/` or leave blank

#### NODE_ENV

**Type:** String  
**Required:** No (automatically set)  
**Values:** `development`, `production`, `test`  
**Description:** Current environment mode

This is automatically set by npm scripts:
- `npm start` sets `NODE_ENV=development`
- `npm run build` sets `NODE_ENV=production`
- `npm test` sets `NODE_ENV=test`

### Loading Environment Variables

Environment variables are loaded at build time and embedded in the bundle. Changes to `.env` require restarting the development server or rebuilding.

```bash
# After changing .env
# Stop the server (Ctrl+C) and restart
npm start

# Or rebuild for production
npm run build
```

### Environment-Specific Files

You can create multiple environment files:

```
.env                # Default, shared across all environments
.env.local          # Local overrides (not committed to git)
.env.development    # Development-specific
.env.production     # Production-specific
.env.test           # Test-specific
```

**Priority:** `.env.local` > `.env.[environment]` > `.env`

## Application Configuration

### config.json

Location: `public/config.json`

This file configures runtime application settings that can be changed without rebuilding.

```json
{
  "modules": [
    {
      "id": 1,
      "name": "DMS",
      "link": "/dms/documents"
    },
    {
      "id": 2,
      "name": "CTS",
      "link": "/cts/dashboard"
    },
    {
      "id": 3,
      "name": "VMS",
      "link": "/vms/dashboard"
    }
  ],
  "signatureScale": 0.5
}
```

### Configuration Options

#### modules

**Type:** Array of Module Objects  
**Required:** Yes  
**Description:** Defines available modules in the application

**Module Object:**
```typescript
{
  id: number;        // Unique identifier
  name: string;      // Module name (DMS, CTS, or VMS)
  link: string;      // Default route for the module
}
```

**Examples:**

Enable all modules:
```json
{
  "modules": [
    {"id": 1, "name": "DMS", "link": "/dms/documents"},
    {"id": 2, "name": "CTS", "link": "/cts/dashboard"},
    {"id": 3, "name": "VMS", "link": "/vms/dashboard"}
  ]
}
```

Enable only DMS:
```json
{
  "modules": [
    {"id": 1, "name": "DMS", "link": "/dms/documents"}
  ]
}
```

Enable CTS and VMS:
```json
{
  "modules": [
    {"id": 2, "name": "CTS", "link": "/cts/dashboard"},
    {"id": 3, "name": "VMS", "link": "/vms/dashboard"}
  ]
}
```

#### signatureScale

**Type:** Number (0.0 - 1.0)  
**Required:** No  
**Default:** 0.5  
**Description:** Scale factor for signature rendering

```json
{
  "signatureScale": 0.5  // 50% of original size
}
```

**Recommended Values:**
- `0.3` - Small signatures
- `0.5` - Medium signatures (default)
- `0.7` - Large signatures

## Module Configuration

### Enabling/Disabling Modules

Modules can be enabled or disabled by editing `public/config.json`:

**To disable a module:** Remove it from the modules array
**To enable a module:** Add it back with correct id, name, and link

**Important:** Module IDs must match the backend configuration:
- `1` = DMS
- `2` = CTS
- `3` = VMS

### User Module Access

Module access is controlled by user permissions in the backend. Each user has a `modules` field that contains comma-separated module IDs:

- `"1"` - Access to DMS only
- `"2"` - Access to CTS only
- `"3"` - Access to VMS only
- `"1,2"` - Access to DMS and CTS
- `"1,2,3"` - Access to all modules

Admin users automatically have access to all configured modules.

## Internationalization

### Language Configuration

HexMate supports multiple languages through i18next.

**Location:** `/src/locales/`

**Supported Languages:**
- English (en)
- Arabic (ar)

### Adding a New Language

1. Create a new folder in `/src/locales/` (e.g., `/src/locales/fr/`)
2. Add translation files:
   - `translation.json` - General translations
   - `cts.json` - CTS module translations
   - `dms.json` - DMS module translations
   - `vms.json` - VMS module translations

3. Update i18n configuration (typically in `/src/shared/`)

### Translation File Structure

```json
{
  "key": "Translation value",
  "nested": {
    "key": "Nested translation"
  },
  "with_variable": "Hello {{name}}"
}
```

### Default Language

The default language is detected from:
1. User's browser language setting
2. Fallback to English if not supported

## Theme Customization

HexMate uses Material-UI theming. Theme configuration can be customized in the application code.

### Colors

Primary and secondary colors are defined in the theme provider. To customize:

1. Locate theme configuration (typically in a context or App.tsx)
2. Modify color values
3. Rebuild the application

### Styling

HexMate uses:
- Material-UI's `sx` prop for inline styles
- CSS modules for component-specific styles
- Global CSS in `src/index.css`

## API Configuration

### Endpoints

All API endpoints are relative to `REACT_APP_BASE_API`:

```typescript
// If REACT_APP_BASE_API=https://api.example.com/api/

// Login endpoint becomes:
https://api.example.com/api/auth/login

// Documents endpoint becomes:
https://api.example.com/api/dms/documents
```

### Axios Configuration

Axios is configured with:
- Base URL from environment variable
- Request/response interceptors for:
  - Adding authentication tokens
  - Handling token refresh
  - Error handling
  - Request/response logging (development only)

### Authentication

Authentication uses JWT tokens:

**Access Token:**
- Short-lived (typically 15-60 minutes)
- Sent in Authorization header: `Bearer [token]`
- Stored in AuthContext

**Refresh Token:**
- Long-lived (typically 7-30 days)
- Used to obtain new access token
- Automatically used when access token expires

### CORS Configuration

The backend must be configured to accept requests from the frontend origin:

**Development:**
```
Access-Control-Allow-Origin: http://localhost:3000
```

**Production:**
```
Access-Control-Allow-Origin: https://hexmate.example.com
```

## Build Configuration

### package.json Scripts

```json
{
  "scripts": {
    "start": "ncp node_modules/dwt/dist public/dwt-resources && react-scripts start",
    "build": "react-scripts build && ncp node_modules/dwt/dist build/dwt-resources",
    "test": "ncp node_modules/dwt/dist public/dwt-resources && react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

### Script Explanation

#### start
- Copies DWT resources to public folder
- Starts development server on port 3000
- Enables hot module replacement

#### build
- Creates optimized production build
- Outputs to `build/` directory
- Copies DWT resources to build folder
- Minifies and optimizes assets

#### test
- Copies DWT resources to public folder
- Runs Jest test runner
- Watches for changes

### Build Output

After running `npm run build`, the `build/` folder contains:

```
build/
├── static/
│   ├── css/          # Minified CSS
│   ├── js/           # Minified JavaScript
│   └── media/        # Images and fonts
├── dwt-resources/    # Document scanning resources
├── Images/           # Static images
├── fonts/            # Font files
├── index.html        # Entry point
├── config.json       # Runtime configuration
└── ...               # Other static assets
```

### tsconfig.json

TypeScript configuration in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"]
}
```

### Environment-Specific Builds

**Development Build:**
```bash
NODE_ENV=development npm run build
```

**Production Build:**
```bash
NODE_ENV=production npm run build
```

## Advanced Configuration

### Webpack Configuration

HexMate uses Create React App's webpack configuration. To customize:

1. Run `npm run eject` (one-way operation, not recommended)
2. Or use alternatives like `craco` or `react-app-rewired`

### Service Worker

Service worker is not enabled by default. To enable PWA features:

1. Change `serviceWorker.unregister()` to `serviceWorker.register()` in `src/index.tsx`
2. Configure service worker in `src/serviceWorker.ts`
3. Rebuild the application

### Browser Support

Configured in `package.json`:

```json
{
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

## Configuration Best Practices

1. **Never commit sensitive data** to `.env` - use `.env.local` for secrets
2. **Use environment-specific files** for different deployment targets
3. **Keep `config.json` flexible** for runtime configuration changes
4. **Document custom configurations** for team members
5. **Test configuration changes** in a development environment first
6. **Backup configurations** before making changes
7. **Use version control** for configuration templates

## Troubleshooting Configuration

### Environment variables not working

- Ensure variable name starts with `REACT_APP_`
- Restart development server after changes
- Clear browser cache
- Check that `.env` file is in project root

### config.json changes not reflected

- Hard refresh browser (Ctrl+Shift+R)
- Clear browser cache
- Verify JSON syntax
- Check browser console for errors

### Module not appearing

- Check module is in `config.json`
- Verify user has module permission
- Check console for configuration errors
- Ensure module ID matches backend

## See Also

- [Installation Guide](INSTALLATION.md)
- [Development Guide](DEVELOPMENT.md)
- [Deployment Guide](DEPLOYMENT.md)
- [API Documentation](API.md)
