# FuelApp - Comprehensive Product Documentation

## Table of Contents
- [Overview](#overview)
- [Getting Started](#getting-started)
- [Login Credentials](#login-credentials)
- [User Types](#user-types)
- [Features by User Type](#features-by-user-type)
  - [Super Admin](#super-admin)
  - [Fleet Owner](#fleet-owner)
  - [Station Owner](#station-owner)
- [Common Features](#common-features)
- [Support](#support)

---

## Overview

FuelApp is a comprehensive fuel management system designed to streamline fleet operations, fuel consumption tracking, and financial management for fleet owners, station owners, and system administrators. The platform provides real-time analytics, subscription management, and detailed reporting capabilities.

**Key Benefits:**
- Real-time fuel consumption monitoring
- Automated invoicing and payment processing
- Multi-branch management capabilities
- Advanced analytics and reporting
- Role-based access control
- NFC card integration for secure transactions

---

## Getting Started

### Accessing the Application

1. Navigate to the FuelApp login page
2. Enter your username/email and password
3. Complete the reCAPTCHA verification (if prompted)
4. Click the "Login" button

![Login Page](https://github.com/user-attachments/assets/67e7e0d5-3e11-43ff-b562-12cd52f8362a)

### Login Credentials

For testing and demonstration purposes, use the following credentials:

| User Type | Username/Email | Password |
|-----------|---------------|----------|
| Super Admin | `superadmin` | `1234` |
| Fleet Owner | `fleetowner` | `1234` |
| Station Owner | `stationowner` | `1234` |

> **Note:** These are test credentials. In production, users should create secure passwords and enable two-factor authentication.

---

## User Types

FuelApp supports three distinct user types, each with specific roles and permissions:

### 1. Super Admin
System administrators with full access to manage the entire platform, including users, finance, marketing, and system settings.

### 2. Fleet Owner
Business owners managing their fleet of vehicles, delegates, fuel consumption, and subscription plans.

### 3. Station Owner
Fuel station operators managing branches, employees, invoices, and fuel pricing.

---

## Features by User Type

## Super Admin

![Super Admin Dashboard](https://github.com/user-attachments/assets/6f6fd162-ce3b-4975-beda-0cf15fe4ea46)

### Dashboard
The Super Admin dashboard provides a comprehensive overview of platform activity:
- **Orders Overview**: Daily, weekly, and monthly order statistics with trend indicators
- **Active Users**: Total active user count and unique user metrics
- **Total Revenue**: Revenue tracking with comparison to previous periods
- **Top Stations**: Visual breakdown of top-performing fuel stations by order volume
- **Top Cities**: Geographic distribution of orders and consumption

### User Management

#### Customers
- View all registered customers
- Add new customers
- Edit customer details
- View detailed customer profiles
- Track customer order history

#### Service Providers
- Manage fuel station service providers
- Add new providers
- Update provider information
- Monitor provider performance

#### Admins
- Create and manage admin accounts
- Assign admin roles and permissions
- Monitor admin activity logs

### Station Map
- Interactive map showing all fuel stations
- Real-time station status
- Geographic distribution analysis
- Quick access to station details

### Finance Management

#### Overview
- Financial dashboard with key metrics
- Revenue trends and forecasts
- Payment status monitoring
- Balance summaries

#### Settlements
- Process financial settlements
- Track settlement history
- Manage payment schedules
- Generate settlement reports

#### Invoices
- Create and manage invoices
- Track invoice status (pending, paid, overdue)
- Automated invoice generation
- Invoice history and archives

### System Settings
- Configure platform-wide settings
- Manage system parameters
- Update application configurations
- Define business rules

### Two-Factor Authentication (2FA)
- Enable/disable 2FA for enhanced security
- Configure authentication methods
- Manage 2FA settings for all users

### Marketing

#### Promotions
- Create promotional campaigns
- Set discount rules and conditions
- Schedule promotion periods
- Track promotion effectiveness
- Manage promotion codes

### Analytics
- Comprehensive reporting dashboard
- Custom report generation
- Data export capabilities
- Visual analytics and charts
- Performance metrics

---

## Fleet Owner

![Fleet Owner Dashboard](https://github.com/user-attachments/assets/16f95b55-3f29-4c5b-9c82-3dc3f2bd5ed5)

### Dashboard
The Fleet Owner dashboard focuses on fleet operations and financial management:

#### Financial Balances
- **Company Main Balance**: Current available balance for fuel purchases
- **Company Overall Balance**: Total balance including all fuel types

#### Main Subscription
- Subscription tier information (Bronze, Silver, Gold)
- Subscription expiry date
- Price per vehicle
- Number of vehicles purchased
- Usage tracking (vehicles used vs. purchased)
- Quick access to update or renew subscription

#### Balance Breakdown
- **Fuel Type 91 Balance**: Available balance and free balance
- **Fuel Type 95 Balance**: Available balance and free balance
- **Fuel Type 98 Balance**: Available balance and free balance

#### Consumption Analytics
- **Monthly Fuel Consumption**: Visual chart showing fuel usage trends
- **Fuel Consumption by Type**: Pie chart breakdown by fuel grade
- **Total Consumption Rate**: Comparison with effective rate
- **Top 10 Consuming Vehicles**: List of highest fuel consumers

#### Additional Insights
- Fuel types breakdown
- Transaction breakdown (fuel purchases vs. recharges)
- Vehicle status (activated vs. suspended)

### Payments & Subscription

#### Wallet
- View current balance
- Recharge account
- Transaction history
- Payment methods management

#### Ledger
- Detailed transaction logs
- Account statement downloads
- Balance history
- Financial reports

#### Subscription & NFC Cards
- Manage subscription plans
- Order NFC cards for vehicles
- Track card activation status
- Update vehicle assignments

#### SMS Packages
- Purchase SMS notification packages
- Track SMS usage
- Configure notification preferences

### Branches Management

#### Branches List
- View all company branches
- Add new branches
- Edit branch details
- Assign branch managers
- Set branch-specific settings

#### Balance Transfers
- Transfer funds between branches
- Track transfer history
- Approve/reject transfer requests
- Monitor inter-branch transactions

### Blocked Stations
- Block specific fuel stations
- Manage blocked station list
- Set blocking reasons and notes
- Unblock stations as needed

### Users Management
- Add company users
- Assign roles and permissions
- Manage user access levels
- Track user activity

### Vehicles & Delegates

#### Vehicles
- Register fleet vehicles
- Assign NFC cards to vehicles
- Set vehicle fuel limits
- Track vehicle consumption
- Suspend/activate vehicles
- Vehicle maintenance records

#### Delegates
- Register authorized drivers
- Assign vehicles to delegates
- Set delegation periods
- Track delegate fuel usage
- Manage delegate permissions

### Fuel Reports

#### Fuel Consumption Report
- Detailed fuel usage by vehicle
- Date range filtering
- Export to Excel/PDF
- Visual consumption trends

#### Monthly Consumption Report
- Month-by-month comparison
- Fuel type breakdown
- Cost analysis
- Budget tracking

#### Delegates Consumption Report
- Individual delegate fuel usage
- Performance metrics
- Consumption patterns
- Anomaly detection

#### Filling Frequency Report
- Refueling patterns
- Station preferences
- Time-based analysis
- Frequency trends

#### NFC Operation Log Report
- Card usage history
- Transaction logs
- Security events
- Unauthorized access attempts

#### Consumption by Branch Report
- Branch-wise fuel consumption
- Inter-branch comparison
- Branch performance metrics
- Cost allocation

### Profile System Settings
- Update company profile
- Configure notification preferences
- Set default branch
- Language and calendar settings

### Help & Support
- WhatsApp support integration
- Direct contact with support team
- Help documentation
- FAQs and guides

---

## Station Owner

![Station Owner Dashboard](https://github.com/user-attachments/assets/3f0f7da1-237c-45e4-bc2e-a146f5d358bb)

### Dashboard
The Station Owner dashboard provides operational insights:

#### Key Metrics
- **Pending Invoices**: Count of invoices awaiting approval
- **Rejected Invoices**: Number of rejected invoices requiring attention
- **Number of Active Workers**: Currently active employees
- **Number of Inactive Workers**: Inactive employee count

#### Analytics
- **Monthly Fuel Consumption**: Bar chart showing consumption by fuel type (91, 95, Diesel) across months
- **Annual Fuel Consumption**: Pie chart showing fuel distribution by type for the year

### Branches Management
- Manage multiple station locations
- Add new branches
- Update branch information
- Assign employees to branches
- Track branch performance

### Employees

#### Employee List
- View all station employees
- Add new employees
- Edit employee details
- Set employee roles (cashier, manager, etc.)
- Manage employee schedules

#### Employee Management
- Track employee attendance
- Monitor employee performance
- Set access permissions
- Manage employee credentials

### Fuel Price Change Requests
- Submit fuel price change requests
- Track request status (pending, approved, rejected)
- View price change history
- Set effective dates for price changes
- Attach supporting documentation

### Account Statements
- View detailed account statements
- Filter by date range
- Track payments and receivables
- Download statements
- View transaction details

### E-Invoices
- Electronic invoice management
- Generate ZATCA-compliant invoices
- Track invoice delivery status
- Invoice validation and verification
- Archive invoices

### Tax Invoice Report
- Generate tax-compliant reports
- VAT calculations
- Tax period summaries
- Export for accounting systems
- Regulatory compliance tracking

### Sales

#### Invoices
- View all sales invoices
- Create new invoices
- Edit draft invoices
- Track invoice lifecycle
- Invoice details and history

#### Pending Invoices
- Invoices awaiting customer approval
- Follow-up management
- Payment reminders
- Pending invoice aging

#### Rejected Invoices
- View rejected invoices with reasons
- Resubmit corrected invoices
- Dispute management
- Resolution tracking

### Approved Invoices
- Successfully approved invoices
- Payment tracking
- Revenue recognition
- Archive approved invoices

### Marketing Commission Invoice
- Track marketing-related commissions
- Generate commission invoices
- Payment processing
- Commission rate management

---

## Common Features

### Navigation
All user types have access to:
- **Sidebar Menu**: Quick access to main features
- **Header Controls**: 
  - Language selector (English/Arabic)
  - Calendar type toggle (Gregorian/Hijri)
  - Account settings
  - Notifications
  - Profile menu

### Language Support
- **English**: Default language
- **Arabic**: Full RTL support
- **Calendar Options**:
  - Gregorian calendar
  - Hijri (Islamic) calendar

### Date Range Filtering
Most reports and dashboards support:
- Custom date range selection
- Quick filters (Today, Last 7 days, Last 30 days, etc.)
- Calendar-specific date pickers

### Data Export
Export data in multiple formats:
- **Excel**: For detailed data analysis
- **PDF**: For printing and sharing
- **CSV**: For data integration

### Responsive Design
- **Desktop**: Full-featured interface
- **Tablet**: Optimized layout
- **Mobile**: Touch-friendly interface

### Security Features
- Role-based access control (RBAC)
- Two-factor authentication (2FA)
- Session timeout
- Secure password requirements
- Activity logging and audit trails

---

## Support

### Getting Help

#### For Fleet Owners
- Access Help & Support via WhatsApp integration
- Contact: [To be configured by system administrator]
- Submit support tickets
- Access knowledge base

#### For Station Owners
- Submit fuel price change requests
- Contact system administrator
- Access documentation
- Report technical issues

#### For System Administrators
- Full system access for troubleshooting
- User management capabilities
- System configuration tools
- Analytics and monitoring

### Best Practices

#### For Fleet Owners
1. **Regular Monitoring**: Check dashboard daily for consumption anomalies
2. **Budget Management**: Set vehicle fuel limits to control costs
3. **NFC Security**: Regularly review NFC operation logs
4. **Reports**: Generate monthly reports for financial planning
5. **Subscription**: Monitor usage to optimize subscription tier

#### For Station Owners
1. **Price Updates**: Submit price changes in advance
2. **Invoice Management**: Process invoices promptly to maintain cash flow
3. **Employee Tracking**: Monitor employee activity for security
4. **Compliance**: Keep tax invoices up to date

#### For System Administrators
1. **User Management**: Regular user access reviews
2. **System Monitoring**: Track platform performance metrics
3. **Financial Oversight**: Monitor settlements and payments
4. **Security**: Enable 2FA for all admin accounts

---

## Technical Information

### System Requirements
- **Browser**: Modern web browser (Chrome, Firefox, Safari, Edge)
- **Internet**: Stable internet connection
- **Resolution**: Minimum 1024x768 (1920x1080 recommended)

### Data Retention
- Transaction data: 7 years
- Reports: Available for download at any time
- Invoices: Permanent retention for tax compliance

### Maintenance
- Regular updates deployed during off-peak hours
- Scheduled maintenance notifications sent in advance
- 24/7 system availability (99.9% uptime SLA)

---

## Glossary

- **NFC**: Near Field Communication - Technology used for secure vehicle identification
- **Delegate**: Authorized driver assigned to company vehicles
- **Settlement**: Financial reconciliation between parties
- **ZATCA**: Zakat, Tax and Customs Authority (Saudi Arabia)
- **2FA**: Two-Factor Authentication
- **RBAC**: Role-Based Access Control

---

## Version History

- **v1.0.0**: Initial documentation release
- Date: December 2025

---

**Developed by CompassDX**

© 2025 FuelApp. All rights reserved.
