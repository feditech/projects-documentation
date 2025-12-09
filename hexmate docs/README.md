# HexMate

HexMate is a comprehensive enterprise management platform that integrates three powerful modules to streamline organizational operations. Built with React and TypeScript, HexMate provides a modern, intuitive interface for document management, correspondence tracking, and visitor management.

## Overview

HexMate combines three integrated modules:

- **DMS (Document Management System)**: Organize, store, and manage documents with advanced features including version control, document profiles, and hierarchical cabinet structures.
- **CTS (Correspondence Tracking System)**: Track and manage organizational correspondence with workflow automation, routing groups, and comprehensive reporting.
- **VMS (Visitor Management System)**: Manage visitor appointments, check-ins, and workflows with real-time tracking and notifications.

## Key Features

### Document Management System (DMS)
- Hierarchical document organization with cabinets and folders
- Document profiles and categories
- Structure templates for consistent organization
- Version control and document editing
- Content editing requests and approval workflows
- Advanced search and attachment management
- Comprehensive audit logs and reporting

### Correspondence Tracking System (CTS)
- Correspondence lifecycle management
- Workflow automation and routing
- Entity management and delegation
- Document template system
- Privacy and importance level classification
- Advanced filtering and search
- Real-time dashboards and analytics

### Visitor Management System (VMS)
- Appointment scheduling and management
- Visitor check-in/check-out tracking
- Workflow configuration
- Dashboard with real-time statistics
- Appointment history and archiving

## Technology Stack

- **Frontend**: React 18.2, TypeScript 4.9
- **UI Framework**: Material-UI (MUI) 5.14
- **Routing**: React Router DOM 6.14
- **State Management**: React Context API
- **PDF Generation**: jsPDF, PDF-lib, @react-pdf/renderer
- **Document Processing**: Dynamsoft Document Web Twain (DWT)
- **OCR**: Tesseract.js
- **Internationalization**: i18next
- **Charts & Visualization**: MUI X-Charts, MUI X-Data-Grid

## Quick Start

### Prerequisites

- Node.js (version 16 or higher)
- npm (version 7 or higher)

### Installation

```bash
# Clone the repository
git clone https://github.com/feditech/hexmate.git

# Navigate to project directory
cd hexmate

# Install dependencies
npm install
```

### Configuration

Create or update the `.env` file in the root directory:

```env
REACT_APP_BASE_API=https://your-api-endpoint.com/api/
```

Configure modules in `public/config.json`:

```json
{
  "modules": [
    {"id": 1, "name": "DMS", "link": "/dms/documents"},
    {"id": 2, "name": "CTS", "link": "/cts/dashboard"},
    {"id": 3, "name": "VMS", "link": "/vms/dashboard"}
  ]
}
```

### Running the Application

```bash
# Development mode
npm start

# Build for production
npm run build

# Run tests
npm test
```

The application will be available at [http://localhost:3000](http://localhost:3000).

## Documentation

Comprehensive documentation is available in the `/docs` directory:

- [Architecture](docs/ARCHITECTURE.md) - System architecture and design patterns
- [Installation](docs/INSTALLATION.md) - Detailed installation and setup guide
- [Configuration](docs/CONFIGURATION.md) - Configuration options and environment variables
- [Development](docs/DEVELOPMENT.md) - Development guidelines and best practices
- [Deployment](docs/DEPLOYMENT.md) - Production deployment guide
- [API Integration](docs/API.md) - API endpoints and integration guide
- [DMS Module](docs/DMS.md) - Document Management System documentation
- [CTS Module](docs/CTS.md) - Correspondence Tracking System documentation
- [VMS Module](docs/VMS.md) - Visitor Management System documentation
- [Troubleshooting](docs/TROUBLESHOOTING.md) - Common issues and solutions
- [Security](docs/SECURITY.md) - Security best practices and considerations
- [Contributing](docs/CONTRIBUTING.md) - Contribution guidelines

## User Manuals

User manuals for each module are available in the `public` folder:
- [DMS User Manual](public/usermanual_dms.pdf)
- [CTS User Manual](public/usermanual_cts.pdf)
- [VMS User Manual](public/usermanual_vms.pdf)

## Project Structure

```
hexmate/
├── public/              # Static assets and configuration
├── src/
│   ├── assets/         # Images, fonts, and other assets
│   ├── components/     # Reusable React components
│   ├── context/        # React Context providers
│   ├── locales/        # Internationalization files
│   ├── pages/          # Page components (DMS, CTS, VMS)
│   ├── shared/         # Shared utilities and hooks
│   ├── templates/      # Layout templates
│   └── App.tsx         # Main application component
├── docs/               # Documentation
└── package.json        # Project dependencies and scripts
```

## Support

For issues, questions, or contributions, please refer to:
- [Issue Tracker](https://github.com/feditech/hexmate/issues)
- [Contributing Guidelines](docs/CONTRIBUTING.md)
- [Security Policy](docs/SECURITY.md)

## License

[Add license information here]

## Acknowledgments

HexMate uses several open-source libraries and tools. See `package.json` for a complete list of dependencies.
