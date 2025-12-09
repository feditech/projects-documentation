# Frequently Asked Questions (FAQ)

Common questions and answers about the Units warehouse management system.

## General Questions

### What is Units?

Units is a cloud-based warehouse management system (WMS) designed to manage inventory, warehouse operations, and order fulfillment. It handles the complete logistics cycle from receiving goods to dispatching orders.

### Who can use Units?

Units is designed for:

- **Warehouse operators**: Businesses that provide warehousing and logistics services
- **E-commerce companies**: Managing inventory and fulfillment
- **Retailers**: Multi-location inventory management
- **Distributors**: Managing stock and orders
- **3PL providers**: Third-party logistics companies

### What makes Units different?

- **Multi-language support**: Full English and Arabic interface
- **Multi-tenant architecture**: Serve multiple clients from one system
- **Complete workflow management**: From receiving to dispatch
- **Mobile optimized**: Use on tablets and mobile devices
- **Integration ready**: E-commerce and carrier integrations

### Is Units a SaaS or on-premise solution?

Units is primarily a cloud-based SaaS (Software as a Service) solution. The frontend is a web application that connects to a cloud-hosted backend API.

### What browsers are supported?

- Google Chrome (recommended)
- Mozilla Firefox
- Apple Safari
- Microsoft Edge

All modern versions are supported. For best experience, use the latest version of Chrome.

## Account and Access

### How do I get a Units account?

Admin users create accounts for new users. Contact your warehouse administrator or the Units support team to request an account.

### Can I have multiple users under one customer account?

Yes. A customer account can have multiple users. Each user has their own login credentials while sharing the same inventory and orders.

### What's the difference between Admin and Customer users?

**Admin Users**:

- Full system access
- Manage all customers
- Perform warehouse operations
- Configure system settings
- Access all reports

**Customer Users**:

- Access their own data only
- Create orders and inbound requests
- View their inventory
- Generate their reports
- Cannot perform physical warehouse operations

### How do I reset my password?

1. Click "Forgot Password?" on the login page
2. Enter your email address
3. Check your email for reset link
4. Click the link and set a new password
5. Password must meet security requirements

### Can I change my email address?

Yes, but this must be done by an administrator. Contact your admin to update your email address.

### How long does my session last?

- With "Remember Me": Extended session (typically 30 days)
- Without "Remember Me": 24 hours or until you log out
- Sessions expire for security if inactive too long

## Features and Functionality

### Can I use Units on my mobile phone?

Yes! Units is responsive and works on mobile devices. However, some tasks are better suited for tablets or desktops. Warehouse operators typically use tablets with barcode scanners.

### Does Units support barcode scanning?

Yes. Units supports:

- USB barcode scanners (keyboard wedge mode)
- Bluetooth barcode scanners
- Camera-based scanning (mobile devices)
- QR codes and standard barcodes (Code 128, EAN, UPC)

### Can I import data in bulk?

Yes. Units supports bulk import via Excel for:

- SKUs (products)
- Customers
- Suppliers
- Inventory adjustments
- Order creation (in some cases)

Download the import template, fill it in, and upload.

### Can I export reports to Excel?

Yes. Most reports can be exported to:

- Excel (.xlsx)
- PDF
- CSV

Look for the "Export" button on report pages.

### Does Units integrate with e-commerce platforms?

Yes. Currently Units integrates with:

- **Salla**: Saudi e-commerce platform
- **Custom integrations**: Via API

More integrations can be added as needed.

### Can I track inventory by lot or batch number?

Yes. Units supports:

- Batch/lot number tracking
- Serial number tracking (individual items)
- Expiry date management
- FIFO (First In, First Out) rotation
- FEFO (First Expired, First Out) rotation

### Does Units support multi-warehouse operations?

Yes. You can:

- Manage multiple warehouses
- Transfer stock between warehouses
- View inventory across all locations
- Generate reports per warehouse

### Can customers see real-time inventory?

Yes. Customer users can view their real-time inventory levels, locations, and stock movements through their dashboard and reports.

## Inbound Operations

### How do I create an inbound request?

