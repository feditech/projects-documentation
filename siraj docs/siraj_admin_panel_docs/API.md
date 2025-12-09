# API Documentation

## Table of Contents

- [Overview](#overview)
- [Base Configuration](#base-configuration)
- [Authentication](#authentication)
- [Service Modules](#service-modules)
- [Error Handling](#error-handling)
- [Rate Limiting](#rate-limiting)
- [Response Formats](#response-formats)

## Overview

The Siraj Admin Panel communicates with the backend API using Axios for HTTP requests. All API calls are organized into service modules that correspond to different resource types.

### API Architecture

```
Frontend (React)
    ↓
Service Layer (Axios)
    ↓
HTTP Requests
    ↓
Backend API
    ↓
Database
```

## Base Configuration

### Axios Client Setup

Located in `src/services/base/index.js`:

```javascript
import axios from "axios";

const apiUrl = process.env.REACT_APP_API_URL || "http://localhost:8000/api/";

const axiosClient = axios.create({
  headers: {
    "content-type": "application/json",
  },
  baseURL: apiUrl,
});

// Request interceptor for adding auth token
axiosClient.interceptors.request.use(
  (config) => {
    const accessToken = localStorage.getItem("token");
    if (accessToken) {
      config.headers.Authorization = `Bearer ${accessToken}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

export default axiosClient;
```

### Environment Variables

Configure API endpoints using environment variables:

```bash
# Development
REACT_APP_API_URL=http://localhost:8000/api/

# Production
REACT_APP_API_URL=https://api.siraj.com/api/

# Crawler Service
REACT_APP_CRAWLER_API_URL=https://app-siraj-crawler.azurewebsites.net/api/
```

## Authentication

### Login Flow

**Endpoint**: `POST /api/auth/login`

**Request**:
```json
{
  "email": "admin@siraj.com",
  "password": "securepassword"
}
```

**Response**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 1,
    "email": "admin@siraj.com",
    "userType": "ADMIN",
    "name": "Admin User"
  }
}
```

**Service Implementation** (`src/services/auth/index.js`):
```javascript
export const login = (credentials) => {
  return axiosClient.post("auth/login", credentials);
};
```

### Token Management

- **Storage**: JWT token stored in `localStorage` with key `"token"`
- **Transmission**: Automatically added to `Authorization` header as `Bearer {token}`
- **Expiration**: Token expiration handled by backend; frontend redirects to login on 401 errors

### Protected Routes

All routes except login require authentication:

```javascript
// src/routes/ProtectedRoute/index.js
const ProtectedRoute = ({ children }) => {
  const token = localStorage.getItem("token");
  
  if (!token) {
    return <Navigate to="/login" />;
  }
  
  return children;
};
```

## Service Modules

### 1. Product Service

**Location**: `src/services/product/index.js`

#### Get All Products

```javascript
export const getProducts = () => {
  return axiosClient.get("products");
};
```

**Endpoint**: `GET /api/products`

**Response**:
```json
{
  "data": [
    {
      "id": 1,
      "title": "Basic Package",
      "features": "<ul><li>5 sessions</li><li>Career assessment</li></ul>",
      "priceInUSD": 99,
      "priceInJordan": 70,
      "totalSessions": 5,
      "totalJobTrialExps": 1,
      "isJobTrial": false,
      "updatedAt": "2025-01-15T10:30:00Z",
      "createdAt": "2025-01-01T00:00:00Z"
    }
  ]
}
```

#### Update Product

```javascript
export const updateProduct = ({
  id,
  title,
  features,
  priceInUSD,
  priceInJordan,
  totalSessions,
  totalJobTrialExps,
  isJobTrial,
}) => {
  return axiosClient.put(`products/${id}`, {
    title,
    features,
    priceInUSD,
    priceInJordan,
    totalSessions,
    totalJobTrialExps,
    isJobTrial,
  });
};
```

**Endpoint**: `PUT /api/products/:id`

**Request Body**:
```json
{
  "title": "Premium Package",
  "features": "<ul><li>10 sessions</li></ul>",
  "priceInUSD": 299,
  "priceInJordan": 210,
  "totalSessions": 10,
  "totalJobTrialExps": 3,
  "isJobTrial": true
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "id": 1,
    "title": "Premium Package",
    // ... updated fields
  }
}
```

### 2. Student Service

**Location**: `src/services/student/index.js`

#### Get All Students

```javascript
export const getStudents = () => {
  return axiosClient.get("students");
};
```

**Endpoint**: `GET /api/students`

**Query Parameters**:
- `page` (optional): Page number for pagination
- `limit` (optional): Results per page
- `search` (optional): Search by name or email
- `status` (optional): Filter by account status

#### Get Student by ID

```javascript
export const getStudentById = (id) => {
  return axiosClient.get(`students/${id}`);
};
```

**Endpoint**: `GET /api/students/:id`

#### Update Student

```javascript
export const updateStudent = (id, studentData) => {
  return axiosClient.put(`students/${id}`, studentData);
};
```

**Endpoint**: `PUT /api/students/:id`

### 3. Advisor Service

**Location**: `src/services/advisor/index.js`

#### Get All Advisors

```javascript
export const getAdvisors = () => {
  return axiosClient.get("advisors");
};
```

**Endpoint**: `GET /api/advisors`

#### Create Advisor

```javascript
export const createAdvisor = (advisorData) => {
  return axiosClient.post("advisors", advisorData);
};
```

**Endpoint**: `POST /api/advisors`

#### Update Advisor

```javascript
export const updateAdvisor = (id, advisorData) => {
  return axiosClient.put(`advisors/${id}`, advisorData);
};
```

**Endpoint**: `PUT /api/advisors/:id`

### 4. University Service

**Location**: `src/services/university/index.js`

#### Get All Universities

```javascript
export const getUniversities = () => {
  return axiosClient.get("universities");
};
```

**Endpoint**: `GET /api/universities`

#### Create University

```javascript
export const createUniversity = (universityData) => {
  return axiosClient.post("universities", universityData);
};
```

**Endpoint**: `POST /api/universities`

**Request Body**:
```json
{
  "name": "Example University",
  "location": "City, Country",
  "country": "Country Name",
  "contactEmail": "admin@university.edu",
  "contactPhone": "+1234567890",
  "website": "https://www.university.edu",
  "admissionRequirements": "High school diploma, SAT scores",
  "applicationDeadline": "2025-12-31"
}
```

#### Update University

```javascript
export const updateUniversity = (id, universityData) => {
  return axiosClient.put(`universities/${id}`, universityData);
};
```

**Endpoint**: `PUT /api/universities/:id`

#### Delete University

```javascript
export const deleteUniversity = (id) => {
  return axiosClient.delete(`universities/${id}`);
};
```

**Endpoint**: `DELETE /api/universities/:id`

### 5. Program Service

**Location**: `src/services/program/index.js`

#### Get All Programs

```javascript
export const getPrograms = () => {
  return axiosClient.get("programs");
};
```

**Endpoint**: `GET /api/programs`

#### Create Program

```javascript
export const createProgram = (programData) => {
  return axiosClient.post("programs", programData);
};
```

**Endpoint**: `POST /api/programs`

#### Update Program

```javascript
export const updateProgram = (id, programData) => {
  return axiosClient.put(`programs/${id}`, programData);
};
```

**Endpoint**: `PUT /api/programs/:id`

### 6. Company Service

**Location**: `src/services/company/index.js`

#### Get All Companies

```javascript
export const getCompanies = () => {
  return axiosClient.get("companies");
};
```

**Endpoint**: `GET /api/companies`

#### Create Company

```javascript
export const createCompany = (companyData) => {
  return axiosClient.post("companies", companyData);
};
```

**Endpoint**: `POST /api/companies`

### 7. Job Trial Service

**Location**: `src/services/jobTrial/index.js`

#### Get All Job Trials

```javascript
export const getJobTrials = () => {
  return axiosClient.get("job-trials");
};
```

**Endpoint**: `GET /api/job-trials`

#### Create Job Trial

```javascript
export const createJobTrial = (jobTrialData) => {
  return axiosClient.post("job-trials", jobTrialData);
};
```

**Endpoint**: `POST /api/job-trials`

#### Get Applications for Job Trial

```javascript
export const getJobTrialApplications = (jobTrialId) => {
  return axiosClient.get(`job-trials/${jobTrialId}/applications`);
};
```

**Endpoint**: `GET /api/job-trials/:id/applications`

### 8. Session Service

**Location**: `src/services/session/index.js`

#### Get All Sessions

```javascript
export const getSessions = () => {
  return axiosClient.get("sessions");
};
```

**Endpoint**: `GET /api/sessions`

**Query Parameters**:
- `startDate` (optional): Filter sessions from this date
- `endDate` (optional): Filter sessions until this date
- `advisorId` (optional): Filter by advisor
- `studentId` (optional): Filter by student
- `status` (optional): Filter by status

#### Create Session

```javascript
export const createSession = (sessionData) => {
  return axiosClient.post("sessions", sessionData);
};
```

**Endpoint**: `POST /api/sessions`

#### Update Session

```javascript
export const updateSession = (id, sessionData) => {
  return axiosClient.put(`sessions/${id}`, sessionData);
};
```

**Endpoint**: `PUT /api/sessions/:id`

### 9. Coupon Service

**Location**: `src/services/coupon/index.js`

#### Get All Coupons

```javascript
export const getCoupons = () => {
  return axiosClient.get("coupons");
};
```

**Endpoint**: `GET /api/coupons`

#### Create Coupon

```javascript
export const createCoupon = (couponData) => {
  return axiosClient.post("coupons", couponData);
};
```

**Endpoint**: `POST /api/coupons`

**Request Body**:
```json
{
  "code": "SAVE20",
  "discountType": "percentage",
  "discountValue": 20,
  "validFrom": "2025-01-01",
  "validTo": "2025-12-31",
  "maxUses": 100,
  "productIds": [1, 2, 3]
}
```

#### Validate Coupon

```javascript
export const validateCoupon = (code) => {
  return axiosClient.get(`coupons/validate/${code}`);
};
```

**Endpoint**: `GET /api/coupons/validate/:code`

### 10. Crawling Job Service

**Location**: `src/services/crawlingJob/index.js`

#### Get All Crawling Jobs

```javascript
export const getCrawlingJobs = () => {
  return axiosClient.get("crawling-jobs");
};
```

**Endpoint**: `GET /api/crawling-jobs`

#### Create Crawling Job

```javascript
export const createCrawlingJob = (jobData) => {
  return axiosClient.post("crawling-jobs", jobData);
};
```

**Endpoint**: `POST /api/crawling-jobs`

#### Get Crawling Job Status

```javascript
export const getCrawlingJobStatus = (jobId) => {
  return axiosClient.get(`crawling-jobs/${jobId}/status`);
};
```

**Endpoint**: `GET /api/crawling-jobs/:id/status`

### 11. Country Service

**Location**: `src/services/country/index.js`

#### Get All Countries

```javascript
export const getCountries = () => {
  return axiosClient.get("countries");
};
```

**Endpoint**: `GET /api/countries`

### 12. Major Service

**Location**: `src/services/major/index.js`

#### Get All Majors

```javascript
export const getMajors = () => {
  return axiosClient.get("majors");
};
```

**Endpoint**: `GET /api/majors`

## Error Handling

### Error Response Format

All API errors follow a consistent format:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Email is required"
      }
    ]
  }
}
```

### Common HTTP Status Codes

| Status Code | Meaning | Handling |
|-------------|---------|----------|
| 200 | Success | Parse response data |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Validation error, show field errors |
| 401 | Unauthorized | Redirect to login, clear token |
| 403 | Forbidden | Show permission error |
| 404 | Not Found | Show resource not found error |
| 500 | Server Error | Show generic error, retry option |

### Error Handling in Components

```javascript
try {
  const response = await productService.updateProduct(productData);
  notification.success({
    message: "Success!",
    description: "Product updated successfully"
  });
} catch (error) {
  notification.error({
    message: "Error!",
    description: error.response?.data?.error?.message || "An error occurred"
  });
}
```

### Axios Interceptors

Add response interceptor for global error handling:

```javascript
axiosClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem("token");
      window.location.href = "/login";
    }
    return Promise.reject(error);
  }
);
```

## Rate Limiting

### Default Limits

- **Authenticated requests**: 100 requests per minute per user
- **Unauthenticated requests**: 20 requests per minute per IP

### Rate Limit Headers

Response includes rate limit information:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

### Handling Rate Limits

```javascript
if (error.response?.status === 429) {
  const resetTime = error.response.headers['x-ratelimit-reset'];
  notification.warning({
    message: "Rate Limit Exceeded",
    description: `Please try again after ${new Date(resetTime * 1000).toLocaleTimeString()}`
  });
}
```

## Response Formats

### Success Response

```json
{
  "success": true,
  "data": {
    // Resource data
  },
  "meta": {
    "timestamp": "2025-01-15T10:30:00Z"
  }
}
```

### List Response with Pagination

```json
{
  "success": true,
  "data": [
    // Array of resources
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "pages": 8
  }
}
```

### Error Response

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  }
}
```

