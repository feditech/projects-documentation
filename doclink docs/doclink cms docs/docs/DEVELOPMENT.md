# Development Guide

## Table of Contents

- [Getting Started](#getting-started)
- [Development Environment Setup](#development-environment-setup)
- [Project Structure](#project-structure)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Component Development](#component-development)
- [State Management](#state-management)
- [API Integration](#api-integration)
- [Styling Guidelines](#styling-guidelines)
- [Testing](#testing)
- [Debugging](#debugging)
- [Performance Optimization](#performance-optimization)
- [Git Workflow](#git-workflow)
- [Contributing](#contributing)

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js**: v14.0.0 or higher (LTS recommended)
- **npm**: v6.0.0 or higher (or yarn 1.22.0+)
- **Git**: Latest version
- **Code Editor**: VS Code (recommended) with extensions:
  - ESLint
  - Prettier
  - ES7+ React/Redux/React-Native snippets
  - Auto Import
  - GitLens

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/feditech/doclink-cms-updated.git
cd doclink-cms-updated
```

2. **Install dependencies:**
```bash
npm install
```

If you encounter peer dependency warnings, use:
```bash
npm install --legacy-peer-deps
```

3. **Environment Configuration:**

Create a `.env` file in the root directory:
```env
# API Configuration
REACT_APP_API_BASE_URL=http://localhost:5000/api/v1
REACT_APP_API_TIMEOUT=30000

# Google Maps API
REACT_APP_GOOGLE_MAPS_API_KEY=your_google_maps_api_key

# Environment
REACT_APP_ENV=development

# Feature Flags (optional)
REACT_APP_ENABLE_LOGGER=true
REACT_APP_ENABLE_REDUX_DEVTOOLS=true
```

4. **Start development server:**
```bash
npm start
```

The application will open at `http://localhost:3000`.

## Development Environment Setup

### VS Code Configuration

Create `.vscode/settings.json`:
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "javascript.updateImportsOnFileMove.enabled": "always",
  "eslint.validate": [
    "javascript",
    "javascriptreact"
  ]
}
```

### Recommended VS Code Extensions

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "dsznajder.es7-react-js-snippets",
    "steoates.autoimport",
    "eamodio.gitlens",
    "formulahendry.auto-rename-tag",
    "christian-kohler.path-intellisense"
  ]
}
```

## Project Structure

```
doclink-cms-updated/
├── public/                     # Static files
│   ├── index.html             # HTML template
│   ├── favicon.ico            # App icon
│   └── manifest.json          # PWA manifest
├── src/
│   ├── api/                   # API configuration
│   │   ├── index.js          # Axios instance
│   │   └── endPoints.js      # API endpoints
│   ├── assets/               # Static assets
│   │   ├── images/          # Images
│   │   ├── icons/           # Icon files
│   │   └── fonts/           # Font files
│   ├── components/          # Reusable components
│   │   ├── Table/          # Table components
│   │   ├── Calendar/       # Calendar component
│   │   └── ...
│   ├── hooks/              # Custom React hooks
│   ├── redux/              # Redux store and slices
│   │   ├── store.js       # Store configuration
│   │   └── slices/        # Feature slices
│   ├── screens/           # Page components
│   │   ├── authorized/   # Protected pages
│   │   └── unauthorized/ # Public pages
│   ├── utils/            # Utility functions
│   ├── App.js            # Main App component
│   ├── App.css           # Global styles
│   ├── index.js          # Entry point
│   ├── menu.js           # Menu component
│   └── menuitems.js      # Menu configuration
├── .babelrc              # Babel configuration
├── .eslintrc             # ESLint configuration (if exists)
├── .prettierrc           # Prettier configuration
├── .gitignore           # Git ignore rules
├── package.json         # Dependencies
└── webpack.config.js    # Webpack configuration
```

## Development Workflow

### 1. Starting a New Feature

```bash
# Create a new branch
git checkout -b feature/feature-name

# Make your changes
# ...

# Test your changes
npm start

# Commit your changes
git add .
git commit -m "feat: add feature description"

# Push to remote
git push origin feature/feature-name

# Create a Pull Request
```

### 2. Daily Development

```bash
# Update your local repository
git pull origin main

# Start development server
npm start

# Run in parallel (optional)
# Terminal 1: npm start
# Terminal 2: npm test -- --watch
```

## Coding Standards

### JavaScript/React Best Practices

#### 1. Component Structure

```javascript
// Import external libraries
import React, { useState, useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';

// Import Material-UI components
import { Button, TextField } from '@mui/material';

// Import local components
import CustomComponent from './CustomComponent';

// Import utilities
import { formatDate } from '../../utils/helpers';

// Import styles
import { Container } from './styledComponents';

// Component definition
const MyComponent = ({ propName }) => {
  // Hooks
  const dispatch = useDispatch();
  const state = useSelector(state => state.feature);
  const [localState, setLocalState] = useState(null);

  // Effects
  useEffect(() => {
    // Effect logic
  }, []);

  // Event handlers
  const handleClick = () => {
    // Handler logic
  };

  // Render
  return (
    <Container>
      {/* JSX */}
    </Container>
  );
};

export default MyComponent;
```

#### 2. Naming Conventions

- **Components**: PascalCase (`MyComponent`)
- **Files**: PascalCase for components (`MyComponent.js`)
- **Variables/Functions**: camelCase (`myVariable`, `handleClick`)
- **Constants**: UPPER_SNAKE_CASE (`API_BASE_URL`)
- **CSS Classes**: kebab-case or camelCase (consistent with styled-components)

#### 3. Props and PropTypes

```javascript
import PropTypes from 'prop-types';

const MyComponent = ({ title, data, onSubmit }) => {
  // Component logic
};

MyComponent.propTypes = {
  title: PropTypes.string.isRequired,
  data: PropTypes.array,
  onSubmit: PropTypes.func.isRequired,
};

MyComponent.defaultProps = {
  data: [],
};

export default MyComponent;
```

### ESLint Rules

The project follows Airbnb's ESLint configuration with custom overrides:

```javascript
// .eslintrc (if you need to create one)
{
  "extends": [
    "react-app",
    "airbnb",
    "prettier"
  ],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
    "react/prop-types": "warn",
    "no-console": "warn",
    "import/prefer-default-export": "off"
  }
}
```

### Prettier Configuration

```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2
}
```

## Component Development

### Creating a New Component

1. **Create component directory:**
```bash
mkdir -p src/components/NewComponent
```

2. **Create component files:**
```
NewComponent/
├── index.js              # Main component
├── styledComponents.js   # Styled components (if using)
├── NewComponent.test.js  # Tests (optional)
└── README.md            # Component documentation (optional)
```

3. **Component template:**

```javascript
// src/components/NewComponent/index.js
import React from 'react';
import { Container } from './styledComponents';

const NewComponent = ({ children }) => {
  return <Container>{children}</Container>;
};

export default NewComponent;
```

### Reusable Component Guidelines

- Keep components small and focused
- Use composition over inheritance
- Extract complex logic into custom hooks
- Document props and usage
- Make components configurable through props
- Avoid hardcoding values

### Example: Reusable Table Component

```javascript
import React from 'react';
import MaterialTable from '@material-table/core';

const DataTable = ({ 
  title,
  columns,
  data,
  onAdd,
  onEdit,
  onDelete,
  actions = []
}) => {
  return (
    <MaterialTable
      title={title}
      columns={columns}
      data={data}
      actions={[
        {
          icon: 'add',
          tooltip: 'Add',
          isFreeAction: true,
          onClick: onAdd,
        },
        ...actions,
      ]}
      editable={{
        onRowUpdate: onEdit,
        onRowDelete: onDelete,
      }}
      options={{
        actionsColumnIndex: -1,
        pageSize: 10,
      }}
    />
  );
};

export default DataTable;
```

## State Management

### Redux Slice Structure

```javascript
// src/redux/slices/feature/index.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  data: [],
  loading: false,
  error: null,
};

const featureSlice = createSlice({
  name: 'feature',
  initialState,
  reducers: {
    setData: (state, action) => {
      state.data = action.payload;
    },
    setLoading: (state, action) => {
      state.loading = action.payload;
    },
    setError: (state, action) => {
      state.error = action.payload;
    },
  },
});

export const { setData, setLoading, setError } = featureSlice.actions;
export default featureSlice.reducer;
```

### Using Redux in Components

```javascript
import { useDispatch, useSelector } from 'react-redux';
import { setData, setLoading } from '../../redux/slices/feature';

const MyComponent = () => {
  const dispatch = useDispatch();
  const { data, loading } = useSelector(state => state.feature);

  const fetchData = async () => {
    dispatch(setLoading(true));
    try {
      const response = await Api.get('/endpoint');
      dispatch(setData(response.data));
    } catch (error) {
      console.error(error);
    } finally {
      dispatch(setLoading(false));
    }
  };

  return (
    // Component JSX
  );
};
```

## API Integration

### Making API Calls

```javascript
import { Api } from '../../api';
import { endPoints } from '../../api/endPoints';

// GET request
const fetchData = async () => {
  try {
    const response = await Api.get(endPoints.doctor.getAll);
    return response.data;
  } catch (error) {
    throw error;
  }
};

// POST request
const createData = async (data) => {
  try {
    const response = await Api.post(endPoints.doctor.create, data);
    return response.data;
  } catch (error) {
    throw error;
  }
};

// PUT request
const updateData = async (id, data) => {
  try {
    const response = await Api.put(`${endPoints.doctor.edit}/${id}`, data);
    return response.data;
  } catch (error) {
    throw error;
  }
};

// DELETE request
const deleteData = async (id) => {
  try {
    const response = await Api.delete(`${endPoints.doctor.delete}/${id}`);
    return response.data;
  } catch (error) {
    throw error;
  }
};
```

### Adding New Endpoints

1. Add to `src/api/endPoints.js`:
```javascript
export const endPoints = {
  // ... existing endpoints
  newFeature: {
    getAll: '/new-feature/get-all',
    create: '/new-feature/create',
    edit: '/new-feature/edit',
    delete: '/new-feature/delete',
  },
};
```

## Styling Guidelines

### Using Styled Components

```javascript
import styled from 'styled-components';

export const Container = styled.div`
  display: flex;
  flex-direction: column;
  padding: ${props => props.padding || '1rem'};
  background-color: ${props => props.theme.background};
  
  @media (max-width: 768px) {
    padding: 0.5rem;
  }
`;

export const Title = styled.h1`
  font-size: 2rem;
  color: ${props => props.color || '#333'};
  margin-bottom: 1rem;
`;
```

### Using Material-UI

```javascript
import { makeStyles } from '@mui/styles';

const useStyles = makeStyles((theme) => ({
  root: {
    padding: theme.spacing(2),
    backgroundColor: theme.palette.background.paper,
  },
  button: {
    margin: theme.spacing(1),
  },
}));

const MyComponent = () => {
  const classes = useStyles();
  
  return (
    <div className={classes.root}>
      <Button className={classes.button}>Click Me</Button>
    </div>
  );
};
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm test -- --watch

# Run tests with coverage
npm test -- --coverage
```

### Writing Tests

```javascript
import { render, screen, fireEvent } from '@testing-library/react';
import MyComponent from './MyComponent';

describe('MyComponent', () => {
  test('renders correctly', () => {
    render(<MyComponent />);
    expect(screen.getByText('Hello')).toBeInTheDocument();
  });

  test('handles click event', () => {
    const handleClick = jest.fn();
    render(<MyComponent onClick={handleClick} />);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
});
```

## Debugging

### React DevTools

1. Install React DevTools browser extension
2. Open DevTools
3. Navigate to Components or Profiler tab

### Redux DevTools

1. Install Redux DevTools extension
2. View state changes in real-time
3. Time-travel debugging

### Console Logging

```javascript
// Development only
if (process.env.NODE_ENV === 'development') {
  console.log('Debug info:', data);
}
```

### Network Debugging

Use browser DevTools Network tab to inspect:
- API requests/responses
- Request headers
- Response times
- Error responses

## Performance Optimization

### Code Splitting

```javascript
import React, { lazy, Suspense } from 'react';

const LazyComponent = lazy(() => import('./LazyComponent'));

const MyComponent = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);
```

### Memoization

```javascript
import React, { useMemo, useCallback } from 'react';

const MyComponent = ({ data }) => {
  const expensiveValue = useMemo(() => {
    return computeExpensiveValue(data);
  }, [data]);

  const handleClick = useCallback(() => {
    // Handle click
  }, []);

  return <div>{expensiveValue}</div>;
};
```

## Git Workflow

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Example:**
```
feat(doctor): add doctor profile edit functionality

- Add edit button to doctor profile
- Implement edit form with validation
- Update API integration

Closes #123
```

### Branch Naming

- `feature/feature-name`: New features
- `fix/bug-description`: Bug fixes
- `refactor/description`: Code refactoring
- `docs/description`: Documentation updates

## Contributing

1. Fork the repository
2. Create your feature branch
3. Make your changes
4. Write/update tests
5. Ensure all tests pass
6. Update documentation
7. Commit your changes
8. Push to your fork
9. Create a Pull Request

### Pull Request Checklist

- [ ] Code follows project style guidelines
- [ ] Tests are written and passing
- [ ] Documentation is updated
- [ ] No console errors or warnings
- [ ] Changes are reviewed and approved
- [ ] Commits are properly formatted

---

For questions or issues, please contact the development team or create an issue in the repository.
