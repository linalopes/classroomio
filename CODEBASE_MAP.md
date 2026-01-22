# ClassroomIO Codebase Map & Mental Model

## 📁 Apps Overview

### `/apps` Directory Structure

1. **`apps/dashboard`** - Main admin/teacher dashboard
   - **Purpose**: Core LMS application for educators and organizations
   - **Tech**: SvelteKit, TailwindCSS, Carbon Components
   - **Features**: Course creation, student management, assignments, quizzes, forums, AI integration
   - **Routes**: Organization pages, course management, LMS student view, settings

2. **`apps/course-app`** - Template showcase/marketing site
   - **Purpose**: Landing page showcasing available course site templates
   - **Tech**: SvelteKit, TailwindCSS
   - **Note**: This is the marketing site, NOT the actual course site template

3. **`apps/api`** - Backend API
   - **Purpose**: REST API server for the platform
   - **Tech**: TypeScript, Express-like framework

4. **`apps/classroomio-com`** - Marketing website
   - **Purpose**: Main marketing site for ClassroomIO product
   - **Tech**: SvelteKit

5. **`apps/docs`** - Documentation site
   - **Purpose**: Product documentation
   - **Tech**: Fumadocs (React/TSX)

---

## 🎯 Dashboard App (`apps/dashboard`)

### Main Layout & Navigation

**Root Layout**: `apps/dashboard/src/routes/+layout.svelte`
- **Key Responsibilities**:
  - Theme initialization (`setTheme()` from `$lib/utils/functions/theme.ts`)
  - Navigation component selection (OrgNavigation, LMSNavigation, LandingNavigation)
  - Auth state management
  - Dark mode toggle
  - Organization site detection

**Navigation Components**:
- `src/lib/components/Navigation/index.svelte` - Landing/public navigation
- `src/lib/components/Navigation/app.svelte` - Organization dashboard navigation
- `src/lib/components/Navigation/lms.svelte` - Student LMS navigation

**Navigation Selection Logic** (in `+layout.svelte`):
```svelte
{#if isOrgPage() || isCoursesPage()}
  <OrgNavigation />  <!-- Teacher/org dashboard -->
{:else if isLMSPage()}
  <LMSNavigation />   <!-- Student view -->
{:else}
  <LandingNavigation />  <!-- Public landing -->
{/if}
```

### Theming System

**Theme Configuration**:
- **File**: `apps/dashboard/src/lib/utils/functions/theme.ts`
- **How it works**:
  - Supports preset themes: `theme-rose`, `theme-green`, `theme-orange`, `theme-violet`
  - Supports custom hex colors (injected as CSS variables)
  - Theme stored in `organization.theme` database field
  - Applied via `setTheme(org.theme)` in layout

**Theme Application**:
- Themes applied via body class names
- Custom themes generate CSS variables for primary color shades (50-900)
- Uses Carbon Components Svelte Theme component for dark mode

**Global Styles**:
- `apps/dashboard/src/app.postcss` - Main stylesheet
- `apps/dashboard/tailwind.config.js` - Tailwind configuration (minimal)
- CSS variables defined in `+layout.svelte` style block:
  - `--main-primary-color`
  - `--border-color`
  - `--app-background-color`
  - `--app-background` (gradient)

---

## 🎨 Course App (Public Course Site)

### Template System

**Location**: `packages/course-app/src/template/`

**Template Selection**:
- Controlled by `VITE_TEMPLATE` environment variable
- Available templates: `classic`, `minimal`, `posthog`, `webflow`, `bootcamp`, `examprep`, `cal` (default)
- Template components loaded dynamically in `src/lib/components/index.ts`

### Classic Template

**Location**: `packages/course-app/src/template/src/lib/components/classic/`

**Components**:
- `Navigation.svelte` - Site navigation
- `Footer.svelte` - Site footer
- `PrimaryButton.svelte` - Button component
- `pages/Home.svelte` - Homepage layout
- `pages/Courses.svelte` - Courses listing page
- `CourseCard.svelte`, `BlogCard.svelte`, `TestimonialCard.svelte`, etc.

**Configuration**:
- **Template Index**: `packages/course-app/src/template/src/lib/components/classic/index.ts`
  - Exports component mapping
  - Exports font link (Inter font for Classic)

**Site Configuration**:
- **File**: `packages/course-app/src/template/src/lib/data/pages.json`
  - Contains page layouts, navigation items, SEO settings
  - Configurable sections: header, about, courses, instructors, FAQ, testimonials, etc.
  - Logo path: `seo.settings.logo` (default: `/logo.svg`)

**Layout**:
- **File**: `packages/course-app/src/template/src/routes/+layout.svelte`
  - Loads template components dynamically
  - Applies template-specific font via `font-{VITE_TEMPLATE}` class
  - Renders navigation and footer (except on course detail pages)

**Styling**:
- **Tailwind Config**: `packages/course-app/src/template/tailwind.config.ts`
  - Template-specific colors via CSS variables:
    - `--classic-primary`: `300 98% 41%` (magenta/purple)
    - `--classic-secondary`: `300 100% 95%`
  - Template-specific fonts (Inter for Classic)

- **Global CSS**: `packages/course-app/src/template/src/app.css`
  - CSS variables for all templates
  - Dark mode support
  - Typography styles

---

## 🎨 Safe Branding Areas

### Dashboard (`apps/dashboard`)

**✅ Safe to Change**:

1. **Logo**:
   - `apps/dashboard/static/logo-*.png` - Default logo files
   - `apps/dashboard/src/lib/components/Navigation/Logo.svelte` - Logo component
   - Organization logos come from `organization.avatar_url` (database)