1. Go to **Inbound Requests**
2. Click **Add Inbound Request**
3. Enter supplier and expected delivery details
4. Add SKUs and quantities
5. Select delivery time slot
6. Submit request

### What if I receive more or less than expected?

The system tracks variances:

- **Overshipment**: Counted quantity exceeds expected
- **Undershipment**: Counted quantity less than expected

These are flagged during the counting stage, and you'll need to decide how to handle them (accept, reject, or await customer instructions).

### Can I schedule a delivery time?

Yes. When creating an inbound request, you can select a time slot. Available time slots are configured by the warehouse administrator.

### What happens after goods are received?

The standard workflow is:

1. **Goods Receiving (GRN)**: Record receipt
2. **Counting**: Verify quantities
3. **Quality Control**: Inspect condition
4. **Putaway**: Store in locations
5. **Completed**: Inventory updated

### Can I skip QC for some products?

This depends on your warehouse's standard operating procedures. Contact your administrator if you need to bypass QC for certain SKUs.

## Outbound Operations

### How do I create an order?

1. Go to **Orders**
2. Click **Add Order**
3. Select customer (or it's auto-selected if you're a customer user)
4. Choose delivery address
5. Add SKUs and quantities
6. Select shipping method
7. Submit order

### How do I know if I have enough stock?

When adding items to an order, the system shows available quantity. If there's insufficient stock, you'll see a warning and cannot proceed.

### Can I cancel an order?

Yes, but it depends on the order status:

- **Before picking starts**: Usually can cancel
- **During picking/packing**: May need admin approval
- **After dispatch**: Cannot cancel, must process as return

Contact your administrator or check the order status page for options.

### What shipping carriers are supported?

This depends on your warehouse's configuration. Common carriers include:

- Local delivery services
- International couriers (DHL, FedEx, Aramex, etc.)
- Self-collection

Ask your administrator about available carriers.

### Can customers pick up orders themselves?

Yes. Select "Self Collection" as the shipping method when creating an order. The system will schedule a pickup time slot.

### How do I track my order?

1. Go to **Orders**
2. Find your order in the list
3. Click to view details
4. See current status and tracking information

You'll also receive notifications for key milestones (picked, dispatched, etc.).

### What are the different order statuses?

- **Unassigned**: Order created, awaiting picker assignment
- **Assigned**: Picker assigned, not started
- **Picked**: Items picked, awaiting QC
- **Packed**: Packed and labeled, ready for dispatch
- **Dispatched**: Handed to carrier or ready for collection
- **Completed**: Successfully delivered
- **On Hold**: Temporarily paused
- **Cancelled**: Order cancelled
- **Returned**: Order returned by customer

## Inventory Management

### How do I add a new product (SKU)?

1. Go to **SKU** menu
2. Click **Add SKU**
3. Enter SKU code (unique)
4. Fill in description, dimensions, weight
5. Select category, brand, supplier
6. Upload product images
7. Save

### Can I edit SKU information later?

Yes. Open the SKU and click **Edit**. You can update most fields. The SKU code typically cannot be changed once created.

### How do I check current stock levels?

**Method 1: SKU List**

- Go to **SKU** menu
- View stock column for each SKU

**Method 2: SKU Details**

- Open specific SKU
- View detailed stock by location

**Method 3: Reports**

- Go to **Reports → SKU Report**
- View comprehensive inventory report

### What if inventory count is wrong?

**For Admins**:

1. Perform physical count
2. Navigate to stock adjustment page
3. Enter correct quantity
4. Provide reason for adjustment
5. Submit

**For Customers**:

- Request admin to perform adjustment
- Provide evidence if needed (photos, documents)

### How do I track where my inventory is located?

1. Go to **SKU** menu
2. Click on specific SKU
3. View "Locations" tab
4. See quantity at each warehouse location

### Can I see history of stock movements?

Yes. Go to **Reports → Stock Movement Report**:

- Select date range
- Optionally filter by SKU
- View all ins, outs, and adjustments
- Export to Excel for analysis

## Reporting

### What reports are available?

**Admin Reports**:

- Inbound Report: Receiving metrics
- Order Report: Fulfillment statistics

