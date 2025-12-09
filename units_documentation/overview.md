# Overview

## What is Units?

**Units** is a modern, cloud-based warehouse management system (WMS) designed to optimize logistics and inventory operations. It provides end-to-end visibility and control over warehouse processes, from receiving goods to dispatching orders.

## Key Capabilities

### 1. Warehouse Management
- Multi-warehouse support with hierarchical structure (Warehouses → Areas → Racks → Locations)
- Real-time inventory visibility across all storage locations
- Capacity planning and utilization tracking
- Warehouse mapping and bin location management

### 2. Inbound Logistics
- Inbound request creation and management
- Goods receiving (GRN) process
- Quality control and counting workflows
- Automated putaway recommendations
- Supplier management and tracking

### 3. Outbound Operations
- Order management and fulfillment
- Pick-pack-dispatch workflows
- Carrier integration and shipping management
- Order tracking and status updates
- Returns processing

### 4. Inventory Management
- SKU (Stock Keeping Unit) master data management
- Real-time stock levels and movements
- Product categorization and attributes
- Batch and lot tracking
- Stock movement reports

### 5. Customer & Supplier Management
- Customer account management
- Multiple delivery addresses per customer
- Supplier database and performance tracking
- Lead management and quotation processing

### 6. Reporting & Analytics
- Inbound and outbound reports
- SKU reports and stock movement history
- Order fulfillment metrics
- Dashboard with key performance indicators
- Customizable report generation

### 7. Multi-tenancy
- Support for multiple tenant organizations
- Tenant-specific customizations and branding
- Isolated data and user management per tenant

## User Types

Units supports different user roles with varying levels of access:

- **Admin Users**: Full system access, configuration, and user management
- **Customer Users**: Access to their inventory, orders, and reports
- **Warehouse Operators**: Daily operational tasks (receiving, picking, packing)

## Technology Stack

- **Frontend**: React 18 with TypeScript
- **UI Framework**: Material-UI (MUI) v5
- **State Management**: React Context API
- **Routing**: React Router v6
- **Internationalization**: i18next for multi-language support
- **Data Visualization**: MUI X-Charts
- **PDF Generation**: jsPDF and pdf-lib
- **API Communication**: Axios
- **Maps Integration**: Google Maps API

## Core Principles

1. **Ease of Use**: Intuitive interface designed for warehouse operators
2. **Real-time Updates**: Live inventory and order status tracking
3. **Flexibility**: Configurable workflows to match business needs
4. **Scalability**: Support for growing operations and multiple locations
5. **Accuracy**: Built-in validation and quality control checks
6. **Visibility**: Comprehensive reporting and audit trails

## Integration Capabilities

- **E-commerce Platforms**: Integration with Salla and other e-commerce systems
- **Shipping Carriers**: Multiple carrier support for label generation and tracking
- **Import/Export**: Excel-based data import and export capabilities
- **API Access**: RESTful API for third-party integrations

## Business Value

Units helps businesses:

- **Reduce operational costs** through process optimization
- **Improve order accuracy** with guided workflows
- **Increase warehouse efficiency** with better space utilization
- **Enhance customer satisfaction** with faster fulfillment
- **Gain visibility** into inventory and operations
- **Scale operations** without proportional cost increases

## Next Steps

- For installation and setup, see [Getting Started](./getting-started.md)
- To learn about specific features, see [Features](./features.md)
- To understand operational workflows, see [Workflows](./workflows.md)
