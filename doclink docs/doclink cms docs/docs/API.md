# API Documentation

## Overview

DocLink CMS communicates with a RESTful backend API for all data operations. This document provides an overview of the API structure, authentication, and available endpoints.

## Base Configuration

The API client is configured using Axios with the following features:

- **Base URL**: Configured via environment variables
- **Authentication**: JWT token-based authentication
- **Request Interceptors**: Automatic token injection
- **Response Interceptors**: Error handling and loading state management
- **Timeout**: Configurable request timeout
- **Content-Type**: application/json (default)

## Authentication

### Authentication Flow

1. **Login**: POST credentials to `/auth/login`
2. **Receive Token**: Backend returns JWT token
3. **Store Token**: Save token in Redux store and localStorage
4. **Automatic Injection**: Axios interceptor adds token to all requests
5. **Token Refresh**: Handle token expiration and refresh

### Authentication Endpoints

#### Login
```
POST /auth/login
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword"
}
```

**Response:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user_id",
    "email": "user@example.com",
    "role": "admin",
    "permissions": []
  }
}
```

#### Logout
```
POST /auth/logout
```

#### Forgot Password - Email Verification
```
POST /forget_password/verify_email
```

**Request Body:**
```json
{
  "email": "user@example.com"
}
```

#### Forgot Password - OTP Verification
```
POST /forget_password/verify_otp
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "otp": "123456"
}
```

#### Forgot Password - Change Password
```
POST /forget_password/change_password
```

**Request Body:**
```json
{
  "email": "user@example.com",
  "otp": "123456",
  "newPassword": "newSecurePassword"
}
```

#### Resend OTP
```
POST /forget_password/resend_otp
```

#### Change Password (Authenticated)
```
POST /auth/change_password
```

**Request Body:**
```json
{
  "currentPassword": "oldPassword",
  "newPassword": "newPassword"
}
```

## Doctor Management API

### Doctor Profiles

#### Get All Doctors
```
GET /doctor/get_all_doctor
```

**Query Parameters:**
- `page`: Page number (optional)
- `limit`: Items per page (optional)
- `search`: Search term (optional)

**Response:**
```json
{
  "success": true,
  "response": {
    "doctors": [...],
    "total": 100,
    "page": 1,
    "limit": 10
  }
}
```

#### Create Doctor
```
POST /doctor/add_new_doctor
```

**Request Body:** (Multipart/form-data)
```json
{
  "name": "Dr. John Doe",
  "email": "doctor@example.com",
  "phone": "+1234567890",
  "specialization": "Cardiology",
  "experience": 10,
  "qualifications": "MBBS, MD",
  "profileImage": "[File]",
  "documents": "[Files]"
}
```

#### Update Doctor
```
PUT /doctor/update_new_doctor
```

#### Delete Doctor
```
DELETE /doctor/delete_doctor/:id
```

#### View Onboarded Doctors
```
GET /doctor/view_all_onboard_doctors
```

#### View Active/Inactive Doctors
```
GET /doctor/all_active_inactive_doctors
```

#### View Pending/Rejected Doctors
```
GET /doctor/pending_rejected_doctor
```

#### View Flagged Doctors
```
GET /doctor/view_flagged_doctors
```

#### Flag/Unflag Doctor
```
POST /doctor/flagged_unflagged_doctor
```

### Doctor Specializations

#### Get All Specializations
```
GET /doctor/get_specializations
```

#### Get All Specializations (No Pagination)
```
GET /doctor/get_all_specializations
```

#### Create Specialization
```
POST /doctor/add_specialization
```

**Request Body:**
```json
{
  "name": "Cardiology",
  "description": "Heart and cardiovascular system",
  "icon": "[File]"
}
```

#### Update Specialization
```
PUT /doctor/edit_specialization
```

#### Delete Specialization
```
DELETE /doctor/delete_specialization/:id
```

### Disease Management

#### View All Diseases
```
GET /disease/view_disease
```

#### View Diseases (No Pagination)
```
GET /disease/view_disease_without_pagination
```

#### Create Disease
```
POST /disease/add_disease
```

#### Update Disease
```
PUT /disease/edit_disease
```

#### Delete Disease
```
DELETE /disease/delete_disease/:id
```

### Health Concerns

#### View All Health Concerns
```
GET /health_concern/view_health_concern
```

#### View Health Concerns (No Pagination)
```
GET /health_concern/view_health_concern_without_pagination
```

#### Create Health Concern
```
POST /health_concern/add_health_concern
```

#### Update Health Concern
```
PUT /health_concern/edit_health_concern
```

#### Delete Health Concern
```
DELETE /health_concern/delete_health/:id
```

### Doctor Subscriptions

#### View Subscriptions
```
GET /subscription/view_subscription
```

#### Create Subscription
```
POST /subscription/add_subscription
```

#### Update Subscription
```
PUT /subscription/edit_subscription
```

#### Delete Subscription
```
DELETE /subscription/delete_subscription/:id
```

### Doctor Connections

#### View Connections
```
GET /doctor/view_connections
```

### Reviews & Ratings

#### View Reviews
```
GET /doctor/view_reviews
```

#### Moderate Review
```
PUT /doctor/moderate_review
```

## Patient Management API

### Patient Profiles

#### Get All Patients
```
GET /patient/get_all_patients
```

#### Get Patient Details
```
GET /patient/get_patient/:id
```

#### Update Patient
```
PUT /patient/update_patient
```

#### Delete Patient
```
DELETE /patient/delete_patient/:id
```

## Lab Management API

### Lab Profiles

#### View All Labs
```
GET /lab/view_lab
```

#### Create Lab
```
POST /lab/add_lab
```

**Request Body:**
```json
{
  "name": "Lab Name",
  "address": "Lab Address",
  "phone": "+1234567890",
  "email": "lab@example.com",
  "services": ["service1", "service2"]
}
```

#### Update Lab
```
PUT /lab/edit_lab
```

#### Delete Lab
```
DELETE /lab/delete_lab/:id
```

### Lab Service Categories

#### View Lab Service Categories
```
GET /lab/parent_category/view
```

#### Add Service Category
```
POST /lab/parent_category/add
```

#### Edit Service Category
```
PUT /lab/parent_category/edit
```

#### Delete Service Category
```
DELETE /lab/parent_category/delete/:id
```

### Lab Test Categories

#### View Lab Test Categories
```
GET /lab/child_category/view
```

#### Add Test Category
```
POST /lab/child_category/add
```

#### Edit Test Category
```
PUT /lab/child_category/edit
```

#### Delete Test Category
```
DELETE /lab/child_category/delete/:id
```

## Content Management API

### Blogs

#### View All Blogs
```
GET /blog/view_blogs
```

#### Create Blog
```
POST /blog/add_blog
```

**Request Body:**
```json
{
  "title": "Blog Title",
  "category": "category_id",
  "content": "<p>Blog content in HTML</p>",
  "author": "author_name",
  "featuredImage": "[File]",
  "tags": ["tag1", "tag2"],
  "status": "published"
}
```

#### Update Blog
```
PUT /blog/edit_blog
```

#### Delete Blog
```
DELETE /blog/delete_blog/:id
```

#### Get Blog by ID
```
GET /blog/get_blog/:id
```

### Blog Categories

#### View Categories
```
GET /blog/view_categories
```

#### Create Category
```
POST /blog/add_category
```

#### Update Category
```
PUT /blog/edit_category
```

#### Delete Category
```
DELETE /blog/delete_category/:id
```

### Health Tips

#### View Health Tips
```
GET /health_tips/view
```

#### Create Health Tip
```
POST /health_tips/add
```

#### Update Health Tip
```
PUT /health_tips/edit
```

#### Delete Health Tip
```
DELETE /health_tips/delete/:id
```

### Banners

#### View Banners
```
GET /banner/view
```

#### Create Banner
```
POST /banner/add
```

**Request Body:** (Multipart/form-data)
```json
{
  "title": "Banner Title",
  "image": "[File]",
  "link": "https://example.com",
  "screenId": "screen_id",
  "position": 1,
  "isActive": true
}
```

#### Update Banner
```
PUT /banner/edit
```

#### Delete Banner
```
DELETE /banner/delete/:id
```

### Screens

#### View Screens
```
GET /screens/view
```

#### Create Screen
```
POST /screens/add
```

#### Update Screen
```
PUT /screens/edit
```

#### Delete Screen
```
DELETE /screens/delete/:id
```

### Short Messages

#### View Short Messages
```
GET /short_message/view
```

#### Create Short Message
```
POST /short_message/add
```

#### Update Short Message
```
PUT /short_message/edit
```

#### Delete Short Message
```
DELETE /short_message/delete/:id
```

### Short Stories

#### View Short Stories
```
GET /short_stories/view
```

#### Create Short Story
```
POST /short_stories/add
```

#### Update Short Story
```
PUT /short_stories/edit
```

#### Delete Short Story
```
DELETE /short_stories/delete/:id
```

### Doctor Directory

#### View Directory
```
GET /doctor_directory/view
```

#### Create Directory Entry
```
POST /doctor_directory/add
```

#### Update Directory Entry
```
PUT /doctor_directory/edit
```

#### Delete Directory Entry
```
DELETE /doctor_directory/delete/:id
```

## Support & Communication API

### Support Team

#### View Support Team
```
GET /support_team/view
```

#### Create Team Member
```
POST /support_team/add
```

#### Update Team Member
```
PUT /support_team/edit
```

#### Delete Team Member
```
DELETE /support_team/delete/:id
```

### Support Team Status

#### View Status Types
```
GET /support_team_status/view
```

#### Create Status Type
```
POST /support_team_status/add
```

#### Update Status Type
```
PUT /support_team_status/edit
```

#### Delete Status Type
```
DELETE /support_team_status/delete/:id
```

### Video Call Packages

#### View Packages
```
GET /video_call_packages/view
```

#### Create Package
```
POST /video_call_packages/add
```

#### Update Package
```
PUT /video_call_packages/edit
```

#### Delete Package
```
DELETE /video_call_packages/delete/:id
```

## Search & Filter API

### Search Filters

#### View Filters
```
GET /search_filters/view
```

#### Create Filter
```
POST /search_filters/add
```

#### Update Filter
```
PUT /search_filters/edit
```

#### Delete Filter
```
DELETE /search_filters/delete/:id
```

## Policy Management API

### Terms & Conditions

#### View Terms
```
GET /policies/terms/view
```

#### Update Terms
```
PUT /policies/terms/update
```

### Payout Policies

#### View Payout Policies Master
```
GET /policies/payout_policies/master/view
```

#### Create Payout Policy
```
POST /policies/payout_policies/master/add
```

#### Update Payout Policy
```
PUT /policies/payout_policies/master/edit
```

#### Delete Payout Policy
```
DELETE /policies/payout_policies/master/delete/:id
```

#### View Payout Policy Requests
```
GET /policies/payout_policies/requests/view
```

#### Approve/Reject Request
```
PUT /policies/payout_policies/requests/action
```

## Settings & Role Management API

### Role Management

#### View Roles
```
GET /roles/view
```

#### Create Role
```
POST /roles/add
```

#### Update Role
```
PUT /roles/edit
```

#### Delete Role
```
DELETE /roles/delete/:id
```

### Permissions

#### View Permissions
```
GET /permissions/view
```

#### Update Permissions
```
PUT /permissions/update
```

### Module Management

#### View Modules
```
GET /modules/view
```

#### Create Module
```
POST /modules/add
```

#### Update Module
```
PUT /modules/edit
```

#### Delete Module
```
DELETE /modules/delete/:id
```

### User Management

#### Add User
```
POST /users/add
```

**Request Body:**
```json
{
  "name": "User Name",
  "email": "user@example.com",
  "role": "role_id",
  "permissions": []
}
```

## API Response Format

### Success Response
```json
{
  "success": true,
  "message": "Operation successful",
  "response": {
    // Response data
  }
}
```

### Error Response
```json
{
  "success": false,
  "message": "Error message",
  "error": {
    "code": "ERROR_CODE",
    "details": "Detailed error information"
  }
}
```

### Pagination Response
```json
{
  "success": true,
  "response": {
    "data": [...],
    "pagination": {
      "total": 100,
      "page": 1,
      "limit": 10,
      "totalPages": 10
    }
  }
}
```

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Bad Request - Invalid input |
| 401 | Unauthorized - Authentication required |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource doesn't exist |
| 409 | Conflict - Resource already exists |
| 422 | Unprocessable Entity - Validation failed |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

## Rate Limiting

The API implements rate limiting to prevent abuse:

- **Rate Limit**: 1000 requests per hour per IP
- **Headers**: 
  - `X-RateLimit-Limit`: Total requests allowed
  - `X-RateLimit-Remaining`: Requests remaining
  - `X-RateLimit-Reset`: Time when limit resets

## File Upload

### Multipart Form Data

For endpoints that accept file uploads:

```javascript
const formData = new FormData();
formData.append('file', fileObject);
formData.append('name', 'File Name');

