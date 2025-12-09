# API Integration Guide

This document describes the API integration architecture and endpoints used by HexMate.

## Table of Contents

- [Overview](#overview)
- [Authentication](#authentication)
- [API Structure](#api-structure)
- [Common Endpoints](#common-endpoints)
- [Module-Specific Endpoints](#module-specific-endpoints)
- [Request/Response Format](#requestresponse-format)
- [Error Handling](#error-handling)
- [Best Practices](#best-practices)

## Overview

HexMate communicates with a backend REST API for all data operations. The API base URL is configured via the `REACT_APP_BASE_API` environment variable.

### API Configuration

```typescript
// Base URL from environment variable
const BASE_URL = process.env.REACT_APP_BASE_API;
// Example: https://api.hexmate.example.com/api/

// All API calls are made relative to this base URL
// Example endpoint: ${BASE_URL}auth/login
// Results in: https://api.hexmate.example.com/api/auth/login
```

### HTTP Client

HexMate uses Axios for HTTP requests:

```typescript
import axios from 'axios';

// Create axios instance with base configuration
const apiClient = axios.create({
  baseURL: process.env.REACT_APP_BASE_API,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Add request interceptor for authentication
apiClient.interceptors.request.use((config) => {
  const token = localStorage.getItem('accessToken');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Add response interceptor for error handling
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    // Handle token expiration
    if (error.response?.status === 401) {
      // Trigger token refresh or logout
    }
    return Promise.reject(error);
  }
);
```

## Authentication

### Login

**Endpoint:** `POST /auth/login`

**Request:**
```json
{
  "username": "user@example.com",
  "password": "password123",
  "rememberMe": true
}
```

**Response:**
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiryDate": "2024-12-06T10:00:00Z",
  "user": {
    "id": 1,
    "username": "user@example.com",
    "fullName": "John Doe",
    "modules": "1,2,3",
    "isAdmin": false
  }
}
```

**Implementation:**
```typescript
export const login = async (username: string, password: string, rememberMe: boolean) => {
  const response = await axios.post(`${BASE_URL}auth/login`, {
    username,
    password,
    rememberMe
  });
  return response.data;
};
```

### Token Refresh

**Endpoint:** `POST /auth/refresh`

**Request:**
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response:**
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiryDate": "2024-12-06T10:00:00Z"
}
```

### Logout

**Endpoint:** `POST /auth/logout`

**Headers:**
```
Authorization: Bearer {accessToken}
```

**Response:**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

### Password Reset

**Request Reset:**
```
POST /auth/forgot-password
Body: { "email": "user@example.com" }
```

**Reset Password:**
```
POST /auth/reset-password
Body: { "token": "...", "newPassword": "..." }
```

## API Structure

### Base Endpoints

All endpoints are relative to `REACT_APP_BASE_API`.

**Authentication:** `/auth/*`
- Login, logout, token refresh, password reset

**User Management:** `/users/*`
- User CRUD operations, profile management

**DMS Endpoints:** `/dms/*`
- Document management operations

**CTS Endpoints:** `/cts/*`
- Correspondence tracking operations

**VMS Endpoints:** `/vms/*`
- Visitor management operations

## Common Endpoints

### User Management

#### Get All Users

```
GET /users
Authorization: Bearer {token}

Response:
[
  {
    "id": 1,
    "username": "user@example.com",
    "fullName": "John Doe",
    "modules": "1,2",
    "isAdmin": false,
    "isActive": true,
    "createdAt": "2024-01-01T00:00:00Z"
  }
]
```

#### Get User by ID

```
GET /users/{id}
Authorization: Bearer {token}

Response:
{
  "id": 1,
  "username": "user@example.com",
  "fullName": "John Doe",
  "email": "user@example.com",
  "modules": "1,2",
  "userGroups": [1, 2],
  "isAdmin": false,
  "isActive": true
}
```

#### Create User

```
POST /users
Authorization: Bearer {token}
Content-Type: application/json

Body:
{
  "username": "newuser@example.com",
  "fullName": "New User",
  "password": "password123",
  "modules": "1,2",
  "isAdmin": false
}

Response:
{
  "id": 2,
  "username": "newuser@example.com",
  "fullName": "New User",
  "modules": "1,2",
  "isAdmin": false
}
```

#### Update User

```
PUT /users/{id}
Authorization: Bearer {token}
Content-Type: application/json

Body:
{
  "fullName": "Updated Name",
  "modules": "1,2,3",
  "isActive": true
}

Response:
{
  "id": 1,
  "username": "user@example.com",
  "fullName": "Updated Name",
  "modules": "1,2,3",
  "isActive": true
}
```

#### Delete User

```
DELETE /users/{id}
Authorization: Bearer {token}

Response:
{
  "success": true,
  "message": "User deleted successfully"
}
```

### User Groups

```
GET /usergroups                    # List all groups
GET /usergroups/{id}               # Get group details
POST /usergroups                   # Create group
PUT /usergroups/{id}               # Update group
DELETE /usergroups/{id}            # Delete group
```

### User Roles

```
GET /userroles                     # List all roles
GET /userroles/{id}                # Get role details
POST /userroles                    # Create role
PUT /userroles/{id}                # Update role
DELETE /userroles/{id}             # Delete role
```

## Module-Specific Endpoints

### DMS (Document Management System)

#### Documents

```
GET /dms/documents                 # List documents
GET /dms/documents/{id}            # Get document details
POST /dms/documents                # Upload document
PUT /dms/documents/{id}            # Update document
DELETE /dms/documents/{id}         # Delete document
GET /dms/documents/{id}/download   # Download document
GET /dms/documents/{id}/versions   # Get document versions
```

#### Directories

```
GET /dms/directories               # List directories
GET /dms/directories/{id}          # Get directory details
POST /dms/directories              # Create directory
PUT /dms/directories/{id}          # Update directory
DELETE /dms/directories/{id}       # Delete directory
```

#### Cabinets

```
GET /dms/cabinets                  # List cabinets
POST /dms/cabinets                 # Create cabinet
PUT /dms/cabinets/{id}             # Update cabinet
DELETE /dms/cabinets/{id}          # Delete cabinet
```

#### Document Types & Categories

```
GET /dms/documenttypes             # List document types
POST /dms/documenttypes            # Create document type
PUT /dms/documenttypes/{id}        # Update document type
DELETE /dms/documenttypes/{id}     # Delete document type

GET /dms/documentcategories        # List categories
POST /dms/documentcategories       # Create category
PUT /dms/documentcategories/{id}   # Update category
DELETE /dms/documentcategories/{id}# Delete category
```

#### Document Profiles

```
GET /dms/documentprofiles          # List profiles
POST /dms/documentprofiles         # Create profile
PUT /dms/documentprofiles/{id}     # Update profile
DELETE /dms/documentprofiles/{id}  # Delete profile
```

#### Reports & Logs

```
GET /dms/reports                   # Get DMS reports
GET /dms/logs                      # Get audit logs
```

### CTS (Correspondence Tracking System)

#### Correspondence

```
GET /cts/correspondence            # List correspondence
GET /cts/correspondence/{id}       # Get correspondence details
POST /cts/correspondence           # Create correspondence
PUT /cts/correspondence/{id}       # Update correspondence
DELETE /cts/correspondence/{id}    # Delete correspondence
```

#### Settings

```
GET /cts/entitytypes               # List entity types
GET /cts/privacylevels             # List privacy levels
GET /cts/importancelevels          # List importance levels
GET /cts/correspondencetypes       # List correspondence types
GET /cts/entities                  # List entities
GET /cts/categories                # List categories
GET /cts/referencetypes            # List reference types
GET /cts/contacttypes              # List contact types
GET /cts/domaintypes               # List domain types
```

#### Routing & Delegation

```
GET /cts/routinggroups             # List routing groups
POST /cts/routinggroups            # Create routing group
PUT /cts/routinggroups/{id}        # Update routing group

GET /cts/delegations               # List delegations
POST /cts/delegations              # Create delegation
PUT /cts/delegations/{id}          # Update delegation
DELETE /cts/delegations/{id}       # Delete delegation
```

#### Templates

```
GET /cts/templates                 # List document templates
GET /cts/templates/{id}            # Get template details
POST /cts/templates                # Create template
PUT /cts/templates/{id}            # Update template
DELETE /cts/templates/{id}         # Delete template
```

#### Dashboard & Reports

```
GET /cts/dashboard                 # Get dashboard data
GET /cts/reports                   # Get CTS reports
GET /cts/logs                      # Get audit logs
```

### VMS (Visitor Management System)

#### Appointments

```
GET /vms/appointments              # List appointments
GET /vms/appointments/{id}         # Get appointment details
POST /vms/appointments             # Create appointment
PUT /vms/appointments/{id}         # Update appointment
DELETE /vms/appointments/{id}      # Delete appointment
GET /vms/appointments/archived     # List archived appointments
```

#### Check-ins

```
GET /vms/checkins                  # List check-ins
POST /vms/checkins                 # Create check-in
PUT /vms/checkins/{id}             # Update check-in (check-out)
GET /vms/checkins/active           # List active check-ins
```

#### Workflows

```
GET /vms/workflows                 # List workflows
POST /vms/workflows                # Create workflow
PUT /vms/workflows/{id}            # Update workflow
DELETE /vms/workflows/{id}         # Delete workflow
```

#### Dashboard

```
GET /vms/dashboard                 # Get dashboard statistics
```

## Request/Response Format

### Request Headers

```
Authorization: Bearer {accessToken}
Content-Type: application/json
Accept: application/json
```

### Pagination

For list endpoints that support pagination:

**Query Parameters:**
```
?page=1&pageSize=20&sortBy=createdAt&sortOrder=desc
```

**Response:**
```json
{
  "data": [...],
  "pagination": {
    "currentPage": 1,
    "pageSize": 20,
    "totalItems": 150,
    "totalPages": 8
  }
}
```

### Filtering

```
?filter[status]=active&filter[module]=DMS
?search=keyword
?startDate=2024-01-01&endDate=2024-12-31
```

### File Uploads

**Content-Type:** `multipart/form-data`

```typescript
const formData = new FormData();
formData.append('file', file);
formData.append('name', 'Document Name');
formData.append('description', 'Document description');

const response = await axios.post(`${BASE_URL}dms/documents`, formData, {
  headers: {
    'Content-Type': 'multipart/form-data',
  },
});
```

## Error Handling

### HTTP Status Codes

- `200` - Success
- `201` - Created
- `204` - No Content (successful deletion)
- `400` - Bad Request (validation error)
- `401` - Unauthorized (invalid/expired token)
- `403` - Forbidden (insufficient permissions)
- `404` - Not Found
- `409` - Conflict (duplicate entry)
- `422` - Unprocessable Entity (validation error)
- `500` - Internal Server Error

### Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      },
      {
        "field": "password",
        "message": "Password must be at least 8 characters"
      }
    ]
  }
}
```

### Error Handling in Code

```typescript
try {
  const response = await apiClient.get('/users');
  return response.data;
} catch (error) {
  if (axios.isAxiosError(error)) {
    if (error.response) {
      // Server responded with error
      const { status, data } = error.response;
      
      switch (status) {
        case 401:
          // Handle unauthorized (redirect to login)
          break;
        case 403:
          // Handle forbidden
          break;
        case 404:
          // Handle not found
          break;
        default:
          // Handle other errors
          console.error('API Error:', data.error);
      }
    } else if (error.request) {
      // Request was made but no response
      console.error('Network error:', error.message);
    } else {
      // Something else happened
      console.error('Error:', error.message);
    }
  }
  throw error;
}
```

## Best Practices

### 1. Use TypeScript Interfaces

```typescript
interface User {
  id: number;
  username: string;
  fullName: string;
  modules?: string;
  isAdmin: boolean;
}

interface ApiResponse<T> {
  data: T;
  success: boolean;
  message?: string;
}

const getUser = async (id: number): Promise<User> => {
  const response = await apiClient.get<ApiResponse<User>>(`/users/${id}`);
  return response.data.data;
};
```

### 2. Centralize API Calls

Create dedicated API service files:

```typescript
// services/userService.ts
export const userService = {
  getAll: () => apiClient.get('/users'),
  getById: (id: number) => apiClient.get(`/users/${id}`),
  create: (data: CreateUserDto) => apiClient.post('/users', data),
  update: (id: number, data: UpdateUserDto) => apiClient.put(`/users/${id}`, data),
  delete: (id: number) => apiClient.delete(`/users/${id}`),
};
```

### 3. Handle Loading States

```typescript
const [loading, setLoading] = useState(false);
const [error, setError] = useState<string | null>(null);

const fetchData = async () => {
  try {
    setLoading(true);
    setError(null);
    const data = await userService.getAll();
    setUsers(data);
  } catch (err) {
    setError('Failed to load users');
  } finally {
    setLoading(false);
  }
};
```

### 4. Implement Request Cancellation

```typescript
useEffect(() => {
  const controller = new AbortController();
  
  const fetchData = async () => {
    try {
      const response = await axios.get('/users', {
        signal: controller.signal
      });
      setUsers(response.data);
    } catch (error) {
      if (!axios.isCancel(error)) {
        console.error(error);
      }
    }
  };
  
  fetchData();
  
  return () => controller.abort();
}, []);
```

### 5. Implement Retry Logic

```typescript
const apiCallWithRetry = async (fn: () => Promise<any>, retries = 3) => {
  for (let i = 0; i < retries; i++) {
    try {
      return await fn();
    } catch (error) {
      if (i === retries - 1) throw error;
      await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
    }
  }
};
```

### 6. Cache API Responses

Consider implementing caching for frequently accessed data:

```typescript
const cache = new Map();

const getCachedData = async (key: string, fetcher: () => Promise<any>, ttl = 60000) => {
  if (cache.has(key)) {
    const { data, timestamp } = cache.get(key);
    if (Date.now() - timestamp < ttl) {
      return data;
    }
  }
  
  const data = await fetcher();
  cache.set(key, { data, timestamp: Date.now() });
  return data;
};
```

## See Also

- [Architecture Documentation](ARCHITECTURE.md)
- [Development Guide](DEVELOPMENT.md)
- [Configuration Guide](CONFIGURATION.md)
- [Security Guide](SECURITY.md)
