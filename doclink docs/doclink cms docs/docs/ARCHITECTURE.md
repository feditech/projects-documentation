# System Architecture

## Overview

DocLink CMS is built using a modern frontend architecture with React and follows a component-based design pattern. The application connects to a backend API service for data management and business logic.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        Browser                               │
│  ┌────────────────────────────────────────────────────────┐ │
│  │             DocLink CMS (React SPA)                    │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌─────────────┐ │ │
│  │  │   UI Layer   │  │  Redux Store │  │  API Client │ │ │
│  │  │ (Components) │◄─┤   (State)    │◄─┤   (Axios)   │ │ │
│  │  └──────────────┘  └──────────────┘  └─────────────┘ │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ HTTPS/REST API
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     Backend API Server                       │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  API Endpoints (Authentication, Doctors, Patients,    │ │
│  │  Labs, Content, Sessions, Finance)                     │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       Database Layer                         │
└─────────────────────────────────────────────────────────────┘
```

## Technology Stack

### Frontend Framework
- **React 17.0.2**: Core UI library for building component-based interfaces
- **React Router 6.2.1**: Client-side routing and navigation
- **React DOM**: React rendering for web browsers

### State Management
- **Redux 4.1.2**: Centralized state management
- **Redux Toolkit**: Official Redux toolset for efficient development
- **Redux Persist**: Local storage persistence for state
- **Redux Logger**: Development tool for state debugging

### UI Framework & Components
- **Material-UI (MUI) 5.4.3**: Primary component library
  - `@mui/material`: Core components
  - `@mui/icons-material`: Icon library
  - `@mui/lab`: Experimental components
  - `@mui/styles`: Styling solution
- **Styled Components 5.3.3**: CSS-in-JS styling
- **Material Table**: Advanced data table components

### Data Visualization
- **Chart.js 3.7.1**: Charting library
- **React ChartJS 2**: React wrapper for Chart.js
- **chartjs-adapter-date-fns**: Date handling for charts

### Form & Input Components
- **React DatePicker**: Date selection
- **React Flatpickr**: Alternative date picker
- **React Select**: Enhanced select dropdowns
- **@mui/x-date-pickers**: MUI date/time pickers

### Rich Text Editing
- **TinyMCE React**: Rich text editor
- **React Quill**: Alternative WYSIWYG editor
- **Draft.js**: Rich text editor framework
- **MUI RTE**: Material-UI rich text editor

### Location Services
- **@react-google-maps/api**: Google Maps integration
- **React Google Autocomplete**: Address autocomplete
- **React Places Autocomplete**: Location search
- **use-places-autocomplete**: Custom hook for places

### HTTP & API Communication
- **Axios 0.26.1**: Promise-based HTTP client
- **Custom API layer**: Abstraction for API calls

### Utilities
- **Moment.js & date-fns**: Date manipulation
- **File Saver**: Client-side file saving
- **React Toastify**: Toast notifications
- **React Icons**: Icon library
- **bytes**: Byte formatting
- **html-react-parser**: HTML string parsing

### Build Tools & Development
- **Webpack**: Module bundler
- **Babel**: JavaScript transpiler
- **React Scripts**: Create React App scripts
- **ESLint**: Code linting
- **Prettier**: Code formatting

## Application Layers

### 1. Presentation Layer (UI Components)

The presentation layer is organized into screens and reusable components:

```
src/
├── screens/
│   ├── authorized/       # Protected routes
│   │   ├── dashboard/    # Dashboard screen
│   │   ├── doctors/      # Doctor management
│   │   ├── patients/     # Patient management
│   │   ├── masters/      # Master data management
│   │   ├── blogs/        # Blog management
│   │   ├── policies/     # Policy management
│   │   └── setting/      # Settings and configuration
│   └── unauthorized/     # Public routes
│       ├── login/        # Login screen
│       └── forgotPassword/ # Password recovery
├── components/           # Reusable components
│   ├── Table/           # Table components
│   ├── Calendar/        # Calendar component
│   ├── FilterDateWeek/  # Date filtering
│   └── uploadFile/      # File upload
└── menu.js              # Navigation menu
```

**Key Design Patterns:**
- **Component Composition**: Breaking down UI into small, reusable components
- **Container/Presentational Pattern**: Separating logic from presentation
- **Higher-Order Components**: Code reuse through component wrapping
- **Custom Hooks**: Extracting and reusing stateful logic

### 2. State Management Layer (Redux)

Redux manages the application state with feature-based slices:

```
src/redux/
├── store.js              # Redux store configuration
└── slices/
    ├── activeAccount/    # User authentication state
    ├── loader/           # Loading states
    └── master/           # Master data (lab categories, etc.)
```

**State Management Patterns:**
- **Redux Toolkit**: Simplified Redux development with createSlice
- **Normalization**: Organizing nested data structures
- **Selectors**: Computed state derivation
- **Middleware**: Redux Logger for development
- **Persistence**: Redux Persist for local storage

**State Flow:**
```
User Action → Dispatch Action → Reducer → Update Store → 
Component Re-render
```

### 3. Data Access Layer (API)

The API layer provides a centralized interface for backend communication:

```
src/api/
├── index.js          # Axios instance and interceptors
└── endPoints.js      # API endpoint definitions
```

**API Organization:**
- **Centralized Configuration**: Single Axios instance with interceptors
- **Endpoint Mapping**: Organized by feature domain
- **Request/Response Interceptors**: 
  - Adding authentication tokens
  - Error handling
  - Request/response transformation
  - Loading state management

**Example API Structure:**
```javascript
// Authentication
auth: { login, logout, forget, verifyOtp, changePassword }

// Doctor Management
docProfile: { create, getAll, edit, delete }
docSpec: { create, getAll, edit, delete }
docDisease: { getAll, create, edit, delete }
docHealthConcerns: { getAll, create, edit, delete }

