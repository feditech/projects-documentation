# Features

This comprehensive guide covers all features available in the Units warehouse management system.

## 1. Dashboard

### Overview
The dashboard provides a centralized view of key metrics and recent activities.

### Admin Dashboard
- **Utilization Box**: Warehouse space utilization metrics
- **Annual Utilization**: Yearly trends and capacity planning
- **Recent Activities**: Latest system events and updates
- **Quick Actions**: Fast access to common tasks
- **Alerts and Notifications**: Important system messages

### Customer Dashboard
- **Inventory Summary**: Current stock levels across all SKUs
- **Order Status**: Active orders and their fulfillment status
- **Recent Inbound**: Latest goods received
- **Analytics**: Key performance indicators
- **Quick Links**: Navigate to frequently used functions

## 2. Lead Management

### Purpose
Track potential customers and manage quotation requests before they become active customers.

### Features
- Create and manage leads
- Track lead source and status
- Convert leads to customers
- Lead pipeline visualization
- Activity history and notes

### Workflow
1. Capture lead information (contact details, requirements)
2. Create and send quotations
3. Track quotation acceptance
4. Convert to customer upon acceptance

## 3. Quotations

### Overview
Generate and manage pricing quotations for warehouse services.

### Capabilities
- Create detailed quotations with itemized pricing
- Support for different service types:
  - Storage fees (monthly, annually)
  - Handling charges
  - Value-added services
- Version control for quotation revisions
- PDF generation for quotation documents
- Quotation approval workflow
- Terms and conditions inclusion

### Quotation Process
1. Create quotation from lead or customer request
2. Add line items with pricing
3. Include terms and conditions
4. Send to customer for review
5. Track acceptance/rejection
6. Convert accepted quotations to contracts

## 4. Inbound Management

### Overview
Manage the complete lifecycle of goods entering the warehouse.

### Inbound Request Stages

#### 4.1 Requests
- Create new inbound requests
- Specify expected items and quantities
- Set delivery dates and time slots
- Assign supplier information
- Generate advance shipping notices (ASN)

#### 4.2 Goods Receiving (GRN)
- Record actual receipt of goods
- Capture delivery vehicle details
- Photograph shipment condition
- Record receipt timestamp
- Match against expected quantities
- Note any discrepancies

#### 4.3 Counting
- Physical count verification
- Item-by-item quantity confirmation
- Variance reporting
- Batch/lot number recording
- Serial number capture (if applicable)

#### 4.4 Quality Control (QC)
- Visual inspection
- Quality parameters verification
- Damage assessment
- Accept/reject decisions
- QC notes and photo documentation
- Sampling procedures

#### 4.5 Putaway
- Automated location suggestions
- Location scanning/confirmation
- Bulk putaway operations
- Putaway task assignment
- Completion verification

#### 4.6 Completed
- Archived completed inbound requests
- Full audit trail
- Historical reference
- Performance metrics

### Features
- **Time Slot Management**: Schedule receiving times
- **Multi-item Support**: Handle multiple SKUs per request
- **Document Upload**: Attach invoices and packing lists
- **Status Tracking**: Real-time progress monitoring
- **Mobile-friendly**: Optimized for warehouse scanners/tablets

## 5. Outbound Management (Orders)

### Overview
Complete order fulfillment from order creation to dispatch.

### Order Stages

#### 5.1 All Requests
- View all orders regardless of status
- Filter by date, customer, or status
- Bulk operations support
- Export order lists

#### 5.2 Unassigned Picker
- Orders pending picker assignment
- Automatic or manual assignment
- Workload balancing

#### 5.3 Assigned Picker
- Orders assigned to specific pickers
- View picker workload
- Reassignment capabilities

#### 5.4 Picked
- Orders with picking completed
- Ready for QC and packing
- Picking accuracy metrics

#### 5.5 Packed
- Orders packed and labeled
- Weight and dimension capture
- Shipping label generation
- Ready for dispatch

#### 5.6 Dispatched
- Orders handed to carrier
- Tracking number assignment
- Delivery date estimation
- Customer notification

#### 5.7 Completed
- Successfully delivered orders
- Proof of delivery capture
- Customer confirmation

#### 5.8 On Hold
- Orders temporarily paused
- Reason tracking
- Resume capabilities

#### 5.9 Cancelled
- Cancelled orders with reasons
- Inventory release
- Audit trail

#### 5.10 Returned
- Orders returned by customer
- Return reason capture
- Re-stocking process
- Refund/replacement tracking

#### 5.11 Self Collection
- Customer pickup orders
- Collection slot scheduling
- ID verification
- Collection confirmation

### Outbound Features
- **Wave Picking**: Group orders for efficient picking
- **Pick List Generation**: Optimized pick paths
- **Barcode Scanning**: Verify items during picking
- **QC Checks**: Quality verification before packing
- **Multi-carrier Support**: Integration with various carriers
- **Tracking**: Real-time shipment tracking
- **Returns Processing**: Handle returns efficiently

## 6. SKU Management

### Overview
Comprehensive product catalog and inventory management.

### SKU Master Data
- SKU code (unique identifier)
- Product description
- Category and subcategory
- Brand information
- Supplier details
- Dimensions (L x W x H)
- Weight
- Unit of measure
- Images (multiple photos)
- Barcode/UPC
- Reorder points
- Safety stock levels

