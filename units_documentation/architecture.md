# Architecture

This document describes the technical architecture of the Units warehouse management system.

## System Overview

Units is a modern, single-page application (SPA) built with React and TypeScript, communicating with a RESTful API backend.

```
┌─────────────────────────────────────────────────────────────┐
│                        Client Browser                        │
│  ┌───────────────────────────────────────────────────────┐  │
│  │         React Application (TypeScript)                 │  │
│  │  ┌─────────┐  ┌──────────┐  ┌──────────────────────┐ │  │
│  │  │  Pages  │  │Components│  │  Context (State Mgmt)│ │  │
│  │  └─────────┘  └──────────┘  └──────────────────────┘ │  │
│  │  ┌─────────────────────────────────────────────────┐  │  │
│  │  │         React Router (Client-side routing)      │  │  │
│  │  └─────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ HTTPS/REST
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      Backend API Server                      │
│                (api.units.compass-dx.com)                    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              RESTful API Endpoints                   │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                         Database                             │
│                   (User Data, Inventory, etc.)               │
└─────────────────────────────────────────────────────────────┘
```

## Frontend Architecture

### Technology Stack

#### Core Framework
- **React 18**: UI library for building component-based interfaces
- **TypeScript 4.9**: Adds static typing to JavaScript
- **React Router v6**: Client-side routing and navigation

#### UI Components
- **Material-UI (MUI) v5**: Comprehensive React component library
  - `@mui/material`: Core components
  - `@mui/icons-material`: Icon library
  - `@mui/lab`: Experimental components
  - `@mui/x-data-grid`: Advanced data grid
  - `@mui/x-charts`: Chart components
  - `@mui/x-date-pickers`: Date/time pickers
  - `@mui/x-tree-view`: Tree view component
- **@emotion/react & @emotion/styled**: CSS-in-JS styling solution

#### State Management
- **React Context API**: Global state management
  - `AuthContext`: User authentication and session
  - `NotificationContext`: System notifications
  - `ConfigContext`: Application configuration
  - `TenantContext`: Multi-tenant information

#### Data Fetching
- **Axios**: HTTP client for API communication
- Custom service hooks for API abstraction

#### Internationalization
- **i18next**: Internationalization framework
- **react-i18next**: React bindings for i18next
- **i18next-browser-languagedetector**: Automatic language detection
- Supports: English (en), Arabic (ar)

#### Form Handling
- Custom form components built on MUI
- Real-time validation
- Error handling and display

#### Document Generation
- **jsPDF**: PDF generation
- **jspdf-autotable**: Table generation in PDFs
- **pdf-lib**: PDF manipulation
- **jsbarcode**: Barcode generation

#### Additional Libraries
- **moment**: Date/time manipulation
- **react-datepicker**: Date picker component
- **react-loading-skeleton**: Loading placeholders
- **react-to-pdf**: React component to PDF conversion
- **xlsx**: Excel file parsing and generation
- **react-google-maps/api**: Google Maps integration
- **react-image-file-resizer**: Image optimization

### Project Structure

