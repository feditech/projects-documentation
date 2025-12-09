# Development Guide

This guide provides information for developers working on HexMate.

## Table of Contents

- [Getting Started](#getting-started)
- [Development Environment](#development-environment)
- [Project Structure](#project-structure)
- [Coding Standards](#coding-standards)
- [Component Development](#component-development)
- [State Management](#state-management)
- [API Integration](#api-integration)
- [Testing](#testing)
- [Debugging](#debugging)
- [Common Development Tasks](#common-development-tasks)

## Getting Started

### Prerequisites

Ensure you have completed the [Installation Guide](INSTALLATION.md) before proceeding.

### Starting Development Server

```bash
npm start
```

The application will start on `http://localhost:3000` with:
- Hot module replacement enabled
- Automatic browser refresh on changes
- Error overlay in browser
- Source maps for debugging

### Development Workflow

1. Create a feature branch: `git checkout -b feature/your-feature-name`
2. Make changes and test locally
3. Run tests: `npm test`
4. Commit changes with descriptive messages
5. Push to remote: `git push origin feature/your-feature-name`
6. Create a pull request

## Development Environment

### Recommended IDE

**Visual Studio Code** with extensions:
- ESLint
- Prettier - Code formatter
- TypeScript Hero
- ES7+ React/Redux/React-Native snippets
- GitLens
- Auto Import

### VS Code Configuration

Create `.vscode/settings.json`:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib",
  "typescript.preferences.importModuleSpecifier": "relative"
}
```

### Browser DevTools

Install browser extensions:
- **React Developer Tools** - Inspect React component tree
- **Redux DevTools** (if using Redux)
- **Axios Inspector** - Monitor API requests

## Project Structure

```
hexmate/
├── public/                 # Static assets
│   ├── Images/            # Image assets
│   ├── fonts/             # Font files
│   ├── dwt-resources/     # Document scanning resources
│   ├── config.json        # Runtime configuration
│   └── index.html         # HTML template
├── src/
│   ├── assets/            # Source assets (images, icons)
│   ├── components/        # Reusable components
│   │   ├── alerts/        # Alert components
│   │   ├── controls/      # Form controls
│   │   ├── editmodals/    # Edit dialogs
│   │   ├── pages/         # Page-specific components
│   │   │   ├── DMS/       # DMS components
│   │   │   ├── VMS/       # VMS components
│   │   │   └── reports/   # Report components
│   │   ├── loadingoverlay/# Loading indicators
│   │   └── route/         # Route components
│   ├── context/           # React Context providers
│   │   ├── authcontext.tsx
│   │   ├── configcontext.tsx
│   │   └── notificationcontext.tsx
│   ├── dwt/               # Document Web TWAIN integration
│   ├── locales/           # i18n translations
│   │   ├── ar/            # Arabic
│   │   └── en/            # English
│   ├── pages/             # Page components
│   │   ├── account/       # Authentication pages
│   │   ├── cts/           # CTS pages
│   │   ├── dms/           # DMS pages
│   │   └── vms/           # VMS pages
│   ├── shared/            # Shared utilities
│   │   ├── hooks/         # Custom hooks
│   │   └── utils/         # Utility functions
│   ├── templates/         # Layout templates
│   ├── App.tsx            # Main app component
│   ├── App.css            # Global styles
│   └── index.tsx          # Entry point
├── docs/                  # Documentation
├── .env                   # Environment variables
├── .gitignore            # Git ignore rules
├── package.json          # Dependencies and scripts
├── tsconfig.json         # TypeScript configuration
└── README.md             # Project readme
```

## Coding Standards

### TypeScript

HexMate uses TypeScript for type safety.

**Type Definitions:**
```typescript
// Define interfaces for data structures
interface User {
  id: number;
  username: string;
  email: string;
  modules?: string;
  isAdmin: boolean;
}

// Use types for component props
type ButtonProps = {
  label: string;
  onClick: () => void;
  disabled?: boolean;
  variant?: 'contained' | 'outlined' | 'text';
};

// Type component props
const CustomButton: React.FC<ButtonProps> = ({ label, onClick, disabled, variant = 'contained' }) => {
  // Component implementation
};
```

**Avoid `any` type:**
```typescript
// ❌ Bad
const handleData = (data: any) => {
  console.log(data);
};

// ✅ Good
const handleData = (data: unknown) => {
  if (typeof data === 'object' && data !== null) {
    console.log(data);
  }
};
```

### React Best Practices

**Functional Components:**
```typescript
// Use functional components with hooks
import React, { useState, useEffect } from 'react';

const MyComponent: React.FC = () => {
  const [data, setData] = useState<DataType[]>([]);
  
  useEffect(() => {
    fetchData();
  }, []);
  
  return <div>{/* JSX */}</div>;
};
```

**Props Destructuring:**
```typescript
// ✅ Good - Destructure props
const UserCard: React.FC<UserProps> = ({ name, email, avatar }) => {
  return (
    <div>
      <img src={avatar} alt={name} />
      <h3>{name}</h3>
      <p>{email}</p>
    </div>
  );
};
```

**Conditional Rendering:**
```typescript
// Use short-circuit evaluation or ternary
return (
  <div>
    {isLoading && <LoadingSpinner />}
    {error ? <ErrorMessage message={error} /> : <ContentView data={data} />}
  </div>
);
```

### Naming Conventions

**Files:**
- Components: `PascalCase.tsx` (e.g., `UserProfile.tsx`)
- Utilities: `camelCase.ts` (e.g., `formatDate.ts`)
- Styles: `lowercase.css` (e.g., `userprofile.css`)

**Variables:**
- Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_FILE_SIZE`)
- Functions: `camelCase` (e.g., `getUserData`)
- Components: `PascalCase` (e.g., `UserProfile`)
- Hooks: `use` prefix (e.g., `useAuth`, `useFormValidation`)

**Booleans:**
```typescript
// Use is/has/can prefix
const isLoading = true;
const hasPermission = false;
const canEdit = true;
```

### Code Formatting

HexMate follows ESLint and Prettier configurations.

**Format code:**
```bash
# Using Prettier (if installed)
npx prettier --write "src/**/*.{ts,tsx}"
```

**Lint code:**
```bash
# Check for linting errors
npm run lint  # if lint script exists

# Or use ESLint directly
npx eslint src/
```

## Component Development

### Creating a New Component

1. **Determine component location:**
   - Shared/reusable → `/src/components/`
   - Page-specific → `/src/pages/[module]/`
   - Module-specific → `/src/components/pages/[MODULE]/`

2. **Create component file:**

```typescript
// src/components/UserAvatar.tsx
import React from 'react';
import { Avatar } from '@mui/material';

interface UserAvatarProps {
  name: string;
  imageUrl?: string;
  size?: 'small' | 'medium' | 'large';
}

const UserAvatar: React.FC<UserAvatarProps> = ({ 
  name, 
  imageUrl, 
  size = 'medium' 
}) => {
  const getInitials = (fullName: string) => {
    return fullName
      .split(' ')
      .map(n => n[0])
      .join('')
      .toUpperCase();
  };

  return (
    <Avatar 
      src={imageUrl} 
      alt={name}
      sx={{ 
        width: size === 'small' ? 32 : size === 'large' ? 64 : 48,
        height: size === 'small' ? 32 : size === 'large' ? 64 : 48,
      }}
    >
      {!imageUrl && getInitials(name)}
    </Avatar>
  );
};

export default UserAvatar;
```

3. **Export from index (if creating a component library):**

```typescript
// src/components/index.ts
export { default as UserAvatar } from './UserAvatar';
export { default as LoadingOverlay } from './loadingoverlay';
```

### Material-UI Integration

HexMate uses Material-UI v5. Follow MUI patterns:

```typescript
import { Button, TextField, Box, Grid } from '@mui/material';

const MyForm: React.FC = () => {
  return (
    <Box sx={{ p: 2 }}>
      <Grid container spacing={2}>
        <Grid item xs={12} md={6}>
          <TextField fullWidth label="Name" />
        </Grid>
        <Grid item xs={12} md={6}>
          <TextField fullWidth label="Email" />
        </Grid>
        <Grid item xs={12}>
          <Button variant="contained" color="primary">
            Submit
          </Button>
        </Grid>
      </Grid>
    </Box>
  );
};
```

## State Management

### Context API

Use React Context for global state:

```typescript
// Create context
import React, { createContext, useContext, useState } from 'react';

interface AppState {
  theme: 'light' | 'dark';
  setTheme: (theme: 'light' | 'dark') => void;
}

const AppContext = createContext<AppState | undefined>(undefined);

// Provider component
export const AppProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [theme, setTheme] = useState<'light' | 'dark'>('light');

  return (
    <AppContext.Provider value={{ theme, setTheme }}>
      {children}
    </AppContext.Provider>
  );
};

// Custom hook
export const useAppContext = () => {
  const context = useContext(AppContext);
  if (!context) {
    throw new Error('useAppContext must be used within AppProvider');
  }
  return context;
};
```

### Local State

Use `useState` for component-local state:

```typescript
const [formData, setFormData] = useState({
  name: '',
  email: '',
});

const handleChange = (field: string, value: string) => {
  setFormData(prev => ({
    ...prev,
    [field]: value
  }));
};
```

## API Integration

### Creating API Functions

```typescript
// src/shared/api/userApi.ts
import axios from 'axios';

const BASE_URL = process.env.REACT_APP_BASE_API;

export const userApi = {
  getUsers: async () => {
    const response = await axios.get(`${BASE_URL}users`);
    return response.data;
  },

  getUserById: async (id: number) => {
    const response = await axios.get(`${BASE_URL}users/${id}`);
    return response.data;
  },

  createUser: async (userData: CreateUserDto) => {
    const response = await axios.post(`${BASE_URL}users`, userData);
    return response.data;
  },

  updateUser: async (id: number, userData: UpdateUserDto) => {
    const response = await axios.put(`${BASE_URL}users/${id}`, userData);
    return response.data;
  },

  deleteUser: async (id: number) => {
    const response = await axios.delete(`${BASE_URL}users/${id}`);
    return response.data;
  },
};
```

### Using in Components

```typescript
import { useState, useEffect } from 'react';
import { userApi } from '../shared/api/userApi';

const UserList: React.FC = () => {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    loadUsers();
  }, []);

  const loadUsers = async () => {
    try {
      setLoading(true);
      const data = await userApi.getUsers();
      setUsers(data);
    } catch (err) {
      setError('Failed to load users');
      console.error(err);
    } finally {
      setLoading(false);
    }
  };

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
};
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run specific test file
npm test -- UserProfile.test.tsx

# Run tests with coverage
npm test -- --coverage

# Run tests in CI mode
CI=true npm test
```

### Writing Tests

```typescript
// UserAvatar.test.tsx
import { render, screen } from '@testing-library/react';
import UserAvatar from './UserAvatar';

describe('UserAvatar', () => {
  it('renders with name', () => {
    render(<UserAvatar name="John Doe" />);
    expect(screen.getByText('JD')).toBeInTheDocument();
  });

  it('renders with image', () => {
    render(<UserAvatar name="John Doe" imageUrl="https://example.com/avatar.jpg" />);
    const avatar = screen.getByAltText('John Doe');
    expect(avatar).toHaveAttribute('src', 'https://example.com/avatar.jpg');
  });
});
```

## Debugging

### React DevTools

1. Install React Developer Tools browser extension
2. Open browser DevTools (F12)
3. Navigate to "Components" or "Profiler" tab
4. Inspect component props, state, and hooks

### Console Logging

```typescript
// Use descriptive console logs
console.log('User data:', userData);
console.error('Failed to fetch:', error);
console.warn('Deprecated API usage');

// Group related logs
console.group('User Login Process');
console.log('Validating credentials...');
console.log('Fetching user data...');
console.groupEnd();
```

### Debugging in VS Code

Create `.vscode/launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "Launch Chrome",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}/src"
    }
  ]
}
```

## Common Development Tasks

### Adding a New Page

1. Create page component in `/src/pages/[module]/`
2. Add route in `App.tsx`
3. Add navigation link in sidebar/menu
4. Update module documentation

### Adding a New API Endpoint

1. Define TypeScript interfaces
2. Create API function in shared/api
3. Add error handling
4. Update API documentation

### Adding Internationalization

1. Add translation keys to locale files
2. Use `useTranslation` hook in components
3. Test with different languages

### Optimizing Performance

- Use `React.memo()` for expensive components
- Implement code splitting with `React.lazy()`
- Use `useMemo()` and `useCallback()` for expensive computations
- Implement virtualization for long lists

## Best Practices

1. **Keep components small** - Single responsibility principle
2. **Use TypeScript** - Type everything properly
3. **Write tests** - Test critical functionality
4. **Handle errors** - Always have error boundaries
5. **Optimize performance** - Profile and optimize
6. **Document code** - Write clear comments
7. **Follow conventions** - Maintain consistency
8. **Review code** - Peer review before merge

## Resources

- [React Documentation](https://react.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Material-UI Documentation](https://mui.com/)
- [React Router Documentation](https://reactrouter.com/)

## Getting Help

- Check [Troubleshooting Guide](TROUBLESHOOTING.md)
- Review existing code examples
- Ask in team chat/Slack
- Create GitHub issue for bugs
