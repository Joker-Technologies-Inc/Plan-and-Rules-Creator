# Plan and Rules Creator - Repository Documentation

## Overview

This repository serves as the **comprehensive planning, documentation, and rules repository** for the **Axis Pro** mobile application development project. It contains all architectural decisions, development guidelines, feature documentation, migration strategies, and planning documents needed to build a React Native (Expo) mobile app that maintains feature parity with the existing Next.js web application.

## Repository Purpose

This repository is designed to:

1. **Document Architecture**: Define the complete architecture, patterns, and best practices for the mobile app
2. **Guide Development**: Provide comprehensive rules and guidelines that developers must follow
3. **Plan Features**: Outline the development plan and phases for building the mobile app
4. **Document Features**: Provide detailed documentation for all 11 modules of the Axis Pro application
5. **Enable Migration**: Provide step-by-step migration guide from Next.js to React Native (Expo)

## Repository Structure

```
Plan-and-Rules-Creator/
├── .cursorrules                          # Development guidelines and rules
├── .gitignore                            # Git ignore patterns
├── README.md                              # This file
│
├── axis-pro-features/                     # Feature documentation for Axis Pro app
│   ├── README.md                          # Feature documentation index
│   ├── 01-Authentication/                # Authentication module docs
│   ├── 02-Dashboard/                      # Dashboard module docs
│   ├── 03-Clients-Management/             # Clients module docs
│   ├── 04-Calendar-Time-Records/          # Calendar module docs
│   ├── 05-Invoices/                      # Invoices module docs
│   ├── 06-Reports/                       # Reports module docs
│   ├── 07-Sessions/                      # Sessions module docs
│   ├── 08-Profile/                       # Profile module docs
│   ├── 09-Settings/                      # Settings module docs
│   ├── 10-Admin-Panel/                   # Admin Panel module docs
│   └── 11-Language-Management/            # Language Management module docs
│
├── plans/                                 # Development planning documents
│   ├── main-plan-core-premises.md         # Main development plan
│   └── secondaries-plan.md                # Module-specific planning guide
│
├── premises/                              # Core architectural premises
│   ├── core-premises.md                   # Core architectural principles
│   ├── core-premises-folder-structure.md  # Folder structure guidelines
│   └── core-premises-frontend-rules.md    # Frontend-specific rules
│
├── rules/                                 # Migration and development rules
│   └── migration-rules-nextjs-to-react-native.md  # Comprehensive migration guide
│
├── expo_ecosystem.md                      # Expo ecosystem overview and requirements
└── migration-rules-nextjs-to-react-native.md  # Migration guide (root level)
```

## Directory Details

### 📋 `.cursorrules`

**Purpose**: Comprehensive development guidelines that must be followed when writing, reviewing, or refactoring code.

**Contents**:
- Architecture foundation (technology stack, layered data flow)
- Folder structure and organization
- Maintainability and reusability principles
- SOLID architecture principles
- Type safety and reliability requirements
- State management strategy
- Performance optimization guidelines
- UI & styling standards
- Forms and validation patterns
- API integration standards
- User experience requirements
- Code quality standards
- Common patterns and anti-patterns

**Usage**: This file is automatically read by Cursor IDE and should be referenced by all developers. It defines the "rules of the game" for the entire project.

---

### 📚 `axis-pro-features/`

**Purpose**: Comprehensive documentation for all 11 modules/features of the Axis Pro application.

**Structure**: Each module folder contains three types of documentation:

1. **`[Module-Name]-Module-Documentation.md`** - Technical documentation:
   - Feature overview and purpose
   - Detailed feature breakdown
   - API endpoints and data structures
   - Service layer documentation
   - Component descriptions
   - User workflows and business logic
   - Integration points
   - Role-based features
   - Error handling
   - Testing considerations

2. **`User-Journey.md`** - User experience documentation:
   - Multiple user journey scenarios
   - Step-by-step flows
   - User actions and system responses
   - Success criteria
   - Error scenarios and resolutions
   - User personas
   - UX principles