### SKU Categories
- Hierarchical category structure
- Custom attributes per category
- Category-based rules and workflows

### SKU Kits
- Bundle multiple SKUs into kits
- Kit assembly and disassembly
- Kit BOM (Bill of Materials)
- Kit pricing

### Inventory Functions
- **Real-time Stock Levels**: Current quantity by location
- **Stock Movements**: Track all ins and outs
- **Stock Adjustments**: Correct discrepancies
- **Cycle Counting**: Regular count schedules
- **Lot/Batch Tracking**: Trace specific batches
- **Expiry Date Management**: Track expiration dates
- **Serial Number Tracking**: Individual item tracking

## 7. Warehouse Settings

### 7.1 Warehouse Management
- Create and configure warehouses
- Define warehouse areas
- Set up rack systems
- Configure bin locations
- Capacity planning
- Warehouse mapping
- Location barcode generation

### 7.2 Users
- User account creation
- Role assignment (Admin/Customer/Operator)
- Permission management
- Active/inactive status
- User activity logging

### 7.3 Customers
- Customer profile management
- Multiple delivery addresses
- Contact information
- Customer-specific pricing
- Credit limits
- Customer portal access

### 7.4 Suppliers
- Supplier database
- Contact details
- Performance metrics
- Supplier ratings
- Preferred supplier flags

### 7.5 Brands
- Brand registry
- Brand-SKU associations
- Brand-specific handling rules

### 7.6 Carriers
- Shipping carrier setup
- API integration credentials
- Service levels (Standard, Express, etc.)
- Rate cards
- Carrier performance tracking

### 7.7 Packaging Materials
- Package types (boxes, envelopes, pallets)
- Dimensions and weight
- Material costs
- Stock management for packaging

### 7.8 Order Bins
- Sortation bin configuration
- Bin assignments for picking
- Bin location mapping

### 7.9 Time Slots
- Configure receiving windows
- Set delivery time slots
- Capacity limits per slot
- Holiday and blackout dates

### 7.10 Packages (Size Templates)
- Standard package sizes
- Dimensional rules
- Package selection logic

### 7.11 Tenants (Multi-tenancy)
- Tenant organization setup
- Tenant-specific configurations
- Custom branding per tenant
- Data isolation

### 7.12 Customizations
- Theme customization
- Logo and branding
- Color schemes
- Layout preferences

## 8. Reporting

### Admin Reports

#### 8.1 Inbound Report
- Receipts over time period
- Supplier performance
- Receiving efficiency
- Quality metrics
- Discrepancy analysis

#### 8.2 Order Report
- Order volume and trends
- Fulfillment rates
- Order cycle time
- Carrier performance
- Geographic distribution

### Customer Reports

#### 8.3 SKU Report
- Inventory valuation
- Stock aging
- Fast/slow movers
- SKU performance
- Turnover ratios

#### 8.4 Stock Movement Report
- Date range filtering
- Movement types (in/out/adjustment)
- SKU-specific movements
- Location-based analysis
- Export to Excel

### Report Features
- **Date Range Selection**: Custom time periods
- **Export Options**: PDF, Excel, CSV
- **Scheduled Reports**: Automatic generation
- **Email Distribution**: Send to stakeholders
- **Chart Visualizations**: Graphs and charts
- **Drill-down Capability**: Detail analysis

## 9. Address Management

### Customer Addresses
- Multiple addresses per customer
- Default shipping address
- Address validation
- Google Maps integration
- Delivery instructions
- Address type (warehouse, retail, home)

## 10. Integration Features

### 10.1 Salla Integration
- E-commerce platform connection
- Automatic order import
- Inventory synchronization
- Order status updates
- OAuth authentication

### 10.2 Data Import/Export
- Excel-based bulk upload
- Template downloads
- Data validation
- Error reporting
- Batch processing

### 10.3 Barcode Support
- Generate barcodes for SKUs
- Print barcode labels
- Scan during operations
- Barcode format support (Code 128, EAN, UPC)

## 11. Notifications and Alerts

### System Notifications
- Real-time alerts
- Email notifications
- In-app notification center
- Customizable alert preferences
- Priority levels

### Alert Types
- Low stock warnings
- Overdue orders
- Quality issues
- System errors
- Task assignments

## 12. Multi-language Support

### Languages
- English (default)
- Arabic (RTL support)

### Features
- Complete UI translation
- Document generation in both languages
- User preference saving
- Dynamic language switching
- Date/number formatting per locale

## 13. Mobile Optimization

### Responsive Design
- Adapts to tablet and mobile screens
- Touch-friendly controls
- Optimized for warehouse scanners
- Offline capability considerations

## 14. Security Features

### Authentication
- Secure login with password requirements
- Email verification
- Password reset functionality
- Session management
- Remember me option

### Authorization
- Role-based access control (RBAC)
- Feature-level permissions
- Data isolation by tenant/customer
- Audit logging

### Data Security
- HTTPS encryption
- Secure API communication
- Input validation
- XSS protection
- CSRF protection

## Next Steps

- Learn about operational workflows in [Workflows](./workflows.md)
- Understand user permissions in [User Roles](./user-roles.md)
- Configure the system in [Configuration](./configuration.md)
