# Document Warehouse Web Application

A comprehensive document management system (DMS) built with React, TypeScript, and Material-UI. This web application provides a complete solution for managing physical document storage, lending operations, disposal workflows, and administrative tasks.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Running the Application](#running-the-application)
- [Available Scripts](#available-scripts)
- [Architecture](#architecture)
  - [Authentication & Authorization](#authentication--authorization)
  - [Routing](#routing)
  - [Internationalization](#internationalization)
  - [Theming](#theming)
- [API Integration](#api-integration)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Document Warehouse Web Application is designed to help organizations manage their physical document archives efficiently. It provides features for document cataloging, storage location tracking (halls, cabinets, columns, shelves, boxes, envelopes), lending management, and document disposal workflows.

## Features

### Document Management
- **Document Explorer (DMS)**: Navigate and manage documents using a hierarchical tree structure
- **Storage Location Tracking**: Organize documents by Hall → Cabinet → Column → Shelf → Box → Envelope
- **Barcode Generation**: Generate and print barcodes for physical document tracking
- **Document Search**: Advanced search capabilities with OCR support
- **PDF Operations**: View, download, and generate PDF reports

### Lending Management
- **Lending Requests**: Create and track document lending requests
- **Active Lending**: Monitor currently lent documents
- **Lending Extensions**: Request and approve lending period extensions
- **Return Tracking**: Track document returns and overdue items

### Disposal Workflow
- **Disposal Requests**: Create requests for document disposal
- **Approval Workflow**: Multi-step approval process for disposal
- **Disposal History**: Track previously disposed documents

### Administrative Features
- **User Management**: Create and manage user accounts with role-based access
- **Entity Management**: Manage organizational entities
- **Department Management**: Configure departments within entities
- **Hall Management**: Configure physical storage halls and their capacity
- **Attachment Types**: Define and manage document attachment types

### Dashboard & Analytics
- **User Statistics**: View personal lending and disposal statistics
- **Hall Statistics**: Monitor hall usage and capacity
- **Activity Logs**: Track system activities and user actions
- **Date Range Filtering**: Filter statistics by custom date ranges

### Internationalization
- **Multi-language Support**: Full support for English and Arabic
- **RTL Support**: Right-to-left layout for Arabic language
- **Hijri Calendar**: Support for both Gregorian and Hijri date formats

## Tech Stack

### Core
- **React 19** - UI library
- **TypeScript 5.7** - Type-safe JavaScript
- **Vite 6** - Build tool and dev server

### UI Framework
- **Material-UI (MUI) 6** - Component library
  - `@mui/material` - Core components
  - `@mui/icons-material` - Icon set
  - `@mui/x-data-grid` - Data tables
  - `@mui/x-date-pickers` - Date/time pickers
  - `@mui/x-charts` - Charts and graphs
  - `@mui/x-tree-view` - Tree view components
  - `@mui/lab` - Lab components

### State Management & Routing
- **React Router 7** - Client-side routing
- **React Context** - State management for auth, config, and notifications

### Internationalization
- **i18next** - Internationalization framework
- **react-i18next** - React bindings for i18next
- **moment-hijri** - Hijri calendar support

### PDF & Document Processing
- **jsPDF** - PDF generation
- **jspdf-autotable** - PDF table generation
- **pdf-lib** - PDF manipulation
- **pdfjs-dist** - PDF viewing
- **Tesseract.js** - OCR capabilities

### Other Libraries
- **Axios** - HTTP client
- **xlsx** - Excel file processing
- **export-to-csv** - CSV export functionality
- **JsBarcode** - Barcode generation
- **react-dropzone** - File upload handling

## Project Structure

```
src/
├── assets/                    # Static assets (fonts, images)
├── components/                # Reusable UI components
│   ├── alerts/               # Alert/notification components
│   ├── business/             # Business logic components
│   ├── charts/               # Chart components
│   ├── controls/             # Form controls and inputs
│   ├── editmodals/           # Modal dialog components
│   ├── layout/               # Layout components (Grid, Box, etc.)
│   ├── multilingual/         # i18n configuration
│   ├── pages/                # Page-specific components
│   └── route/                # Route protection components
├── context/                   # React Context providers
│   ├── authcontext.tsx       # Authentication state
│   ├── configcontext.tsx     # Application configuration
│   └── notificationcontext.tsx # Notification handling
├── locales/                   # Translation files
│   ├── ar/                   # Arabic translations
│   └── en/                   # English translations
├── pages/                     # Page components
│   ├── account/              # Login, password reset
│   ├── disposal/             # Disposal management
│   ├── lending/              # Lending management
│   ├── settings/             # Administrative settings
│   ├── dashboard.tsx         # Main dashboard
│   ├── dms.tsx              # Document explorer
│   ├── logs.tsx             # Activity logs
│   └── statistics.tsx       # Statistics page
├── routes/                    # Route configuration
│   └── routeConfig.ts        # Route definitions with ACL
├── shared/                    # Shared utilities
│   ├── hooks/                # Custom React hooks
│   ├── services/             # API service modules
│   ├── authorization.ts      # Authorization utilities
│   ├── globals.ts           # Global constants and utilities
│   └── pdfoperations.ts     # PDF utilities
├── templates/                 # Page layout templates
│   ├── accounttemplate.tsx   # Public pages layout
│   ├── listpagetemplate.tsx  # List page layout
│   └── maintemplate.tsx      # Authenticated pages layout
├── App.tsx                    # Main application component
├── main.tsx                   # Application entry point
└── theme.ts                   # MUI theme configuration
```

## Getting Started

### Prerequisites

- **Node.js** 18.x or higher
- **npm** 9.x or higher (or yarn/pnpm)
- A running backend API server

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd document-wh-webapp
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

### Configuration

1. **API Configuration**
   
   The application loads its API URL from `public/config.json`:
   ```json
   {
     "APIURL": "https://your-api-server.com/api/"
   }
   ```

2. **Environment Variables** (Optional)
   
   Create a `.env` file in the root directory:
   ```env
   REACT_APP_BASE_API=https://your-api-server.com/api/
   ```

### Running the Application

**Development mode:**
```bash
npm run dev
```
The application will be available at `http://localhost:3000`

**Production build:**
```bash
npm run build
```

**Preview production build:**
```bash
npm run preview
```

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server on port 3000 |
| `npm run build` | Type-check and build for production |
| `npm run build-temp` | Build without type-checking |
| `npm run lint` | Run ESLint for code quality |
| `npm run preview` | Preview production build locally |

## Architecture

### Authentication & Authorization

The application uses a token-based authentication system with role-based access control (RBAC).

**User Roles:**
- **Super Admin**: Full access to all features and settings
- **Hall Admin**: Access to assigned halls and limited settings
- **Regular User**: Access based on assigned claims

**Claims System:**
Claims control access to specific features:
- `ADD_STORAGE_UNITS` - Create storage locations
- `ADD_DOCUMENTS` - Add new documents
- `PRINT_BARCODE` - Generate barcodes
- `CREATE_LENDING_REQUEST` - Create lending requests
- `PERFORM_LENDING_PRINT` / `EXTEND` / `RETURN` - Lending operations
- `CREATE_DISPOSAL_REQUEST` / `PERFORM_DISPOSAL_ACTIONS` - Disposal operations
- `VIEW_STATISTICS` - Access statistics
- `VIEW_LOGS` - Access activity logs

**Implementation:**
```typescript
// Check user claims
const { hasClaim, hasAnyClaim } = useAuthContext();

// Single claim check
if (hasClaim('CREATE_LENDING_REQUEST')) {
  // User can create lending requests
}

// Multiple claims (any)
if (hasAnyClaim(['VIEW_STATISTICS', 'VIEW_LOGS'])) {
  // User can access at least one feature
}
```

### Routing

Routes are defined in `src/routes/routeConfig.ts` with ACL (Access Control List) integration:

```typescript
{
  id: "lending",
  label: "Lending",
  path: "/lending",
  element: LendingTabs,
  showInMenu: true,
  requiredClaims: {
    claims: [CLAIM_TYPES.CREATE_LENDING_REQUEST, ...],
    mode: "any"  // "any" or "all"
  }
}
```

**Protected Routes:**
- All authenticated routes are wrapped with `ProtectedRoute`
- Individual routes are wrapped with `ACLRoute` for claim-based access

### Internationalization

The application supports English and Arabic with full RTL support.

**Adding Translations:**
1. Add keys to `src/locales/en/translation.json`
2. Add corresponding Arabic translations to `src/locales/ar/translation.json`

**Usage in Components:**
```typescript
import { useTranslation } from 'react-i18next';

const { t, i18n } = useTranslation();

// Translate text
<Typography>{t('Dashboard')}</Typography>

// Check current language
if (i18n.language === 'ar') {
  // Arabic-specific logic
}
```

### Theming

The application uses Material-UI theming with custom color palette:

**Primary Colors:**
- Main: `#0B8DCD` (Blue)
- Secondary: `#FB9D4B` (Orange)

**Custom Theme Properties:**
- Dynamic RTL/LTR direction based on language
- Custom palette for DMS-specific styling
- Font switching between Roboto (English) and Tajawal (Arabic)

## API Integration

API services are located in `src/shared/services/`. Each service module provides functions for specific API endpoints.

**Available Services:**
- `authservice.ts` - Authentication endpoints
- `documentservice.ts` - Document CRUD operations
- `folderservice.ts` - Storage location management
- `lendingservice.ts` - Lending operations
- `disposalservice.ts` - Disposal operations
- `userservices.ts` - User management
- `entityservice.ts` - Entity management
- `departmentservice.ts` - Department management
- `hallservice.ts` - Hall management
- `logsservice.ts` - Activity logs
- `dashboardservice.ts` - Dashboard statistics

**Usage Example:**
```typescript
import useDocumentService from '../shared/services/documentservice';

const { getDocuments, createDocument } = useDocumentService();

// Fetch documents
const documents = await getDocuments(params);
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Style

- Follow TypeScript best practices
- Use ESLint for code quality (`npm run lint`)
- Follow existing code patterns and naming conventions
- Add translations for any user-facing text

## License

This project is proprietary software. All rights reserved.
