# Contributing to DocLink

Thank you for your interest in contributing to DocLink! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Requirements](#testing-requirements)
- [Documentation](#documentation)
- [Community](#community)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of:
- Experience level
- Gender identity and expression
- Sexual orientation
- Disability
- Personal appearance
- Body size
- Race or ethnicity
- Age
- Religion or belief
- Nationality

### Expected Behavior

- Be respectful and considerate
- Use welcoming and inclusive language
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards other community members

### Unacceptable Behavior

- Harassment or discriminatory language
- Personal attacks or insults
- Publishing others' private information
- Trolling or inflammatory comments
- Other conduct inappropriate in a professional setting

## Getting Started

### Prerequisites

Before contributing, ensure you have:
- Node.js (v14 or higher)
- npm (v6 or higher)
- Git
- A code editor (VS Code recommended)

### Fork and Clone

1. **Fork the repository** on GitHub
2. **Clone your fork**:
```bash
git clone https://github.com/YOUR_USERNAME/doclink-web.git
cd doclink-web
```

3. **Add upstream remote**:
```bash
git remote add upstream https://github.com/feditech/doclink-web.git
```

4. **Install dependencies**:
```bash
npm install
```

5. **Start development server**:
```bash
npm run dev
```

## Development Workflow

### 1. Create a Branch

Always create a new branch for your work:

```bash
# Update your main branch
git checkout main
git pull upstream main

# Create feature branch
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/bug-description
```

**Branch Naming Convention:**
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Adding or updating tests
- `chore/` - Maintenance tasks

### 2. Make Changes

- Write clean, readable code
- Follow existing code patterns
- Add comments for complex logic
- Update documentation if needed

### 3. Test Your Changes

```bash
# Run linter
npm run lint

# Build the project
npm run build

# Test production build
npm run start
```

### 4. Commit Your Changes

```bash
git add .
git commit -m "feat: add new subscription feature"
```

See [Commit Guidelines](#commit-guidelines) below for proper commit message format.

### 5. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 6. Create Pull Request

1. Go to your fork on GitHub
2. Click "New Pull Request"
3. Select your branch
4. Fill in the PR template
5. Submit for review

## Coding Standards

### JavaScript/React Style Guide

#### General Rules

- Use **ES6+ syntax** (const/let, arrow functions, destructuring)
- Use **functional components** over class components
- Follow **React Hooks** best practices
- Keep components **small and focused**
- Use **meaningful variable names**

#### Example Component Structure

```javascript
import { useState, useEffect } from 'react';
import { Container } from '@mui/material';
import PropTypes from 'prop-types';

/**
 * ComponentName - Brief description
 * @param {Object} props - Component props
 */
const ComponentName = ({ title, data }) => {
  const [state, setState] = useState(null);

  useEffect(() => {
    // Effect logic
  }, []);

  const handleAction = () => {
    // Handler logic
  };

  return (
    <Container>
      <h1>{title}</h1>
      {/* Component JSX */}
    </Container>
  );
};

ComponentName.propTypes = {
  title: PropTypes.string.isRequired,
  data: PropTypes.array,
};

ComponentName.defaultProps = {
  data: [],
};

export default ComponentName;
```

### File Organization

```
components/
├── ComponentName/
│   ├── ComponentName.js      # Main component
│   ├── styledComponent/
│   │   └── index.js          # Styled components
│   └── SubComponent.js       # Sub-components if needed
```

### Styling Guidelines

#### Styled Components

```javascript
import styled from 'styled-components';

export const Container = styled.div`
  display: flex;
  flex-direction: column;
  padding: ${props => props.padding || '2rem'};
  
  @media (max-width: 768px) {
    padding: 1rem;
  }
`;
```

#### Material-UI Usage

```javascript
import { Box, Typography } from '@mui/material';
import { styled } from '@mui/material/styles';

const StyledBox = styled(Box)(({ theme }) => ({
  padding: theme.spacing(2),
  backgroundColor: theme.palette.background.paper,
}));
```

### Code Comments

```javascript
/**
 * Fetches blog posts from the API
 * @param {string} categoryId - Category ID to filter by
 * @param {number} page - Page number for pagination
 * @returns {Promise<Object>} Blog posts and pagination data
 */
async function fetchBlogPosts(categoryId, page = 1) {
  // Implementation
}
```

## Commit Guidelines

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no code change)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependency updates

### Examples

```bash
# New feature
git commit -m "feat(subscriptions): add annual subscription plan"

# Bug fix
git commit -m "fix(header): resolve mobile menu not closing"

# Documentation
git commit -m "docs(readme): update installation instructions"

# Multiple lines
git commit -m "feat(blogs): add blog filtering by category

- Add category dropdown
- Implement filter logic
- Update API integration

Closes #123"
```

### Scope

Common scopes in DocLink:
- `header`, `footer`, `nav`
- `home`, `about`, `contact`
- `subscriptions`, `doctors`, `blogs`
- `api`, `redux`, `utils`
- `styles`, `components`

## Pull Request Process

### PR Title Format

Follow the same format as commit messages:

```
feat(subscriptions): add annual subscription plan
```

### PR Description Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Changes Made
- List of changes
- Another change
- More changes

## Screenshots (if applicable)
![Screenshot](url)

## Testing
- [ ] Tested locally
- [ ] All tests pass
- [ ] Linter passes
- [ ] Build succeeds

## Related Issues
Closes #123
Relates to #456

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-reviewed code
- [ ] Commented complex code
- [ ] Updated documentation
- [ ] No new warnings
- [ ] Added/updated tests
```

### Review Process

1. **Automated Checks**: CI/CD runs automatically
2. **Code Review**: Team members review your code
3. **Feedback**: Address any requested changes
4. **Approval**: At least one approval required
5. **Merge**: Maintainer merges your PR

### Addressing Feedback

```bash
# Make requested changes
git add .
git commit -m "fix: address review feedback"
git push origin feature/your-feature-name
```

## Testing Requirements

### Manual Testing

Before submitting PR:

1. **Test all affected pages**
2. **Test on multiple screen sizes**
3. **Test in different browsers** (Chrome, Firefox, Safari)
4. **Test with slow network** (throttle network in DevTools)
5. **Check console for errors**

### Automated Testing (Future)

When test infrastructure is added:

```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run E2E tests
npm run test:e2e

# Test coverage
npm run test:coverage
```

## Documentation

### When to Update Documentation

Update documentation when you:
- Add new features
- Change existing functionality
- Add new APIs or endpoints
- Modify configuration
- Change deployment process

### Documentation Files

- `README.md` - Overview and quick start
- `docs/GETTING_STARTED.md` - Installation and setup
- `docs/FEATURES.md` - Feature documentation
- `docs/ARCHITECTURE.md` - Technical architecture
- `docs/API_DOCUMENTATION.md` - API reference
- `docs/DEPLOYMENT.md` - Deployment guide
- `docs/DEVELOPMENT.md` - Development workflow
- `docs/USER_GUIDE.md` - End-user guide

### Code Documentation

```javascript
/**
 * Component/function description
 * @param {type} param - Parameter description
 * @returns {type} Return value description
 */
```

## Issue Reporting

### Bug Reports

Use the bug report template:

```markdown
**Description**
Clear description of the bug

**To Reproduce**
1. Go to '...'
2. Click on '...'
3. See error

**Expected Behavior**
What should happen

**Screenshots**
If applicable

**Environment**
- OS: [e.g., Windows 10]
- Browser: [e.g., Chrome 96]
- Node version: [e.g., 16.13.0]

**Additional Context**
Any other relevant information
```

### Feature Requests

```markdown
**Feature Description**
Clear description of the feature

**Use Case**
Why this feature is needed

**Proposed Solution**
How it could be implemented

**Alternatives**
Other solutions considered

**Additional Context**
Any mockups, examples, etc.
```

## Community

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and discussions
- **Pull Requests**: Code contributions
- **Email**: For private matters: dev@doclink.com

### Getting Help

- Check existing documentation
- Search existing issues
- Ask in GitHub Discussions
- Contact maintainers

## Recognition

Contributors will be recognized in:
- README.md contributors section
- Release notes
- Project website (when available)

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

## Questions?

If you have questions about contributing, please:
1. Check the documentation
2. Search existing issues
3. Create a new discussion
4. Contact maintainers

Thank you for contributing to DocLink! 🎉

---

## Related Documentation

- [Getting Started](./GETTING_STARTED.md)
- [Development Guide](./DEVELOPMENT.md)
- [Architecture](./ARCHITECTURE.md)
