# Projects Documentation Repository

Welcome to the **FediTech Projects Documentation** repository! This centralized documentation hub contains comprehensive documentation for all FediTech software projects and applications.

## 📋 Table of Contents

- [Overview](#overview)
- [Projects](#projects)
  - [Beezi WebApp](#beezi-webapp)
  - [Units - Warehouse Management System](#units---warehouse-management-system)
  - [HexMate Enterprise Platform](#hexmate-enterprise-platform)
  - [FuelApp](#fuelapp)
  - [Document Warehouse](#document-warehouse)
  - [Fixed Asset Management](#fixed-asset-management)
  - [DocLink](#doclink)
  - [Siraj](#siraj)
- [Repository Structure](#repository-structure)
- [How to Use This Repository](#how-to-use-this-repository)
- [Contributing](#contributing)
- [Support](#support)

## Overview

This repository serves as a centralized documentation hub for FediTech's suite of enterprise applications. Each project has its own dedicated documentation folder containing comprehensive guides, API references, architecture documentation, and user manuals.

## Projects

### Beezi WebApp

**Location:** [`beezi docs/`](./beezi%20docs/)

A comprehensive Customer Relationship Management (CRM) and business management web application designed to help organizations manage their sales pipeline, customer relationships, and business operations efficiently.

**Key Features:**
- User authentication and management
- Dashboard with analytics
- Leads, opportunities, accounts, and contacts management
- Quotations and invoicing
- Task management
- Team and organization management
- Multi-language support (English/Arabic)

**Tech Stack:** React 18.3, TypeScript 5.6, Vite 6.0, Ant Design 5.23, Tailwind CSS 4.0

[📖 Read Full Documentation →](./beezi%20docs/README.md)

---

### Units - Warehouse Management System

**Location:** [`units_documentation/`](./units_documentation/)

A modern warehouse management and logistics system designed to streamline inventory operations, order fulfillment, and warehouse processes.

**Key Features:**
- Real-time inventory tracking across multiple warehouses
- Inbound logistics management (receiving to putaway)
- Outbound order fulfillment (picking, packing, dispatch)
- SKU and product catalog management
- Customer and supplier management
- Reporting and analytics
- Multi-language support (English/Arabic)
- Role-based access control

**Documentation Contents:**
- [Overview](./units_documentation/overview.md)
- [Getting Started](./units_documentation/getting-started.md)
- [User Guide](./units_documentation/user-guide.md)
- [Features](./units_documentation/features.md)
- [Workflows](./units_documentation/workflows.md)
- [User Roles](./units_documentation/user-roles.md)
- [API Reference](./units_documentation/api-reference.md)
- [Architecture](./units_documentation/architecture.md)
- [Configuration](./units_documentation/configuration.md)
- [Troubleshooting](./units_documentation/troubleshooting.md)
- [FAQ](./units_documentation/faq.md)

[📖 Read Full Documentation →](./units_documentation/README.md)

---

### HexMate Enterprise Platform

**Location:** [`hexmate docs/`](./hexmate%20docs/)

A comprehensive enterprise management platform that integrates three powerful modules: Document Management System (DMS), Correspondence Tracking System (CTS), and Visitor Management System (VMS).

**Key Modules:**
- **DMS**: Document organization, version control, hierarchical cabinet structures
- **CTS**: Correspondence tracking with workflow automation and routing
- **VMS**: Visitor appointment management and check-in/check-out tracking

**Tech Stack:** React 18.2, TypeScript 4.9, Material-UI 5.14, jsPDF, Dynamsoft Document Web Twain

**Documentation Contents:**
- [Architecture](./hexmate%20docs/docs/ARCHITECTURE.md)
- [Installation](./hexmate%20docs/docs/INSTALLATION.md)
- [Configuration](./hexmate%20docs/docs/CONFIGURATION.md)
- [Development](./hexmate%20docs/docs/DEVELOPMENT.md)
- [Deployment](./hexmate%20docs/docs/DEPLOYMENT.md)
- [API Integration](./hexmate%20docs/docs/API.md)
- [Troubleshooting](./hexmate%20docs/docs/TROUBLESHOOTING.md)
- [Security](./hexmate%20docs/docs/SECURITY.md)

[📖 Read Full Documentation →](./hexmate%20docs/README.md)

---

### FuelApp

**Location:** [`fuel app docs/`](./fuel%20app%20docs/)

A comprehensive fuel management system designed to streamline fleet operations, fuel consumption tracking, and financial management for fleet owners, station owners, and system administrators.

**User Types:**
- **Super Admin**: Platform-wide management and analytics
- **Fleet Owner**: Fleet and fuel consumption management
- **Station Owner**: Station operations and invoicing

**Key Features:**
- Real-time fuel consumption monitoring
- Automated invoicing and payment processing
- Multi-branch management
- Advanced analytics and reporting
- NFC card integration for secure transactions
- Multi-language support with Hijri calendar integration

[📖 Read Full Documentation →](./fuel%20app%20docs/README.md)

---

### Document Warehouse

**Location:** [`document warehouse docs/`](./document%20warehouse%20docs/)

A comprehensive document management system (DMS) for managing physical document storage, lending operations, disposal workflows, and administrative tasks.

**Key Features:**
- Hierarchical storage location tracking (Hall → Cabinet → Column → Shelf → Box → Envelope)
- Document explorer with tree structure navigation
- Barcode generation and tracking
- Lending management with approval workflows
- Disposal request management
- Multi-language support (English/Arabic with RTL)
- Hijri calendar support

**Tech Stack:** React 19, TypeScript 5.7, Vite 6, Material-UI 6, jsPDF, Tesseract.js (OCR)

[📖 Read Full Documentation →](./document%20warehouse%20docs/README.md)

---

### Fixed Asset Management

**Location:** [`fixed asset management docs/`](./fixed%20asset%20management%20docs/)

A comprehensive web application for managing fixed assets within an organization, providing complete tracking from acquisition to disposal.

**Key Features:**
- Dashboard analytics with visual charts
- Complete asset lifecycle management
- 5-level location hierarchy (Country → City → Branch → Location → Sub Location)
- 4-level category hierarchy
- Advanced reporting with multi-criteria filtering
- Department and user management
- Multi-language and multi-calendar support (Gregorian/Hijri)

**Tech Stack:** React 18, TypeScript 4.9, Material-UI 5, jsPDF, xlsx

[📖 Read Full Documentation →](./fixed%20asset%20management%20docs/README.md)

---

### DocLink

**Location:** [`doclink docs/`](./doclink%20docs/)

DocLink consists of two main components:

#### DocLink CMS
**Location:** [`doclink docs/doclink cms docs/`](./doclink%20docs/doclink%20cms%20docs/)

Content Management System for DocLink platform.

**Documentation Contents:**
- [Architecture](./doclink%20docs/doclink%20cms%20docs/docs/ARCHITECTURE.md)
- [Development Guide](./doclink%20docs/doclink%20cms%20docs/docs/DEVELOPMENT.md)
- [User Guide](./doclink%20docs/doclink%20cms%20docs/docs/USER_GUIDE.md)
- [Deployment](./doclink%20docs/doclink%20cms%20docs/docs/DEPLOYMENT.md)
- [API Documentation](./doclink%20docs/doclink%20cms%20docs/docs/API.md)
- [Features](./doclink%20docs/doclink%20cms%20docs/docs/FEATURES.md)
- [Troubleshooting](./doclink%20docs/doclink%20cms%20docs/docs/TROUBLESHOOTING.md)
- [Security](./doclink%20docs/doclink%20cms%20docs/docs/SECURITY.md)

[📖 Read CMS Documentation →](./doclink%20docs/doclink%20cms%20docs/README.md)

#### DocLink Website
**Location:** [`doclink docs/doclink website docs/`](./doclink%20docs/doclink%20website%20docs/)

Public-facing website for DocLink platform.

[📖 Read Website Documentation →](./doclink%20docs/doclink%20website%20docs/README.md)

---

### Siraj

**Location:** [`siraj docs/`](./siraj%20docs/)

Siraj consists of two main components:

#### Siraj Admin Panel
**Location:** [`siraj docs/siraj_admin_panel_docs/`](./siraj%20docs/siraj_admin_panel_docs/)

Administrative interface for managing the Siraj platform.

[📖 Read Admin Panel Documentation →](./siraj%20docs/siraj_admin_panel_docs/)

#### Siraj Website
**Location:** [`siraj docs/siraj_website_docs/`](./siraj%20docs/siraj_website_docs/)

Public-facing website for the Siraj platform.

[📖 Read Website Documentation →](./siraj%20docs/siraj_website_docs/)

---

## Repository Structure

```
projects-documentation/
├── README.md                           # This file - main documentation index
├── beezi docs/                         # Beezi CRM documentation
├── units_documentation/                # Units WMS documentation
├── hexmate docs/                       # HexMate enterprise platform documentation
├── fuel app docs/                      # FuelApp documentation
├── document warehouse docs/            # Document Warehouse DMS documentation
├── fixed asset management docs/        # Fixed Asset Management documentation
├── doclink docs/                       # DocLink platform documentation
│   ├── doclink cms docs/              # DocLink CMS documentation
│   └── doclink website docs/          # DocLink website documentation
└── siraj docs/                         # Siraj platform documentation
    ├── siraj_admin_panel_docs/        # Siraj admin panel documentation
    └── siraj_website_docs/            # Siraj website documentation
```

## How to Use This Repository

### For Project Managers & Stakeholders
- Start with this README to get an overview of all projects
- Navigate to specific project documentation for detailed information
- Review feature lists to understand capabilities

### For Developers
- Navigate to the specific project documentation folder
- Review architecture and API documentation
- Check development and deployment guides
- Follow setup instructions in individual project READMEs

### For End Users
- Check user guides and feature documentation for your specific application
- Review troubleshooting guides for common issues
- Refer to FAQ sections for quick answers

### For System Administrators
- Review configuration and deployment documentation
- Check security guidelines
- Follow installation and setup instructions

## Contributing

When adding or updating documentation:

1. **Maintain Structure**: Keep the existing folder structure and naming conventions
2. **Update Main README**: If adding a new project, update this main README
3. **Use Markdown**: All documentation should be in Markdown format
4. **Include Examples**: Provide code examples and screenshots where appropriate
5. **Keep Updated**: Ensure documentation reflects the current state of applications
6. **Cross-Reference**: Link between related documentation when relevant

## Support

For questions, issues, or contributions related to documentation:

1. Check the specific project's documentation first
2. Review troubleshooting guides
3. Contact the respective project maintainers
4. For documentation issues, open an issue in this repository

---

**Last Updated:** December 2025  
**Maintained by:** FediTech Development Team

