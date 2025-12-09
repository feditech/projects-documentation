# API Documentation

This document provides comprehensive information about the DocLink API endpoints and their usage.

## Overview

The DocLink API provides programmatic access to various features of the platform. The API follows RESTful principles and returns JSON responses.

## Base URL

```
# Development
http://localhost:3000/api

# Production
https://api.doclink.com (or configured base URL)
```

## API Endpoint Structure

API endpoints are defined in `restApis/API_ENDPOINTS.js`:

```javascript
export const API_ENDPOINTS = {
  // blogsCategory
  blogsCategory: {
    getAll: "/blogs/viewBlogsCategory",
    getBlogViaCategory: "/blogs/blogsViaCategory",
    getPopularBlogs: "/blogs/popularPosts",
  },
  // contact us form
  contactUs: {
    contactUsForm: "/contactUs/contactUsForm",
  },
};
```

## Authentication

### API Key Authentication
```http
Authorization: Bearer YOUR_API_KEY
```

### Session-Based Authentication
For web application users, authentication is handled through secure session cookies.

## Common Headers

All API requests should include:

```http
Content-Type: application/json
Accept: application/json
Authorization: Bearer YOUR_API_KEY
```

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {
    // Response data
  },
  "message": "Operation successful"
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description"
  }
}
```

## Status Codes

| Code | Description |
|------|-------------|
| 200 | OK - Request successful |
| 201 | Created - Resource created successfully |
| 400 | Bad Request - Invalid request parameters |
| 401 | Unauthorized - Authentication required |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 500 | Internal Server Error - Server error |
| 503 | Service Unavailable - Service temporarily unavailable |

---

## Blogs API

### Get All Blog Categories

Retrieve all available blog categories.

**Endpoint:** `GET /blogs/viewBlogsCategory`

**Request:**
```http
GET /blogs/viewBlogsCategory
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "1",
      "name": "Health Tips",
      "slug": "health-tips",
      "description": "General health tips and advice",
      "postCount": 25
    },
    {
      "id": "2",
      "name": "Nutrition",
      "slug": "nutrition",
      "description": "Diet and nutrition information",
      "postCount": 18
    }
  ]
}
```

---

### Get Blogs by Category

Retrieve blogs filtered by category.

**Endpoint:** `GET /blogs/blogsViaCategory`

**Query Parameters:**
- `categoryId` (required): Category ID
- `page` (optional): Page number (default: 1)
- `limit` (optional): Results per page (default: 10)

**Request:**
```http
GET /blogs/blogsViaCategory?categoryId=1&page=1&limit=10
```

**Response:**
```json
{
  "success": true,
  "data": {
    "blogs": [
      {
        "id": "101",
        "title": "10 Health Tips for Better Living",
        "slug": "10-health-tips-better-living",
        "excerpt": "Discover essential health tips...",
        "content": "Full blog content...",
        "author": {
          "name": "Dr. Ahmed Khan",
          "title": "General Physician"
        },
        "category": "Health Tips",
        "publishedAt": "2024-12-01T10:00:00Z",
        "readTime": "5 min",
        "featured": true,
        "imageUrl": "/assets/img/blogs/blog-101.jpg"
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 5,
      "totalBlogs": 48,
      "hasNext": true,
      "hasPrev": false
    }
  }
}
```

---

### Get Popular Blogs

Retrieve most popular blog posts.

**Endpoint:** `GET /blogs/popularPosts`

**Query Parameters:**
- `limit` (optional): Number of posts to return (default: 5)

**Request:**
```http
GET /blogs/popularPosts?limit=5
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "105",
      "title": "Understanding Diabetes Management",
      "slug": "understanding-diabetes-management",
      "excerpt": "Learn about diabetes...",
      "views": 1250,
      "likes": 340,
      "publishedAt": "2024-11-28T09:00:00Z",
      "imageUrl": "/assets/img/blogs/blog-105.jpg"
    }
  ]
}
```

---

## Contact Us API

### Submit Contact Form

Submit a contact form inquiry.

**Endpoint:** `POST /contactUs/contactUsForm`

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "phone": "+92-300-1234567",
  "subject": "General Inquiry",
  "message": "I would like to know more about subscription plans."
}
```

