# Features Documentation

## Table of Contents

- [Overview](#overview)
- [Doctor Management](#doctor-management)
- [Patient Management](#patient-management)
- [Lab Management](#lab-management)
- [Content Management](#content-management)
- [Session Management](#session-management)
- [Financial Management](#financial-management)
- [User Feedback](#user-feedback)
- [Settings & Administration](#settings--administration)
- [Policy Management](#policy-management)

## Overview

DocLink CMS provides a comprehensive suite of features for managing a healthcare platform. This document details each feature, its purpose, and how to use it.

## Doctor Management

### 1. Doctor Profiles

**Purpose**: Manage doctor accounts, credentials, and professional information.

**Features**:
- View all registered doctors in a searchable, filterable table
- Add new doctor profiles with complete information
- Edit existing doctor information
- Delete or deactivate doctor accounts
- View detailed doctor profiles
- Upload and manage doctor documents
- Profile verification status tracking

**Key Fields**:
- Personal Information (Name, Email, Phone)
- Professional Details (Specialization, Experience, Qualifications)
- Registration Details (License Number, Registration Date)
- Profile Picture and Documents
- Verification Status
- Activity Status (Active/Inactive)

**Access Path**: Dashboard → Doctors → Profiles

### 2. Doctor Requests

**Purpose**: Review and approve/reject doctor registration requests.

**Features**:
- View pending doctor registration requests
- Review submitted documents and credentials
- Approve or reject applications
- Request additional information
- Track application status
- Bulk operations for multiple requests

**Workflow**:
1. New doctor submits registration
2. Admin reviews application
3. Verify credentials and documents
4. Approve or request changes
5. Doctor profile is activated

**Access Path**: Dashboard → Doctors → Requests

### 3. Specializations

**Purpose**: Manage medical specializations available in the platform.

**Features**:
- Add new medical specializations
- Edit specialization details
- Delete unused specializations
- Upload specialization icons/images
- Set specialization descriptions
- View doctors by specialization

**Common Specializations**:
- Cardiology
- Dermatology
- Pediatrics
- Orthopedics
- Neurology
- General Medicine
- And more...

**Access Path**: Dashboard → Doctors → Specializations

### 4. Disease Management

**Purpose**: Maintain a database of diseases and health conditions.

**Features**:
- Add new diseases and conditions
- Categorize diseases
- Link diseases to specializations
- Edit disease information
- Delete obsolete entries
- Search and filter diseases

**Use Cases**:
- Doctor profile tagging
- Patient condition tracking
- Search and filter functionality
- Health content categorization

**Access Path**: Dashboard → Doctors → Disease

### 5. Health Concerns

**Purpose**: Manage common health concerns and symptoms.

**Features**:
- Add health concern categories
- Edit concern descriptions
- Link concerns to specializations
- Enable patient self-assessment
- Track trending health concerns

**Examples**:
- Back Pain
- Headache
- Fever
- Skin Problems
- Digestive Issues

**Access Path**: Dashboard → Doctors → Health Concerns

### 6. Subscriptions

**Purpose**: Manage doctor subscription plans and pricing.

**Features**:
- Create subscription tiers
- Set pricing and billing cycles
- Define subscription benefits
- Track active subscriptions
- Manage renewals and cancellations
- View subscription analytics

**Subscription Types**:
- Free Trial
- Basic Plan
- Professional Plan
- Premium Plan
- Enterprise Plan

**Access Path**: Dashboard → Doctors → Subscriptions

### 7. Subscription Features

**Purpose**: Define features available in each subscription tier.

**Features**:
- Add/edit subscription features
- Assign features to subscription tiers
- Set feature limits (e.g., consultations per month)
- Enable/disable features
- Track feature usage

**Common Features**:
- Number of video consultations
- Chat support
- Profile visibility boost
- Analytics dashboard access
- Priority support
- Custom branding

**Access Path**: Dashboard → Doctors → Subscription Features

### 8. Doctor Connections

**Purpose**: Manage relationships between doctors and patients.

**Features**:
- View active doctor-patient connections
- Track consultation history
- Monitor connection quality
- Manage connection requests
- View connection analytics

**Access Path**: Dashboard → Doctors → Connections

### 9. Reviews & Ratings

**Purpose**: Manage patient reviews and ratings for doctors.

**Features**:
- View all reviews and ratings
- Moderate inappropriate reviews
- Respond to reviews (as admin)
- Flag/remove spam or abusive reviews
- View rating statistics
- Generate rating reports

**Moderation Actions**:
- Approve review
- Flag for review
- Hide review
- Delete review
- Contact reviewer

**Access Path**: Dashboard → Doctors → Reviews & Ratings

## Patient Management

### Patient Profiles

**Purpose**: Manage patient accounts and health information.

**Features**:
- View all registered patients
- Search and filter patients
- View patient details
- Edit patient information
- Deactivate/delete accounts
- View patient activity history
- Track consultations and appointments

**Key Information**:
- Personal Details
- Contact Information
- Health History
- Active Conditions
- Consultation History
- Subscription Status

**Access Path**: Dashboard → Patients → Profiles

## Lab Management

### 1. Lab Profiles

**Purpose**: Manage laboratory and diagnostic center profiles.

**Features**:
- Add new lab profiles
- Edit lab information
- View lab details
- Manage lab services
- Upload lab certifications
- Set lab operating hours
- Track lab performance

**Lab Information**:
- Lab Name and Address
- Contact Details
- Certifications
- Available Tests
- Service Categories
- Pricing
- Operating Hours

**Access Path**: Dashboard → Masters → Labs

### 2. Lab Service Categories

**Purpose**: Organize lab services into categories.

**Features**:
- Create service categories
- Edit category details
- Add category icons
- Link tests to categories
- View category-wise services

**Example Categories**:
- Blood Tests
- Imaging (X-Ray, MRI, CT)
- Pathology
- Microbiology
- Biochemistry

**Access Path**: Dashboard → Masters → Lab Service Category

### 3. Lab Test Categories

**Purpose**: Manage specific lab test types.

**Features**:
- Add new test types
- Edit test details
- Set test pricing
- Define test requirements
- Link to parent categories
- Manage test availability

**Example Tests**:
- Complete Blood Count (CBC)
- Lipid Profile
- Thyroid Function Test
- Liver Function Test
- Kidney Function Test

**Access Path**: Dashboard → Masters → Lab Test Category

## Content Management

### 1. Blogs

**Purpose**: Create and manage healthcare blog content.

**Features**:
- Rich text editor for content creation
- Add images and media
- Categorize blogs
- Tag blogs for better discovery
- Schedule blog publication
- SEO optimization
- View/edit/delete blogs
- Track blog analytics

**Blog Fields**:
- Title
- Category
- Author
- Content (HTML)
- Featured Image
- Tags
- Publish Date
- Status (Draft/Published)

**Access Path**: Dashboard → Blogs → List

### 2. Blog Categories

**Purpose**: Organize blogs into categories.

**Features**:
- Create blog categories
- Edit category details
- Delete categories
- View blogs by category

**Example Categories**:
- Health Tips
- Disease Information
- Lifestyle
- Nutrition
- Mental Health

**Access Path**: Dashboard → Blogs → Category

### 3. Health Tips

**Purpose**: Quick health tips and advice for users.

**Features**:
- Add short health tips
- Categorize tips
- Schedule tip display
- Track tip engagement
- Edit/delete tips

**Use Cases**:
- Daily health tips
- Seasonal health advice
- Preventive care tips
- Wellness suggestions

**Access Path**: Dashboard → Masters → Health Tips

### 4. Banners

**Purpose**: Manage promotional banners for the application.

**Features**:
- Upload banner images
- Set banner links
- Schedule banner display
- Assign banners to screens
- Set banner priority/order
- Enable/disable banners
- Track banner clicks

**Banner Configuration**:
- Image upload
- Target screen
- Click action/link
- Display duration
- Priority/position
- Active status

**Access Path**: Dashboard → Masters → Banner

### 5. Screens

**Purpose**: Define application screens for content management.

**Features**:
- Add application screens
- Edit screen details
- Link content to screens
- Manage screen layouts

**Common Screens**:
- Home Screen
- Doctor Listing
- Search Results
- Profile Screen
- Blog Listing

**Access Path**: Dashboard → Masters → Screens

### 6. Short Messages

**Purpose**: Quick messages and notifications for users.

**Features**:
- Create short messages
- Schedule message delivery
- Target specific user groups
- Track message engagement
- Edit/delete messages

**Access Path**: Dashboard → Masters → Short Message

### 7. Short Stories

**Purpose**: Brief health stories and case studies.

**Features**:
- Add short stories
- Rich media support
- Categorize stories
- Feature stories
- Track story views

**Access Path**: Dashboard → Masters → Short Stories

### 8. Doctor Directory

**Purpose**: Curated directory of featured doctors.

**Features**:
- Add doctors to directory
- Set directory categories
- Feature top doctors
- Manage directory listings
- Set display order

**Access Path**: Dashboard → Masters → Doctor Directories

## Session Management

### Active Sessions

**Purpose**: Monitor ongoing consultation sessions.

**Features**:
- View all active sessions
- Session details (doctor, patient, duration)
- Session status tracking
- Emergency intervention capability
- Session analytics

### Chat Request Sessions

**Purpose**: Manage chat consultation requests.

**Features**:
- View pending chat requests
- Assign chats to doctors
- Monitor chat sessions
- Track response times
- Chat history access

## Financial Management

### 1. Top-ups

**Purpose**: Manage user wallet top-ups and recharges.

**Features**:
- View top-up transactions
- Track payment methods
- Process refunds
- Generate top-up reports
- Monitor failed transactions

### 2. Transactions

**Purpose**: Track all financial transactions.

**Features**:
- View transaction history
- Filter by type, user, date
- Transaction status tracking
- Export transaction reports
- Reconciliation tools

**Transaction Types**:
- Consultation fees
- Subscription payments
- Wallet top-ups
- Refunds
- Commissions

### 3. Settlements

**Purpose**: Manage payments to doctors and labs.

**Features**:
- Calculate doctor payouts
- Process settlements
- Track settlement status
- Generate settlement reports
- Manage payout schedules

## User Feedback

### 1. Report a Problem

**Purpose**: Manage user-reported issues and problems.

**Features**:
- View all problem reports
- Categorize issues
- Assign to support team
- Track resolution status
- Respond to reports
- Close resolved issues

**Issue Categories**:
- Technical Issues
- Payment Problems
- Doctor Concerns
- App Bugs
- Feature Requests

### 2. Session Feedback

**Purpose**: Collect and manage consultation feedback.

**Features**:
- View session feedback
- Ratings and comments
- Doctor performance tracking
- Issue identification
- Quality improvement insights

## Settings & Administration

### 1. Role Management

**Purpose**: Define and manage user roles.

**Features**:
- Create custom roles
- Edit role details
- Assign permissions to roles
- Delete unused roles
- View users by role

**Default Roles**:
- Super Admin
- Admin
- Content Manager
- Support Staff
- Finance Manager

**Access Path**: Dashboard → Settings → Role Management

### 2. Permissions

**Purpose**: Control access to features and data.

**Features**:
- Define permission sets
- Assign permissions to roles
- Granular access control
- View permission matrix
- Audit permission changes

**Permission Types**:
- Read
- Write
- Delete
- Approve
- Export

**Access Path**: Dashboard → Settings → Permissions

### 3. Add User

**Purpose**: Create new admin/staff accounts.

**Features**:
- Add new users
- Assign roles
- Set permissions
- Configure access level
- Send invitation emails

**Access Path**: Dashboard → Settings → Add User

### 4. Module Management

**Purpose**: Manage application modules and features.

**Features**:
- Enable/disable modules
- Configure module settings
- View module usage
- Manage module access

**Access Path**: Dashboard → Modules Management → Modules

## Policy Management

### 1. Terms & Conditions

**Purpose**: Manage platform terms and conditions.

**Features**:
- Edit terms and conditions
- Version control
- Publish updates
- Track user acceptance

**Access Path**: Dashboard → Settings → Terms & Conditions

### 2. Payout Policies Master

**Purpose**: Define payout rules and policies.

**Features**:
- Create payout policies
- Set commission rates
- Define payout schedules
- Configure payment methods
- Manage policy versions

**Access Path**: Dashboard → Policies → Payout Policies Master

### 3. Payout Policies Requests

**Purpose**: Handle doctor payout policy requests.

**Features**:
- View policy change requests
- Review request details
- Approve/reject requests
- Track request status
- Communication with doctors

**Access Path**: Dashboard → Policies → Payout Policies Requests

## Support Features

### Support Team

**Purpose**: Manage customer support team members.

**Features**:
- Add support staff
- Assign support areas
- Track support performance
- Manage availability
- View support statistics

**Access Path**: Dashboard → Masters → Support Team

### Support Team Status

**Purpose**: Manage support team availability status types.

**Features**:
- Define status types
- Set status colors/indicators
- Manage status descriptions

**Status Types**:
- Available
- Busy
- Away
- Offline

**Access Path**: Dashboard → Masters → Support Team Status

## Additional Features

### Video Call Packages

**Purpose**: Manage video consultation package pricing.

**Features**:
- Create call packages
- Set package pricing
- Define call duration
- Manage package features
- Track package sales

**Access Path**: Dashboard → Masters → Video Call Packages

### Search Filters

**Purpose**: Configure search and filter options.

**Features**:
- Add filter categories
- Define filter values
- Enable/disable filters
- Set filter hierarchy
- Manage filter display

**Access Path**: Dashboard → Masters → Search Filters

### Actions

**Purpose**: Manage system actions and workflows.

**Features**:
- Define action types
- Configure workflows
- Set action permissions
- Track action logs

**Access Path**: Dashboard → Masters → Actions

---

Each feature is designed to provide maximum flexibility and control while maintaining ease of use. For detailed usage instructions, refer to the [USER_GUIDE.md](./USER_GUIDE.md).
