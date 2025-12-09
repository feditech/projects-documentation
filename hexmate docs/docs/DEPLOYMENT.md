# Deployment Guide

This guide provides instructions for deploying HexMate to production environments.

## Table of Contents

- [Deployment Overview](#deployment-overview)
- [Pre-Deployment Checklist](#pre-deployment-checklist)
- [Build Process](#build-process)
- [Deployment Options](#deployment-options)
- [Web Server Configuration](#web-server-configuration)
- [Environment Setup](#environment-setup)
- [Post-Deployment](#post-deployment)
- [Monitoring and Maintenance](#monitoring-and-maintenance)

## Deployment Overview

HexMate is a static React application that can be deployed to any web server or hosting platform that can serve static files.

### Deployment Architecture

```
┌─────────────┐
│   Browser   │
└──────┬──────┘
       │ HTTPS
       ▼
┌─────────────────┐
│   Web Server    │
│  (Nginx/Apache) │
└──────┬──────────┘
       │
       ├─→ Static Files (HTML, JS, CSS)
       │
       └─→ API Proxy (Optional)
              │
              ▼
       ┌────────────┐
       │ Backend API│
       └────────────┘
```

## Pre-Deployment Checklist

Before deploying, ensure:

- [ ] All tests pass: `npm test`
- [ ] Build completes successfully: `npm run build`
- [ ] Environment variables are configured correctly
- [ ] API endpoint is accessible from production
- [ ] SSL certificate is ready (for HTTPS)
- [ ] Domain/subdomain DNS is configured
- [ ] Backup existing deployment (if updating)
- [ ] Database migrations completed (backend)
- [ ] Security scan completed
- [ ] Performance testing done

## Build Process

### Creating Production Build

```bash
# Set production environment
NODE_ENV=production npm run build
```

This creates an optimized production build in the `build/` directory with:
- Minified JavaScript and CSS
- Optimized images
- Source maps (optional)
- Cache-busting file names
- Compressed assets

### Build Output

```
build/
├── static/
│   ├── css/
│   │   └── main.[hash].css
│   ├── js/
│   │   ├── main.[hash].js
│   │   └── [chunk].[hash].js
│   └── media/
│       └── [files].[hash].[ext]
├── dwt-resources/
├── Images/
├── fonts/
├── index.html
├── config.json
├── favicon.ico
├── manifest.json
└── robots.txt
```

### Build Optimization

**Reduce bundle size:**
```bash
# Analyze bundle size
npm install --save-dev webpack-bundle-analyzer
npm run build -- --stats

# View analysis
npx webpack-bundle-analyzer build/bundle-stats.json
```

**Environment-specific builds:**
```bash
# Staging
REACT_APP_BASE_API=https://staging-api.example.com/api/ npm run build

# Production
REACT_APP_BASE_API=https://api.example.com/api/ npm run build
```

## Deployment Options

### Option 1: Traditional Web Server (Nginx/Apache)

#### Nginx Configuration

Create `/etc/nginx/sites-available/hexmate`:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name hexmate.example.com;

    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name hexmate.example.com;

    # SSL Configuration
    ssl_certificate /etc/ssl/certs/hexmate.crt;
    ssl_certificate_key /etc/ssl/private/hexmate.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Root directory
    root /var/www/hexmate/build;
    index index.html;

    # Gzip compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_comp_level 6;
    gzip_min_length 1000;

    # Cache static assets
    location /static/ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Don't cache index.html and config.json
    location = /index.html {
        add_header Cache-Control "no-cache, no-store, must-revalidate";
    }

    location = /config.json {
        add_header Cache-Control "no-cache, no-store, must-revalidate";
    }

    # React Router support
    location / {
        try_files $uri $uri/ /index.html;
    }

    # Optional: Proxy API requests
    location /api/ {
        proxy_pass https://api.example.com/api/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    add_header Content-Security-Policy "default-src 'self' https:; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline';" always;
}
```

**Enable site:**
```bash
sudo ln -s /etc/nginx/sites-available/hexmate /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

#### Apache Configuration

Create `/etc/apache2/sites-available/hexmate.conf`:

```apache
<VirtualHost *:80>
    ServerName hexmate.example.com
    Redirect permanent / https://hexmate.example.com/
</VirtualHost>

<VirtualHost *:443>
    ServerName hexmate.example.com
    DocumentRoot /var/www/hexmate/build

    # SSL Configuration
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/hexmate.crt
    SSLCertificateKeyFile /etc/ssl/private/hexmate.key

    <Directory /var/www/hexmate/build>
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

    # Compression
    <IfModule mod_deflate.c>
        AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css application/javascript application/json
    </IfModule>

    # Caching
    <IfModule mod_expires.c>
        ExpiresActive On
        ExpiresByType text/html "access plus 0 seconds"
        ExpiresByType application/json "access plus 0 seconds"
        ExpiresByType text/css "access plus 1 year"
        ExpiresByType application/javascript "access plus 1 year"
        ExpiresByType image/png "access plus 1 year"
        ExpiresByType image/jpg "access plus 1 year"
        ExpiresByType image/jpeg "access plus 1 year"
    </IfModule>

    # Security Headers
    Header always set X-Frame-Options "SAMEORIGIN"
    Header always set X-Content-Type-Options "nosniff"
    Header always set X-XSS-Protection "1; mode=block"
</VirtualHost>
```

**Enable site:**
```bash
sudo a2enmod rewrite ssl headers expires deflate
sudo a2ensite hexmate
sudo apache2ctl configtest
sudo systemctl reload apache2
```

### Option 2: Docker Deployment

Create `Dockerfile`:

```dockerfile
# Build stage
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY . .

# Build application
RUN npm run build

# Production stage
FROM nginx:alpine

# Copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy built app
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port
EXPOSE 80

# Health check
HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget --quiet --tries=1 --spider http://localhost/ || exit 1

CMD ["nginx", "-g", "daemon off;"]
```

Create `nginx.conf`:

```nginx
server {
    listen 80;
    server_name localhost;
    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /static/ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  hexmate:
    build: .
    ports:
      - "80:80"
    environment:
      - NODE_ENV=production
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost/"]
      interval: 30s
      timeout: 3s
      retries: 3
```

**Deploy with Docker:**
```bash
# Build image
docker build -t hexmate:latest .

# Run container
docker run -d -p 80:80 --name hexmate hexmate:latest

# Or use docker-compose
docker-compose up -d
```

### Option 3: Cloud Platforms

#### AWS S3 + CloudFront

```bash
# Install AWS CLI
pip install awscli

# Configure AWS credentials
aws configure

# Create S3 bucket
aws s3 mb s3://hexmate-app

# Enable static website hosting
aws s3 website s3://hexmate-app --index-document index.html --error-document index.html

# Upload build
aws s3 sync build/ s3://hexmate-app --delete

# Set proper MIME types
aws s3 cp s3://hexmate-app s3://hexmate-app --recursive \
  --exclude "*" --include "*.js" --content-type "application/javascript" \
  --metadata-directive REPLACE

# Create CloudFront distribution (optional, for CDN and HTTPS)
```

#### Vercel

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel --prod
```

#### Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
netlify deploy --prod --dir=build
```

Create `netlify.toml`:

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
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "/*.html"
  [headers.values]
    Cache-Control = "no-cache"
```

## Environment Setup

### Production Environment Variables

Create `.env.production`:

```env
REACT_APP_BASE_API=https://api.hexmate.example.com/api/
NODE_ENV=production
GENERATE_SOURCEMAP=false
```

### Runtime Configuration

Update `public/config.json` for production:

```json
{
  "modules": [
    {"id": 1, "name": "DMS", "link": "/dms/documents"},
    {"id": 2, "name": "CTS", "link": "/cts/dashboard"},
    {"id": 3, "name": "VMS", "link": "/vms/dashboard"}
  ],
  "signatureScale": 0.5
}
```

## Post-Deployment

### Verification Checklist

- [ ] Application loads without errors
- [ ] All modules are accessible
- [ ] API connections work correctly
- [ ] User authentication works
- [ ] File uploads function properly
- [ ] Document viewing/editing works
- [ ] Reports generate successfully
- [ ] Mobile responsiveness works
- [ ] All links navigate correctly
- [ ] SSL certificate is valid
- [ ] No console errors
- [ ] Performance is acceptable

### Testing in Production

```bash
# Check response headers
curl -I https://hexmate.example.com

# Test API connectivity
curl https://hexmate.example.com/config.json

# Load test (using Apache Bench)
ab -n 1000 -c 10 https://hexmate.example.com/
```

### Performance Optimization

**Enable Compression:**
- Gzip/Brotli compression on web server
- Compress response sizes by 70-80%

**Enable Caching:**
- Static assets: 1 year cache
- HTML files: no-cache
- API responses: appropriate cache headers

**Use CDN:**
- Serve static assets from CDN
- Reduce latency for global users
- Offload traffic from origin server

**Enable HTTP/2:**
- Multiplexing for faster loading
- Server push for critical resources
- Header compression

## Monitoring and Maintenance

### Logging

**Nginx Access Logs:**
```bash
tail -f /var/log/nginx/access.log
```

**Error Logs:**
```bash
tail -f /var/log/nginx/error.log
```

### Monitoring Tools

Consider integrating:
- **Google Analytics** - User behavior tracking
- **Sentry** - Error tracking and monitoring
- **LogRocket** - Session replay
- **New Relic** - Application performance monitoring
- **Pingdom/UptimeRobot** - Uptime monitoring

### Backup Strategy

**Regular Backups:**
1. Configuration files (`.env`, `config.json`)
2. SSL certificates
3. Web server configuration
4. Application build (optional)

**Backup Script:**
```bash
#!/bin/bash
BACKUP_DIR="/backup/hexmate"
DATE=$(date +%Y%m%d_%H%M%S)

# Create backup directory
mkdir -p $BACKUP_DIR/$DATE

# Backup configuration
cp /var/www/hexmate/build/config.json $BACKUP_DIR/$DATE/
cp /var/www/hexmate/.env $BACKUP_DIR/$DATE/
cp /etc/nginx/sites-available/hexmate $BACKUP_DIR/$DATE/

# Compress
tar -czf $BACKUP_DIR/hexmate_$DATE.tar.gz $BACKUP_DIR/$DATE/
rm -rf $BACKUP_DIR/$DATE
```

### Update Process

1. **Backup current deployment**
2. **Build new version**
3. **Test in staging environment**
4. **Schedule maintenance window** (if needed)
5. **Deploy to production**
6. **Verify deployment**
7. **Monitor for issues**
8. **Rollback if necessary**

**Zero-Downtime Deployment:**
```bash
# Build new version
npm run build

# Backup current
mv /var/www/hexmate/build /var/www/hexmate/build.backup

# Deploy new version
cp -r build /var/www/hexmate/

# If issues occur, rollback
# mv /var/www/hexmate/build.backup /var/www/hexmate/build
```

### Security Updates

- Regularly update Node.js and npm
- Update dependencies: `npm audit fix`
- Renew SSL certificates before expiry
- Review and update security headers
- Monitor security advisories

## Rollback Procedure

If deployment fails:

1. **Stop serving new version**
2. **Restore from backup**
3. **Verify rollback successful**
4. **Investigate issues**
5. **Fix and redeploy**

```bash
# Quick rollback
mv /var/www/hexmate/build /var/www/hexmate/build.failed
mv /var/www/hexmate/build.backup /var/www/hexmate/build
sudo systemctl reload nginx
```

## Troubleshooting Deployment Issues

### Issue: Blank page after deployment

**Solutions:**
- Check browser console for errors
- Verify PUBLIC_URL is set correctly
- Check file permissions
- Ensure config.json is accessible

### Issue: API requests failing

**Solutions:**
- Verify REACT_APP_BASE_API is correct
- Check CORS configuration on backend
- Ensure SSL certificates are valid
- Check firewall rules

### Issue: Routes not working (404 errors)

**Solutions:**
- Configure web server for SPA routing
- Add rewrite rules (see Nginx/Apache config above)
- Verify .htaccess or nginx config

## See Also

- [Configuration Guide](CONFIGURATION.md)
- [Security Guide](SECURITY.md)
- [Troubleshooting Guide](TROUBLESHOOTING.md)
- [Architecture Documentation](ARCHITECTURE.md)