```
unitswebapp/
├── public/              # Static assets
│   ├── index.html
│   └── manifest.json
├── src/
│   ├── assets/          # Images, logos
│   ├── components/      # Reusable React components
│   │   ├── alerts/      # Alert/notification components
│   │   ├── business/    # Business logic components
│   │   │   ├── appbar/  # Application bar components
│   │   │   └── tenantthemeprovider.tsx
│   │   ├── charts/      # Chart components
│   │   ├── controls/    # Form controls (inputs, buttons)
│   │   ├── editmodals/  # Edit modal dialogs
│   │   ├── layout/      # Layout components (grids, cards)
│   │   ├── multilingual/# Language switching components
│   │   ├── pages/       # Page-specific components
│   │   │   ├── customers/
│   │   │   ├── dashboard/
│   │   │   ├── reports/
│   │   │   ├── tenants/
│   │   │   └── warehouse/
│   │   ├── route/       # Routing components (ProtectedRoute)
│   │   ├── units_components/  # Units-specific components
│   │   ├── units_controls/    # Custom form controls
│   │   └── units_forms/       # Complex form components
│   │       ├── brands/
│   │       ├── carriers/
│   │       ├── inboundrequests/
│   │       ├── leads/
│   │       ├── orderbins/
│   │       ├── outbound/
│   │       ├── outboundrequests/
│   │       ├── packingmaterials/
│   │       ├── putawayrequests/
│   │       ├── quotations/
│   │       ├── sku/
│   │       ├── suppliers/
│   │       └── warehouse/
│   ├── context/         # React Context providers
│   │   ├── authcontext.tsx
│   │   ├── configcontext.tsx
│   │   ├── notificationcontext.tsx
│   │   └── tenantcontext.tsx
│   ├── locales/         # Internationalization files
│   │   ├── ar/          # Arabic translations
│   │   └── en/          # English translations
│   ├── pages/           # Top-level page components
│   │   ├── account/     # Login, password reset
│   │   ├── inboundrequests/
│   │   ├── outboundrequests/
│   │   ├── reports/
│   │   ├── salla/       # E-commerce integration
│   │   ├── settings/    # Configuration pages
│   │   └── sku/         # Inventory pages
│   ├── shared/          # Shared utilities
│   │   ├── hooks/       # Custom React hooks
│   │   └── services/    # API service functions
│   ├── styles/          # Global styles
│   ├── templates/       # Page templates/layouts
│   ├── App.tsx          # Main application component
│   ├── App.css          # Application styles
│   ├── index.tsx        # Entry point
│   └── index.css        # Global styles
├── .env                 # Environment variables
├── package.json         # Dependencies and scripts
├── tsconfig.json        # TypeScript configuration
└── README.md            # Project readme
```

### Component Architecture

#### Component Hierarchy

```
App
├── ConfigProvider
├── NotificationContextProvider
├── AuthProvider
├── TenantContextProvider
│   └── TenantThemeProvider
│       └── Router
│           └── ApplicationRoutes
│               ├── AccountTemplate (public routes)
│               │   ├── LoginPage
│               │   ├── RequestQuoteForm
│               │   └── AcceptQuotation
│               └── ProtectedRoute
│                   └── UnitsMainTemplate (authenticated routes)
│                       ├── Dashboard
│                       ├── UnitsListPageTemplate
│                       │   ├── Leads
│                       │   ├── Quotations
│                       │   ├── InboundRequests
│                       │   ├── OutboundRequests
│                       │   ├── SKU
│                       │   └── Settings pages
│                       └── DetailsPageTemplate
│                           └── Detail forms
```

#### Key Component Types

**1. Page Components**
- Top-level route components
- Orchestrate data fetching and display
- Example: `Dashboard`, `InboundRequests`, `SKU`

**2. Template Components**
- Provide consistent layouts
- `UnitsMainTemplate`: Main authenticated layout with navigation
- `UnitsListPageTemplate`: List page layout with filters
- `DetailsPageTemplate`: Detail page layout
- `AccountTemplate`: Public page layout

**3. Form Components**
- Handle data entry
- Located in `components/units_forms/`
- Include validation and submission logic
- Example: `InboundRequestForm`, `QuotationForm`

**4. Control Components**
- Reusable form controls
- Located in `components/controls/` and `components/units_controls/`
- Wrappers around MUI components
- Example: `TextFieldDX`, `ButtonDX`, `UnitsDatePicker`

**5. Layout Components**
- Structural components
- Located in `components/layout/`
- Example: `GridDX`, `CardDX`, `TypographyDX`

**6. Business Components**
- Domain-specific logic
- Located in `components/business/` and `components/units_components/`
- Example: `ItemBox`, `UtilizationBox`

### State Management

#### Context Providers

