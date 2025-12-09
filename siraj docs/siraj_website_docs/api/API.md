# API Documentation

This document describes the integration between the Siraj frontend and backend API.

## Table of Contents

1. [API Overview](#api-overview)
2. [Authentication](#authentication)
3. [API Endpoints](#api-endpoints)
4. [Request/Response Format](#requestresponse-format)
5. [Error Handling](#error-handling)
6. [Rate Limiting](#rate-limiting)
7. [Integration Examples](#integration-examples)

---

## API Overview

### Base URL

The API base URL is configured via environment variables:

- **Development:** `http://localhost:3001/api`
- **Staging:** `https://staging-api.siraj.app/api`
- **Production:** `https://api.siraj.app/api`

### API Version

Current API version: **v1** (implicit in base URL)

### Content Type

All requests and responses use `application/json` content type.

### HTTP Methods

- **GET** - Retrieve resources
- **POST** - Create resources
- **PUT** - Update resources (full update)
- **PATCH** - Update resources (partial update)
- **DELETE** - Delete resources

---

## Authentication

### WhatsApp OTP Authentication

Siraj uses WhatsApp OTP (One-Time Password) for authentication.

#### Authentication Flow

```
1. Request OTP
   POST /api/auth/request-otp
   
2. Verify OTP
   POST /api/auth/verify-otp
   
3. Receive JWT Token
   Use token for authenticated requests
   
4. Refresh Token (if expired)
   POST /api/auth/refresh-token
```

#### Token Usage

Include the JWT token in the Authorization header:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### Token Expiration

- **Access Token:** Valid for 7 days
- **Refresh Token:** Valid for 30 days

---

## API Endpoints

### Authentication

#### Request OTP

Request an OTP code to be sent via WhatsApp.

**Endpoint:** `POST /api/auth/request-otp`

**Request Body:**
```json
{
  "phone": "+962791234567",
  "countryCode": "+962"
}
```

**Response:**
```json
{
  "success": true,
  "message": "OTP sent successfully",
  "expiresIn": 300
}
```

**Error Response:**
```json
{
  "success": false,
  "error": "Too many attempts. Please try again in 2 minutes.",
  "code": "RATE_LIMIT_EXCEEDED"
}
```

---

#### Verify OTP

Verify the OTP code and receive authentication token.

**Endpoint:** `POST /api/auth/verify-otp`

**Request Body:**
```json
{
  "phone": "+962791234567",
  "otp": "123456"
}
```

**Success Response:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user123",
    "phone": "+962791234567",
    "name": "Ahmad Hassan",
    "email": "ahmad@example.com",
    "profileComplete": true,
    "hasCompletedMBTI": true
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": "Invalid OTP code",
  "code": "INVALID_OTP"
}
```

---

#### Refresh Token

Refresh an expired access token.

**Endpoint:** `POST /api/auth/refresh-token`

**Request Body:**
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response:**
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiresIn": 604800
}
```

---

### User Profile

#### Get User Profile

Retrieve the authenticated user's profile.

**Endpoint:** `GET /api/users/profile`

**Headers:**
```http
Authorization: Bearer {token}
```

**Response:**
```json
{
  "id": "user123",
  "phone": "+962791234567",
  "name": "Ahmad Hassan",
  "email": "ahmad@example.com",
  "age": 17,
  "gender": "male",
  "educationLevel": "high_school",
  "profileComplete": true,
  "hasCompletedMBTI": true,
  "personalityType": "INTJ",
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-20T14:45:00Z"
}
```

---

#### Update User Profile

Update the authenticated user's profile.

**Endpoint:** `PATCH /api/users/profile`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "name": "Ahmad Hassan",
  "email": "ahmad@example.com",
  "age": 17,
  "gender": "male",
  "educationLevel": "high_school"
}
```

**Response:**
```json
{
  "success": true,
  "user": {
    "id": "user123",
    "name": "Ahmad Hassan",
    "email": "ahmad@example.com",
    "age": 17,
    "gender": "male",
    "educationLevel": "high_school",
    "profileComplete": true,
    "updatedAt": "2024-01-20T15:00:00Z"
  }
}
```

---

### MBTI Test

#### Get Test Questions

Retrieve MBTI test questions.

**Endpoint:** `GET /api/mbti/questions`

**Headers:**
```http
Authorization: Bearer {token}
```

**Query Parameters:**
- `locale` (optional): Language code (`en` or `ar`)

**Response:**
```json
{
  "questions": [
    {
      "id": "q1",
      "text": "You are the person who...",
      "options": [
        {
          "id": "opt1",
          "text": "Prefers to plan ahead",
          "dimension": "J",
          "weight": 1
        },
        {
          "id": "opt2",
          "text": "Likes to keep options open",
          "dimension": "P",
          "weight": 1
        }
      ]
    }
    // ... more questions
  ],
  "totalQuestions": 60
}
```

---

#### Submit Test Answers

Submit MBTI test answers and get results.

**Endpoint:** `POST /api/mbti/submit`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "answers": [
    {
      "questionId": "q1",
      "optionId": "opt1"
    },
    {
      "questionId": "q2",
      "optionId": "opt2"
    }
    // ... all answers
  ]
}
```

**Response:**
```json
{
  "success": true,
  "result": {
    "personalityType": "INTJ",
    "typeName": "The Architect",
    "description": "Imaginative and strategic thinkers with a plan for everything.",
    "traits": {
      "introversion": 75,
      "intuition": 68,
      "thinking": 82,
      "judging": 71
    },
    "coreValues": [
      "Knowledge",
      "Competence",
      "Independence"
    ],
    "perceivedBy": [
      "Analytical",
      "Strategic",
      "Independent"
    ],
    "suggestedMajors": [
      {
        "id": "major1",
        "name": "Computer Science",
        "description": "Study of computation and information processing"
      }
      // ... more majors
    ],
    "careerPaths": [
      {
        "id": "career1",
        "name": "Software Engineer",
        "description": "Design and develop software systems"
      }
      // ... more careers
    ],
    "completedAt": "2024-01-20T15:30:00Z"
  }
}
```

---

#### Get Test Results

Retrieve saved MBTI test results.

**Endpoint:** `GET /api/mbti/results`

**Headers:**
```http
Authorization: Bearer {token}
```

**Response:**
```json
{
  "personalityType": "INTJ",
  "typeName": "The Architect",
  "description": "Imaginative and strategic thinkers with a plan for everything.",
  "traits": {
    "introversion": 75,
    "intuition": 68,
    "thinking": 82,
    "judging": 71
  },
  "suggestedMajors": [...],
  "careerPaths": [...],
  "completedAt": "2024-01-20T15:30:00Z"
}
```

---

#### Request Test Retake

Request permission to retake the MBTI test.

**Endpoint:** `POST /api/mbti/retake-request`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "reason": "I feel the results don't reflect my true personality"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Retake request submitted successfully",
  "requestId": "req123",
  "status": "pending"
}
```

---

#### Send Results to Email

Send MBTI results to user's email.

**Endpoint:** `POST /api/mbti/send-results`

**Headers:**
```http
Authorization: Bearer {token}
```

**Response:**
```json
{
  "success": true,
  "message": "Results sent to your email successfully"
}
```

---

### Counseling Sessions

#### Get Available Plans

Retrieve available counseling session plans.

**Endpoint:** `GET /api/plans`

**Headers:**
```http
Authorization: Bearer {token}
```

**Response:**
```json
{
  "plans": [
    {
      "id": "plan1",
      "name": "Starter Pack",
      "description": "Get started with 3 counseling sessions",
      "sessions": 3,
      "price": 99,
      "currency": "USD",
      "features": [
        "3 one-on-one sessions",
        "Personality analysis",
        "Career recommendations"
      ],
      "duration": 30,
      "popular": false
    },
    {
      "id": "plan2",
      "name": "Premium Pack",
      "description": "Comprehensive guidance with 10 sessions",
      "sessions": 10,
      "price": 299,
      "currency": "USD",
      "features": [
        "10 one-on-one sessions",
        "Unlimited major recommendations",
        "Priority booking",
        "Email support"
      ],
      "duration": 90,
      "popular": true
    }
  ]
}
```

---

#### Purchase Plan

Purchase a counseling session plan.

**Endpoint:** `POST /api/plans/purchase`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "planId": "plan2",
  "paymentMethod": "credit_card",
  "paymentDetails": {
    "cardNumber": "4111111111111111",
    "expiryMonth": "12",
    "expiryYear": "2025",
    "cvv": "123"
  }
}
```

**Response:**
```json
{
  "success": true,
  "orderId": "order123",
  "sessions": 10,
  "expiresAt": "2024-04-20T15:30:00Z",
  "message": "Purchase successful"
}
```

---

#### Get Available Advisors

Retrieve list of available career advisors.

**Endpoint:** `GET /api/advisors`

**Headers:**
```http
Authorization: Bearer {token}
```

**Query Parameters:**
- `specialty` (optional): Filter by specialty
- `language` (optional): Filter by language (`en`, `ar`)

**Response:**
```json
{
  "advisors": [
    {
      "id": "advisor1",
      "name": "Dr. Sarah Ahmad",
      "title": "Career Counselor",
      "bio": "10+ years of experience in career guidance",
      "specialty": ["Technology", "Engineering"],
      "languages": ["en", "ar"],
      "rating": 4.8,
      "totalSessions": 250,
      "availability": [
        {
          "date": "2024-01-25",
          "slots": [
            {
              "time": "10:00",
              "available": true
            },
            {
              "time": "14:00",
              "available": false
            }
          ]
        }
      ]
    }
  ]
}
```

---

#### Book Session

Book a counseling session with an advisor.

**Endpoint:** `POST /api/bookings`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "advisorId": "advisor1",
  "date": "2024-01-25",
  "time": "10:00",
  "type": "counseling",
  "notes": "I need help choosing between computer science and engineering"
}
```

**Response:**
```json
{
  "success": true,
  "booking": {
    "id": "booking123",
    "advisorId": "advisor1",
    "advisorName": "Dr. Sarah Ahmad",
    "date": "2024-01-25",
    "time": "10:00",
    "duration": 60,
    "type": "counseling",
    "status": "confirmed",
    "meetingLink": "https://meet.siraj.app/session/123",
    "notes": "I need help choosing between computer science and engineering"
  }
}
```

---

#### Get My Bookings

Retrieve user's bookings.

**Endpoint:** `GET /api/bookings/my-bookings`

**Headers:**
```http
Authorization: Bearer {token}
```

**Query Parameters:**
- `status` (optional): Filter by status (`upcoming`, `completed`, `cancelled`)

**Response:**
```json
{
  "bookings": [
    {
      "id": "booking123",
      "advisorName": "Dr. Sarah Ahmad",
      "date": "2024-01-25",
      "time": "10:00",
      "duration": 60,
      "status": "confirmed",
      "meetingLink": "https://meet.siraj.app/session/123"
    }
  ],
  "remainingSessions": 7
}
```

---

### Universities & Programs

#### Search Universities

Search universities in the database.

**Endpoint:** `GET /api/universities`

**Headers:**
```http
Authorization: Bearer {token}
```

**Query Parameters:**
- `country` (optional): Filter by country
- `major` (optional): Filter by available major
- `page` (optional): Page number (default: 1)
- `limit` (optional): Results per page (default: 20)

**Response:**
```json
{
  "universities": [
    {
      "id": "uni1",
      "name": "University of Jordan",
      "country": "Jordan",
      "city": "Amman",
      "ranking": 450,
      "programs": 120,
      "tuitionRange": {
        "min": 2000,
        "max": 8000,
        "currency": "USD"
      }
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "pages": 8
  }
}
```

---

#### Get University Details

Get detailed information about a specific university.

**Endpoint:** `GET /api/universities/:id`

**Headers:**
```http
Authorization: Bearer {token}
```

**Response:**
```json
{
  "id": "uni1",
  "name": "University of Jordan",
  "country": "Jordan",
  "city": "Amman",
  "established": 1962,
  "ranking": {
    "global": 450,
    "regional": 15
  },
  "description": "Leading university in Jordan...",
  "website": "https://ju.edu.jo",
  "email": "admission@ju.edu.jo",
  "phone": "+96265355000",
  "programs": [
    {
      "id": "prog1",
      "name": "Computer Science",
      "degree": "Bachelor",
      "duration": 4,
      "tuition": 3500,
      "currency": "USD",
      "requirements": {
        "gpa": 75,
        "tests": ["SAT", "TOEFL"]
      }
    }
  ]
}
```

---

### Trial Programs

#### Get Available Trials

Get available VR experiences and job trials.

**Endpoint:** `GET /api/trials`

**Headers:**
```http
Authorization: Bearer {token}
```

**Query Parameters:**
- `type` (optional): Filter by type (`vr`, `job`)
- `category` (optional): Filter by career category

**Response:**
```json
{
  "trials": [
    {
      "id": "trial1",
      "name": "Software Developer VR Experience",
      "type": "vr",
      "category": "Technology",
      "description": "Experience a day in the life of a software developer",
      "duration": 30,
      "location": "Siraj VR Lab - Amman",
      "availability": [
        {
          "date": "2024-01-26",
          "slots": ["10:00", "14:00", "16:00"]
        }
      ]
    },
    {
      "id": "trial2",
      "name": "Marketing Internship",
      "type": "job",
      "category": "Business",
      "company": "ABC Marketing Agency",
      "description": "2-day marketing trial at our office",
      "duration": 16,
      "location": "ABC Office - Amman"
    }
  ]
}
```

---

#### Book Trial

Book a trial program.

**Endpoint:** `POST /api/trials/book`

**Headers:**
```http
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "trialId": "trial1",
  "date": "2024-01-26",
  "time": "10:00"
}
```

**Response:**
```json
{
  "success": true,
  "booking": {
    "id": "trial-booking123",
    "trialId": "trial1",
    "trialName": "Software Developer VR Experience",
    "date": "2024-01-26",
    "time": "10:00",
    "location": "Siraj VR Lab - Amman",
    "status": "confirmed"
  }
}
```

---

## Request/Response Format

### Standard Request Format

```http
POST /api/endpoint HTTP/1.1
Host: api.siraj.app
Content-Type: application/json
Authorization: Bearer {token}

{
  "field1": "value1",
  "field2": "value2"
}
```

### Standard Success Response

```json
{
  "success": true,
  "data": {
    // Response data
  },
  "message": "Operation completed successfully"
}
```

### Standard Error Response

```json
{
  "success": false,
  "error": "Human-readable error message",
  "code": "ERROR_CODE",
  "details": {
    // Additional error details (optional)
  }
}
```

---

## Error Handling

### HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid request data |
| 401 | Unauthorized | Authentication required or failed |
| 403 | Forbidden | Access denied |
| 404 | Not Found | Resource not found |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |
| 503 | Service Unavailable | Service temporarily unavailable |

### Error Codes

| Code | Description |
|------|-------------|
| `INVALID_CREDENTIALS` | Invalid login credentials |
| `INVALID_OTP` | Invalid OTP code |
| `OTP_EXPIRED` | OTP code has expired |
| `RATE_LIMIT_EXCEEDED` | Too many requests |
| `PROFILE_INCOMPLETE` | User profile not complete |
| `TEST_REQUIRED` | MBTI test not completed |
| `INSUFFICIENT_SESSIONS` | No counseling sessions available |
| `BOOKING_CONFLICT` | Time slot already booked |
| `PAYMENT_FAILED` | Payment processing failed |

---

## Rate Limiting

### Limits

- **OTP Requests:** 5 per phone number per hour
- **API Requests:** 100 per minute per user
- **File Uploads:** 10 per hour per user

### Rate Limit Headers

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

### Rate Limit Exceeded Response

```json
{
  "success": false,
  "error": "Rate limit exceeded",
  "code": "RATE_LIMIT_EXCEEDED",
  "retryAfter": 120
}
```

---

## Integration Examples

### Example: Complete Authentication Flow

```typescript
// 1. Request OTP
const requestOTP = async (phone: string) => {
  const response = await axios.post('/api/auth/request-otp', {
    phone: phone
  });
  return response.data;
};

// 2. Verify OTP
const verifyOTP = async (phone: string, otp: string) => {
  const response = await axios.post('/api/auth/verify-otp', {
    phone: phone,
    otp: otp
  });
  
  // Store token
  localStorage.setItem('authToken', response.data.token);
  localStorage.setItem('refreshToken', response.data.refreshToken);
  
  return response.data.user;
};

// 3. Make authenticated request
const getProfile = async () => {
  const token = localStorage.getItem('authToken');
  
  const response = await axios.get('/api/users/profile', {
    headers: {
      'Authorization': `Bearer ${token}`
    }
  });
  
  return response.data;
};
```

### Example: MBTI Test Flow

```typescript
// 1. Get test questions
const getQuestions = async () => {
  const response = await axiosInstance.get('/api/mbti/questions');
  return response.data.questions;
};

// 2. Submit answers
const submitTest = async (answers: Answer[]) => {
  const response = await axiosInstance.post('/api/mbti/submit', {
    answers: answers
  });
  return response.data.result;
};

// 3. Get saved results
const getResults = async () => {
  const response = await axiosInstance.get('/api/mbti/results');
  return response.data;
};
```

### Example: Error Handling

```typescript
try {
  const response = await axiosInstance.post('/api/bookings', bookingData);
  // Handle success
} catch (error) {
  if (axios.isAxiosError(error)) {
    const errorData = error.response?.data;
    
    switch (errorData?.code) {
      case 'PROFILE_INCOMPLETE':
        // Redirect to profile completion
        router.push('/profile/edit');
        break;
      case 'TEST_REQUIRED':
        // Redirect to MBTI test
        router.push('/test/mbti');
        break;
      case 'INSUFFICIENT_SESSIONS':
        // Redirect to plans page
        router.push('/choose-your-plan');
        break;
      default:
        // Show generic error
        showError(errorData?.error || 'An error occurred');
    }
  }
}
```

---

**For Backend API Development:**

- Contact backend team for implementation details
- API documentation should be kept in sync with backend changes
- Use API versioning for breaking changes

---

*Last updated: January 2025*
