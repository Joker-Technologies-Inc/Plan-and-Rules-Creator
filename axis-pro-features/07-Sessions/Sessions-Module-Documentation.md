# Sessions Module Documentation

## Overview
The Sessions Module manages session lifecycle, confirmation workflows, and session-to-invoice conversion. It handles pending sessions, session status management, and provides session selection for invoice creation.

## Features

### 1. Session Management
- **Purpose**: Core session CRUD operations
- **Location**: Integrated with Calendar and Invoices modules
- **API Endpoint**: `/api/sessions`
- **Service**: `sessionsService`

**Session Operations**:
- Create new sessions
- Update existing sessions
- Delete sessions
- View session details
- Update session status

### 2. Pending Sessions
- **Purpose**: Manage sessions requiring confirmation
- **Location**: `/app/components/PendingSessions.tsx`
- **API Endpoint**: `/api/sessions/pending`
- **Service**: `sessionsService.getPendingSessions()`

**Pending Session Features**:
- List all sessions with `needsConfirmation: true`
- Quick confirmation action
- Session details preview
- Status update on confirmation
- Notification indicators
- Sidebar display in main navigation

**Pending Session Display**:
- Client name
- Session date and time
- Duration
- Status (Scheduled)
- Quick confirm button
- View details link

### 3. Session Confirmation
- **Purpose**: Confirm pending sessions
- **Location**: `/app/components/PendingSessionsConfirmation.tsx`
- **Service**: `sessionsService.updateSessionStatus()`

**Confirmation Flow**:
1. User views pending sessions list
2. Clicks confirm button on session
3. System updates status to "Confirmed"
4. Removes `needsConfirmation` flag
5. Updates calendar display
6. Removes from pending list

**Bulk Confirmation** (Future):
- Select multiple sessions
- Confirm all at once
- Batch status update

### 4. Session Status Management
- **Purpose**: Track session lifecycle
- **Service**: `sessionsService.updateSessionStatus()`

**Status Types**:
- **Scheduled**: Newly created, awaiting confirmation
- **Confirmed**: Approved and ready
- **Invoiced**: Included in an invoice

**Status Transitions**:
- Scheduled → Confirmed (via confirmation)
- Confirmed → Invoiced (when added to invoice)
- Status updates are irreversible (future: allow reversal)

### 5. Session Selection for Invoices
- **Purpose**: Select sessions to include in invoices
- **Location**: `/app/components/SessionSelector.tsx`, `/app/components/UnInvoicedSessionSelector.tsx`
- **Integration**: Invoice creation flow

**Session Selection Features**:
- List uninvoiced sessions for a client
- Multi-select sessions
- Session details display:
  - Date and time
  - Duration
  - Rate/Price
  - Total amount
- Total calculation preview
- Filter by date range
- Select all/none options

**Selection Criteria**:
- Only shows sessions for selected client
- Only shows uninvoiced sessions (status != "Invoiced")
- Only shows confirmed sessions (status = "Confirmed")
- Date range filtering

### 6. Uninvoiced Sessions Selector
- **Purpose**: Specialized selector for invoice creation
- **Location**: `/app/components/UnInvoicedSessionSelector.tsx`
- **Usage**: Invoice creation workflow

**Features**:
- Client-specific session list
- Uninvoiced filter applied automatically
- Session grouping by date
- Amount calculation
- Quick selection tools

### 7. Session Details
- **Purpose**: View comprehensive session information
- **Location**: Session detail views

**Session Information**:
- Client information
- Date and time
- Duration
- Status
- Pricing information:
  - Rate type (predefined/manual)
  - Rate details
  - Total amount
- Confirmation status
- Invoice reference (if invoiced)
- Notes (future)

## Data Structure

### TimeRecord/Session Type (`/app/types/calendar.ts`)
```typescript
type TimeRecord = {
  id: string
  clientId: string
  clientName: string
  date: Date
  duration: number // in minutes
  status: 'Scheduled' | 'Confirmed' | 'Invoiced'
  pricingType: 'predefined' | 'manual'
  rateId?: string
  manualPrice?: number
  needsConfirmation: boolean
}
```

## API Endpoints

### GET `/api/sessions`
- **Response**: Array of all sessions (TimeRecord objects)
- **Query Parameters**:
  - `clientId`: Filter by client
  - `status`: Filter by status
  - `needsConfirmation`: Filter by confirmation status

### GET `/api/sessions/pending`
- **Response**: Array of sessions needing confirmation
- **Filters**: Automatically filters `needsConfirmation: true`