**Customer Reports**:

- SKU Report: Inventory valuation
- Stock Movement Report: Transaction history

**Dashboard**: Real-time KPIs and metrics

### Can I schedule reports to run automatically?

This feature may be available depending on your system configuration. Contact your administrator to set up scheduled reports.

### How far back can I view historical data?

You can typically view all historical data from when your account started. Use date range filters on reports to select the period you want to view.

### Can I customize reports?

Standard reports have predefined formats. For custom reports, contact your administrator. They may be able to:

- Generate custom queries
- Create new report templates
- Provide raw data exports

## Technical Questions

### What happens if I lose internet connection?

Units requires internet connectivity to function. If connection is lost:

- Unsaved data will be lost
- Save work frequently
- Connection restored: page may need refresh
- Some browsers cache data temporarily

### Is my data backed up?

Yes. The backend system performs regular backups. Data is stored securely and redundantly in the cloud.

### Is Units secure?

Yes. Units uses industry-standard security measures:

- HTTPS encryption for all communication
- JWT-based authentication
- Role-based access control
- Regular security updates
- Password complexity requirements
- Session management

### Can I access Units from anywhere?

Yes, as long as you have internet access and a web browser. Some organizations may restrict access to certain IP addresses for security.

### Does Units work offline?

No. Units requires internet connectivity. It's a cloud-based system that needs to communicate with the backend API.

### What if Units is down?

- Check [status page](https://status.units.abc.com) if available
- Contact your system administrator
- Check your internet connection first
- Try accessing from different device/network

### Can I integrate Units with our existing systems?

Yes. Units provides a RESTful API for integration. Contact your administrator or the Units support team to discuss integration options.

## Billing and Pricing

### How is Units priced?

Pricing typically depends on:

- Number of users
- Storage capacity used
- Transaction volume (inbounds/outbounds)
- Additional features and integrations

Contact Units sales team for specific pricing.

### Is there a free trial?

Contact Units sales team for trial availability and demo options.

### What's included in the base price?

This varies by plan. Typically includes:

- Core WMS features
- Standard reporting
- Customer support
- Regular updates

Check your contract or contact sales for details.

## Support and Training

### How do I get help?

1. **Documentation**: Check this guide and other docs
2. **In-app help**: Look for (?) icons
3. **Administrator**: Contact your system admin
4. **Support**: Email support@units.abc.com
5. **Training**: Request training sessions

### Is training available?

Yes. Training options typically include:

- Initial onboarding training
- Role-specific training
- On-site or remote sessions
- Video tutorials
- Documentation

Contact your administrator or sales team.

### What support hours are available?

Support hours depend on your service agreement. Typically:

- Standard support: Business hours (8 AM - 7 PM)
- Premium support: Extended hours or 24/7

Check your contract for specific SLA.

### How quickly will my issue be resolved?

Resolution time depends on:

- Issue severity (Critical, High, Medium, Low)
- Support plan level
- Complexity of the issue

Critical issues affecting business operations are prioritized.

## Future and Updates

### How often is Units updated?

Units is continuously improved with:

- Regular feature updates
- Bug fixes and security patches
- Performance improvements
- New integrations

Updates are applied transparently without downtime.

### Can I request new features?

Yes! Feature requests are welcome:

- Contact your account manager
- Submit via support channel
- Participate in user feedback sessions

Popular requests are prioritized for development.

### Will my data be affected by updates?

No. Updates are designed to be backward compatible. Your data remains safe and accessible during and after updates.

## Still Have Questions?

If your question isn't answered here:

1. **Search the documentation**: Use Ctrl+F in relevant docs
2. **Contact your administrator**: They may have organization-specific answers
3. **Contact support**: Email support@units.abc.com with your question
4. **Training**: Request a training session to learn more

## Helpful Resources

- [Getting Started](./getting-started.md) - First steps with Units
- [User Guide](./user-guide.md) - Detailed usage instructions
- [Features](./features.md) - Complete feature list
- [Workflows](./workflows.md) - Operational procedures
- [Troubleshooting](./troubleshooting.md) - Fixing common issues
