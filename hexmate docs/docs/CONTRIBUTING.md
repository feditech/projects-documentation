# Contributing to HexMate

Thank you for your interest in contributing to HexMate! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Development Process](#development-process)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Pull Request Process](#pull-request-process)
- [Issue Guidelines](#issue-guidelines)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inspiring community for all. Please treat all contributors and users with respect.

### Expected Behavior

- Use welcoming and inclusive language
- Be respectful of differing viewpoints and experiences
- Gracefully accept constructive criticism
- Focus on what is best for the community
- Show empathy towards other community members

### Unacceptable Behavior

- Trolling, insulting/derogatory comments, and personal attacks
- Public or private harassment
- Publishing others' private information without permission
- Other conduct which could reasonably be considered inappropriate

## Getting Started

### Prerequisites

Before contributing, ensure you have:

1. **Development Environment**
   - Node.js 16+ and npm 7+
   - Git
   - Code editor (VS Code recommended)

2. **Knowledge Requirements**
   - React and TypeScript
   - Material-UI
   - REST API integration
   - Git workflow

3. **Documentation**
   - Read the [README](../README.md)
   - Review [Architecture](ARCHITECTURE.md)
   - Follow [Development Guide](DEVELOPMENT.md)

### Setting Up Your Development Environment

1. **Fork the Repository**
   ```bash
   # Click 'Fork' button on GitHub
   # Clone your fork
   git clone https://github.com/YOUR_USERNAME/hexmate.git
   cd hexmate
   ```

2. **Add Upstream Remote**
   ```bash
   git remote add upstream https://github.com/feditech/hexmate.git
   git fetch upstream
   ```

3. **Install Dependencies**
   ```bash
   npm install
   ```

4. **Create Environment File**
   ```bash
   cp .env.example .env
   # Edit .env with your settings
   ```

5. **Start Development Server**
   ```bash
   npm start
   ```

## How to Contribute

### Ways to Contribute

1. **Report Bugs**
   - Check existing issues first
   - Provide detailed reproduction steps
   - Include system information

2. **Suggest Features**
   - Describe the feature clearly
   - Explain the use case
   - Consider implementation impact

3. **Improve Documentation**
   - Fix typos and errors
   - Add missing information
   - Improve clarity
   - Add examples

4. **Submit Code**
   - Fix bugs
   - Implement features
   - Improve performance
   - Refactor code

5. **Review Pull Requests**
   - Provide constructive feedback
   - Test changes
   - Suggest improvements

## Development Process

### Branching Strategy

**Main Branches:**
- `main` - Production-ready code
- `develop` - Integration branch for features

**Feature Branches:**
- `feature/feature-name` - New features
- `bugfix/bug-name` - Bug fixes
- `hotfix/issue-name` - Urgent fixes
- `docs/doc-name` - Documentation updates

### Workflow

1. **Create Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Changes**
   - Write clean code
   - Follow coding standards
   - Add tests
   - Update documentation

3. **Commit Changes**
   ```bash
   git add .
   git commit -m "feat: add user profile feature"
   ```

4. **Keep Updated**
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

5. **Push Changes**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create Pull Request**
   - Go to GitHub
   - Click "New Pull Request"
   - Fill in template
   - Request review

### Commit Message Convention

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

**Format:**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Code style (formatting, missing semi-colons, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `test`: Adding tests
- `chore`: Maintenance tasks
- `ci`: CI/CD changes

**Examples:**
```
feat(dms): add document version comparison

Implement side-by-side comparison view for document versions
with highlighted differences and download options.

Closes #123
```

```
fix(cts): resolve routing loop in workflow

Fix infinite loop when routing correspondence with circular
approval chain. Add cycle detection and error handling.

Fixes #456
```

```
docs(api): update authentication documentation

Add examples for token refresh and error handling.
Clarify CORS requirements.
```

## Coding Standards

### TypeScript

**Use Explicit Types:**
```typescript
// ✅ Good
const getUserName = (user: User): string => {
  return user.fullName;
};

// ❌ Bad
const getUserName = (user: any) => {
  return user.fullName;
};
```

**Interface vs Type:**
```typescript
// Use interface for object shapes
interface User {
  id: number;
  name: string;
}

// Use type for unions and complex types
type Status = 'pending' | 'approved' | 'rejected';
type ApiResponse<T> = { data: T; error?: string };
```

### React Components

**Functional Components:**
```typescript
// ✅ Good - Named export with explicit type
export const UserCard: React.FC<UserCardProps> = ({ user }) => {
  return <div>{user.name}</div>;
};

// ❌ Bad - Default export, no types
export default ({ user }) => {
  return <div>{user.name}</div>;
};
```

**Hooks:**
```typescript
// Custom hooks should start with 'use'
const useUserData = (userId: number) => {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    fetchUser(userId).then(setUser).finally(() => setLoading(false));
  }, [userId]);
  
  return { user, loading };
};
```

### File Organization

```typescript
// 1. Imports - External
import React, { useState, useEffect } from 'react';
import { Button, TextField } from '@mui/material';

// 2. Imports - Internal
import { UserService } from '../../services';
import { User } from '../../types';

// 3. Interfaces/Types
interface UserFormProps {
  userId?: number;
  onSave: (user: User) => void;
}

// 4. Component
export const UserForm: React.FC<UserFormProps> = ({ userId, onSave }) => {
  // Component implementation
};

// 5. Helper functions (if any)
const validateEmail = (email: string): boolean => {
  // Validation logic
};
```

### Naming Conventions

**Variables:**
```typescript
const userName = 'John'; // camelCase
const MAX_RETRIES = 3; // UPPER_CASE for constants
```

**Functions:**
```typescript
const getUserData = () => {}; // camelCase
const handleClick = () => {}; // event handlers
```

**Components:**
```typescript
const UserProfile = () => {}; // PascalCase
const DashboardWidget = () => {}; // PascalCase
```

**Boolean Variables:**
```typescript
const isLoading = true; // is/has/can prefix
const hasPermission = false;
const canEdit = true;
```

### Code Comments

**Use JSDoc for Functions:**
```typescript
/**
 * Fetches user data from the API
 * @param userId - The unique identifier of the user
 * @returns Promise resolving to user data
 * @throws Error if user not found
 */
const fetchUser = async (userId: number): Promise<User> => {
  // Implementation
};
```

**Inline Comments:**
```typescript
// ✅ Good - Explain why, not what
// Use exponential backoff to avoid overwhelming the server
await delay(Math.pow(2, attempt) * 1000);

// ❌ Bad - States the obvious
// Loop through users
users.forEach(user => {});
```

## Testing Guidelines

### Writing Tests

**Test Structure:**
```typescript
describe('UserProfile', () => {
  it('should render user name', () => {
    render(<UserProfile user={mockUser} />);
    expect(screen.getByText(mockUser.name)).toBeInTheDocument();
  });

  it('should call onEdit when edit button is clicked', () => {
    const handleEdit = jest.fn();
    render(<UserProfile user={mockUser} onEdit={handleEdit} />);
    
    fireEvent.click(screen.getByRole('button', { name: /edit/i }));
    expect(handleEdit).toHaveBeenCalledWith(mockUser.id);
  });
});
```

**Test Coverage:**
- Aim for 80%+ code coverage
- Test critical paths thoroughly
- Include edge cases
- Test error handling

**Running Tests:**
```bash
# Run all tests
npm test

# Run with coverage
npm test -- --coverage

# Run specific test file
npm test -- UserProfile.test.tsx
```

## Documentation

### Code Documentation

**Document:**
- Complex algorithms
- Non-obvious implementations
- API integrations
- Configuration options
- Known limitations

**Examples:**
```typescript
/**
 * Calculates the signature position based on page dimensions
 * and configured scale factor. Uses PDF-lib coordinate system
 * where (0,0) is bottom-left corner.
 */
const calculateSignaturePosition = (page: PDFPage, scale: number) => {
  // Implementation
};
```

### Documentation Files

When adding/updating documentation:

1. **Keep it Current**
   - Update docs with code changes
   - Remove obsolete information
   - Add migration guides for breaking changes

2. **Be Clear and Concise**
   - Use simple language
   - Provide examples
   - Include screenshots where helpful

3. **Follow Structure**
   - Use consistent formatting
   - Include table of contents
   - Add cross-references

## Pull Request Process

### Before Submitting

- [ ] Code follows style guidelines
- [ ] Tests are added/updated
- [ ] All tests pass
- [ ] Documentation is updated
- [ ] Commits follow convention
- [ ] Branch is up to date with main

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
How has this been tested?

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] Tests added/updated
- [ ] All tests passing
```

### Review Process

1. **Automated Checks**
   - Build passes
   - Tests pass
   - Linting passes
   - No security vulnerabilities

2. **Code Review**
   - At least one approval required
   - Address all comments
   - Resolve all discussions

3. **Merge**
   - Squash and merge for feature branches
   - Keep commit history clean
   - Delete branch after merge

## Issue Guidelines

### Reporting Bugs

**Use the Bug Template:**

```markdown
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '...'
3. See error

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment:**
- OS: [e.g. Windows 10]
- Browser: [e.g. Chrome 90]
- Version: [e.g. 1.0.0]

**Additional context**
Any other context about the problem.
```

### Suggesting Features

**Use the Feature Template:**

```markdown
**Is your feature request related to a problem?**
A clear description of the problem.

**Describe the solution you'd like**
A clear description of what you want to happen.

**Describe alternatives you've considered**
Alternative solutions or features you've considered.

**Additional context**
Any other context or screenshots.
```

### Issue Labels

- `bug` - Something isn't working
- `enhancement` - New feature request
- `documentation` - Documentation improvements
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention needed
- `question` - Further information requested
- `duplicate` - Issue already exists
- `wontfix` - Will not be worked on

## Community

### Getting Help

- **Documentation:** Start with our docs
- **Issues:** Search existing issues
- **Discussions:** Use GitHub Discussions for questions
- **Email:** Contact maintainers for sensitive matters

### Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Recognized in the community

## License

By contributing to HexMate, you agree that your contributions will be licensed under the same license as the project.

## Questions?

If you have questions about contributing, please:
1. Check this document thoroughly
2. Search existing issues and discussions
3. Create a new discussion if needed

Thank you for contributing to HexMate! 🎉
