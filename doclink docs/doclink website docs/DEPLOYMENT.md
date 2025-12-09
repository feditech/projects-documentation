# Deployment Guide

This guide covers deploying the DocLink web application to various hosting platforms.

## Overview

DocLink is a Next.js application that can be deployed in multiple ways:
- **Static Export**: Pre-rendered HTML files
- **Server-Side Rendering (SSR)**: Node.js server
- **Serverless**: Edge functions (Vercel, AWS Lambda)
- **Container**: Docker deployment

## Prerequisites

Before deploying, ensure you have:
- ✅ Completed development and testing
- ✅ All environment variables configured
- ✅ Production API endpoints ready
- ✅ Build process runs without errors
- ✅ All tests passing

## Build for Production

### 1. Install Dependencies

```bash
npm install --production
```

### 2. Run Production Build

```bash
npm run build
```

This creates an optimized production build in the `.next` directory.

### 3. Test Production Build Locally

```bash
npm run start
```

Visit `http://localhost:3000` to verify the production build works correctly.

---

## Deployment Options

### Option 1: Vercel (Recommended)

Vercel is the creator of Next.js and provides the best Next.js deployment experience.

#### Quick Deploy

1. **Install Vercel CLI**
```bash
npm install -g vercel
```

2. **Deploy**
```bash
vercel
```

3. **Follow Prompts**
- Link to Git repository (recommended)
- Configure project settings
- Set environment variables

#### Deploy from Git

1. **Push to GitHub**
```bash
git push origin main
```