3. **`FAQ.md`** - Support documentation:
   - General questions
   - How-to questions
   - Troubleshooting
   - Error message explanations
   - Best practices
   - Technical questions

**Modules Documented**:
1. Authentication
2. Dashboard
3. Clients Management
4. Calendar & Time Records
5. Invoices
6. Reports
7. Sessions
8. Profile
9. Settings
10. Admin Panel
11. Language Management

**Usage**: 
- **Developers**: Reference when implementing features
- **Product/UX Teams**: Understand user flows and requirements
- **Support Teams**: Answer customer questions and troubleshoot issues

**See**: [`axis-pro-features/README.md`](./axis-pro-features/README.md) for complete module documentation index.

---

### 📝 `plans/`

**Purpose**: Development planning documents that outline the strategy and approach for building the mobile app.

#### `main-plan-core-premises.md`

**Contents**:
- Technology stack decisions (Expo React Native, TypeScript, React Query, Zustand)
- Architecture requirements (feature parity, minimalist UI, simplified navigation)
- Integration strategy (reuse existing Next.js API endpoints)
- Development approach (Expo ecosystem, feature branching by phase)
- Design requirements (color scheme, dark mode, mobile optimization)
- Performance targets (load time, caching, offline support)
- Deployment strategy (EAS Build, EAS Submit, OTA updates)
- Success criteria (feature parity, reliability, user experience)
- Component reusability strategy
- Development flow (sequential phases, review gates)

**Usage**: Primary reference for understanding the overall project plan and requirements.

#### `secondaries-plan.md`

**Contents**:
- Fundamental architectural premises (layered architecture, dependency direction)
- Cross-module architectural premises (consistency, reusability, configuration-driven)
- Module-specific planning guidelines

**Usage**: Reference when planning individual module implementation.

---

### 🏗️ `premises/`

**Purpose**: Core architectural premises that define the foundation of the application architecture.

#### `core-premises.md`

**Contents**:
- Maintainability and reusability principles (DRY, module decoupling)
- Mobile-first performance requirements
- SOLID architecture principles (dependency injection, interfaces)
- Type safety and reliability standards
- State management separation (React Query, Zustand, useState)
- Performance optimization guidelines
- User experience requirements
- Consistency across modules
- Expo ecosystem requirements
- Code quality standards

**Usage**: Foundation principles that all code must follow.

#### `core-premises-folder-structure.md`

**Contents**:
- Technology stack definition
- Feature independence requirements
- Layered architecture within features (Screen → Component → Hook → Service)
- Consistent structure across features
- Shared code centralization
- Benefits and implementation principles

**Usage**: Reference when setting up project structure and organizing code.

#### `core-premises-frontend-rules.md`

**Contents**:
- Architecture foundation (React.js + Next.js, TypeScript)
- UI and styling requirements (Tailwind CSS, shadcn/ui)
- Data management patterns (TanStack Query, query keys)
- Error handling standards
- Component architecture guidelines
- Forms and validation requirements
- Search and filtering requirements
- State management strategy
- File organization standards
- Development tools configuration
- Quality standards
- API integration patterns
- Notification requirements
- Environment configuration

**Usage**: Frontend-specific rules that complement the general core premises.

---

### 📖 `rules/`

**Purpose**: Detailed migration and development rules for converting the Next.js web app to React Native (Expo).

#### `migration-rules-nextjs-to-react-native.md`

**Contents**: Comprehensive 1,782-line migration guide covering:

1. **Expo Ecosystem Requirements** - Mandatory Expo-only approach
2. **Architecture Migration** - Maintaining layered architecture
3. **Project Structure Migration** - Directory mapping and organization
4. **Component Migration Patterns** - HTML to React Native component mapping
5. **Routing Migration** - Next.js App Router to Expo Router
6. **Styling Migration** - Tailwind CSS to React Native StyleSheet
7. **State Management Migration** - React Query and Zustand patterns
8. **API Integration Migration** - Reusing existing endpoints
9. **Type System Migration** - Sharing TypeScript types
10. **Forms and Validation Migration** - React Hook Form and Zod
11. **Image and Asset Migration** - expo-image usage
12. **Navigation Patterns** - Simplified navigation structure
13. **Performance Optimization** - Mobile-first performance
14. **Error Handling Migration** - Global error handlers
15. **Testing Migration** - React Native Testing Library
16. **Development Workflow** - Phase-based development
17. **Code Reusability Strategy** - Reusing web app logic

