# Fixed Assets Web Application

A comprehensive web application for managing fixed assets within an organization. Built with React and TypeScript, this application provides a complete solution for tracking, categorizing, and reporting on organizational assets.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Configuration](#environment-configuration)
- [Usage Guide](#usage-guide)
  - [Authentication](#authentication)
  - [Dashboard](#dashboard)
  - [Asset Management](#asset-management)
  - [Reports](#reports)
  - [Settings](#settings)
- [Project Structure](#project-structure)
- [Internationalization](#internationalization)
- [API Integration](#api-integration)
- [Available Scripts](#available-scripts)

## Overview

The Fixed Assets Web Application is designed to help organizations efficiently manage their physical assets throughout their lifecycle. From acquisition to disposal, this application provides tools for tracking asset locations, conditions, custodians, and generating comprehensive reports.

## Features

### Core Features

- **Dashboard Analytics**: Visual representation of asset data including:
  - Asset transaction pie charts (Transferred, Audited, Added, Warranty, Tagged, Elimination, Disposed, Maintain)
  - Asset acquisition trends over time (line charts)
  - Assets per branch distribution
  - Assets per status breakdown
  - Summary cards for inactive, non-capitalized, under construction, and disposed assets

- **Asset Management**:
  - Complete CRUD operations for fixed assets
  - Asset code, description, and entry date tracking
  - Asset status management (Active, Inactive, Defected, Disposed)
  - Asset condition tracking
  - Manufacturer details (brand, model, serial code, specifications)
  - Image attachment support
  - Pending asset workflow for approval processes

- **Hierarchical Location Management**:
  - 5-level location hierarchy (Country → City → Branch → Location → Sub Location)
  - Tree view interface for easy navigation
  - Location-based asset filtering

- **Category Management**:
  - 4-level category hierarchy (Category → Sub Category → Group → Sub Group)
  - Tree view organization
  - Flexible categorization system

- **Department Management**:
  - Department creation and management
  - Department-based asset assignment

- **User Management**:
  - User administration
  - Role-based access control

- **Advanced Reporting**:
  - Multi-criteria filtering:
    - By user who entered the asset
    - By asset codes
    - By description
    - By date range (entry date)
    - By location hierarchy
    - By category hierarchy
    - By manufacturer details
    - By custodian
    - By asset condition
    - By asset status
    - By department
  - Export capabilities
  - PDF generation

### Additional Features

- **Multi-language Support**: Full support for English and Arabic (RTL)
- **Multi-calendar Support**: Gregorian and Hijri calendar systems
- **Responsive Design**: Works across desktop and mobile devices
- **Remember Me**: Persistent login sessions
- **Password Recovery**: Forgot password flow with email verification

## Technology Stack

| Category | Technology |
|----------|------------|
| **Frontend Framework** | React 18.x |
| **Language** | TypeScript 4.9.x |
| **UI Components** | Material-UI (MUI) 5.x |
| **State Management** | React Context API |
| **Routing** | React Router DOM 6.x |
| **HTTP Client** | Axios |
| **Internationalization** | i18next, react-i18next |
| **Date Handling** | Moment.js, Moment Hijri (for Hijri calendar support) |
| **Data Grid** | MUI X Data Grid |
| **Charts** | MUI X Charts |
| **PDF Generation** | jsPDF, jsPDF-AutoTable |
| **Excel Export** | xlsx |
| **Build Tool** | Create React App |

## Getting Started

### Prerequisites

- Node.js (v16 or higher recommended)
- npm (v8 or higher) or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd fixedassets-webapp
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```

4. Open [http://localhost:3000](http://localhost:3000) in your browser.

### Environment Configuration

The application uses environment variables for configuration. Create or modify the following files in the project root:

#### `.env` (Production)
```env
REACT_APP_BASE_API=https://your-api-server.com/api/
```

#### `.env.development` (Development)
```env
REACT_APP_BASE_API=https://localhost:7027/api/
```

**Environment Variables:**

| Variable | Description |
|----------|-------------|
| `REACT_APP_BASE_API` | Base URL for the backend API server |

## Usage Guide

### Authentication

1. **Login**: Navigate to the application root to access the login page
   - Enter your username (email format required)
   - Enter your password (minimum 8 characters with uppercase, lowercase, number, and special character)
   - Optionally enable "Remember Me" for persistent sessions

2. **Password Recovery**:
   - Click "Forgot my password" on the login page
   - Enter your email address
   - Follow the reset password link sent to your email

### Dashboard

The dashboard provides an at-a-glance view of your asset portfolio:

- **Asset Summary Card**: Total asset count with breakdowns by status
- **Asset Transactions**: Pie chart showing distribution of asset activities
- **Asset Acquisition Per Year**: Line chart displaying acquisition trends
- **Asset Per Branch**: Distribution of assets across organizational branches
- **Asset Per Status**: Current status distribution of all assets

### Asset Management

#### Fixed Assets Cards
Access via the sidebar menu to view all registered assets:

- **View Assets**: Browse the complete list with search and filter capabilities
- **Add Asset**: Click the add button to register a new asset
- **Edit Asset**: Click on an asset row to modify its details
- **Delete Asset**: Remove assets (with confirmation)
- **Generate Report**: Apply filters and generate custom reports

#### Pending Assets
View and manage assets awaiting approval or additional processing.

### Reports

The Reports section provides powerful filtering capabilities:

1. **Basic Filters**:
   - Entered By (user who created the asset record)
   - Asset Codes
   - Description
   - Date Range (From/To entry dates)

2. **Location Filters**:
   - Country
   - City
   - Branch
   - Location
   - Sub Locations
   - Department

3. **Category Filters**:
   - Category
   - Sub Category
   - Group
   - Sub Group

4. **Manufacturer Filters**:
   - Serial Code
   - Brand
   - Model

5. **Other Filters**:
   - Custodian
   - Asset Condition
   - Asset Status

Click "Generate Report" to view filtered results in a data grid format.

### Settings

Access configuration options from the Settings menu:

- **Locations**: Manage the 5-level location hierarchy using a tree view interface
- **Categories**: Manage the 4-level category hierarchy using a tree view interface
- **Departments**: Add, edit, and delete departments
- **Users**: Manage user accounts and permissions

## Project Structure

```
src/
├── assets/                 # Static assets (images, fonts)
├── components/
│   ├── addeditmodals/     # Modal dialogs for add/edit operations
│   ├── alerts/            # Alert and notification components
│   ├── business/          # Business-specific components
│   │   ├── appbar/        # Application header/navbar
│   │   ├── menu/          # Navigation menu components
│   │   └── listpagedx.tsx # Reusable list page component
│   ├── charts/            # Chart components (Pie, Line)
│   ├── controls/          # Form controls (TextField, Select, DatePicker, etc.)
│   ├── layout/            # Layout components (Grid, Box, Card)
│   ├── multilingual/      # i18n configuration
│   └── route/             # Route protection components
├── context/
│   ├── authcontext.tsx    # Authentication state management
│   └── notificationcontext.tsx  # Notification/toast management
├── locales/
│   ├── ar/                # Arabic translations
│   └── en/                # English translations
├── pages/
│   ├── account/           # Login, password reset pages
│   ├── asset/             # Asset management pages
│   ├── settings/          # Settings pages (locations, categories, etc.)
│   ├── dashboard.tsx      # Main dashboard
│   └── reports.tsx        # Reports page
├── shared/
│   ├── api/               # API configuration
│   ├── hooks/             # Custom React hooks
│   ├── services/          # API service functions
│   ├── globals.ts         # Global utilities
│   └── typetranslator.ts  # Type translation utilities
├── templates/             # Page layout templates
├── App.tsx                # Main application component
└── index.tsx              # Application entry point
```

## Internationalization

The application supports multiple languages:

- **English (en)**: Left-to-right layout
- **Arabic (ar)**: Right-to-left layout with Hijri calendar support

### Adding Translations

1. Navigate to `src/locales/{language}/`
2. Add or modify translation keys in the translation files
3. Use the `useTranslation` hook in components:
   ```typescript
   const { t } = useTranslation();
   return <span>{t('Your Translation Key')}</span>;
   ```

### Language Switching

The application automatically detects browser language preferences and supports runtime language switching via the user interface.

## API Integration

The application communicates with a backend API for all data operations.

### API Endpoints

| Entity | Endpoints |
|--------|-----------|
| **Authentication** | `POST /login`, `POST /refresh-token`, `POST /forgot-password` |
| **Assets** | `GET/POST/PUT/DELETE /Asset`, `GET /Asset/{id}` |
| **Pending Assets** | `GET/POST/PUT/DELETE /PendingAsset` |
| **Locations** | `GET/POST/PUT/DELETE /Location` |
| **Categories** | `GET/POST/PUT/DELETE /Category` |
| **Departments** | `GET/POST/PUT/DELETE /Department` |
| **Users** | `GET/POST/PUT/DELETE /User` |
| **Employees** | `GET /Employee` |
| **Reports** | `POST /Report` |
| **Asset Types** | `GET /AssetType`, `GET /AssetConditionType`, `GET /AssetStatusType` |

### Authentication

The API uses JWT (JSON Web Token) authentication. Tokens are automatically:
- Stored in local storage (encoded)
- Refreshed before expiration
- Included in API request headers

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in development mode at [http://localhost:3000](http://localhost:3000).

The page will reload when you make edits. You will also see any lint errors in the console.

### `npm test`

Launches the test runner in interactive watch mode.

### `npm run build`

Builds the app for production to the `build` folder. The build is minified and optimized for best performance.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

Ejects the Create React App configuration for full customization control.

---

## License

This project is proprietary software. All rights reserved.

## Support

For support inquiries, please contact the development team.
