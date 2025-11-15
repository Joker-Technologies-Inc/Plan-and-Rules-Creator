# Settings Module Documentation

## Overview
The Settings Module provides comprehensive configuration options for billing, notifications, and application preferences. It allows users to customize their account settings, manage subscriptions, and configure notification preferences.

## Features

### 1. Settings Dashboard
- **Purpose**: Central hub for all settings
- **Location**: `/app/settings/page.tsx`
- **Features**:
  - Settings category navigation
  - Quick access to common settings
  - Settings overview

**Settings Categories**:
- Billing Settings
- Notification Settings
- General Settings (future)
- Privacy Settings (future)
- Security Settings (future)

### 2. Billing Settings
- **Purpose**: Manage subscription and payment information
- **Location**: `/app/settings/billing/page.tsx`
- **Service**: `billingService`

**Billing Features**:

#### a. Current Plan Display
- **Service**: `billingService.getCurrentPlan()`
- **Information Displayed**:
  - Plan Name (Free, Pro)
  - Plan Price
  - Plan Description
  - Plan Features List
  - Plan Status

**Plan Types**:
- **Free Plan**:
  - Price: $0
  - Features:
    - Up to 3 clients
    - Basic invoicing
    - Calendar management
    - Email support
- **Pro Plan**:
  - Price: $8/month
  - Features:
    - Unlimited clients
    - Priority support
    - Custom branding
    - Analytics dashboard

#### b. Plan Management
- **Service**: `billingService.updatePlan()`
- **Features**:
  - Upgrade to Pro plan
  - Downgrade to Free plan
  - Plan comparison
  - Upgrade prompts

**Upgrade Flow**:
1. View current plan
2. Click "Upgrade" button
3. Review plan features
4. Enter payment information
5. Process payment
6. Activate new plan
7. Update account limits

#### c. Payment Method Management
- **Service**: `billingService.getPaymentMethod()`, `billingService.processPayment()`
- **Features**:
  - View current payment method
  - Update payment method
  - Add new payment method
  - Remove payment method
  - Payment method security

**Payment Method Information**:
- Card Type
- Last 4 digits
- Expiration Date
- Billing Address (future)

**Payment Processing**:
- Secure payment processing
- Payment validation
- Transaction confirmation
- Error handling

### 3. Notification Settings
- **Purpose**: Configure notification preferences
- **Location**: `/app/settings/notifications/page.tsx`
- **Service**: `notificationService`

**Notification Types**:

#### a. Invoice Reminders
- **Setting ID**: `invoice_reminders`
- **Description**: Receive reminders for invoices overdue by more than one month
- **Default**: Enabled
- **Features**:
  - Toggle on/off
  - Configure reminder frequency (future)
  - Set reminder thresholds (future)

#### b. Appointment Reminders
- **Setting ID**: `appointment_reminders`
- **Description**: Receive reminders for upcoming appointments
- **Default**: Enabled
- **Features**:
  - Toggle on/off
  - Configure reminder timing (future)
  - Set advance notice period (future)

#### c. New Message Alerts
- **Setting ID**: `new_message_alerts`
- **Description**: Get notified when you receive new messages
- **Default**: Enabled
- **Features**:
  - Toggle on/off
  - Notification channels (future)

**Notification Management**:
- Enable/disable individual notifications
- Bulk enable/disable (future)
- Notification channel selection (future)
- Notification frequency settings (future)

### 4. Settings Components
- **Location**: `/app/components/settings/`

**Available Components**:
- Billing settings forms
- Notification toggles
- Settings navigation
- Settings sections

## Data Structure

### BillingPlan Type (`/app/types/billing.ts`)
```typescript
type BillingPlan = {
  name: string
  price: string
  description: string
  features: string[]
}
```

### PaymentMethod Type
```typescript
type PaymentMethod = {
  type: 'credit_card' | 'debit_card' | 'paypal' | 'bank_transfer'
  last4: string
  expirationMonth: string
  expirationYear: string
}
```

### NotificationSetting Type (`/app/types/notifications.ts`)
```typescript
type NotificationSetting = {
  id: string
  label: string
  description: string
  enabled: boolean
}
```

## API Endpoints

### GET `/api/settings/billing/plan`
- **Response**: Current BillingPlan object

### PUT `/api/settings/billing/plan`
- **Request Body**: `{ planName: 'free' | 'pro' }`
- **Response**: Updated BillingPlan object

### GET `/api/settings/billing/payment-method`
- **Response**: PaymentMethod object

### POST `/api/settings/billing/payment-method`
- **Request Body**: Payment details
- **Response**: Updated PaymentMethod object