// Send request
await Api.post('/endpoint', formData, {
  headers: {
    'Content-Type': 'multipart/form-data'
  }
});
```

### File Types Supported

- **Images**: JPG, PNG, GIF, WEBP
- **Documents**: PDF, DOC, DOCX
- **Maximum Size**: 10MB per file

## Best Practices

### 1. Error Handling
```javascript
try {
  const response = await Api.get('/endpoint');
  // Handle success
} catch (error) {
  if (error.response) {
    // Server responded with error
    console.error(error.response.data.message);
  } else if (error.request) {
    // No response received
    console.error('Network error');
  } else {
    // Request setup error
    console.error('Request failed');
  }
}
```

### 2. Loading States
```javascript
dispatch(setLoading(true));
try {
  const response = await Api.get('/endpoint');
  // Process response
} finally {
  dispatch(setLoading(false));
}
```

### 3. Token Management
```javascript
// Token is automatically added by interceptor
// No need to manually add Authorization header

// Token refresh (if needed)
Api.interceptors.response.use(
  response => response,
  async error => {
    if (error.response?.status === 401) {
      // Token expired, refresh or logout
    }
    return Promise.reject(error);
  }
);
```

### 4. Request Cancellation
```javascript
const source = axios.CancelToken.source();

Api.get('/endpoint', {
  cancelToken: source.token
});

// Cancel request if needed
source.cancel('Operation canceled');
```

## API Client Configuration

### Environment Variables
```env
REACT_APP_API_BASE_URL=https://api.doclink.com/v1
REACT_APP_API_TIMEOUT=30000
```

### Axios Instance Setup
```javascript
import axios from 'axios';

const Api = axios.create({
  baseURL: process.env.REACT_APP_API_BASE_URL,
  timeout: process.env.REACT_APP_API_TIMEOUT,
  headers: {
    'Content-Type': 'application/json'
  }
});

// Request interceptor
Api.interceptors.request.use(
  config => {
    const token = getToken();
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  error => Promise.reject(error)
);

// Response interceptor
Api.interceptors.response.use(
  response => response,
  error => {
    // Handle errors globally
    return Promise.reject(error);
  }
);

export default Api;
```

---

For backend API implementation details, please contact the backend development team.
