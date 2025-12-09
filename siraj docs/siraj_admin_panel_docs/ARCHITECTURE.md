# Architecture Documentation

## Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Frontend Architecture](#frontend-architecture)
- [Component Architecture](#component-architecture)
- [State Management](#state-management)
- [API Integration Layer](#api-integration-layer)
- [Routing Architecture](#routing-architecture)
- [Authentication & Authorization](#authentication--authorization)
- [Deployment Architecture](#deployment-architecture)
- [Security Architecture](#security-architecture)
- [Performance Considerations](#performance-considerations)
- [Scalability](#scalability)

## Overview

The Siraj Admin Panel is a Single Page Application (SPA) built with React that serves as the administrative interface for the Siraj platform. It follows a modular, component-based architecture with clear separation of concerns.

### Design Principles

1. **Modularity**: Components are self-contained and reusable
2. **Separation of Concerns**: Clear boundaries between UI, business logic, and data access
3. **Scalability**: Architecture supports growth in features and users
4. **Maintainability**: Code is organized for easy updates and debugging
5. **Performance**: Optimized for fast loading and smooth user experience

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         User Browser                         │
│  ┌────────────────────────────────────────────────────────┐ │
│  │              Siraj Admin Panel (React SPA)             │ │
│  │                                                        │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌────────────┐  │ │
│  │  │     Pages    │  │  Components  │  │  Services  │  │ │
│  │  └──────────────┘  └──────────────┘  └────────────┘  │ │
│  │         │                  │                │          │ │
│  │         └──────────────────┴────────────────┘          │ │
│  │                       │                                │ │
│  │              ┌────────▼────────┐                       │ │
│  │              │  Axios Client   │                       │ │
│  │              └────────┬────────┘                       │ │
│  └───────────────────────┼─────────────────────────────────┘ │
└────────────────────────────┼──────────────────────────────────┘
                             │ HTTPS
                             │
                   ┌─────────▼─────────┐
                   │   Nginx / CDN     │
                   └─────────┬─────────┘
                             │
                   ┌─────────▼─────────┐
                   │   Backend API     │
                   │   (Node.js/NestJS)│
                   └─────────┬─────────┘
                             │
                   ┌─────────▼─────────┐
                   │     Database      │
                   │  (PostgreSQL/etc) │
                   └───────────────────┘
```

## Frontend Architecture

### Layer Structure

```
┌─────────────────────────────────────────────────────────┐
│                    Presentation Layer                    │
│  (React Components, Pages, UI Elements)                 │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                    Business Logic Layer                  │
│  (Hooks, Context Providers, State Management)           │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                  Data Access Layer                       │
│  (API Services, Axios Client, HTTP Requests)            │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                    External APIs                         │
│  (Backend REST API, Crawler API)                        │
└─────────────────────────────────────────────────────────┘
```

### Directory Structure

```
src/
├── pages/                      # Page-level components
│   ├── login/                 # Login page
│   └── dashboard/             # Main dashboard
│       ├── components/        # Page-specific components
│       ├── hooks/            # Custom hooks
│       └── common/           # Utilities and helpers
├── common/                    # Shared code
│   ├── components/           # Reusable UI components
│   └── constants/            # Application constants
├── contexts/                  # React Context providers
│   ├── user/                 # User authentication state
│   ├── majors/              # Majors data
│   └── countryCodes/        # Country codes data
├── services/                  # API service layer
│   ├── base/                 # Axios configuration
│   ├── auth/                # Authentication services
│   ├── product/             # Product services
│   └── ...                  # Other resource services
├── routes/                    # Routing configuration
│   ├── index.js             # Main router
│   └── ProtectedRoute/      # Auth guard
├── assets/                    # Static assets
│   └── icons/               # SVG icons
├── App.js                     # Root component
└── index.js                   # Entry point
```

## Component Architecture

### Component Hierarchy

```
App
├── ConfigProvider (Ant Design theming)
│   └── UserProvider (Authentication state)
│       └── CountryCodesProvider (Country data)
│           └── RouterProvider
│               ├── Login
│               └── Dashboard (Protected)
│                   ├── Sider (Navigation)
│                   ├── Header (User info)
│                   └── Content (Dynamic based on menu)
│                       ├── StudentManagement
│                       ├── AdvisorManagement
│                       ├── ProductManagement
│                       ├── UniversityManagement
│                       └── ... (other management components)
```

### Component Types

#### 1. Page Components

Located in `src/pages/`. Represent full pages/views.

**Example**: `Dashboard`, `Login`

**Characteristics**:
- Top-level routing targets
- Orchestrate multiple sub-components
- Handle page-level state and logic
- Connect to context providers

#### 2. Container Components

Smart components with business logic.

**Example**: `ProductManagement`, `UserManagement`

**Characteristics**:
- Manage local state
- Handle data fetching
- Process business logic
- Pass data to presentational components

#### 3. Presentational Components

Dumb components focused on rendering.

**Example**: `CustomTable`, `Button`, `Modal`

**Characteristics**:
- Receive data via props
- No business logic
- Highly reusable
- UI-focused

#### 4. Layout Components

Structure and layout wrappers.

**Example**: `ContentWrapper`, `Sidebar`, `Header`

**Characteristics**:
- Provide consistent layout
- Handle responsive behavior
- No business logic

### Component Communication

```
┌──────────────────┐
│  Parent Component│
│                  │
│  ┌────────────┐  │
│  │   State    │  │
│  └──────┬─────┘  │
│         │Props   │
└─────────┼────────┘
          │
    ┌─────▼─────┐
    │   Child   │
    │ Component │
    │           │
    │ Callbacks │
    └─────┬─────┘
          │
    ┌─────▼─────┐
    │  Parent   │
    │  Updates  │
    └───────────┘
```

**Data Flow**:
- Props flow down from parent to child
- Events bubble up through callbacks
- Context used for deeply nested data
- Services handle external data

## State Management

### Local State (useState)

Used for component-specific state:

```javascript
const [loading, setLoading] = useState(false);
const [data, setData] = useState([]);
const [selectedItem, setSelectedItem] = useState(null);
```

**Use Cases**:
- Form inputs
- UI state (modals, dropdowns)
- Component-specific data

### Context API

Used for global/shared state:

```javascript
// UserContext - Authentication state
const UserContext = createContext();

// Usage
const { user, setUser, logout } = useUser();
```

**Current Contexts**:
1. **UserContext**: Authentication, user info, logout
2. **MajorsContext**: List of academic majors
3. **CountryCodesContext**: Country codes for forms

**When to Use**:
- Data needed by many components
- Authentication state
- Theme/configuration
- Reference data (countries, majors)

### Custom Hooks

Encapsulate reusable logic:

```javascript
// useProducts.js
export const useProducts = () => {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  
  const fetchProducts = async () => {
    // Fetch logic
  };
  
  const updateProduct = async (data) => {
    // Update logic
  };
  
  return { products, loading, fetchProducts, updateProduct };
};
```

**Benefits**:
- Reusable logic
- Cleaner components
- Easier testing
- Better organization

## API Integration Layer

### Architecture

```
Component
    ↓
Custom Hook (useProducts)
    ↓
Service Layer (productService)
    ↓
Axios Client (base configuration)
    ↓
HTTP Request
    ↓
Backend API
```

### Service Layer Pattern

Each resource has a dedicated service module:

```javascript
// src/services/product/index.js

import axiosClient from '../base';

export const getProducts = () => {
  return axiosClient.get('products');
};

export const updateProduct = (data) => {
  return axiosClient.put(`products/${data.id}`, data);
};

export const deleteProduct = (id) => {
  return axiosClient.delete(`products/${id}`);
};
```

### Axios Configuration

Base configuration with interceptors:

```javascript
// src/services/base/index.js

const axiosClient = axios.create({
  baseURL: process.env.REACT_APP_API_URL,
  headers: {
    'content-type': 'application/json',
  }
});

// Request interceptor - Add auth token
axiosClient.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  }
);

// Response interceptor - Handle errors
axiosClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Redirect to login
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);
```

### Error Handling

Three levels of error handling:

1. **Global**: Axios interceptors catch all API errors
2. **Service**: Service methods can handle specific errors
3. **Component**: Try-catch in components for user feedback

```javascript
try {
  await productService.updateProduct(data);
  notification.success({ message: 'Success!' });
} catch (error) {
  notification.error({ 
    message: 'Error', 
    description: error.response?.data?.message 
  });
}
```

## Routing Architecture

### Router Configuration

```javascript
// src/routes/index.js

export const router = createBrowserRouter([
  {
    path: '*',
    element: <Login />
  },
  {
    path: '/dashboard',
    element: (
      <ProtectedRoute>
        <MajorsProvider>
          <Dashboard />
        </MajorsProvider>
      </ProtectedRoute>
    )
  }
]);
```

### Route Protection

```javascript
// src/routes/ProtectedRoute/index.js

const ProtectedRoute = ({ children }) => {
  const token = localStorage.getItem('token');
  
  if (!token) {
    return <Navigate to="/login" replace />;
  }
  
  return children;
};
```

### Navigation Flow

```
User Access URL
    ↓
Router matches path
    ↓
Is route protected? → Yes → Check auth token
                      ↓              ↓
                      No         Token exists?
                      ↓              ↓
                   Render        Yes: Render
                                 No: Redirect to /login
```

## Authentication & Authorization

### Authentication Flow

```
1. User enters credentials
        ↓
2. POST /api/auth/login
        ↓
3. Receive JWT token
        ↓
4. Store in localStorage
        ↓
5. Update UserContext
        ↓
6. Redirect to /dashboard
        ↓
7. Token added to all API requests
```

### Token Management

```javascript
// Store token
localStorage.setItem('token', jwt);

// Retrieve token
const token = localStorage.getItem('token');

// Remove token (logout)
localStorage.removeItem('token');

// Auto-inject in requests
config.headers.Authorization = `Bearer ${token}`;
```

### Authorization

Currently single admin role. Future expansion:

```
Admin (Full access)
    ├── Content Manager (Read/Write educational content)
    ├── Support Staff (Read user data, manage sessions)
    └── Viewer (Read-only access)
```

## Deployment Architecture

### Docker Architecture

```
┌─────────────────────────────────────────┐
│         Docker Image                    │
│                                         │
│  ┌────────────────────────────────┐    │
│  │  Stage 1: Build                │    │
│  │  - Node.js 18                  │    │
│  │  - npm install                 │    │
│  │  - npm run build               │    │
│  │  - Output: /app/build          │    │
│  └────────────────────────────────┘    │
│                                         │
│  ┌────────────────────────────────┐    │
│  │  Stage 2: Serve                │    │
│  │  - Nginx Alpine                │    │
│  │  - Copy build artifacts        │    │
│  │  - nginx.conf                  │    │
│  │  - Listen on port 80           │    │
│  └────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

### Kubernetes Architecture

```
┌──────────────────────────────────────────────────────┐
│                  Kubernetes Cluster                   │
│                                                       │
│  ┌─────────────────────────────────────────────┐    │
│  │              Ingress Controller              │    │
│  │  (siraj.local → siraj-admin service)        │    │
│  └────────────────────┬─────────────────────────┘    │
│                       │                              │
│  ┌────────────────────▼─────────────────────────┐    │
│  │              Service (ClusterIP)             │    │
│  │  (Load balancer for pods)                   │    │
│  └────────────────────┬─────────────────────────┘    │
│                       │                              │
│  ┌────────────────────▼─────────────────────────┐    │
│  │             Deployment                       │    │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐     │    │
│  │  │  Pod 1  │  │  Pod 2  │  │  Pod 3  │     │    │
│  │  │ (Nginx) │  │ (Nginx) │  │ (Nginx) │     │    │
│  │  └─────────┘  └─────────┘  └─────────┘     │    │
│  └──────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────┘
```

## Security Architecture

### Security Layers

1. **Transport Layer**: HTTPS/TLS encryption
2. **Authentication**: JWT token validation
3. **Authorization**: Role-based access (future)
4. **Input Validation**: Client-side and server-side
5. **XSS Prevention**: React automatic escaping
6. **CSRF Protection**: Token-based authentication

### Security Best Practices

- Tokens stored in localStorage (consider httpOnly cookies for future)
- No sensitive data in Redux/state
- Environment variables for configuration
- CORS configured on backend
- Content Security Policy headers
- Regular dependency updates

## Performance Considerations

### Optimization Techniques

1. **Code Splitting**: React.lazy() for route-based splitting
2. **Lazy Loading**: Load components on demand
3. **Memoization**: React.memo for expensive components
4. **Virtualization**: For long lists (future enhancement)
5. **Caching**: Service worker for static assets
6. **Compression**: Gzip enabled in Nginx
7. **CDN**: Static assets served from CDN

### Bundle Optimization

```javascript
// Current bundle size: ~533 KB (gzipped)

// Optimization strategies:
- Code splitting by route
- Tree shaking (already enabled)
- Lazy load Ant Design components
- Remove unused dependencies
- Use production builds
```

### Performance Metrics

Target metrics:
- **First Contentful Paint**: < 1.5s
- **Time to Interactive**: < 3.5s
- **Largest Contentful Paint**: < 2.5s
- **Cumulative Layout Shift**: < 0.1

## Scalability

### Horizontal Scaling

Kubernetes supports horizontal pod autoscaling:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: siraj-admin-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: siraj-admin
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
```

### Caching Strategy

```
Browser Cache
    ↓
CDN Cache
    ↓
Application
    ↓
API Response Cache
    ↓
Database
```

### Future Considerations

- Implement Redis for session management
- Add service worker for offline support
- Consider GraphQL for optimized data fetching
- Implement real-time updates with WebSocket
- Add monitoring with Application Insights

---

## Diagrams Summary

This document includes several architectural diagrams:

1. **System Architecture**: Overall system structure
2. **Layer Structure**: Frontend architectural layers
3. **Component Hierarchy**: React component tree
4. **Component Communication**: Data flow patterns
5. **API Integration**: Service layer architecture
6. **Navigation Flow**: Routing and authentication
7. **Authentication Flow**: Login and token management
8. **Docker Architecture**: Multi-stage build structure
9. **Kubernetes Architecture**: Cluster deployment topology

For implementation details, see:
- [README.md](./README.md) - General documentation
- [API.md](./API.md) - API integration details
- [DEPLOYMENT.md](./DEPLOYMENT.md) - Deployment specifics

---

**Last Updated**: December 2025
