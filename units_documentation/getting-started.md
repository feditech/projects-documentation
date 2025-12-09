# Getting Started

This guide will help you set up and start using the Units warehouse management system.

## Prerequisites

Before you begin, ensure you have:

- A modern web browser (latest version of Chrome, Firefox, Safari, or Edge)
- Internet connection
- Login credentials provided by your system administrator

## Installation for Developers

If you're setting up the application for development:

### System Requirements

- Node.js (version 16 or higher)
- npm (Node Package Manager)
- Git

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/feditech/unitswebapp.git
   cd unitswebapp
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   
   Create a `.env` file in the root directory with the following:
   ```
   REACT_APP_BASE_API=https://your-api-endpoint.com/api/
   REACT_APP_GOOGLE_MAPS_API_KEY=your-google-maps-api-key
   ```

4. **Start the development server**
   ```bash
   npm start
   ```
   
   The application will open at [http://localhost:3000](http://localhost:3000)

5. **Build for production**
   ```bash
   npm run build
   ```
   
   This creates an optimized production build in the `build` folder.

## First Time Login

### Accessing the System

1. Open your web browser and navigate to the Units application URL
2. You'll see the login page with the Units logo

### Logging In

1. **Enter your credentials**
   - Email address
   - Password (must meet the following requirements):
     - At least 8 characters long
     - Contains at least one uppercase letter
     - Contains at least one lowercase letter
     - Contains at least one number
     - Contains at least one special character

2. **Remember Me option**
   - Check this box if you want the system to remember your login on this device
   - Recommended only for personal devices

3. **Click "Sign In"**

### After Login

Upon successful login, you'll be directed to:
- **Dashboard** - Your main landing page with key metrics and recent activities
- The interface will be customized based on your user role (Admin or Customer)

## Navigating the Interface

### Main Components

1. **Top Navigation Bar**
   - Application logo and branding
   - User profile menu
   - Language selector (English/Arabic)
   - Notifications
   - Logout option

2. **Side Navigation Menu** (for admin users)
   - Dashboard
   - Leads & Quotations
   - Inbound Requests
   - Orders (Outbound Requests)
   - Inventory (SKU Management)
   - Reports
   - Settings

3. **Main Content Area**
   - List views with filtering and search
   - Detail forms and data entry
   - Charts and reports
   - Action buttons and contextual menus

### Language Selection

Units supports both English and Arabic:

1. Click the language selector in the top navigation
2. Choose your preferred language
3. The entire interface will switch to the selected language
4. Your preference is saved for future sessions

## Key Concepts

Before diving into daily operations, familiarize yourself with these core concepts:

### Warehouse Hierarchy

```
Warehouse
  └── Area
      └── Rack
          └── Location (Bin)
```

- **Warehouse**: Top-level storage facility
- **Area**: Section within a warehouse (e.g., Zone A, Zone B)
- **Rack**: Storage rack within an area
- **Location**: Specific bin or slot on a rack

### SKU (Stock Keeping Unit)

- Unique identifier for each product
- Contains product details, dimensions, weight
- Used to track inventory across the system

### Inbound Process Flow

```
Request → Goods Receipt → Counting → QC → Putaway → Completed
```

### Outbound Process Flow

```
Order → Picking → QC → Packing → Dispatch → Completed
```

## Common First Steps

### For Administrators

1. **Set up warehouse structure**
   - Go to Settings → Warehouses
   - Create warehouses, areas, racks, and locations

2. **Configure master data**
   - Add carriers, packing materials, and order bins
   - Set up time slots for receiving/shipping

3. **Create users**
   - Go to Settings → Users
   - Invite users and assign roles

4. **Add customers**
   - Go to Settings → Customers
   - Create customer accounts

### For Customers

1. **Review your dashboard**
   - Check current inventory levels
   - View recent order activity

2. **Browse your SKU catalog**
   - Go to SKU menu
   - Review your products and stock levels

3. **Create an outbound request**
   - Navigate to Orders
   - Click "Add Order"
   - Select products and quantities

### For Warehouse Operators

1. **Check today's tasks**
   - Dashboard shows pending inbound/outbound requests
   - Review assignments

2. **Process inbound receipts**
   - Go to Inbound Requests
   - Select items in "Goods Received" tab
   - Complete counting and QC

3. **Fulfill orders**
   - Go to Orders
   - Pick assigned orders
   - Complete packing and dispatch

## Getting Help

- **In-app help**: Look for the (?) icon throughout the interface
- **Documentation**: Refer to this documentation for detailed guides
- **Support**: Contact your system administrator for assistance
- **Training**: Request training sessions for your team

## Security Best Practices

1. **Password Management**
   - Use a strong, unique password
   - Don't share your credentials
   - Change password regularly

2. **Session Security**
   - Always log out when finished
   - Don't leave your session unattended
   - Use "Remember Me" only on trusted devices

3. **Data Entry**
   - Double-check important data before saving
   - Review quantities and addresses carefully
   - Use the system's validation features

## Next Steps

- Learn about specific features in the [Features](./features.md) guide
- Understand operational workflows in the [Workflows](./workflows.md) guide
- Review your role's capabilities in the [User Roles](./user-roles.md) guide

## Troubleshooting Login Issues

If you can't log in:

1. **Verify your credentials** - Check for typos in email/password
2. **Reset password** - Click "Forgot Password?" on the login page
3. **Check email confirmation** - Ensure your email is verified
4. **Browser issues** - Clear cache or try a different browser
5. **Contact support** - Reach out to your administrator if issues persist

See the [Troubleshooting](./troubleshooting.md) guide for more help.
