# Invoices Module Documentation

## Overview
The Invoices Module provides comprehensive invoice creation, management, tracking, and payment processing functionality. It supports multiple invoice types, payment methods, recurring invoices, and invoice templates.

## Features

### 1. Invoice List Management
- **Purpose**: View and manage all invoices
- **Location**: `/app/invoices/page.tsx`
- **API Endpoint**: `/api/invoices`
- **Service**: `invoiceService.getAllInvoices()`

**Invoice List Features**:
- Display all invoices in sortable table
- Filter by status (Created, Sent, Paid, Overdue)
- Search by invoice number, client name
- Sort by date, amount, status
- Pagination support
- Quick actions (View, Edit, Delete, Send, Remind)

**Invoice Information Displayed**:
- Invoice Number
- Client Name
- Issue Date
- Due Date
- Total Amount
- Status
- Payment Method

### 2. Create New Invoice
- **Purpose**: Create invoices through a multi-step wizard
- **Location**: `/app/invoices/new/page.tsx`
- **Service**: `invoiceService.createInvoice()`

**Invoice Creation Flow**:

#### Step 1: Select Invoice Type
- **Location**: `/app/invoices/select-type/page.tsx`
- **Options**:
  - **Session-based Invoice**: Create from selected sessions
  - **Manual Invoice**: Create from scratch with custom items
  - **Recurring Invoice**: Set up automatic recurring invoices

#### Step 2: Select Client
- **Location**: `/app/invoices/select-client/page.tsx`
- **Features**:
  - Client search and selection
  - Client information display
  - Client selection validation

#### Step 3: Select Sessions (for session-based invoices)
- **Location**: `/app/invoices/select-sessions/page.tsx`
- **Features**:
  - List of uninvoiced sessions for selected client
  - Session selection (checkbox)
  - Session details (date, duration, rate, amount)
  - Total calculation preview
  - Filter by date range

#### Step 4: Invoice Details
- **Location**: `/app/invoices/new/page.tsx`
- **Fields**:
  - Invoice Number (auto-generated or manual)
  - Issue Date
  - Due Date
  - Invoice Items (from sessions or manual)
  - Discount (amount or percentage)
  - Tax (amount or percentage)
  - Notes
  - Payment Method
  - Recurring Settings (if applicable)

### 3. Invoice Templates
- **Purpose**: Customize invoice appearance
- **Location**: `/app/components/InvoiceTemplateSelector.tsx`
- **Service**: Template management

**Template Options**:
- **Standard Template**: Default professional layout
- **Detailed Template**: Comprehensive item breakdown
- **Minimal Template**: Simple, clean design

**Template Customization** (Future):
- Logo upload
- Color scheme
- Custom fields
- Branding elements

### 4. Invoice Preview
- **Purpose**: Preview invoice before sending
- **Location**: `/app/invoices/preview/page.tsx`
- **Features**:
  - Full invoice preview
  - Print-friendly view
  - PDF generation (future)
  - Email preview

### 5. Invoice Details and Editing
- **Purpose**: View and edit invoice details
- **Location**: `/app/invoices/[id]/page.tsx`, `/app/invoices/[id]/edit/page.tsx`
- **API Endpoint**: `/api/invoices/[id]`
- **Service**: `invoiceService.getInvoiceById()`, `invoiceService.updateInvoice()`

**Invoice Details Display**:
- Complete invoice information
- Invoice items breakdown
- Payment history
- Status timeline
- Actions (Edit, Send, Remind, Record Payment, Delete)

**Edit Functionality**:
- Edit all invoice fields
- Add/remove invoice items
- Update amounts and dates
- Modify payment information
- Update status

### 6. Invoice Status Management
- **Purpose**: Track invoice lifecycle
- **Service**: `invoiceService.updateInvoice()`

**Status Types**:
- **Created**: Draft invoice, not yet sent
- **Sent**: Invoice sent to client
- **Paid**: Invoice fully paid
- **Overdue**: Past due date, not paid

**Status Transitions**:
- Created → Sent (when sent to client)
- Sent → Paid (when payment recorded)
- Sent → Overdue (when past due date)

### 7. Payment Recording
- **Purpose**: Record payments against invoices
- **Location**: `/app/components/RecordPaymentDialog.tsx`
- **Service**: Payment recording

**Payment Information**:
- Payment Amount
- Payment Date
- Payment Method (PayPal, Venmo, Zelle, Bank Transfer)
- Reference/Transaction ID (optional)
- Notes (optional)

