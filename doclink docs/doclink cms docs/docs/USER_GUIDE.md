# User Guide

## Table of Contents

- [Getting Started](#getting-started)
- [Login & Authentication](#login--authentication)
- [Dashboard Overview](#dashboard-overview)
- [Common Tasks](#common-tasks)
- [Module Guides](#module-guides)
- [Tips & Best Practices](#tips--best-practices)
- [FAQ](#faq)

## Getting Started

Welcome to DocLink CMS! This guide will help you navigate the system and perform common tasks.

### System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Stable internet connection
- Screen resolution: 1366x768 or higher (recommended)

### First Time Login

1. Open your web browser
2. Navigate to the DocLink CMS URL
3. Enter your credentials provided by your administrator
4. Click "Login"
5. You may be prompted to change your password on first login

## Login & Authentication

### Logging In

1. Go to the login page
2. Enter your email address
3. Enter your password
4. Click "Login" button

### Forgot Password

If you've forgotten your password:

1. Click "Forgot Password" on the login page
2. Enter your registered email address
3. Click "Submit"
4. Check your email for the verification code (OTP)
5. Enter the OTP on the verification page
6. Create a new password
7. Confirm your new password
8. Click "Submit" to save

### Password Requirements

- Minimum 8 characters
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- At least one special character (recommended)

### Changing Your Password

1. Click on your profile icon in the top right
2. Select "Change Password"
3. Enter your current password
4. Enter your new password
5. Confirm new password
6. Click "Submit"

## Dashboard Overview

### Navigation Menu

The left sidebar contains the main navigation menu with the following sections:

- **Dashboard**: Home page with overview statistics
- **Doctors**: Doctor management features
- **Patients**: Patient management
- **Blogs**: Content management for blogs
- **Masters**: Configuration and master data
- **Sessions**: Active and chat sessions
- **Finance**: Financial operations
- **Prepaid Card**: Card management
- **User Feedback**: Reports and feedback
- **Stories**: Story management
- **Settings**: System configuration
- **Policies**: Policy management
- **Modules Management**: Module configuration

### Top Bar

- **Search**: Quick search functionality
- **Notifications**: System notifications and alerts
- **Profile Menu**: Access to profile settings and logout

### Dashboard Widgets

The dashboard displays:
- Total doctors, patients, labs
- Recent activities
- Pending approvals
- Revenue statistics
- Active sessions
- Recent feedback

## Common Tasks

### Adding a New Record

Most modules follow a similar pattern for adding records:

1. Navigate to the relevant module (e.g., Doctors → Profiles)
2. Click the "Add" or "+" button (usually top right)
3. Fill in the required fields (marked with *)
4. Upload any necessary files/images
5. Click "Save" or "Submit"
6. Confirmation message will appear

### Editing an Existing Record

1. Navigate to the module
2. Find the record in the table (use search if needed)
3. Click the edit icon (pencil icon) in the actions column
4. Modify the fields as needed
5. Click "Update" or "Save"
6. Confirmation message will appear

### Deleting a Record

1. Navigate to the module
2. Find the record in the table
3. Click the delete icon (trash icon) in the actions column
4. Confirm deletion in the popup dialog
5. Record will be removed

⚠️ **Warning**: Deletion is usually permanent. Make sure you want to delete before confirming.

### Searching and Filtering

Most tables include search and filter options:

**Search**:
1. Locate the search box above the table
2. Enter your search term
3. Results update automatically or after clicking "Search"

**Filtering**:
1. Click the filter icon
2. Select filter criteria (date range, status, category, etc.)
3. Click "Apply"
4. Clear filters by clicking "Reset" or "Clear Filters"

### Exporting Data

Many tables allow data export:

1. Click the export button (usually near search/filters)
2. Select format (CSV, Excel, PDF)
3. File will download automatically
4. Open the file with appropriate application

### Pagination

Navigate through large datasets:
- **Items per page**: Select 10, 25, 50, or 100 items per page
- **Page numbers**: Click page numbers to jump to specific pages
- **Next/Previous**: Use arrows to move between pages

## Module Guides

### Doctor Management

#### Approving Doctor Requests

1. Go to **Dashboard → Doctors → Requests**
2. Review pending requests in the table
3. Click on a request to view details
4. Verify submitted documents:
   - License certificate
   - Educational certificates
   - ID proof
5. Check all information for accuracy
6. Click "Approve" to approve or "Reject" with reason
7. Doctor will be notified via email

#### Managing Doctor Profiles

1. Go to **Dashboard → Doctors → Profiles**
2. View all registered doctors
3. Use filters to find specific doctors:
   - By specialization
   - By status (Active/Inactive)
   - By verification status
4. Click on a doctor name to view full profile
5. Edit profile by clicking the edit button
6. Update information as needed
7. Save changes

#### Adding Specializations

1. Go to **Dashboard → Doctors → Specializations**
2. Click "Add Specialization"
3. Enter specialization name
4. Add description
5. Upload icon (optional)
6. Click "Save"

### Lab Management

#### Adding a New Lab

1. Go to **Dashboard → Masters → Labs**
2. Click "Add Lab"
3. Fill in lab details:
   - Lab name
   - Address and location
   - Contact information
   - Operating hours
   - Available services
4. Upload lab certification documents
5. Click "Save"

#### Managing Lab Services

1. Go to **Dashboard → Masters → Lab Service Category**
2. Add service categories (e.g., Blood Tests, Imaging)
3. Go to **Dashboard → Masters → Lab Test Category**
4. Add specific tests under each category
5. Set pricing for each test
6. Assign tests to labs

### Content Management

#### Creating a Blog Post

1. Go to **Dashboard → Blogs → List**
2. Click "Add Blog"
3. Enter blog title
4. Select category
5. Write content using the rich text editor:
   - Format text (bold, italic, underline)
   - Add headings
   - Insert images
   - Add links
   - Create lists
6. Upload featured image
7. Add tags for better discoverability
8. Select status:
   - **Draft**: Save for later
   - **Published**: Make live immediately
9. Click "Save"

#### Managing Banners

1. Go to **Dashboard → Masters → Banner**
2. Click "Add Banner"
3. Upload banner image (recommended size: 1920x1080px)
4. Select target screen
5. Set click action/link (if applicable)
6. Set display order/priority
7. Enable/disable banner
8. Click "Save"

### Financial Management

#### Viewing Transactions

1. Go to **Dashboard → Finance → Transactions**
2. Use filters to narrow down:
   - Date range
   - Transaction type
   - Status
   - User
3. View transaction details
4. Export for reporting

#### Processing Settlements

1. Go to **Dashboard → Finance → Settlements**
2. View pending settlements
3. Calculate settlement amount
4. Verify payment details
5. Process payment
6. Update settlement status
7. Generate settlement report

### User Management

#### Adding a New Admin User

1. Go to **Dashboard → Settings → Add User**
2. Enter user details:
   - Full name
   - Email address
   - Phone number
3. Select role (Admin, Content Manager, Support, etc.)
4. Set permissions (if custom)
5. Click "Save"
6. User will receive invitation email

#### Managing Roles and Permissions

1. Go to **Dashboard → Settings → Role Management**
2. View existing roles
3. Click "Add Role" to create new role
4. Enter role name and description
5. Go to **Dashboard → Settings → Permissions**
6. Assign permissions to the role:
   - Read
   - Write
   - Delete
   - Approve
   - Export
7. Save changes

### Support & Feedback

#### Handling Problem Reports

1. Go to **Dashboard → User Feedback → Report a Problem**
2. View all reported problems
3. Click on a report to view details
4. Assign to support team member
5. Add internal notes
6. Update status (In Progress, Resolved)
7. Respond to user if needed
8. Close ticket when resolved

#### Reviewing Session Feedback

1. Go to **Dashboard → User Feedback → Session Feedback**
2. View feedback and ratings
3. Filter by doctor, date, rating
4. Identify patterns or issues
5. Take action if needed (contact doctor, patient)
6. Export feedback reports

## Tips & Best Practices

### Data Entry

- **Required Fields**: Always fill all required fields (marked with *)
- **Validation**: Pay attention to validation messages
- **Images**: Use appropriate image sizes for faster loading
- **Documents**: Upload clear, readable documents
- **Naming**: Use clear, descriptive names

### Search & Filter

- **Keywords**: Use specific keywords for better search results
- **Filters**: Combine multiple filters for precise results
- **Date Ranges**: Use date filters to find recent records
- **Save Filters**: Some modules allow saving frequently used filters

### Performance

- **Pagination**: Use appropriate page sizes (don't load too many records at once)
- **Filters**: Apply filters before exporting large datasets
- **Browser**: Clear browser cache if pages load slowly
- **Images**: Optimize images before uploading

### Security

- **Password**: Use strong, unique passwords
- **Logout**: Always logout when done, especially on shared computers
- **Permissions**: Only grant necessary permissions
- **Sensitive Data**: Handle patient and financial data with care

### Workflow

- **Regular Checks**: Check pending approvals regularly
- **Backup**: Export important data regularly
- **Documentation**: Keep notes of important actions
- **Communication**: Keep users informed of decisions

## FAQ

### General

**Q: How do I reset my password?**
A: Click "Forgot Password" on the login page and follow the instructions.

**Q: Can I access the CMS from my mobile device?**
A: Yes, the CMS is responsive and works on tablets and phones, but desktop is recommended for best experience.

**Q: How often is data backed up?**
A: Contact your system administrator for backup schedules.

### Doctor Management

**Q: How long does doctor approval take?**
A: Review pending requests in the Doctors → Requests section and approve/reject as needed.

**Q: Can I bulk approve doctors?**
A: Check if bulk actions are available in your version. Use checkboxes to select multiple doctors.

**Q: How do I deactivate a doctor?**
A: Edit the doctor profile and change status to "Inactive".

### Content Management

**Q: Can I schedule blog posts?**
A: Check if your version supports scheduled publishing. Save as draft and set publish date.

**Q: What image formats are supported?**
A: JPG, PNG, GIF, and WEBP are commonly supported.

**Q: Can I edit a published blog?**
A: Yes, edit the blog and save changes. It will be updated immediately.

### Financial

**Q: How do I issue a refund?**
A: Navigate to the transaction and use the refund option if available.

**Q: Can I export financial reports?**
A: Yes, use the export function in Transactions and Settlements.

**Q: When are settlements processed?**
A: Check your platform's settlement schedule with administration.

### Technical Issues

**Q: The page is loading slowly. What should I do?**
A: Try clearing your browser cache, reducing page size, or checking your internet connection.

**Q: I can't upload images. What's wrong?**
A: Check file size (usually max 10MB) and format. Try a different browser.

**Q: I'm getting an error message. What should I do?**
A: Take a screenshot of the error and contact support with details of what you were doing.

### Access & Permissions

**Q: I can't see certain menu items. Why?**
A: Your role may not have access to those features. Contact your administrator.

**Q: Can I change my own permissions?**
A: No, only administrators can modify permissions.

**Q: How do I request access to a feature?**
A: Contact your system administrator with your request.

## Getting Help

### Support Channels

1. **In-App Help**: Look for help icons (?) throughout the interface
2. **Documentation**: Refer to this guide and other documentation
3. **Support Team**: Contact your support team via email or phone
4. **Admin**: Reach out to your system administrator

### Reporting Issues

When reporting an issue, include:
- What you were trying to do
- Steps to reproduce the issue
- Error messages (screenshots helpful)
- Your browser and operating system
- Your role/permissions

### Training

Request training sessions for:
- New features
- Complex workflows
- Best practices
- Advanced functionality

---

**Need more help?** Contact your system administrator or support team.

**Quick Reference**: Keep this guide bookmarked for easy access!
