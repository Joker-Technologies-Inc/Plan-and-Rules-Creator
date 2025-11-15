# Clients Management Module Documentation

## Overview
The Clients Management Module provides comprehensive functionality for managing client information, contacts, assignments, and rates. It serves as the central hub for all client-related operations in the application.

## Features

### 1. Client List Management
- **Purpose**: View, search, and manage all clients
- **Location**: `/app/clients/page.tsx`
- **API Endpoint**: `/api/clients`
- **Service**: `clientService.getClients()`

**Functionality**:
- Display all clients in a searchable, sortable table
- Client status indicators (Active/Inactive)
- Quick actions (Edit, Delete, View Details)
- Search and filter capabilities
- Pagination support

**Client Information Displayed**:
- Client Name
- Email Address
- Phone Number
- Status (Active/Inactive)
- Total Invoiced Amount
- Total Paid Amount
- Outstanding Balance

### 2. Add New Client
- **Purpose**: Create new client records
- **Location**: `/app/clients/NewContactForm.tsx`, `/app/components/clients/ClientDialog.tsx`
- **API Endpoint**: `/api/clients/add`
- **Service**: `clientService.addClient()`

**Form Fields**:
- Client Name (required)
- Email Address (required, validated)
- Phone Number (required, formatted)
- Status (Active/Inactive, default: Active)

**Validation**:
- Email format validation
- Phone number format validation
- Required field validation
- Duplicate email checking

**User Flow**:
1. Click "Add Client" button
2. Fill in client information form
3. Submit form
4. System creates client and first contact automatically
5. Redirect to client list or details

### 3. Edit Client
- **Purpose**: Update existing client information
- **Location**: `/app/components/clients/ClientDialog.tsx`
- **API Endpoint**: `/api/clients/[id]`
- **Service**: `clientService.updateClient()`

**Functionality**:
- Edit all client fields
- Update status
- Preserve contact relationships
- Validation on update

### 4. Delete Client
- **Purpose**: Remove client records
- **Location**: Client management components
- **API Endpoint**: `/api/clients/[id]` (DELETE)
- **Service**: `clientService.deleteClient()`

**Safety Features**:
- Confirmation dialog before deletion
- Check for associated invoices/sessions
- Prevent deletion if active relationships exist
- Soft delete option (future enhancement)

### 5. Contact Management
- **Purpose**: Manage multiple contacts per client
- **Location**: `/app/components/ContactsSubTable.tsx`
- **API Endpoint**: `/api/clients/[id]/contacts`
- **Service**: `clientService.getContacts()`, `clientService.addContact()`, etc.

**Contact Features**:
- Multiple contacts per client
- Add new contacts
- Edit existing contacts
- Delete contacts
- Primary contact designation

**Contact Information**:
- Contact Name
- Email Address
- Phone Number
- Relationship to client (future enhancement)

### 6. Client Search and Filtering
- **Purpose**: Quickly find specific clients
- **Location**: `/app/components/clients/SearchBar.tsx`
- **Service**: Client-side filtering

**Search Capabilities**:
- Search by name
- Search by email
- Search by phone number
- Real-time search results
- Case-insensitive search

**Filter Options**:
- Filter by status (Active/Inactive)
- Filter by payment status (future)
- Sort by name, date added, total invoiced

### 7. Client Rates Management
- **Purpose**: Manage pricing rates for clients
- **Location**: `/app/components/ClientRates.tsx`
- **Service**: `rateService` integration

**Rate Features**:
- Assign predefined rates to clients
- Custom rate per client
- Rate history tracking
- Rate type support (hourly, fixed, package)

### 8. Client Assignment
- **Purpose**: Assign clients to sessions/invoices
- **Location**: `/app/components/ClientAssignment.tsx`
- **Service**: Integration with sessions and invoices

**Functionality**:
- Select client for new session
- Assign client to invoice
- Quick client selection dropdown
- Client search in assignment dialogs

## Data Structure

### Client Type (`/app/types/client.ts`)
```typescript
type Client = {
  id: string
  name: string
  email: string
  phone: string
  status: 'Active' | 'Inactive'
  contacts: Contact[]
  totalInvoiced?: number
  totalPaid?: number
  outstandingBalance?: number
}
```

### Contact Type
```typescript
type Contact = {
  id: string
  name: string
  email: string
  phone: string
}
```

## API Endpoints

### GET `/api/clients`
- **Response**: Array of Client objects
- **Query Parameters**: 
  - `search`: Search term
  - `status`: Filter by status
  - `page`: Page number for pagination

### POST `/api/clients/add`
- **Request Body**: 
```typescript
{
  name: string,
  email: string,
  phone: string,
  status: 'Active' | 'Inactive'
}
```
- **Response**: Created Client object

### GET `/api/clients/[id]`
- **Response**: Single Client object with contacts

### PUT `/api/clients/[id]`
- **Request Body**: Updated Client object
- **Response**: Updated Client object

