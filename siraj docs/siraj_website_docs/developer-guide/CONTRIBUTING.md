# Contributing Guidelines

Thank you for your interest in contributing to Siraj! This document provides guidelines for contributing to the project.

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [Getting Started](#getting-started)
3. [Development Process](#development-process)
4. [Coding Standards](#coding-standards)
5. [Commit Guidelines](#commit-guidelines)
6. [Pull Request Process](#pull-request-process)
7. [Testing](#testing)
8. [Documentation](#documentation)
9. [Reporting Issues](#reporting-issues)
10. [Community](#community)

---

## Code of Conduct

### Our Pledge

We pledge to make participation in our project a harassment-free experience for everyone, regardless of:
- Age, body size, disability, ethnicity
- Gender identity and expression
- Level of experience
- Nationality, personal appearance
- Race, religion, sexual identity and orientation

### Our Standards

**Positive behavior includes:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behavior includes:**
- Trolling, insulting/derogatory comments
- Public or private harassment
- Publishing others' private information
- Other conduct which could reasonably be considered inappropriate

### Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by contacting the project team. All complaints will be reviewed and investigated promptly and fairly.

---

## Getting Started

### Prerequisites

Before contributing, ensure you have:
- Node.js 18+ installed
- Git configured with your GitHub account
- Familiarity with React, Next.js, and TypeScript
- Understanding of the project architecture (see [Architecture docs](../architecture/ARCHITECTURE.md))

### Fork and Clone

1. **Fork the repository** on GitHub
2. **Clone your fork locally:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/siraj-fronted.git
   cd siraj-fronted
   ```

3. **Add upstream remote:**
   ```bash
   git remote add upstream https://github.com/feditech/siraj-fronted.git
   ```

4. **Install dependencies:**
   ```bash
   npm install
   ```

5. **Create your environment file:**
   ```bash
   cp .env .env.local
   # Edit .env.local with your configuration
   ```

---

## Development Process

### Branch Strategy

```
main (production)
  └── develop (integration branch)
      ├── feature/your-feature-name
      ├── bugfix/issue-description
      └── hotfix/critical-fix
```

### Creating a Feature Branch

1. **Update develop branch:**
   ```bash
   git checkout develop
   git pull upstream develop
   ```

2. **Create feature branch:**
   ```bash
   git checkout -b feature/add-user-dashboard
   ```

   **Branch naming conventions:**
   - `feature/` - New features
   - `bugfix/` - Bug fixes
   - `hotfix/` - Critical fixes for production
   - `docs/` - Documentation updates
   - `refactor/` - Code refactoring
   - `test/` - Adding tests

3. **Make your changes**
   - Write clean, maintainable code
   - Follow coding standards
   - Add tests if applicable
   - Update documentation

4. **Test locally:**
   ```bash
   npm run dev        # Development server
   npm run build      # Production build
   npm run lint       # Linting
   ```

5. **Commit your changes:**
   ```bash
   git add .
   git commit -m "feat(dashboard): add user dashboard component"
   ```

6. **Push to your fork:**
   ```bash
   git push origin feature/add-user-dashboard
   ```

7. **Create Pull Request** on GitHub

---

## Coding Standards

### TypeScript

**Always use TypeScript:**
```typescript
// ✅ Good
interface Props {
  title: string;
  onClose: () => void;
}

export function Modal({ title, onClose }: Props) {
  return <div>{title}</div>;
}

// ❌ Bad
export function Modal({ title, onClose }) {
  return <div>{title}</div>;
}
```

**Avoid `any` type:**
```typescript
// ✅ Good
const processData = (data: UserData): ProcessedData => {
  // ...
};

// ❌ Bad
const processData = (data: any): any => {
  // ...
};
```

### React Components

**Use functional components:**
```typescript
// ✅ Good
export default function UserCard({ user }: Props) {
  return <div>{user.name}</div>;
}

// ❌ Bad
class UserCard extends React.Component {
  // ...
}
```

**Component structure:**
```typescript
// 1. Imports
import React from 'react';
import { useState } from 'react';

// 2. Types/Interfaces
interface ComponentProps {
  title: string;
}

// 3. Component
export default function Component({ title }: ComponentProps) {
  // 4. Hooks
  const [state, setState] = useState();
  
  // 5. Event handlers
  const handleClick = () => {
    // ...
  };
  
  // 6. Effects
  useEffect(() => {
    // ...
  }, []);
  
  // 7. Render
  return (
    <div>
      <h1>{title}</h1>
    </div>
  );
}
```

### File Organization

```
ComponentName/
├── ComponentName.tsx       # Main component
├── ComponentName.test.tsx  # Tests (if applicable)
├── ComponentName.styles.ts # Styled components (if needed)
├── index.ts               # Exports
└── types.ts               # Type definitions (if complex)
```

### Naming Conventions

- **Components:** PascalCase - `UserProfile.tsx`
- **Utilities:** camelCase - `formatDate.ts`
- **Constants:** UPPER_SNAKE_CASE - `API_BASE_URL`
- **Interfaces:** PascalCase with 'I' prefix (optional) - `IUserData` or `UserData`
- **Types:** PascalCase with 'T' prefix (optional) - `TUser` or `User`

### Code Style

**Use const over let:**
```typescript
// ✅ Good
const userName = 'Ahmad';
const users = ['Ahmad', 'Sarah'];

// ❌ Bad
let userName = 'Ahmad';
var users = ['Ahmad', 'Sarah'];
```

**Destructure props:**
```typescript
// ✅ Good
function Component({ title, description }: Props) {
  return <div>{title}</div>;
}

// ❌ Bad
function Component(props: Props) {
  return <div>{props.title}</div>;
}
```

**Use arrow functions for handlers:**
```typescript
// ✅ Good
const handleClick = () => {
  // ...
};

// ❌ Bad
function handleClick() {
  // ...
}
```

### Internationalization

**Always use translation keys:**
```tsx
// ✅ Good
import { useTranslations } from 'next-intl';

export default function Component() {
  const t = useTranslations('ComponentName');
  return <h1>{t('title')}</h1>;
}

// ❌ Bad
export default function Component() {
  return <h1>Welcome to Siraj</h1>;
}
```

**Add translations for both languages:**
```json
// en.json
{
  "ComponentName": {
    "title": "Welcome to Siraj"
  }
}

// ar.json
{
  "ComponentName": {
    "title": "مرحباً بك في سراج"
  }
}
```

### Comments

**Write self-documenting code:**
```typescript
// ✅ Good - code is clear
const isUserEligible = age >= 18 && hasCompletedTest;

// ❌ Bad - unnecessary comment
// Check if user is 18 or older and has completed test
const check = age >= 18 && hasCompletedTest;
```

**Add comments for complex logic:**
```typescript
// ✅ Good - explains why
// Use exponential backoff to prevent API rate limiting
const delay = Math.min(1000 * Math.pow(2, retryCount), 30000);
```

**JSDoc for functions (when helpful):**
```typescript
/**
 * Calculates the user's personality type based on test scores
 * @param scores - Array of dimension scores (E/I, S/N, T/F, J/P)
 * @returns MBTI personality type (e.g., "INTJ")
 */
function calculatePersonalityType(scores: number[]): string {
  // ...
}
```

---

## Commit Guidelines

### Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Example:**
```
feat(auth): add WhatsApp OTP authentication

Implement WhatsApp-based OTP login flow including:
- OTP request endpoint integration
- OTP verification with error handling
- Token storage and management

Closes #123
```

### Commit Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Build process, dependencies, tooling

### Scope Examples

- `auth` - Authentication
- `mbti` - MBTI test functionality
- `booking` - Session booking
- `profile` - User profile
- `ui` - UI components
- `i18n` - Internationalization
- `api` - API integration

### Commit Message Rules

1. **Use imperative mood:** "add feature" not "added feature"
2. **Be concise:** Subject line < 72 characters
3. **Capitalize subject line**
4. **No period at end of subject**
5. **Separate subject from body with blank line**
6. **Explain what and why, not how**

**Good examples:**
```
feat(dashboard): add user statistics widget
fix(auth): prevent double OTP requests
docs(readme): update installation instructions
refactor(api): simplify error handling
```

**Bad examples:**
```
update files
fixed bug
WIP
changes
```

---

## Pull Request Process

### Before Creating PR

- [ ] Code follows style guidelines
- [ ] All tests pass locally
- [ ] No console.log or debugger statements
- [ ] Translation keys added for both languages
- [ ] Documentation updated (if needed)
- [ ] Commits follow commit guidelines
- [ ] Branch is up to date with develop

### Creating a Pull Request

1. **Push to your fork:**
   ```bash
   git push origin feature/your-feature
   ```

2. **Create PR on GitHub:**
   - Base: `feditech/siraj-fronted` `develop`
   - Compare: `your-fork/siraj-fronted` `feature/your-feature`

3. **Fill out PR template:**

   ```markdown
   ## Description
   Brief description of changes
   
   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Breaking change
   - [ ] Documentation update
   
   ## Testing
   - [ ] Tests pass locally
   - [ ] Tested on mobile
   - [ ] Tested in both languages
   
   ## Screenshots (if applicable)
   Add screenshots here
   
   ## Related Issues
   Closes #123
   ```

4. **Request review** from maintainers

### PR Review Process

1. **Automated checks run:**
   - Linting
   - Type checking
   - Build verification

2. **Code review by maintainers:**
   - Code quality
   - Adherence to standards
   - Test coverage
   - Documentation

3. **Address feedback:**
   - Make requested changes
   - Push to same branch
   - PR updates automatically

4. **Approval and merge:**
   - 1-2 approvals required
   - Squash and merge to develop

### PR Etiquette

- **Be responsive** to feedback
- **Be respectful** in discussions
- **Explain your decisions** when asked
- **Ask questions** if unclear
- **Keep PRs focused** - one feature/fix per PR
- **Keep PRs small** - easier to review

---

## Testing

### Manual Testing

Before submitting PR, test:

1. **Functionality:**
   - Feature works as expected
   - Edge cases handled
   - Error states work correctly

2. **Responsiveness:**
   - Mobile (iOS/Android)
   - Tablet
   - Desktop

3. **Browsers:**
   - Chrome
   - Firefox
   - Safari
   - Edge (if possible)

4. **Languages:**
   - English interface
   - Arabic interface (RTL)
   - All text translated

5. **User States:**
   - Logged out
   - Logged in
   - Profile incomplete
   - Test not completed

### Automated Tests (Future)

Once test infrastructure is added:

```bash
# Run tests
npm test

# Run specific test
npm test -- ComponentName

# Run with coverage
npm test -- --coverage
```

---

## Documentation

### When to Update Documentation

Update docs when you:
- Add new features
- Change existing features
- Add/change API endpoints
- Update configuration
- Change development process

### Documentation Files

- `README.md` - Project overview
- `docs/PRODUCT_OVERVIEW.md` - Product information
- `docs/user-guide/USER_GUIDE.md` - User instructions
- `docs/developer-guide/DEVELOPER_GUIDE.md` - Development guide
- `docs/architecture/ARCHITECTURE.md` - Technical architecture
- `docs/api/API.md` - API documentation
- `docs/DEPLOYMENT.md` - Deployment instructions

### Code Documentation

Add inline documentation for:
- Complex algorithms
- Non-obvious business logic
- API integrations
- Utility functions

---

## Reporting Issues

### Before Reporting

1. **Search existing issues** - may already be reported
2. **Check documentation** - may be explained
3. **Try latest version** - may be fixed

### Bug Reports

Include:
- **Clear title** - describe the bug
- **Description** - what happened vs. expected
- **Steps to reproduce** - detailed steps
- **Environment:**
  - Browser and version
  - Device (mobile/desktop)
  - Operating system
  - Language (EN/AR)
- **Screenshots** - if visual bug
- **Console errors** - if applicable

**Template:**
```markdown
## Bug Description
Clear description of the bug

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- Browser: Chrome 120
- Device: iPhone 13
- OS: iOS 17
- Language: Arabic

## Screenshots
[Attach screenshots]

## Additional Context
Any other information
```

### Feature Requests

Include:
- **Clear title** - feature name
- **Problem** - what problem it solves
- **Proposed solution** - how it should work
- **Alternatives** - other solutions considered
- **Use cases** - who benefits and how

---

## Community

### Getting Help

- **Documentation:** Check docs first
- **Issues:** Search or create issue
- **Discussions:** GitHub Discussions (if enabled)
- **Email:** info@siraj.app

### Communication

- **Be respectful** and professional
- **Be patient** - maintainers are often volunteers
- **Be constructive** in criticism
- **Be helpful** to other contributors

### Recognition

Contributors are recognized:
- In project README
- In release notes
- Through GitHub contributor stats

---

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

## Questions?

If you have questions about contributing:
- Open an issue with the `question` label
- Email the team at info@siraj.app
- Check the [Developer Guide](DEVELOPER_GUIDE.md)

---

**Thank you for contributing to Siraj! 🎉**

Your contributions help students across the Arab world make better career decisions.

---

*Last updated: January 2025*
