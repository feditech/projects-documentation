# User Roles and Permissions

This guide explains the different user types in the Units system and their associated permissions.

## User Types Overview

Units supports three primary user types, each with distinct access levels and capabilities:

1. **Admin Users** - Full system access and configuration
2. **Customer Users** - Access to their own inventory and orders
3. **Warehouse Operators** - Operational tasks (implicit through admin permissions)

## 1. Admin Users

### Overview
Admin users have complete access to the system and are typically warehouse managers, system administrators, or operations staff.

### Access Level
- Full read/write access to all modules
- System configuration and setup
- User management capabilities
- Multi-customer visibility
- Advanced reporting and analytics

### Key Capabilities

#### Dashboard Access
- View system-wide metrics
- Annual utilization charts
- All customer activities
- System health indicators
- Warehouse capacity planning

#### Lead Management
- Create and manage leads
- Generate quotations
- Track sales pipeline
- Convert leads to customers
- View all lead activities

#### Quotation Management
- Create detailed quotations
- Edit pricing and terms
- Send quotations to prospects
- Track quotation status
- Approve/reject quotations

#### Inbound Operations
- View all inbound requests (all customers)
- Create inbound requests on behalf of customers
- Manage goods receiving process
- Oversee counting and QC
- Assign putaway tasks
- View completed inbound history

#### Outbound Operations
- View all orders (all customers)
- Create orders on behalf of customers
- Assign pickers to orders
- Monitor picking progress
- Oversee packing and dispatch
- Handle exceptions (holds, cancellations, returns)
- Manage self-collection orders

#### Inventory Management
- View all SKUs across all customers
- Create and edit SKUs
- Manage SKU categories
- Create and manage SKU kits
- Perform inventory adjustments
- Conduct cycle counts
- View real-time inventory levels
- Manage stock locations

#### Customer Management
- Create and edit customer accounts
- Manage customer addresses
- View customer activity
- Set customer preferences
- Manage customer users
- View customer-specific pricing

#### Warehouse Configuration
- Create and manage warehouses
- Configure warehouse hierarchy (areas, racks, locations)
- Set up location barcodes
- Manage warehouse capacity
- Configure time slots for receiving/shipping

#### User Management
- Create new users (admin and customer)
- Edit user details
- Activate/deactivate users
- Assign roles and permissions
- Reset user passwords
- View user activity logs

#### Master Data Management
- **Suppliers**: Add/edit supplier information
- **Brands**: Manage brand registry
- **Carriers**: Configure shipping carriers
- **Packing Materials**: Manage packaging inventory
- **Order Bins**: Set up sortation bins
- **Time Slots**: Configure appointment windows
- **Packages**: Define standard package sizes

#### Reporting
- Access all report types
- **Inbound Report**: Receiving metrics and supplier performance
- **Order Report**: Fulfillment statistics and carrier performance
- **SKU Report**: Inventory valuation (all customers)
- **Stock Movement Report**: Detailed transaction history
- Generate custom date ranges
- Export reports in multiple formats
- Schedule automated reports

#### System Settings
- **Tenants**: Multi-tenant configuration (if applicable)
- **Customizations**: Theme and branding settings
- Configure system preferences
- Manage integration settings

### Typical Admin User Profiles

#### Warehouse Manager
- Oversees daily operations
- Manages warehouse staff
- Monitors KPIs
- Handles customer escalations
- Plans capacity and resources

#### Operations Supervisor
- Assigns tasks to warehouse operators
- Monitors workflow progress
- Ensures quality standards
- Manages exceptions
- Trains new staff

#### System Administrator
- User account management
- System configuration
- Technical troubleshooting
- Integration management
- Data backup and security

#### Account Manager
- Lead and customer relationship management
- Quotation generation
- Contract negotiation
- Customer onboarding
- Revenue management

## 2. Customer Users

### Overview
Customer users represent the warehouse clients who store inventory and create orders. They have access only to their own data.

### Access Level
- Read/write access to their own inventory
- Create and manage their orders
- View their reports
- Limited to their own data
- No system configuration access

### Key Capabilities

#### Dashboard Access
- View their inventory summary
- See their active orders
- Track recent inbound receipts
- View their analytics and KPIs
- Quick links to common tasks

#### Lead Management
- **No Access** - Customers don't manage leads

#### Quotation Management
- **Read Only** - View quotations sent to them
- Accept/reject quotations via external link
- Cannot create quotations

#### Inbound Operations
- Create inbound requests
- View their inbound requests only
- Track inbound request status
- Upload supporting documents
- View completed inbound history
- **Cannot** perform GRN, counting, QC, or putaway (warehouse operations)

#### Outbound Operations
- Create orders for their inventory
- View their orders only
- Track order status
- View order history
- Request order cancellations (admin approval may be required)
- Schedule self-collection
- **Cannot** perform picking, packing, or dispatch (warehouse operations)

#### Inventory Management
- View their SKUs only
- Create and edit their SKUs
- View real-time stock levels
- View stock locations
- Request inventory adjustments (admin performs actual adjustment)
- Manage SKU categories
- Create SKU kits
- **Cannot** perform physical stock movements