2. **Import to Vercel**
- Visit [vercel.com](https://vercel.com)
- Click "Import Project"
- Select your repository
- Configure settings
- Deploy

#### Environment Variables

In Vercel dashboard, add:
```
NEXT_PUBLIC_API_BASE_URL=your_production_api_url
```

#### Custom Domain

1. Go to Project Settings → Domains
2. Add your domain
3. Configure DNS records as shown

---

### Option 2: Static Export

Export as static HTML for hosting on any static host (Netlify, GitHub Pages, etc.).

#### Build Static Export

```bash
npm run build
npm run export
```

This creates an `out/` directory with static HTML files.

#### Deploy to Netlify

1. **Via Netlify CLI**
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=out
```

2. **Via Git Integration**
- Connect repository to Netlify
- Set build command: `npm run build && npm run export`
- Set publish directory: `out`

#### Deploy to GitHub Pages

```bash
# Install gh-pages
npm install -g gh-pages

# Deploy
gh-pages -d out
```

#### Limitations of Static Export
- No API routes
- No server-side rendering
- No dynamic routing with fallback
- No image optimization

---

### Option 3: Node.js Server

Deploy to traditional Node.js hosting.

#### Server Setup

1. **Build Application**
```bash
npm run build
```

2. **Start Server**
```bash
npm run start
```

3. **Use Process Manager (PM2)**
```bash
npm install -g pm2

# Start application
pm2 start npm --name "doclink" -- start

# Configure auto-restart
pm2 startup
pm2 save
```

#### Nginx Configuration

```nginx
server {
    listen 80;
    server_name doclink.com www.doclink.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

### Option 4: Docker Deployment

Containerize the application for deployment anywhere.

#### Create Dockerfile

```dockerfile
# Base image
FROM node:18-alpine AS base

# Install dependencies only when needed
FROM base AS deps
RUN apk add --no-cache libc6-compat
WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm ci

# Rebuild the source code only when needed
FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .

RUN npm run build

# Production image
FROM base AS runner
WORKDIR /app

ENV NODE_ENV production

RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs

COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static

USER nextjs

EXPOSE 3000

ENV PORT 3000

CMD ["node", "server.js"]
```

#### Create .dockerignore

```
node_modules
.next
.git
*.md
.env.local
```

#### Build Docker Image

```bash
docker build -t doclink-web .
```

#### Run Docker Container

```bash
docker run -p 3000:3000 -e NEXT_PUBLIC_API_BASE_URL=your_api_url doclink-web
```

#### Docker Compose

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_BASE_URL=${API_BASE_URL}
    restart: unless-stopped
```

---

### Option 5: AWS Deployment

#### AWS Amplify

1. **Connect Repository**
- Open AWS Amplify Console
- Connect Git repository
- Configure build settings

2. **Build Settings**
```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - npm install
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: .next
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

#### AWS Elastic Beanstalk

1. **Install EB CLI**
```bash
pip install awsebcli
```

2. **Initialize**
```bash
eb init -p node.js doclink-web
```

3. **Create Environment**
```bash
eb create doclink-production
```

4. **Deploy**
```bash
eb deploy
```

---

## Environment Variables

### Required Variables

```bash
# API Configuration
NEXT_PUBLIC_API_BASE_URL=https://api.doclink.com

# Optional: Analytics
NEXT_PUBLIC_GA_ID=your_google_analytics_id

# Optional: Error Tracking
SENTRY_DSN=your_sentry_dsn
```

### Setting Environment Variables

#### Vercel
```bash
vercel env add NEXT_PUBLIC_API_BASE_URL production
```

#### Netlify
```bash
netlify env:set NEXT_PUBLIC_API_BASE_URL "your_value"
```

#### Docker
```bash
docker run -e NEXT_PUBLIC_API_BASE_URL=value doclink-web
```

---

## SSL/HTTPS Configuration

### Vercel & Netlify
- Automatic HTTPS enabled
- Free SSL certificates

### Custom Server (Let's Encrypt)

```bash
# Install Certbot
sudo apt-get install certbot python3-certbot-nginx

# Obtain certificate
sudo certbot --nginx -d doclink.com -d www.doclink.com

# Auto-renewal is configured automatically
```

---

## Performance Optimization

### 1. Enable Compression

Nginx:
```nginx
gzip on;
gzip_types text/plain text/css application/json application/javascript;
```

### 2. Caching Strategy

```nginx
location /_next/static/ {
    expires 365d;
    add_header Cache-Control "public, immutable";
}
```

### 3. CDN Configuration

Use CDN for static assets:
- Cloudflare
- AWS CloudFront
- Fastly

---

## Monitoring & Analytics

### 1. Application Monitoring

**Recommended Tools:**
- Vercel Analytics (built-in for Vercel)
- Google Analytics
- New Relic
- Datadog

### 2. Error Tracking

**Recommended Tools:**
- Sentry
- Bugsnag
- Rollbar

**Sentry Integration:**
```bash
npm install @sentry/nextjs
```

```javascript
// next.config.js
const { withSentryConfig } = require('@sentry/nextjs');

module.exports = withSentryConfig({
  // Your Next.js config
});
```

### 3. Performance Monitoring

**Web Vitals:**
```javascript
// pages/_app.js
export function reportWebVitals(metric) {
  console.log(metric);
  // Send to analytics
}
```

---

## Database Considerations

If using a database:

### Environment Variables
```bash
DATABASE_URL=postgresql://user:password@host:5432/dbname
```

### Migration Strategy
1. Run migrations before deployment
2. Use blue-green deployment for zero downtime
3. Always backup before migrating

---

## Rollback Strategy

### Vercel
- Instant rollback from dashboard
- Keep previous deployments for quick rollback

### Docker
```bash
# Tag images
docker tag doclink-web:latest doclink-web:v1.0.0

# Rollback
docker run doclink-web:v1.0.0
```

### PM2
```bash
# List previous versions
pm2 list

# Revert to previous
pm2 reload doclink --update-env
```

---

## CI/CD Pipeline

### GitHub Actions Example

```yaml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run tests
        run: npm test
      
      - name: Build
        run: npm run build
      
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
```

---

## Post-Deployment Checklist

- [ ] Application loads correctly
- [ ] All pages accessible
- [ ] API endpoints responding
- [ ] Images loading properly
- [ ] Forms submitting successfully
- [ ] SSL certificate active
- [ ] Analytics tracking working
- [ ] Error tracking configured
- [ ] Performance metrics acceptable
- [ ] Mobile responsive working
- [ ] SEO meta tags present
- [ ] Sitemap accessible

---

## Scaling Considerations

### Horizontal Scaling
- Load balancer (Nginx, AWS ALB)
- Multiple server instances
- Session management (Redis)

### Database Scaling
- Read replicas
- Connection pooling
- Caching layer (Redis, Memcached)

### CDN & Caching
- Static assets on CDN
- API response caching
- Browser caching headers

---

## Security Best Practices

1. **Environment Variables**: Never commit secrets
2. **HTTPS Only**: Force HTTPS redirect
3. **Security Headers**: Configure CSP, HSTS
4. **Rate Limiting**: Prevent abuse
5. **Input Validation**: Sanitize all inputs
6. **Dependencies**: Regular security updates

---

## Backup Strategy

1. **Code**: Git repository backups
2. **Database**: Daily automated backups
3. **Assets**: CDN/S3 backups
4. **Configuration**: Document all configs

---

## Related Documentation

- [Getting Started](./GETTING_STARTED.md)
- [Architecture](./ARCHITECTURE.md)
- [Development Guide](./DEVELOPMENT.md)
- [Contributing](./CONTRIBUTING.md)
