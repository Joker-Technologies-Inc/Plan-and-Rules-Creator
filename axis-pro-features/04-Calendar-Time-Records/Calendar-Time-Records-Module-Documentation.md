# Calendar & Time Records Module Documentation

## Overview
The Calendar & Time Records Module provides comprehensive scheduling, time tracking, and session management functionality. It allows users to view, create, edit, and manage appointments and time records in multiple calendar views.

## Features

### 1. Calendar Views
- **Purpose**: Display time records and sessions in different time perspectives
- **Location**: `/app/calendar/page.tsx`, `/app/components/calendar/Calendar.tsx`

**Available Views**:

#### a. Month View
- **Component**: `MonthView.tsx`
- **Features**:
  - Full month calendar grid
  - All sessions displayed on respective dates
  - Color-coded by status (Confirmed, Scheduled, Invoiced)
  - Click date to view day details
  - Navigation between months
  - Today indicator

#### b. Week View
- **Component**: `WeekView.tsx`
- **Features**:
  - Seven-day week display
  - Hourly time slots
  - Session blocks with duration
  - Drag-and-drop scheduling (future)
  - Time slot indicators
  - Week navigation

#### c. Day View
- **Component**: `DayView.tsx`
- **Features**:
  - Single day detailed view
  - Hour-by-hour breakdown
  - All sessions for the day
  - Time slot availability
  - Session details on click
  - Day navigation

**View Switching**:
- Toggle between views
- Maintain selected date across views
- Smooth transitions
- Responsive design

### 2. Time Record Management
- **Purpose**: Create, edit, and manage time records/sessions
- **Location**: `/app/components/calendar/TimeRecordDialog.tsx`
- **API Endpoint**: `/api/time-records`
- **Service**: `timeRecordService`, `sessionsService`

**Time Record Fields**:
- Client (required, dropdown selection)
- Date and Time (required, date/time picker)
- Duration (required, in minutes)
- Status (Confirmed, Scheduled, Invoiced)
- Pricing Type:
  - Predefined Rate (select from rates)
  - Manual Price (enter custom amount)
- Needs Confirmation flag

**Time Record Actions**:
- Create new time record
- Edit existing time record
- Delete time record
- Confirm pending sessions
- Mark as invoiced

### 3. Add Time Record Dialog
- **Purpose**: Quick creation of time records
- **Location**: `/app/components/calendar/TimeRecordDialog.tsx`
- **Trigger**: Plus button or date click

**Dialog Features**:
- Form validation
- Client search/selection
- Date/time picker
- Duration selector
- Rate selection
- Save and cancel actions
- Loading states

### 4. Calendar Summary
- **Purpose**: Display calendar statistics and quick actions
- **Location**: `/app/components/calendar/CalendarSummary.tsx`

**Summary Information**:
- Total sessions this month
- Upcoming sessions count
- Pending confirmations count
- Total hours scheduled
- Revenue projection (future)

**Quick Actions**:
- View pending sessions
- Add new session
- Filter by client
- Export calendar (future)

### 5. Pending Sessions Management
- **Purpose**: Manage sessions requiring confirmation
- **Location**: `/app/components/PendingSessions.tsx`
- **API Endpoint**: `/api/sessions/pending`
- **Service**: `sessionsService.getPendingSessions()`

**Features**:
- List of sessions needing confirmation
- Quick confirm action
- Session details preview
- Bulk confirmation (future)
- Notification indicators

### 6. Session Status Management
- **Purpose**: Track and update session statuses
- **Service**: `sessionsService.updateSessionStatus()`

**Status Types**:
- **Scheduled**: Newly created, not yet confirmed
- **Confirmed**: Approved and ready
- **Invoiced**: Included in an invoice
- **Completed**: Session finished (future)

**Status Transitions**:
- Scheduled → Confirmed
- Confirmed → Invoiced
- Status updates affect calendar display

### 7. Pricing and Rates Integration
- **Purpose**: Apply pricing to time records
- **Integration**: Rate Service

**Pricing Options**:
- **Predefined Rate**: Select from client's assigned rates
- **Manual Price**: Enter custom amount
- **Rate Types Supported**:
  - Hourly rates
  - Fixed rates
  - Package rates

**Pricing Calculation**:
- Automatic calculation for hourly rates
- Manual entry for fixed/package rates
- Price displayed in session details

## Data Structure

### TimeRecord Type (`/app/types/calendar.ts`)
```typescript
type TimeRecord = {
  id: string
  clientId: string
  clientName: string
  date: Date
  duration: number // in minutes
  status: 'Scheduled' | 'Confirmed' | 'Invoiced'
  pricingType: 'predefined' | 'manual'
  rateId?: string // if predefined
  manualPrice?: number // if manual
  needsConfirmation: boolean
}
```

## API Endpoints

### GET `/api/time-records`
- **Response**: Array of TimeRecord objects
- **Query Parameters**:
  - `startDate`: Filter start date
  - `endDate`: Filter end date
  - `clientId`: Filter by client

### POST `/api/time-records`
- **Request Body**: TimeRecord object (without id)
- **Response**: Created TimeRecord object

### GET `/api/time-records/[id]`
- **Response**: Single TimeRecord object

### PUT `/api/time-records/[id]`
- **Request Body**: Updated TimeRecord object
- **Response**: Updated TimeRecord object

### DELETE `/api/time-records/[id]`
- **Response**: Success confirmation

### GET `/api/sessions`
- **Response**: Array of all sessions (TimeRecord objects)

### GET `/api/sessions/pending`
- **Response**: Array of sessions needing confirmation

