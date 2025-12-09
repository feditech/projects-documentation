# User Guide

A comprehensive guide for end users of the Units warehouse management system.

## Introduction

This guide is designed to help you navigate and use Units effectively in your daily work. Whether you're a warehouse operator, customer, or administrator, this guide will walk you through common tasks and best practices.

## Getting Around Units

### Main Navigation

The Units interface consists of several key areas:

#### Top Navigation Bar
- **Logo**: Click to return to dashboard
- **User Menu**: Access your profile and logout
- **Language Selector**: Switch between English and Arabic
- **Notifications**: View system alerts and messages

#### Side Menu (Admin Users)
- Dashboard
- Leads
- Quotations
- Inbound Requests
- Orders
- SKU (Inventory)
- Reports
- Settings

#### Side Menu (Customer Users)
- Dashboard
- Inbound Requests
- Orders
- SKU (Inventory)
- Reports
- Customer Address

### Navigation Tips
1. **Use breadcrumbs** at the top of pages to track your location
2. **Search bars** are available on list pages to quickly find records
3. **Filter buttons** help narrow down data
4. **Action buttons** are context-sensitive based on record status

## Common Tasks

### For All Users

#### Changing Your Password
1. Click your **username** in the top right
2. Select **Profile** or **Settings**
3. Click **Change Password**
4. Enter current password
5. Enter new password (must meet requirements)
6. Confirm new password
7. Click **Save**

#### Switching Languages
1. Click the **language selector** (EN/AR) in top navigation
2. Choose your preferred language
3. The entire interface will update immediately
4. Your preference is saved for future sessions

#### Viewing Notifications
1. Click the **bell icon** in top navigation
2. Review recent notifications
3. Click on a notification to view details
4. Mark as read when addressed

### For Customer Users

#### Creating an Outbound Order

**Step 1: Start New Order**
1. Go to **Orders**
2. Click **Add Order** button
3. Order form opens

**Step 2: Basic Information**
1. **Customer** is auto-selected (your account)
2. **Delivery Address**: Select from dropdown or add new
3. **Required Delivery Date**: Choose from calendar
4. **Time Slot**: Select preferred delivery window (if applicable)
5. **Special Instructions**: Add any delivery notes

**Step 3: Add Products**
1. Click **Add Item**
2. **Select SKU**: Choose from your product catalog
3. **Quantity**: Enter amount to ship
4. **Verify Stock**: System shows available quantity
5. Repeat for each product

**Step 4: Shipping Method**
1. **Carrier**: Select shipping carrier
2. **Service Level**: Choose (Standard, Express, etc.)
3. Or select **Self Collection** if picking up

**Step 5: Review and Submit**
1. Review order summary
2. Check total quantities
3. Verify delivery details
4. Click **Submit Order**
5. Note your **Order Number** for tracking

**Step 6: Track Your Order**
- Order appears in your orders list
- Status updates automatically
- Receive notifications at key milestones
- Click order to view detailed status

#### Checking Inventory Levels
1. Navigate to **SKU** menu
2. View list of all your products
3. **Stock** column shows current quantity
4. Click on SKU for location details
5. View stock by warehouse location
6. Check stock movement history

#### Creating an Inbound Request
1. Go to **Inbound Requests**
2. Click **Add Inbound Request**
3. Fill in details:
   - **Supplier**: Select supplier or enter details
   - **Expected Delivery Date**: Choose date
   - **Time Slot**: Select receiving window
4. Add products:
   - Select SKU
   - Enter expected quantity
5. Attach documents (PO, packing list)
6. Submit request
7. Warehouse team will process upon arrival

#### Adding a New SKU
1. Navigate to **SKU**
2. Click **Add SKU**
3. Enter required information:
   - **SKU Code**: Unique identifier
   - **Description**: Product name/description
   - **Category**: Product category
   - **Brand**: Product brand
   - **Supplier**: Primary supplier
   - **Dimensions**: Length, Width, Height
   - **Weight**: Product weight
4. Upload product images
5. Set reorder points (optional)
6. Click **Save**

#### Adding a Delivery Address
1. Go to **Customer Address**
2. Click **Add Address**
3. Enter address details:
   - Address name/label
   - Street address
   - City, Region
   - Postal code
   - Country
4. Add delivery instructions
5. Set as default (optional)
6. Click **Save**

#### Viewing Reports
1. Navigate to **Reports**
2. Select report type:
   - **SKU Report**: Inventory summary
   - **Stock Movement Report**: Transaction history
3. Set parameters:
   - Date range
   - Specific SKUs (optional)
