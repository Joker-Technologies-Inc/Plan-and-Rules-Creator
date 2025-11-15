# Dashboard Module Documentation

## Overview
The Dashboard Module provides a comprehensive overview of business metrics, recent activities, and key performance indicators (KPIs). It serves as the central hub for users to monitor their business performance at a glance.

## Features

### 1. Key Performance Indicators (KPIs)
- **Purpose**: Display critical business metrics
- **Location**: `/app/dashboard/page.tsx`, `/app/components/dashboard/DashboardContent.tsx`
- **API Endpoint**: `/api/dashboard/kpi`
- **Service**: `dashboardService.getKPIData()`

**KPI Cards**:

#### a. Total Revenue
- **Metric**: Total revenue amount
- **Display**: Currency formatted amount
- **Additional Info**: Percentage change from previous period
- **Icon**: DollarSign icon
- **Data Source**: Aggregated from invoices and payments

#### b. Upcoming Sessions
- **Metric**: Count of upcoming sessions
- **Display**: Total count
- **Additional Info**: Number of sessions scheduled for today
- **Icon**: Calendar icon
- **Data Source**: Calendar/time records with future dates

#### c. Active Clients
- **Metric**: Number of active clients
- **Display**: Client count
- **Additional Info**: 
  - Free users: Remaining client slots (e.g., "1 slot remaining")
  - Paid users: "Unlimited clients"
- **Icon**: Users icon
- **Data Source**: Client database with active status

**Technical Details**:
- Real-time data updates
- Loading skeleton states
- Error handling for failed API calls
- Responsive grid layout (3 columns on desktop, stacked on mobile)

### 2. Recent Activity Feed
- **Purpose**: Display recent business activities
- **Location**: `/app/components/dashboard/DashboardContent.tsx`
- **API Endpoint**: `/api/dashboard/recent-activity`
- **Service**: `dashboardService.getRecentActivity()`

**Activity Types**:
- **Session**: New session bookings, completed sessions
- **Invoice**: Invoice creation, payments, reminders
- **Client**: New client additions, client updates

**Activity Display**:
- Activity description
- Timestamp (relative time format)
- Activity type icon
- Chronological ordering (newest first)

**Features**:
- Real-time updates
- Scrollable list
- Activity type filtering (future enhancement)
- Click to view details (future enhancement)

### 3. Weekly Earnings Chart
- **Purpose**: Visualize earnings trends over the week
- **Location**: `/app/components/dashboard/DashboardContent.tsx`
- **API Endpoint**: `/api/dashboard/weekly-earnings`
- **Service**: `dashboardService.getWeeklyEarnings()`

**Chart Features**:
- Bar/line chart visualization
- Daily earnings breakdown (Mon-Sun)
- Currency formatted values
- Interactive tooltips
- Responsive design

**Data Points**:
- Monday earnings
- Tuesday earnings
- Wednesday earnings
- Thursday earnings
- Friday earnings
- Saturday earnings
- Sunday earnings

### 4. Summarized Invoice Table
- **Purpose**: Quick overview of recent invoices
- **Location**: `/app/components/dashboard/SummarizedInvoiceTable.tsx`
- **Data Source**: Dashboard service aggregated invoices

**Table Columns**:
- Invoice Number
- Client Name
- Issue Date
- Due Date
- Total Amount
- Status (Created, Sent, Paid, Overdue)
- Actions (Send, Remind, View)

**Actions**:
- **Send Invoice**: Email invoice to client
- **Remind Invoice**: Send payment reminder
- **View Details**: Navigate to invoice detail page

**Status Indicators**:
- Color-coded status badges
- Visual distinction for overdue invoices
- Payment status indicators

## Data Flow

### Data Fetching
1. Component mounts
2. Multiple API calls in parallel:
   - KPI data
   - Recent activity
   - Weekly earnings
   - Recent invoices
3. Data aggregation and processing
4. UI updates with loading states
5. Error handling and fallback UI

### State Management
- Uses React Query for data fetching and caching
- Global state context for user role
- Local component state for UI interactions

## API Endpoints

### GET `/api/dashboard/kpi`
- **Response**: 
```typescript
{
  totalRevenue: { amount: number, percentageChange: number },
  upcomingSessions: { count: number, todayCount: number },
  activeClients: { count: number, remainingSlots?: number }
}
```

