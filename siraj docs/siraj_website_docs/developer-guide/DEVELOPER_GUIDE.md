# Developer Guide

Complete guide for developers working on the Siraj platform.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setup](#setup)
3. [Project Structure](#project-structure)
4. [Development Workflow](#development-workflow)
5. [Coding Standards](#coding-standards)
6. [Testing](#testing)
7. [Building](#building)
8. [Common Tasks](#common-tasks)
9. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Required Software

- **Node.js:** Version 18.x or higher
- **npm:** Version 9.x or higher (comes with Node.js)
- **Git:** Latest version
- **Code Editor:** VS Code recommended

### Recommended Tools

- **Docker:** For containerized development
- **Postman/Insomnia:** For API testing
- **React DevTools:** Browser extension for React debugging
- **Redux DevTools:** If using Redux state management

### Knowledge Requirements

- **JavaScript/TypeScript:** Strong understanding
- **React & Next.js:** Familiarity with React 18+ and Next.js 14+
- **CSS/Styling:** Experience with Tailwind CSS and/or Material-UI
- **Git:** Basic version control knowledge
- **REST APIs:** Understanding of API integration

---

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/feditech/siraj-fronted.git
cd siraj-fronted
```

### 2. Install Dependencies

```bash
npm install
```

This will install all dependencies defined in `package.json`.

### 3. Environment Configuration

Create a `.env.local` file in the root directory:

```bash
cp .env .env.local
```

Edit `.env.local` with your configuration:

```env
# Backend Configuration
BACKEND_ENV=dev
BACKEND_BASE_URL=http://localhost:3001/api

# Meta Tags
META_CONTENT=

# Add any additional environment variables here
```

**Important Environment Variables:**
- `BACKEND_ENV`: Environment (dev, staging, production)
- `BACKEND_BASE_URL`: Backend API base URL
- `META_CONTENT`: Meta tag content for SEO

### 4. Run Development Server

```bash
npm run dev
```

The application will be available at [http://localhost:3000](http://localhost:3000)

### 5. Verify Setup

1. Open browser to `http://localhost:3000`
2. Check that the landing page loads
3. Test language switching (EN/AR)
4. Verify console has no errors

---

## Project Structure

```
siraj-fronted/
├── .github/               # GitHub workflows and CI/CD
├── .vscode/              # VS Code configuration
├── docs/                 # Documentation
├── public/               # Static assets
│   ├── images/          # Image files
│   ├── fonts/           # Font files
│   └── ...
├── src/                  # Source code
│   ├── app/             # Next.js app directory
│   │   └── [locale]/    # Internationalized routes
│   │       ├── (app)/           # Authenticated app routes
│   │       └── (landingPage)/   # Public landing pages
│   ├── components/      # React components
│   │   ├── LandingPage/
│   │   ├── NavigationBar/
│   │   ├── ui-components/
│   │   └── ...
│   ├── dictionaries/    # i18n translations
│   │   ├── en.json     # English translations
│   │   └── ar.json     # Arabic translations
│   ├── helpers/         # Utility functions
│   ├── hooks/           # Custom React hooks
│   ├── modules/         # Feature modules
│   ├── providers/       # React context providers
│   ├── services/        # API services
│   ├── store/           # State management
│   ├── styles/          # Global styles
│   ├── i18n.ts         # i18n configuration
│   ├── middleware.ts    # Next.js middleware
│   ├── navigation.ts    # Navigation configuration
│   └── theme.ts         # MUI theme configuration
├── templates/           # Kubernetes/Helm templates
├── .dockerignore       # Docker ignore rules
├── .env                # Environment variables (template)
├── .eslintrc.json      # ESLint configuration
├── .gitignore          # Git ignore rules
├── Chart.yaml          # Helm chart metadata
├── Dockerfile          # Docker container definition
├── next.config.mjs     # Next.js configuration
├── package.json        # Project dependencies
├── postcss.config.mjs  # PostCSS configuration
├── tailwind.config.ts  # Tailwind CSS configuration
├── tsconfig.json       # TypeScript configuration
└── values.yaml         # Helm values

```

### Key Directories

#### `/src/app`
Next.js 14 App Router structure with:
- `[locale]/` - Internationalized routes
- `(app)/` - Protected routes requiring authentication
- `(landingPage)/` - Public landing pages

#### `/src/components`
Reusable React components organized by feature:
- Shared UI components
- Feature-specific components
- Layout components

#### `/src/services`
API service layer:
- HTTP client configuration
- API endpoint definitions
- Request/response handlers

#### `/src/dictionaries`
Translation files for internationalization:
- `en.json` - English translations
- `ar.json` - Arabic translations

---

## Development Workflow

### Branch Strategy

```
main                 # Production-ready code
  ├── staging       # Pre-production testing
  └── develop       # Active development
      └── feature/* # Feature branches
      └── bugfix/*  # Bug fix branches
```

### Creating a New Feature

1. **Create Feature Branch**
```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

2. **Make Changes**
- Write code following standards
- Test locally
- Commit regularly with clear messages

3. **Test Your Changes**
```bash
npm run lint          # Check code style
npm run build         # Build for production
npm run dev           # Test locally
```

4. **Create Pull Request**
- Push branch to remote
- Open PR against `develop`
- Fill out PR template
- Request review

### Commit Message Format

Follow conventional commits:

```
type(scope): subject

body (optional)

footer (optional)
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Build/tooling changes

**Examples:**
```
feat(auth): add WhatsApp OTP authentication
fix(mbti): resolve test progress save issue
docs(readme): update setup instructions
refactor(api): improve error handling
```

---

## Coding Standards

### TypeScript

**Use TypeScript for all new files:**
```typescript
// ✅ Good
interface UserProfile {
  name: string;
  email: string;
  age?: number;
}

const user: UserProfile = {
  name: "Ahmad",
  email: "ahmad@example.com"
};

// ❌ Bad - avoid 'any'
const user: any = { ... };
```

**Define prop types:**
```typescript
// ✅ Good
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

export default function Button({ label, onClick, disabled }: ButtonProps) {
  // ...
}

// ❌ Bad - no types
export default function Button({ label, onClick, disabled }) {
  // ...
}
```

### React Components

**Use functional components:**
```typescript
// ✅ Good - functional component
export default function MyComponent({ prop1, prop2 }: MyComponentProps) {
  return <div>...</div>;
}

// ❌ Bad - class component
class MyComponent extends React.Component {
  // ...
}
```

**Component file structure:**
```typescript
// 1. Imports
import React from 'react';
import { useState } from 'react';

// 2. Type definitions
interface ComponentProps {
  // ...
}

// 3. Component
export default function Component({ props }: ComponentProps) {
  // 4. Hooks
  const [state, setState] = useState();
  
  // 5. Functions
  const handleClick = () => {
    // ...
  };
  
  // 6. Effects
  useEffect(() => {
    // ...
  }, []);
  
  // 7. Render
  return (
    <div>...</div>
  );
}
```

### File Naming

- **Components:** PascalCase - `MyComponent.tsx`
- **Utilities:** camelCase - `apiHelpers.ts`
- **Styles:** kebab-case - `my-component.module.scss`
- **Constants:** UPPER_CASE - `API_CONSTANTS.ts`

### Styling

**Prefer Tailwind CSS:**
```tsx
// ✅ Good
<div className="flex items-center justify-between p-4 bg-blue-500">
  <h1 className="text-2xl font-bold text-white">Title</h1>
</div>

// Use MUI for complex components
import { Button } from '@mui/material';

<Button variant="contained" color="primary">
  Click Me
</Button>
```

### Internationalization

**Always use translation keys:**
```tsx
// ✅ Good
import { useTranslations } from 'next-intl';

export default function Component() {
  const t = useTranslations('MyComponent');
  
  return <h1>{t('title')}</h1>;
}

// ❌ Bad - hardcoded text
return <h1>Welcome to Siraj</h1>;
```

**Add translations to both languages:**
```json
// en.json
{
  "MyComponent": {
    "title": "Welcome to Siraj"
  }
}

// ar.json
{
  "MyComponent": {
    "title": "مرحباً بك في سراج"
  }
}
```

---

## Testing

### Running Tests

Currently, the project uses manual testing. Future additions will include:

```bash
# Unit tests (to be implemented)
npm run test

# E2E tests (to be implemented)
npm run test:e2e

# Coverage (to be implemented)
npm run test:coverage
```

### Manual Testing Checklist

Before submitting a PR:

- [ ] Test on desktop (Chrome, Firefox, Safari)
- [ ] Test on mobile (iOS Safari, Android Chrome)
- [ ] Test both languages (EN/AR)
- [ ] Test with different user states (logged in/out)
- [ ] Test error scenarios
- [ ] Check console for errors
- [ ] Verify responsive design
- [ ] Test keyboard navigation
- [ ] Test screen reader compatibility (basic)

### Testing User Flows

**Authentication Flow:**
1. Open app in incognito/private mode
2. Click "Log in"
3. Enter phone number
4. Receive and enter OTP
5. Verify redirect to app

**MBTI Test Flow:**
1. Log in as new user
2. Complete profile
3. Start MBTI test
4. Answer all questions
5. Submit test
6. Verify results display

---

## Building

### Development Build

```bash
npm run dev
```

- Hot reload enabled
- Source maps included
- Not optimized for performance

### Production Build

```bash
npm run build
```

Outputs to `.next/` directory.

**Build artifacts:**
- `.next/static` - Static assets
- `.next/server` - Server-side code
- `.next/standalone` - Standalone build (for deployment)

### Production Build with Artifacts

```bash
npm run prod-build
```

This command:
1. Runs `next build`
2. Copies static files
3. Copies public folder
4. Creates `release.zip` in `.next/standalone/`

### Docker Build

```bash
# Build image
docker build -t siraj-frontend:latest .

# Run container
docker run -p 3000:3000 siraj-frontend:latest
```

---

## Common Tasks

### Adding a New Page

1. **Create page file:**
```bash
# Public page
touch src/app/[locale]/(landingPage)/my-page/page.tsx

# Protected page
touch src/app/[locale]/(app)/app/(withNav)/my-page/page.tsx
```

2. **Implement page:**
```typescript
export default function MyPage() {
  return (
    <div>
      <h1>My New Page</h1>
    </div>
  );
}
```

3. **Add translations:**
```json
// en.json
{
  "MyPage": {
    "title": "My Page Title"
  }
}
```

4. **Add navigation (if needed):**
Update navigation bar component.

### Adding a New Component

1. **Create component file:**
```bash
mkdir src/components/MyComponent
touch src/components/MyComponent/MyComponent.tsx
```

2. **Implement component:**
```typescript
interface MyComponentProps {
  title: string;
}

export default function MyComponent({ title }: MyComponentProps) {
  return (
    <div>
      <h2>{title}</h2>
    </div>
  );
}
```

3. **Use component:**
```typescript
import MyComponent from '@/components/MyComponent/MyComponent';

<MyComponent title="Hello" />
```

### Adding an API Service

1. **Define service in `/src/services`:**
```typescript
// src/services/myFeature.service.ts
import axios from 'axios';
import { baseService } from './base.service';

export const myFeatureService = {
  getData: async () => {
    const response = await baseService.get('/my-endpoint');
    return response.data;
  },
  
  postData: async (data: any) => {
    const response = await baseService.post('/my-endpoint', data);
    return response.data;
  }
};
```

2. **Use in component:**
```typescript
import { myFeatureService } from '@/services/myFeature.service';

useEffect(() => {
  const fetchData = async () => {
    const data = await myFeatureService.getData();
    setData(data);
  };
  
  fetchData();
}, []);
```

### Adding Translations

1. **Edit both language files:**

```json
// src/dictionaries/en.json
{
  "NewFeature": {
    "welcomeMessage": "Welcome to new feature",
    "buttonLabel": "Click here"
  }
}

// src/dictionaries/ar.json
{
  "NewFeature": {
    "welcomeMessage": "مرحباً بك في الميزة الجديدة",
    "buttonLabel": "اضغط هنا"
  }
}
```

2. **Use in component:**
```typescript
const t = useTranslations('NewFeature');

<h1>{t('welcomeMessage')}</h1>
<button>{t('buttonLabel')}</button>
```

### Updating Dependencies

```bash
# Check outdated packages
npm outdated

# Update specific package
npm update package-name

# Update all packages (careful!)
npm update

# Install new package
npm install package-name

# Install dev dependency
npm install --save-dev package-name
```

---

## Troubleshooting

### Build Errors

**Problem: `Module not found` error**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

**Problem: TypeScript errors**
```bash
# Check TypeScript configuration
npm run type-check

# Clear TypeScript cache
rm -rf .next
npm run build
```

### Runtime Errors

**Problem: `Cannot read property of undefined`**
- Check for null/undefined values
- Add optional chaining: `object?.property`
- Add default values: `value ?? defaultValue`

**Problem: Hydration mismatch**
- Ensure server and client render the same HTML
- Avoid using browser-only APIs during SSR
- Use `useEffect` for client-side only code

### Development Server Issues

**Problem: Port 3000 already in use**
```bash
# Kill process on port 3000
# On macOS/Linux:
lsof -ti:3000 | xargs kill -9

# On Windows:
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Or use different port
PORT=3001 npm run dev
```

**Problem: Changes not reflecting**
```bash
# Clear Next.js cache
rm -rf .next
npm run dev
```

### Docker Issues

**Problem: Docker build fails**
```bash
# Clear Docker cache
docker builder prune

# Rebuild without cache
docker build --no-cache -t siraj-frontend:latest .
```

**Problem: Container won't start**
```bash
# Check logs
docker logs <container-id>

# Check environment variables
docker inspect <container-id>
```

### Git Issues

**Problem: Merge conflicts**
```bash
# Check conflicted files
git status

# Resolve conflicts in editor
# Then mark as resolved
git add <file>
git commit
```

**Problem: Accidentally committed sensitive data**
```bash
# Remove from last commit
git rm --cached <file>
git commit --amend

# If pushed, contact team lead
```

---

## Best Practices

### Performance

1. **Use Next.js Image component:**
```tsx
import Image from 'next/image';

<Image 
  src="/images/hero.jpg" 
  alt="Hero image"
  width={800}
  height={600}
  priority // for above-fold images
/>
```

2. **Lazy load components:**
```typescript
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <p>Loading...</p>
});
```

3. **Memoize expensive computations:**
```typescript
import { useMemo } from 'react';

const expensiveValue = useMemo(() => {
  return computeExpensiveValue(input);
}, [input]);
```

### Security

1. **Never commit secrets:**
- Use `.env.local` for sensitive data
- Add to `.gitignore`
- Use environment variables

2. **Sanitize user input:**
```typescript
// Always validate and sanitize
const sanitizedInput = input.trim().toLowerCase();
```

3. **Use HTTPS in production:**
- Enforce in middleware
- Set secure cookies

### Accessibility

1. **Semantic HTML:**
```tsx
// ✅ Good
<nav>
  <ul>
    <li><a href="/home">Home</a></li>
  </ul>
</nav>

// ❌ Bad
<div onClick={goHome}>Home</div>
```

2. **ARIA labels:**
```tsx
<button aria-label="Close dialog">
  <CloseIcon />
</button>
```

3. **Keyboard navigation:**
```tsx
<div 
  role="button"
  tabIndex={0}
  onKeyPress={(e) => e.key === 'Enter' && handleClick()}
  onClick={handleClick}
>
  Clickable
</div>
```

### Code Review Checklist

Before submitting PR:

- [ ] Code follows style guide
- [ ] No console.logs or debugger statements
- [ ] All TypeScript types defined
- [ ] Translations added for both languages
- [ ] Components are reusable
- [ ] No hardcoded values (use constants/env vars)
- [ ] Error handling implemented
- [ ] Loading states added
- [ ] Responsive design verified
- [ ] Accessibility considerations
- [ ] Performance optimized
- [ ] Documentation updated

---

## Useful Commands

```bash
# Development
npm run dev                 # Start dev server
npm run build              # Build for production
npm run start              # Start production server
npm run lint               # Run ESLint
npm run prod-build         # Build and package for deployment

# Git
git status                 # Check status
git add .                  # Stage all changes
git commit -m "message"    # Commit changes
git push origin branch     # Push to remote
git pull origin branch     # Pull from remote

# Docker
docker build -t siraj .    # Build image
docker run -p 3000:3000 siraj  # Run container
docker ps                  # List containers
docker logs <id>          # View logs

# Cleanup
rm -rf node_modules        # Remove dependencies
rm -rf .next              # Remove build cache
npm install               # Reinstall dependencies
```

---

## Additional Resources

### Documentation
- [Next.js Docs](https://nextjs.org/docs)
- [React Docs](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Material-UI Docs](https://mui.com/material-ui/)

### Learning Resources
- [Next.js Learn](https://nextjs.org/learn)
- [React Tutorial](https://react.dev/learn)
- [TypeScript in 5 Minutes](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

### Community
- [Next.js GitHub](https://github.com/vercel/next.js)
- [React Community](https://react.dev/community)

---

**Need Help?**

- 📧 **Team Email:** Contact team lead
- 💬 **Slack/Discord:** Join team channel
- 📖 **Docs:** Check this guide first
- 🐛 **Issues:** Open GitHub issue

---

*Last updated: January 2025*
