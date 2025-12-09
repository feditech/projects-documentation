# Siraj Admin Panel

Siraj Admin Panel is a comprehensive React-based administrative dashboard for managing the Siraj platform, which provides career guidance, university information, job trials, and advisory services to students.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Development](#development)
- [Building for Production](#building-for-production)
- [Deployment](#deployment)
- [Project Structure](#project-structure)
- [API Integration](#api-integration)
- [Available Scripts](#available-scripts)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Siraj Admin Panel is the central management interface for administrators to oversee and manage all aspects of the Siraj platform. It provides a user-friendly interface to manage students, advisors, companies, universities, programs, products, and various other resources.

### Key Capabilities

- **User Management**: Manage students and advisors with comprehensive profile information
- **Educational Content**: Manage universities, programs, and majors
- **Job Management**: Handle job trials, applications, and company partnerships
- **Advisory Services**: Manage booked sessions, time slots, and retake requests
- **Product Management**: Configure and update platform products and pricing
- **Coupon System**: Create and manage promotional coupons
- **Data Crawling**: Monitor and manage web crawling jobs for data collection
- **Multi-currency Support**: Handle pricing in USD and Jordanian Dinars

## Features

### 1. Student Management
- View and manage student profiles
- Track student activities and engagement
- Monitor student progress and interactions

### 2. Advisor Management
- Manage advisor profiles and availability
- Track advisor performance and session history
- Assign and schedule advisory sessions

### 3. University & Program Management
- Add, edit, and manage university information
- Maintain program catalogs
- Update admission requirements and deadlines
- Manage university-specific data

### 4. Job Trial Management
- Create and manage job trial opportunities
- Track student applications and participation
- Monitor job trial completion and feedback

### 5. Product Management
- Configure platform products (subscription plans)
- Set pricing in multiple currencies (USD, JOD)
- Define product features using rich text editor
- Manage session allocations and job trial experience counts
- Toggle job trial eligibility per product

### 6. Company Management
- Manage company profiles and partnerships
- Track job opportunities from companies
- Maintain company contact information

### 7. Booked Sessions
- View all scheduled advisory sessions
- Monitor session status and completion
- Manage session conflicts and rescheduling

### 8. Time Slot Management
- Configure available time slots for advisors
- Manage recurring schedules (daily/weekly)
- Handle time zone considerations

### 9. Coupon Management
- Create promotional coupons
- Set discount values and expiration dates
- Track coupon usage and redemption

### 10. Crawling Job Management
- Monitor web crawling operations
- Track data collection status
- Manage crawler configurations

### 11. Job Application Management
- Review student job applications
- Track application status
- Manage application workflows

### 12. Retake Request Management
- Handle student requests for retaking assessments
- Approve or reject retake requests
- Track retake history

## Technology Stack

### Frontend
- **React 18.3.1**: Core framework for building the user interface
- **React Router DOM 6.26.2**: Client-side routing
- **Ant Design 5.20.6**: UI component library
- **Axios 1.7.7**: HTTP client for API requests
- **React Quill 2.0.0**: Rich text editor for features
- **Day.js 1.11.13**: Date manipulation library
- **Moment 2.30.1**: Date formatting and timezone handling
- **Lodash 4.17.21**: Utility library
- **React CSV 2.2.2**: CSV export functionality

### Build Tools
- **React Scripts 5.0.1**: Build configuration and scripts
- **Cross-env 7.0.3**: Cross-platform environment variable management
- **Babel**: JavaScript transpilation

### Development Tools
- **ESLint**: Code linting
- **Jest**: Testing framework (via react-scripts)
- **React Testing Library**: Component testing utilities

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js**: Version 18.x or higher (recommended: 18 LTS)
- **npm**: Version 8.x or higher (comes with Node.js)
- **Git**: For version control
- **Docker** (optional): For containerized deployment
- **Kubernetes** (optional): For Helm-based deployment

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/feditech/siraj-fe-admin.git
cd siraj-fe-admin
```

### 2. Install Dependencies

```bash
npm install
```

This will install all required dependencies as specified in `package.json`.

### 3. Verify Installation

Check that everything is installed correctly:

```bash
npm --version
node --version
```

## Configuration

### Environment Variables

The application uses environment variables for configuration. Create a `.env` file in the root directory:

```bash
# API Configuration
REACT_APP_API_URL=http://localhost:8000/api/
REACT_APP_CRAWLER_API_URL=https://app-siraj-crawler-bpbde2abe5hjhpdm.uaenorth-01.azurewebsites.net/api/

# Optional: Additional configurations
# REACT_APP_ENV=development
```

### Environment-Specific Configuration

- **Development**: Uses `REACT_APP_API_URL` from `.env` or defaults to `http://localhost:8000/api/`
- **Production**: Build script sets `REACT_APP_CRAWLER_API_URL` for crawler services

### Authentication

The application uses JWT (JSON Web Token) for authentication:
- Tokens are stored in browser's `localStorage`
- Automatically attached to API requests via Axios interceptors
- Protected routes redirect to login if no valid token exists

## Development

### Starting the Development Server

```bash
npm start
```

This will:
- Start the development server on `http://localhost:3000`
- Open the application in your default browser
- Enable hot module replacement (HMR) for live reloading
- Display lint errors in the console

### Development Workflow

1. **Login**: Access the application and login with admin credentials
2. **Navigation**: Use the sidebar menu to access different management sections
3. **Make Changes**: Edit files in the `src/` directory
4. **Hot Reload**: Changes are automatically reflected in the browser
5. **Check Console**: Monitor browser console for errors or warnings

### Code Structure Best Practices

- **Components**: Reusable UI components in `src/common/components/`
- **Pages**: Page-level components in `src/pages/`
- **Services**: API service functions in `src/services/`
- **Contexts**: React Context providers in `src/contexts/`
- **Routes**: Route configuration in `src/routes/`
- **Assets**: Static files (images, icons) in `src/assets/`

## Building for Production

### Create Production Build

```bash
npm run build
```

This command:
- Creates an optimized production build in the `build/` folder
- Minifies JavaScript and CSS files
- Includes content hashes in filenames for cache busting
- Optimizes images and assets
- Sets production-specific environment variables

### Build Output

The `build/` directory will contain:
- `index.html`: Entry point
- `static/js/`: Bundled JavaScript files
- `static/css/`: Bundled CSS files
- `static/media/`: Optimized images and fonts
- Other static assets

### Verifying the Build

Test the production build locally:

```bash
# Install a static server (if not already installed)
npm install -g serve

# Serve the build directory
serve -s build -l 3000
```

## Deployment

### Docker Deployment

#### Build Docker Image

```bash
docker build -t siraj-admin:latest .
```

#### Run Docker Container

```bash
docker run -p 80:80 siraj-admin:latest
```

#### Docker Compose (Optional)

Create a `docker-compose.yml`:

```yaml
version: '3.8'
services:
  siraj-admin:
    build: .
    ports:
      - "80:80"
    environment:
      - REACT_APP_API_URL=http://your-api-url/api/
```

Run with:

```bash
docker-compose up -d
```

### Kubernetes Deployment with Helm

#### Prerequisites
- Kubernetes cluster running
- Helm 3.x installed
- kubectl configured

#### Deploy with Helm

```bash
# Update values.yaml with your configuration
helm install siraj-admin . --values values.yaml

# Or upgrade existing deployment
helm upgrade siraj-admin . --values values.yaml
```

#### Verify Deployment

```bash
kubectl get pods
kubectl get services
kubectl get ingress
```

#### Access the Application

The application will be accessible at the hostname configured in `values.yaml`:
```
http://siraj.local
```

### Azure Deployment

For Azure App Service deployment, the `.deployment` file is included to specify build configuration.

### CI/CD Integration

The project is ready for integration with:
- GitHub Actions
- Azure DevOps
- Jenkins
- GitLab CI/CD

## Project Structure

```
siraj-fe-admin/
├── public/                      # Static public assets
│   ├── index.html              # HTML template
│   └── favicon.ico             # Favicon
├── src/                        # Source code
│   ├── assets/                 # Images, icons, and static assets
│   │   └── icons/              # SVG icons
│   ├── common/                 # Shared/common code
│   │   ├── components/         # Reusable UI components
│   │   └── constants/          # Application constants
│   ├── contexts/               # React Context providers
│   │   ├── user/              # User authentication context
│   │   ├── majors/            # Majors data context
│   │   └── countryCodes/      # Country codes context
│   ├── pages/                  # Page components
│   │   ├── login/             # Login page
│   │   └── dashboard/         # Dashboard and all management pages
│   │       ├── components/    # Dashboard components
│   │       │   ├── AdvisorManagement/
│   │       │   ├── BookedSessionManagement/
│   │       │   ├── CompanyManagement/
│   │       │   ├── CouponManagement/
│   │       │   ├── CrawlingManagement/
│   │       │   ├── JobApplicationManagement/
│   │       │   ├── JobTrialManagement/
│   │       │   ├── ProductManagement/
│   │       │   ├── ProgramManagement/
│   │       │   ├── RetakeRequestManagement/
│   │       │   ├── TimeSlotManagement/
│   │       │   ├── UniversityManagement/
│   │       │   ├── UserManagement/
│   │       │   └── Table/     # Reusable table with column definitions
│   │       ├── hooks/         # Custom React hooks
│   │       └── common/        # Dashboard-specific utilities
│   ├── routes/                 # Route configuration
│   │   ├── index.js           # Main router setup
│   │   └── ProtectedRoute/    # Authentication guard
│   ├── services/               # API service layer
│   │   ├── base/              # Axios base configuration
│   │   ├── auth/              # Authentication services
│   │   ├── student/           # Student management services
│   │   ├── advisor/           # Advisor management services
│   │   ├── company/           # Company management services
│   │   ├── product/           # Product management services
│   │   ├── university/        # University management services
│   │   ├── program/           # Program management services
│   │   ├── jobTrial/          # Job trial services
│   │   ├── coupon/            # Coupon services
│   │   ├── session/           # Session management services
│   │   ├── crawlingJob/       # Crawler services
│   │   ├── country/           # Country data services
│   │   ├── major/             # Major data services
│   │   └── personality/       # Personality assessment services
│   ├── App.js                  # Root application component
│   ├── App.css                 # Global application styles
│   ├── index.js                # Application entry point
│   └── index.css               # Global CSS styles
├── templates/                  # Kubernetes templates
│   ├── deployment.yaml        # Kubernetes deployment config
│   ├── service.yaml           # Kubernetes service config
│   └── ingress.yaml           # Kubernetes ingress config
├── .dockerignore              # Docker ignore file
├── .gitignore                 # Git ignore file
├── Chart.yaml                 # Helm chart metadata
├── Dockerfile                 # Docker build configuration
├── nginx.conf                 # Nginx configuration for production
├── package.json               # Node.js dependencies and scripts
├── package-lock.json          # Locked dependency versions
├── values.yaml                # Helm chart values
└── README.md                  # This file
```

## API Integration

### Base Configuration

API requests are configured in `src/services/base/index.js`:

```javascript
const apiUrl = process.env.REACT_APP_API_URL || "http://localhost:8000/api/";
```

### Authentication Flow

1. User logs in via `/api/auth/login`
2. JWT token received and stored in `localStorage`
3. Token automatically attached to all subsequent requests
4. Token validated on each protected route access

### Service Layer Structure

Each resource has its own service module:

```javascript
// Example: src/services/product/index.js
export const getProducts = () => {
  return axiosClient.get("products");
};

export const updateProduct = (productData) => {
  const { id, ...data } = productData;
  return axiosClient.put(`products/${id}`, data);
};
```

### API Endpoints

The application integrates with the following endpoint categories:

- **Authentication**: `/api/auth/*`
- **Students**: `/api/students/*`
- **Advisors**: `/api/advisors/*`
- **Companies**: `/api/companies/*`
- **Products**: `/api/products/*`
- **Universities**: `/api/universities/*`
- **Programs**: `/api/programs/*`
- **Job Trials**: `/api/job-trials/*`
- **Sessions**: `/api/sessions/*`
- **Coupons**: `/api/coupons/*`
- **Crawling Jobs**: `/api/crawling-jobs/*`

## Available Scripts

### `npm start`

Runs the app in development mode at [http://localhost:3000](http://localhost:3000).

- Hot module replacement enabled
- Real-time error reporting
- Automatic browser refresh on file changes

### `npm test`

Launches the test runner in interactive watch mode.

```bash
npm test
```

### `npm run build`

Creates an optimized production build.

```bash
npm run build
```

Build artifacts are output to the `build/` directory.

### `npm run eject`

**Warning**: This is a one-way operation!

Ejects from Create React App, giving full control over configuration files.

```bash
npm run eject
```

Only use if you need to customize webpack, Babel, or ESLint configurations.

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run tests in CI mode (no watch)
npm test -- --coverage --watchAll=false

# Run specific test file
npm test -- src/components/Button.test.js
```

### Writing Tests

Tests are located alongside components:

```
src/
  components/
    Button.js
    Button.test.js
```

Example test structure:

```javascript
import { render, screen } from '@testing-library/react';
import Button from './Button';

test('renders button with text', () => {
  render(<Button>Click Me</Button>);
  expect(screen.getByText('Click Me')).toBeInTheDocument();
});
```

## Troubleshooting

### Common Issues

#### 1. Build Fails with "cross-env: not found"

**Solution**: Install dependencies

```bash
npm install
```

#### 2. API Requests Fail with CORS Error

**Solution**: Ensure backend API has CORS enabled for the frontend origin.

Update backend to allow:
```
Access-Control-Allow-Origin: http://localhost:3000
```

#### 3. Blank Page After Deployment

**Solution**: Check browser console for errors. Common causes:

- Incorrect `homepage` in `package.json`
- Missing environment variables
- JavaScript errors in production build

#### 4. Authentication Issues

**Solution**: Check:

- Token is being stored in localStorage
- API endpoint is correct
- Token format matches backend expectations

#### 5. Styles Not Loading

**Solution**: Ensure Ant Design CSS is imported:

```javascript
import 'antd/dist/antd.css';
```

### Debug Mode

Enable React DevTools for debugging:

```bash
# Development mode includes React DevTools automatically
npm start
```

### Logging

Add console logs for debugging:

```javascript
console.log('API Response:', response);
console.error('Error:', error);
```

Remove debug logs before production deployment.

## Contributing

We welcome contributions! Please follow these guidelines:

### Getting Started

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Run tests: `npm test`
5. Commit your changes: `git commit -m 'Add some feature'`
6. Push to the branch: `git push origin feature/your-feature`
7. Submit a pull request

### Code Style

- Follow existing code style and conventions
- Use meaningful variable and function names
- Add comments for complex logic
- Keep functions small and focused
- Use Ant Design components consistently

### Commit Messages

Follow conventional commits format:

```
feat: add new product export feature
fix: correct session time display
docs: update API integration guide
style: format code with prettier
refactor: simplify user service logic
test: add tests for product management
```

## License

This project is proprietary software owned by Feditech. All rights reserved.

---

For more information or support, please contact the development team.