#### Customer Profile
- Edit their company information
- Manage delivery addresses
- View their contract/pricing
- Update contact details
- Manage their team members (customer users under same account)

#### Address Management
- Add/edit delivery addresses
- Set default addresses
- View address history

#### Reporting
- **SKU Report**: Their inventory valuation
- **Stock Movement Report**: Their stock transaction history
- View order fulfillment metrics
- Export their reports
- **Cannot** access other customers' data
- **Cannot** access system-wide reports

### Typical Customer User Profiles

#### E-commerce Business Owner
- Creates outbound orders from online sales
- Monitors inventory levels
- Tracks order fulfillment
- Reviews stock reports

#### Retail Manager
- Manages product catalog (SKUs)
- Creates replenishment orders
- Plans inventory distribution
- Analyzes stock performance

#### Supply Chain Coordinator
- Creates inbound requests for new stock
- Tracks shipments
- Manages delivery schedules
- Coordinates with suppliers

## 3. Permission Matrix

| Feature | Admin | Customer |
|---------|-------|----------|
| **Dashboard** | All data | Own data only |
| **Leads** | Full access | No access |
| **Quotations** | Create/Edit | View only |
| **Inbound Requests** | All customers | Own requests |
| **Inbound Operations** | Perform tasks | View status |
| **Orders** | All customers | Own orders |
| **Order Operations** | Perform tasks | View status |
| **SKU Management** | All SKUs | Own SKUs |
| **Inventory Adjustments** | Perform | Request |
| **Customer Management** | All customers | Own profile |
| **User Management** | All users | Own team |
| **Warehouse Config** | Full access | No access |
| **Suppliers** | Full access | View (their suppliers) |
| **Brands** | Full access | View |
| **Carriers** | Full access | View |
| **Packing Materials** | Full access | No access |
| **Reports - Admin** | Full access | No access |
| **Reports - Customer** | All customers | Own data |
| **System Settings** | Full access | No access |

## 4. Role-Based Features

### Admin-Only Features
- Lead and quotation management
- Physical warehouse operations (receiving, picking, packing)
- User management (all users)
- Warehouse configuration
- Master data management (suppliers, carriers, etc.)
- System settings and customization
- Multi-customer visibility
- Tenant management

### Customer-Only Features
- Self-service order creation
- Real-time inventory visibility (own stock)
- Delivery address management
- Customer-specific reporting

### Shared Features
Both admin and customer users can:
- View dashboard (filtered by access)
- Create inbound requests
- Create outbound orders
- Manage SKUs (within their scope)
- View reports (within their scope)
- Upload documents

## 5. User Management Workflows

### Creating Admin Users
**Who can do this**: Existing admin users

1. Navigate to **Settings → Users**
2. Click **Add User**
3. Select **User Type**: Admin
4. Enter user details
5. Assign permissions (typically full admin)
6. Send invitation
7. User sets password on first login

### Creating Customer Users
**Who can do this**: Admin users

1. Navigate to **Settings → Users**
2. Click **Add User**
3. Select **User Type**: Customer
4. **Select Customer**: Choose which customer account
5. Enter user details
6. Set permissions (typically standard customer access)
7. Send invitation
8. User sets password on first login

### Customer Self-Management
Customer admin users (designated by admin) may:
- Invite additional users to their account
- Deactivate users on their account
- Edit user details for their team
- Cannot create users for other customers

## 6. Security Considerations

### Password Requirements
All users must have passwords that meet these criteria:
- Minimum 8 characters
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- At least one special character

### Access Control
- Users can only access data within their permission scope
- Customer users cannot view other customers' data
- Session timeout after inactivity
- Activity logging for audit trails

### Data Isolation
- Customer data is logically separated
- Each customer can only see their own:
  - Inventory (SKUs and stock levels)
  - Orders (inbound and outbound)
  - Reports and analytics
  - User accounts

### Best Practices
1. **Principle of Least Privilege**: Grant minimum necessary access
2. **Regular Access Reviews**: Periodically review user permissions
3. **Immediate Deactivation**: Disable accounts for departed staff
4. **Unique Accounts**: No shared login credentials
5. **Strong Passwords**: Enforce password complexity
6. **Activity Monitoring**: Review user activity logs

## 7. User Scenarios

### Scenario 1: New Customer Onboarding
1. Admin creates customer account
2. Admin creates first customer user (customer admin)
3. Customer admin logs in
4. Customer admin invites their team members
5. Team members can now manage inventory and orders

### Scenario 2: Warehouse Operator
1. Admin creates admin user for warehouse operator
2. Operator logs in with full admin access
3. Operator can perform receiving, picking, packing
4. Operator cannot modify system configuration

### Scenario 3: Customer Account Manager
1. Admin creates customer user
2. User is designated as "customer admin" for their account
3. Can manage their team's users
4. Can oversee all activity for their account
5. Still cannot see other customers' data

## Next Steps

- Understand operational workflows in [Workflows](./workflows.md)
- Review all system features in [Features](./features.md)
- Configure user accounts in [Configuration](./configuration.md)