**Features**:
- Partial payment support
- Multiple payments per invoice
- Payment history tracking
- Automatic status updates
- Outstanding balance calculation

### 8. Invoice Actions

#### Send Invoice
- **Purpose**: Email invoice to client
- **Service**: Email integration
- **Features**:
  - Email template
  - Client email validation
  - Send confirmation
  - Delivery tracking (future)

#### Remind Invoice
- **Purpose**: Send payment reminder
- **Service**: Email integration
- **Features**:
  - Reminder email template
  - Automatic overdue reminders (future)
  - Reminder history

#### Delete Invoice
- **Purpose**: Remove invoice
- **Safety**: Confirmation dialog
- **Restrictions**: Cannot delete paid invoices (future)

### 9. Recurring Invoices
- **Purpose**: Automatically generate invoices on schedule
- **Location**: Invoice creation flow
- **Service**: Recurring invoice management

**Recurring Options**:
- **Frequency**: Monthly, Bi-Monthly, Weekly
- **Monthly**: Specific day of month
- **Bi-Monthly**: Two specific days
- **Weekly**: Specific day of week

**Recurring Features**:
- Automatic generation
- End date option
- Pause/resume recurring
- Edit recurring settings
- Recurring invoice history

### 10. Invoice KPIs
- **Purpose**: Display invoice metrics
- **Location**: `/app/components/invoices/KPICards.tsx`
- **API Endpoint**: `/api/invoices/kpi`
- **Service**: `invoiceService.getInvoiceKPIData()`

**KPI Metrics**:
- Total Invoices
- Paid Invoices Count
- Total Open Amount
- Total Paid Amount

## Data Structure

### Invoice Type (`/app/types/invoice.ts`)
```typescript
type Invoice = {
  id: string
  clientId: string
  clientName: string
  invoiceNumber: string
  issueDate: string
  dueDate: string
  items: InvoiceItem[]
  subtotal: number
  discount: number
  tax: number
  total: number
  notes: string
  status: 'Created' | 'Sent' | 'Paid' | 'Overdue'
  paymentMethod: PaymentMethod
  payments: Payment[]
  recurring: RecurringInfo
  sessionIds: string[]
}
```

### InvoiceItem Type
```typescript
type InvoiceItem = {
  id: string
  description: string
  quantity: number
  rate: number
  amount: number
  sessionId?: string
}
```

### Payment Type
```typescript
type Payment = {
  id: string
  amount: number
  date: string
  method: PaymentMethod
}
```

### RecurringInfo Type
```typescript
type RecurringInfo = {
  isRecurring: boolean
  frequency?: 'Monthly' | 'Bi-Monthly' | 'Weekly'
  monthlyDay?: number
  biMonthlyDays?: [number, number]
  weeklyDay?: number
}
```

## API Endpoints

### GET `/api/invoices`
- **Response**: Array of Invoice objects
- **Query Parameters**:
  - `status`: Filter by status
  - `clientId`: Filter by client
  - `page`: Page number

### GET `/api/invoices/[id]`
- **Response**: Single Invoice object

### POST `/api/invoices`
- **Request Body**: Invoice object (without id)
- **Response**: Created Invoice object

### PUT `/api/invoices/[id]`
- **Request Body**: Updated Invoice object
- **Response**: Updated Invoice object

### DELETE `/api/invoices/[id]`
- **Response**: Success confirmation

### GET `/api/invoices/kpi`
- **Response**: InvoiceKPIData object

### POST `/api/invoices/[id]/send`
- **Response**: Send confirmation

### POST `/api/invoices/[id]/remind`
- **Response**: Reminder confirmation

### POST `/api/invoices/[id]/payments`
- **Request Body**: Payment object
- **Response**: Updated Invoice with payment

## Service Layer

### `invoiceService` (`/app/services/invoiceService.ts`)

**Methods**:
- `getAllInvoices()`: Fetch all invoices
- `getPaginatedInvoices(page)`: Fetch paginated invoices
- `getInvoiceById(id)`: Fetch single invoice
- `getInvoicesByClient(clientId)`: Fetch client's invoices
- `getInvoicesByStatus(status)`: Filter by status
- `createInvoice(invoice)`: Create new invoice
- `updateInvoice(id, invoice)`: Update invoice
- `deleteInvoice(id)`: Delete invoice
- `getInvoiceKPIData()`: Fetch KPI metrics
- `getInvoicesForPeriod(timeframe, period)`: Fetch for reporting

## Hooks

