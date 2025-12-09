# DocLink CMS - Healthcare Management System

![DocLink CMS](https://img.shields.io/badge/version-0.1.0-blue.svg)
![React](https://img.shields.io/badge/React-17.0.2-61DAFB?logo=react)
![Material-UI](https://img.shields.io/badge/Material--UI-5.4.3-0081CB?logo=material-ui)
![Redux](https://img.shields.io/badge/Redux-4.1.2-764ABC?logo=redux)

DocLink CMS is a comprehensive Content Management System designed for healthcare platforms. It provides a unified dashboard for managing doctors, patients, lab services, healthcare content, and administrative operations.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [Documentation](#documentation)
- [Project Structure](#project-structure)
- [Available Scripts](#available-scripts)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

DocLink CMS is a React-based web application that serves as the administrative interface for a healthcare platform. It enables administrators to manage healthcare providers, patients, content, and platform operations through an intuitive dashboard.

### Key Capabilities

- **Doctor Management**: Profile management, verification requests, specializations, and subscriptions
- **Patient Management**: User profiles and health records
- **Lab Services**: Laboratory management, test categories, and service offerings
- **Content Management**: Blogs, health tips, banners, and educational content
- **Session Management**: Video consultation sessions and chat requests
- **Financial Operations**: Transactions, settlements, and payout policies
- **User Feedback**: Problem reports and session feedback collection
- **Role & Permission Management**: Access control and user role configuration

## ✨ Features

### Doctor Module
- Doctor profile creation and management
- Verification and approval workflow
- Specialization and disease management
- Health concern categorization
- Subscription plan management
- Doctor connection tracking
- Reviews and ratings system
- Sales referral tracking

### Patient Module
- Patient profile management
- Health record access
- Activity tracking

### Lab Management
- Laboratory profile management
- Lab service category organization
- Test category management
- Service offering configuration

### Content Management
- Blog creation and publication
- Blog category management
- Health tips and educational content
- Banner management for app screens
- Short messages and stories
- Doctor directory management

### Administrative Features
- Role-based access control
- Permission management
- User management and creation
- Activity logging
- Module management
- Policy configuration (Terms & Conditions, Privacy Policy, Payout Policies)

### Session & Communication
- Active session monitoring
- Chat request management
- Video call package configuration
- Emergency contact management

### Financial Management
- Top-up tracking
- Transaction monitoring
- Settlement processing
- Payout policy management

## 🛠 Technology Stack

### Frontend
- **React 17.0.2**: UI library
- **Material-UI (MUI) 5.4.3**: Component library
- **Redux Toolkit**: State management
- **React Router 6.2.1**: Routing
- **Styled Components**: CSS-in-JS styling

### Rich Text & Data Visualization
- **TinyMCE**: Rich text editing
- **React Quill**: Alternative text editor
- **Chart.js**: Data visualization
- **Material Table**: Advanced data tables

### Maps & Location
- **React Google Maps API**: Location services
- **React Places Autocomplete**: Address autocomplete

### Form & Date Management
- **React DatePicker**: Date selection
- **React Select**: Enhanced select components
- **Flatpickr**: Alternative date picker

### Utilities
- **Axios**: HTTP client
- **Redux Logger**: State debugging
- **Redux Persist**: State persistence
- **React Toastify**: Notifications
- **File Saver**: File download functionality
- **Moment.js & date-fns**: Date manipulation

### Development Tools
- **Webpack**: Module bundler
- **Babel**: JavaScript compiler
- **ESLint**: Code linting
- **Prettier**: Code formatting

## 🚀 Getting Started

### Prerequisites

- Node.js (v14 or higher recommended)
- npm or yarn package manager
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/feditech/doclink-cms-updated.git
cd doclink-cms-updated
```

2. Install dependencies:
```bash
npm install
```

3. Configure environment variables:
Create a `.env` file in the root directory and add necessary configuration:
```env
REACT_APP_API_BASE_URL=your_api_base_url
REACT_APP_GOOGLE_MAPS_API_KEY=your_google_maps_key
```

4. Start the development server:
```bash
npm start
```

The application will open at [http://localhost:3000](http://localhost:3000).

### Building for Production

```bash
npm run build
```

This creates an optimized production build in the `build` folder.

## 📚 Documentation

For detailed documentation, please refer to:

- [**ARCHITECTURE.md**](./docs/ARCHITECTURE.md) - System architecture and design patterns
- [**DEVELOPMENT.md**](./docs/DEVELOPMENT.md) - Development setup and guidelines
- [**API.md**](./docs/API.md) - API endpoints and integration
- [**DEPLOYMENT.md**](./docs/DEPLOYMENT.md) - Deployment instructions
- [**USER_GUIDE.md**](./docs/USER_GUIDE.md) - User manual and workflows
- [**FEATURES.md**](./docs/FEATURES.md) - Detailed feature documentation
- [**SECURITY.md**](./docs/SECURITY.md) - Security guidelines and best practices
- [**TROUBLESHOOTING.md**](./docs/TROUBLESHOOTING.md) - Common issues and solutions

## 📁 Project Structure

```
doclink-cms-updated/
├── public/                 # Static files
│   ├── index.html         # HTML template
│   └── favicon.ico        # App icon
├── src/
│   ├── api/               # API configuration and endpoints
│   ├── assets/            # Images, fonts, and static assets
│   ├── components/        # Reusable React components
│   ├── hooks/             # Custom React hooks
│   ├── redux/             # Redux store, slices, and actions
│   ├── screens/           # Page components
│   │   ├── authorized/    # Authenticated user screens
│   │   └── unauthorized/  # Public screens (login, forgot password)
│   ├── utils/             # Utility functions and helpers
│   ├── App.js             # Main application component
│   ├── App.css            # Global styles
│   ├── index.js           # Application entry point
│   ├── menu.js            # Navigation menu component
│   └── menuitems.js       # Menu configuration
├── .babelrc               # Babel configuration
├── .prettierrc            # Prettier configuration
├── webpack.config.js      # Webpack configuration
├── package.json           # Project dependencies
└── README.md              # This file
```

## 📜 Available Scripts

### `npm start`
Runs the app in development mode at [http://localhost:3000](http://localhost:3000). The page reloads on changes.

### `npm test`
Launches the test runner in interactive watch mode.

### `npm run build`
Builds the app for production to the `build` folder with optimized bundles.

### `npm run dev`
Runs webpack-dev-server in development mode.

### `npm run prod`
Creates a production webpack build.

### `npm run eject`
**Note**: This is a one-way operation. Ejects from Create React App to gain full configuration control.

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please read [DEVELOPMENT.md](./docs/DEVELOPMENT.md) for detailed contribution guidelines.

## 📄 License

This project is proprietary software. All rights reserved.

## 🆘 Support

For support and questions:
- Create an issue in the GitHub repository
- Contact the development team
- Refer to [TROUBLESHOOTING.md](./docs/TROUBLESHOOTING.md) for common issues

---

**Built with ❤️ for better healthcare management**
