# Axis Pro App - Comprehensive Documentation

## Overview
This directory contains comprehensive documentation for all features and modules of the Axis Pro application. Axis Pro is an invoicing and scheduling application designed to help professionals manage clients, appointments, invoices, and business operations.

## Documentation Structure

The documentation is organized by feature/module, with each module having its own dedicated folder containing detailed documentation:

### 1. [Authentication Module](./01-Authentication/Authentication-Module-Documentation.md)
Complete documentation for user authentication, login, signup, logout, password recovery, and session management.

**Key Features:**
- User login and authentication
- User registration
- Password recovery
- Password change
- Session management
- Role-based access control

### 2. [Dashboard Module](./02-Dashboard/Dashboard-Module-Documentation.md)
Comprehensive guide to the dashboard, KPIs, recent activity, weekly earnings, and invoice summaries.

**Key Features:**
- Key Performance Indicators (KPIs)
- Recent activity feed
- Weekly earnings chart
- Summarized invoice table
- Real-time data updates

### 3. [Clients Management Module](./03-Clients-Management/Clients-Management-Module-Documentation.md)
Detailed documentation for client management, contacts, assignments, and rates.

**Key Features:**
- Client CRUD operations
- Contact management
- Client search and filtering
- Client rates management
- Client assignment

### 4. [Calendar & Time Records Module](./04-Calendar-Time-Records/Calendar-Time-Records-Module-Documentation.md)
Complete guide to calendar views, time record management, and session scheduling.

**Key Features:**
- Multiple calendar views (Month, Week, Day)
- Time record creation and management
- Session scheduling
- Calendar summary
- Pending sessions management

### 5. [Invoices Module](./05-Invoices/Invoices-Module-Documentation.md)
Comprehensive documentation for invoice creation, management, payment tracking, and recurring invoices.

**Key Features:**
- Multi-step invoice creation
- Invoice templates
- Payment recording
- Invoice status management
- Recurring invoices
- Invoice KPIs

### 6. [Reports Module](./06-Reports/Reports-Module-Documentation.md)
Detailed guide to reporting functionality, analytics, and data export.

**Key Features:**
- Client reports
- Invoice reports
- Time period selection
- Report export
- Summary statistics

### 7. [Sessions Module](./07-Sessions/Sessions-Module-Documentation.md)
Complete documentation for session lifecycle, confirmation workflows, and invoice integration.

**Key Features:**
- Session management
- Pending sessions
- Session confirmation
- Session status management
- Session selection for invoices

### 8. [Profile Module](./08-Profile/Profile-Module-Documentation.md)
Guide to user profile management, account settings, and password changes.

**Key Features:**
- Profile viewing and editing
- Password change
- Account information
- Profile picture management (future)

### 9. [Settings Module](./09-Settings/Settings-Module-Documentation.md)
Comprehensive documentation for billing settings, notification preferences, and account configuration.

**Key Features:**
- Billing and subscription management
- Payment method management
- Notification settings
- Account preferences

### 10. [Admin Panel Module](./10-Admin-Panel/Admin-Panel-Module-Documentation.md)
Complete guide to administrative functionality, user management, and system settings.

**Key Features:**
- User management
- Billing management
- System settings
- Support and escalations
- Analytics and reporting

### 11. [Language Management Module](./11-Language-Management/Language-Management-Module-Documentation.md)
Comprehensive documentation for internationalization (i18n), multi-language support, and translation management.

**Key Features:**
- Multi-language support (English, Spanish)
- Language switcher component
- Client-side and server-side translation
- Email localization
- Translation namespaces
- Language detection and persistence

## Application Architecture

### Technology Stack
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **UI Library**: React 18
- **State Management**: React Query (@tanstack/react-query)
- **Forms**: React Hook Form
- **Validation**: Zod
- **Styling**: Tailwind CSS
- **Icons**: Lucide React
- **Date Handling**: date-fns
- **Internationalization**: i18next, react-i18next, i18next-browser-languagedetector

### User Roles
The application supports three user roles:

1. **Free Users**
   - Limited to 3 clients
   - Basic features
   - Standard support

2. **Paid Users**
   - Unlimited clients
   - All features
   - Priority support
   - Advanced analytics

3. **Admin Users**
   - Full system access
   - User management
   - System configuration
   - Admin panel access

## Module Dependencies

```
Authentication
    ↓
Dashboard ← Clients ← Calendar ← Sessions
    ↓         ↓          ↓
Invoices ← Reports
    ↓
Profile → Settings
    ↓
Admin Panel
```

## Key Workflows

### Invoice Creation Workflow
1. Select invoice type (Session-based, Manual, Recurring)
2. Select client
3. Select sessions (if session-based)
4. Configure invoice details
5. Preview invoice
6. Save and send

### Session Management Workflow
1. Create session in calendar
2. Session appears in pending list (if needed)
3. Confirm session
4. Session available for invoicing
5. Add to invoice
6. Session marked as invoiced

### Client Management Workflow
1. Add new client
2. Add contacts (optional)
3. Assign rates
4. Create sessions for client
5. Generate invoices
6. Track payments

## API Structure

All modules follow a consistent API structure:

- **GET** `/api/[module]` - List all items
- **GET** `/api/[module]/[id]` - Get single item
- **POST** `/api/[module]` - Create new item
- **PUT** `/api/[module]/[id]` - Update item
- **DELETE** `/api/[module]/[id]` - Delete item

## Service Layer Pattern

Each module has a corresponding service file in `/app/services/` that handles:
- Data fetching
- CRUD operations
- Business logic
- Error handling

## Component Structure

Components are organized by feature:
- `/app/components/[module]/` - Module-specific components
- `/app/components/ui/` - Reusable UI components
- `/app/[module]/` - Module pages

## Data Flow

1. **User Action** → Component
2. **Component** → Hook
3. **Hook** → Service
4. **Service** → API Endpoint
5. **API** → Database/External Service
6. **Response** → Service → Hook → Component → UI Update

## Security Features

- Role-based access control
- Authentication required for protected routes
- Secure session management
- Input validation
- Error handling
- Data sanitization

## Future Enhancements

Each module documentation includes a "Future Enhancements" section outlining planned features and improvements.

## Getting Started

1. Review the module documentation for the feature you're working on
2. Understand the data structures and API endpoints
3. Review the service layer implementation
4. Check component usage examples
5. Follow the established patterns

## Contributing

When adding new features:
1. Create comprehensive documentation
2. Follow existing patterns
3. Update this README if adding new modules
4. Include API documentation
5. Document data structures
6. Add examples and workflows

## Support

For questions or issues:
1. Review the relevant module documentation
2. Check API endpoint documentation
3. Review service layer implementations
4. Check component examples

## Version History

- **Current Version**: 0.1.0
- **Documentation Version**: 1.0.0
- **Last Updated**: 2025

---

**Note**: This documentation is comprehensive and covers all major features of the Axis Pro application. Each module documentation is self-contained and can be used as a standalone reference.

