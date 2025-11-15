# Reports Module Documentation

## Overview
The Reports Module provides comprehensive reporting and analytics functionality for clients and invoices. It allows users to generate detailed reports, analyze business performance, and export data for external analysis.

## Features

### 1. Reports Dashboard
- **Purpose**: Central hub for all reporting features
- **Location**: `/app/reports/page.tsx`
- **Component**: `/app/components/reports/ReportsContent.tsx`

**Dashboard Features**:
- Report type selection
- Time period selection
- Quick report generation
- Report preview
- Export options

### 2. Client Reports
- **Purpose**: Generate detailed reports on client activity and financials
- **Location**: `/app/components/reports/ClientTable.tsx`
- **API Endpoint**: `/api/reports/clients`
- **Service**: `clientService.getClientsForPeriod()`

**Client Report Data**:
- Client Name
- Email Address
- Phone Number
- Status (Active/Inactive)
- Total Invoiced Amount
- Total Paid Amount
- Outstanding Balance
- Number of Invoices
- Number of Sessions
- Date Range Filtering

**Report Features**:
- Filter by time period (Week, Month, Year)
- Filter by client status
- Sort by any column
- Export to CSV/Excel
- Print report
- Summary statistics

### 3. Invoice Reports
- **Purpose**: Generate detailed reports on invoice performance
- **Location**: `/app/components/reports/InvoiceTable.tsx`
- **API Endpoint**: `/api/reports/invoices`
- **Service**: `invoiceService.getInvoicesForPeriod()`

**Invoice Report Data**:
- Invoice Number
- Client Name
- Issue Date
- Due Date
- Total Amount
- Status (Created, Sent, Paid, Overdue)
- Payment Method
- Days Overdue (for overdue invoices)
- Payment History

**Report Features**:
- Filter by time period
- Filter by status
- Filter by payment method
- Group by client
- Summary totals
- Export functionality

### 4. Time Period Selection
- **Purpose**: Filter reports by specific time periods
- **Component**: Time period selector

**Available Periods**:
- **Week**: Select specific week (W1, W2, etc.)
- **Month**: Select specific month (1-12)
- **Year**: Select specific year

**Period Format**:
- Week: `YYYY-WX` (e.g., `2025-W1`)
- Month: `YYYY-MM` (e.g., `2025-01`)
- Year: `YYYY` (e.g., `2025`)

### 5. Report Summary Statistics
- **Purpose**: Display aggregated metrics for selected period
- **Service**: `reportService.getReportData()`

**Summary Metrics**:
- Total Revenue
- Uninvoiced Total
- Total Unpaid
- Total Invoices Count
- Average Invoice Amount
- Payment Rate
- Outstanding Balance

### 6. Report Export
- **Purpose**: Export reports to external formats
- **Component**: Export functionality

**Export Formats** (Future):
- CSV (Comma-separated values)
- Excel (XLSX)
- PDF
- JSON

**Export Features**:
- Select columns to export
- Custom date ranges
- Filtered data export
- Scheduled exports (future)

### 7. Report Filtering and Sorting
- **Purpose**: Customize report views
- **Component**: Filter and sort controls

**Filtering Options**:
- Date range
- Client status
- Invoice status
- Payment method
- Amount range
- Custom filters (future)

**Sorting Options**:
- Sort by any column
- Ascending/Descending
- Multi-column sorting (future)

## Data Structure

### ReportData Type (`/app/types/report.ts`)
```typescript
type ReportData = {
  totalRevenue: number
  uninvoicedTotal: number
  totalUnpaid: number
  totalInvoices: number
}
```

### ReportTimeframe Type
```typescript
type ReportTimeframe = 'week' | 'month' | 'year'
```

## API Endpoints

### GET `/api/reports/clients`
- **Query Parameters**:
  - `timeframe`: 'week' | 'month' | 'year'
  - `period`: Period identifier (e.g., '2025-W1', '2025-01', '2025')
- **Response**: Array of Client objects with financial data

### GET `/api/reports/invoices`
- **Query Parameters**:
  - `timeframe`: 'week' | 'month' | 'year'
  - `period`: Period identifier
  - `status`: Filter by status (optional)
- **Response**: Array of Invoice objects

### GET `/api/reports`
- **Query Parameters**:
  - `timeframe`: Report timeframe
- **Response**: ReportData object with summary statistics

## Service Layer

