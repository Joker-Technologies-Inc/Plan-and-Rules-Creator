# Language Management / Internationalization Module Documentation

## Overview
The Language Management Module provides comprehensive internationalization (i18n) functionality for the Axis Pro application. It supports multiple languages, dynamic language switching, email localization, and both client-side and server-side translation capabilities.

## Features

### 1. Multi-Language Support
- **Purpose**: Support multiple languages throughout the application
- **Location**: `/app/i18n.ts`
- **Supported Languages**:
  - **English (en)**: Default language
  - **Spanish (es)**: Secondary language

**Language Configuration**:
- Default language: English
- Fallback language: English
- Browser language detection
- Language persistence in localStorage

### 2. Translation Namespaces
- **Purpose**: Organize translations by feature/module
- **Location**: `/locales/[language]/[namespace].json`

**Available Namespaces**:
- `common`: Common translations used across the app
- `dashboard`: Dashboard-specific translations
- `clients`: Client management translations
- `invoices`: Invoice-related translations
- `reports`: Reports module translations
- `calendar`: Calendar and time records translations
- `sidebar`: Sidebar navigation translations
- `topbar`: Top bar menu translations
- `footer`: Footer translations
- `profile`: Profile page translations
- `settings`: Settings page translations
- `timeRecords`: Time records translations

### 3. Language Switcher Component
- **Purpose**: Allow users to change application language
- **Location**: `/app/components/LanguageSwitcher.tsx`
- **Integration**: Top bar menu

**Features**:
- Visual language selector with country flags
- Real-time language switching
- Language persistence in localStorage
- URL pathname locale management (future)
- Smooth language transitions

**UI Elements**:
- Dropdown selector
- Country flag icons (US for English, ES for Spanish)
- Language codes (EN, ES)
- Accessible labels

### 4. Client-Side Translation
- **Purpose**: Translate content in React components
- **Location**: `/app/i18n.ts`, `/app/components/I18nProvider.tsx`
- **Library**: react-i18next

**Implementation**:
- i18next initialization
- React i18next integration
- Language detection
- Dynamic language switching
- Translation hook usage

**Usage in Components**:
```typescript
import { useTranslation } from 'react-i18next';

function MyComponent() {
  const { t } = useTranslation('namespace');
  return <div>{t('key')}</div>;
}
```

### 5. Server-Side Translation
- **Purpose**: Translate content on the server
- **Location**: `/app/lib/serverTranslation.ts`
- **Usage**: Server components and API routes

**Features**:
- File system-based translation loading
- Server-side i18n instance creation
- Translation function for server components
- Error handling for missing translations

**Usage**:
```typescript
import { getServerTranslation } from '@/app/lib/serverTranslation';

const { t } = await getServerTranslation(locale, 'namespace');
```

### 6. Email Localization
- **Purpose**: Localize email content and formatting
- **Location**: `/app/lib/emailLocalization.ts`
- **Class**: `EmailLocalization`

**Localization Features**:
- Date localization (format, timezone)
- Currency localization (format, symbol)
- Number localization (format, decimals)
- Time localization (format, timezone)
- Template data localization

**Localization Options**:
- `locale`: Language and region (e.g., 'en-US', 'es-ES')
- `timezone`: Timezone for date/time formatting
- `currency`: Currency code for amounts
- `dateFormat`: Date format style (short, long, full)
- `numberFormat`: Number format (decimal, currency, percent)

**Usage**:
```typescript
const localizedData = await EmailLocalization.localizeTemplate(
  'templateId',
  'es-ES',
  templateData,
  { timezone: 'America/New_York', currency: 'USD' }
);
```

### 7. Language Detection
- **Purpose**: Automatically detect user's preferred language
- **Library**: i18next-browser-languagedetector

**Detection Methods**:
- Browser language preference
- localStorage stored preference
- URL parameter (future)
- User profile preference (future)

**Priority Order**:
1. localStorage stored preference
2. Browser language
3. Default language (English)

