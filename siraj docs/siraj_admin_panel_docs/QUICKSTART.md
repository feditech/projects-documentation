# Quick Start Guide

This is a quick reference guide to get you up and running with the Siraj Admin Panel.

## 🚀 5-Minute Setup

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Environment

Create `.env` file:

```bash
REACT_APP_API_URL=http://localhost:8000/api/
```

### 3. Start Development Server

```bash
npm start
```

Visit: http://localhost:3000

## 📋 Common Tasks

### Building for Production

```bash
npm run build
```

Output: `build/` directory

### Running Tests

```bash
npm test
```

### Running with Docker

```bash
docker build -t siraj-admin:latest .
docker run -p 80:80 siraj-admin:latest
```

Visit: http://localhost

## 🔑 Key Features

| Feature | Location | Description |
|---------|----------|-------------|
| **Student Management** | Dashboard → Students | Manage student accounts |
| **Advisor Management** | Dashboard → Advisors | Manage advisor profiles |
| **Product Management** | Dashboard → Products | Configure subscription products |
| **University Management** | Dashboard → Universities | Manage university database |
| **Session Management** | Dashboard → Booked Sessions | View and manage advisory sessions |
| **Coupon Management** | Dashboard → Coupons | Create promotional coupons |

## 🔧 Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `REACT_APP_API_URL` | Backend API endpoint | `https://api.siraj.com/api/` |
| `REACT_APP_CRAWLER_API_URL` | Crawler service endpoint | `https://crawler.siraj.com/api/` |
| `REACT_APP_ENV` | Environment name | `production` |

### Default Ports

- **Development**: 3000
- **Production (Docker)**: 80
- **Backend API**: 8000 (configurable)

## 🔐 Authentication

### Login Credentials

Use your admin credentials to access the dashboard.

### Token Storage

JWT token stored in `localStorage` with key `"token"`.

### Protected Routes

All routes except `/login` require authentication.

## 📦 Project Structure

```
siraj-fe-admin/
├── src/
│   ├── pages/              # Page components
│   │   ├── login/         # Login page
│   │   └── dashboard/     # Main dashboard
│   ├── services/          # API services
│   ├── contexts/          # React contexts
│   └── common/            # Shared components
├── public/                # Static assets
├── build/                 # Production build (generated)
└── templates/             # Kubernetes templates
```

## 🎨 Technology Stack

- **React 18.3.1** - UI framework
- **Ant Design 5.20.6** - UI components
- **Axios 1.7.7** - HTTP client
- **React Router 6.26.2** - Routing
- **React Quill 2.0.0** - Rich text editor

## 🐛 Troubleshooting

### Build Fails

```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

### API Connection Issues

Check:
1. Backend is running
2. `REACT_APP_API_URL` is correct
3. CORS is configured on backend

### Port Already in Use

```bash
# Kill process on port 3000
lsof -ti:3000 | xargs kill -9

# Or use different port
PORT=3001 npm start
```

## 📚 Documentation Links

- **[README.md](./README.md)** - Complete documentation
- **[PRODUCT.md](./PRODUCT.md)** - Product features and workflows
- **[API.md](./API.md)** - API integration guide
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - Deployment instructions
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** - Development guidelines

## 🆘 Getting Help

1. Check documentation files
2. Review troubleshooting sections
3. Check existing GitHub issues
4. Contact development team

## ⚡ Quick Commands

```bash
# Development
npm start              # Start dev server
npm test              # Run tests
npm run build         # Production build

# Docker
docker build -t siraj-admin .
docker run -p 80:80 siraj-admin

# Kubernetes (Helm)
helm install siraj-admin .
helm upgrade siraj-admin .
helm uninstall siraj-admin
```

## 📝 Notes

- **Node Version**: Use Node.js 18.x or higher
- **Browser Support**: Modern browsers (Chrome, Firefox, Safari, Edge)
- **Mobile**: Desktop-first design, responsive layouts included
- **Security**: HTTPS required for production deployments

---

**Need more details?** See [README.md](./README.md) for comprehensive documentation.