4. Click **Generate**
5. Review on screen
6. Click **Export** to download (Excel/PDF)

### For Admin Users

#### Processing Goods Receipt (GRN)

**Step 1: Prepare**
1. Review scheduled inbound requests
2. Ensure receiving area is ready
3. Have scanner/mobile device ready

**Step 2: Start GRN**
1. Go to **Inbound Requests**
2. Click **Goods Received** tab
3. Find today's scheduled receipt
4. Click **Start Receiving**

**Step 3: Record Receipt**
1. Enter vehicle details:
   - License plate
   - Driver name
   - Seal number
2. Take photos of:
   - Vehicle exterior
   - Shipment condition
3. Note arrival time (auto-recorded)

**Step 4: Unload and Stage**
1. Unload items to staging area
2. Organize by SKU
3. Perform initial count
4. Note any obvious damages

**Step 5: Complete GRN**
1. Click **Complete GRN**
2. Items move to Counting stage
3. Notify counting team

#### Counting Inbound Items

**Step 1: Access Counting**
1. Go to **Inbound Requests**
2. Click **Counting** tab
3. Select inbound to count

**Step 2: Count Each SKU**
1. Locate first SKU in staging
2. Scan barcode or enter SKU code
3. Count physical quantity
4. Enter quantity in system
5. Record batch/lot numbers
6. Capture serial numbers (if applicable)

**Step 3: Note Discrepancies**
- If count ≠ expected:
  - Recount to verify
  - Take photos
  - Document reason (if known)
  - Add notes

**Step 4: Complete Count**
1. Click **Submit Count**
2. Items move to QC stage
3. System flags variances for review

#### Quality Control (QC) Process

**Step 1: Access QC Panel**
1. Go to **Inbound Requests**
2. Click **QC** tab
3. Select items for inspection

**Step 2: Inspect Each SKU**
1. Check product condition:
   - Packaging intact?
   - Product undamaged?
   - Correct product/version?
2. Verify quality standards:
   - Meets specifications?
   - Acceptable quality level?
3. Check dates:
   - Manufacturing date
   - Expiry date (if applicable)
   - Sufficient shelf life?

**Step 3: Make Decision**
For each SKU:
- **Accept**: Product passes, approve for putaway
- **Reject**: Product fails, quarantine
- **Partial Accept**: Some units pass, some fail

**Step 4: Document**
1. Take photos of issues
2. Add detailed notes
3. Specify reason for rejections
4. Record sample test results (if applicable)

**Step 5: Complete QC**
1. Click **Submit QC**
2. Accepted items move to Putaway
3. Rejected items quarantined
4. Customer notified of issues

#### Putaway Process

**Step 1: Access Putaway**
1. Go to **Inbound Requests**
2. Click **Put Away** tab
3. Select items to putaway

**Step 2: Review Suggestions**
- System suggests optimal locations based on:
  - Product storage requirements
  - Available capacity
  - FIFO/FEFO requirements
  - Picking efficiency

**Step 3: Putaway Each SKU**
1. Take product to suggested location
2. Scan location barcode to confirm
3. Scan product barcode
4. Enter quantity placed
5. Click **Confirm**
6. Move to next SKU

**Step 4: Complete Putaway**
1. All SKUs placed
2. Click **Complete**
3. Inventory updated automatically
4. Inbound marked complete
5. Customer receives notification

#### Order Picking

**Step 1: View Assignments**
1. Go to **Orders**
2. Click **Assigned Picker** tab
3. View your assigned orders
4. Select order to pick

**Step 2: Review Pick List**
- System shows optimized route
- Lists locations in sequence
- Shows quantities per SKU

**Step 3: Pick Each Item**
1. Navigate to first location
2. Scan location barcode
3. Locate product
4. Scan product barcode
5. Pick required quantity
6. Place in order bin
7. Click **Confirm**
8. Move to next location

**Step 4: Complete Pick**
1. All items picked
2. Verify quantities
3. Click **Complete Picking**
4. Deliver to QC/packing area
5. Order moves to Picked status

#### Order Packing

**Step 1: Access Packing**
1. Go to **Orders**
2. Click **Picked** tab
3. Select order to pack

**Step 2: Select Packaging**
- Choose appropriate box/envelope size
- Consider product fragility
- Check carrier requirements

**Step 3: Pack Items**
1. Verify all items present
2. Add packing materials (bubble wrap, etc.)
3. Pack securely
4. Close and seal package

**Step 4: Record Package Details**
1. Enter dimensions (L x W x H)
2. Weigh package
3. Enter weight
4. Record number of boxes (if multiple)

