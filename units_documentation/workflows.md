# Workflows

This guide describes standard operational workflows in the Units warehouse management system.

## 1. Customer Onboarding Workflow

### Step-by-step Process

```
Lead Creation → Quotation → Acceptance → Customer Setup → Service Activation
```

#### 1.1 Lead Creation
1. Navigate to **Leads**
2. Click **Add Lead**
3. Enter lead information:
   - Contact name and details
   - Company information
   - Expected storage requirements
   - Service interests
4. Save lead

#### 1.2 Quotation Generation
1. Open lead record
2. Click **Create Quotation**
3. Add service line items:
   - Storage fees (per pallet/sqm/cubic meter)
   - Handling charges (inbound/outbound)
   - Value-added services
   - Monthly/annual contracts
4. Include terms and conditions
5. Generate PDF quotation
6. Send to customer

#### 1.3 Quotation Acceptance
1. Customer reviews quotation
2. Customer accepts via email or portal
3. Payment processed
4. System records acceptance

#### 1.4 Customer Account Setup
1. Convert lead to customer
2. Create customer profile
3. Set up delivery addresses
4. Configure customer-specific settings
5. Create user accounts for customer
6. Send welcome email with credentials

#### 1.5 Service Activation
1. Assign warehouse space
2. Configure SKU catalog access
3. Schedule initial receipt
4. Provide training and documentation

## 2. Inbound Receiving Workflow

### Complete Inbound Process

```
Create Request → Schedule Delivery → Receive Goods → Count → QC → Putaway → Complete
```

#### 2.1 Create Inbound Request
**Who**: Customer or Admin
1. Navigate to **Inbound Requests**
2. Click **Add Inbound Request**
3. Fill in details:
   - Customer selection
   - Supplier information
   - Expected delivery date
   - Time slot selection
4. Add line items:
   - Select SKUs
   - Enter expected quantities
   - Note special handling requirements
5. Attach documents (PO, packing list)
6. Submit request

#### 2.2 Schedule Delivery
**Who**: Admin/Planner
1. Review inbound request
2. Confirm time slot availability
3. Assign receiving dock
4. Notify warehouse team
5. Send confirmation to customer/supplier

#### 2.3 Goods Receiving (GRN)
**Who**: Receiving Clerk
1. Go to **Inbound Requests → Goods Received** tab
2. Select scheduled inbound
3. Click **Start Receiving**
4. Record:
   - Actual arrival time
   - Vehicle details (license plate, driver)
   - Seal number (if applicable)
5. Take photos of shipment
6. Unload and stage goods
7. Initial visual inspection
8. Complete GRN entry

#### 2.4 Counting
**Who**: Warehouse Operator
1. Navigate to **Inbound Requests → Counting** tab
2. Select items to count
3. For each SKU:
   - Scan barcode or enter SKU code
   - Enter actual quantity received
   - Record batch/lot numbers
   - Capture serial numbers (if applicable)
4. Note any variances from expected
5. Take photos of discrepancies
6. Complete count and submit

#### 2.5 Quality Control
**Who**: QC Inspector
1. Go to **Inbound Requests → QC** tab
2. Select items for inspection
3. For each SKU:
   - Check product condition
   - Verify quality standards
   - Test samples (if required)
   - Check expiry dates
   - Note any damages or defects
4. Decision:
   - **Accept**: Approve for putaway
   - **Reject**: Quarantine and document issues
   - **Partial Accept**: Accept good units, quarantine bad
5. Upload inspection photos
6. Complete QC report

#### 2.6 Putaway
**Who**: Warehouse Operator
1. Navigate to **Inbound Requests → Put Away** tab
2. Select approved items
3. System suggests optimal locations based on:
   - SKU storage rules
   - Available capacity
   - Product characteristics
   - Rotation requirements (FIFO/FEFO)
4. For each SKU:
   - Navigate to suggested location
   - Scan location barcode
   - Scan product barcode
   - Confirm quantity
5. Complete putaway
6. System updates inventory

#### 2.7 Completion
- System automatically marks as completed
- Inventory is now available
- Customer receives notification
- Records archived for reference

### Exception Handling