**AuthContext**
- Purpose: Manage user authentication state
- State:
  - `isLoggedIn`: Boolean
  - `userData`: User profile information
  - `fullToken`: JWT token and expiry
  - `authInitialized`: Whether auth check is complete
- Methods:
  - `signIn(token, userData)`: Log user in
  - `signOut()`: Log user out
  - `updateUserData(data)`: Update user profile

**NotificationContext**
- Purpose: Display system notifications
- State:
  - `notifications`: Array of notifications
- Methods:
  - `setSuccess(message)`: Show success message
  - `setError(message)`: Show error message
  - `setWarning(message)`: Show warning message
  - `setInfo(message)`: Show info message

**ConfigContext**
- Purpose: Application configuration
- State:
  - `configLoaded`: Whether config is loaded
  - `config`: Configuration object
- Methods:
  - `loadConfig()`: Fetch and load configuration

**TenantContext**
- Purpose: Multi-tenant management
- State:
  - `tenant`: Current tenant information
  - `tenantTheme`: Tenant-specific theme
- Methods:
  - `setTenant(tenant)`: Set current tenant
  - `loadTenantTheme()`: Load tenant customizations

#### Local Component State
- Used with `useState` hook
- For component-specific state
- Examples: form values, UI state (open/closed modals)

### Routing

#### Route Structure

**Public Routes** (`/`)
- Login
- Request Quote
- Accept Quotation
- Password Reset
- Email Confirmation
- Salla Authorization

**Protected Routes** (require authentication)
- Dashboard (`/dashboard`)
- Leads (`/leads`)
- Quotations (`/quotations`)
- Inbound Requests (`/inboundrequests`)
- Orders (`/orders`)
- SKU Management (`/sku`, `/skukit`, `/skucategory`)
- Customer Addresses (`/customeraddress`)
- Customers (`/customers`)
- Settings:
  - Users (`/users`)
  - Warehouses (`/warehouses`)
  - Carriers (`/warehousecarriers`)
  - Order Bins (`/warehouseorderbins`)
  - Time Slots (`/warehousetimeslots`)
  - Packages (`/packages`)
  - Packing Materials (`/packingmaterials`)
  - Suppliers (`/supplier`)
  - Brands (`/brands`)
  - Tenants (`/tenants`)
  - Customizations (`/customizations`)
- Reports:
  - Inbound Report (`/inboundreport`)
  - Order Report (`/orderreport`)
  - SKU Report (`/skureport`)
  - Stock Report (`/stockreport`)

#### Protected Route Implementation
```typescript
<ProtectedRoute>
  {isLoggedIn ? <Outlet /> : <Navigate to="/" />}
</ProtectedRoute>
```

### API Communication

#### Service Layer Architecture

Services are organized by domain in `src/shared/services/`:
- `authservice.ts`: Authentication
- `warehouseservice.ts`: Warehouse operations
- `customerservice.ts`: Customer management
- etc.

#### API Request Pattern
```typescript
// Example service function
export const fetchInboundRequests = async (params) => {
  const response = await axios.get(
    `${process.env.REACT_APP_BASE_API}inboundrequests`,
    { params }
  );
  return response.data;
};
```

#### Authentication Flow
1. User submits credentials
2. API returns JWT token
3. Token stored in AuthContext and localStorage
4. Token included in all subsequent requests via Axios interceptor
5. Token refresh on expiry
6. Logout clears token and redirects to login

#### Error Handling
- Axios interceptors catch HTTP errors
- Errors displayed via NotificationContext
- 401 errors trigger logout
- Network errors show user-friendly messages

### Styling Approach

#### Material-UI Theme
- Customizable theme per tenant
- Theme defined in `TenantThemeProvider`
- Supports light/dark mode
- RTL support for Arabic

#### CSS-in-JS with Emotion
```typescript
const StyledComponent = styled('div')`
  color: ${props => props.theme.palette.primary.main};
  padding: ${props => props.theme.spacing(2)};
`;
```

