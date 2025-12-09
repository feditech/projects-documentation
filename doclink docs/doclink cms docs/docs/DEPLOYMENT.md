# Deployment Guide

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Environment Configuration](#environment-configuration)
- [Build Process](#build-process)
- [Deployment Options](#deployment-options)
- [Production Checklist](#production-checklist)
- [Monitoring & Maintenance](#monitoring--maintenance)
- [Rollback Strategy](#rollback-strategy)

## Overview

This guide covers the deployment process for DocLink CMS, including environment setup, build configuration, and deployment to various hosting platforms.

## Prerequisites

### System Requirements

- Node.js v14+ (LTS recommended)
- npm v6+ or yarn v1.22+
- Git
- Web server (Nginx, Apache, or similar)
- SSL certificate for HTTPS

### Access Requirements

- Repository access (GitHub)
- Hosting platform access
- Domain name and DNS configuration
- SSL certificate management
- Backend API access

## Environment Configuration

### Environment Variables

Create appropriate `.env` files for each environment:

#### Development (.env.development)
```env
REACT_APP_API_BASE_URL=http://localhost:5000/api/v1
REACT_APP_GOOGLE_MAPS_API_KEY=your_dev_maps_key
REACT_APP_ENV=development
REACT_APP_ENABLE_LOGGER=true
REACT_APP_ENABLE_REDUX_DEVTOOLS=true
```

#### Staging (.env.staging)
```env
REACT_APP_API_BASE_URL=https://staging-api.doclink.com/api/v1
REACT_APP_GOOGLE_MAPS_API_KEY=your_staging_maps_key
REACT_APP_ENV=staging
REACT_APP_ENABLE_LOGGER=true
REACT_APP_ENABLE_REDUX_DEVTOOLS=true
```

#### Production (.env.production)
```env
REACT_APP_API_BASE_URL=https://api.doclink.com/api/v1
REACT_APP_GOOGLE_MAPS_API_KEY=your_production_maps_key
REACT_APP_ENV=production
REACT_APP_ENABLE_LOGGER=false
REACT_APP_ENABLE_REDUX_DEVTOOLS=false
```

### Security Considerations

⚠️ **Important**: Never commit `.env` files to version control!

- Use environment-specific configuration
- Store sensitive data in secure environment variables
- Rotate API keys regularly
- Use HTTPS in production
- Enable CORS properly on backend

## Build Process

### Production Build

```bash
# Clean previous builds
rm -rf build/

# Install dependencies
npm ci --production=false

# Build for production
npm run build
```

This creates an optimized production build in the `build/` directory.

### Build Output

```
build/
├── static/
│   ├── css/           # Minified CSS files
│   ├── js/            # Minified JavaScript bundles
│   └── media/         # Images and other assets
├── index.html         # Entry HTML file
├── favicon.ico
├── manifest.json
└── asset-manifest.json
```

### Build Optimization

The production build includes:

- Minified and optimized code
- Dead code elimination (tree shaking)
- Code splitting for better performance
- Hashed filenames for cache busting
- Optimized images and assets
- Source maps (optional, for debugging)

### Build Configuration

Modify `webpack.config.js` for custom build settings:

```javascript
module.exports = {
  mode: 'production',
  optimization: {
    minimize: true,
    splitChunks: {
      chunks: 'all',
    },
  },
  // ... other configurations
};
```

## Deployment Options

### Option 1: Vercel (Recommended for Quick Deployment)

#### Initial Setup

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

3. Deploy:
```bash
vercel
```

#### Production Deployment

```bash
vercel --prod
```

#### Configuration (vercel.json)

```json
{
  "version": 2,
  "builds": [
    {
      "src": "package.json",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "build"
      }
    }
  ],
  "routes": [
    {
      "src": "/static/(.*)",
      "headers": {
        "cache-control": "public, max-age=31536000, immutable"
      }
    },
    {
      "src": "/(.*)",
      "dest": "/index.html"
    }
  ]
}
```

### Option 2: Netlify

#### Deployment via Git

1. Connect repository to Netlify
2. Configure build settings:
   - Build command: `npm run build`
   - Publish directory: `build`
3. Add environment variables in Netlify dashboard
4. Deploy

#### Netlify Configuration (netlify.toml)

```toml
[build]
  command = "npm run build"
  publish = "build"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/static/*"
  [headers.values]
    cache-control = "public, max-age=31536000, immutable"
```

### Option 3: AWS S3 + CloudFront

#### S3 Setup

1. Create S3 bucket:
```bash
aws s3 mb s3://doclink-cms
```

2. Configure bucket for static hosting:
```bash
aws s3 website s3://doclink-cms --index-document index.html --error-document index.html
```

3. Upload build files:
```bash
aws s3 sync build/ s3://doclink-cms --delete
```

#### CloudFront Setup

1. Create CloudFront distribution
2. Point to S3 bucket as origin
3. Configure SSL certificate
4. Set custom error pages (route all to index.html)

### Option 4: Traditional Web Server (Nginx)

#### Nginx Configuration

```nginx
server {
    listen 80;
    server_name doclink-cms.com;
    
    # Redirect HTTP to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name doclink-cms.com;

    # SSL Configuration
    ssl_certificate /path/to/ssl/certificate.crt;
    ssl_certificate_key /path/to/ssl/private.key;
    
    # Root directory
    root /var/www/doclink-cms/build;
    index index.html;

    # Gzip compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;

    # Cache static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # React Router support
    location / {
        try_files $uri $uri/ /index.html;
    }

    # API proxy (if needed)
    location /api {
        proxy_pass https://api.doclink.com;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

#### Deployment Script

```bash
#!/bin/bash

# Build the application
npm run build

# Backup current deployment
sudo cp -r /var/www/doclink-cms/build /var/www/doclink-cms/build.backup.$(date +%Y%m%d_%H%M%S)

# Deploy new build
sudo rm -rf /var/www/doclink-cms/build
sudo cp -r build /var/www/doclink-cms/

# Set permissions
sudo chown -R www-data:www-data /var/www/doclink-cms/build

# Reload Nginx
sudo nginx -t && sudo systemctl reload nginx

echo "Deployment completed successfully!"
```

### Option 5: Docker

#### Dockerfile

```dockerfile
# Build stage
FROM node:14-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

#### Docker Compose

```yaml
version: '3.8'

services:
  doclink-cms:
    build: .
    ports:
      - "80:80"
    environment:
      - REACT_APP_API_BASE_URL=https://api.doclink.com/api/v1
    restart: unless-stopped
```

#### Build and Run

```bash
# Build Docker image
docker build -t doclink-cms .

# Run container
docker run -d -p 80:80 --name doclink-cms doclink-cms

# Or with docker-compose
docker-compose up -d
```

## Production Checklist

### Pre-Deployment

- [ ] All tests are passing
- [ ] Code is reviewed and approved
- [ ] Environment variables are configured
- [ ] API endpoints are accessible
- [ ] SSL certificates are valid
- [ ] Backup current production version

### Build Verification

- [ ] Production build completes without errors
- [ ] No console errors in production build
- [ ] All assets are properly loaded
- [ ] Application routes work correctly
- [ ] API integration is working
- [ ] Authentication flow is functional

### Post-Deployment

- [ ] Verify application is accessible
- [ ] Test critical user flows
- [ ] Monitor error logs
- [ ] Check performance metrics
- [ ] Verify SSL/HTTPS is working
- [ ] Test on multiple browsers and devices
- [ ] Monitor API response times

### Security Checklist

- [ ] HTTPS is enforced
- [ ] Security headers are configured
- [ ] No sensitive data in client-side code
- [ ] API keys are environment-specific
- [ ] Authentication is secure
- [ ] CORS is properly configured
- [ ] Rate limiting is in place (backend)

## Monitoring & Maintenance

### Performance Monitoring

1. **Google Analytics**: Track user behavior
2. **Application Monitoring**: Use tools like:
   - Sentry for error tracking
   - LogRocket for session replay
   - New Relic for performance monitoring

### Health Checks

Implement health check endpoint:

```javascript
// Health check route
app.get('/health', (req, res) => {
  res.status(200).json({ status: 'healthy' });
});
```

### Logging

```javascript
// Production logging
if (process.env.REACT_APP_ENV === 'production') {
  // Send errors to monitoring service
  window.addEventListener('error', (event) => {
    // Log to Sentry or similar
  });
}
```

### Maintenance Mode

Create maintenance page:

```html
<!-- maintenance.html -->
<!DOCTYPE html>
<html>
<head>
  <title>DocLink CMS - Maintenance</title>
</head>
<body>
  <h1>We'll be right back!</h1>
  <p>We're performing scheduled maintenance.</p>
</body>
</html>
```

Nginx configuration for maintenance:

```nginx
location / {
    if (-f $document_root/maintenance.html) {
        return 503;
    }
    try_files $uri $uri/ /index.html;
}

error_page 503 @maintenance;
location @maintenance {
    rewrite ^(.*)$ /maintenance.html break;
}
```

## Rollback Strategy

### Quick Rollback (Nginx/Server)

```bash
#!/bin/bash
# Rollback to previous version

BACKUP_DIR="/var/www/doclink-cms/build.backup"
CURRENT_DIR="/var/www/doclink-cms/build"

# Find latest backup
LATEST_BACKUP=$(ls -t $BACKUP_DIR.* | head -1)

if [ -z "$LATEST_BACKUP" ]; then
  echo "No backup found!"
  exit 1
fi

# Restore backup
sudo rm -rf $CURRENT_DIR
sudo cp -r $LATEST_BACKUP $CURRENT_DIR

# Reload server
sudo systemctl reload nginx

echo "Rolled back to: $LATEST_BACKUP"
```

### Git-based Rollback

```bash
# Revert to previous commit
git revert HEAD
git push origin main

# Or reset to specific commit
git reset --hard <commit-hash>
git push origin main --force

# Rebuild and deploy
npm run build
# ... deploy process
```

### Vercel/Netlify Rollback

Both platforms provide instant rollback through their dashboards:
1. Go to deployments
2. Select previous successful deployment
3. Click "Promote to Production"

## CI/CD Pipeline

### GitHub Actions Example

```yaml
name: Deploy to Production

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test -- --passWithNoTests

      - name: Build
        run: npm run build
        env:
          REACT_APP_API_BASE_URL: ${{ secrets.API_BASE_URL }}
          REACT_APP_GOOGLE_MAPS_API_KEY: ${{ secrets.GOOGLE_MAPS_KEY }}

      - name: Deploy to production
        run: |
          # Add your deployment script here
          # e.g., sync to S3, deploy to server, etc.
```

## Troubleshooting Deployment Issues

### Build Failures

```bash
# Clear cache and rebuild
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Module Not Found Errors

- Check import paths are correct
- Ensure all dependencies are in package.json
- Clear node_modules and reinstall

### Environment Variable Issues

- Verify variables are set correctly
- Prefix React environment variables with `REACT_APP_`
- Restart development server after changes

### White Screen After Deployment

- Check browser console for errors
- Verify API endpoints are accessible
- Check CORS configuration on backend
- Verify all assets are loading correctly

---

For additional support, contact the DevOps team or refer to [TROUBLESHOOTING.md](./TROUBLESHOOTING.md).
