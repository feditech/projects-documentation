# Development Guide

This guide provides comprehensive information for developers working on the DocLink web application.

## Table of Contents

- [Development Environment Setup](#development-environment-setup)
- [Project Structure](#project-structure)
- [Development Workflow](#development-workflow)
- [Component Development](#component-development)
- [State Management](#state-management)
- [API Integration](#api-integration)
- [Styling Guidelines](#styling-guidelines)
- [Testing](#testing)
- [Debugging](#debugging)
- [Performance Optimization](#performance-optimization)
- [Best Practices](#best-practices)
- [Common Tasks](#common-tasks)
- [Troubleshooting](#troubleshooting)

## Development Environment Setup

### Required Tools

1. **Node.js & npm**
   ```bash
   node --version  # v14.x or higher
   npm --version   # v6.x or higher
   ```

2. **Git**
   ```bash
   git --version
   ```

3. **Code Editor**
   - VS Code (recommended)
   - WebStorm
   - Sublime Text

### VS Code Extensions

Recommended extensions for DocLink development:

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "bradlc.vscode-tailwindcss",
    "styled-components.vscode-styled-components",
    "ms-vscode.vscode-typescript-next"
  ]
}
```

### Initial Setup

```bash
# Clone repository
git clone https://github.com/feditech/doclink-web.git
cd doclink-web

# Install dependencies
npm install

# Create environment file
cp .env.example .env.local

# Start development server
npm run dev
```

## Project Structure

### Directory Overview

```
doclink-web/
├── components/           # React components
│   ├── header/          # Header components
│   ├── footer/          # Footer variations
│   ├── home/            # Home page components
│   ├── styledComponent/ # Shared styled components
│   └── [feature]/       # Feature-specific components
├── pages/               # Next.js pages (routes)
│   ├── _app.js         # Custom App component
│   ├── _document.js    # Custom Document
│   ├── index.js        # Home page
│   └── [route]/        # Other pages
├── public/              # Static assets
│   └── assets/         # Images, fonts, icons
├── redux/               # Redux store
├── restApis/            # API configurations
├── styles/              # Global styles
├── utils/               # Utility functions
└── docs/                # Documentation
```

### Component Organization

Each major component follows this structure:

```
components/
└── FeatureName/
    ├── FeatureName.js           # Main component
    ├── SubComponent.js          # Related sub-components
    └── styledComponent/
        └── index.js             # Styled components
```

## Development Workflow

### Daily Workflow

1. **Start Development Server**
   ```bash
   npm run dev
   ```

2. **Create Feature Branch**
   ```bash
   git checkout -b feature/new-feature
   ```

3. **Make Changes**
   - Write code
   - Test locally
   - Check for errors

4. **Test Changes**
   ```bash
   npm run lint    # Check code style
   npm run build   # Test build
   ```

5. **Commit Changes**
   ```bash
   git add .
   git commit -m "feat: add new feature"
   ```

6. **Push and Create PR**
   ```bash
   git push origin feature/new-feature
   ```

### Hot Reloading

Next.js provides automatic hot reloading:
- Save file → Browser refreshes automatically
- React Fast Refresh preserves component state
- CSS changes apply instantly

## Component Development

### Creating a New Component

#### 1. Functional Component Template

```javascript
import { useState, useEffect } from 'react';
import { Container } from '@mui/material';
import PropTypes from 'prop-types';
import { Wrapper, Title } from './styledComponent';

/**
 * ComponentName - Brief description
 * @param {Object} props - Component props
 */
const ComponentName = ({ title, data, onAction }) => {
  // State
  const [localState, setLocalState] = useState(null);

  // Effects
  useEffect(() => {
    // Side effects
    return () => {
      // Cleanup
    };
  }, []);

  // Handlers
  const handleClick = () => {
    onAction?.();
  };

  // Render
  return (
    <Container maxWidth="lg">
      <Wrapper>
        <Title>{title}</Title>
        {/* Component content */}
      </Wrapper>
    </Container>
  );
};

// PropTypes
ComponentName.propTypes = {
  title: PropTypes.string.isRequired,
  data: PropTypes.array,
  onAction: PropTypes.func,
};

// Default Props
ComponentName.defaultProps = {
  data: [],
  onAction: null,
};

export default ComponentName;
```

#### 2. Styled Components

```javascript
// components/ComponentName/styledComponent/index.js
import styled from 'styled-components';
import colors from '../../../utils/colors';

const { colorPrimary, colorWhite } = colors;

export const Wrapper = styled.div`
  padding: 2rem;
  background-color: ${colorWhite};
  
  @media (max-width: 768px) {
    padding: 1rem;
  }
`;

export const Title = styled.h1`
  color: ${colorPrimary};
  font-size: 2.5rem;
  margin-bottom: 1rem;
  
  @media (max-width: 768px) {
    font-size: 1.8rem;
  }
`;
```

### Responsive Design

Use Material-UI's `useMediaQuery` hook:

```javascript
import { useMediaQuery } from '@mui/material';

const Component = () => {
  const isMobile = useMediaQuery('(max-width:768px)');
  const isTablet = useMediaQuery('(max-width:1024px)');
  const isDesktop = useMediaQuery('(min-width:1025px)');

  return (
    <div>
      {isMobile && <MobileView />}
      {isTablet && !isMobile && <TabletView />}
      {isDesktop && <DesktopView />}
    </div>
  );
};
```

### Creating Pages

Pages are automatically routed based on file structure:

```javascript
// pages/new-page/index.js
import Layout from '../../components/layout/Layout';
import Header from '../../components/newPage/Header';
import Content from '../../components/newPage/Content';

const NewPage = () => {
  return (
    <Layout
      title="New Page - DocLink"
      metaDescription="Page description"
      metaKeywords="keywords, here"
    >
      <Header />
      <Content />
    </Layout>
  );
};

export default NewPage;
```

## State Management

### Redux Setup

Current store structure:

```javascript
// redux/store.js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import { composeWithDevTools } from 'redux-devtools-extension';

const store = createStore(
  rootReducer,
  composeWithDevTools(applyMiddleware(thunk))
);

export default store;
```

### Using Redux in Components

```javascript
import { useDispatch, useSelector } from 'react-redux';
import { fetchData } from '../redux/actions';

const Component = () => {
  const dispatch = useDispatch();
  const data = useSelector(state => state.data);

  useEffect(() => {
    dispatch(fetchData());
  }, [dispatch]);

  return <div>{/* Use data */}</div>;
};
```

### Local State vs Redux

**Use Local State for:**
- UI state (modals, dropdowns)
- Form inputs
- Component-specific data

**Use Redux for:**
- User authentication
- Global app settings
- Shared data across components

## API Integration

### API Configuration

```javascript
// restApis/API_ENDPOINTS.js
export const API_ENDPOINTS = {
  blogs: {
    getAll: "/blogs/viewBlogsCategory",
    getByCategory: "/blogs/blogsViaCategory",
    getPopular: "/blogs/popularPosts",
  },
  users: {
    login: "/auth/login",
    register: "/auth/register",
  },
};
```

### Making API Calls

```javascript
import axios from 'axios';
import { API_ENDPOINTS } from '../restApis/API_ENDPOINTS';

const baseURL = process.env.NEXT_PUBLIC_API_BASE_URL;

// GET request
const fetchBlogs = async () => {
  try {
    const response = await axios.get(
      `${baseURL}${API_ENDPOINTS.blogs.getAll}`
    );
    return response.data;
  } catch (error) {
    console.error('Error fetching blogs:', error);
    throw error;
  }
};

// POST request
const submitForm = async (data) => {
  try {
    const response = await axios.post(
      `${baseURL}${API_ENDPOINTS.contactUs.submit}`,
      data,
      {
        headers: {
          'Content-Type': 'application/json',
        },
      }
    );
    return response.data;
  } catch (error) {
    console.error('Error submitting form:', error);
    throw error;
  }
};
```

### Error Handling

```javascript
import { toast } from 'react-hot-toast';

const handleAPIError = (error) => {
  if (error.response) {
    // Server responded with error
    toast.error(error.response.data.message || 'An error occurred');
  } else if (error.request) {
    // Request made but no response
    toast.error('Network error. Please check your connection.');
  } else {
    // Other errors
    toast.error('An unexpected error occurred');
  }
};
```

## Styling Guidelines

### Color System

```javascript
// utils/colors.js
const colors = {
  colorPrimary: '#1976d2',
  colorSecondary: '#dc004e',
  colorWhite: '#ffffff',
  colorBlack: '#000000',
  colorGray: '#757575',
  // ... more colors
};

export default colors;
```

### Using Colors

```javascript
import colors from '../../utils/colors';

const { colorPrimary, colorWhite } = colors;

const Button = styled.button`
  background-color: ${colorPrimary};
  color: ${colorWhite};
`;
```

### Material-UI Theming

```javascript
import { createTheme, ThemeProvider } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      main: '#1976d2',
    },
    secondary: {
      main: '#dc004e',
    },
  },
});

// In _app.js
<ThemeProvider theme={theme}>
  <Component {...pageProps} />
</ThemeProvider>
```

## Testing

### Manual Testing Checklist

Before committing:

- [ ] Test on Chrome, Firefox, Safari
- [ ] Test on mobile viewport (375px, 768px)
- [ ] Test on tablet viewport (1024px)
- [ ] Test on desktop (1440px+)
- [ ] Check console for errors
- [ ] Test with slow 3G throttling
- [ ] Verify accessibility (tab navigation)
- [ ] Check print styles

### Browser DevTools

**Chrome DevTools:**
```
F12 or Cmd+Option+I (Mac)
```

**Useful Features:**
- Elements panel for CSS debugging
- Console for JavaScript errors
- Network tab for API calls
- Lighthouse for performance audit
- Device toolbar for responsive testing

## Debugging

### Console Logging

```javascript
// Development only logs
if (process.env.NODE_ENV === 'development') {
  console.log('Debug info:', data);
}
```

### React DevTools

Install React DevTools browser extension:
- Inspect component hierarchy
- View props and state
- Track component renders

### Redux DevTools

View Redux state and actions:
- Time-travel debugging
- Action history
- State snapshots

### Common Debug Scenarios

**Component not rendering:**
```javascript
console.log('Props:', props);
console.log('State:', state);
```

**API call failing:**
```javascript
console.log('Request URL:', url);
console.log('Request data:', data);
console.log('Response:', response);
```

## Performance Optimization

### Image Optimization

```javascript
import Image from 'next/image';

<Image
  src="/assets/img/hero.jpg"
  alt="Hero image"
  width={1200}
  height={600}
  priority // For above-fold images
  placeholder="blur" // Optional blur-up
/>
```

### Code Splitting

```javascript
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(
  () => import('../components/HeavyComponent'),
  { loading: () => <Loading /> }
);
```

### Memoization

```javascript
import { memo, useMemo, useCallback } from 'react';

// Memo component
const ExpensiveComponent = memo(({ data }) => {
  return <div>{/* Render */}</div>;
});

// Memo value
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(data);
}, [data]);

// Memo callback
const handleClick = useCallback(() => {
  // Handle click
}, [dependency]);
```

## Best Practices

### Code Quality

1. **Use ESLint**: `npm run lint`
2. **Consistent naming**: camelCase for variables, PascalCase for components
3. **DRY principle**: Don't Repeat Yourself
4. **Single Responsibility**: One component, one purpose
5. **Meaningful names**: `getUserData` not `getData`

### Component Best Practices

```javascript
// ✅ Good
const UserProfile = ({ user }) => {
  if (!user) return null;
  
  return <div>{user.name}</div>;
};

// ❌ Avoid
const UserProfile = ({ user }) => {
  return user ? <div>{user.name}</div> : null;
};
```

### Performance Best Practices

- Avoid inline functions in render
- Use React.memo for expensive components
- Lazy load images
- Code split large components
- Optimize bundle size

## Common Tasks

### Adding a New Page

1. Create page file: `pages/new-page/index.js`
2. Create components: `components/newPage/`
3. Add navigation link if needed
4. Update sitemap

### Adding a New Feature

1. Create feature components
2. Add to appropriate page
3. Update API endpoints if needed
4. Add to documentation
5. Test thoroughly

### Updating Styles

1. Locate styled component or CSS file
2. Make changes
3. Test across breakpoints
4. Verify browser compatibility

### Adding Dependencies

```bash
# Check for security vulnerabilities first
npm audit

# Install package
npm install package-name

# Update package.json
npm install --save package-name
```

## Troubleshooting

### Build Errors

**Error: Module not found**
```bash
# Clear cache and reinstall
rm -rf node_modules .next
npm install
```

**Error: Port 3000 already in use**
```bash
# Find and kill process
lsof -ti:3000 | xargs kill
# Or use different port
PORT=3001 npm run dev
```

### Runtime Errors

**Hydration errors:**
- Ensure server and client render same HTML
- Check for browser-only APIs in SSR
- Verify date/time consistency

**Memory leaks:**
- Clean up event listeners in useEffect
- Cancel pending API calls on unmount
- Clear intervals and timeouts

### Style Issues

**Styles not applying:**
- Check CSS specificity
- Verify styled-components syntax
- Clear .next cache
- Check import paths

## Related Documentation

- [Getting Started](./GETTING_STARTED.md)
- [Architecture](./ARCHITECTURE.md)
- [Contributing](./CONTRIBUTING.md)
- [API Documentation](./API_DOCUMENTATION.md)