#### Component-level Styles
- Inline styles for dynamic values
- CSS modules not used
- Global styles in `index.css` and `App.css`

### Performance Optimizations

#### Code Splitting
- Route-based code splitting with `React.lazy()`
- Reduces initial bundle size
- Lazy load heavy components

#### Memoization
- `React.memo()` for expensive components
- `useMemo()` for expensive calculations
- `useCallback()` to prevent unnecessary re-renders

#### Virtual Scrolling
- MUI DataGrid uses virtual scrolling
- Handles large datasets efficiently

#### Image Optimization
- `react-image-file-resizer` for uploaded images
- Reduces image size before upload

### Security Measures

#### Authentication
- JWT-based authentication
- Token stored securely
- HTTPS only communication
- Token expiry and refresh

#### Input Validation
- Client-side validation for user experience
- Server-side validation (enforced by API)
- TypeScript prevents type errors

#### XSS Protection
- React escapes rendered content by default
- `dangerouslySetInnerHTML` not used

#### CSRF Protection
- Handled by API backend
- Token-based authentication

## Backend API

### API Endpoint
- Base URL: `https://api.units.compass-dx.com/api/`
- Communication: RESTful JSON API
- Authentication: JWT Bearer tokens

### Expected API Structure

#### Authentication Endpoints
- `POST /auth/login`: User login
- `POST /auth/refresh`: Refresh token
- `POST /auth/logout`: User logout
- `POST /auth/reset-password`: Password reset

#### Resource Endpoints
Pattern: `/api/{resource}`

Examples:
- `/inboundrequests`: Inbound request operations
- `/outboundrequests`: Outbound request operations
- `/sku`: SKU management
- `/warehouses`: Warehouse configuration
- `/customers`: Customer management
- `/users`: User management

#### HTTP Methods
- `GET`: Retrieve resources
- `POST`: Create resources
- `PUT`: Update resources
- `DELETE`: Delete resources

## Deployment Architecture

### Build Process
```bash
npm run build
```
- Creates optimized production build
- Output to `build/` directory
- Minified JavaScript and CSS
- Asset fingerprinting for cache busting

### Hosting
- Static file hosting (e.g., Nginx, Apache, or CDN)
- Serves `build/index.html` and assets
- All routes redirect to `index.html` (SPA routing)

### Environment Configuration
- Environment variables in `.env` file
- Build-time configuration via `REACT_APP_*` variables
- Critical settings:
  - `REACT_APP_BASE_API`: API base URL
  - `REACT_APP_GOOGLE_MAPS_API_KEY`: Google Maps key

### CDN and Caching
- Static assets can be CDN-hosted
- Cache headers for assets (long-lived)
- `index.html` not cached (ensures latest version)

## Integration Points

### Google Maps
- Used for address selection and mapping
- API key required
- Components: `@react-google-maps/api`

### Salla E-commerce
- OAuth integration for authorization
- Order import from Salla stores
- Inventory synchronization

### Barcode Scanning
- `jsbarcode` library for generation
- Camera or scanner hardware for reading

### Excel Import/Export
- `xlsx` library for processing
- Bulk data operations
- Template-based imports

## Browser Compatibility

### Supported Browsers
- Chrome (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Edge (latest 2 versions)

### Progressive Enhancement
- Core functionality works on all modern browsers
- Advanced features may require newer browsers

### Mobile Support
- Responsive design adapts to screen size
- Touch-friendly interface
- Mobile browsers supported (iOS Safari, Chrome Mobile)

## Monitoring and Logging

### Client-side Logging
- Console logging for development
- Error boundary components catch React errors
- Production: errors should be sent to logging service

### Analytics
- Can integrate Google Analytics or similar
- Track user actions and page views
- Monitor performance metrics

## Next Steps

- Review [API Reference](./api-reference.md) for detailed API documentation
- See [Configuration](./configuration.md) for setup details
- Check [Getting Started](./getting-started.md) for installation