### DELETE `/api/clients/[id]`
- **Response**: Success confirmation

### GET `/api/clients/[id]/contacts`
- **Response**: Array of Contact objects

### POST `/api/clients/[id]/contacts`
- **Request Body**: Contact object (without id)
- **Response**: Created Contact object

### PUT `/api/clients/[id]/contacts/[contactId]`
- **Request Body**: Updated Contact object
- **Response**: Updated Contact object

### DELETE `/api/clients/[id]/contacts/[contactId]`
- **Response**: Success confirmation

## Service Layer

### `clientService` (`/app/services/clientService.ts`)

**Methods**:
- `getClients()`: Fetch all clients
- `addClient(client)`: Create new client
- `updateClient(client)`: Update existing client
- `deleteClient(id)`: Delete client
- `getContacts(clientId)`: Get contacts for a client
- `addContact(clientId, contact)`: Add contact to client
- `updateContact(clientId, contact)`: Update contact
- `deleteContact(clientId, contactId)`: Delete contact
- `getClientsForPeriod(timeframe, period)`: Get clients for reporting period
- `getAllClients()`: Get all clients with financial data

## Hooks

### `useClients` (`/app/hooks/useClients.ts`)
- Manages client list state
- Handles client CRUD operations
- Manages loading and error states
- Provides search and filter functionality

### `useContacts` (`/app/hooks/useContacts.ts`)
- Manages contact operations
- Handles contact CRUD for specific clients
- Manages contact list state

### `useClientManagement` (`/app/hooks/useClientManagement.ts`)
- High-level client management operations
- Combines client and contact operations
- Manages complex client workflows

## Components

1. **ClientsPage** (`/app/clients/page.tsx`): Main clients page
2. **ClientList** (`/app/components/clients/ClientList.tsx`): Client table/list view
3. **ClientDialog** (`/app/components/clients/ClientDialog.tsx`): Add/Edit client dialog
4. **SearchBar** (`/app/components/clients/SearchBar.tsx`): Client search component
5. **ClientSkeleton** (`/app/components/clients/ClientSkeleton.tsx`): Loading skeleton
6. **ContactsSubTable** (`/app/components/ContactsSubTable.tsx`): Contacts management table
7. **ClientRates** (`/app/components/ClientRates.tsx`): Client rate management
8. **ClientAssignment** (`/app/components/ClientAssignment.tsx`): Client selection component
9. **NewContactForm** (`/app/clients/NewContactForm.tsx`): New contact form

## User Experience Features

### Search and Filter
- Real-time search as you type
- Instant filter application
- Clear filters button
- Search highlights matching text

### Data Table Features
- Sortable columns
- Pagination
- Row selection
- Expandable rows for contacts
- Responsive design

### Form Validation
- Real-time field validation
- Error messages
- Success confirmations
- Loading states during submission

### Loading States
- Skeleton loaders
- Progress indicators
- Optimistic updates

## Integration Points

1. **Invoices Module**: Client selection for invoices, client financial data
2. **Calendar Module**: Client assignment for sessions
3. **Reports Module**: Client data for reporting
4. **Dashboard Module**: Active client count
5. **Rates Module**: Client-specific rate management

## Role-Based Features

### Free Users
- Limited to 3 active clients
- Warning when approaching limit
- Upgrade prompts
- Basic client management

### Paid Users
- Unlimited clients
- All features available
- Advanced client management

### Admin Users
- View all users' clients
- System-wide client management
- Client analytics

## Business Logic

### Client Status Management
- Active clients can be assigned to sessions
- Inactive clients are hidden from active lists
- Status change affects related data

### Contact Auto-Creation
- When a client is created, a primary contact is automatically created
- Primary contact uses client's information
- Additional contacts can be added manually

### Financial Data Aggregation
- Total invoiced: Sum of all invoices for client
- Total paid: Sum of all payments received
- Outstanding balance: Total invoiced - Total paid

## Error Handling

- Network errors: Display error message, retry option
- Validation errors: Field-specific error messages
- Duplicate email: Prevent creation, show error
- Not found errors: 404 handling for missing clients

## Future Enhancements

1. Client import/export (CSV, Excel)
2. Client notes and tags
3. Client communication history
4. Client document management
5. Client portal access
6. Client activity timeline
7. Bulk client operations
8. Client segmentation
9. Custom client fields
10. Client merge functionality
11. Client archiving
12. Advanced search with multiple criteria
13. Client groups/segments
14. Client referral tracking

## Dependencies

- React 18
- Next.js 14
- @tanstack/react-query (data fetching)
- @tanstack/react-table (table functionality)
- React Hook Form (form management)
- Zod (validation)
- Lucide React (icons)

## Testing Considerations

- Unit tests for client CRUD operations
- Integration tests for API endpoints
- Component tests for UI interactions
- E2E tests for client workflows
- Validation tests for form inputs
- Search and filter functionality tests
- Contact management tests

