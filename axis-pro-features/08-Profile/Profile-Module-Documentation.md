# Profile Module Documentation

## Overview
The Profile Module allows users to view and manage their personal information, update account settings, and change passwords. It provides a centralized location for user account management.

## Features

### 1. Profile View
- **Purpose**: Display current user profile information
- **Location**: `/app/profile/page.tsx`
- **API Endpoint**: `/api/profile`
- **Service**: `profileService.getProfile()`

**Profile Information Displayed**:
- User Name
- Email Address
- User Role (Free, Paid, Admin)
- Account Creation Date (future)
- Last Login Date (future)
- Profile Picture (future)

### 2. Profile Editing
- **Purpose**: Update user profile information
- **Location**: `/app/components/ProfileForm.tsx`
- **API Endpoint**: `/api/profile`
- **Service**: `profileService.updateProfile()`

**Editable Fields**:
- User Name
- Email Address (with validation)
- Profile Picture (future)
- Phone Number (future)
- Address (future)
- Timezone (future)
- Language Preference (future)

**Validation**:
- Email format validation
- Name length validation
- Required field validation
- Duplicate email checking
- Real-time validation feedback

### 3. Password Change
- **Purpose**: Allow users to change their password
- **Location**: `/app/components/ChangePasswordForm.tsx`
- **API Endpoint**: `/api/profile/change-password`
- **Service**: `authService.changePassword()`

**Password Change Features**:
- Current password verification
- New password input
- Confirm new password
- Password strength indicator (future)
- Password requirements display

**Security Features**:
- Current password required
- Password strength validation
- Secure password update
- Success confirmation
- Error handling

**Password Requirements** (Future):
- Minimum length (8 characters)
- Uppercase letter
- Lowercase letter
- Number
- Special character

### 4. Account Information
- **Purpose**: Display account details and settings
- **Location**: Profile page

**Account Details**:
- Account Type (Free/Paid/Admin)
- Subscription Status (for paid users)
- Account Limits (for free users)
- Usage Statistics (future)

### 5. Profile Picture Management (Future)
- **Purpose**: Upload and manage profile pictures
- **Features**:
  - Image upload
  - Image cropping
  - Preview
  - Remove picture

## Data Structure

### User Type (`/app/types/auth-types.ts`)
```typescript
type User = {
  id: string
  email: string
  name: string
  role: 'admin' | 'free' | 'paid'
}
```

## API Endpoints

### GET `/api/profile`
- **Response**: User object with profile information
- **Authentication**: Required

### PUT `/api/profile`
- **Request Body**: Updated user profile (partial)
```typescript
{
  name?: string,
  email?: string,
  // other profile fields
}
```
- **Response**: Updated user object
- **Authentication**: Required

### POST `/api/profile/change-password`
- **Request Body**:
```typescript
{
  currentPassword: string,
  newPassword: string
}
```
- **Response**: `{ success: boolean, message?: string }`
- **Authentication**: Required

## Service Layer

### `profileService` (`/app/services/profileService.ts`)

**Methods**:
- `getProfile()`: Fetch current user profile
- `updateProfile(updatedProfile)`: Update user profile

### `authService` (for password change)
- `changePassword(currentPassword, newPassword)`: Change user password

## Hooks

### `useProfile` (`/app/hooks/useProfile.ts`)
- Manages profile state
- Handles profile fetching
- Handles profile updates
- Manages loading and error states
- Provides profile refresh functionality

## Components

1. **ProfilePage** (`/app/profile/page.tsx`): Main profile page
2. **ProfileForm** (`/app/components/ProfileForm.tsx`): Profile editing form
3. **ChangePasswordForm** (`/app/components/ChangePasswordForm.tsx`): Password change form

## User Workflows

### View Profile
1. Navigate to Profile page
2. System fetches current user profile
3. Display profile information
4. Show edit button if needed

### Edit Profile
1. Click "Edit Profile" button
2. Form opens with current values
3. User modifies fields
4. Real-time validation
5. Submit form
6. System updates profile
7. Display success message
8. Refresh profile display

### Change Password
1. Navigate to Profile page
2. Click "Change Password" button
3. Enter current password
4. Enter new password
5. Confirm new password
6. System validates current password
7. If valid, updates password
8. Display success message
9. Optionally log out user (future)

## Business Logic

### Profile Update Rules
- Email must be unique (if changed)
- Email format must be valid
- Name cannot be empty
- Profile updates require authentication

### Password Change Rules
- Current password must be correct
- New password must meet requirements
- New password cannot be same as current
- Password change requires authentication
- Rate limiting on password attempts (future)

### Role-Based Access
- Users can only edit their own profile
- Admins can view all profiles (future)
- Role changes require admin access

## Integration Points

1. **Authentication Module**: User authentication and session management
2. **Settings Module**: Account settings and preferences
3. **Billing Module**: Subscription information for paid users
4. **Admin Module**: User management for admins

## Role-Based Features

### Free Users
- Basic profile management
- Password change
- Account information display
- Upgrade prompts

### Paid Users
- All free user features
- Subscription management link
- Enhanced profile options
- Priority support information

### Admin Users
- All user features
- Access to user management
- System administration tools

## User Experience Features

### Form Validation
- Real-time field validation
- Error messages
- Success confirmations
- Loading states

### Responsive Design
- Mobile-optimized forms
- Touch-friendly inputs
- Adaptive layouts

### Security Indicators
- Password strength meter (future)
- Security status display (future)
- Two-factor authentication setup (future)

## Error Handling

- Validation errors: Field-specific error messages
- Network errors: Display error, retry option
- Authentication errors: Redirect to login
- Duplicate email: Prevent update, show error
- Invalid current password: Show error message

## Future Enhancements

1. Profile picture upload
2. Two-factor authentication (2FA)
3. Account deletion
4. Email verification
5. Phone number verification
6. Social media links
7. Bio/description field
8. Timezone settings
9. Language preferences
10. Notification preferences (moved to settings)
11. Privacy settings
12. Activity log
13. Login history
14. Security settings
15. API key management
16. Connected accounts
17. Backup codes
18. Account recovery options
19. Profile export
20. Data portability

## Dependencies

- React 18
- Next.js 14
- React Hook Form (form management)
- Zod (validation)
- @tanstack/react-query (data fetching)
- Lucide React (icons)

## Testing Considerations

- Unit tests for profile validation
- Integration tests for profile API
- Component tests for profile forms
- E2E tests for profile update flow
- Password change tests
- Authentication tests
- Validation tests