#### Overshipment (Received > Expected)
1. QC inspector notes overage
2. Take photos
3. Contact customer for instructions
4. Options:
   - Accept all (adjust fees)
   - Return excess
   - Hold for decision

#### Undershipment (Received < Expected)
1. Count verifies shortage
2. Document discrepancy
3. Notify customer and supplier
4. Options:
   - Accept short shipment
   - Wait for remaining items
   - Cancel and return

#### Damaged Goods
1. QC rejects damaged items
2. Document with photos
3. Quarantine damaged goods
4. File claim with carrier/supplier
5. Await customer instructions

## 3. Outbound Fulfillment Workflow

### Complete Outbound Process

```
Order Creation → Picking → QC → Packing → Dispatch → Delivery
```

#### 3.1 Order Creation
**Who**: Customer or Admin
1. Navigate to **Orders**
2. Click **Add Order**
3. Enter order details:
   - Customer selection
   - Delivery address
   - Required delivery date
   - Special instructions
4. Add order lines:
   - Select SKUs
   - Enter quantities
   - Verify stock availability
5. Choose shipping method:
   - Carrier selection
   - Service level (standard, express)
   - Or self-collection
6. Submit order

#### 3.2 Order Allocation
**System Automatic**
- System checks inventory availability
- Allocates stock from optimal locations
- Generates pick list
- Orders priority based on:
  - Delivery date
  - Customer priority
  - Order value

#### 3.3 Picker Assignment
**Who**: Warehouse Supervisor
1. Review **Unassigned Picker** tab
2. Assign orders to pickers based on:
   - Workload balance
   - Zone familiarity
   - Order priority
3. Generate pick waves if batching orders

#### 3.4 Picking
**Who**: Warehouse Picker
1. Access **Assigned Picker** tab
2. Select order to pick
3. Review pick list (optimized route)
4. For each line:
   - Navigate to location
   - Scan location barcode
   - Pick quantity
   - Scan product barcode
   - Place in order bin
5. Mark as picked
6. Move to QC area

#### 3.5 Outbound QC
**Who**: QC Inspector
1. Review picked orders
2. For each order:
   - Verify SKUs match order
   - Check quantities
   - Inspect product condition
   - Confirm lot numbers (if required)
3. Decision:
   - **Pass**: Send to packing
   - **Fail**: Return to picking with notes

#### 3.6 Packing
**Who**: Packing Operator
1. Access **Picked** tab
2. Select order to pack
3. Choose appropriate packaging
4. Pack items securely
5. Record:
   - Package dimensions
   - Weight
   - Number of boxes
6. Apply packing materials
7. Generate shipping label
8. Attach label to package
9. Mark as packed

#### 3.7 Dispatch
**Who**: Dispatch Clerk
1. Review **Packed** tab
2. Group by carrier
3. Schedule carrier pickup
4. Hand over packages to carrier
5. Scan tracking numbers
6. Mark as dispatched
7. Send tracking info to customer

#### 3.8 Delivery Confirmation
**System/Manual**
- Carrier provides delivery confirmation
- Update order status to completed
- Customer receives confirmation
- POD (Proof of Delivery) captured

### Alternative Workflows

#### Self-Collection
1. Customer selects self-collection
2. System schedules collection time slot
3. Picking and packing as normal
4. Items staged in collection area
5. Customer arrives:
   - Verify identity
   - Scan order barcode
   - Customer signs receipt
6. Mark as collected

#### Returns Processing
1. Customer requests return
2. Create return order
3. Customer ships or brings items
4. Receiving process:
   - Check return authorization
   - Inspect condition
   - Determine disposition:
     - Restock (if good)
     - Quarantine (if damaged)
     - Dispose (if unusable)
5. Update inventory
6. Process refund/credit

## 4. Inventory Management Workflows

### 4.1 SKU Creation
**Who**: Admin or Customer Admin
1. Navigate to **SKU**
2. Click **Add SKU**
3. Enter details:
   - SKU code (unique)
   - Description
   - Category and brand
   - Supplier
   - Dimensions and weight
   - Storage requirements
4. Upload product images
5. Set reorder points
6. Save SKU

