# Visitor Management System (VMS) Module

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [User Interface](#user-interface)
- [Appointment Management](#appointment-management)
- [Check-In System](#check-in-system)
- [Workflow Configuration](#workflow-configuration)
- [Settings and Configuration](#settings-and-configuration)
- [Reports and Analytics](#reports-and-analytics)
- [User Permissions](#user-permissions)
- [Best Practices](#best-practices)

## Overview

The Visitor Management System (VMS) module provides comprehensive tools for managing visitor appointments, check-ins, and security workflows. It streamlines the visitor experience while maintaining security and compliance requirements.

### Module Access

Access the VMS module at: `/vms/dashboard`

Users must have module access (module ID: 3) to use VMS features.

## Key Features

### Appointment Scheduling
- Schedule visitor appointments
- Multi-visitor appointments
- Recurring appointments
- Pre-registration
- QR code generation
- Email notifications

### Check-In/Check-Out
- Quick check-in process
- Badge printing
- Host notification
- Real-time tracking
- Automatic check-out
- Visitor photos

### Visitor Tracking
- Real-time visitor status
- Location tracking
- Visit duration monitoring
- Historical records
- Visitor database

### Security & Compliance
- Visitor screening
- Watchlist checking
- NDA and agreement signatures
- Document verification
- Access control integration

### Workflow Management
- Configurable approval workflows
- Multi-level approvals
- Automatic routing
- Escalation rules
- Custom notifications

### Reporting & Analytics
- Visitor statistics
- Peak time analysis
- Host performance
- Compliance reports
- Custom analytics

## User Interface

### Dashboard

The VMS dashboard provides real-time visitor information:

**Key Metrics:**
- Total visitors today
- Currently checked in
- Pending appointments
- Today's appointments
- Completed visits this week
- Average visit duration

**Quick Actions:**
- Create appointment
- Quick check-in
- Search visitors
- View today's schedule
- Access active visitors

**Widgets:**
- Visitors by status (pie chart)
- Appointments timeline
- Recent check-ins
- Pending approvals
- Top hosts

### Appointments View

Manage all visitor appointments:

**List Features:**
- Calendar view option
- List view with filters
- Sort by date/time
- Search functionality
- Bulk actions
- Export options

**Appointment States:**
- **Pending:** Awaiting approval
- **Approved:** Approved for visit
- **In Progress:** Visitor checked in
- **Completed:** Visit finished
- **Cancelled:** Appointment cancelled
- **No Show:** Visitor didn't arrive

**Filters:**
- Date range
- Status
- Host
- Department
- Visitor name
- Purpose of visit

### Check-Ins View

Monitor active and recent check-ins:

**Real-Time Information:**
- Visitor name and photo
- Host information
- Check-in time
- Expected duration
- Current location
- Badge number

**Actions:**
- View details
- Extend visit
- Check out visitor
- Contact host
- Print badge
- Add notes

## Appointment Management

### Creating an Appointment

**Step-by-Step Process:**

1. **Basic Information**
   - Select appointment date and time
   - Choose appointment duration
   - Select purpose of visit
   - Add special instructions

2. **Visitor Details**
   - Enter visitor name(s)
   - Add contact information (email, phone)
   - Company/organization
   - Visitor category
   - Special requirements

3. **Host Assignment**
   - Select host (employee)
   - Choose department
   - Add alternate host
   - Notification preferences

4. **Additional Details**
   - Meeting location
   - Parking requirements
   - Equipment needs
   - Attachments (NDA, agenda)
   - Access requirements

5. **Submit and Notify**
   - Review appointment details
   - Submit for approval (if required)
   - Send confirmation to visitor
   - Notify host

### Appointment Types

**Single Visitor:**
- One visitor, one host
- Specific time slot
- Standard workflow

**Multi-Visitor:**
- Multiple visitors, one appointment
- Group meetings
- Shared approval

**Recurring Appointments:**
- Daily, weekly, monthly
- Contractor access
- Regular meetings
- End date or occurrence count

### Appointment Approval

**Approval Workflow:**
1. Host creates appointment
2. System routes for approval
3. Approver reviews details
4. Approver accepts or rejects
5. System notifies all parties

**Approval Criteria:**
- Visitor category
- Duration of visit
- Access level required
- Department policy
- Security clearance

### Appointment Notifications

**Email Notifications:**
- Appointment confirmation
- Approval status
- Reminder (day before, hour before)
- QR code for check-in
- Directions and instructions
- Cancellation notice

**SMS Notifications (if configured):**
- Check-in reminder
- Arrival notification to host
- Visit completion

### Appointment Modifications

**Reschedule:**
1. Open appointment
2. Click "Reschedule"
3. Select new date/time
4. Notify affected parties
5. Re-approve if required

**Cancel:**
1. Open appointment
2. Click "Cancel"
3. Provide reason
4. Notify visitor and host
5. Update status

**Extend:**
1. During active visit
2. Click "Extend"
3. Add additional time
4. Get approval if needed
5. Update badge expiry

## Check-In System

### Visitor Check-In Process

**Self-Service Kiosk:**
1. Visitor arrives at kiosk
2. Scan QR code or enter details
3. Take photo (if required)
4. Review and sign agreements
5. Print visitor badge
6. Host receives notification

**Reception Check-In:**
1. Receptionist searches appointment
2. Verify visitor identity
3. Capture photo and signature
4. Print visitor badge
5. Assign locker (if needed)
6. Escort or notify host

**Walk-In Check-In:**
1. No prior appointment
2. Enter visitor details
3. Select host or department
4. Get approval (if required)
5. Complete check-in process

### Badge Management

**Badge Information:**
- Visitor name and photo
- Host name
- Department
- Visit date and time
- Badge number
- Expiry time
- QR code
- Access level

**Badge Types:**
- Standard visitor badge
- Contractor badge
- VIP badge
- Temporary employee badge

**Badge Printing:**
- Thermal printer support
- Custom templates
- Multi-language support
- Photo integration

### Security Screening

**Pre-Arrival Screening:**
- Background check integration
- Watchlist verification
- Document verification
- Risk assessment

**On-Arrival Screening:**
- ID verification
- Metal detection (if hardware integrated)
- Bag screening
- Health screening (temperature check)

**Clearance Levels:**
- Public areas only
- Escorted access
- Restricted area access
- Full facility access

### Check-Out Process

**Automatic Check-Out:**
- Based on appointment end time
- Configurable grace period
- Automatic badge deactivation

**Manual Check-Out:**
1. Visitor returns to reception
2. Scan badge or enter details
3. Return visitor badge
4. Return locker key (if used)
5. Complete checkout
6. Update system

**Overdue Notifications:**
- Alert security
- Notify host
- Send reminder to visitor
- Escalate if needed

## Workflow Configuration

### Approval Workflows

**Workflow Components:**
- Trigger conditions
- Approval levels
- Timeout settings
- Escalation rules
- Notification templates

**Common Workflows:**

**Standard Approval:**
- Host creates appointment
- Department head approves
- Visitor notified

**High-Security Approval:**
- Host creates appointment
- Department head reviews
- Security approves
- Facility manager approves
- Visitor notified

**Auto-Approval:**
- Specific visitor categories
- Regular contractors
- Whitelisted companies
- Immediate confirmation

### Creating Custom Workflows

1. Navigate to Workflows
2. Click "Create Workflow"
3. Define workflow name
4. Set trigger conditions:
   - Visitor type
   - Duration threshold
   - Access level
   - Department
5. Add approval steps:
   - Select approvers
   - Set timeout
   - Define escalation
6. Configure notifications
7. Save and activate

### Workflow Management

**Workflow States:**
- Active
- Inactive
- Draft
- Archived

**Workflow Actions:**
- Edit workflow
- Duplicate workflow
- Test workflow
- View usage statistics
- Deactivate/activate

## Settings and Configuration

### General Settings

**System Configuration:**
- Facility information
- Business hours
- Time zones
- Default visit duration
- Check-in/out grace periods
- Badge validity duration

**Notification Settings:**
- Email templates
- SMS templates (if configured)
- Notification timing
- Recipient rules
- Language preferences

### Visitor Categories

**Define Categories:**
- Vendor
- Contractor
- Guest
- Interviewee
- Delivery
- Government Official
- VIP

**Category Properties:**
- Approval required
- Default duration
- Access level
- Required documents
- Badge template
- Workflow assignment

### Location Management

**Facility Locations:**
- Buildings
- Floors
- Rooms
- Parking areas
- Meeting rooms
- Restricted zones

**Location Properties:**
- Name and description
- Capacity
- Access requirements
- Available amenities
- Map/directions

### Host Management

**Host Registration:**
- All employees can be hosts
- Department assignment
- Contact information
- Default meeting location
- Delegation settings

**Host Responsibilities:**
- Create appointments
- Approve visitor access
- Escort visitors
- Ensure check-out
- Report incidents

### Agreement Templates

**Document Types:**
- NDA (Non-Disclosure Agreement)
- Visitor policy acknowledgment
- Safety guidelines
- Photo release
- Health declaration

**Template Management:**
- Create/edit templates
- Multi-language support
- Digital signature fields
- Required vs. optional
- Version control

## Reports and Analytics

### Dashboard Analytics

**Real-Time Metrics:**
- Visitors today
- Currently on-site
- Peak hours
- Average visit duration
- No-show rate
- Check-in efficiency

**Historical Trends:**
- Visitor volume over time
- Popular visiting days/times
- Busiest hosts
- Common purposes
- Department activity

### Available Reports

**Visitor Reports:**
- Daily visitor log
- Visitor by company
- Visitor by purpose
- Repeat visitors
- VIP visitors
- Overdue visitors

**Appointment Reports:**
- Scheduled vs. actual
- Approval turnaround time
- Cancellation reasons
- No-show analysis
- Walk-in vs. scheduled

**Security Reports:**
- Access log
- Security incidents
- Watchlist matches
- After-hours visits
- Unauthorized areas

**Host Reports:**
- Appointments by host
- Host responsiveness
- Average meeting duration
- Most active hosts
- Department statistics

**Compliance Reports:**
- NDA compliance
- Health screening log
- Document verification log
- Audit trail
- Badge usage

### Generating Reports

1. Navigate to Reports section
2. Select report type
3. Set parameters:
   - Date range
   - Filters (host, department, visitor type)
   - Grouping options
4. Preview report
5. Choose format (PDF, Excel, CSV)
6. Download or email
7. Schedule recurring reports (optional)

### Export Options

**Data Export:**
- Visitor database
- Appointment history
- Check-in/out logs
- Compliance records
- Analytics data

**Export Formats:**
- PDF - Formatted reports
- Excel - Data analysis
- CSV - Data import/export
- JSON - API integration

## User Permissions

### Module Access

Users must be assigned VMS module access:
- Admin assigns module in user settings
- Module ID: 3
- Access controlled via `modules` field

### VMS Permissions

**Permission Levels:**

**Receptionist:**
- Check in/out visitors
- View appointments
- Print badges
- Update visitor status

**Host:**
- Create appointments
- Manage own appointments
- Check in visitors
- View visitor history

**Approver:**
- Approve appointments
- Override check-ins
- View all appointments
- Generate reports

**Administrator:**
- Full system access
- Configure workflows
- Manage settings
- Access all reports
- User management

### Department Permissions

**Department-Level Access:**
- View department appointments only
- Approve department visitors
- Department reports
- Department settings

## Best Practices

### Appointment Management

1. **Schedule in Advance**
   - Encourage pre-registration
   - Allow time for approvals
   - Send reminders
   - Update if changes occur

2. **Provide Complete Information**
   - Full visitor details
   - Purpose of visit
   - Special requirements
   - Expected duration

3. **Manage No-Shows**
   - Track no-show patterns
   - Follow up with hosts
   - Consider penalties for repeat no-shows
   - Update appointment status

### Check-In Process

1. **Streamline Check-In**
   - Use QR codes
   - Pre-fill information
   - Minimize wait time
   - Clear signage

2. **Security First**
   - Verify identity
   - Check watchlists
   - Scan documents
   - Issue appropriate badges

3. **Host Accountability**
   - Notify hosts promptly
   - Set response time limits
   - Escalate if host unavailable
   - Ensure proper check-out

### Compliance and Security

1. **Document Everything**
   - Capture visitor photos
   - Digital signatures
   - Agreement acceptance
   - Access logs

2. **Regular Audits**
   - Review access logs
   - Check compliance
   - Verify procedures
   - Update policies

3. **Privacy Protection**
   - Secure visitor data
   - Limit data retention
   - Control access
   - Comply with regulations (GDPR, etc.)

### System Management

1. **Regular Maintenance**
   - Update workflows
   - Review settings
   - Clean old data
   - Test integrations

2. **User Training**
   - Train receptionists
   - Educate hosts
   - Security awareness
   - System updates

3. **Monitor Performance**
   - Check-in times
   - Approval turnaround
   - System uptime
   - User satisfaction

## Common Tasks

### Handling Walk-In Visitors

1. Welcome visitor
2. Create new appointment
3. Enter visitor details
4. Contact host or get approval
5. Complete security screening
6. Issue visitor badge
7. Escort or provide directions
8. Log check-in

### Managing VIP Visitors

1. Create VIP appointment
2. Tag as VIP category
3. Fast-track approval
4. Assign senior host
5. Prepare welcome materials
6. Notify relevant staff
7. Priority check-in
8. Enhanced service

### Handling Contractors

1. Create recurring appointment
2. Set contract duration
3. Assign long-term badge
4. Configure auto-approval
5. Set access restrictions
6. Regular review dates
7. Monitor compliance
8. Revoke on completion

### Emergency Evacuation

1. Access real-time visitor list
2. Export current visitors
3. Print evacuation list
4. Verify all checked out
5. Account for all visitors
6. Report to emergency services
7. Log incident
8. Post-incident review

## Troubleshooting

### Visitor Cannot Check In

**Possible Causes:**
- No appointment found
- Appointment not approved
- Expired QR code
- Wrong date/time

**Solutions:**
- Verify appointment details
- Check approval status
- Create walk-in appointment
- Contact host

### Badge Not Printing

**Possible Causes:**
- Printer offline
- Paper jam
- Template issue
- Connection problem

**Solutions:**
- Check printer status
- Clear paper jam
- Restart printer
- Use backup printer
- Manual badge creation

### Host Not Notified

**Possible Causes:**
- Incorrect email
- Notification settings
- Email delivery issue
- Spam filter

**Solutions:**
- Verify host email
- Check notification settings
- Resend notification
- Use alternate contact method

## Integration Possibilities

### Access Control Integration

- Automatic badge activation
- Access level assignment
- Real-time access tracking
- Automatic deactivation

### Calendar Integration

- Sync with Outlook/Google Calendar
- Room booking integration
- Host availability checking
- Meeting reminders

### HR System Integration

- Employee verification
- Department sync
- Contact information
- Authorization levels

### Parking Management

- Assign parking spots
- Generate parking passes
- Monitor parking usage
- Parking availability

## Related Documentation

- [Installation Guide](INSTALLATION.md)
- [Configuration Guide](CONFIGURATION.md)
- [API Documentation](API.md)
- [User Manual (PDF)](../public/usermanual_vms.pdf)

## Support

For additional help with VMS module:
- Review user manual PDF
- Contact system administrator
- Submit support ticket
- Check troubleshooting guide
