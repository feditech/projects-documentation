# Contributing to Siraj Admin Panel

Thank you for your interest in contributing to Siraj Admin Panel! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Component Guidelines](#component-guidelines)
- [Testing Guidelines](#testing-guidelines)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Pull Request Process](#pull-request-process)
- [Code Review](#code-review)
- [Issue Reporting](#issue-reporting)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of experience level, background, or identity.

### Expected Behavior

- Use welcoming and inclusive language
- Be respectful of differing viewpoints and experiences
- Gracefully accept constructive criticism
- Focus on what is best for the community
- Show empathy towards other community members

### Unacceptable Behavior

- Harassment, discrimination, or offensive comments
- Trolling, insulting/derogatory comments, and personal attacks
- Publishing others' private information without permission
- Other conduct which could reasonably be considered inappropriate

## Getting Started

### Prerequisites

Before contributing, ensure you have:

- Node.js 18.x or higher
- npm 8.x or higher
- Git
- Code editor (VS Code recommended)
- Basic knowledge of React, JavaScript, and Ant Design

### Setting Up Development Environment

1. **Fork the Repository**

```bash
# Fork via GitHub UI, then clone your fork
git clone https://github.com/YOUR_USERNAME/siraj-fe-admin.git
cd siraj-fe-admin
```

2. **Add Upstream Remote**

```bash
git remote add upstream https://github.com/feditech/siraj-fe-admin.git
```

3. **Install Dependencies**

```bash
npm install
```

4. **Configure Environment**

```bash
cp .env.example .env
# Edit .env with your configuration
```

5. **Start Development Server**

```bash
npm start
```

### Project Structure Familiarization

Review the project structure in [README.md](./README.md) to understand:
- Component organization
- Service layer architecture
- Routing structure
- Context providers

## Development Workflow

### 1. Sync with Upstream

Always sync your fork before starting new work:

```bash
git checkout main
git fetch upstream
git merge upstream/main
git push origin main
```

### 2. Create Feature Branch

```bash
# Use descriptive branch names
git checkout -b feature/add-export-functionality
git checkout -b fix/product-form-validation
git checkout -b docs/update-api-documentation
```

Branch naming conventions:
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `refactor/` - Code refactoring
- `test/` - Adding or updating tests
- `chore/` - Maintenance tasks

### 3. Make Changes

Follow the [Coding Standards](#coding-standards) and [Component Guidelines](#component-guidelines).

### 4. Test Your Changes

```bash
# Run tests
npm test

# Run linter
npm run lint

# Build to ensure no errors
npm run build
```

### 5. Commit Changes

Follow [Commit Message Guidelines](#commit-message-guidelines):

```bash
git add .
git commit -m "feat: add CSV export for products"
```

### 6. Push to Your Fork

```bash
git push origin feature/add-export-functionality
```

### 7. Create Pull Request

- Go to your fork on GitHub
- Click "Pull Request"
- Select your feature branch
- Fill in the PR template
- Submit for review

## Coding Standards

### JavaScript/React Style

#### 1. Use Functional Components

```javascript
// ✅ Good - Functional component with hooks
function ProductList() {
  const [products, setProducts] = useState([]);
  
  useEffect(() => {
    fetchProducts();
  }, []);
  
  return <div>{/* JSX */}</div>;
}

// ❌ Bad - Class component
class ProductList extends Component {
  // ...
}
```

#### 2. Destructure Props

```javascript
// ✅ Good
function Button({ text, onClick, loading }) {
  return <button onClick={onClick}>{loading ? 'Loading...' : text}</button>;
}

// ❌ Bad
function Button(props) {
  return <button onClick={props.onClick}>{props.text}</button>;
}
```

#### 3. Use Meaningful Variable Names

```javascript
// ✅ Good
const activeProducts = products.filter(product => product.status === 'active');
const userFullName = `${user.firstName} ${user.lastName}`;

// ❌ Bad
const ap = products.filter(p => p.status === 'active');
const name = `${user.firstName} ${user.lastName}`;
```

#### 4. Keep Functions Small

```javascript
// ✅ Good - Single responsibility
const validateEmail = (email) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};

const handleSubmit = async (formData) => {
  if (!validateEmail(formData.email)) {
    showError('Invalid email');
    return;
  }
  await submitForm(formData);
};

// ❌ Bad - Does too much
const handleSubmit = async (formData) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(formData.email)) {
    notification.error({ message: 'Invalid email' });
    return;
  }
  try {
    const response = await axios.post('/api/submit', formData);
    notification.success({ message: 'Success' });
  } catch (error) {
    notification.error({ message: 'Error' });
  }
};
```

#### 5. Use Constants for Magic Values

```javascript
// ✅ Good
const MAX_RETRY_ATTEMPTS = 3;
const API_TIMEOUT_MS = 5000;

if (retryCount >= MAX_RETRY_ATTEMPTS) {
  throw new Error('Max retries exceeded');
}

// ❌ Bad
if (retryCount >= 3) {
  throw new Error('Max retries exceeded');
}
```

### File Organization

#### Component File Structure

```javascript
// ProductCard.js
import React, { useState } from 'react';
import { Card, Button } from 'antd';
import PropTypes from 'prop-types';
import './ProductCard.css'; // Component-specific styles

/**
 * ProductCard displays product information in a card format
 * @param {Object} product - Product data object
 * @param {Function} onEdit - Callback when edit button is clicked
 */
function ProductCard({ product, onEdit }) {
  const [loading, setLoading] = useState(false);
  
  const handleEdit = async () => {
    setLoading(true);
    try {
      await onEdit(product.id);
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <Card title={product.title}>
      <p>{product.description}</p>
      <Button loading={loading} onClick={handleEdit}>
        Edit
      </Button>
    </Card>
  );
}

ProductCard.propTypes = {
  product: PropTypes.shape({
    id: PropTypes.number.isRequired,
    title: PropTypes.string.isRequired,
    description: PropTypes.string
  }).isRequired,
  onEdit: PropTypes.func.isRequired
};

export default ProductCard;
```

#### Service File Structure

```javascript
// src/services/product/index.js
import axiosClient from '../base';

/**
 * Fetches all products from the API
 * @returns {Promise<Object>} Response containing product array
 */
export const getProducts = () => {
  return axiosClient.get('products');
};

/**
 * Updates a product by ID
 * @param {Object} productData - Product data to update
 * @param {number} productData.id - Product ID
 * @param {string} productData.title - Product title
 * @returns {Promise<Object>} Response containing updated product
 */
export const updateProduct = (productData) => {
  const { id, ...data } = productData;
  return axiosClient.put(`products/${id}`, data);
};
```

### CSS/Styling

#### 1. Use CSS Modules or Styled Components (if applicable)

```css
/* ProductCard.module.css */
.card {
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.cardTitle {
  font-size: 18px;
  font-weight: 600;
  color: #00B4DE;
}
```

```javascript
import styles from './ProductCard.module.css';

<Card className={styles.card}>
  <h2 className={styles.cardTitle}>{title}</h2>
</Card>
```

#### 2. Follow BEM Naming Convention (for regular CSS)

```css
/* ✅ Good */
.product-card { }
.product-card__title { }
.product-card__title--highlighted { }

/* ❌ Bad */
.productCard { }
.title { }
.highlighted { }
```

#### 3. Use Ant Design Theme Variables

```javascript
// App.js
<ConfigProvider
  theme={{
    components: {
      Button: {
        colorPrimary: '#00B4DE',
      }
    }
  }}
>
  {/* App content */}
</ConfigProvider>
```

## Component Guidelines

### Creating New Components

1. **Create component directory**

```
src/common/components/ProductCard/
├── index.js
├── ProductCard.js
├── ProductCard.test.js
└── ProductCard.module.css
```

2. **Implement component with proper structure**

```javascript
// ProductCard.js
import React from 'react';
import PropTypes from 'prop-types';

function ProductCard({ product, onEdit, onDelete }) {
  // Hooks at the top
  const [loading, setLoading] = useState(false);
  
  // Event handlers
  const handleEdit = () => {
    onEdit(product.id);
  };
  
  const handleDelete = async () => {
    setLoading(true);
    try {
      await onDelete(product.id);
    } finally {
      setLoading(false);
    }
  };
  
  // Render helpers (if complex)
  const renderActions = () => (
    <div>
      <Button onClick={handleEdit}>Edit</Button>
      <Button loading={loading} onClick={handleDelete}>Delete</Button>
    </div>
  );
  
  // Main render
  return (
    <Card>
      <h3>{product.title}</h3>
      {renderActions()}
    </Card>
  );
}

ProductCard.propTypes = {
  product: PropTypes.object.isRequired,
  onEdit: PropTypes.func.isRequired,
  onDelete: PropTypes.func.isRequired
};

export default ProductCard;
```

3. **Export from index.js**

```javascript
// index.js
export { default } from './ProductCard';
```

### Component Reusability

Create reusable components in `src/common/components/`:

```
src/common/components/
├── Button/
├── Modal/
├── Table/
├── Form/
└── Icon/
```

Page-specific components go in respective page directories:

```
src/pages/dashboard/components/
├── ProductManagement/
├── UserManagement/
└── ...
```

## Testing Guidelines

### Writing Tests

#### Component Tests

```javascript
// ProductCard.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import ProductCard from './ProductCard';

describe('ProductCard', () => {
  const mockProduct = {
    id: 1,
    title: 'Test Product',
    description: 'Test description'
  };
  
  const mockOnEdit = jest.fn();
  const mockOnDelete = jest.fn();
  
  beforeEach(() => {
    jest.clearAllMocks();
  });
  
  test('renders product information', () => {
    render(
      <ProductCard 
        product={mockProduct} 
        onEdit={mockOnEdit} 
        onDelete={mockOnDelete} 
      />
    );
    
    expect(screen.getByText('Test Product')).toBeInTheDocument();
    expect(screen.getByText('Test description')).toBeInTheDocument();
  });
  
  test('calls onEdit when edit button is clicked', () => {
    render(
      <ProductCard 
        product={mockProduct} 
        onEdit={mockOnEdit} 
        onDelete={mockOnDelete} 
      />
    );
    
    fireEvent.click(screen.getByText('Edit'));
    expect(mockOnEdit).toHaveBeenCalledWith(1);
  });
});
```

#### Service Tests

```javascript
// product.test.js
import { getProducts, updateProduct } from './product';
import axiosClient from '../base';

jest.mock('../base');

describe('Product Service', () => {
  test('getProducts calls API correctly', async () => {
    const mockData = { data: [{ id: 1, title: 'Product' }] };
    axiosClient.get.mockResolvedValue(mockData);
    
    const result = await getProducts();
    
    expect(axiosClient.get).toHaveBeenCalledWith('products');
    expect(result).toEqual(mockData);
  });
  
  test('updateProduct sends correct data', async () => {
    const productData = { id: 1, title: 'Updated Product' };
    axiosClient.put.mockResolvedValue({ data: productData });
    
    await updateProduct(productData);
    
    expect(axiosClient.put).toHaveBeenCalledWith(
      'products/1',
      { title: 'Updated Product' }
    );
  });
});
```

### Test Coverage

Aim for:
- **Components**: 80%+ coverage
- **Services**: 90%+ coverage
- **Utilities**: 95%+ coverage

Run coverage report:

```bash
npm test -- --coverage --watchAll=false
```

## Commit Message Guidelines

Follow Conventional Commits specification:

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, missing semicolons, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependency updates

### Examples

```bash
feat(products): add CSV export functionality

Implement CSV export for product list with custom column selection.
Users can now download product data in CSV format.

Closes #123

---

fix(auth): correct token expiration handling

Fixed issue where expired tokens were not properly cleared,
causing redirect loop on login page.

Fixes #456

---

docs(readme): update installation instructions

Added Docker setup instructions and troubleshooting section.

---

refactor(services): simplify error handling

Extracted error handling logic into a shared utility function
to reduce code duplication across service modules.
```

## Pull Request Process

### Before Submitting

- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Tests added/updated and passing
- [ ] Documentation updated (if applicable)
- [ ] No console.log or debug code left behind
- [ ] Build passes without warnings
- [ ] Branch is up to date with main

### PR Template

When creating a PR, include:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Refactoring

## Testing
How to test these changes

## Screenshots (if applicable)
Before/after screenshots for UI changes

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] Build passes
```

### PR Size

Keep PRs focused and reasonably sized:
- **Small**: < 200 lines changed (preferred)
- **Medium**: 200-500 lines changed
- **Large**: 500-1000 lines changed (consider splitting)
- **Very Large**: > 1000 lines (must split)

## Code Review

### For Reviewers

- Be respectful and constructive
- Focus on code quality, not personal preferences
- Explain reasoning behind suggestions
- Approve when satisfied or request changes if needed
- Respond within 1-2 business days

### Review Checklist

- [ ] Code is clean and readable
- [ ] Logic is sound and efficient
- [ ] Error handling is appropriate
- [ ] Tests are comprehensive
- [ ] No security vulnerabilities
- [ ] Performance is acceptable
- [ ] Documentation is clear

### For Authors

- Be open to feedback
- Respond to all comments
- Make requested changes promptly
- Explain your reasoning when disagreeing
- Thank reviewers for their time

## Issue Reporting

### Bug Reports

Use the bug report template:

```markdown
**Describe the bug**
Clear description of the issue

**To Reproduce**
Steps to reproduce:
1. Go to '...'
2. Click on '...'
3. See error

**Expected behavior**
What should happen

**Screenshots**
If applicable

**Environment**
- Browser: [e.g., Chrome 90]
- OS: [e.g., Windows 10]
- Version: [e.g., 1.0.0]

**Additional context**
Any other relevant information
```

### Feature Requests

```markdown
**Is your feature request related to a problem?**
Description of the problem

**Describe the solution you'd like**
Clear description of desired functionality

**Describe alternatives you've considered**
Other approaches considered

**Additional context**
Mockups, examples, etc.
```

## Questions?

If you have questions about contributing:

1. Check existing documentation
2. Search closed issues/PRs
3. Open a discussion on GitHub
4. Contact the maintainers

---

Thank you for contributing to Siraj Admin Panel! 🎉