### 8. Translation File Structure
- **Purpose**: Organize translations by language and namespace
- **Location**: `/locales/[language]/[namespace].json`

**Structure**:
```
locales/
  en/
    common.json
    dashboard.json
    clients.json
    invoices.json
    reports.json
    calendar.json
    sidebar.json
    topbar.json
    footer.json
    profile.json
    settings.json
    timeRecords.json
  es/
    common.json
    dashboard.json
    clients.json
    invoices.json
    reports.json
    calendar.json
    sidebar.json
    topbar.json
    footer.json
    profile.json
    settings.json
    timeRecords.json
```

**Translation File Format**:
- JSON format
- Nested objects for organization
- Key-value pairs
- Support for interpolation
- Support for pluralization (future)

## Data Structure

### i18n Configuration (`/app/i18n.ts`)
```typescript
{
  ns: string[], // Namespaces
  defaultNS: string, // Default namespace
  resources: {
    [language]: {
      [namespace]: TranslationObject
    }
  },
  fallbackLng: string, // Fallback language
  debug: boolean, // Debug mode
  interpolation: {
    escapeValue: boolean
  },
  react: {
    useSuspense: boolean
  }
}
```

### Translation Object Structure
```typescript
{
  "key": "Translation text",
  "nested": {
    "key": "Nested translation"
  },
  "withInterpolation": "Hello {{name}}",
  "plural": {
    "one": "{{count}} item",
    "other": "{{count}} items"
  }
}
```

## API and Configuration

### i18n Initialization
- **File**: `/app/i18n.ts`
- **Function**: `initI18n()`
- **Client-side only**: Initializes on browser
- **Singleton pattern**: Only initializes once

### Next.js i18n Configuration
- **File**: `/next-i18next.config.js`
- **Configuration**:
  - Default locale: 'en'
  - Supported locales: ['en', 'es']
  - Locale path: './locales'
  - Reload on prerender: false

## Service Layer

### `EmailLocalization` (`/app/lib/emailLocalization.ts`)

**Methods**:
- `localizeTemplate(templateId, locale, data, options)`: Localize email template data
- `localizeDates(data, locale, options)`: Localize date fields
- `localizeCurrency(data, locale, options)`: Localize currency amounts
- `localizeNumbers(data, locale, options)`: Localize number fields
- `localizeTime(data, locale, options)`: Localize time fields

### `getServerTranslation` (`/app/lib/serverTranslation.ts`)

**Function**:
- `getServerTranslation(locale, ns)`: Get server-side translation function

## Components

1. **LanguageSwitcher** (`/app/components/LanguageSwitcher.tsx`): Language selector component
2. **I18nProvider** (`/app/components/I18nProvider.tsx`): i18n context provider
3. **I18nClientInit** (`/app/components/I18nClientInit.tsx`): Client-side initialization

## Hooks

### `useTranslation` (from react-i18next)
- **Purpose**: Access translations in components
- **Usage**: `const { t, i18n } = useTranslation('namespace')`
- **Returns**:
  - `t`: Translation function
  - `i18n`: i18n instance

**Example**:
```typescript
const { t } = useTranslation('dashboard');
const title = t('welcome.title');
```

## User Workflows

### Change Language
1. User clicks language switcher in top bar
2. Selects desired language (EN or ES)
3. Language changes immediately
4. Preference saved to localStorage
5. All UI elements update to new language
6. Page refresh maintains language preference

### Language Detection on First Visit
1. User visits application
2. System checks localStorage for preference
3. If not found, detects browser language
4. If browser language supported, uses it
5. Otherwise, defaults to English
6. Language preference saved for future visits

## Integration Points

1. **All Modules**: All modules use translations for UI text
2. **Email Service**: Email content localization
3. **Settings Module**: Language preference storage (future)
4. **Profile Module**: User language preference (future)
5. **Top Bar**: Language switcher display
6. **Layout**: i18n provider wrapper

## Translation Management

### Adding New Translations

