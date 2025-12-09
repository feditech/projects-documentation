# Beezi WebApp

Beezi is a comprehensive Customer Relationship Management (CRM) and business management web application designed to help organizations manage their sales pipeline, customer relationships, and business operations efficiently.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Available Scripts](#available-scripts)
- [Internationalization](#internationalization)

## Features

### Authentication & User Management

- **User Registration**: New user signup with email verification
- **Login/Logout**: Secure authentication with JWT tokens
- **Password Recovery**: Forgot password flow with OTP verification
- **Profile Management**: Users can view and edit their profile information
- **Google OAuth**: Sign in with Google integration
- **Remember Me**: Persistent login with token refresh

### Dashboard & Analytics

- **Overview Dashboard**: Comprehensive view of key business metrics
- **Statistics Cards**: Quick insights into leads, opportunities, accounts, and more
- **Top Employees Chart**: Visual representation of top-performing team members
- **Sales Achievement Target**: Gauge chart showing progress toward sales goals
- **SLA Performance**: Horizontal bar chart for Service Level Agreement tracking
- **Task Summary**: Pie chart visualization of task distribution
- **Schedule View**: Table view of upcoming schedules and their statuses
- **Team/User Filtering**: Filter dashboard data by teams or individual users

### CRM Features

#### Leads Management
- **Lead List View**: View all leads in a tabular format
- **Kanban Board**: Visual lead management with drag-and-drop functionality
- **Lead Details**: View comprehensive lead information
- **Lead Form**: Create and edit lead records
- **Lead Modal**: Quick lead preview and actions

#### Opportunities Management
- **Opportunity List View**: Track all sales opportunities
- **Kanban Board**: Visual pipeline management with stages
- **Opportunity Details**: Detailed opportunity information and history
- **Opportunity Form**: Create and modify opportunity records

#### Accounts Management
- **Account List View**: Manage all customer accounts
- **Account Details**: Comprehensive account information
- **Account Form**: Create and edit account records

#### Contacts Management
- **Contact List View**: Centralized contact management
- **Contact Form**: Add and update contact information
- **Contact Modal**: Quick contact preview

### Sales & Billing

#### Quotations
- **Quotation List View**: Track all quotations
- **Quotation Form**: Create detailed quotations with line items
- **Quotation View**: Review quotation details
- **Quotation Invoice**: Generate invoices from quotations
- **Item Modal**: Add/edit quotation line items

#### Invoices
- **Invoice List View**: Manage all invoices
- **Invoice Form**: Create and edit invoices
- **Invoice View**: Review invoice details
- **PDF Generation**: Export invoices as PDF documents

#### Payment Terms
- **Payment Terms List**: Configure payment term options
- **Payment Terms Form**: Create and modify payment terms

### Services Management
- **Services List View**: Manage service offerings
- **Services Form**: Create and edit service details

### Task Management
- **Task List View**: View all tasks
- **Task Form**: Create and manage tasks
- **Task Modal**: Quick task actions and preview

### Team & Organization

#### Teams Management
- **Teams List View**: View all teams
- **Team Form**: Create and configure teams

#### Shifts Management
- **Shifts List View**: Manage work shifts
- **Shift Form**: Create and configure shift schedules

#### Organizations
- **Organization View**: View organization details
- **Organization Form**: Edit organization settings

### User Administration
- **Users List View**: Manage system users
- **User Form**: Add and edit user accounts
- **User View**: View user details and permissions

### Leaderboard
- **Performance Rankings**: View employee performance rankings and metrics

## Technology Stack

| Category | Technology |
|----------|------------|
| **Frontend Framework** | React 18.3 |
| **Language** | TypeScript 5.6 |
| **Build Tool** | Vite 6.0 |
| **UI Components** | Ant Design 5.23 |
| **Styling** | Tailwind CSS 4.0 |
| **Routing** | React Router DOM 7.1 |
| **HTTP Client** | Axios with axios-hooks |
| **Charts** | @ant-design/charts |
| **Drag & Drop** | @dnd-kit |
| **Internationalization** | i18next, react-i18next |
| **PDF Generation** | jsPDF, jspdf-autotable, react-to-pdf |
| **QR Codes** | qrcode.react |
| **Excel Export** | xlsx |
| **Icons** | react-icons |
| **Date Handling** | Day.js |
| **Linting** | ESLint 9.20 |

## Getting Started

### Prerequisites

- Node.js (version 18 or higher recommended)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd beezi-webapp
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to `http://localhost:3000`

## Project Structure

```
src/
├── assets/              # Static assets (images, fonts, etc.)
├── components/          # Reusable UI components
│   ├── alerts/          # Alert and notification components
│   ├── business/        # Business logic components
│   ├── controls/        # Form controls and inputs
│   ├── layout/          # Layout components (cards, grids, charts)
│   ├── multilingual/    # Language-related components
│   └── route/           # Routing components (protected routes)
├── context/             # React Context providers
│   ├── authcontext      # Authentication state management
│   └── notificationcontext # Notification handling
├── locales/             # Internationalization files
│   ├── ar/              # Arabic translations
│   └── en/              # English translations
├── pages/               # Page components
│   ├── account/         # Authentication pages (login, signup, OTP)
│   ├── accounts/        # Account management pages
│   ├── contacts/        # Contact management pages
│   ├── invoices/        # Invoice management pages
│   ├── leads/           # Lead management pages
│   ├── opportunities/   # Opportunity management pages
│   ├── organizations/   # Organization settings pages
│   ├── paymentterms/    # Payment terms pages
│   ├── profiles/        # User profile pages
│   ├── quotations/      # Quotation management pages
│   ├── services/        # Service management pages
│   ├── shifts/          # Shift management pages
│   ├── tasks/           # Task management pages
│   ├── teams/           # Team management pages
│   └── users/           # User administration pages
├── shared/              # Shared utilities and services
│   ├── api/             # API configuration and endpoints
│   ├── hooks/           # Custom React hooks
│   └── services/        # Business logic services
├── templates/           # Page templates/layouts
├── types/               # TypeScript type definitions
├── App.tsx              # Main application component
└── index.tsx            # Application entry point
```

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server on port 3000 |
| `npm run build` | Build for production (TypeScript compilation + Vite build) |
| `npm run lint` | Run ESLint for code quality checks |
| `npm run preview` | Preview production build locally |

## Internationalization

Beezi WebApp supports multiple languages:

- **English (en)**: Default language
- **Arabic (ar)**: Full RTL support

Language preferences are persisted in localStorage and automatically applied on application load. Users can switch languages at any time through the language selector in the application.

### Adding New Languages

1. Create a new folder under `src/locales/` with the language code
2. Add a `translation.json` file with all required translation keys
3. Configure the language in the i18n setup

## Security Features

- **Protected Routes**: Role-based access control for all authenticated routes
- **Restricted Routes**: Module and action-based permission checks
- **JWT Token Management**: Secure token handling with automatic refresh
- **Session Management**: Configurable session persistence with "Remember Me" option

## License

This project is proprietary software. All rights reserved.
