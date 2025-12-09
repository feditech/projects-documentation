# System Architecture

Technical architecture documentation for the Siraj Career Guidance Platform.

## Table of Contents

1. [Overview](#overview)
2. [Technology Stack](#technology-stack)
3. [Architecture Diagram](#architecture-diagram)
4. [Frontend Architecture](#frontend-architecture)
5. [State Management](#state-management)
6. [Routing & Navigation](#routing--navigation)
7. [Internationalization](#internationalization)
8. [API Integration](#api-integration)
9. [Authentication](#authentication)
10. [Deployment Architecture](#deployment-architecture)
11. [Performance Optimization](#performance-optimization)
12. [Security](#security)

---

## Overview

Siraj is built as a modern, server-rendered React application using Next.js 14 with the App Router. The architecture emphasizes:

- **Server-Side Rendering (SSR)** for improved performance and SEO
- **Internationalization (i18n)** for Arabic and English support
- **Responsive Design** for mobile and desktop experiences
- **Component-Based Architecture** for maintainability and reusability
- **Type Safety** with TypeScript
- **Containerization** with Docker for consistent deployment

---

## Technology Stack

### Core Framework
- **Next.js 14.2.28** - React framework with App Router
- **React 18** - UI library
- **TypeScript 5** - Type-safe JavaScript

### UI & Styling
- **Material-UI (MUI) 6.1.1** - Component library
  - `@mui/material` - Core components
  - `@mui/icons-material` - Icons
  - `@mui/lab` - Experimental components
  - `@mui/x-date-pickers` - Date/time pickers
- **Tailwind CSS 3.4.9** - Utility-first CSS framework
- **Styled Components 6.1.13** - CSS-in-JS styling
- **Emotion** - CSS-in-JS library (MUI dependency)
- **SASS 1.77.8** - CSS preprocessor
- **Flowbite 2.5.1** - Component library

### Animation & Graphics
- **GSAP (@gsap/react 2.1.1)** - Animation library
- **Lottie (@lottiefiles/dotlottie-react)** - JSON-based animations
- **Swiper 11.1.12** - Touch slider

### Internationalization
- **next-intl 3.17.2** - i18n solution for Next.js

### HTTP & API
- **Axios 1.7.5** - HTTP client
- **Sharp 0.34.1** - Image optimization

### Forms & Validation
- **React Hook Form 7.53.1** - Form state management
- **Input OTP 1.2.4** - OTP input component
- **React OTP Input 3.1.1** - Alternative OTP input

### Date & Time
- **Day.js 1.11.13** - Date manipulation
- **Moment 2.30.1** - Date/time formatting

### Utilities
- **clsx 2.1.1** - Conditional classNames utility

### Development Tools
- **ESLint 8** - Code linting
- **Autoprefixer 10.4.20** - CSS vendor prefixing
- **PostCSS 8.4.41** - CSS transformations

### Deployment & DevOps
- **Docker** - Containerization
- **Kubernetes** - Container orchestration
- **Helm** - Kubernetes package manager
- **Node.js 18** - Runtime environment

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        Client Layer                          │
│                                                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Desktop    │  │   Mobile     │  │   Tablet     │      │
│  │   Browser    │  │   Browser    │  │   Browser    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│         │                  │                  │              │
└─────────┼──────────────────┼──────────────────┼──────────────┘
          │                  │                  │
          └──────────────────┴──────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                   Next.js Frontend (Port 3000)               │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │                  App Router (Next.js 14)               │ │
│  │                                                          │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │ │
│  │  │   [locale]/  │  │  Middleware  │  │  Navigation  │ │ │
│  │  │   Routes     │  │  (i18n, auth)│  │              │ │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘ │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │          Landing Pages (Public)                  │  │ │
│  │  │  - Home  - About  - Services  - Contact         │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  │                                                          │ │
│  │  ┌──────────────────────────────────────────────────┐  │ │
│  │  │      App Pages (Authenticated)                   │  │ │
│  │  │  - Profile  - MBTI Test  - Booking              │  │ │
│  │  │  - Plans  - Programs  - Settings                │  │ │
│  │  └──────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │              Component Layer                            │ │
│  │                                                          │ │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────┐ │ │
│  │  │  Layout  │  │   UI     │  │  Forms   │  │ Modals │ │ │
│  │  │Components│  │Components│  │          │  │        │ │ │
│  │  └──────────┘  └──────────┘  └──────────┘  └────────┘ │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │              Service Layer                              │ │
│  │                                                          │ │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────┐ │ │
│  │  │   Auth   │  │   MBTI   │  │  Booking │  │ Profile│ │ │
│  │  │ Service  │  │ Service  │  │  Service │  │Service │ │ │
│  │  └──────────┘  └──────────┘  └──────────┘  └────────┘ │ │
│  │                                                          │ │
│  │  ┌─────────────────────────────────────────────────┐   │ │
│  │  │         Base Service (Axios)                    │   │ │
│  │  │  - Request/Response Interceptors                │   │ │
│  │  │  - Error Handling                               │   │ │
│  │  │  - Authentication Headers                       │   │ │
│  │  └─────────────────────────────────────────────────┘   │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │          State Management & Context                     │ │
│  │                                                          │ │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐             │ │
│  │  │   User   │  │   Theme  │  │   i18n   │             │ │
│  │  │ Context  │  │ Context  │  │ Context  │             │ │
│  │  └──────────┘  └──────────┘  └──────────┘             │ │
│  └────────────────────────────────────────────────────────┘ │
└───────────────────────────┬───────────────────────────────────┘
                            │
                            ▼
                   ┌────────────────┐
                   │   HTTP/HTTPS   │
                   └────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              Backend API (siraj-be:3001)                     │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              RESTful API Endpoints                    │  │
│  │                                                         │  │
│  │  /api/auth/*        - Authentication                  │  │
│  │  /api/mbti/*        - Personality Tests               │  │
│  │  /api/bookings/*    - Session Bookings                │  │
│  │  /api/users/*       - User Management                 │  │
│  │  /api/programs/*    - Programs & Trials               │  │
│  │  /api/universities/* - College Data                   │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              Database Layer                           │  │
│  │         (MongoDB/PostgreSQL/etc.)                     │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## Frontend Architecture

### Next.js App Router

Siraj uses Next.js 14's App Router with the following structure:

```
src/app/
└── [locale]/                    # Dynamic locale parameter
    ├── (landingPage)/          # Route group - public pages
    │   ├── page.tsx            # Landing page
    │   ├── about-us/
    │   ├── our-services/
    │   ├── contact-us/
    │   ├── privacy-policy/
    │   └── terms-and-conditions/
    │
    ├── (app)/                  # Route group - authenticated
    │   └── app/
    │       ├── (withNav)/      # Pages with navigation
    │       │   ├── profile/
    │       │   ├── my-booking/
    │       │   ├── choose-your-plan/
    │       │   ├── order/
    │       │   └── program/
    │       │
    │       └── (withoutNav)/   # Pages without navigation
    │           └── test/mbti/
    │
    ├── login/                  # Login page
    ├── layout.tsx              # Root layout
    └── globals.scss            # Global styles
```

**Key Concepts:**

1. **`[locale]` Dynamic Segment:** Enables internationalization
2. **Route Groups `()`:** Organize routes without affecting URL
3. **Nested Layouts:** Shared UI across route segments
4. **Server Components:** Default rendering strategy

### Component Architecture

```
src/components/
├── LandingPage/              # Landing page components
│   ├── LandingPageDesktop.tsx
│   ├── Personalities.tsx
│   ├── Partners.tsx
│   └── ...
│
├── LandingPageMobile/        # Mobile-specific landing
│   └── LandingPageMobile.tsx
│
├── NavigationBar/            # Navigation components
│   ├── NavigationComponent.tsx
│   ├── UserAvatar.tsx
│   └── LanguageSwitcher.tsx
│
├── ui-components/            # Feature components
│   ├── BookNewSession/
│   ├── BookNewJobTrial/
│   └── ...
│
├── AboutUsPage/              # Page-specific components
├── Footer/
├── Dialog.tsx                # Shared components
├── Alert.tsx
└── Countdown.tsx
```

**Component Patterns:**

1. **Server vs Client Components:**
   - Default: Server Components (no `'use client'`)
   - Client: Use `'use client'` directive for interactivity

2. **Responsive Design:**
   - Separate mobile/desktop components where UX differs significantly
   - Use responsive Tailwind classes for minor differences

3. **Component Composition:**
   - Small, focused components
   - Composition over inheritance
   - Props for configuration

---

## State Management

### Approaches Used

#### 1. React Context
For global state shared across components:

```typescript
// Example: User context
export const UserContext = createContext<UserContextType>(undefined);

export function UserProvider({ children }: Props) {
  const [user, setUser] = useState<User | null>(null);
  
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}
```

#### 2. React Hooks
For local component state:

```typescript
// useState for simple state
const [isOpen, setIsOpen] = useState(false);

// useReducer for complex state
const [state, dispatch] = useReducer(reducer, initialState);
```

#### 3. URL State
For shareable state (filters, pagination):

```typescript
// Use search params
const searchParams = useSearchParams();
const page = searchParams.get('page') || '1';
```

#### 4. Server State
For data from APIs (cached by Next.js):

```typescript
// Server Component - automatic caching
async function getData() {
  const res = await fetch('https://api.example.com/data');
  return res.json();
}

export default async function Page() {
  const data = await getData();
  return <div>{data.title}</div>;
}
```

### State Organization

```
State Type          │ Location              │ Purpose
────────────────────┼───────────────────────┼─────────────────────
User Session        │ Context + Cookies     │ Authentication state
Theme Preferences   │ Context + LocalStorage│ UI customization
Language            │ URL + Cookies         │ i18n locale
Form Data           │ React Hook Form       │ Form state
API Data            │ Server Components     │ Backend data
UI State            │ Local useState        │ Component behavior
```

---

## Routing & Navigation

### Internationalized Routing

```typescript
// navigation.ts
import { createSharedPathnamesNavigation } from 'next-intl/navigation';

export const locales = ['en', 'ar'] as const;
export const localePrefix = 'always'; // Always show locale in URL

export const { Link, redirect, usePathname, useRouter } =
  createSharedPathnamesNavigation({ locales, localePrefix });
```

**Usage:**
```typescript
import { Link } from '@/navigation';

<Link href="/about-us">About Us</Link>
// Renders: /en/about-us or /ar/about-us
```

### Middleware

```typescript
// middleware.ts
import createMiddleware from 'next-intl/middleware';

export default createMiddleware({
  locales: ['en', 'ar'],
  defaultLocale: 'en',
  localePrefix: 'always'
});

export const config = {
  matcher: ['/((?!api|_next|.*\\..*).*)']
};
```

**Responsibilities:**
1. Detect user's locale (cookie, header, browser)
2. Redirect to localized route
3. Set locale cookie

### Protected Routes

```typescript
// Authentication check in layout or page
export default async function AppLayout({ children }) {
  const user = await getUser();
  
  if (!user) {
    redirect('/login');
  }
  
  return <>{children}</>;
}
```

---

## Internationalization

### Dictionary Structure

```json
// src/dictionaries/en.json
{
  "LandingPage": {
    "section1_headline": "Find Your future spark with SIRAJ",
    "section1_cta": "Get Started Today"
  },
  "Navbar": {
    "home": "Home",
    "about_us": "About Us"
  }
}

// src/dictionaries/ar.json
{
  "LandingPage": {
    "section1_headline": "اكتشف شرارة مستقبلك مع سراج",
    "section1_cta": "ابدأ اليوم"
  },
  "Navbar": {
    "home": "الرئيسية",
    "about_us": "من نحن"
  }
}
```

### Usage in Components

```typescript
import { useTranslations } from 'next-intl';

export default function LandingPage() {
  const t = useTranslations('LandingPage');
  
  return (
    <div>
      <h1>{t('section1_headline')}</h1>
      <button>{t('section1_cta')}</button>
    </div>
  );
}
```

### Server-Side Translations

```typescript
import { getTranslations } from 'next-intl/server';

export default async function Page() {
  const t = await getTranslations('MyPage');
  
  return <h1>{t('title')}</h1>;
}
```

### RTL Support

Handled automatically by Material-UI's theme:

```typescript
// theme.ts
import { createTheme } from '@mui/material/styles';

export const createCustomTheme = (locale: string) => {
  return createTheme({
    direction: locale === 'ar' ? 'rtl' : 'ltr',
    // ...other theme config
  });
};
```

---

## API Integration

### Base Service

```typescript
// src/services/base.service.ts
import axios from 'axios';

const baseService = axios.create({
  baseURL: process.env.BACKEND_BASE_URL,
  timeout: 30000,
  headers: {
    'Content-Type': 'application/json',
  }
});

// Request interceptor - add auth token
baseService.interceptors.request.use(
  (config) => {
    const token = getAuthToken();
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor - handle errors
baseService.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Handle unauthorized
      redirectToLogin();
    }
    return Promise.reject(error);
  }
);

export default baseService;
```

### Feature Services

```typescript
// Example: MBTI service
export const mbtiService = {
  getQuestions: async () => {
    const response = await baseService.get('/mbti/questions');
    return response.data;
  },
  
  submitAnswers: async (answers: Answer[]) => {
    const response = await baseService.post('/mbti/submit', { answers });
    return response.data;
  },
  
  getResults: async (userId: string) => {
    const response = await baseService.get(`/mbti/results/${userId}`);
    return response.data;
  }
};
```

### Error Handling

```typescript
try {
  const data = await mbtiService.getQuestions();
  setQuestions(data);
} catch (error) {
  if (axios.isAxiosError(error)) {
    // Handle Axios-specific errors
    const message = error.response?.data?.message || 'An error occurred';
    showError(message);
  } else {
    // Handle other errors
    showError('Unexpected error');
  }
}
```

---

## Authentication

### WhatsApp OTP Flow

```
1. User enters phone number
   │
   ├─> POST /api/auth/request-otp
   │   Request: { phone: "+962..." }
   │   Response: { success: true }
   │
2. User receives OTP via WhatsApp
   │
3. User enters OTP code
   │
   ├─> POST /api/auth/verify-otp
   │   Request: { phone: "+962...", otp: "123456" }
   │   Response: { token: "jwt...", user: {...} }
   │
4. Store token in cookies/localStorage
   │
5. Redirect to app
```

### Session Management

**Token Storage:**
```typescript
// Set token in HTTP-only cookie (secure)
setCookie('auth_token', token, {
  httpOnly: true,
  secure: true,
  sameSite: 'strict',
  maxAge: 30 * 24 * 60 * 60 // 30 days
});
```

**Protected Route Check:**
```typescript
// Server Component
async function checkAuth() {
  const token = cookies().get('auth_token');
  
  if (!token) {
    redirect('/login');
  }
  
  // Verify token with backend
  const user = await verifyToken(token.value);
  return user;
}
```

---

## Deployment Architecture

### Docker Container

```dockerfile
# Multi-stage build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --frozen-lockfile
COPY . .
RUN npm run build

FROM node:18-alpine
ENV NODE_ENV=production
WORKDIR /app
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./package.json
EXPOSE 3000
CMD ["npm", "start"]
```

### Kubernetes Deployment

```yaml
# deployment.yaml (simplified)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: siraj-frontend
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
        image: siraj-frontend:latest
        ports:
        - containerPort: 3000
        env:
        - name: BACKEND_BASE_URL
          value: "http://siraj-be:3001/api"
```

### Helm Chart Structure

```
Chart.yaml              # Chart metadata
values.yaml             # Default configuration
templates/
├── deployment.yaml     # Deployment resource
├── service.yaml        # Service resource
└── ingress.yaml        # Ingress resource
```

### Environment Variables

```yaml
# Development
BACKEND_ENV=dev
BACKEND_BASE_URL=http://localhost:3001/api

# Staging
BACKEND_ENV=staging
BACKEND_BASE_URL=https://staging-api.siraj.app/api

# Production
BACKEND_ENV=production
BACKEND_BASE_URL=https://api.siraj.app/api
```

---

## Performance Optimization

### 1. Next.js Optimizations

**Automatic Code Splitting:**
- Each route is automatically code-split
- Only necessary JavaScript is loaded

**Image Optimization:**
```tsx
import Image from 'next/image';

<Image
  src="/hero.jpg"
  alt="Hero"
  width={1200}
  height={800}
  priority        // Load immediately for above-fold
  placeholder="blur" // Show blur while loading
/>
```

**Font Optimization:**
```typescript
import { Inter } from 'next/font/google';

const inter = Inter({ subsets: ['latin'] });
```

### 2. Caching Strategies

**Static Generation:**
```typescript
// Generate at build time
export default async function Page() {
  const data = await fetch('https://api.example.com/data', {
    next: { revalidate: 3600 } // Revalidate every hour
  });
  
  return <div>{data.title}</div>;
}
```

**Dynamic Rendering:**
```typescript
// Render on each request
export const dynamic = 'force-dynamic';

export default async function Page() {
  const data = await getUserData();
  return <div>{data.name}</div>;
}
```

### 3. Bundle Size Optimization

**Dynamic Imports:**
```typescript
const DynamicComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <Skeleton />,
  ssr: false // Don't render on server
});
```

**Tree Shaking:**
```typescript
// ✅ Import only what you need
import { Button } from '@mui/material';

// ❌ Avoid importing entire library
import * as MUI from '@mui/material';
```

### 4. Performance Monitoring

**Core Web Vitals:**
- LCP (Largest Contentful Paint): < 2.5s
- FID (First Input Delay): < 100ms
- CLS (Cumulative Layout Shift): < 0.1

**Monitoring Tools:**
- Lighthouse (built into Chrome DevTools)
- Next.js Analytics (Vercel)
- Google Analytics
- Custom performance metrics

---

## Security

### 1. Authentication & Authorization

- JWT tokens stored in HTTP-only cookies
- Token expiration and refresh
- Role-based access control
- Protected API routes

### 2. Data Protection

**Input Validation:**
```typescript
// Sanitize user input
const sanitizedPhone = phone.replace(/[^\d+]/g, '');

// Validate format
if (!/^\+\d{10,15}$/.test(sanitizedPhone)) {
  throw new Error('Invalid phone number');
}
```

**Output Encoding:**
```tsx
// React automatically escapes HTML
<div>{userInput}</div> // Safe from XSS
```

### 3. HTTPS & Secure Communication

- Enforce HTTPS in production
- Secure cookie flags:
  - `httpOnly`: Prevent JavaScript access
  - `secure`: Only send over HTTPS
  - `sameSite`: CSRF protection

### 4. Environment Variables

- Never commit sensitive data
- Use `.env.local` for secrets
- Access only on server side:

```typescript
// ✅ Server Component - secure
const apiKey = process.env.SECRET_API_KEY;

// ❌ Client Component - exposed!
const apiKey = process.env.NEXT_PUBLIC_API_KEY;
```

### 5. CORS Configuration

Backend should set appropriate CORS headers:
```
Access-Control-Allow-Origin: https://siraj.app
Access-Control-Allow-Credentials: true
```

### 6. Rate Limiting

- Implement on backend
- Prevent brute force attacks
- Example: OTP rate limiting (5 requests per hour)

---

## Scalability Considerations

### Horizontal Scaling
- Kubernetes enables multiple pod replicas
- Load balancer distributes traffic
- Stateless frontend (no local session storage)

### Caching Strategy
- CDN for static assets
- API response caching
- Browser caching headers

### Database Optimization
- Efficient queries
- Proper indexing
- Connection pooling

---

## Monitoring & Logging

### Application Logs
```typescript
// Use structured logging
console.log({
  level: 'info',
  message: 'User logged in',
  userId: user.id,
  timestamp: new Date().toISOString()
});
```

### Error Tracking
- Sentry or similar service
- Track frontend errors
- Performance monitoring

### Analytics
- Google Analytics
- User behavior tracking
- Conversion funnels

---

## Future Architecture Enhancements

1. **Progressive Web App (PWA)**
   - Offline support
   - Push notifications
   - App-like experience

2. **GraphQL API**
   - Efficient data fetching
   - Reduce over-fetching
   - Strong typing

3. **Micro-frontends**
   - Independent feature deployment
   - Team autonomy
   - Technology flexibility

4. **Real-time Features**
   - WebSockets for live updates
   - Real-time chat with counselors
   - Live availability updates

---

*Last updated: January 2025*