### GET `/api/sessions/[id]`
- **Response**: Single session object

### POST `/api/sessions`
- **Request Body**: Session object (without id)
- **Response**: Created session object

### PUT `/api/sessions/[id]`
- **Request Body**: Updated session object
- **Response**: Updated session object

### DELETE `/api/sessions/[id]`
- **Response**: Success confirmation

### PUT `/api/sessions/[id]/status`
- **Request Body**: `{ status: 'Confirmed' | 'Invoiced' }`
- **Response**: Updated session object

## Service Layer

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

### `usePendingSessions` (`/app/hooks/usePendingSessions.ts`)
- Manages pending sessions state
- Handles confirmation actions
- Updates session status
- Provides notification counts
- Auto-refreshes pending list

### `useTimeRecords` (`/app/hooks/useTimeRecords.ts`)
- Manages all time records/sessions
- Handles CRUD operations
- Provides filtering capabilities
- Manages loading states

## Components

1. **PendingSessions** (`/app/components/PendingSessions.tsx`): Pending sessions list
2. **PendingSessionsConfirmation** (`/app/components/PendingSessionsConfirmation.tsx`): Confirmation dialog
3. **SessionSelector** (`/app/components/SessionSelector.tsx`): General session selector
4. **UnInvoicedSessionSelector** (`/app/components/UnInvoicedSessionSelector.tsx`): Invoice-specific selector
5. **TimeRecordDialog** (`/app/components/calendar/TimeRecordDialog.tsx`): Session creation/editing

## Session Lifecycle

### Creation
1. User creates session (via calendar or directly)
2. Session created with `status: 'Scheduled'`
3. If manual pricing or special conditions: `needsConfirmation: true`
4. Session appears in calendar and pending list

### Confirmation
1. User views pending sessions
2. Reviews session details
3. Confirms session
4. Status changes to "Confirmed"
5. `needsConfirmation` set to false
6. Removed from pending list

### Invoicing
1. User creates invoice
2. Selects confirmed sessions
3. Sessions added to invoice
4. Status changes to "Invoiced"
5. Sessions no longer available for selection
6. Invoice reference stored (future)

## Business Logic

### Confirmation Requirements
- Sessions with manual pricing may require confirmation
- Sessions outside normal hours may require confirmation
- Admin can configure confirmation rules (future)

### Invoice Eligibility
- Only confirmed sessions can be invoiced
- Already invoiced sessions cannot be selected
- Sessions must belong to selected client

### Status Rules
- Cannot change status from "Invoiced" back to "Confirmed"
- Cannot invoice "Scheduled" sessions
- Confirmation is required before invoicing

## Integration Points

1. **Calendar Module**: Session creation and display
2. **Invoices Module**: Session selection for invoices
3. **Clients Module**: Client association
4. **Rates Module**: Rate application
5. **Dashboard Module**: Pending sessions count

## Role-Based Features

### Free Users
- Basic session management
- Standard confirmation workflow
- Limited session history

### Paid Users
- All session features
- Advanced filtering
- Bulk operations (future)
- Session templates (future)

### Admin Users
- View all users' sessions
- System-wide session management
- Session analytics

## User Experience Features

### Pending Sessions Notification
- Badge count in sidebar
- Visual indicators
- Quick access from navigation
- Auto-refresh on updates

### Session Selection UI
- Checkbox selection
- Visual feedback
- Total calculation
- Select all/none
- Date grouping

### Status Indicators
- Color-coded status badges
- Visual status transitions
- Clear status labels

## Error Handling

- Network errors: Display error, retry option
- Validation errors: Field-specific messages
- Status transition errors: Prevent invalid transitions
- Not found errors: Handle missing sessions gracefully

## Future Enhancements

1. Bulk session confirmation
2. Session templates
3. Recurring session creation
4. Session notes and attachments
5. Session reminders
6. Session cancellation workflow
7. Session rescheduling
8. Session waitlist
9. Session conflict detection
10. Automatic confirmation rules
11. Session rating/feedback
12. Session history tracking
13. Session analytics
14. Session export
15. Session import
16. Session tags/categories
17. Session search
18. Advanced session filtering
19. Session reports
20. Session notifications

## Dependencies

- React 18
- Next.js 14
- @tanstack/react-query (data fetching)
- Date-fns (date manipulation)
- Lucide React (icons)

## Testing Considerations

- Unit tests for session status transitions
- Integration tests for session CRUD
- Component tests for session selectors
- E2E tests for confirmation workflow
- Invoice selection tests
- Status validation tests

