# DocLink Architecture

This document provides a comprehensive overview of the DocLink web application's technical architecture, design patterns, and component structure.

## Technology Stack

### Core Framework
- **Next.js 12.3.1**: React framework with server-side rendering, static generation, and optimized routing
- **React 17**: UI library for building component-based interfaces

### UI & Styling
- **Material-UI (MUI) v5**: Comprehensive React component library
  - `@mui/material`: Core components
  - `@mui/icons-material`: Icon components
  - `@mui/joy`: Joy UI components (alpha)
- **Styled Components**: CSS-in-JS styling solution
- **Emotion**: CSS-in-JS library for styling
- **Sass**: CSS preprocessor for enhanced styling capabilities

### State Management
- **Redux**: Centralized state management
- **Redux Thunk**: Middleware for handling asynchronous actions
- **Redux DevTools Extension**: Development tools for debugging
- **Next Redux Wrapper**: Integration between Next.js and Redux

### Data Fetching & APIs
- **Axios**: Promise-based HTTP client for API requests
- **React Query**: Data fetching and caching library

### Additional Libraries
- **Framer Motion**: Animation library for React
- **React Player**: Media player component
- **React Slick**: Carousel component
- **React Hot Toast & React Toastify**: Toast notification libraries
- **Moment.js & date-fns**: Date manipulation and formatting
- **React Scroll**: Smooth scrolling functionality

## Project Structure

```
doclink-web/
├── components/              # React components
│   ├── header/             # Application header
│   ├── footer/             # Footer components (footer, footer1, footer2, footer3)
│   ├── nav1, nav2, nav3/   # Navigation components
│   ├── responsiveNav/      # Mobile/responsive navigation
│   ├── layout/             # Layout wrapper components
│   ├── home/               # Home page specific components
│   │   ├── features/       # Features section
│   │   ├── stories/        # User stories/testimonials
│   │   ├── topDoctors/     # Top doctors showcase
│   │   ├── blogs/          # Blog preview section
│   │   └── downloadApp/    # App download section
│   ├── aboutus/            # About us page components
│   │   ├── header/         # About us header
│   │   ├── whatDoclink/    # What is DocLink section
│   │   ├── doclinkCreated/ # DocLink creation story
│   │   ├── connectPatients/# Patient connection info
│   │   └── doclinkFeatures/# DocLink features
│   ├── doctor/             # Doctor-related components
│   ├── blogs/              # Blog components
│   ├── contactUs/          # Contact form components
│   ├── faqs/               # FAQ components
│   ├── subscriptionPlans/  # Subscription plan components
│   ├── inviteYourDoctor/   # Doctor invitation components
│   ├── modals/             # Modal dialogs
│   ├── DownloadAppDialog/  # App download dialogs
│   └── styledComponent/    # Shared styled components
├── pages/                  # Next.js pages (automatic routing)
│   ├── _app.js            # Custom App component
│   ├── _document.js       # Custom Document component
│   ├── index.js           # Home page
│   ├── about-us/          # About us page
│   ├── doctors/           # Doctors listing page
│   ├── blogs/             # Blogs listing page
│   ├── viewblog/          # Individual blog view
│   ├── contact-us/        # Contact page
│   ├── faqs/              # FAQs page
│   ├── subscription-plans/# Subscription plans page
│   ├── invite-your-doctor/# Invite doctor page
│   ├── privacy-policy/    # Privacy policy page
│   ├── terms-and-conditions/ # Terms and conditions
│   ├── refund-policy/     # Refund policy
│   ├── cancellation-policy/ # Cancellation policy
│   └── payments-policy/   # Payments policy
├── public/                 # Static assets
│   └── assets/            # Images, fonts, icons
│       ├── img/           # Image assets
│       └── fonts/         # Font files
├── redux/                  # Redux state management
│   └── store.js           # Redux store configuration
├── restApis/              # API integration
│   └── API_ENDPOINTS.js   # API endpoint definitions
├── store/                 # Additional store logic
├── styles/                # Global styles
│   ├── globals.css        # Global CSS styles
│   └── Home.module.css    # Home page module styles
├── utils/                 # Utility functions
│   ├── colors.js          # Color constants
│   ├── fonts.js           # Font configurations
│   ├── helper.js          # Helper functions
│   └── toaster.js         # Toast notification utilities
├── hooks/                 # Custom React hooks
├── next.config.js         # Next.js configuration
└── package.json           # Project dependencies and scripts
```

## Architecture Patterns

### 1. Component-Based Architecture

The application follows a component-based architecture where UI is broken down into reusable, self-contained components.

**Component Categories:**
- **Layout Components**: Wrappers that provide consistent structure (header, footer, navigation)
- **Page Components**: Top-level components that represent routes
- **Feature Components**: Specific functionality components (features, stories, downloadApp)
- **UI Components**: Reusable UI elements (buttons, cards, modals)
- **Styled Components**: CSS-in-JS components for consistent styling

### 2. File-Based Routing

