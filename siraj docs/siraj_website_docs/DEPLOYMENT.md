# Deployment Guide

Complete guide for deploying the Siraj Career Guidance Platform.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Environment Setup](#environment-setup)
3. [Local Deployment](#local-deployment)
4. [Docker Deployment](#docker-deployment)
5. [Kubernetes Deployment](#kubernetes-deployment)
6. [Production Deployment](#production-deployment)
7. [CI/CD Pipeline](#cicd-pipeline)
8. [Monitoring & Maintenance](#monitoring--maintenance)
9. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Required Tools

- **Node.js** 18.x or higher
- **npm** 9.x or higher
- **Docker** 20.x or higher (for containerized deployment)
- **kubectl** (for Kubernetes deployment)
- **Helm** 3.x or higher (for Kubernetes package management)
- **Git** for version control

### Access Requirements

- Access to the repository
- Backend API URL and credentials
- Docker registry access (if using private registry)
- Kubernetes cluster access (for production deployment)
- Domain name and SSL certificates (for production)

---

## Environment Setup

### Environment Variables

Create appropriate environment files for each environment:

#### Development (`.env.local`)
```env
BACKEND_ENV=dev
BACKEND_BASE_URL=http://localhost:3001/api
META_CONTENT=
NODE_ENV=development
```

#### Staging (`.env.staging`)
```env
BACKEND_ENV=staging
BACKEND_BASE_URL=https://staging-api.siraj.app/api
META_CONTENT=Siraj - Career Guidance Platform (Staging)
NODE_ENV=production
```

#### Production (`.env.production`)
```env
BACKEND_ENV=production
BACKEND_BASE_URL=https://api.siraj.app/api
META_CONTENT=Siraj - Your Personalized Academic Guidance
NODE_ENV=production
```

### Required Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `BACKEND_ENV` | Deployment environment | `dev`, `staging`, `production` |
| `BACKEND_BASE_URL` | Backend API base URL | `https://api.siraj.app/api` |
| `META_CONTENT` | Meta description for SEO | `Career guidance platform` |
| `NODE_ENV` | Node environment | `development`, `production` |

---

## Local Deployment

### Step 1: Install Dependencies

```bash
cd /path/to/siraj-fronted
npm install
```

### Step 2: Configure Environment

```bash
# Copy template
cp .env .env.local

# Edit with your values
nano .env.local
```

### Step 3: Run Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:3000`

### Step 4: Build for Production (Test)

```bash
npm run build
npm start
```

This tests the production build locally.

---

## Docker Deployment

### Building the Docker Image

#### Step 1: Build Image

```bash
docker build -t siraj-frontend:latest .
```

**With specific tag:**
```bash
docker build -t siraj-frontend:v1.0.0 .
```

#### Step 2: Verify Image

```bash
docker images | grep siraj-frontend
```

### Running the Container

#### Basic Run

```bash
docker run -p 3000:3000 \
  -e BACKEND_BASE_URL=http://backend:3001/api \
  siraj-frontend:latest
```

#### With Environment File

```bash
docker run -p 3000:3000 \
  --env-file .env.production \
  siraj-frontend:latest
```

#### With Volume Mounts (Development)

```bash
docker run -p 3000:3000 \
  -v $(pwd)/src:/app/src \
  --env-file .env.local \
  siraj-frontend:latest
```

### Docker Compose

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - BACKEND_BASE_URL=http://backend:3001/api
      - BACKEND_ENV=production
    depends_on:
      - backend
    restart: unless-stopped

  backend:
    image: siraj-backend:latest
    ports:
      - "3001:3001"
    environment:
      - DATABASE_URL=postgresql://...
    restart: unless-stopped
```

**Run with Docker Compose:**
```bash
docker-compose up -d
```

### Pushing to Registry

#### Docker Hub

```bash
# Tag image
docker tag siraj-frontend:latest username/siraj-frontend:latest

# Login
docker login

# Push
docker push username/siraj-frontend:latest
```

#### Private Registry

```bash
# Tag for private registry
docker tag siraj-frontend:latest registry.example.com/siraj-frontend:latest

# Login to private registry
docker login registry.example.com

# Push
docker push registry.example.com/siraj-frontend:latest
```

---

## Kubernetes Deployment

### Prerequisites

- Kubernetes cluster (v1.20+)
- kubectl configured
- Helm 3.x installed
- Docker image pushed to registry

### Using Helm Chart

The project includes a Helm chart for Kubernetes deployment.

#### Step 1: Review Chart Configuration

**Chart.yaml**
```yaml
apiVersion: v2
name: siraj-fe
version: 0.1.0
description: Helm chart for siraj-fe (Next.js frontend)
type: application
```

#### Step 2: Configure Values

**values.yaml**
```yaml
replicaCount: 3

image:
  repository: your-registry/siraj-frontend
  tag: "latest"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80
  targetPort: 3000

ingress:
  enabled: true
  className: nginx
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
  hosts:
    - host: siraj.app
      paths:
        - path: /
          pathType: Prefix
  tls:
    - secretName: siraj-tls
      hosts:
        - siraj.app

env:
  - name: BACKEND_BASE_URL
    value: "http://siraj-be:3001/api"
  - name: BACKEND_ENV
    value: "production"
  - name: NODE_ENV
    value: "production"

resources:
  limits:
    cpu: 1000m
    memory: 1Gi
  requests:
    cpu: 500m
    memory: 512Mi

autoscaling:
  enabled: true
  minReplicas: 2
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
  targetMemoryUtilizationPercentage: 80

livenessProbe:
  httpGet:
    path: /
    port: 3000
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: 3000
  initialDelaySeconds: 20
  periodSeconds: 10
```

#### Step 3: Install with Helm

```bash
# Dry run to check configuration
helm install siraj-frontend . --dry-run --debug

# Install to default namespace
helm install siraj-frontend .

# Install to specific namespace
helm install siraj-frontend . --namespace production --create-namespace

# Install with custom values
helm install siraj-frontend . -f values.production.yaml
```

#### Step 4: Verify Deployment

```bash
# Check pods
kubectl get pods -l app=siraj-frontend

# Check service
kubectl get svc siraj-frontend

# Check ingress
kubectl get ingress

# View logs
kubectl logs -l app=siraj-frontend --tail=50
```

### Updating Deployment

```bash
# Update with Helm
helm upgrade siraj-frontend . -f values.yaml

# Rollback if needed
helm rollback siraj-frontend

# View history
helm history siraj-frontend
```

### Manual Kubernetes Deployment (Without Helm)

#### Deployment

**deployment.yaml**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: siraj-frontend
  labels:
    app: siraj-frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: siraj-frontend
  template:
    metadata:
      labels:
        app: siraj-frontend
    spec:
      containers:
      - name: frontend
        image: your-registry/siraj-frontend:latest
        ports:
        - containerPort: 3000
        env:
        - name: BACKEND_BASE_URL
          value: "http://siraj-be:3001/api"
        - name: BACKEND_ENV
          value: "production"
        resources:
          limits:
            cpu: "1"
            memory: "1Gi"
          requests:
            cpu: "500m"
            memory: "512Mi"
        livenessProbe:
          httpGet:
            path: /
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /
            port: 3000
          initialDelaySeconds: 20
          periodSeconds: 10
```

```bash
kubectl apply -f deployment.yaml
```

#### Service

**service.yaml**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: siraj-frontend
spec:
  selector:
    app: siraj-frontend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: ClusterIP
```

```bash
kubectl apply -f service.yaml
```

#### Ingress

**ingress.yaml**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: siraj-frontend
  annotations:
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - siraj.app
    secretName: siraj-tls
  rules:
  - host: siraj.app
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: siraj-frontend
            port:
              number: 80
```

```bash
kubectl apply -f ingress.yaml
```

---

## Production Deployment

### Pre-Deployment Checklist

- [ ] Environment variables configured correctly
- [ ] Docker image built and pushed to registry
- [ ] Database migrations completed (backend)
- [ ] SSL certificates configured
- [ ] DNS records updated
- [ ] Backup procedures in place
- [ ] Monitoring tools configured
- [ ] Load testing completed
- [ ] Security audit performed
- [ ] Rollback plan prepared

### Deployment Steps

#### 1. Build Production Image

```bash
# Build with production configuration
npm run prod-build

# Build Docker image
docker build -t siraj-frontend:v1.0.0 .

# Tag with latest
docker tag siraj-frontend:v1.0.0 siraj-frontend:latest

# Push to registry
docker push siraj-frontend:v1.0.0
docker push siraj-frontend:latest
```

#### 2. Deploy to Kubernetes

```bash
# Update Helm chart with new image tag
helm upgrade siraj-frontend . \
  --set image.tag=v1.0.0 \
  --namespace production \
  -f values.production.yaml
```

#### 3. Verify Deployment

```bash
# Check rollout status
kubectl rollout status deployment/siraj-frontend -n production

# Check pods are running
kubectl get pods -n production -l app=siraj-frontend

# Check logs for errors
kubectl logs -n production -l app=siraj-frontend --tail=100

# Test application
curl https://siraj.app
```

#### 4. Monitor

- Check application logs
- Monitor resource usage
- Verify user traffic
- Check error rates
- Monitor API response times

### Blue-Green Deployment

```bash
# Deploy green environment
helm install siraj-frontend-green . \
  --set image.tag=v1.1.0 \
  --namespace production-green

# Test green environment
# Run smoke tests and validation

# Switch traffic to green
kubectl patch service siraj-frontend \
  -n production \
  -p '{"spec":{"selector":{"version":"green"}}}'

# Remove blue environment (after validation)
helm uninstall siraj-frontend-blue -n production-blue
```

### Canary Deployment

```yaml
# Canary deployment - 10% traffic
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: siraj-frontend
spec:
  hosts:
  - siraj.app
  http:
  - match:
    - headers:
        canary:
          exact: "true"
    route:
    - destination:
        host: siraj-frontend-canary
      weight: 10
    - destination:
        host: siraj-frontend-stable
      weight: 90
```

---

## CI/CD Pipeline

### GitHub Actions Example

**.github/workflows/deploy.yml**
```yaml
name: Deploy to Production

on:
  push:
    branches:
      - main
    tags:
      - 'v*'

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run tests
      run: npm test
    
    - name: Build application
      run: npm run build
      env:
        BACKEND_BASE_URL: ${{ secrets.BACKEND_BASE_URL }}
        BACKEND_ENV: production
    
    - name: Build Docker image
      run: |
        docker build -t ${{ secrets.REGISTRY }}/siraj-frontend:${{ github.sha }} .
        docker tag ${{ secrets.REGISTRY }}/siraj-frontend:${{ github.sha }} \
                   ${{ secrets.REGISTRY }}/siraj-frontend:latest
    
    - name: Login to registry
      uses: docker/login-action@v2
      with:
        registry: ${{ secrets.REGISTRY }}
        username: ${{ secrets.REGISTRY_USERNAME }}
        password: ${{ secrets.REGISTRY_PASSWORD }}
    
    - name: Push Docker image
      run: |
        docker push ${{ secrets.REGISTRY }}/siraj-frontend:${{ github.sha }}
        docker push ${{ secrets.REGISTRY }}/siraj-frontend:latest
    
    - name: Deploy to Kubernetes
      uses: azure/k8s-deploy@v1
      with:
        manifests: |
          k8s/deployment.yaml
          k8s/service.yaml
          k8s/ingress.yaml
        images: |
          ${{ secrets.REGISTRY }}/siraj-frontend:${{ github.sha }}
        kubectl-version: 'latest'
```

---

## Monitoring & Maintenance

### Health Checks

```bash
# Application health
curl https://siraj.app

# Check pod health
kubectl get pods -n production

# Check logs
kubectl logs -n production -l app=siraj-frontend --tail=100 -f
```

### Scaling

```bash
# Manual scaling
kubectl scale deployment siraj-frontend --replicas=5 -n production

# Check autoscaling status
kubectl get hpa -n production
```

### Updates

```bash
# Rolling update
kubectl set image deployment/siraj-frontend \
  frontend=siraj-frontend:v1.1.0 -n production

# Check rollout status
kubectl rollout status deployment/siraj-frontend -n production

# Rollback if needed
kubectl rollout undo deployment/siraj-frontend -n production
```

### Backup

```bash
# Backup Helm release
helm get values siraj-frontend -n production > backup-values.yaml

# Backup Kubernetes resources
kubectl get all -n production -o yaml > backup-resources.yaml
```

---

## Troubleshooting

### Common Issues

#### Pods Not Starting

```bash
# Check pod status
kubectl describe pod <pod-name> -n production

# Check logs
kubectl logs <pod-name> -n production

# Common causes:
# - Image pull errors (check registry credentials)
# - Resource limits (increase CPU/memory)
# - Configuration errors (check env variables)
```

#### Application Not Accessible

```bash
# Check service
kubectl get svc siraj-frontend -n production

# Check ingress
kubectl describe ingress siraj-frontend -n production

# Check DNS
nslookup siraj.app

# Check SSL certificate
curl -vI https://siraj.app
```

#### High Memory Usage

```bash
# Check resource usage
kubectl top pods -n production

# Increase memory limits
kubectl set resources deployment/siraj-frontend \
  --limits=memory=2Gi -n production
```

#### Slow Response Times

```bash
# Check pod metrics
kubectl top pods -n production

# Check logs for errors
kubectl logs -n production -l app=siraj-frontend --tail=500

# Scale up if needed
kubectl scale deployment/siraj-frontend --replicas=5 -n production
```

### Logging

```bash
# View recent logs
kubectl logs -l app=siraj-frontend -n production --tail=100

# Follow logs
kubectl logs -l app=siraj-frontend -n production -f

# Logs from specific pod
kubectl logs <pod-name> -n production

# Logs from previous crashed container
kubectl logs <pod-name> -n production --previous
```

### Debugging

```bash
# Execute command in pod
kubectl exec -it <pod-name> -n production -- /bin/sh

# Port forward for local testing
kubectl port-forward deployment/siraj-frontend 3000:3000 -n production

# Check environment variables
kubectl exec <pod-name> -n production -- env
```

---

## Security Considerations

### SSL/TLS

- Use cert-manager for automatic certificate management
- Enforce HTTPS redirects
- Use strong cipher suites
- Keep certificates up to date

### Secrets Management

```bash
# Create secret
kubectl create secret generic siraj-secrets \
  --from-literal=api-key=your-secret-key \
  -n production

# Use in deployment
env:
- name: API_KEY
  valueFrom:
    secretKeyRef:
      name: siraj-secrets
      key: api-key
```

### Network Policies

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: siraj-frontend-policy
spec:
  podSelector:
    matchLabels:
      app: siraj-frontend
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    ports:
    - protocol: TCP
      port: 3000
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: siraj-backend
    ports:
    - protocol: TCP
      port: 3001
```

---

## Performance Optimization

### CDN Configuration

- Use CDN for static assets
- Configure cache headers
- Enable compression (gzip/brotli)

### Resource Limits

```yaml
resources:
  limits:
    cpu: "1"
    memory: "1Gi"
  requests:
    cpu: "500m"
    memory: "512Mi"
```

### Caching

- Enable Next.js caching
- Configure reverse proxy caching
- Use Redis for session storage

---

## Disaster Recovery

### Backup Strategy

1. **Regular backups** of Helm values and Kubernetes resources
2. **Database backups** (backend responsibility)
3. **Image registry backups**
4. **Configuration backups**

### Recovery Procedures

```bash
# Restore from backup
helm install siraj-frontend . -f backup-values.yaml -n production

# Rollback to previous version
helm rollback siraj-frontend -n production

# Restore specific resource
kubectl apply -f backup-resources.yaml
```

---

**Need Help?**

- 📧 **DevOps Team:** devops@siraj.app
- 📖 **Documentation:** /docs
- 🐛 **Issues:** GitHub Issues

---

*Last updated: January 2025*
