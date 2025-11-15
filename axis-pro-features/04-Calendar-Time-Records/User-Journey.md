# Calendar & Time Records Module - User Journey

## Overview
This document describes the user journey through the Calendar and Time Records module, covering session scheduling, calendar navigation, time record management, and session confirmation workflows.

---

## Journey 1: Creating a New Time Record

### User Goal
Schedule a new session/appointment with a client.

### Step-by-Step Journey

#### Step 1: Navigate to Calendar
- **User Action**: User clicks "Calendar" in sidebar or navigates to `/calendar`
- **System Response**: Displays calendar view (default: Month view)
- **User Experience**: Full calendar interface

#### Step 2: Initiate Time Record Creation
- **User Action**: User clicks "Add Time Record" button or clicks on a date
- **System Response**: Opens time record creation dialog
- **User Experience**: Time record form appears

#### Step 3: Select Client
- **User Action**: User selects client from dropdown
- **System Response**: 
  - Shows client list
  - Filters/searchable client list
  - Displays client information
- **User Experience**: Easy client selection

#### Step 4: Set Date and Time
- **User Action**: User selects:
  - Date (using date picker)
  - Time (using time picker)
- **System Response**: 
  - Date picker opens
  - Time slots available
  - Validates date/time
- **User Experience**: Intuitive date/time selection

#### Step 5: Set Duration
- **User Action**: User enters duration (in minutes)
- **System Response**: 
  - Validates duration
  - Shows duration in readable format
  - Calculates end time
- **User Experience**: Clear duration input

