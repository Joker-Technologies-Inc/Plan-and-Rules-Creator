# Invoices Module - User Journey

## Overview
This document describes the user journey through the Invoices module, covering invoice creation, management, payment tracking, and invoice-related operations.

---

## Journey 1: Creating a Session-Based Invoice

### User Goal
Generate an invoice from completed sessions.

### Step-by-Step Journey

#### Step 1: Navigate to Invoice Creation
- **User Action**: User clicks "Invoices" → "New Invoice" or navigates to `/invoices/new`
- **System Response**: Displays invoice creation wizard
- **User Experience**: Step-by-step invoice creation

#### Step 2: Select Invoice Type
- **User Action**: User selects "Session-based Invoice"
- **System Response**: Proceeds to client selection step
- **User Experience**: Clear type selection

#### Step 3: Select Client
- **User Action**: User selects client from list
- **System Response**: 
  - Shows client information
  - Proceeds to session selection
  - Filters sessions for selected client
- **User Experience**: Easy client selection

#### Step 4: Select Sessions
- **User Action**: User selects sessions to invoice:
  - Views list of uninvoiced sessions
  - Checks sessions to include
  - Reviews session details (date, duration, rate, amount)
  - Sees total calculation preview
- **System Response**: 
  - Shows only confirmed, uninvoiced sessions
  - Calculates total as sessions selected
  - Updates preview
- **User Experience**: Clear session selection

#### Step 5: Configure Invoice Details
- **User Action**: User enters:
  - Invoice Number (auto-generated or manual)
  - Issue Date
  - Due Date
  - Discount (if applicable)
  - Tax (if applicable)
  - Notes
  - Payment Method
- **System Response**: 
  - Validates dates
  - Calculates totals
  - Shows preview
- **User Experience**: Complete invoice configuration

#### Step 6: Preview Invoice
- **User Action**: User reviews invoice preview
- **System Response**: Displays formatted invoice preview
- **User Experience**: Professional invoice preview

#### Step 7: Save Invoice
- **User Action**: User clicks "Save Invoice"
- **System Response**:
  - Creates invoice
  - Marks sessions as "Invoiced"
  - Saves invoice to database
  - Shows success message
- **User Experience**: Invoice created successfully

#### Step 8: Send Invoice (Optional)
- **User Action**: User clicks "Send Invoice"
- **System Response**: 
  - Opens email composition dialog
  - Pre-fills invoice details
  - Sends email to client
- **User Experience**: Quick invoice delivery

### Success Criteria
- ✅ Invoice created from sessions
- ✅ Sessions marked as invoiced
- ✅ Invoice details are correct
- ✅ Invoice can be sent to client

---

## Journey 2: Creating a Manual Invoice

### User Goal
Create an invoice with custom line items.

### Step-by-Step Journey

#### Step 1: Start Manual Invoice
- **User Action**: User selects "Manual Invoice" type
- **System Response**: Proceeds to client selection
- **User Experience**: Manual invoice option

#### Step 2: Select Client
- **User Action**: User selects client
- **System Response**: Proceeds to invoice details
- **User Experience**: Client selected

#### Step 3: Add Invoice Items
- **User Action**: User adds line items:
  - Description
  - Quantity
  - Rate
  - Amount (auto-calculated)
- **System Response**: 
  - Calculates item totals
  - Updates subtotal
  - Shows running total
- **User Experience**: Easy item addition

#### Step 4: Configure Invoice
- **User Action**: User sets dates, discount, tax, notes
- **System Response**: Calculates final total
- **User Experience**: Complete invoice setup

#### Step 5: Save and Send
- **User Action**: User saves and sends invoice
- **System Response**: Invoice created and sent
- **User Experience**: Invoice delivered

### Success Criteria
- ✅ Manual invoice created
- ✅ Custom items included
- ✅ Totals calculated correctly

---

## Journey 3: Recording Payment

### User Goal
Record payment received for an invoice.

### Step-by-Step Journey

#### Step 1: Access Invoice
- **User Action**: User opens invoice details
- **System Response**: Displays invoice with payment section
- **User Experience**: Invoice details visible

#### Step 2: Record Payment
- **User Action**: User clicks "Record Payment"
- **System Response**: Opens payment recording dialog
- **User Experience**: Payment form appears

#### Step 3: Enter Payment Details
- **User Action**: User enters:
  - Payment Amount
  - Payment Date
  - Payment Method (PayPal, Venmo, Zelle, Bank Transfer)
  - Reference/Transaction ID (optional)
  - Notes (optional)
- **System Response**: 
  - Validates amount (cannot exceed outstanding balance)
  - Validates date
  - Shows remaining balance
- **User Experience**: Clear payment input

#### Step 4: Save Payment
- **User Action**: User clicks "Record Payment"
- **System Response**:
  - Records payment
  - Updates invoice status (to "Paid" if fully paid)
  - Calculates new outstanding balance
  - Updates payment history
- **User Experience**: Payment recorded successfully

#### Step 5: View Updated Invoice
- **User Action**: User views invoice
- **System Response**: Shows updated status and balance
- **User Experience**: Confirmed payment recording

### Success Criteria
- ✅ Payment recorded correctly
- ✅ Invoice status updated
- ✅ Balance calculated accurately
- ✅ Payment history maintained

---

## Journey 4: Sending Invoice Reminder

### User Goal
Remind client about overdue or pending invoice.

### Step-by-Step Journey

#### Step 1: Identify Invoice to Remind
- **User Action**: User views invoice list or details
- **System Response**: Shows invoice status
- **User Experience**: Clear invoice status