**Step 5: Generate Label**
1. Click **Generate Shipping Label**
2. System creates label from carrier
3. Print label
4. Apply to package

**Step 6: Complete Packing**
1. Click **Complete Packing**
2. Order moves to Packed status
3. Ready for dispatch

#### Assigning Pickers to Orders

**Step 1: View Unassigned**
1. Go to **Orders**
2. Click **Unassigned Picker** tab
3. See list of orders needing assignment

**Step 2: Assign Orders**
1. Select one or more orders
2. Click **Assign Picker**
3. Choose picker from dropdown:
   - Consider workload
   - Check zone familiarity
   - Balance assignments
4. Click **Assign**

**Step 3: Wave Picking (Optional)**
- Group multiple orders
- Assign to one picker
- Efficient for similar locations
- Reduces travel time

#### Creating a Customer Account
1. Go to **Settings → Customers**
2. Click **Add Customer**
3. Enter company details:
   - Company name
   - Tax ID/Registration
   - Contact person
   - Email and phone
4. Add address
5. Set pricing tier (if applicable)
6. Click **Save**
7. Create user accounts for customer:
   - Go to **Settings → Users**
   - Add users and link to customer

## Tips and Best Practices

### General Tips
1. **Save frequently** - Don't lose your work
2. **Use search** - Faster than scrolling
3. **Check notifications** - Stay informed
4. **Review before submitting** - Verify data accuracy
5. **Keep notes** - Document unusual situations

### Inventory Management Tips
1. **Regular cycle counts** - Maintain accuracy
2. **FIFO/FEFO rotation** - First in/first out
3. **Label clearly** - Easy to find items
4. **Update promptly** - Real-time accuracy
5. **Monitor reorder points** - Avoid stockouts

### Order Fulfillment Tips
1. **Scan everything** - Reduces picking errors
2. **Follow pick path** - System optimizes route
3. **Verify quantities** - Count twice, ship once
4. **Pack properly** - Prevent damage in transit
5. **Ship on time** - Meet delivery commitments

### Quality Control Tips
1. **Be thorough** - Don't rush inspections
2. **Document issues** - Photos and notes
3. **Communicate quickly** - Alert customers ASAP
4. **Follow standards** - Consistent criteria
5. **Sample appropriately** - Balance speed and accuracy

## Keyboard Shortcuts

- **Ctrl + S**: Save current form
- **Esc**: Close modal/dialog
- **Ctrl + F**: Focus search box
- **Tab**: Navigate between fields
- **Enter**: Submit form (when focused on submit button)

## Mobile Usage

Units is optimized for tablets and mobile devices:

1. **Responsive Design**: Adapts to screen size
2. **Touch-friendly**: Large buttons and controls
3. **Barcode Scanning**: Use device camera
4. **Offline Mode**: Basic functionality without internet (limited)
5. **Quick Actions**: Swipe gestures on lists

### Using on Mobile
1. Open web browser on mobile device
2. Navigate to Units URL
3. Login with your credentials
4. Interface automatically adjusts
5. Use landscape mode for better view

## Accessibility

Units supports accessibility features:

- **Keyboard Navigation**: Full keyboard access
- **Screen Readers**: Compatible with common screen readers
- **High Contrast**: Support for high contrast modes
- **Font Scaling**: Respects browser zoom settings
- **Alt Text**: Images have descriptive text

## Data Entry Best Practices

### Required Fields
- Marked with asterisk (*)
- Must be filled before saving
- Red border indicates missing

### Field Validation
- Real-time validation as you type
- Error messages explain issues
- Fix errors before proceeding

### Date Entry
- Use date picker for consistency
- Format: YYYY-MM-DD or as per locale
- Time zones: System uses your local time

### Quantity Entry
- Positive numbers only
- Decimals allowed where appropriate
- System checks against limits

## Getting Help

### In-System Help
1. Look for **(?)** icons next to fields
2. Hover for tooltip explanations
3. Click for detailed help articles

### Support Resources
1. **Documentation**: This guide and others
2. **Admin Contact**: Reach out to your system administrator
3. **Training**: Request additional training if needed
4. **FAQ**: Check [FAQ](./faq.md) for common questions

### Reporting Issues
If you encounter a problem:
1. Note what you were doing
2. Take a screenshot if helpful
3. Note any error messages
4. Contact your administrator with details
5. Include your username and timestamp

## Next Steps

- Review [Features](./features.md) for detailed feature documentation
- Learn [Workflows](./workflows.md) for operational processes
- Check [User Roles](./user-roles.md) to understand your permissions
- See [Troubleshooting](./troubleshooting.md) for common issues