### GET `/api/dashboard/recent-activity`
- **Response**: Array of RecentActivity objects
```typescript
{
  id: string,
  type: 'session' | 'invoice' | 'client',
  description: string,
  date: string (ISO format)
}[]
```

### GET `/api/dashboard/weekly-earnings`
- **Response**: Array of WeeklyEarning objects
```typescript
{
  day: 'Mon' | 'Tue' | 'Wed' | 'Thu' | 'Fri' | 'Sat' | 'Sun',
  amount: number
}[]
```

## Service Layer

### `dashboardService` (`/app/services/dashboardService.ts`)

**Methods**:
- `getKPIData()`: Fetch KPI metrics
- `getRecentActivity()`: Fetch recent activities
- `getWeeklyEarnings()`: Fetch weekly earnings data
- `getAllDashboardData()`: Fetch all dashboard data in one call

## Hooks

### `useDashboardData` (`/app/hooks/useDashboardData.ts`)
- Manages dashboard data fetching
- Handles loading states
- Manages error states
- Provides data refresh functionality

## Components

1. **DashboardPage** (`/app/dashboard/page.tsx`): Main dashboard page wrapper
2. **DashboardContent** (`/app/components/dashboard/DashboardContent.tsx`): Main dashboard content
3. **KPICard** (`/app/components/KPICard.tsx`): Individual KPI card component
4. **RecentActivityCard** (`/app/components/dashboard/RecentActivityCard.tsx`): Activity feed component
5. **WeeklyEarningsCard** (`/app/components/dashboard/WeeklyEarningsCard.tsx`): Earnings chart component
6. **SummarizedInvoiceTable** (`/app/components/dashboard/SummarizedInvoiceTable.tsx`): Invoice summary table
7. **DashboardSkeleton** (`/app/components/dashboard/DashboardSkeleton.tsx`): Loading skeleton

## Type Definitions

### KPIData (`/app/types/dashboard.ts`)
```typescript
type KPIData = {
  totalRevenue: { amount: number, percentageChange: number },
  upcomingSessions: { count: number, todayCount: number },
  activeClients: { count: number, remainingSlots?: number }
}
```

### RecentActivity (`/app/types/recentActivity.ts`)
```typescript
type RecentActivity = {
  id: string,
  type: 'session' | 'invoice' | 'client',
  description: string,
  date: string
}
```

### WeeklyEarning (`/app/types/weeklyEarning.ts`)
```typescript
type WeeklyEarning = {
  day: 'Mon' | 'Tue' | 'Wed' | 'Thu' | 'Fri' | 'Sat' | 'Sun',
  amount: number
}
```

## User Experience Features

### Loading States
- Skeleton loaders for all sections
- Smooth transitions when data loads
- Progressive loading (show data as it arrives)

### Error Handling
- Graceful error messages
- Retry functionality
- Fallback UI for failed requests

### Responsive Design
- Mobile-first design
- Adaptive grid layouts
- Touch-friendly interactions
- Optimized for all screen sizes

### Performance Optimizations
- Data caching with React Query
- Parallel API calls
- Lazy loading for charts
- Optimized re-renders

## Role-Based Features

### Free Users
- Limited client count display
- Remaining slots indicator
- Basic dashboard features

### Paid Users
- Unlimited clients indicator
- Full dashboard access
- Advanced analytics (future)

### Admin Users
- System-wide metrics
- User management access
- Admin panel navigation

## Integration Points

1. **Invoices Module**: Invoice data and actions
2. **Calendar Module**: Session data and upcoming appointments
3. **Clients Module**: Client count and activity
4. **Reports Module**: Historical data for trends

## Future Enhancements

1. Customizable dashboard widgets
2. Date range filtering
3. Export dashboard data
4. Real-time notifications
5. Advanced analytics and insights
6. Comparison with previous periods
7. Goal tracking
8. Revenue forecasting
9. Client activity heatmap
10. Custom KPI configuration

## Dependencies

- React 18
- Next.js 14
- @tanstack/react-query (data fetching)
- Recharts (chart visualization)
- Lucide React (icons)
- Tailwind CSS (styling)

## Testing Considerations

- Unit tests for KPI calculations
- Integration tests for API endpoints
- Component tests for UI rendering
- E2E tests for user interactions
- Performance tests for data loading
- Accessibility tests for screen readers

