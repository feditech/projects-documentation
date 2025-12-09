# Document Management System (DMS) Module

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [User Interface](#user-interface)
- [Document Organization](#document-organization)
- [Document Operations](#document-operations)
- [Settings and Configuration](#settings-and-configuration)
- [Reports and Logs](#reports-and-logs)
- [User Permissions](#user-permissions)
- [Best Practices](#best-practices)

## Overview

The Document Management System (DMS) module provides comprehensive document storage, organization, and management capabilities. It enables users to organize documents hierarchically using cabinets, folders, and files with rich metadata and version control.

### Module Access

Access the DMS module at: `/dms/documents`

Users must have module access (module ID: 1) to use DMS features.

## Key Features

### Document Storage
- Upload and store documents in various formats
- Support for PDF, Word, Excel, images, and more
- Large file support with chunked uploads
- Automatic file type detection

### Organization
- Hierarchical structure with cabinets and folders
- Structure templates for consistent organization
- Document profiles for classification
- Categories and tags for easy discovery

### Version Control
- Track document versions
- Compare version changes
- Restore previous versions
- Version history and metadata

### Document Processing
- OCR (Optical Character Recognition) support
- Document scanning integration
- PDF generation and manipulation
- Thumbnail generation

### Security & Access Control
- Permission-based access
- Document-level security
- Audit trail for all operations
- Secure document sharing

### Search & Discovery
- Full-text search
- Advanced filtering
- Metadata-based search
- Quick access to recent documents

## User Interface

### Document Explorer

The main interface for browsing and managing documents:

**Navigation Pane:**
- Hierarchical tree view of cabinets and folders
- Expandable/collapsible folders
- Quick navigation breadcrumbs

**Document List View:**
- Grid or list view options
- Sortable columns (name, date, size, type)
- Multi-select for batch operations
- Contextual actions menu

**Actions Toolbar:**
- Upload document
- Create folder
- Bulk operations
- View options
- Search/filter

### Document Information Page

Detailed view of document properties:

**Tabs:**
- **General:** Basic information and metadata
- **Versions:** Version history and comparison
- **Permissions:** Access control settings
- **Activity:** Audit log and history
- **Preview:** Document preview/viewer

## Document Organization

### Cabinets

Top-level organizational containers:

**Creating a Cabinet:**
1. Navigate to Settings → Cabinets
2. Click "Add Cabinet"
3. Enter cabinet name and description
4. Set permissions and ownership
5. Save cabinet

**Cabinet Properties:**
- Name and description
- Owner/administrator
- Default permissions
- Structure template (optional)

### Folders

Organize documents within cabinets:

**Creating a Folder:**
1. Navigate to parent location
2. Click "New Folder"
3. Enter folder name and metadata
4. Set folder properties
5. Save folder

**Folder Features:**
- Nested folder structure
- Custom metadata fields
- Inherited permissions
- Folder templates

### Structure Templates

Predefined folder hierarchies:

**Use Cases:**
- Standardize project structures
- Enforce organizational policies
- Rapid setup of new cabinets
- Consistent naming conventions

**Creating a Template:**
1. Navigate to Settings → Structure Templates
2. Define folder hierarchy
3. Set default properties
4. Assign to cabinets

## Document Operations

### Uploading Documents

**Single File Upload:**
1. Navigate to target folder
2. Click "Upload" button
3. Select file from computer
4. Fill in metadata
5. Click "Upload"

**Drag & Drop:**
- Drag files from desktop to browser
- Automatic folder detection
- Bulk upload support

**Scanner Integration:**
- Direct scanning using TWAIN-compatible scanners
- Multi-page scanning
- Image enhancement options
- Automatic OCR processing

### Editing Documents

**Content Editing:**
- In-browser document editing
- Track changes
- Collaborative editing support
- Auto-save functionality

**Edit Requests:**
1. Request document editing permission
2. Admin approves request
3. Document locked for editing
4. Save changes and release lock

### Versioning

**Creating New Version:**
1. Open document
2. Click "Upload New Version"
3. Select updated file
4. Add version notes
5. Save version

**Version Management:**
- View version history
- Compare versions
- Download specific version
- Restore previous version
- Delete old versions

### Document Sharing

**Share Options:**
- Internal users/groups
- Public links (with expiry)
- Password-protected links
- Download/view-only permissions

**Share Process:**
1. Select document
2. Click "Share"
3. Choose recipients or generate link
4. Set permissions and expiry
5. Send notification

### Document Actions

**Available Actions:**
- Download
- Preview
- Edit
- Move
- Copy
- Rename
- Delete
- Share
- Add to favorites
- Export metadata

## Settings and Configuration

### Document Types

Define types of documents:

**Configuration:**
- Name and description
- File extension associations
- Default metadata fields
- Icon/thumbnail
- Processing rules

**Examples:**
- Contract
- Invoice
- Report
- Presentation
- Spreadsheet

### Document Categories

Classify documents by category:

**Configuration:**
- Category name
- Subcategories
- Color coding
- Default permissions
- Retention policies

**Examples:**
- Legal
- Financial
- HR
- Marketing
- Technical

### Document Profiles

Templates for document metadata:

**Profile Components:**
- Required fields
- Optional fields
- Field types and validation
- Default values
- Conditional fields

**Common Profiles:**
- Contract Profile: parties, dates, values
- Invoice Profile: vendor, amount, due date
- Report Profile: author, department, period

### Cabinets Management

**Settings:**
- Cabinet creation/deletion
- Permission templates
- Storage quotas
- Retention policies
- Archive rules

### Access Permissions

**Permission Levels:**
- **Read:** View documents
- **Write:** Edit and upload
- **Delete:** Remove documents
- **Admin:** Full control

**Permission Assignment:**
- User-level permissions
- Group-level permissions
- Inherited permissions
- Override permissions

## Reports and Logs

### Available Reports

**Document Reports:**
- Documents by type
- Documents by category
- Documents by date range
- Storage usage by cabinet
- Most accessed documents

**User Activity Reports:**
- User uploads/downloads
- User access logs
- Document modifications
- Share activity

**System Reports:**
- Storage capacity
- System performance
- Error logs
- Audit trail

### Audit Logs

Track all document operations:

**Logged Events:**
- Document upload
- Document download
- Document modification
- Document deletion
- Permission changes
- Access attempts
- Share activity

**Log Information:**
- Timestamp
- User
- Action performed
- Document/folder affected
- IP address
- Result (success/failure)

### Generating Reports

1. Navigate to Reports section
2. Select report type
3. Set date range and filters
4. Choose format (PDF, Excel, CSV)
5. Generate and download

## User Permissions

### Module Access

Users must be assigned DMS module access:
- Admin assigns module in user settings
- Module ID: 1
- Access controlled via `modules` field

### Document Permissions

**Folder-Level Permissions:**
- Permissions inherited by documents
- Override at document level
- Group-based access control

**Permission Matrix:**

| Action | Read | Write | Delete | Admin |
|--------|------|-------|--------|-------|
| View | ✓ | ✓ | ✓ | ✓ |
| Download | ✓ | ✓ | ✓ | ✓ |
| Upload | ✗ | ✓ | ✓ | ✓ |
| Edit | ✗ | ✓ | ✓ | ✓ |
| Delete | ✗ | ✗ | ✓ | ✓ |
| Share | ✗ | ✓ | ✓ | ✓ |
| Permissions | ✗ | ✗ | ✗ | ✓ |

### Role-Based Access

**Common Roles:**
- **Document Administrator:** Full DMS access
- **Power User:** Upload, edit, organize
- **Standard User:** View and download
- **Guest:** View only specific documents

## Best Practices

### Organization

1. **Use Consistent Structure**
   - Apply structure templates
   - Follow naming conventions
   - Maintain logical hierarchy

2. **Implement Metadata Standards**
   - Define required metadata
   - Use document profiles
   - Enforce consistent tagging

3. **Regular Maintenance**
   - Archive old documents
   - Delete obsolete files
   - Review and update permissions

### Security

1. **Principle of Least Privilege**
   - Grant minimum necessary permissions
   - Review permissions regularly
   - Use groups for access control

2. **Document Retention**
   - Define retention policies
   - Implement automatic archival
   - Comply with legal requirements

3. **Audit and Monitor**
   - Review audit logs regularly
   - Monitor unusual activity
   - Track document access

### Performance

1. **File Optimization**
   - Compress large files
   - Use appropriate formats
   - Optimize images and PDFs

2. **Storage Management**
   - Monitor storage usage
   - Implement quotas
   - Archive old documents

3. **Search Optimization**
   - Use meaningful filenames
   - Add relevant metadata
   - Keep structure organized

### Workflow

1. **Version Control**
   - Use meaningful version notes
   - Don't keep excessive versions
   - Lock documents during editing

2. **Collaboration**
   - Use edit requests properly
   - Communicate changes
   - Respect document locks

3. **Sharing**
   - Set appropriate expiry dates
   - Use view-only when possible
   - Track shared documents

## Common Tasks

### Creating a New Project Structure

1. Create cabinet for project
2. Apply structure template
3. Set project team permissions
4. Create initial folders
5. Upload project documents

### Scanning Paper Documents

1. Open document scanner tool
2. Configure scanner settings
3. Scan document pages
4. Apply OCR if needed
5. Save to appropriate folder
6. Add metadata

### Finding Documents

**Quick Search:**
- Use search bar
- Enter keywords
- Filter by type/category

**Advanced Search:**
- Set multiple criteria
- Date range filtering
- Metadata-based search
- Full-text search

### Batch Operations

1. Select multiple documents
2. Choose batch action:
   - Move to folder
   - Change category
   - Update metadata
   - Download as ZIP
   - Delete

## Troubleshooting

### Upload Fails

**Possible Causes:**
- File too large
- Insufficient permissions
- Storage quota exceeded
- Network timeout

**Solutions:**
- Check file size limits
- Verify permissions
- Contact administrator for quota
- Try smaller file or compress

### Cannot Edit Document

**Possible Causes:**
- Document locked by another user
- Insufficient permissions
- Edit request not approved

**Solutions:**
- Check document lock status
- Request edit permission
- Wait for approval
- Contact document owner

### Search Not Finding Documents

**Possible Causes:**
- Incorrect search terms
- Document not indexed
- Permission restrictions

**Solutions:**
- Try different keywords
- Use advanced search
- Check document permissions
- Verify document exists

## Related Documentation

- [Installation Guide](INSTALLATION.md)
- [Configuration Guide](CONFIGURATION.md)
- [API Documentation](API.md)
- [User Manual (PDF)](../public/usermanual_dms.pdf)

## Support

For additional help with DMS module:
- Review user manual PDF
- Contact system administrator
- Submit support ticket
- Check troubleshooting guide