1. **Add to Translation File**:
   - Open appropriate namespace file in `/locales/[language]/`
   - Add new key-value pair
   - Follow existing structure

2. **Use in Component**:
   ```typescript
   const { t } = useTranslation('namespace');
   <div>{t('new.key')}</div>
   ```

3. **Add to All Languages**:
   - Add translation to English file
   - Add translation to Spanish file
   - Maintain consistency in structure

### Adding New Language

1. Create language folder in `/locales/`
2. Copy all namespace files from English
3. Translate all content
4. Add language to i18n configuration
5. Add language option to LanguageSwitcher
6. Update next-i18next.config.js

### Translation Best Practices

- Use descriptive keys
- Organize by feature/namespace
- Keep translations consistent
- Use interpolation for dynamic content
- Test all languages
- Maintain translation files in sync

## Business Logic

### Language Persistence
- Language preference stored in localStorage
- Persists across browser sessions
- Can be overridden by user profile (future)
- Admin can set default language (future)

### Fallback Behavior
- If translation key missing, shows key
- Falls back to English if translation not found
- Logs missing translations in development
- Graceful degradation

### Performance
- Translations loaded on initialization
- Cached in memory
- No runtime translation file loading
- Optimized bundle size

## Role-Based Features

### All Users
- Language switcher access
- Language preference persistence
- All UI translations

### Admin Users
- Default language configuration (future)
- Translation management (future)
- Language analytics (future)

## Error Handling

- Missing translation keys: Shows key or fallback
- Missing translation files: Falls back to English
- Invalid locale: Uses default locale
- Translation loading errors: Graceful error handling

## Future Enhancements

1. Additional languages (French, German, etc.)
2. User profile language preference
3. Admin language management
4. Translation management UI
5. Automatic translation suggestions
6. Translation versioning
7. Context-aware translations
8. Right-to-left (RTL) language support
9. Regional variants (en-US, en-GB, es-ES, es-MX)
10. Translation completion tracking
11. Missing translation alerts
12. Translation import/export
13. Professional translation services integration
14. Translation memory
15. Pluralization rules for all languages
16. Date/time format preferences
17. Number format preferences
18. Currency format preferences
19. Language-specific email templates
20. Language-specific invoice templates
21. Language-specific PDF generation
22. URL-based language routing
23. Language-specific SEO
24. Language detection from IP (future)
25. Multi-language content management

## Dependencies

- **i18next**: Core internationalization framework
- **react-i18next**: React bindings for i18next
- **i18next-browser-languagedetector**: Browser language detection
- **next-i18next**: Next.js integration (if used)
- **react-country-flag**: Country flag icons

## Testing Considerations

- Unit tests for translation functions
- Integration tests for language switching
- Component tests with different languages
- E2E tests for language workflows
- Translation completeness tests
- Missing translation detection
- Language persistence tests
- Email localization tests

## Translation File Examples

### Common Translations (`/locales/en/common.json`)
```json
{
  "hello": "Hello",
  "welcome": "Welcome to Axis Pro",
  "status_update_success": "Invoice status updated successfully."
}
```

### Dashboard Translations (`/locales/en/dashboard.json`)
```json
{
  "title": "Dashboard",
  "total_revenue": "Total Revenue",
  "upcoming_sessions": "Upcoming Sessions"
}
```

### Spanish Translations (`/locales/es/common.json`)
```json
{
  "hello": "Hola",
  "welcome": "Bienvenido a Axis Pro",
  "status_update_success": "Estado de factura actualizado correctamente."
}
```

## Configuration Files

### `/next-i18next.config.js`
```javascript
{
  i18n: {
    defaultLocale: "en",
    locales: ["en", "es"]
  },
  defaultNS: "common",
  localePath: "./locales",
  reloadOnPrerender: false
}
```

## Notes

- Language switching is instant and doesn't require page reload
- Translations are loaded at application startup
- Email localization happens server-side
- All user-facing text should be translated
- Technical terms may remain in English if appropriate
- Maintain consistency in translation style