**Usage**: Step-by-step reference when migrating features from web to mobile.

---

### 📘 `expo_ecosystem.md`

**Purpose**: Overview of the Expo ecosystem and its components.

**Contents**:
- Expo Framework (managed and bare workflows)
- Expo Modules & APIs (100+ ready-to-use modules)
- Expo Tooling (CLI, Expo Go, Expo Router, DevTools, Snack)
- Expo Application Services (EAS Build, EAS Submit, EAS Update, EAS Device, EAS Metadata)
- Community & Extras (third-party modules, config plugins, UI kits)

**Usage**: Reference for understanding what Expo provides and what tools are available.

---

### 🔄 `migration-rules-nextjs-to-react-native.md` (Root Level)

**Purpose**: Duplicate of the migration rules file in the `rules/` directory for easy access.

**Note**: This file appears in both the root directory and the `rules/` directory. The content is identical.

---

## How Everything Relates

### Development Flow

```
1. Read .cursorrules
   ↓
2. Review plans/main-plan-core-premises.md
   ↓
3. Understand premises/ (core architectural principles)
   ↓
4. Study rules/migration-rules-nextjs-to-react-native.md
   ↓
5. Reference expo_ecosystem.md for Expo tools
   ↓
6. Implement features using axis-pro-features/ documentation
```

### Document Relationships

```
.cursorrules
  ↑ (implements)
premises/core-premises*.md
  ↑ (defines foundation for)
plans/main-plan-core-premises.md
  ↑ (executes via)
rules/migration-rules-nextjs-to-react-native.md
  ↑ (applied to)
axis-pro-features/[module]/
  ↑ (references)
expo_ecosystem.md
```

### Key Principles Flow

1. **Core Premises** (`premises/`) define **WHAT** principles to follow
2. **Main Plan** (`plans/`) defines **WHY** and **WHEN** to build
3. **Migration Rules** (`rules/`) define **HOW** to migrate
4. **Cursor Rules** (`.cursorrules`) define **HOW** to code
5. **Feature Docs** (`axis-pro-features/`) define **WHAT** to build

---

## Usage Guide

### For Project Managers

1. **Start Here**: Read `plans/main-plan-core-premises.md` to understand the project scope
2. **Review Success Criteria**: Check success criteria in the main plan
3. **Track Progress**: Use feature documentation to track module completion
4. **Reference FAQs**: Use `axis-pro-features/[module]/FAQ.md` for support planning

### For Developers

1. **Read First**: 
   - `.cursorrules` - Development guidelines
   - `premises/core-premises.md` - Architectural principles
   - `rules/migration-rules-nextjs-to-react-native.md` - Migration guide

2. **Before Starting a Feature**:
   - Read `axis-pro-features/[module]/[Module]-Module-Documentation.md`
   - Review `axis-pro-features/[module]/User-Journey.md`
   - Check `expo_ecosystem.md` for available Expo tools

3. **During Development**:
   - Follow `.cursorrules` strictly
   - Reference migration rules for patterns
   - Use feature documentation for API endpoints and data structures

4. **Code Review**:
   - Verify compliance with `.cursorrules`
   - Check adherence to core premises
   - Ensure migration patterns are followed

### For Designers/UX

1. **User Journeys**: Read `axis-pro-features/[module]/User-Journey.md` for each module
2. **Design Requirements**: Check `plans/main-plan-core-premises.md` for design requirements
3. **Mobile Optimization**: Review `rules/migration-rules-nextjs-to-react-native.md` for mobile patterns

