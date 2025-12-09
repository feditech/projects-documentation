# Configuration

This guide covers how to configure the Units warehouse management system.

## Environment Configuration

### Environment Variables

The application uses environment variables for configuration. These are defined in the `.env` file at the project root.

#### Required Variables

**`REACT_APP_BASE_API`**

- **Description**: Base URL for the backend API
- **Example**: `https://api.units.abc.com/api/`
- **Note**: Must end with a trailing slash
- **Required**: Yes

**`REACT_APP_GOOGLE_MAPS_API_KEY`**

- **Description**: Google Maps API key for address selection and mapping
- **Example**: `AIzaSyA3FzKwewewqqqqaubinG6wqCZt8Dw7Yk`
- **Required**: Yes (for address features)
- **How to get**: [Google Cloud Console](https://console.cloud.google.com/)

#### Example `.env` File

```env
REACT_APP_BASE_API=https://api.units.abc.com/api/
REACT_APP_GOOGLE_MAPS_API_KEY=your-google-maps-api-key-here
```

### Environment-Specific Configuration

#### Development Environment

```env
REACT_APP_BASE_API=http://localhost:5000/api/
REACT_APP_GOOGLE_MAPS_API_KEY=your-dev-api-key
```

#### Staging Environment

```env
REACT_APP_BASE_API=https://staging-api.units.abc.com/api/
REACT_APP_GOOGLE_MAPS_API_KEY=your-staging-api-key
```

#### Production Environment

```env
REACT_APP_BASE_API=https://api.units.abc.com/api/
REACT_APP_GOOGLE_MAPS_API_KEY=your-production-api-key
```

## Application Configuration

### Language Configuration

The application supports English and Arabic by default.

#### Adding New Language

1. **Create translation file**:

   ```
   src/locales/{language-code}/translation.json
   ```

2. **Add translations**:

   ```json
   {
     "Dashboard": "Translated Dashboard",
     "Orders": "Translated Orders",
     ...
   }
   ```

3. **Register language** in `src/index.tsx`:
   ```typescript
   i18n.use(initReactI18next).init({
     resources: {
       en: { translation: enTranslation },
       ar: { translation: arTranslation },
       es: { translation: esTranslation } // New language
     },
     ...
   });
   ```

#### Setting Default Language

Edit `src/index.tsx`:

```typescript
i18n.use(initReactI18next).init({
  lng: 'en', // Change default language here
  fallbackLng: 'en',
  ...
});
```

### Theme Configuration

#### Customizing Theme

Themes are managed in the `TenantThemeProvider` component.

**Edit**: `src/components/business/tenantthemeprovider.tsx`

```typescript
const theme = createTheme({
  palette: {
    primary: {
      main: "#1976d2", // Primary color
    },
    secondary: {
      main: "#dc004e", // Secondary color
    },
  },
  typography: {
    fontFamily: '"Roboto", "Helvetica", "Arial", sans-serif',
  },
});
```

#### Tenant-Specific Themes

For multi-tenant deployments, themes can be customized per tenant:

1. Store theme settings in database
2. Load via `TenantContext`
3. Apply dynamically in `TenantThemeProvider`

### Date and Time Configuration

#### Date Format

Default format is based on locale:

- English: MM/DD/YYYY
- Arabic: DD/MM/YYYY

To customize, edit date picker components in `src/components/units_controls/`

#### Timezone

The application uses the browser's local timezone. To set a specific timezone:

1. Install `moment-timezone`:

   ```bash
   npm install moment-timezone
   ```

2. Configure default timezone:
   ```typescript
   import moment from "moment-timezone";
   moment.tz.setDefault("Asia/Riyadh");
   ```

## Build Configuration

### TypeScript Configuration

**File**: `tsconfig.json`

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

### Package Configuration

**File**: `package.json`

#### Available Scripts

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

**Script Usage**:

- `npm start`: Start development server (port 3000)
- `npm run build`: Create production build
- `npm test`: Run tests in watch mode
- `npm run eject`: Eject from Create React App (irreversible)

#### Browser Support Configuration

```json
{
  "browserslist": {
    "production": [">0.2%", "not dead", "not op_mini all"],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### ESLint Configuration

**File**: `package.json` (or `.eslintrc.json`)

```json
{
  "eslintConfig": {
    "extends": ["react-app", "react-app/jest"]
  }
}
```

## Deployment Configuration

### Static File Hosting

#### Nginx Configuration

**File**: `/etc/nginx/sites-available/units`

```nginx
server {
    listen 80;
    server_name units.example.com;

    root /var/www/units/build;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /static/ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Gzip compression
    gzip on;
    gzip_types text/css application/javascript application/json;
    gzip_min_length 1000;

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
}
```

#### Apache Configuration

**File**: `/etc/apache2/sites-available/units.conf`

```apache
<VirtualHost *:80>
    ServerName units.example.com
    DocumentRoot /var/www/units/build

    <Directory /var/www/units/build>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted

        # React Router support
        RewriteEngine On
        RewriteBase /
        RewriteRule ^index\.html$ - [L]
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteCond %{REQUEST_FILENAME} !-d
        RewriteRule . /index.html [L]
    </Directory>

    # Gzip compression
    <IfModule mod_deflate.c>
        AddOutputFilterByType DEFLATE text/html text/css application/javascript application/json
    </IfModule>

    # Cache static assets
    <FilesMatch "\.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$">
        Header set Cache-Control "max-age=31536000, public"
    </FilesMatch>
</VirtualHost>
```

### SSL/HTTPS Configuration

#### Nginx with Let's Encrypt

1. **Install Certbot**:

   ```bash
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Obtain certificate**:

   ```bash
   sudo certbot --nginx -d units.example.com
   ```

3. **Auto-renewal** is configured automatically

#### SSL Configuration

```nginx
server {
    listen 443 ssl http2;
    server_name units.example.com;

    ssl_certificate /etc/letsencrypt/live/units.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/units.example.com/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    # ... rest of configuration
}

# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name units.example.com;
    return 301 https://$server_name$request_uri;
}
```

### CDN Configuration

#### CloudFront (AWS)

1. **Create distribution**:

   - Origin: Your S3 bucket or web server
   - Default root object: `index.html`
   - Error pages: Redirect 404 to `/index.html` (200 status)

2. **Custom error responses**:

   - 404 → `/index.html` (200) for SPA routing
   - 403 → `/index.html` (200) for SPA routing

3. **Cache behaviors**:
   - Default: Cache based on query strings
   - `/static/*`: Long cache duration
   - `/index.html`: No cache

### Docker Configuration

#### Dockerfile

```dockerfile
# Build stage
FROM node:16-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

#### docker-compose.yml

```yaml
version: "3.8"

services:
  units-web:
    build: .
    ports:
      - "80:80"
    environment:
      - REACT_APP_BASE_API=https://api.units.abc.com/api/
      - REACT_APP_GOOGLE_MAPS_API_KEY=your-api-key
    restart: unless-stopped
```

## Integration Configuration

### Google Maps

1. **Get API Key**:

   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create project
   - Enable Maps JavaScript API
   - Create credentials (API key)
   - Restrict key to your domain

2. **Configure in app**:

   - Add to `.env`: `REACT_APP_GOOGLE_MAPS_API_KEY=your-key`

3. **Usage limits**:
   - Monitor usage in Google Cloud Console
   - Set quotas if needed
   - Consider billing alerts

### Salla E-commerce

1. **Register app** in Salla Developer Portal

2. **Configure OAuth**:

   - Client ID: From Salla
   - Client Secret: Store securely (backend)
   - Redirect URI: `https://units.example.com/sallaauthresponse`

3. **Integration endpoints**:
   - Authorization: `/sallagetauthorization`
   - Callback: `/sallaauthresponse`

## Performance Configuration

### Code Splitting

Already configured via React.lazy() in routes. To add more:

```typescript
const HeavyComponent = React.lazy(() => import("./HeavyComponent"));
```

### Build Optimization

#### Analyze Bundle Size

```bash
npm install --save-dev source-map-explorer
```

Add to `package.json`:

```json
{
  "scripts": {
    "analyze": "source-map-explorer 'build/static/js/*.js'"
  }
}
```

Run:

```bash
npm run build
npm run analyze
```

### Caching Strategy

#### Service Worker (Optional)

To enable offline support:

1. Edit `src/index.tsx`:

   ```typescript
   // Change from:
   serviceWorkerRegistration.unregister();

   // To:
   serviceWorkerRegistration.register();
   ```

2. This enables PWA features

## Monitoring Configuration

### Error Tracking

#### Sentry Integration

1. **Install**:

   ```bash
   npm install @sentry/react
   ```

2. **Configure** in `src/index.tsx`:

   ```typescript
   import * as Sentry from "@sentry/react";

   Sentry.init({
     dsn: "your-sentry-dsn",
     environment: "production",
     tracesSampleRate: 1.0,
   });
   ```

### Analytics

#### Google Analytics

1. **Install**:

   ```bash
   npm install react-ga4
   ```

2. **Configure** in `src/index.tsx`:

   ```typescript
   import ReactGA from "react-ga4";

   ReactGA.initialize("G-XXXXXXXXXX");
   ```

3. **Track page views** in `App.tsx`:
   ```typescript
   useEffect(() => {
     ReactGA.send({ hitType: "pageview", page: location.pathname });
   }, [location]);
   ```

## Security Configuration

### Content Security Policy

Add to `public/index.html`:

```html
<meta
  http-equiv="Content-Security-Policy"
  content="default-src 'self'; 
               script-src 'self' 'unsafe-inline'; 
               style-src 'self' 'unsafe-inline'; 
               img-src 'self' data: https:; 
               connect-src 'self' https://api.units.abc.com;"
/>
```

### CORS Configuration

CORS must be configured on the backend API to allow requests from your domain.

## Backup and Recovery

### Data Backup

- Frontend: Static files, rebuild from source
- Backend: Database backups (handled by backend team)
- Configuration: Version control `.env` template

### Disaster Recovery

1. **Source code**: Version controlled in Git
2. **Build artifacts**: Reproducible from source
3. **Configuration**: Documented and stored securely

## Maintenance Mode

To display maintenance message:

1. Create `public/maintenance.html`
2. Configure web server to serve it:

```nginx
if (-f $document_root/maintenance.html) {
    return 503;
}

error_page 503 @maintenance;
location @maintenance {
    rewrite ^(.*)$ /maintenance.html break;
}
```

## Next Steps

- Review [Architecture](./architecture.md) for system design
- See [Getting Started](./getting-started.md) for installation
- Check [Troubleshooting](./troubleshooting.md) for common issues