Next.js automatic routing based on the `pages/` directory structure:

- `pages/index.js` → `/`
- `pages/about-us/index.js` → `/about-us`
- `pages/doctors/index.js` → `/doctors`
- `pages/subscription-plans/index.js` → `/subscription-plans`

### 3. State Management Pattern

```
User Action → Component → Redux Action → Reducer → Store Update → Component Re-render
```

**Redux Store Structure:**
- Centralized state management
- Redux Thunk for async operations
- Integration with Next.js through next-redux-wrapper

### 4. API Integration Pattern

```javascript
// API endpoints defined in restApis/API_ENDPOINTS.js
export const API_ENDPOINTS = {
  blogsCategory: {
    getAll: "/blogs/viewBlogsCategory",
    getBlogViaCategory: "/blogs/blogsViaCategory",
    getPopularBlogs: "/blogs/popularPosts",
  },
  contactUs: {
    contactUsForm: "/contactUs/contactUsForm",
  },
};
```

Components use Axios to make API calls based on these endpoints.

### 5. Styling Architecture

Multiple styling approaches are used:

1. **Global Styles**: `styles/globals.css` for application-wide styles
2. **CSS Modules**: `styles/Home.module.css` for scoped styles
3. **Styled Components**: Component-specific styles using styled-components
4. **Material-UI Theme**: MUI theming system
5. **Emotion**: Additional CSS-in-JS styling

**Color Management:**
- Centralized in `utils/colors.js`
- Consistent color palette across the application

## Key Components

### Layout Component
Wraps all pages with consistent metadata, SEO, and structure:

```javascript
<Layout
  title="Page Title"
  metaDescription="Description"
  metaKeywords="keywords"
>
  {/* Page content */}
</Layout>
```

### Header Component
Main navigation and hero section with:
- Logo and branding
- Search functionality
- Call-to-action buttons
- Responsive design

### Features Component
Showcases main platform features:
- Subscription Plans
- Lab Tests
- Medical Records

### Footer Components
Multiple footer variations (footer, footer1, footer2, footer3) for different pages.

## Responsive Design

The application uses Material-UI's `useMediaQuery` hook for responsive behavior:

```javascript
const screen1024 = useMediaQuery("(max-width:1024px)");
const screen768 = useMediaQuery("(max-width:768px)");
const screen426 = useMediaQuery("(max-width:426px)");
```

**Breakpoints:**
- Desktop: > 1024px
- Tablet: 768px - 1024px
- Mobile Large: 426px - 768px
- Mobile: < 426px

## Performance Optimizations

### 1. Image Optimization
- Next.js `Image` component for automatic optimization
- Lazy loading of images
- Responsive image serving

### 2. Code Splitting
- Automatic code splitting by Next.js
- Dynamic imports for large components
- Route-based splitting

### 3. Static Generation
- Pre-rendering pages at build time where possible
- Improved initial load performance
- Better SEO

### 4. Bundle Optimization
- Tree shaking to remove unused code
- Minification and compression
- Sharp for image optimization

## Security Considerations

1. **Environment Variables**: Sensitive data stored in environment variables
2. **API Security**: API calls through Axios with proper error handling
3. **Client-Side Validation**: Form validation before submission
4. **Content Security**: Sanitization of user inputs

## Data Flow

### 1. Page Load Flow
```
User Request → Next.js Router → Page Component → Layout → API Calls → Render
```

### 2. User Interaction Flow
```
User Action → Event Handler → State Update (Redux) → Component Re-render
```

### 3. API Call Flow
```
Component → Axios Request → API Endpoint → Response → State Update → UI Update
```

## Development Workflow

1. **Component Development**: Create components in `components/` directory
2. **Page Creation**: Add pages in `pages/` directory for new routes
3. **Styling**: Use styled-components or MUI for styling
4. **State Management**: Use Redux for global state
5. **API Integration**: Define endpoints in `API_ENDPOINTS.js` and use Axios

## Build Process

1. **Development**: `npm run dev` - Hot reloading enabled
2. **Production Build**: `npm run build` - Optimized build
3. **Static Export**: `npm run export` - Generate static HTML
4. **Production Server**: `npm run start` - Run production build

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers (iOS Safari, Chrome Mobile)
- Responsive design for all screen sizes

## Future Architectural Considerations

1. **TypeScript Migration**: Consider adding TypeScript for type safety
2. **Testing Infrastructure**: Add Jest and React Testing Library
3. **API Layer Abstraction**: Create a more robust API service layer
4. **Component Library**: Extract common components into a shared library
5. **Performance Monitoring**: Add performance monitoring tools
6. **Error Tracking**: Implement error tracking service (e.g., Sentry)

## Related Documentation

- [Getting Started](./GETTING_STARTED.md) - Setup and installation
- [Development Guide](./DEVELOPMENT.md) - Development best practices
- [Features](./FEATURES.md) - Feature documentation
- [API Documentation](./API_DOCUMENTATION.md) - API details
