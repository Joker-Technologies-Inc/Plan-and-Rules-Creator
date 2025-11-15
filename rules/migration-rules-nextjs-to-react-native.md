# Migration Rules: Next.js to React Native (Expo) - Comprehensive Guide

## Table of Contents

0. [Expo Ecosystem Requirements](#0-expo-ecosystem-requirements)
1. [Architecture Migration](#1-architecture-migration)
2. [Project Structure Migration](#2-project-structure-migration)
3. [Component Migration Patterns](#3-component-migration-patterns)
4. [Routing Migration](#4-routing-migration)
5. [Styling Migration](#5-styling-migration)
6. [State Management Migration](#6-state-management-migration)
7. [API Integration Migration](#7-api-integration-migration)
8. [Type System Migration](#8-type-system-migration)
9. [Forms and Validation Migration](#9-forms-and-validation-migration)
10. [Image and Asset Migration](#10-image-and-asset-migration)
11. [Navigation Patterns](#11-navigation-patterns)
12. [Performance Optimization](#12-performance-optimization)
13. [Error Handling Migration](#13-error-handling-migration)
14. [Testing Migration](#14-testing-migration)
15. [Development Workflow](#15-development-workflow)
16. [Code Reusability Strategy](#16-code-reusability-strategy)

---

## 0. Expo Ecosystem Requirements

### 0.1 Mandatory: Use Expo Ecosystem Exclusively

**CRITICAL RULE:** This migration MUST use the complete Expo ecosystem. Do NOT use bare React Native packages or native modules directly. Always prefer `expo-*` packages over their React Native equivalents.

**Reference:** See `expo_ecosystem.md` for complete Expo ecosystem overview.

### 0.2 Expo Framework

**MANDATORY:** Use Expo managed workflow (no ejecting):

- ✅ Use `expo install` for all native dependencies
- ✅ Configure via `app.json` / `app.config.js`
- ✅ Stay within Expo SDK compatibility
- ❌ NEVER use `react-native install` or `npm install` for native packages
- ❌ NEVER eject from managed workflow

### 0.3 Expo Modules & APIs

**MANDATORY:** Use Expo modules instead of native modules:

| Need | Use Expo Module | Never Use |
|------|----------------|-----------|
| Secure Storage | `expo-secure-store` | `@react-native-async-storage/async-storage` (for sensitive data) |
| Images | `expo-image` | `react-native` Image |
| Camera | `expo-camera` | `react-native-camera` |
| Notifications | `expo-notifications` | `@react-native-community/push-notification-ios` |
| Location | `expo-location` | `@react-native-community/geolocation` |
| File System | `expo-file-system` | `react-native-fs` |
| Fonts | `expo-font` | Custom font loading |
| Splash Screen | `expo-splash-screen` | Custom splash implementations |
| Haptics | `expo-haptics` | `react-native-haptic-feedback` |
| Crypto | `expo-crypto` | `crypto-js` or native crypto |

**Installation Pattern:**
```bash
# ✅ CORRECT
npx expo install expo-secure-store expo-image expo-camera

# ❌ WRONG
npm install @react-native-async-storage/async-storage
npm install react-native-image-picker
```

### 0.4 Expo Tooling

**MANDATORY:** Use Expo CLI and tooling:

**Expo CLI Commands:**
```bash
# Development
npx expo start              # Start development server
npx expo start --dev-client # Start with development build
npx expo prebuild           # Generate native projects (if needed)

# Package Management
npx expo install [package]  # Install Expo-compatible packages

# Development Tools
npx expo customize:web      # Customize web configuration
```

**Expo Go:**
- Use Expo Go for rapid development and testing
- Scan QR code to preview instantly
- No building required during development

**Expo DevTools:**
- Use browser dashboard for logs, devices, and project controls
- Access at `http://localhost:19002` when running `expo start`

### 0.5 Expo Router (File-Based Navigation)

**MANDATORY:** Use Expo Router for all navigation:

- ✅ File-based routing (similar to Next.js App Router)
- ✅ Type-safe navigation with TypeScript
- ✅ Deep linking support built-in
- ✅ Layout system with `_layout.tsx`
- ❌ Do NOT use React Navigation directly
- ❌ Do NOT use imperative navigation patterns

**Example Structure:**
```
app/
├─ _layout.tsx           # Root layout
├─ index.tsx             # Home screen
├─ (tabs)/               # Tab group
│  ├─ _layout.tsx
│  ├─ home.tsx
│  └─ profile.tsx
└─ [id].tsx              # Dynamic route
```

### 0.6 Expo Application Services (EAS)

**MANDATORY:** Use EAS for builds, updates, and deployment:

**EAS Build:**
```bash
# ✅ CORRECT - Use EAS Build
eas build --platform ios
eas build --platform android
eas build --profile preview

# ❌ WRONG - Don't build locally for production
# (Only for development/testing)
```

**EAS Submit:**
```bash
# ✅ CORRECT - Use EAS Submit
eas submit --platform ios
eas submit --platform android
```

**EAS Update (OTA Updates):**
```bash
# ✅ CORRECT - Use EAS Update for JS changes
eas update --branch production --message "Bug fixes"
```

**EAS Configuration:**
```json
// eas.json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal"
    },
    "preview": {
      "distribution": "internal"
    },
    "production": {}
  },
  "submit": {
    "production": {}
  }
}
```

### 0.7 Expo Config Plugins

**MANDATORY:** Use Expo config plugins for native customization:

```typescript
// app.config.js
export default {
  plugins: [
    'expo-router',
    [
      'expo-build-properties',
      {
        ios: {
          deploymentTarget: '13.0',
        },
        android: {
          minSdkVersion: 21,
        },
      },
    ],
  ],
};
```

### 0.8 Package Installation Rules

**MANDATORY:** Follow these rules for all package installations:

1. **Check Expo SDK compatibility first:**
   ```bash
   npx expo install --check
   ```

2. **Use `expo install` for Expo-compatible packages:**
   ```bash
   npx expo install @tanstack/react-query zustand
   ```

3. **Use `expo install` for React Native packages:**
   ```bash
   npx expo install react-native-safe-area-context
   ```

4. **For Expo modules, always use `expo-*` prefix:**
   ```bash
   npx expo install expo-secure-store expo-image
   ```

5. **Verify compatibility before installing:**
   - Check [Expo SDK compatibility](https://docs.expo.dev/versions/latest/)
   - Verify package is in Expo SDK
   - Use `npx expo-doctor` to check for issues

### 0.9 Development Environment

**MANDATORY:** Set up development environment with Expo tools:

```bash
# Install Expo CLI globally (optional but recommended)
npm install -g expo-cli

# Or use npx (recommended)
npx expo@latest init MyApp

# Start development
npx expo start

# Run on specific platform
npx expo start --ios
npx expo start --android
npx expo start --web
```

### 0.10 Expo Ecosystem Checklist

Before starting migration, verify:

- [ ] Project initialized with `npx expo init` or `create-expo-app`
- [ ] Using latest Expo SDK version
- [ ] All native dependencies installed via `expo install`
- [ ] `app.json` / `app.config.js` properly configured
- [ ] Expo Router installed and configured
- [ ] EAS account set up (`eas login`)
- [ ] `eas.json` configured for builds
- [ ] Using `expo-*` packages instead of native alternatives
- [ ] No bare React Native native modules
- [ ] Managed workflow (not ejected)

### 0.11 Expo Ecosystem Benefits

**Why use Expo ecosystem exclusively:**

1. **Simplified Development:**
   - No native code knowledge required
   - Unified APIs across iOS/Android
   - Fast iteration with Expo Go

2. **Better Tooling:**
   - EAS Build (cloud builds, no Mac needed for iOS)
   - EAS Update (OTA updates without app store)
   - Expo DevTools (better debugging)

3. **Maintained & Tested:**
   - Expo modules are maintained by Expo team
   - Tested across platforms
   - Regular updates and security patches

4. **Future-Proof:**
   - Easy SDK upgrades
   - New features added regularly
   - Community support

### 0.12 Common Mistakes to Avoid

**❌ WRONG:**
```bash
# Installing native packages directly
npm install react-native-camera
npm install @react-native-community/geolocation

# Using bare React Native Image
import { Image } from 'react-native';

# Ejecting from managed workflow
npx expo eject

# Using React Navigation directly
npm install @react-navigation/native
```

**✅ CORRECT:**
```bash
# Using Expo modules
npx expo install expo-camera expo-location

# Using Expo Image
import { Image } from 'expo-image';

# Staying in managed workflow
# (No eject command needed)

# Using Expo Router (includes navigation)
# (Already included with Expo Router)
```

---

## 1. Architecture Migration

### 1.1 Core Principles

**MANDATORY:**
- Maintain the same layered architecture: `Screen → Component → Hook → Service → API`
- Preserve feature independence - no direct imports between features
- Keep dependency direction: dependencies flow downward only
- Maintain separation of concerns at each layer

### 1.2 Technology Stack Mapping

| Next.js | React Native (Expo) | Notes |
|---------|---------------------|-------|
| Next.js App Router | Expo Router | File-based routing maintained |
| React.js | React Native | Core React patterns unchanged |
| TypeScript | TypeScript | Full type safety maintained |
| TanStack Query | React Query | Same library, same patterns |
| Zustand | Zustand | Identical state management |
| Tailwind CSS | React Native StyleSheet / NativeWind | Styling approach changes |
| shadcn/ui | Custom components / React Native UI libraries | Rebuild with mobile patterns |

### 1.3 Architecture Layers

**Screen Layer (Expo Router)**
```typescript
// app/(tabs)/home/index.tsx
// Equivalent to Next.js app/home/page.tsx
// Use Expo Router file conventions
```

**Component Layer**
```typescript
// features/home/components/HomeCard.tsx
// Same structure, adapt JSX to React Native components
```

**Hook Layer**
```typescript
// features/home/hooks/useHomeData.ts
// Identical logic, same React Query patterns
```

**Service Layer**
```typescript
// features/home/services/homeService.ts
// Same API calls, same data transformations
```

**Type Layer**
```typescript
// features/home/types/index.ts
// Shared types between web and mobile
```

---

## 2. Project Structure Migration

### 2.1 Directory Structure Mapping

**Next.js Structure:**
```
/app/
/components/
/hooks/
/lib/
/docs/
```

**React Native (Expo) Structure:**
```
/app/                    # Expo Router screens (replaces Next.js /app)
/features/               # Feature-based organization
  /[feature-name]/
    /components/
    /hooks/
    /services/
    /types/
    /utils/
    /constants/
    /index.ts
/shared/                 # Shared code across features
  /components/
  /hooks/
  /services/
  /types/
  /utils/
  /constants/
  /providers/
/lib/                    # Core utilities (API, config, etc.)
/docs/                   # Documentation
```

### 2.2 File Naming Conventions

**MANDATORY:**
- Components: `PascalCase.tsx` (e.g., `HomeCard.tsx`)
- Hooks: `use` prefix, `camelCase.ts` (e.g., `useHomeData.ts`)
- Services: `camelCase.ts` with `Service` suffix (e.g., `homeService.ts`)
- Types: `PascalCase.ts` (e.g., `HomeTypes.ts`)
- Utils: `camelCase.ts` (e.g., `formatDate.ts`)
- Constants: `UPPER_SNAKE_CASE.ts` (e.g., `API_ENDPOINTS.ts`)
- Screens: Follow Expo Router conventions (e.g., `index.tsx`, `[id].tsx`)

### 2.3 Barrel Exports Pattern

**MANDATORY:** Every feature must have an `index.ts` barrel export:

```typescript
// features/home/index.ts
export { HomeCard, HomeList } from './components';
export { useHomeData, useHomeActions } from './hooks';
export { homeService } from './services';
export type { HomeData, HomeFilters } from './types';
```

**Usage:**
```typescript
// ✅ CORRECT
import { HomeCard, useHomeData } from '@/features/home';

// ❌ WRONG
import { HomeCard } from '@/features/home/components/HomeCard';
```

---

## 3. Component Migration Patterns

### 3.1 HTML to React Native Component Mapping

| HTML/Web | React Native | Notes |
|----------|--------------|-------|
| `<div>` | `<View>` | Container component |
| `<span>`, `<p>`, `<h1>` | `<Text>` | All text uses Text |
| `<button>` | `<Pressable>` or `<TouchableOpacity>` | Touch interactions |
| `<input>` | `<TextInput>` | Text input fields |
| `<img>` | `<Image>` from `expo-image` | Image component |
| `<a>` | `<Link>` from `expo-router` | Navigation links |
| `<ul>`, `<ol>` | `<FlatList>` or `<ScrollView>` | Lists |
| `<table>` | Custom with `<View>` and `<FlatList>` | Tables need custom implementation |

### 3.2 Component Migration Checklist

**For each component, verify:**

1. ✅ Replace all HTML elements with React Native equivalents
2. ✅ Convert CSS classes to StyleSheet or styled components
3. ✅ Replace `onClick` with `onPress`
4. ✅ Replace `className` with `style` prop
5. ✅ Remove web-specific props (`href`, `target`, etc.)
6. ✅ Adapt layout from flexbox to React Native flexbox (column by default)
7. ✅ Replace `window`/`document` APIs with React Native equivalents
8. ✅ Update event handlers (touch events vs mouse events)
9. ✅ Ensure minimum touch target size (44x44pt)
10. ✅ Add accessibility props (`accessibilityLabel`, `accessibilityRole`)

### 3.3 Component Migration Template

```typescript
// BEFORE (Next.js)
import { Button } from '@/components/ui/button';

export function HomeCard({ title, onClick }: HomeCardProps) {
  return (
    <div className="p-4 bg-white rounded-lg shadow">
      <h2 className="text-xl font-bold">{title}</h2>
      <Button onClick={onClick}>View Details</Button>
    </div>
  );
}

// AFTER (React Native)
import { View, Text, Pressable, StyleSheet } from 'react-native';
import { Button } from '@/shared/components/ui/Button';

export function HomeCard({ title, onPress }: HomeCardProps) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>{title}</Text>
      <Button onPress={onPress}>View Details</Button>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#fff',
    borderRadius: 8,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3, // Android shadow
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
  },
});
```

### 3.4 Reusable Component Strategy

**MANDATORY:** Create shared UI components in `/shared/components/ui/`:

```typescript
// shared/components/ui/Button.tsx
// Adapt shadcn/ui Button for React Native
// Accept same props interface where possible
// Use configuration objects for variants
```

**Pattern:**
- Extract web component logic
- Rebuild UI layer for React Native
- Maintain same props interface
- Use configuration objects for styling variants

---

## 4. Routing Migration

### 4.1 Next.js App Router to Expo Router Mapping

| Next.js | Expo Router | Notes |
|---------|-------------|-------|
| `app/page.tsx` | `app/index.tsx` | Root route |
| `app/about/page.tsx` | `app/about.tsx` | Simple route |
| `app/users/[id]/page.tsx` | `app/users/[id].tsx` | Dynamic route |
| `app/users/[id]/edit/page.tsx` | `app/users/[id]/edit.tsx` | Nested route |
| `app/(auth)/login/page.tsx` | `app/(auth)/login.tsx` | Route groups |
| `app/layout.tsx` | `app/_layout.tsx` | Layout file |
| `useRouter()` | `useRouter()` from `expo-router` | Similar API |
| `usePathname()` | `usePathname()` from `expo-router` | Similar API |
| `useSearchParams()` | `useLocalSearchParams()` | Similar API |
| `<Link href="/">` | `<Link href="/">` | Same component |

### 4.2 Navigation Patterns

**MANDATORY:** Use Expo Router navigation:

```typescript
// ✅ CORRECT - Expo Router navigation
import { useRouter } from 'expo-router';

function MyComponent() {
  const router = useRouter();
  
  const handleNavigate = () => {
    router.push('/users/123');
  };
  
  return <Button onPress={handleNavigate}>Navigate</Button>;
}

// ❌ WRONG - Don't use React Navigation directly
import { useNavigation } from '@react-navigation/native';
```

### 4.3 Tab Navigation Setup

**MANDATORY:** Implement 3 bottom tabs (Home, Alerts, Menu):

```typescript
// app/(tabs)/_layout.tsx
import { Tabs } from 'expo-router';

export default function TabLayout() {
  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: '#007AFF',
        headerShown: false,
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          title: 'Home',
          tabBarIcon: ({ color }) => <HomeIcon color={color} />,
        }}
      />
      <Tabs.Screen
        name="alerts"
        options={{
          title: 'Alerts',
          tabBarIcon: ({ color }) => <AlertIcon color={color} />,
        }}
      />
      <Tabs.Screen
        name="menu"
        options={{
          title: 'Menu',
          tabBarIcon: ({ color }) => <MenuIcon color={color} />,
        }}
      />
    </Tabs>
  );
}
```

### 4.4 Deep Linking

**MANDATORY:** Configure deep linking to match web app routes:

```json
// app.json
{
  "expo": {
    "scheme": "yourapp",
    "android": {
      "intentFilters": [
        {
          "action": "VIEW",
          "data": [
            {
              "scheme": "https",
              "host": "yourapp.com"
            }
          ]
        }
      ]
    }
  }
}
```

---

## 5. Styling Migration

### 5.1 Styling Approach

**MANDATORY:** Use React Native StyleSheet API or NativeWind (Tailwind for React Native):

**Option 1: StyleSheet (Recommended for performance)**
```typescript
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#fff',
  },
});
```

**Option 2: NativeWind (If Tailwind consistency is critical)**
```typescript
// Requires NativeWind setup
import { View } from 'react-native';

<View className="p-4 bg-white">
```

### 5.2 Color System Migration

**MANDATORY:** Extract colors from shadcn/Tailwind config and create shared color constants:

```typescript
// shared/constants/colors.ts
export const colors = {
  light: {
    background: '#ffffff',
    foreground: '#09090b',
    primary: '#007AFF',
    // ... shadcn colors
  },
  dark: {
    background: '#09090b',
    foreground: '#fafafa',
    primary: '#0a84ff',
    // ... shadcn dark colors
  },
} as const;
```

### 5.3 Spacing System

**MANDATORY:** Use 4px base unit for consistent spacing:

```typescript
// shared/constants/spacing.ts
export const spacing = {
  xs: 4,
  sm: 8,
  md: 16,
  lg: 24,
  xl: 32,
  '2xl': 48,
} as const;
```

### 5.4 Typography System

**MANDATORY:** Create typography constants:

```typescript
// shared/constants/typography.ts
export const typography = {
  h1: {
    fontSize: 32,
    fontWeight: 'bold' as const,
    lineHeight: 40,
  },
  h2: {
    fontSize: 24,
    fontWeight: 'bold' as const,
    lineHeight: 32,
  },
  body: {
    fontSize: 16,
    fontWeight: '400' as const,
    lineHeight: 24,
  },
} as const;
```

### 5.5 Dark Mode Support

**MANDATORY:** Implement dark mode from day 1 using React Native's `useColorScheme`:

```typescript
// shared/hooks/useTheme.ts
import { useColorScheme } from 'react-native';
import { colors } from '@/shared/constants/colors';

export function useTheme() {
  const colorScheme = useColorScheme();
  const isDark = colorScheme === 'dark';
  
  return {
    colors: isDark ? colors.dark : colors.light,
    isDark,
  };
}
```

---

## 6. State Management Migration

### 6.1 State Management Strategy

**MANDATORY:** Maintain same state management patterns:

| State Type | Library | Usage |
|------------|---------|-------|
| Server state | React Query | API data, caching, background refetching |
| Persistent client state | Zustand | Preferences, selected project, theme |
| UI-only state | `useState` | Form inputs, modal visibility |
| URL state | Expo Router params | Filters, pagination, search |

### 6.2 React Query Migration

**MANDATORY:** Use same React Query patterns:

```typescript
// ✅ CORRECT - Same pattern as web
import { useQuery } from '@tanstack/react-query';
import { queryKeys } from '@/lib/queryKeys';

export function useHomeData(filters: HomeFilters) {
  return useQuery({
    queryKey: queryKeys.home.list(filters),
    queryFn: () => homeService.getList(filters),
    staleTime: 30000, // 30s
    gcTime: 86400000, // 24h
  });
}
```

### 6.3 Query Keys Centralization

**MANDATORY:** Maintain centralized query keys:

```typescript
// lib/queryKeys.ts
export const queryKeys = {
  home: {
    all: ['home'] as const,
    lists: () => [...queryKeys.home.all, 'list'] as const,
    list: (filters: HomeFilters) => [...queryKeys.home.lists(), filters] as const,
    details: () => [...queryKeys.home.all, 'detail'] as const,
    detail: (id: string) => [...queryKeys.home.details(), id] as const,
  },
  // ... other features
} as const;
```

### 6.4 Zustand Store Migration

**MANDATORY:** Reuse Zustand stores with minimal changes:

```typescript
// shared/stores/userStore.ts
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';
import AsyncStorage from '@react-native-async-storage/async-storage';

interface UserState {
  selectedProject: string | null;
  setSelectedProject: (id: string | null) => void;
}

export const useUserStore = create<UserState>()(
  persist(
    (set) => ({
      selectedProject: null,
      setSelectedProject: (id) => set({ selectedProject: id }),
    }),
    {
      name: 'user-storage',
      storage: createJSONStorage(() => AsyncStorage), // React Native storage
    }
  )
);
```

---

## 7. API Integration Migration

### 7.1 API Client Setup

**MANDATORY:** Reuse existing API endpoints with React Native fetch:

```typescript
// lib/api/client.ts
import { queryClient } from '@/lib/queryClient';

const API_BASE_URL = process.env.EXPO_PUBLIC_API_URL || 'https://api.yourapp.com';

export async function customFetch<T>(
  endpoint: string,
  options: RequestInit = {}
): Promise<T> {
  const token = await getAuthToken(); // From secure storage
  
  const response = await fetch(`${API_BASE_URL}/api/v1${endpoint}`, {
    ...options,
    headers: {
      'Content-Type': 'application/json',
      Authorization: `Bearer ${token}`,
      ...options.headers,
    },
  });

  if (!response.ok) {
    throw new Error(`API Error: ${response.status}`);
  }

  return response.json();
}
```

### 7.2 Service Layer Migration

**MANDATORY:** Keep service layer identical:

```typescript
// features/home/services/homeService.ts
// ✅ SAME as web - no changes needed
import { customFetch } from '@/lib/api/client';
import type { HomeData, HomeFilters } from '../types';

export const homeService = {
  getList: async (filters: HomeFilters): Promise<HomeData[]> => {
    return customFetch<HomeData[]>('/home', {
      method: 'GET',
      // ... same as web
    });
  },
  // ... other methods identical to web
};
```

### 7.3 Request Interceptors

**MANDATORY:** Implement request/response interceptors:

```typescript
// lib/api/interceptors.ts
export function setupInterceptors() {
  // Request interceptor
  // Response interceptor
  // Error handling
  // Token refresh logic
}
```

### 7.4 Retry Logic

**MANDATORY:** Implement retry with exponential backoff:

```typescript
// lib/api/retry.ts
export async function fetchWithRetry<T>(
  fetchFn: () => Promise<T>,
  maxRetries = 3
): Promise<T> {
  for (let i = 0; i < maxRetries; i++) {
    try {
      return await fetchFn();
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      await new Promise(resolve => setTimeout(resolve, Math.pow(2, i) * 1000));
    }
  }
  throw new Error('Max retries exceeded');
}
```

### 7.5 Offline Support (Expo Ecosystem)

**MANDATORY:** Implement offline support with React Query using Expo-compatible packages:

**Installation:**
```bash
# ✅ CORRECT - Install via expo install
npx expo install @react-native-community/netinfo

# ❌ WRONG - Don't use npm install directly
# npm install @react-native-community/netinfo
```

**Implementation:**
```typescript
// lib/queryClient.ts
import { QueryClient } from '@tanstack/react-query';
import { onlineManager } from '@tanstack/react-query';
import NetInfo from '@react-native-community/netinfo';

// Setup network status (Expo-compatible package)
onlineManager.setEventListener((setOnline) => {
  return NetInfo.addEventListener((state) => {
    setOnline(state.isConnected ?? false);
  });
});

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 30000, // 30s
      gcTime: 86400000, // 24h
      retry: (failureCount, error) => {
        // Custom retry logic
        return failureCount < 3;
      },
    },
  },
});
```

**Note:** `@react-native-community/netinfo` is Expo-compatible and should be installed via `expo install` to ensure correct version compatibility with your Expo SDK.

---

## 8. Type System Migration

### 8.1 Type Sharing Strategy

**MANDATORY:** Share TypeScript types between web and mobile:

**Option 1: Shared Type Package (Recommended)**
```
/packages/
  /shared-types/        # Shared between web and mobile
    /src/
      /features/
        /home/
          types.ts
```

**Option 2: Monorepo Shared Directory**
```
/shared-types/         # If using monorepo
  /features/
    /home/
      types.ts
```

**Option 3: Copy Types (If separate repos)**
- Copy types from web to mobile
- Keep in sync via scripts or manual process
- Document type ownership

### 8.2 Type Migration Checklist

**For each type file:**

1. ✅ Copy types from web to mobile
2. ✅ Remove web-specific types (HTML element types, etc.)
3. ✅ Add React Native-specific types where needed
4. ✅ Ensure union types for constrained values
5. ✅ Avoid literal strings - use const enums or union types
6. ✅ Export from feature `index.ts`

### 8.3 Type Safety Patterns

**MANDATORY:** Use strict TypeScript:

```typescript
// ✅ CORRECT - Union types
type Status = 'pending' | 'completed' | 'failed';

// ❌ WRONG - Literal strings
const status: string = 'pending';

// ✅ CORRECT - Const assertions
const STATUSES = ['pending', 'completed', 'failed'] as const;
type Status = typeof STATUSES[number];
```

---

## 9. Forms and Validation Migration

### 9.1 Form Library Migration

**MANDATORY:** Use React Hook Form (same as web):

```typescript
// ✅ CORRECT - Same library
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const schema = z.object({
  name: z.string().min(1, 'Name is required'),
  email: z.string().email('Invalid email'),
});

export function MyForm() {
  const { control, handleSubmit } = useForm({
    resolver: zodResolver(schema),
  });

  return (
    <View>
      <Controller
        control={control}
        name="name"
        render={({ field, fieldState }) => (
          <TextInput
            value={field.value}
            onChangeText={field.onChange}
            placeholder="Name"
          />
        )}
      />
    </View>
  );
}
```

### 9.2 Form Component Patterns

**MANDATORY:** Create reusable form components:

```typescript
// shared/components/forms/FormInput.tsx
// Adapt shadcn/ui form components for React Native
// Maintain same validation patterns
```

### 9.3 Add Dialog Pattern

**MANDATORY:** Reuse Add Dialog pattern from web:

```typescript
// Follow pattern from docs/patterns/add-entity-flow.md
// Adapt modal/dialog for React Native (use Modal or bottom sheet)
```

---

## 10. Image and Asset Migration

### 10.1 Image Component (Expo Ecosystem)

**MANDATORY:** Use `expo-image` (Expo module) instead of Next.js Image or React Native Image:

**Installation:**
```bash
# ✅ CORRECT - Use Expo module
npx expo install expo-image

# ❌ WRONG - Don't use React Native Image
# (expo-image is already included, no need for react-native Image)
```

**Usage:**
```typescript
// ✅ CORRECT - Use expo-image
import { Image } from 'expo-image';

<Image
  source={{ uri: 'https://example.com/image.jpg' }}
  style={styles.image}
  contentFit="cover"
  transition={200}
  placeholder={{ blurhash: 'L6PZfSi_.AyE_3t7t7R**0o#DgR4' }}
  cachePolicy="memory-disk"
/>

// ❌ WRONG - Don't use React Native Image
import { Image } from 'react-native';
```

**Why expo-image:**
- Better performance than React Native Image
- Built-in caching (memory and disk)
- Blur hash support for placeholders
- Better image loading and error handling
- Part of Expo ecosystem (maintained and optimized)

### 10.2 Image Optimization

**MANDATORY:** Implement image optimization with expo-image features:

```typescript
// lib/utils/imageOptimization.ts
export function getOptimizedImageUrl(url: string, width?: number) {
  // Use image CDN or optimization service
  return `${url}?w=${width || 800}&q=80`;
}

// Usage with expo-image
<Image
  source={{ uri: getOptimizedImageUrl(imageUrl, 400) }}
  style={styles.image}
  contentFit="cover"
  cachePolicy="memory-disk" // Built-in caching
/>
```

### 10.3 Asset Management (Expo Asset System)

**MANDATORY:** Use Expo asset system for local assets:

**Installation:**
```bash
# expo-asset is included with Expo, no installation needed
```

**Usage:**
```typescript
// ✅ CORRECT - Use Expo asset system
// assets/images/logo.png
import logo from '@/assets/images/logo.png';

<Image source={logo} style={styles.logo} />

// For remote assets, use require or URI
<Image source={require('@/assets/images/logo.png')} />

// Or use Asset API for more control
import { Asset } from 'expo-asset';

const [asset, setAsset] = useState<Asset | null>(null);

useEffect(() => {
  Asset.fromModule(require('@/assets/images/logo.png'))
    .downloadAsync()
    .then(setAsset);
}, []);

{asset && <Image source={{ uri: asset.localUri }} />}
```

### 10.4 Image Loading States

**MANDATORY:** Use expo-image loading states:

```typescript
import { Image } from 'expo-image';
import { ActivityIndicator } from 'react-native';

<Image
  source={{ uri: imageUrl }}
  style={styles.image}
  placeholder={<ActivityIndicator />}
  contentFit="cover"
  onLoadStart={() => console.log('Loading started')}
  onLoad={() => console.log('Loaded')}
  onError={(error) => console.log('Error:', error)}
/>
```

---

## 11. Navigation Patterns

### 11.1 Navigation Structure

**MANDATORY:** Implement simplified navigation (max 2 levels deep):

```
Home (Tab)
  └─ Module Detail
      └─ Item Detail (max depth)

Alerts (Tab)
  └─ Alert Detail

Menu (Tab)
  └─ Settings
  └─ Profile
  └─ etc.
```

### 11.2 Hamburger Menu

**MANDATORY:** Implement hamburger menu (like web app):

```typescript
// shared/components/navigation/DrawerMenu.tsx
// Use expo-router drawer or custom implementation
```

### 11.3 Bottom Tabs

**MANDATORY:** Implement 3 bottom tabs (Home, Alerts, Menu)

---

## 12. Performance Optimization

### 12.1 Performance Targets

**MANDATORY:**
- App loads in < 2 seconds on 4G
- Smooth 60fps animations
- No memory leaks
- Efficient list rendering

### 12.2 Memoization

**MANDATORY:** Use `React.memo()` for shared/reusable components:

```typescript
// ✅ CORRECT
export const HomeCard = React.memo(function HomeCard({ data }: Props) {
  // Component implementation
});

// ❌ WRONG - Missing memo for reusable component
export function HomeCard({ data }: Props) {
  // Component implementation
}
```

### 12.3 List Optimization

**MANDATORY:** Use `FlatList` for large datasets:

```typescript
// ✅ CORRECT
<FlatList
  data={items}
  renderItem={({ item }) => <ItemCard item={item} />}
  keyExtractor={(item) => item.id}
  getItemLayout={(data, index) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  })}
  removeClippedSubviews
  maxToRenderPerBatch={10}
  windowSize={5}
/>

// ❌ WRONG - Using ScrollView for large lists
<ScrollView>
  {items.map(item => <ItemCard key={item.id} item={item} />)}
</ScrollView>
```

### 12.4 Lazy Loading

**MANDATORY:** Lazy load heavy components (charts, etc.):

```typescript
// ✅ CORRECT
import { useFocusEffect } from 'expo-router';
import { useState } from 'react';

export function ChartScreen() {
  const [shouldRenderChart, setShouldRenderChart] = useState(false);

  useFocusEffect(
    useCallback(() => {
      setShouldRenderChart(true);
      return () => setShouldRenderChart(false);
    }, [])
  );

  return shouldRenderChart ? <HeavyChart /> : <SkeletonChart />;
}
```

### 12.5 Memory Management

**MANDATORY:** Cleanup event listeners, intervals, and timeouts:

```typescript
// ✅ CORRECT
useEffect(() => {
  const interval = setInterval(() => {
    // Do something
  }, 1000);

  return () => clearInterval(interval);
}, []);
```

### 12.6 Code Splitting

**MANDATORY:** Use dynamic imports for large features:

```typescript
// ✅ CORRECT
const HeavyFeature = lazy(() => import('@/features/heavy-feature'));

<Suspense fallback={<Loading />}>
  <HeavyFeature />
</Suspense>
```

---

## 13. Error Handling Migration

### 13.1 Global Error Handler

**MANDATORY:** Implement global error handler:

```typescript
// shared/hooks/useGlobalErrorHandler.ts
import { useCallback } from 'react';
import Toast from 'react-native-toast-message';
import { logger } from '@/lib/logger';

export function useGlobalErrorHandler() {
  const handleError = useCallback((error: Error, context?: string) => {
    logger.error(error, { context });
    
    Toast.show({
      type: 'error',
      text1: 'Error',
      text2: error.message || 'Something went wrong',
    });
  }, []);

  return { handleError };
}
```

### 13.2 Error Boundaries

**MANDATORY:** Wrap critical components with error boundaries:

```typescript
// shared/components/ErrorBoundary.tsx
import React from 'react';
import { View, Text } from 'react-native';

export class ErrorBoundary extends React.Component<
  { children: React.ReactNode },
  { hasError: boolean }
> {
  // Error boundary implementation
}
```

### 13.3 Logging

**MANDATORY:** Use centralized logger (never `console.log`):

```typescript
// lib/logger.ts
export const logger = {
  error: (error: Error, context?: Record<string, unknown>) => {
    // Log to service (Sentry, etc.)
  },
  info: (message: string, data?: Record<string, unknown>) => {
    // Log to service
  },
};
```

### 13.4 Toast Notifications

**MANDATORY:** Use toast notifications for CRUD operations:

```typescript
// ✅ CORRECT
import Toast from 'react-native-toast-message';

const mutation = useMutation({
  mutationFn: createItem,
  onSuccess: () => {
    Toast.show({
      type: 'success',
      text1: 'Success',
      text2: 'Item created successfully',
    });
  },
  onError: (error) => {
    Toast.show({
      type: 'error',
      text1: 'Error',
      text2: error.message,
    });
  },
});
```

---

## 14. Testing Migration

### 14.1 Testing Strategy

**MANDATORY:**
- Unit tests for all components (React Native Testing Library)
- Integration tests for complex flows
- Test data transformations
- Test hooks independently

### 14.2 Component Testing

```typescript
// __tests__/components/HomeCard.test.tsx
import { render, fireEvent } from '@testing-library/react-native';
import { HomeCard } from '@/features/home/components/HomeCard';

describe('HomeCard', () => {
  it('renders correctly', () => {
    const { getByText } = render(<HomeCard title="Test" />);
    expect(getByText('Test')).toBeTruthy();
  });
});
```

### 14.3 Hook Testing

```typescript
// __tests__/hooks/useHomeData.test.ts
import { renderHook, waitFor } from '@testing-library/react';
import { useHomeData } from '@/features/home/hooks/useHomeData';

describe('useHomeData', () => {
  it('fetches data correctly', async () => {
    const { result } = renderHook(() => useHomeData({}));
    
    await waitFor(() => {
      expect(result.current.isSuccess).toBe(true);
    });
  });
});
```

---

## 15. Development Workflow (Expo Ecosystem)

### 15.1 Phase-Based Development

**MANDATORY:**
- Feature branching by phase (one branch per phase)
- Sequential phase execution
- Review and approval before merging each phase
- Sub-branches per module in Phase 7 if needed
- Use Expo tools for all development tasks

### 15.2 Development Phases

**Phase 1: Foundation (Expo Setup)**
- Project setup with `npx expo init` or `create-expo-app`
- Configure `app.json` / `app.config.js`
- Set up Expo Router
- Install core Expo modules via `expo install`
- Core architecture
- Shared components
- API integration

**Phase 2: Authentication (Expo Secure Storage)**
- Auth flow
- Token management with `expo-secure-store`
- Secure storage setup

**Phase 3: Navigation (Expo Router)**
- Tab navigation with Expo Router
- Drawer menu (Expo Router or custom)
- Deep linking configuration in `app.json`

**Phase 4: Core Features**
- Home module
- Common patterns
- Use Expo modules for all native features

**Phase 5-11: Module Implementation**
- One module per phase
- Follow established patterns
- Use Expo ecosystem exclusively

### 15.3 Expo Development Commands

**MANDATORY:** Use Expo CLI for all development tasks:

```bash
# Development
npx expo start                    # Start development server
npx expo start --dev-client       # Start with development build
npx expo start --ios              # Start on iOS simulator
npx expo start --android          # Start on Android emulator
npx expo start --web              # Start web version

# Package Management
npx expo install [package]        # Install Expo-compatible packages
npx expo install --check          # Check package compatibility

# Project Management
npx expo prebuild                 # Generate native projects
npx expo customize:web            # Customize web configuration
npx expo-doctor                   # Check for common issues

# EAS (Expo Application Services)
eas login                         # Login to EAS
eas build --platform ios          # Build iOS app
eas build --platform android     # Build Android app
eas build --profile preview       # Build preview version
eas submit --platform ios        # Submit to App Store
eas submit --platform android    # Submit to Play Store
eas update --branch production    # Push OTA update
```

### 15.4 EAS Build Workflow

**MANDATORY:** Use EAS Build for all production builds:

```bash
# 1. Configure eas.json (see section 0.6)
# 2. Login to EAS
eas login

# 3. Build for development
eas build --profile development --platform ios

# 4. Build for preview/testing
eas build --profile preview --platform all

# 5. Build for production
eas build --profile production --platform all

# 6. Submit to stores
eas submit --platform ios
eas submit --platform android
```

### 15.5 EAS Update Workflow (OTA Updates)

**MANDATORY:** Use EAS Update for JavaScript changes:

```bash
# 1. Configure update channels in app.json
# 2. Push update to channel
eas update --branch production --message "Bug fixes and improvements"

# 3. Target specific builds
eas update --branch production --message "Update" --group <update-group-id>
```

### 15.6 Development Environment Setup

**MANDATORY:** Set up development environment with Expo:

```bash
# 1. Install Expo CLI (optional, can use npx)
npm install -g expo-cli

# 2. Initialize project
npx expo init MyApp
# OR
npx create-expo-app MyApp

# 3. Install dependencies
cd MyApp
npx expo install expo-router expo-image expo-secure-store

# 4. Start development
npx expo start

# 5. Install EAS CLI
npm install -g eas-cli

# 6. Login to EAS
eas login

# 7. Configure EAS
eas build:configure
```

### 15.7 Code Review Checklist

**Before merging each phase:**

1. ✅ Follows architecture patterns
2. ✅ No direct imports between features
3. ✅ Types are properly defined
4. ✅ Components use React.memo() where needed
5. ✅ Error handling implemented
6. ✅ Loading/error/empty states handled
7. ✅ Accessibility props added
8. ✅ Performance optimized (lists, images, etc.)
9. ✅ Tests written for critical functionality
10. ✅ Documentation updated
11. ✅ **Uses Expo modules (expo-*) instead of native alternatives**
12. ✅ **All packages installed via `expo install`**
13. ✅ **No bare React Native native modules**
14. ✅ **Stays in managed workflow (not ejected)**
15. ✅ **EAS configuration updated if needed**

---

## 16. Code Reusability Strategy

### 16.1 Reusability Principles

**MANDATORY:**
- Reuse web app logic, adapt UI for mobile
- Share TypeScript types
- Keep endpoint calls and data transformations identical
- Adapt complex components (date range selector, charts, calendar)

### 16.2 Logic Reuse Pattern

```typescript
// ✅ CORRECT - Reuse service logic
// features/home/services/homeService.ts
// SAME as web - no changes

// ✅ CORRECT - Reuse hook logic
// features/home/hooks/useHomeData.ts
// SAME as web - React Query patterns identical

// ✅ CORRECT - Adapt UI component
// features/home/components/HomeCard.tsx
// Different JSX, same logic
```

### 16.3 Complex Component Adaptation

**Date Range Selector:**
- Extract logic to hook
- Rebuild UI with React Native date picker
- Maintain same API

**Charts:**
- Use `react-native-chart-kit` or `victory-native`
- Extract data transformation logic
- Reuse same data processing

**Calendar:**
- Use `react-native-calendars`
- Extract business logic
- Maintain same event handling

### 16.4 Type Sharing

**MANDATORY:** Share types between web and mobile:

```typescript
// Option 1: Shared package
// packages/shared-types/src/features/home/types.ts

// Option 2: Copy and sync
// features/home/types/index.ts (same as web)
```

---

## Migration Checklist Summary

### Before Starting Migration

- [ ] Review all existing web app features
- [ ] Document current architecture
- [ ] Identify shared code to extract
- [ ] Plan feature migration order
- [ ] **Review Expo ecosystem overview (`expo_ecosystem.md`)**
- [ ] **Set up Expo project with `npx expo init` or `create-expo-app`**
- [ ] **Configure `app.json` / `app.config.js`**
- [ ] **Set up Expo Router**
- [ ] **Install EAS CLI and login (`eas login`)**
- [ ] **Configure `eas.json` for builds**
- [ ] Set up Expo project structure
- [ ] Configure development environment

### For Each Feature Migration

- [ ] Copy and adapt types
- [ ] Reuse service layer (no changes)
- [ ] Reuse hook layer (minimal changes)
- [ ] Rebuild component layer (UI adaptation)
- [ ] Create screen with Expo Router
- [ ] Add error handling
- [ ] Add loading/error/empty states
- [ ] Add accessibility props
- [ ] Optimize performance
- [ ] Write tests
- [ ] Update documentation

### Quality Gates

- [ ] No direct imports between features
- [ ] All components use React.memo() where needed
- [ ] All lists use FlatList
- [ ] **All images use `expo-image` (Expo module)**
- [ ] **All native features use Expo modules (expo-*)**
- [ ] **All packages installed via `expo install`**
- [ ] **No bare React Native native modules**
- [ ] **Stays in managed workflow (not ejected)**
- [ ] All API calls use customFetch()
- [ ] All errors handled with global handler
- [ ] All types properly defined
- [ ] All tests passing
- [ ] Performance targets met
- [ ] Accessibility requirements met
- [ ] **EAS builds configured and working**
- [ ] **OTA updates configured (if applicable)**

---

## Best Practices Summary

1. **Expo Ecosystem (CRITICAL):** Use Expo ecosystem exclusively - Expo modules, Expo Router, EAS services, Expo CLI. Always prefer `expo-*` packages. Never use bare React Native native modules. Stay in managed workflow. Reference: `expo_ecosystem.md`
2. **Architecture:** Maintain layered architecture, feature independence
3. **Types:** Share types between web and mobile
4. **Logic:** Reuse business logic, adapt UI
5. **Performance:** Optimize for mobile (lists, images, memory)
6. **Error Handling:** Global error handler, error boundaries
7. **State:** React Query for server state, Zustand for client state
8. **Navigation:** Expo Router (file-based routing), simplified structure
9. **Styling:** StyleSheet or NativeWind, 4px base unit
10. **Testing:** Test components, hooks, and services
11. **Code Quality:** Zero warnings, consistent patterns
12. **Deployment:** Use EAS Build for all builds, EAS Submit for store submission, EAS Update for OTA updates

---

## Important References

- **Expo Ecosystem Overview:** See `expo_ecosystem.md` for complete Expo ecosystem documentation
- **Expo Documentation:** https://docs.expo.dev/
- **Expo Router:** https://docs.expo.dev/router/introduction/
- **EAS Documentation:** https://docs.expo.dev/build/introduction/

---

This comprehensive guide ensures a systematic, maintainable migration from Next.js to React Native (Expo) while preserving code quality, architecture patterns, and best practices. **The Expo ecosystem is mandatory and must be used exclusively throughout the migration.**