### `useInvoices` (`/app/hooks/useInvoices.ts`)
- Manages invoice list state
- Handles invoice CRUD operations
- Manages loading and error states
- Provides filtering and sorting

## Components

1. **InvoicesPage** (`/app/invoices/page.tsx`): Main invoices page
2. **InvoiceTable** (`/app/components/invoices/InvoiceTable.tsx`): Invoice list table
3. **NewInvoicePage** (`/app/invoices/new/page.tsx`): Invoice creation
4. **SelectTypePage** (`/app/invoices/select-type/page.tsx`): Invoice type selection
5. **SelectClientPage** (`/app/invoices/select-client/page.tsx`): Client selection
6. **SelectSessionsPage** (`/app/invoices/select-sessions/page.tsx`): Session selection
7. **InvoiceDetails** (`/app/invoices/[id]/InvoiceDetails.tsx`): Invoice details view
8. **InvoicePreview** (`/app/invoices/preview/page.tsx`): Invoice preview
9. **RecordPaymentDialog** (`/app/components/RecordPaymentDialog.tsx`): Payment recording
10. **InvoiceTemplateSelector** (`/app/components/InvoiceTemplateSelector.tsx`): Template selection
11. **KPICards** (`/app/components/invoices/KPICards.tsx`): Invoice KPIs

## Invoice Creation Workflow

### Session-Based Invoice
1. Select "Session-based Invoice"
2. Select client
3. Select sessions to invoice
4. Review session details and amounts
5. Configure invoice details (dates, discount, tax, notes)
6. Preview invoice
7. Save and send

### Manual Invoice
1. Select "Manual Invoice"
2. Select client
3. Add invoice items manually
4. Configure invoice details
5. Preview invoice
6. Save and send

### Recurring Invoice
1. Select "Recurring Invoice"
2. Select client
3. Configure recurring settings
4. Set up initial invoice
5. Save recurring invoice
6. System generates invoices automatically

## Business Logic

### Invoice Number Generation
- Auto-generated format: INV-XXX
- Sequential numbering
- Manual override option
- Uniqueness validation

### Amount Calculations
- Subtotal: Sum of all items
- Discount: Applied to subtotal
- Tax: Applied to (subtotal - discount)
- Total: Subtotal - Discount + Tax

### Payment Processing
- Partial payments supported
- Outstanding balance = Total - Sum of payments
- Status updates automatically:
  - Paid: When outstanding balance = 0
  - Overdue: When past due date and not paid

### Session Integration
- Sessions marked as "Invoiced" when added
- Cannot add same session to multiple invoices
- Session reference stored in invoice

## Integration Points

1. **Clients Module**: Client selection and information
2. **Calendar Module**: Session selection for invoices
3. **Rates Module**: Rate application to invoice items
4. **Dashboard Module**: Invoice KPIs and summaries
5. **Reports Module**: Invoice data for reporting
6. **Email Service**: Invoice sending and reminders

## Role-Based Features

### Free Users
- Basic invoice creation
- Limited invoice history
- Standard templates

### Paid Users
- All invoice features
- Recurring invoices
- Custom templates
- Advanced reporting

### Admin Users
- View all users' invoices
- System-wide invoice management
- Invoice analytics

## Error Handling

- Validation errors: Field-specific messages
- Network errors: Display error, retry option
- Payment errors: Transaction failure handling
- Duplicate invoice numbers: Prevent creation
- Session already invoiced: Warn user

## Future Enhancements

1. PDF generation and download
2. Email integration (SMTP)
3. Online payment processing (Stripe, PayPal)
4. Invoice templates customization
5. Multi-currency support
6. Invoice approval workflow
7. Invoice attachments
8. Client portal for invoice viewing
9. Automated payment reminders
10. Invoice aging reports
11. Tax calculation automation
12. Invoice numbering customization
13. Batch invoice operations
14. Invoice archiving
15. Invoice versioning
16. Credit notes/refunds
17. Invoice estimates/quotes
18. Invoice line item templates
19. Automatic tax calculation
20. Invoice approval workflow

## Dependencies

- React 18
- Next.js 14
- @tanstack/react-query (data fetching)
- @tanstack/react-table (table functionality)
- React Hook Form (form management)
- Zod (validation)
- jsPDF (PDF generation, future)
- Lucide React (icons)

## Testing Considerations

- Unit tests for invoice calculations
- Integration tests for invoice CRUD
- Component tests for invoice forms
- E2E tests for invoice creation flow
- Payment processing tests
- Recurring invoice tests
- Validation tests for invoice fields