// Lab Management
lab: { view, create, edit, delete }
lab_parent_category: { view, add, edit, delete }
lab_child_category: { view, add, edit, delete }

// Content Management
blogs: { getAll, create, edit, delete }
healthTips: { getAll, create, edit, delete }
banner: { getAll, create, edit, delete }
```

### 4. Routing Layer

**React Router Configuration:**
```javascript
<Routes>
  <Route path="/" element={<Layout />}>
    {/* Public Routes */}
    <Route path="/login" element={<Login />} />
    <Route path="/forgotten-password" element={<ForgotPassword />} />
    
    {/* Protected Routes */}
    <Route element={<RequireAuth />}>
      <Route path="/" element={<Dashboard />} />
      <Route path="/doctor/*" element={...} />
      <Route path="/patient/*" element={...} />
      <Route path="/masters/*" element={...} />
      {/* ... more routes ... */}
    </Route>
  </Route>
</Routes>
```

**Route Protection:**
- `RequireAuth` component checks authentication state
- Redirects to login if not authenticated
- Token validation on protected routes

### 5. Utility Layer

Common utilities and helpers:

```
src/utils/
├── helpers.js          # General helper functions
├── api.js             # API utility functions
├── colors.js          # Color constants
├── fonts.js           # Font constants
├── layout.js          # Layout components
├── materialIcons.js   # Icon exports
└── requireAuth.js     # Route protection
```

## Data Flow

### Authentication Flow

```
1. User enters credentials → Login Component
2. Dispatch login action → Redux Action
3. API call to backend → Axios Request
4. Receive JWT token → API Response
5. Store token in Redux → State Update
6. Persist token locally → Redux Persist
7. Set Authorization header → Axios Interceptor
8. Redirect to Dashboard → React Router
```

### CRUD Operation Flow

```
1. User interacts with UI → Component Event
2. Component dispatches action → Redux Action
3. Show loading indicator → Loader Slice
4. API request with auth token → Axios + Interceptor
5. Backend processes request → API Server
6. Receive response data → API Response
7. Update Redux state → Reducer
8. Hide loading indicator → Loader Slice
9. Show success/error toast → React Toastify
10. Component re-renders → React Update
```

## Security Architecture

### Authentication
- **JWT Token-based**: Stateless authentication
- **Token Storage**: Redux + LocalStorage (via Redux Persist)
- **Token Refresh**: Automatic refresh on expiry
- **Secure Headers**: Authorization header for API requests

### Authorization
- **Role-Based Access Control (RBAC)**: User roles and permissions
- **Route Guards**: Protected routes with `RequireAuth`
- **API-Level Authorization**: Backend validates user permissions
- **Permission Checking**: UI elements hidden based on permissions

### Data Security
- **HTTPS Only**: Encrypted data transmission
- **Input Validation**: Client-side validation before API calls
- **XSS Prevention**: React's automatic escaping
- **CSRF Protection**: Token-based protection

## Performance Optimizations

### Code Splitting
- **React.lazy**: Dynamic imports for route-based splitting
- **Suspense**: Loading states for lazy components

### State Management
- **Normalized State**: Efficient state updates
- **Memoization**: React.memo for expensive components
- **Selector Optimization**: Reselect for computed state

### Network Optimization
- **API Caching**: Redux state caching
- **Request Debouncing**: Preventing excessive API calls
- **Loading States**: User feedback during async operations

### Bundle Optimization
- **Tree Shaking**: Removing unused code
- **Minification**: Production build optimization
- **Asset Optimization**: Image and asset compression

## Scalability Considerations

### Frontend Scalability
- **Modular Architecture**: Feature-based organization
- **Component Reusability**: DRY principle
- **Lazy Loading**: On-demand feature loading
- **State Isolation**: Feature-specific state slices

### Development Scalability
- **TypeScript Ready**: Easy migration path
- **Testing Infrastructure**: Jest + React Testing Library
- **Linting & Formatting**: Consistent code style
- **Documentation**: Inline comments and external docs

## Browser Compatibility

**Production:**
- \>0.2% market share
- Not dead browsers
- Not Opera Mini

**Development:**
- Latest Chrome
- Latest Firefox
- Latest Safari

## Integration Points

### Third-Party Services
1. **Google Maps API**: Location services and map display
2. **Backend API**: RESTful API for all data operations
3. **File Storage**: File upload and retrieval

### External Libraries
- Material-UI for consistent UI/UX
- Chart.js for data visualization
- TinyMCE for rich text editing
- Redux for predictable state management

## Future Architecture Considerations

1. **Microservices**: Backend API could be split into microservices
2. **GraphQL**: Consider GraphQL for more flexible data fetching
3. **TypeScript**: Gradual migration for type safety
4. **Testing**: Comprehensive test coverage
5. **PWA**: Progressive Web App capabilities
6. **Real-time**: WebSocket integration for live updates
7. **Mobile**: React Native for mobile applications

## Deployment Architecture

```
Development → Staging → Production

Development:
- Local development server (npm start)
- Hot module replacement
- Source maps enabled

Staging:
- Production build (npm run build)
- Testing environment
- Performance monitoring

Production:
- Optimized production build
- CDN for static assets
- Error tracking and monitoring
- Load balancing
```

## Monitoring & Logging

### Frontend Monitoring
- Redux Logger (development)
- Error boundaries for error catching
- Performance monitoring with Web Vitals
- User analytics (if integrated)

### Error Handling
- Try-catch blocks in async operations
- API error interceptors
- User-friendly error messages
- Error logging to backend

---

This architecture provides a solid foundation for a scalable, maintainable healthcare management system while maintaining flexibility for future enhancements.