**Validation Rules:**
- `name`: Required, min 3 characters, max 100 characters
- `email`: Required, valid email format
- `phone`: Optional, valid phone format
- `subject`: Required, max 200 characters
- `message`: Required, min 10 characters, max 1000 characters

**Success Response:**
```json
{
  "success": true,
  "message": "Thank you for contacting us. We will respond within 24 hours.",
  "data": {
    "ticketId": "TICKET-12345",
    "submittedAt": "2024-12-06T15:30:00Z"
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": {
      "email": "Invalid email format"
    }
  }
}
```

---

## Subscription Plans API (Expected Structure)

### Get All Plans

**Endpoint:** `GET /subscriptions/plans`

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "plan-monthly",
      "name": "Monthly Plan",
      "price": 699,
      "currency": "PKR",
      "duration": "1 month",
      "features": [
        "Unlimited consultations",
        "24/7 doctor access",
        "Digital prescriptions",
        "Medical records storage"
      ],
      "discount": {
        "percentage": 50,
        "validUntil": "2024-12-31"
      }
    }
  ]
}
```

---

### Subscribe to Plan

**Endpoint:** `POST /subscriptions/subscribe`

**Request Body:**
```json
{
  "planId": "plan-monthly",
  "userId": "user-123",
  "paymentMethod": "card",
  "autoRenew": true
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "subscriptionId": "sub-789",
    "status": "active",
    "startDate": "2024-12-06",
    "endDate": "2025-01-06",
    "paymentStatus": "completed"
  }
}
```

---

## Doctors API (Expected Structure)

### Get Doctor Listings

**Endpoint:** `GET /doctors`

**Query Parameters:**
- `specialty`: Filter by specialty
- `location`: Filter by location
- `availability`: Filter by availability
- `page`: Page number
- `limit`: Results per page

**Response:**
```json
{
  "success": true,
  "data": {
    "doctors": [
      {
        "id": "doc-001",
        "name": "Dr. Fatima Ahmed",
        "specialty": "General Physician",
        "qualifications": ["MBBS", "FCPS"],
        "experience": 10,
        "rating": 4.8,
        "reviewCount": 156,
        "availability": "Available",
        "imageUrl": "/assets/img/doctors/doc-001.jpg"
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 10,
      "totalDoctors": 95
    }
  }
}
```

---

## Medical Records API (Expected Structure)

### Upload Medical Record

**Endpoint:** `POST /medical-records/upload`

**Request:** Multipart form data

**Fields:**
- `userId`: User ID
- `recordType`: Type of record (prescription, lab-report, scan, etc.)
- `file`: File upload
- `date`: Record date
- `notes`: Optional notes

**Response:**
```json
{
  "success": true,
  "data": {
    "recordId": "rec-456",
    "fileName": "lab-report-2024.pdf",
    "fileUrl": "/records/rec-456.pdf",
    "uploadedAt": "2024-12-06T16:00:00Z"
  }
}
```

---

### Get User Medical Records

**Endpoint:** `GET /medical-records/:userId`

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "recordId": "rec-456",
      "recordType": "lab-report",
      "fileName": "CBC Test Results",
      "date": "2024-11-15",
      "fileUrl": "/records/rec-456.pdf",
      "uploadedAt": "2024-11-16T10:00:00Z"
    }
  ]
}
```

---

## Lab Tests API (Expected Structure)

### Get Available Tests

**Endpoint:** `GET /lab-tests`

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "testId": "test-001",
      "name": "Complete Blood Count (CBC)",
      "category": "Blood Tests",
      "price": 500,
      "discountedPrice": 250,
      "description": "Measures blood cell counts",
      "preparationRequired": "8 hours fasting",
      "reportTime": "24 hours"
    }
  ]
}
```

---

### Book Lab Test

**Endpoint:** `POST /lab-tests/book`

**Request Body:**
```json
{
  "userId": "user-123",
  "testId": "test-001",
  "labId": "lab-001",
  "collectionType": "home",
  "preferredDate": "2024-12-08",
  "preferredTime": "09:00",
  "address": "123 Main Street, Karachi"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "bookingId": "book-789",
    "status": "confirmed",
    "scheduledAt": "2024-12-08T09:00:00Z",
    "confirmationCode": "LAB-12345"
  }
}
```

---

## Consultations API (Expected Structure)

### Book Consultation

**Endpoint:** `POST /consultations/book`

**Request Body:**
```json
{
  "userId": "user-123",
  "doctorId": "doc-001",
  "consultationType": "video",
  "preferredDate": "2024-12-07",
  "preferredTime": "14:00",
  "symptoms": "Fever and headache",
  "urgency": "normal"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "consultationId": "cons-456",
    "status": "scheduled",
    "scheduledAt": "2024-12-07T14:00:00Z",
    "meetingLink": "https://meet.doclink.com/cons-456"
  }
}
```

---

## Error Handling

### Common Error Codes

| Code | Description |
|------|-------------|
| `VALIDATION_ERROR` | Request validation failed |
| `AUTHENTICATION_REQUIRED` | User must be authenticated |
| `INSUFFICIENT_PERMISSIONS` | User lacks required permissions |
| `RESOURCE_NOT_FOUND` | Requested resource not found |
| `RATE_LIMIT_EXCEEDED` | Too many requests |
| `SUBSCRIPTION_REQUIRED` | Feature requires active subscription |
| `PAYMENT_FAILED` | Payment processing failed |
| `SERVER_ERROR` | Internal server error |

### Error Response Example

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": {
      "field": "email",
      "issue": "Invalid email format",
      "provided": "invalid-email"
    }
  }
}
```

