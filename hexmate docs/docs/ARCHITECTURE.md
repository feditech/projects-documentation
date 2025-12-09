# HexMate Architecture

This document describes the architecture and design patterns used in HexMate.

## Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Frontend Architecture](#frontend-architecture)
- [Module Structure](#module-structure)
- [State Management](#state-management)
- [Routing Architecture](#routing-architecture)
- [Component Hierarchy](#component-hierarchy)
- [Data Flow](#data-flow)
- [Authentication & Authorization](#authentication--authorization)

## Overview

HexMate is a modular, single-page application (SPA) built with React and TypeScript. The architecture follows modern React best practices with a component-based design, context-based state management, and module-based code organization.

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                       HexMate Frontend                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │     DMS     │  │     CTS     │  │     VMS     │         │
│  │   Module    │  │   Module    │  │   Module    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │           Shared Components & Utilities                 │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │         Context Providers (Auth, Config, etc.)         │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ REST API
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      Backend API Server                      │
│                   (Not part of this repo)                    │
└─────────────────────────────────────────────────────────────┘
```

## Frontend Architecture

### Technology Stack

- **Framework**: React 18.2 with TypeScript 4.9
- **UI Library**: Material-UI (MUI) v5.14
- **Routing**: React Router DOM v6.14
- **State Management**: React Context API
- **Build Tool**: Create React App with react-scripts 5.0.1
- **HTTP Client**: Axios

### Key Design Principles

1. **Modularity**: Each major feature (DMS, CTS, VMS) is organized as a separate module
2. **Reusability**: Common components are shared across modules
3. **Separation of Concerns**: Clear separation between UI, business logic, and data
4. **Type Safety**: TypeScript for compile-time type checking
5. **Responsive Design**: Mobile-first approach with Material-UI
6. **Accessibility**: WCAG 2.1 compliant components

## Module Structure

HexMate consists of three main modules:

### 1. Document Management System (DMS)
- **Path**: `/src/pages/dms/`
- **Routes**: `/dms/*`
- **Components**: `/src/components/pages/DMS/`

Features:
- Document explorer with hierarchical navigation
- Document/folder information pages
- Settings management (cabinets, templates, profiles)
- Document editing and content management
- Reports and logs

### 2. Correspondence Tracking System (CTS)
- **Path**: `/src/pages/cts/`
- **Routes**: `/cts/*`
- **Components**: `/src/components/pages/reports/cts/`

Features:
- Correspondence dashboard
- Correspondence creation and tracking
- Workflow and delegation management
- Settings and configurations
- Templates and document generation
- Reports and logs

### 3. Visitor Management System (VMS)
- **Path**: `/src/pages/vms/`
- **Routes**: `/vms/*`
- **Components**: `/src/components/pages/VMS/`

Features:
- Visitor dashboard
- Appointment scheduling and management
- Check-in/check-out system
- Workflow configuration
- Reports

## State Management

### Context Providers

HexMate uses React Context API for global state management:

#### 1. AuthContext (`/src/context/authcontext`)
Manages:
- User authentication state
- Login/logout functionality
- Token management (access & refresh tokens)
- User profile information
- Remember me functionality

#### 2. ConfigContext (`/src/context/configcontext`)
Manages:
- Application configuration
- Module availability (DMS, CTS, VMS)
- Dynamic feature flags
- System-wide settings

#### 3. NotificationContext (`/src/context/notificationcontext`)
Manages:
- Toast notifications
- Success/error messages
- Alert dialogs
- Loading states

### Local State
Component-level state is managed using React Hooks:
- `useState` for local component state
- `useEffect` for side effects
- `useReducer` for complex state logic
- Custom hooks for reusable logic

## Routing Architecture

### Route Structure

```
/                           → Login Page (Public)
/forget-password           → Password Recovery (Public)
/ResetPassword             → Password Reset (Public)

/welcome                   → Landing Page (Protected)
/userprofile              → User Profile (Protected)

/dms/*                    → DMS Module Routes (Protected)
  /dms/documents          → Document Explorer
  /dms/reports            → Reports
  /dms/logs               → Audit Logs
  /dms/cabinets           → Cabinet Settings
  ... (other DMS routes)

/cts/*                    → CTS Module Routes (Protected)
  /cts/dashboard          → CTS Dashboard
  /cts/correspondence     → Correspondence List
  /cts/reports            → Reports
  ... (other CTS routes)

/vms/*                    → VMS Module Routes (Protected)
  /vms/dashboard          → VMS Dashboard
  /vms/appointments       → Appointments
  /vms/checkins           → Check-ins
  ... (other VMS routes)
```

### Protected Routes

All authenticated routes are wrapped with `ProtectedRoute` component that:
- Checks authentication status
- Redirects to login if not authenticated
- Validates token expiry
- Handles token refresh

### Dynamic Route Loading

Routes are dynamically loaded based on:
- User's assigned modules
- User's admin status
- Module configuration in `config.json`

## Component Hierarchy

### Template Components

1. **AccountTemplate** - Layout for login/authentication pages
2. **MainTemplate** - Layout for authenticated application pages
3. **ListPageTemplate** - Layout for list/grid pages
4. **LandingPageTemplate** - Layout for module selection page

### Page Components

Located in `/src/pages/`:
- Module-specific pages (dms, cts, vms)
- User management pages
- Account management pages

### Shared Components

Located in `/src/components/`:
- **alerts**: Alert dialogs and notifications
- **controls**: Form controls and inputs
- **editmodals**: Modal dialogs for editing
- **loadingoverlay**: Loading indicators
- **route**: Route protection and navigation

## Data Flow

### API Communication

```
Component
    ↓
Custom Hook (e.g., useAPI)
    ↓
Axios HTTP Client
    ↓
Backend API
    ↓
Response
    ↓
State Update
    ↓
Re-render
```

### Typical Flow Example

1. User interacts with UI component
2. Component calls API function via custom hook
3. Loading state is set in context/local state
4. Axios makes HTTP request to backend
5. Response is processed
6. State is updated (context or local)
7. Notification is shown (success/error)
8. Component re-renders with new data

## Authentication & Authorization

### Authentication Flow

1. **Login**:
   - User submits credentials
   - Backend validates and returns tokens
   - Tokens stored in AuthContext
   - User redirected based on modules/roles

2. **Token Management**:
   - Access token used for API requests
   - Refresh token used to obtain new access token
   - Automatic token refresh on expiry
   - Token stored with expiry timestamp

3. **Logout**:
   - Clear auth context
   - Remove tokens
   - Redirect to login page

### Authorization Levels

1. **Admin Users**:
   - Access to all modules
   - User and system management
   - Full CRUD operations

2. **Module Users**:
   - Access to assigned modules only
   - Limited to module-specific features
   - Permission-based actions

### Route Protection

```typescript
<ProtectedRoute>
  <MainTemplate />
</ProtectedRoute>
```

- Validates authentication before rendering
- Checks token validity
- Handles token refresh
- Redirects unauthorized users

## Internationalization

HexMate supports multiple languages through i18next:

- Translation files in `/src/locales/`
- Language detection from browser
- Dynamic language switching
- RTL support for Arabic/Hebrew

## Document Processing

### Dynamsoft Document Web Twain (DWT)

- Document scanning from physical scanners
- Image capture and processing
- Document upload and conversion
- Resources copied to public folder on build

### PDF Processing

Multiple PDF libraries used for different purposes:
- **jsPDF**: PDF generation
- **PDF-lib**: PDF manipulation
- **@react-pdf/renderer**: React-based PDF generation
- **pdfjs-dist**: PDF rendering and viewing

### OCR Processing

- **Tesseract.js**: Optical Character Recognition
- Language data loaded from public folder
- Supports multiple languages

## Performance Optimizations

1. **Code Splitting**: Routes loaded on demand
2. **Lazy Loading**: Components loaded when needed
3. **Memoization**: React.memo for expensive components
4. **Virtualization**: react-window for large lists
5. **Debouncing**: Search and input optimizations
6. **Caching**: API response caching where appropriate

## Error Handling

1. **Component Level**: Error boundaries for graceful failures
2. **API Level**: Axios interceptors for global error handling
3. **User Feedback**: Notifications for all user actions
4. **Logging**: Console logging in development

## Build & Deployment

### Build Process

```bash
npm run build
```

Creates optimized production build:
- Minified JavaScript and CSS
- Tree shaking to remove unused code
- Asset optimization
- Source maps for debugging

### Environment Configuration

- `.env` file for environment variables
- `config.json` for runtime configuration
- Separate configs for dev/staging/production

## Future Considerations

1. **State Management**: Consider Redux or Zustand for complex state
2. **Testing**: Expand test coverage with Jest and React Testing Library
3. **PWA**: Progressive Web App capabilities
4. **Offline Support**: Service workers for offline functionality
5. **Real-time Updates**: WebSocket integration for live updates
6. **Performance Monitoring**: Integration with performance monitoring tools