### GET `/api/settings/notifications`
- **Response**: Array of NotificationSetting objects

### PUT `/api/settings/notifications`
- **Request Body**: Array of updated NotificationSetting objects
- **Response**: Updated NotificationSetting array

## Service Layer

### `billingService` (`/app/services/billingService.ts`)

**Methods**:
- `getCurrentPlan()`: Fetch current subscription plan
- `updatePlan(planName)`: Update subscription plan
- `getPaymentMethod()`: Fetch payment method
- `processPayment(paymentDetails)`: Process payment

### `notificationService` (`/app/services/notificationService.ts`)

**Methods**:
- `getNotificationSettings()`: Fetch notification preferences
- `updateNotificationSettings(settings)`: Update notification preferences

## Hooks

### Settings Management Hooks (Future)
- `useBillingSettings()`: Manage billing state
- `useNotificationSettings()`: Manage notification state
- `useSettings()`: General settings management

## Components

1. **SettingsPage** (`/app/settings/page.tsx`): Main settings page
2. **BillingSettingsPage** (`/app/settings/billing/page.tsx`): Billing settings
3. **NotificationSettingsPage** (`/app/settings/notifications/page.tsx`): Notification settings
4. **Settings Components** (`/app/components/settings/`): Various settings components

## User Workflows

### View Billing Settings
1. Navigate to Settings
2. Click "Billing" tab
3. View current plan information
4. View payment method
5. Access plan management options

### Upgrade Plan
1. View current plan
2. Click "Upgrade to Pro"
3. Review plan features and pricing
4. Enter payment information
5. Confirm upgrade
6. Process payment
7. Activate new plan
8. Update account limits immediately

### Update Payment Method
1. Navigate to Billing Settings
2. Click "Update Payment Method"
3. Enter new payment details
4. Validate payment information
5. Save payment method
6. Confirm update

### Configure Notifications
1. Navigate to Settings
2. Click "Notifications" tab
3. View all notification types
4. Toggle individual notifications on/off
5. Save preferences
6. Confirm changes

## Business Logic

### Plan Upgrade Rules
- Free users can upgrade to Pro
- Pro users can downgrade to Free
- Plan changes take effect immediately
- Payment required for Pro plan
- Refund policy (future)

### Payment Processing
- Secure payment handling
- Payment validation
- Transaction recording
- Error handling and retry

### Notification Rules
- Notifications respect user preferences
- Enabled notifications are sent
- Disabled notifications are suppressed
- Default settings for new users

## Integration Points

1. **Profile Module**: User account information
2. **Billing Service**: Payment processing (future: Stripe integration)
3. **Notification Service**: Email/SMS notifications
4. **Admin Module**: Plan management for admins

## Role-Based Features

### Free Users
- View current plan
- Upgrade to Pro
- Basic notification settings
- Limited settings access

### Paid Users
- All free user features
- Plan management
- Payment method management
- All notification settings
- Priority support access

### Admin Users
- All user features
- System-wide settings management
- User plan management
- Billing analytics

## User Experience Features

### Settings Navigation
- Tab-based navigation
- Clear section organization
- Quick access to common settings
- Settings search (future)

### Form Validation
- Real-time validation
- Error messages
- Success confirmations
- Loading states

### Responsive Design
- Mobile-optimized forms
- Touch-friendly toggles
- Adaptive layouts

## Error Handling

- Payment errors: Display error, retry option
- Network errors: Display error, retry option
- Validation errors: Field-specific messages
- Plan change errors: Rollback and error message

## Future Enhancements

1. Multiple payment methods
2. Payment history
3. Invoice downloads
4. Subscription cancellation
5. Prorated billing
6. Annual billing option
7. Team/organization plans
8. Usage-based billing
9. Custom notification channels (Email, SMS, Push)
10. Notification scheduling
11. Notification templates
12. Quiet hours
13. Notification grouping
14. Advanced notification rules
15. Integration settings (API keys, webhooks)
16. Data export settings
17. Privacy settings
18. Security settings (2FA, etc.)
19. Theme/appearance settings
20. Language and region settings
21. Timezone settings
22. Date/time format preferences
23. Currency settings
24. Tax settings
25. Business information settings

## Dependencies

- React 18
- Next.js 14
- React Hook Form (form management)
- Zod (validation)
- @tanstack/react-query (data fetching)
- Lucide React (icons)

## Testing Considerations

- Unit tests for billing logic
- Integration tests for payment processing
- Component tests for settings forms
- E2E tests for plan upgrade flow
- Notification preference tests
- Payment validation tests