### For QA/Testing

1. **Test Scenarios**: Use `axis-pro-features/[module]/User-Journey.md` for test cases
2. **Error Scenarios**: Check FAQ documents for error handling
3. **Success Criteria**: Reference `plans/main-plan-core-premises.md` for acceptance criteria

### For Support Teams

1. **Primary Resource**: `axis-pro-features/[module]/FAQ.md` for each module
2. **User Flows**: `axis-pro-features/[module]/User-Journey.md` for step-by-step guides
3. **Error Messages**: FAQ documents contain error explanations

---

## Key Concepts

### Layered Architecture

All code follows this pattern:
```
Screen → Component → Hook → Service → Endpoint → Data
```

### Feature Independence

- Features are autonomous and self-contained
- No direct imports between features
- Shared code lives in `/shared/`

### State Management

- **Server State** → React Query (TanStack Query)
- **Persistent Client State** → Zustand
- **UI-only State** → `useState`
- **URL State** → Query parameters

### Technology Stack

- **Framework**: Expo React Native (managed workflow)
- **Language**: TypeScript throughout
- **Routing**: Expo Router (file-based)
- **Data Fetching**: TanStack Query (React Query)
- **State Management**: Zustand
- **Styling**: React Native StyleSheet
- **API**: Reuse existing Next.js endpoints (`/api/v1`)

---

## Development Phases

Based on `plans/main-plan-core-premises.md`, development follows sequential phases:

1. **Phase 1: Foundation** - Project setup, core architecture, shared components
2. **Phase 2: Authentication** - Auth flow, token management, secure storage
3. **Phase 3: Navigation** - Tab navigation, drawer menu, deep linking
4. **Phase 4: Core Features** - Home module, common patterns
5. **Phase 5-11: Module Implementation** - One module per phase (11 modules total)

Each phase requires review and approval before merging.

---

## Success Criteria

From `plans/main-plan-core-premises.md`:

- ✅ Feature parity: all 11 modules functional
- ✅ Reliability: >99% auth success, >99.5% crash-free
- ✅ User experience: >4.5 stars App Store rating
- ✅ Adoption: 80% of web users use mobile app within 3 months

---

## Contributing

When adding or updating documentation:

1. **Follow Structure**: Maintain the existing folder structure
2. **Update Index**: Update `axis-pro-features/README.md` if adding modules
3. **Cross-Reference**: Link related documents
4. **Be Comprehensive**: Include all necessary details
5. **Keep Updated**: Update documentation as features evolve

---

## Quick Reference

### Most Important Files

1. **`.cursorrules`** - Development guidelines (MUST READ for developers)
2. **`plans/main-plan-core-premises.md`** - Project plan (MUST READ for PMs)
3. **`rules/migration-rules-nextjs-to-react-native.md`** - Migration guide (MUST READ for migration)
4. **`premises/core-premises.md`** - Architectural principles (MUST READ for architects)

### Documentation Statistics

- **Total Modules**: 11
- **Total Documentation Files**: 33+
  - 11 Module Documentation files
  - 11 User Journey files
  - 11 FAQ files
- **Total User Journeys**: 60+ scenarios
- **Total FAQ Questions**: 400+ questions and answers
- **Migration Guide**: 1,782 lines
- **Development Rules**: 453 lines

---

## Repository Information

- **Repository Name**: Plan-and-Rules-Creator
- **Purpose**: Planning, documentation, and rules repository for Axis Pro mobile app
- **Organization**: Joker-Technologies-Inc
- **GitHub**: https://github.com/Joker-Technologies-Inc/Plan-and-Rules-Creator

---

## Support

For questions about:
- **Architecture**: See `premises/` and `.cursorrules`
- **Planning**: See `plans/`
- **Migration**: See `rules/migration-rules-nextjs-to-react-native.md`
- **Features**: See `axis-pro-features/`
- **Expo**: See `expo_ecosystem.md`

---

**Last Updated**: 2025-11-15

**Version**: 1.0.0