---

## Rate Limiting

- **Free Users**: 100 requests per hour
- **Subscription Users**: 1000 requests per hour
- **API Partners**: Custom rate limits

### Rate Limit Headers

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1670345600
```

---

## Pagination

For endpoints that return lists, pagination is supported:

**Query Parameters:**
- `page`: Page number (default: 1)
- `limit`: Results per page (default: 10, max: 100)

**Response includes pagination metadata:**
```json
{
  "pagination": {
    "currentPage": 1,
    "totalPages": 10,
    "totalItems": 100,
    "hasNext": true,
    "hasPrev": false
  }
}
```

---

## Webhooks

DocLink can send webhook notifications for various events.

### Available Events
- `subscription.created`
- `subscription.renewed`
- `subscription.cancelled`
- `consultation.booked`
- `consultation.completed`
- `lab-test.booked`
- `lab-test.completed`
- `payment.succeeded`
- `payment.failed`

### Webhook Payload Format
```json
{
  "event": "subscription.created",
  "timestamp": "2024-12-06T16:00:00Z",
  "data": {
    "subscriptionId": "sub-789",
    "userId": "user-123",
    "planId": "plan-monthly"
  }
}
```

---

## SDK & Client Libraries

### JavaScript/Node.js
```javascript
import { DoclinkAPI } from '@doclink/api-client';

const client = new DoclinkAPI({
  apiKey: 'YOUR_API_KEY',
  baseURL: 'https://api.doclink.com'
});

// Example usage
const blogs = await client.blogs.getPopular({ limit: 5 });
```

### Usage with Axios (Current Implementation)
```javascript
import axios from 'axios';
import { API_ENDPOINTS } from './restApis/API_ENDPOINTS';

const response = await axios.get(
  `${baseURL}${API_ENDPOINTS.blogsCategory.getAll}`
);
```

---

## API Versioning

Current API version: `v1`

Version is included in the URL:
```
https://api.doclink.com/v1/blogs/popularPosts
```

---

## Testing

### Test Environment
```
https://api-staging.doclink.com
```

### Test Credentials
Contact development team for test API keys.

---

## Support

For API support:
- **Email**: api-support@doclink.com
- **Documentation**: https://docs.doclink.com
- **Status Page**: https://status.doclink.com

---

## Related Documentation

- [Getting Started](./GETTING_STARTED.md) - Setup guide
- [Architecture](./ARCHITECTURE.md) - Technical architecture
- [Development](./DEVELOPMENT.md) - Development workflow
- [Features](./FEATURES.md) - Feature documentation
