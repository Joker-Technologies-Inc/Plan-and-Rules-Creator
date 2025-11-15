# Authentication Module Documentation

## Overview
The Authentication Module handles user authentication, authorization, and session management for the Axis Pro application. It provides secure login, signup, logout, password recovery, and password change functionality.

## Features

### 1. User Login
- **Purpose**: Authenticate users and establish secure sessions
- **Location**: `/app/login/page.tsx`
- **API Endpoint**: `/api/auth/login`
- **Service**: `authService.login()`

**Functionality**:
- Email and password authentication
- Session token generation and management
- Cookie-based authentication (httpOnly, secure, sameSite)
- Error handling for invalid credentials
- Redirect to dashboard upon successful login

**User Flow**:
1. User enters email and password
2. System validates credentials
3. On success: Creates session token, sets secure cookie, redirects to dashboard
4. On failure: Displays error message

**Technical Details**:
- Uses Next.js server-side authentication
- Token stored in httpOnly cookies for security
- Session duration: 1 hour (configurable)
- Base64 encoded token format: `userId:email`

### 2. User Signup
- **Purpose**: Register new users in the system
- **Location**: `/app/signup/page.tsx`
- **API Endpoint**: `/api/auth/signup`
- **Service**: `authService.signup()`

**Functionality**:
- New user registration
- Email validation
- Password strength requirements
- Automatic account creation
- Role assignment (free/paid/admin)

**User Flow**:
1. User provides registration details (name, email, password)
2. System validates input
3. Creates new user account
4. Automatically logs in the new user
5. Redirects to dashboard

### 3. User Logout
- **Purpose**: Terminate user sessions securely
- **Location**: `/app/components/LogoutButton.tsx`
- **API Endpoint**: `/api/auth/logout`
- **Service**: `authService.logout()`

**Functionality**:
- Clears authentication cookies
- Invalidates session tokens
- Redirects to login page
- Clears user state from global context

**User Flow**:
1. User clicks logout button
2. System clears authentication cookies
3. Redirects to login page
4. User must re-authenticate for next session

### 4. Password Recovery
- **Purpose**: Allow users to reset forgotten passwords
- **Location**: `/app/password-recovery/page.tsx`
- **API Endpoint**: `/api/auth/password-recovery`

**Functionality**:
- Email-based password reset
- Secure token generation for reset links
- Time-limited reset tokens
- Email notification with reset link

**User Flow**:
1. User requests password reset
2. System sends reset email with secure link
3. User clicks link and enters new password
4. System validates token and updates password
5. User can log in with new password

### 5. Password Change
- **Purpose**: Allow authenticated users to change their passwords
- **Location**: `/app/components/ChangePasswordForm.tsx`
- **API Endpoint**: `/api/profile/change-password`
- **Service**: `authService.changePassword()`

**Functionality**:
- Current password verification
- New password validation
- Password strength requirements
- Secure password update

**User Flow**:
1. User navigates to profile settings
2. Enters current password and new password
3. System verifies current password
4. Updates password if verification succeeds
5. Displays success/error message

### 6. Authentication Check
- **Purpose**: Verify user authentication status on protected routes
- **Location**: `/app/components/AuthCheck.tsx`
- **API Endpoint**: `/api/auth/check`
- **Service**: `authService.check()`

**Functionality**:
- Automatic authentication verification
- Route protection
- Redirect to login if not authenticated
- User role verification

**Implementation**:
- Wraps protected routes
- Checks authentication on page load
- Validates session tokens
- Manages redirect logic

## User Roles

The application supports three user roles:

1. **Admin**: Full system access, admin panel access
2. **Free**: Limited features, up to 3 clients
3. **Paid**: Unlimited features, all functionality

## Security Features

1. **HttpOnly Cookies**: Prevents XSS attacks
2. **Secure Cookies**: Only sent over HTTPS in production
3. **SameSite Protection**: Prevents CSRF attacks
4. **Token Expiration**: Automatic session timeout
5. **Password Hashing**: Secure password storage (in production)
6. **Input Validation**: Prevents injection attacks

## API Endpoints

### POST `/api/auth/login`
- **Request Body**: `{ email: string, password: string }`
- **Response**: `{ success: boolean, user?: User, message?: string }`

### POST `/api/auth/signup`
- **Request Body**: `{ name: string, email: string, password: string }`
- **Response**: `{ success: boolean, user?: User, message?: string }`

### POST `/api/auth/logout`
- **Response**: `{ success: boolean }`

### GET `/api/auth/check`
- **Response**: `{ authenticated: boolean, user?: User }`

### POST `/api/profile/change-password`
- **Request Body**: `{ currentPassword: string, newPassword: string }`
- **Response**: `{ success: boolean, message?: string }`

## Service Layer

### `authService` (`/app/services/authService.ts`)

**Methods**:
- `login(email, password)`: Authenticate user
- `logout()`: Terminate session
- `check()`: Verify authentication status
- `changePassword(currentPassword, newPassword)`: Update password

## Hooks

### `useAuth` (`/app/hooks/useAuth.ts`)
- Manages authentication state
- Provides login/logout functions
- Handles authentication errors
- Manages user session data

## Components

1. **LoginPage** (`/app/login/page.tsx`): Login form and UI
2. **SignupPage** (`/app/signup/page.tsx`): Registration form
3. **PasswordRecoveryPage** (`/app/password-recovery/page.tsx`): Password reset form
4. **AuthCheck** (`/app/components/AuthCheck.tsx`): Route protection wrapper
5. **LogoutButton** (`/app/components/LogoutButton.tsx`): Logout functionality
6. **ChangePasswordForm** (`/app/components/ChangePasswordForm.tsx`): Password change form

## Type Definitions

### User Type (`/app/types/auth-types.ts`)
```typescript
type User = {
  id: string
  email: string
  name: string
  role: 'admin' | 'free' | 'paid'
}
```

## Error Handling

- Invalid credentials: "Invalid credentials"
- Session expired: Redirect to login
- Network errors: Display error message
- Validation errors: Field-specific error messages

## Future Enhancements

1. Two-factor authentication (2FA)
2. Social login (Google, Facebook)
3. Remember me functionality
4. Session management dashboard
5. Password strength meter
6. Account lockout after failed attempts
7. Email verification
8. OAuth integration

## Dependencies

- Next.js 14 (App Router)
- React 18
- Next.js cookies API
- TypeScript

## Testing Considerations

- Unit tests for authentication logic
- Integration tests for API endpoints
- E2E tests for login/signup flows
- Security testing for token validation
- Password strength validation tests