#### Step 2: Send Reminder
- **User Action**: User clicks "Remind" button
- **System Response**: 
  - Opens reminder composition dialog
  - Pre-fills invoice information
  - Allows message customization
- **User Experience**: Easy reminder sending

#### Step 3: Customize Reminder (Optional)
- **User Action**: User edits reminder message
- **System Response**: Shows preview
- **User Experience**: Customizable reminder

#### Step 4: Send Reminder
- **User Action**: User clicks "Send Reminder"
- **System Response**:
  - Sends reminder email
  - Shows confirmation
  - Updates reminder history
- **User Experience**: Reminder sent successfully

### Success Criteria
- ✅ Reminder sent to client
- ✅ Message is clear and professional
- ✅ Reminder tracked in history

---

## Journey 5: Viewing Invoice Details

### User Goal
Review complete invoice information.

### Step-by-Step Journey

#### Step 1: Access Invoice List
- **User Action**: User navigates to invoices page
- **System Response**: Displays invoice table
- **User Experience**: Complete invoice overview

#### Step 2: Open Invoice
- **User Action**: User clicks on invoice or "View" button
- **System Response**: Opens invoice details page
- **User Experience**: Full invoice view

#### Step 3: Review Invoice Information
- **User Action**: User reviews:
  - Invoice header (number, dates, client)
  - Line items
  - Totals (subtotal, discount, tax, total)
  - Payment history
  - Status
  - Notes
- **System Response**: Displays all invoice information
- **User Experience**: Complete invoice details

#### Step 4: Take Actions
- **User Action**: User can:
  - Edit invoice
  - Send invoice
  - Send reminder
  - Record payment
  - Delete invoice
- **System Response**: Provides action buttons
- **User Experience**: Easy invoice management

### Success Criteria
- ✅ All invoice information visible
- ✅ Actions are accessible
- ✅ Information is accurate

---

## Journey 6: Editing an Invoice

### User Goal
Update invoice information.

### Step-by-Step Journey

#### Step 1: Access Edit Mode
- **User Action**: User clicks "Edit" on invoice
- **System Response**: Opens invoice edit form
- **User Experience**: Editable invoice form

#### Step 2: Modify Invoice
- **User Action**: User updates:
  - Dates
  - Line items
  - Discount/tax
  - Notes
  - Payment method
- **System Response**: 
  - Validates changes
  - Recalculates totals
  - Shows preview
- **User Experience**: Easy editing

#### Step 3: Save Changes
- **User Action**: User clicks "Save"
- **System Response**:
  - Validates invoice
  - Updates invoice
  - Refreshes display
- **User Experience**: Changes saved successfully

### Success Criteria
- ✅ Invoice updated correctly
- ✅ Totals recalculated
- ✅ Changes saved

---

## Journey 7: Setting Up Recurring Invoice

### User Goal
Create automatically recurring invoices.

### Step-by-Step Journey

#### Step 1: Select Recurring Type
- **User Action**: User selects "Recurring Invoice"
- **System Response**: Proceeds to recurring setup
- **User Experience**: Recurring option

#### Step 2: Configure Recurring Settings
- **User Action**: User sets:
  - Frequency (Monthly, Bi-Monthly, Weekly)
  - Specific days
  - End date (optional)
- **System Response**: Validates recurring settings
- **User Experience**: Clear recurring configuration

#### Step 3: Set Up Initial Invoice
- **User Action**: User creates initial invoice
- **System Response**: Saves recurring invoice template
- **User Experience**: Recurring invoice created

#### Step 4: Automatic Generation
- **User Action**: User waits for next cycle
- **System Response**: Automatically generates invoice on schedule
- **User Experience**: Automated invoicing

### Success Criteria
- ✅ Recurring invoice configured
- ✅ Invoices generate automatically
- ✅ Settings are correct

---

## User Personas

### Persona 1: Service Provider (Session Invoicing)
- **Goal**: Invoice completed sessions
- **Journey**: Calendar → Select Sessions → Create Invoice → Send
- **Pain Points**: Selecting sessions, calculating totals
- **Success**: Quick invoice from sessions

### Persona 2: Freelancer (Manual Invoicing)
- **Goal**: Create custom invoices
- **Journey**: Invoices → Manual Invoice → Add Items → Send
- **Pain Points**: Item entry, calculations
- **Success**: Professional custom invoices

### Persona 3: Business Owner (Payment Tracking)
- **Goal**: Track invoice payments
- **Journey**: Invoices → View Invoice → Record Payment → Track Status
- **Pain Points**: Payment recording, status tracking
- **Success**: Complete payment tracking

---

## Key User Experience Principles

1. **Step-by-Step Creation**: Clear invoice creation flow
2. **Flexible Options**: Multiple invoice types
3. **Quick Actions**: Easy send, remind, payment recording
4. **Clear Status**: Visual invoice status indicators
5. **Payment Tracking**: Complete payment history
6. **Professional Output**: High-quality invoice preview

---

## Metrics to Track

- Invoice creation completion rate
- Average time to create invoice
- Payment recording frequency
- Invoice send rate
- Reminder send rate
- Invoice status distribution
- Payment collection rate

---

## Future Enhancements

- PDF generation and download
- Email integration (SMTP)
- Online payment processing (Stripe, PayPal)
- Invoice templates customization
- Multi-currency support
- Invoice approval workflow
- Invoice attachments
- Client portal for invoice viewing
- Automated payment reminders
- Invoice aging reports