### 4.2 Inventory Adjustment
**Who**: Admin
1. Navigate to **Stock Report**
2. Find SKU to adjust
3. Click adjustment action
4. Enter:
   - Adjustment type (add/remove)
   - Quantity
   - Reason
   - Reference document
5. Submit adjustment
6. System updates inventory

### 4.3 Cycle Counting
**Who**: Warehouse Operator
1. Generate cycle count list
2. For each location:
   - Navigate to location
   - Count physical stock
   - Enter count in system
3. System compares to book inventory
4. Investigate variances
5. Adjust if necessary
6. Document findings

### 4.4 Stock Transfer
**Who**: Warehouse Operator
1. Select SKU and quantity
2. Specify:
   - From location
   - To location
   - Reason
3. Scan from location
4. Pick quantity
5. Scan to location
6. Confirm transfer
7. System updates locations

## 5. Reporting Workflows

### 5.1 Generate Standard Report
1. Navigate to **Reports**
2. Select report type
3. Set parameters:
   - Date range
   - Filters (customer, SKU, warehouse)
4. Click **Generate**
5. Review on screen
6. Export if needed (PDF/Excel)

### 5.2 Schedule Automated Reports
**Who**: Admin
1. Go to report configuration
2. Select report type
3. Define schedule:
   - Frequency (daily, weekly, monthly)
   - Time of day
   - Recipients
4. Set parameters
5. Save schedule
6. Reports auto-generate and email

## 6. User Management Workflows

### 6.1 Create New User
**Who**: Admin
1. Navigate to **Settings → Users**
2. Click **Add User**
3. Enter details:
   - Name and email
   - User type (Admin/Customer)
   - Assigned customer (if customer user)
   - Permissions
4. Send invitation email
5. User receives credentials
6. User logs in and sets password

### 6.2 Deactivate User
**Who**: Admin
1. Find user in list
2. Click edit
3. Change status to inactive
4. Save
5. User immediately loses access

## 7. Warehouse Setup Workflows

### 7.1 Configure New Warehouse
**Who**: Admin
1. Navigate to **Settings → Warehouses**
2. Click **Add Warehouse**
3. Enter warehouse details:
   - Name and address
   - Contact information
   - Operating hours
4. Create Areas:
   - Define zones (A, B, C, etc.)
   - Assign area types (ambient, chilled, frozen)
5. Create Racks within each area:
   - Rack identifiers
   - Number of levels
6. Generate Locations:
   - Location codes (e.g., A-01-01)
   - Capacity per location
7. Print location barcodes
8. Apply labels to physical locations

## 8. Exception Management

### 8.1 Stock Discrepancy
1. Discrepancy identified
2. Investigate cause:
   - Count error
   - Unreported damage
   - Theft
   - System error
3. Perform recount
4. Document findings
5. Adjust inventory
6. Implement corrective actions

### 8.2 Damaged Inventory
1. Damage discovered
2. Quarantine items
3. Document with photos
4. Notify customer
5. Determine cause
6. Disposition decision:
   - Write off
   - Return to supplier
   - Customer instruction
7. Adjust inventory
8. File claim if applicable

### 8.3 Expired Products
1. Automated alerts for near-expiry
2. Review expiring items
3. Notify customer
4. Options:
   - Return to customer
   - Dispose (if customer authorizes)
   - Discount sale (if applicable)
5. Remove from sellable inventory

## Best Practices

1. **Always scan barcodes** - Reduces errors
2. **Complete tasks same day** - Don't leave work pending
3. **Verify quantities** - Count twice, adjust once
4. **Document exceptions** - Photos and notes
5. **Communicate proactively** - Alert customers early
6. **Follow FIFO/FEFO** - First in/first expired, first out
7. **Keep locations organized** - Makes picking faster
8. **Regular cycle counts** - Maintain inventory accuracy
9. **Review reports** - Monitor performance metrics
10. **Continuous improvement** - Learn from issues

## Next Steps

- Review specific [Features](./features.md) for detailed capabilities
- Understand [User Roles](./user-roles.md) and permissions
- Check [Troubleshooting](./troubleshooting.md) for common issues