## Best Practices

### 1. Always Handle Errors

```javascript
// ✅ Good
try {
  const response = await service.getData();
  handleSuccess(response.data);
} catch (error) {
  handleError(error);
}

// ❌ Bad
const response = await service.getData();
handleSuccess(response.data);
```

### 2. Use Loading States

```javascript
const [loading, setLoading] = useState(false);

const fetchData = async () => {
  setLoading(true);
  try {
    const response = await service.getData();
    setData(response.data);
  } catch (error) {
    handleError(error);
  } finally {
    setLoading(false);
  }
};
```

### 3. Debounce Search Requests

```javascript
import { debounce } from 'lodash';

const debouncedSearch = debounce(async (query) => {
  const results = await service.search(query);
  setSearchResults(results.data);
}, 300);
```

### 4. Cancel Pending Requests

```javascript
useEffect(() => {
  const cancelToken = axios.CancelToken.source();
  
  fetchData(cancelToken.token);
  
  return () => {
    cancelToken.cancel("Component unmounted");
  };
}, []);
```

### 5. Cache Static Data

```javascript
// Use React Context or state management for country/major lists
const [countries, setCountries] = useState([]);

useEffect(() => {
  if (countries.length === 0) {
    fetchCountries(); // Only fetch if not already loaded
  }
}, []);
```

## Testing API Services

### Mock Service for Testing

```javascript
// src/services/__mocks__/product.js
export const getProducts = jest.fn(() => 
  Promise.resolve({
    data: [
      { id: 1, title: "Test Product" }
    ]
  })
);
```

### Test Example

```javascript
import { render, waitFor } from '@testing-library/react';
import { getProducts } from '../services/product';

jest.mock('../services/product');

test('loads products', async () => {
  getProducts.mockResolvedValue({
    data: [{ id: 1, title: "Test Product" }]
  });
  
  render(<ProductList />);
  
  await waitFor(() => {
    expect(screen.getByText('Test Product')).toBeInTheDocument();
  });
});
```

---

## Additional Resources

- [Axios Documentation](https://axios-http.com/)
- [React Query](https://tanstack.com/query/latest) - Consider for advanced data fetching
- [SWR](https://swr.vercel.app/) - Alternative data fetching library

For frontend implementation details, see [README.md](./README.md).
For product features, see [PRODUCT.md](./PRODUCT.md).