### PUT `/api/sessions/[id]`
- **Request Body**: Updated session data
- **Response**: Updated session

## Service Layer

### `timeRecordService` (`/app/services/timeRecordService.ts`)

**Methods**:
- `getTimeRecords()`: Fetch all time records
- `addTimeRecord(record)`: Create new time record
- `updateTimeRecord(record)`: Update existing record
- `deleteTimeRecord(id)`: Delete time record

### `sessionsService` (`/app/services/sessionsService.ts`)

**Methods**:
- `getAllSessions()`: Fetch all sessions
- `getPendingSessions()`: Fetch sessions needing confirmation
- `addSession(session)`: Create new session
- `updateSession(session)`: Update session
- `updateSessionStatus(id, status)`: Update session status
- `deleteSession(id)`: Delete session
- `getTimeRecords()`: Alias for getAllSessions
- `addTimeRecord(record)`: Alias for addSession
- `updateTimeRecord(record)`: Alias for updateSession
- `deleteTimeRecord(id)`: Alias for deleteSession

## Hooks

### `useTimeRecords` (`/app/hooks/useTimeRecords.ts`)
- Manages time record state
- Handles CRUD operations
- Manages loading and error states
- Provides date filtering

### `usePendingSessions` (`/app/hooks/usePendingSessions.ts`)
- Manages pending sessions
- Handles confirmation actions
- Updates session status
- Provides notification counts

## Components

1. **CalendarPage** (`/app/calendar/page.tsx`): Main calendar page
2. **Calendar** (`/app/components/calendar/Calendar.tsx`): Main calendar component
3. **MonthView** (`/app/components/calendar/MonthView.tsx`): Month view component
4. **WeekView** (`/app/components/calendar/WeekView.tsx`): Week view component
5. **DayView** (`/app/components/calendar/DayView.tsx`): Day view component
6. **TimeRecordDialog** (`/app/components/calendar/TimeRecordDialog.tsx`): Add/Edit dialog
7. **CalendarSummary** (`/app/components/calendar/CalendarSummary.tsx`): Summary sidebar
8. **CalendarSkeleton** (`/app/components/calendar/CalendarSkeleton.tsx`): Loading skeleton
9. **PlusButton** (`/app/components/calendar/PlusButton.tsx`): Add record button
10. **PendingSessions** (`/app/components/PendingSessions.tsx`): Pending sessions list

## Utility Functions

### Calendar Utilities (`/app/utils/calendar.ts`, `/app/utils/calendarUtils.ts`)
- Date formatting functions
- Date range calculations
- Week/month navigation
- Time slot generation
- Session grouping by date
- Calendar grid generation

## User Experience Features

### Calendar Navigation
- Previous/Next month/week/day buttons
- Today button for quick navigation
- Date picker for direct navigation
- Keyboard shortcuts (future)

### Visual Indicators
- Color-coded session statuses
- Today highlight
- Selected date highlight
- Hover effects on sessions
- Loading indicators

### Responsive Design
- Mobile-optimized views
- Touch-friendly interactions
- Adaptive layout
- Swipe gestures (future)

### Performance Optimizations
- Lazy loading of calendar data
- Virtual scrolling for large date ranges
- Memoized calculations
- Optimized re-renders

## Integration Points

1. **Clients Module**: Client selection for sessions
2. **Invoices Module**: Sessions can be converted to invoice items
3. **Rates Module**: Rate selection for pricing
4. **Dashboard Module**: Upcoming sessions count
5. **Reports Module**: Session data for reporting

## Business Logic

### Session Confirmation Flow
1. Session created with `needsConfirmation: true`
2. Appears in pending sessions list
3. User confirms session
4. Status changes to "Confirmed"
5. Removed from pending list

### Invoice Integration
1. Sessions marked as "Invoiced" when added to invoice
2. Cannot be added to multiple invoices
3. Status prevents duplicate invoicing
4. Invoice reference stored (future)

### Time Slot Management
- Sessions can overlap (future: conflict detection)
- Duration affects time slot allocation
- Calendar shows availability (future)

## Role-Based Features

### Free Users
- Basic calendar functionality
- Limited session history
- Standard views available

### Paid Users
- All calendar features
- Advanced filtering
- Export capabilities
- Recurring sessions (future)

### Admin Users
- View all users' calendars
- System-wide session management
- Calendar analytics

## Error Handling

- Network errors: Display error, retry option
- Validation errors: Field-specific messages
- Conflict errors: Warn about overlapping sessions
- Not found errors: Handle missing sessions gracefully

## Future Enhancements

1. Recurring sessions/appointments
2. Session reminders and notifications
3. Calendar sync (Google Calendar, Outlook)
4. Drag-and-drop scheduling
5. Conflict detection and resolution
6. Availability management
7. Session templates
8. Bulk session operations
9. Calendar sharing
10. Time zone support
11. Session notes and attachments
12. Client calendar view
13. Session waitlist
14. Automatic session confirmation rules
15. Calendar export (iCal, PDF)
16. Mobile app integration
17. Session check-in/check-out
18. Real-time calendar updates

## Dependencies

- React 18
- Next.js 14
- date-fns (date manipulation)
- React Day Picker (date picker)
- @tanstack/react-query (data fetching)
- Lucide React (icons)
- Tailwind CSS (styling)

## Testing Considerations

- Unit tests for calendar calculations
- Integration tests for time record CRUD
- Component tests for calendar views
- E2E tests for session creation flow
- Date manipulation tests
- Time zone handling tests
- Conflict detection tests