### `reportService` (`/app/services/reportService.ts`)

**Methods**:
- `getReportData(timeframe)`: Fetch summary report data
- Additional methods for specific report types (future)

### `clientService` (for client reports)
- `getClientsForPeriod(timeframe, period)`: Get clients with financial data for period
- `getAllClients()`: Get all clients with financial data

### `invoiceService` (for invoice reports)
- `getInvoicesForPeriod(timeframe, period)`: Get invoices for specific period

## Hooks

### `useReportData` (`/app/hooks/useReportData.ts`)
- Manages report data fetching
- Handles time period selection
- Manages filtering and sorting
- Provides export functionality

## Components

1. **ReportsPage** (`/app/reports/page.tsx`): Main reports page
2. **ReportsContent** (`/app/components/reports/ReportsContent.tsx`): Reports dashboard
3. **ClientTable** (`/app/components/reports/ClientTable.tsx`): Client report table
4. **InvoiceTable** (`/app/components/reports/InvoiceTable.tsx`): Invoice report table
5. **ReportsSkeleton** (`/app/components/reports/ReportsSkeleton.tsx`): Loading skeleton
6. **ExportButton** (`/app/components/ExportButton.tsx`): Export functionality

## Report Generation Workflow

### Client Report Generation
1. Navigate to Reports page
2. Select "Client Reports" tab
3. Select time period (week/month/year)
4. Select specific period
5. System fetches client data for period
6. Display report table with data
7. Apply filters/sorting if needed
8. Export or print report

### Invoice Report Generation
1. Navigate to Reports page
2. Select "Invoice Reports" tab
3. Select time period
4. Select specific period
5. Optionally filter by status
6. System fetches invoice data for period
7. Display report table with data
8. Apply filters/sorting if needed
9. Export or print report

## Business Logic

### Date Range Calculation
- **Week**: Start of week (Monday) to end of week (Sunday)
- **Month**: First day of month to last day of month
- **Year**: January 1 to December 31

### Financial Aggregation
- Total Invoiced: Sum of all invoice totals
- Total Paid: Sum of all payments
- Outstanding Balance: Total Invoiced - Total Paid
- Uninvoiced Total: Sum of uninvoiced sessions

### Period Filtering
- Filters data based on issue date (invoices)
- Filters data based on activity date (clients)
- Handles timezone considerations
- Supports custom date ranges (future)

## Integration Points

1. **Clients Module**: Client data for reports
2. **Invoices Module**: Invoice data for reports
3. **Calendar Module**: Session data for reports
4. **Dashboard Module**: Shared KPI calculations

## Role-Based Features

### Free Users
- Basic reports
- Limited date range
- Standard export formats

### Paid Users
- All report features
- Extended date ranges
- Advanced export options
- Custom report builder (future)

### Admin Users
- System-wide reports
- All users' data aggregation
- Advanced analytics

## User Experience Features

### Report Loading
- Loading skeletons
- Progress indicators
- Smooth data transitions

### Data Visualization
- Summary cards
- Charts and graphs (future)
- Trend indicators (future)

### Responsive Design
- Mobile-optimized tables
- Scrollable data views
- Touch-friendly interactions

## Error Handling

- Network errors: Display error, retry option
- No data: Show empty state message
- Invalid period: Validation and error message
- Export errors: Handle gracefully

## Future Enhancements

1. Custom report builder
2. Scheduled report generation
3. Email report delivery
4. Advanced data visualization (charts, graphs)
5. Comparative reports (period over period)
6. Revenue forecasting
7. Client lifetime value reports
8. Payment trend analysis
9. Session utilization reports
10. Custom date ranges
11. Report templates
12. Saved report configurations
13. Multi-user report sharing
14. Real-time report updates
15. Drill-down capabilities
16. Pivot table functionality
17. Report scheduling
18. Automated report generation
19. Report annotations
20. Interactive dashboards

## Dependencies

- React 18
- Next.js 14
- @tanstack/react-query (data fetching)
- @tanstack/react-table (table functionality)
- jsPDF (PDF export, future)
- jspdf-autotable (PDF tables, future)
- Recharts (charts, future)
- Lucide React (icons)

## Testing Considerations

- Unit tests for report calculations
- Integration tests for report API endpoints
- Component tests for report tables
- E2E tests for report generation flow
- Date range calculation tests
- Export functionality tests
- Filter and sort tests

