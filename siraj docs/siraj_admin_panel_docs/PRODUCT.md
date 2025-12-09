# Siraj Admin Panel - Product Documentation

## Table of Contents

- [Product Overview](#product-overview)
- [User Roles and Permissions](#user-roles-and-permissions)
- [Feature Documentation](#feature-documentation)
- [User Workflows](#user-workflows)
- [Business Logic](#business-logic)
- [Data Models](#data-models)
- [UI/UX Guidelines](#uiux-guidelines)

## Product Overview

Siraj Admin Panel is a comprehensive administrative dashboard designed for managing the Siraj career guidance and education platform. It serves as the central hub for administrators to manage all aspects of the platform, including users, educational content, job opportunities, advisory services, and subscription products.

### Target Users

- **Platform Administrators**: Full access to all features and management capabilities
- **Content Managers**: Manage educational content (universities, programs)
- **Support Staff**: Handle user inquiries and session management

### Core Value Proposition

- **Centralized Management**: Single interface for all platform operations
- **Efficient Workflows**: Streamlined processes for common administrative tasks
- **Real-time Updates**: Immediate reflection of changes across the platform
- **Multi-currency Support**: Handle global pricing in USD and regional pricing in JOD
- **Rich Content Editing**: HTML-based feature descriptions with WYSIWYG editor

## User Roles and Permissions

### Administrator
- Full access to all features
- Can create, read, update, and delete all resources
- Manage user accounts and permissions
- Configure platform settings and products

### Content Manager
- Manage universities and programs
- Update educational content
- Review and approve submissions
- Limited access to user management

### Support Staff
- View user information
- Manage sessions and bookings
- Handle retake requests
- Limited modification capabilities

## Feature Documentation

### 1. Dashboard Home

**Purpose**: Landing page providing overview of platform activity

**Components**:
- Navigation sidebar with all management modules
- Header with user information and logout option
- Content area that switches based on selected menu item

**User Actions**:
- Select management module from sidebar
- View current admin user information
- Logout from the system

### 2. Student Management

**Purpose**: Manage student accounts and track their activity on the platform

**Key Features**:
- View list of all registered students
- Search and filter students by various criteria
- View detailed student profiles
- Monitor student engagement metrics
- Track student sessions and job trials

**Data Displayed**:
- Student name and contact information
- Registration date
- Account status (active, inactive, deleted)
- Number of booked sessions
- Job trial participation
- Last login date

**Actions Available**:
- View student details
- Update student information
- Suspend or activate accounts
- View student activity history

### 3. Advisor Management

**Purpose**: Manage advisor profiles and their availability on the platform

**Key Features**:
- View and manage all advisors
- Add new advisors to the platform
- Update advisor profiles and specializations
- Manage advisor availability and schedules
- Track advisor performance metrics

**Data Displayed**:
- Advisor name and credentials
- Areas of expertise
- Available time slots
- Number of completed sessions
- Average rating (if applicable)
- Account status

**Actions Available**:
- Add new advisor
- Edit advisor profile
- Manage time slot availability
- View session history
- Activate/deactivate advisor accounts

### 4. University Management

**Purpose**: Maintain comprehensive database of universities and their information

**Key Features**:
- Add and manage university profiles
- Update admission requirements
- Maintain contact information
- Manage university rankings and statistics
- Track programs offered by each university

**Data Displayed**:
- University name and logo
- Location and country
- Admission requirements
- Application deadlines
- Contact information
- Number of programs offered
- Rankings and ratings

**Actions Available**:
- Add new university
- Edit university details
- Upload university logos and images
- Manage program associations
- Delete or archive universities

**Business Rules**:
- University names must be unique
- At least one contact method required
- Programs can be associated with multiple universities

### 5. Program Management

**Purpose**: Manage academic programs and their details

**Key Features**:
- Create and edit program listings
- Define program requirements and prerequisites
- Set tuition fees and duration
- Associate programs with universities
- Categorize by major/field of study

**Data Displayed**:
- Program name and degree level
- Associated university
- Major/field of study
- Duration and credits
- Tuition fees
- Admission requirements
- Application deadlines

**Actions Available**:
- Create new program
- Edit program details
- Link to university
- Set prerequisites
- Update fees and requirements

### 6. Product Management

**Purpose**: Configure subscription products that students can purchase

**Key Features**:
- Define product tiers (Basic, Premium, etc.)
- Set pricing in multiple currencies (USD and JOD)
- Configure product features using rich text editor
- Define session allocations per product
- Set job trial experience counts
- Toggle job trial eligibility

**Data Displayed**:
| Field | Description |
|-------|-------------|
| Title | Product name (e.g., "Premium Package") |
| Features | HTML-formatted list of features |
| Price in USD | Price in US Dollars |
| Price in Jordan | Price in Jordanian Dinars |
| Total Sessions | Number of advisory sessions included |
| Total Job Trial Exps | Number of job trial experiences included |
| Is Job Trial | Boolean flag for job trial eligibility |
| Updated At | Last modification timestamp |

**Actions Available**:
- Edit product details
- Update pricing
- Modify features (with rich text editor)
- Adjust session allocations
- Enable/disable job trial access

**Business Rules**:
- All fields are required
- Prices must be positive numbers
- Total sessions must be at least 1
- Total job trial experiences must be at least 1
- Features support HTML formatting for rich display

**Example Product Configuration**:
```
Title: Premium Career Package
Price in USD: 299
Price in Jordan: 210
Total Sessions: 10
Total Job Trial Exps: 3
Is Job Trial: true
Features: 
  <ul>
    <li>10 one-on-one advisory sessions</li>
    <li>3 job trial experiences</li>
    <li>Career assessment and planning</li>
    <li>Resume review and optimization</li>
    <li>Priority support</li>
  </ul>
```

### 7. Company Management

**Purpose**: Manage companies offering job opportunities and partnerships

**Key Features**:
- Add and manage company profiles
- Track company partnerships
- Manage job postings
- Monitor job trial offerings
- Store company contact information

**Data Displayed**:
- Company name and logo
- Industry and size
- Location
- Contact information
- Active job postings
- Job trials offered
- Partnership status

**Actions Available**:
- Add new company
- Edit company profile
- Manage job postings
- Update partnership status
- View job trial history

### 8. Job Trial Management

**Purpose**: Manage job trial opportunities and student participation

**Key Features**:
- Create and publish job trials
- Define trial requirements and duration
- Track student applications
- Monitor trial progress and completion
- Manage feedback and evaluations

**Data Displayed**:
- Job trial title and description
- Company offering the trial
- Requirements and qualifications
- Duration and time commitment
- Number of applicants
- Number of participants
- Completion rate

**Actions Available**:
- Create new job trial
- Edit trial details
- Approve/reject applications
- Monitor participant progress
- Close or extend trials

### 9. Booked Sessions Management

**Purpose**: Monitor and manage all advisory sessions scheduled on the platform

**Key Features**:
- View all scheduled sessions
- Filter by date, advisor, student
- Track session status (upcoming, completed, cancelled)
- Handle rescheduling requests
- Monitor no-shows

**Data Displayed**:
- Student and advisor names
- Session date and time
- Session type (career guidance, university selection, etc.)
- Status (scheduled, completed, cancelled, no-show)
- Duration
- Notes or feedback

**Actions Available**:
- View session details
- Reschedule sessions (if permitted)
- Cancel sessions
- View session notes
- Generate session reports

### 10. Time Slot Management

**Purpose**: Configure available time slots for advisors

**Key Features**:
- Create individual time slots
- Set up recurring schedules (daily/weekly)
- Define slot duration
- Manage advisor availability
- Handle time zone considerations

**Data Displayed**:
- Advisor name
- Date and time
- Duration
- Availability status (available, booked, blocked)
- Recurring pattern (if applicable)

**Actions Available**:
- Create single time slot
- Create recurring slots (daily/weekly)
- Edit time slot details
- Delete time slots
- Block specific times

**Recurring Schedule Options**:
- **Daily**: Same time every day for specified date range
- **Weekly**: Same day/time every week for specified date range

### 11. Coupon Management

**Purpose**: Create and manage promotional discount coupons

**Key Features**:
- Generate coupon codes
- Set discount values (percentage or fixed amount)
- Define expiration dates
- Limit usage count
- Track redemption history

**Data Displayed**:
- Coupon code
- Discount type and value
- Valid from/to dates
- Maximum uses
- Current usage count
- Status (active, expired, depleted)

**Actions Available**:
- Create new coupon
- Edit coupon details
- Deactivate coupon
- View redemption history
- Generate coupon report

**Business Rules**:
- Coupon codes must be unique
- Discount value must be valid (0-100% for percentage)
- End date must be after start date
- Cannot modify used coupons (only deactivate)

### 12. Crawling Job Management

**Purpose**: Monitor and manage automated web crawling operations

**Key Features**:
- View active crawling jobs
- Monitor crawl progress
- Review collected data
- Configure crawl parameters
- Handle errors and retries

**Data Displayed**:
- Job ID and name
- Target URL or domain
- Status (running, completed, failed, paused)
- Start time and duration
- Records collected
- Error messages

**Actions Available**:
- Start new crawl job
- Pause/resume jobs
- Stop running jobs
- View crawled data
- Configure crawl settings
- Review error logs

### 13. Job Application Management

**Purpose**: Review and manage student applications for job opportunities

**Key Features**:
- View all job applications
- Filter by status, company, student
- Review application materials
- Update application status
- Communicate with applicants

**Data Displayed**:
- Student name and profile
- Job/company applied to
- Application date
- Status (pending, reviewed, accepted, rejected)
- Resume and cover letter
- Additional materials

**Actions Available**:
- Review application details
- Update application status
- Add notes or comments
- Forward to company
- Bulk status updates

### 14. Retake Request Management

**Purpose**: Handle student requests to retake assessments or sessions

**Key Features**:
- View all retake requests
- Review request justifications
- Approve or reject requests
- Track retake history
- Set retake conditions

**Data Displayed**:
- Student name
- Original assessment/session
- Request date
- Reason for retake
- Status (pending, approved, rejected)
- Number of previous retakes

**Actions Available**:
- Approve retake request
- Reject with reason
- View original assessment results
- Set conditions for retake
- Track retake outcomes

**Business Rules**:
- Students must provide valid reason
- Limit on number of retakes per assessment
- Minimum waiting period between attempts
- Original results preserved

## User Workflows

### Workflow 1: Adding a New University

1. Navigate to University Management
2. Click "Add University" button
3. Fill in university details:
   - Name
   - Location/Country
   - Contact information
   - Logo upload
4. Add admission requirements
5. Set application deadlines
6. Save university
7. Associate relevant programs

### Workflow 2: Creating a Product

1. Navigate to Product Management
2. Select existing product to edit (no "Add New" - products pre-exist)
3. Update product title
4. Set price in USD
5. Set price in Jordan Dinars
6. Configure session allocation
7. Set job trial experience count
8. Toggle job trial eligibility
9. Edit features using rich text editor
10. Save changes

### Workflow 3: Managing a Booked Session

1. Navigate to Booked Sessions
2. Filter by date or advisor
3. Select session to manage
4. View session details (student, advisor, time)
5. Take action:
   - Confirm session
   - Reschedule (if needed)
   - Cancel (with reason)
   - Add notes
6. Save changes

### Workflow 4: Processing a Job Trial Application

1. Navigate to Job Trial Management
2. View list of job trials
3. Select specific job trial
4. Review applicant list
5. For each applicant:
   - Review profile and qualifications
   - Check eligibility (product includes job trials)
   - Approve or reject application
6. Notify approved applicants
7. Monitor trial progress

## Business Logic

### Product Eligibility Logic

```
Student can access job trials IF:
  - Student has active subscription
  - Product includes job trials (isJobTrial = true)
  - Student has remaining job trial experiences (totalJobTrialExps > used)
```

### Session Booking Logic

```
Session can be booked IF:
  - Student has active subscription
  - Product includes sessions (totalSessions > 0)
  - Student has remaining sessions (totalSessions > used)
  - Time slot is available
  - Advisor is available at that time
```

### Coupon Application Logic

```
Coupon can be applied IF:
  - Coupon code is valid
  - Current date is between valid from/to dates
  - Usage count < maximum uses (if limit set)
  - Product is eligible for coupon (if restrictions apply)
```

### Time Slot Availability

```
Time slot is available IF:
  - Status = available
  - No existing booking for that slot
  - Slot time is in the future
  - Advisor is not blocked during that time
```

## Data Models

### Product Model

```javascript
{
  id: number,
  title: string,
  features: string (HTML),
  priceInUSD: number,
  priceInJordan: number,
  totalSessions: number,
  totalJobTrialExps: number,
  isJobTrial: boolean,
  updatedAt: timestamp,
  createdAt: timestamp
}
```

### University Model

```javascript
{
  id: number,
  name: string,
  location: string,
  country: string,
  contactEmail: string,
  contactPhone: string,
  website: string,
  logoUrl: string,
  admissionRequirements: string,
  applicationDeadline: date,
  ranking: number,
  status: string,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### Session Model

```javascript
{
  id: number,
  studentId: number,
  advisorId: number,
  timeSlotId: number,
  date: datetime,
  duration: number,
  type: string,
  status: string,
  notes: string,
  feedback: string,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### Job Trial Model

```javascript
{
  id: number,
  title: string,
  description: string,
  companyId: number,
  requirements: string,
  duration: number,
  startDate: date,
  endDate: date,
  maxParticipants: number,
  status: string,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

## UI/UX Guidelines

### Design Principles

1. **Consistency**: Use Ant Design components consistently across all pages
2. **Clarity**: Clear labels and instructions for all actions
3. **Feedback**: Provide success/error notifications for all operations
4. **Efficiency**: Minimize clicks required for common tasks
5. **Accessibility**: Ensure keyboard navigation and screen reader support

### Color Scheme

- **Primary Color**: #00B4DE (Blue) - used for primary actions and highlights
- **Success**: Green - successful operations
- **Warning**: Orange - warnings and cautions
- **Error**: Red - errors and destructive actions
- **Neutral**: Grays - text and borders

### Component Usage

- **Tables**: Display lists of resources with sortable columns
- **Modals**: Edit forms and detailed views
- **Forms**: Ant Design Form components with validation
- **Buttons**: Primary for main action, default for secondary
- **Notifications**: Toast notifications for operation feedback

### Responsive Behavior

- **Desktop**: Full sidebar navigation with expanded content area
- **Tablet**: Collapsible sidebar, optimized table layouts
- **Mobile**: Bottom navigation, stacked form fields (if applicable)

### Loading States

- **Skeleton loaders** for initial page loads
- **Spinner overlays** for data operations
- **Progress indicators** for long-running operations
- **Disabled states** for unavailable actions

### Error Handling

- **Inline validation** for form fields
- **Error notifications** for failed operations
- **Retry options** for network errors
- **Fallback UI** for missing data

---

## Version History

- **v0.1.0** - Initial product documentation
- Current features documented as of December 2025

For technical implementation details, see [README.md](./README.md) and [API.md](./API.md).