#### Step 6: Choose Pricing Type
- **User Action**: User selects pricing:
  - **Option A**: Predefined Rate (selects from client's rates)
  - **Option B**: Manual Price (enters custom amount)
- **System Response**: 
  - Shows rate options if predefined
  - Shows price input if manual
  - Calculates total amount
- **User Experience**: Flexible pricing options

#### Step 7: Set Status
- **User Action**: User selects status (Scheduled/Confirmed)
- **System Response**: 
  - Updates status
  - Sets needsConfirmation flag if needed
- **User Experience**: Status management

#### Step 8: Save Time Record
- **User Action**: User clicks "Save" button
- **System Response**:
  - Validates all fields
  - Creates time record
  - Adds to calendar
  - Shows in pending list (if needs confirmation)
- **User Experience**: Success confirmation

#### Step 9: View on Calendar
- **User Action**: User views calendar
- **System Response**: Displays new time record on selected date/time
- **User Experience**: Visual confirmation on calendar

### Success Criteria
- ✅ Time record created successfully
- ✅ Appears on calendar
- ✅ Client associated correctly
- ✅ Pricing set appropriately

---

## Journey 2: Navigating Calendar Views

### User Goal
View sessions in different time perspectives.

### Step-by-Step Journey

#### Step 1: Month View (Default)
- **User Action**: User opens calendar (defaults to Month view)
- **System Response**: Displays full month grid with:
  - All sessions on respective dates
  - Color-coded by status
  - Today highlighted
- **User Experience**: Monthly overview

#### Step 2: Switch to Week View
- **User Action**: User clicks "Week" view button
- **System Response**: Displays seven-day week with:
  - Hourly time slots
  - Session blocks with duration
  - Time indicators
- **User Experience**: Detailed weekly view

#### Step 3: Switch to Day View
- **User Action**: User clicks "Day" view button
- **System Response**: Displays single day with:
  - Hour-by-hour breakdown
  - All sessions for the day
  - Detailed time slots
- **User Experience**: Focused daily view

#### Step 4: Navigate Between Periods
- **User Action**: User clicks Previous/Next buttons
- **System Response**: 
  - Moves to previous/next month/week/day
  - Maintains selected view
  - Updates sessions display
- **User Experience**: Smooth navigation

#### Step 5: Jump to Today
- **User Action**: User clicks "Today" button
- **System Response**: Returns to current date in selected view
- **User Experience**: Quick return to present

### Success Criteria
- ✅ All views work correctly
- ✅ Navigation is smooth
- ✅ Sessions display accurately
- ✅ Today indicator works

---

## Journey 3: Confirming Pending Sessions

### User Goal
Review and confirm sessions that require approval.

### Step-by-Step Journey

#### Step 1: View Pending Sessions
- **User Action**: User checks sidebar "Pending Confirmation" section
- **System Response**: Displays list of sessions needing confirmation
- **User Experience**: Clear pending list

#### Step 2: Review Session Details
- **User Action**: User views pending session information:
  - Client name
  - Date and time
  - Duration
  - Pricing information
- **System Response**: Shows complete session details
- **User Experience**: All information visible

#### Step 3: Confirm Session
- **User Action**: User clicks "Confirm" button
- **System Response**:
  - Updates status to "Confirmed"
  - Removes needsConfirmation flag
  - Removes from pending list
  - Updates calendar display
- **User Experience**: Quick confirmation

#### Step 4: Bulk Confirmation (Future)
- **User Action**: User selects multiple sessions and confirms all
- **System Response**: Confirms all selected sessions at once
- **User Experience**: Efficient bulk operations

### Success Criteria
- ✅ Pending sessions visible
- ✅ Confirmation works quickly
- ✅ Status updates correctly
- ✅ Calendar reflects changes

---

## Journey 4: Editing a Time Record

### User Goal
Update existing session information.

### Step-by-Step Journey

#### Step 1: Access Time Record
- **User Action**: User clicks on time record in calendar
- **System Response**: Opens time record details or edit dialog
- **User Experience**: Easy access to edit

#### Step 2: Modify Information
- **User Action**: User updates:
  - Date/time
  - Duration
  - Client
  - Pricing
  - Status
- **System Response**: 
  - Validates changes
  - Shows unsaved changes indicator
- **User Experience**: Clear edit interface

#### Step 3: Save Changes
- **User Action**: User clicks "Save" button
- **System Response**:
  - Validates all fields
  - Updates time record
  - Refreshes calendar display
- **User Experience**: Changes applied successfully

### Success Criteria
- ✅ Time record updated
- ✅ Calendar reflects changes
- ✅ All fields editable

---

## Journey 5: Viewing Calendar Summary

### User Goal
Quick overview of calendar statistics.

### Step-by-Step Journey

#### Step 1: View Summary Sidebar
- **User Action**: User views calendar summary panel
- **System Response**: Displays:
  - Total sessions this month
  - Upcoming sessions count
  - Pending confirmations count
  - Total hours scheduled
- **User Experience**: Quick statistics

#### Step 2: Review Metrics
- **User Action**: User examines summary numbers
- **System Response**: Shows calculated metrics
- **User Experience**: Clear overview

### Success Criteria
- ✅ Summary data is accurate
- ✅ Metrics update correctly
- ✅ Information is useful

---

## Journey 6: Deleting a Time Record

### User Goal
Remove a scheduled session.

### Step-by-Step Journey

#### Step 1: Access Delete Option
- **User Action**: User clicks on time record and selects "Delete"
- **System Response**: Shows confirmation dialog
- **User Experience**: Safe deletion process

#### Step 2: Confirm Deletion
- **User Action**: User confirms deletion
- **System Response**:
  - Deletes time record
  - Removes from calendar
  - Updates summary statistics
- **User Experience**: Confirmed deletion

### Success Criteria
- ✅ Deletion requires confirmation
- ✅ Time record removed successfully
- ✅ Calendar updates correctly

---

## Journey 7: Using Calendar for Session Planning

### User Goal
Plan and organize upcoming sessions.

### Step-by-Step Journey

#### Step 1: Review Upcoming Sessions
- **User Action**: User views calendar in Week or Month view
- **System Response**: Shows all upcoming sessions
- **User Experience**: Complete schedule overview

#### Step 2: Identify Gaps
- **User Action**: User looks for available time slots
- **System Response**: Shows empty time slots
- **User Experience**: Easy availability identification

#### Step 3: Schedule New Sessions
- **User Action**: User creates new time records in available slots
- **System Response**: Adds sessions to calendar
- **User Experience**: Efficient scheduling

#### Step 4: Manage Conflicts (Future)
- **User Action**: User attempts to schedule overlapping sessions
- **System Response**: Warns about conflicts
- **User Experience**: Conflict prevention

### Success Criteria
- ✅ Calendar shows complete schedule
- ✅ Availability is clear
- ✅ Scheduling is efficient

---

## User Personas

### Persona 1: Service Provider (Daily Scheduling)
- **Goal**: Schedule daily appointments
- **Journey**: Calendar → Day View → Add Sessions → Confirm
- **Pain Points**: Time management, avoiding conflicts
- **Success**: Well-organized daily schedule

### Persona 2: Therapist (Weekly Planning)
- **Goal**: Plan weekly client sessions
- **Journey**: Calendar → Week View → Schedule Sessions → Review
- **Pain Points**: Balancing schedule, recurring sessions
- **Success**: Balanced weekly schedule

### Persona 3: Consultant (Monthly Overview)
- **Goal**: Overview of monthly appointments
- **Journey**: Calendar → Month View → Review → Plan Ahead
- **Pain Points**: Long-term planning, availability
- **Success**: Clear monthly overview

---

## Key User Experience Principles

1. **Visual Clarity**: Clear calendar display
2. **Easy Scheduling**: Quick session creation
3. **Flexible Views**: Multiple viewing options
4. **Status Management**: Clear session status
5. **Confirmation Workflow**: Easy pending session handling
6. **Navigation**: Smooth calendar navigation

---

## Metrics to Track

- Time records created per day
- Calendar view usage (Month/Week/Day)
- Pending session confirmation rate
- Average time to create record
- Session edit frequency
- Calendar navigation patterns

---

## Future Enhancements

- Recurring sessions/appointments
- Session reminders and notifications
- Calendar sync (Google Calendar, Outlook)
- Drag-and-drop scheduling
- Conflict detection and resolution
- Availability management
- Session templates
- Bulk session operations
- Calendar sharing
- Time zone support
- Session notes and attachments
- Client calendar view
- Session waitlist
- Automatic session confirmation rules
- Calendar export (iCal, PDF)