2. **Colors**:
   - `apps/dashboard/src/routes/+layout.svelte` (lines 172-181) - CSS variables:
     - `--main-primary-color`
     - `--border-color`
     - `--app-background-color`
     - `--app-background` (gradient)
   - `apps/dashboard/src/app.postcss` - Global color overrides
   - Theme colors in `apps/dashboard/src/lib/utils/functions/theme.ts`

3. **Typography**:
   - `apps/dashboard/src/app.postcss` - Font family definitions
   - `apps/dashboard/src/routes/+layout.svelte` - `font-roboto` class

4. **Manifest**:
   - `apps/dashboard/static/manifest.json` - PWA metadata, theme colors

**⚠️ Avoid Changing**:
- Navigation component logic in `+layout.svelte`
- Theme injection logic in `theme.ts`
- Core component structure

### Course App Classic Template

**✅ Safe to Change**:

1. **Logo**:
   - `packages/course-app/src/template/static/logo.svg` - Default logo
   - Configured in `pages.json` → `seo.settings.logo`
   - Component: `packages/course-app/src/template/src/lib/components/ui/_custom/Logo.svelte`

2. **Colors**:
   - `packages/course-app/src/template/src/app.css` (lines 46-47):
     - `--classic-primary`: Change HSL values
     - `--classic-secondary`: Change HSL values
   - Or modify Tailwind classes in component files

3. **Typography**:
   - `packages/course-app/src/template/src/lib/components/classic/index.ts` (line 19):
     - Change Google Fonts link
   - `packages/course-app/src/template/tailwind.config.ts` (line 12):
     - Change font family name

4. **Content**:
   - `packages/course-app/src/template/src/lib/data/pages.json`:
     - All page content, navigation items, SEO settings
     - Safe to modify all content here

5. **Component Styling**:
   - All `.svelte` files in `packages/course-app/src/template/src/lib/components/classic/`
   - Modify Tailwind classes and inline styles

**⚠️ Avoid Changing**:
- Template component interface in `index.ts`
- Layout structure in `+layout.svelte`
- Component prop interfaces

---

## 🗺️ Mental Model

### Architecture Pattern

**Monorepo Structure**:
```
classroomio/
├── apps/           # Deployable applications
│   ├── dashboard/  # Main LMS (teachers/orgs)
│   ├── course-app/ # Template showcase (marketing)
│   ├── api/        # Backend API
│   └── ...
└── packages/        # Shared/reusable code
    └── course-app/ # Course site template package
        └── src/template/  # Actual template code
```

### Key Concepts

1. **Multi-App Architecture**:
   - Dashboard = Admin/teacher interface
   - Course App Template = Public-facing course sites
   - Templates are packaged separately for distribution

2. **Template System**:
   - Templates are isolated component sets
   - Selected via environment variable
   - Each template has its own styling and components
   - Classic is one of 7 available templates

3. **Organization Branding**:
   - Each organization can have custom theme (hex color)
   - Logo stored in database (`organization.avatar_url`)
   - Theme applied dynamically via CSS injection

4. **Navigation Context**:
   - Dashboard has 3 navigation modes:
     - Public landing (no auth)
     - Organization dashboard (teacher view)
     - LMS (student view)
   - Navigation switches based on route detection

5. **Styling Strategy**:
   - Dashboard: Carbon Components + Tailwind + Custom CSS
   - Course Templates: Tailwind with template-specific CSS variables
   - Dark mode: Class-based (`dark:` prefix)

### Data Flow

**Dashboard Theme**:
```
Organization DB → org.theme (hex/theme name)
  ↓
+layout.svelte → setTheme(org.theme)
  ↓
theme.ts → injectCustomTheme() or apply preset
  ↓
CSS variables injected → Components styled
```

**Course Template**:
```
VITE_TEMPLATE env var → Template selection
  ↓
components/index.ts → Load template components
  ↓
+layout.svelte → Render template navigation/footer
  ↓
pages.json → Configure content/structure
```

---

## 📍 Key File Locations

### Dashboard
- **Layout**: `apps/dashboard/src/routes/+layout.svelte`
- **Navigation**: `apps/dashboard/src/lib/components/Navigation/`
- **Theme Logic**: `apps/dashboard/src/lib/utils/functions/theme.ts`
- **Global Styles**: `apps/dashboard/src/app.postcss`
- **Logo Component**: `apps/dashboard/src/lib/components/Navigation/Logo.svelte`

### Classic Template
- **Template Root**: `packages/course-app/src/template/`
- **Classic Components**: `packages/course-app/src/template/src/lib/components/classic/`
- **Template Config**: `packages/course-app/src/template/src/lib/components/classic/index.ts`
- **Site Config**: `packages/course-app/src/template/src/lib/data/pages.json`
- **Layout**: `packages/course-app/src/template/src/routes/+layout.svelte`
- **Global Styles**: `packages/course-app/src/template/src/app.css`
- **Tailwind Config**: `packages/course-app/src/template/tailwind.config.ts`

---

## 🎯 Quick Reference

**Change Dashboard Logo**: Replace `apps/dashboard/static/logo-*.png` files

**Change Dashboard Colors**: Edit CSS variables in `apps/dashboard/src/routes/+layout.svelte` (lines 172-181)

**Change Classic Template Logo**: Update `pages.json` → `seo.settings.logo` or replace `/static/logo.svg`

**Change Classic Template Colors**: Edit `--classic-primary` and `--classic-secondary` in `packages/course-app/src/template/src/app.css`

**Change Classic Template Font**: Update font link in `packages/course-app/src/template/src/lib/components/classic/index.ts`

**Configure Classic Template Content**: Edit `packages/course-app/src/template/src/lib/data/pages.json`
