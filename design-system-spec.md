# Design System Specification

IntegrityNext Design Library · Figma node 71138:958 · React app `integrity-next`

This document maps Figma design tokens to how the React app applies them: **tokens**, **Figma-aligned primitives**, **documented shared components**, and **other high-traffic UI** under `src/common/components/new` and feature modules.

For per-component contracts (semantics, props, rules), use **[COMPONENT_CATALOG.md](COMPONENT_CATALOG.md)** and the linked `COMPONENT_CONFIGURATION.md` files.

---

## Theme & Colour Source of Truth

| Layer | Path | Role |
|---|---|---|
| **App theme (MUI)** | `src/assets/theme/theme.jsx` | `createTheme`: palette, typography (`Inter`), `fontSize` / `iconSize`, component overrides (inputs, buttons, dialogs, etc.) |
| **Legacy token scale** | `src/assets/theme/colors.ts` | Primary (sky / "light blue" scale with numeric keys e.g. `20` for rgba overlays), secondary (navy), semantic colours (`success`, `error`, `warning`, `grey`, …). Surfaced on the theme as `theme.color.*` |
| **Design Library tokens (Figma parity)** | `src/design-system/tokens/colors.ts`, `spacing.ts`, `typography.ts` | Canonical design-library values; use for new Figma-aligned work and `design-system/components/Button` |

> **Practical rule:** Most of the app still consumes `theme` from `theme.jsx` + `colors.ts`. Prefer `design-system/tokens` when building or extending components that must match the Design Library spec.

---

## Typography

### Font Family

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Typography/FontFamily` | `Geometria` — Figma / design library | All new Figma-aligned components and design-system work | Do not substitute with system fonts (Inter, Roboto, Arial) |
| `theme.typography` | `Inter` — React app (`theme.jsx`) | All existing MUI-themed components across the app | Do not use Inter for new Figma-critical surfaces |

### Display & Heading Scale

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Typography/DisplayXL` (H1) | Geometria · font-weight: 600 · UPPERCASE | Page-level headers only. Always uppercase. Highest visual emphasis on a page. | Do not use inside cards, modals, or inline content |
| `Typography/H2` (Display Large) | Geometria · font-size: 24px · font-weight: 700 · line-height: 1.2 · UPPERCASE | Section titles and page sub-headers. Always uppercase. | Avoid for body content or repeated items; max one per section |
| `Typography/TitleMedium` | Geometria · font-weight: 300 (regular) | Main question text in assessments. Always regular weight. | Do not bold; not for navigation or UI controls |
| `Typography/TitleSmall` | Geometria · font-weight: 600 (bold) | Supply chain pages, disclaimer, complaint procedure sections. Always bold. | — |
| `Typography/TitleXS` | Geometria · font-weight: 600 (bold) | Modal and dialog titles. Always bold. | Do not use for body text or interactive labels |

### Body Scale

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Typography/BodyLarge` | Geometria · font-weight: 300 or 600 · line-height: 1.5 | Paragraphs, input field text, general UI labels. Supports regular (300) and bold (600). | — |
| `Typography/BodyMedium` | Geometria · font-weight: 300 or 600 | Table cell content. Supports regular and bold. | Not for headings or primary call-to-actions |
| `Typography/BodySmall` | Geometria · font-weight: 300 or 600 | Tooltip content, helper text, supplemental labels. | Do not use below 12px for accessibility |
| `Typography/Caption` | Geometria · font-size: 12px · font-weight: 400 · line-height: 1.5 | Metadata, secondary labels, annotation text | Do not use for primary content |

---

## Colour Guide

### Primary — Blue

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/primary/default` | `#83CDF0` · `theme.color.primary` (sky scale) | Primary contained button fill, selection highlight, focus rings, active states | Do not use as text color on white; not for error or warning states |
| `color/primary/hover` | `#B7E9FF` | Hover state of primary buttons and interactive elements | — |
| `color/primary/selected-bg` | `rgba(131, 205, 240, 0.1)` · `theme.color.primary[20]` | Selected list items, active tab background, date picker selected range, nav active states | — |
| `color/primary/hover-overlay` | `rgba(131, 205, 240, 0.4)` | ButtonGroup button hover background | — |

### Secondary — Dark Navy

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/secondary/default` | `#002031` · `theme.color.secondary` | Primary text, dark surfaces (Navbar, footer), outlined button borders, secondary icon color | Do not use as background when content must remain legible on small screens |
| `color/secondary/darker` | `#001A28` | Footer background | — |

### Success — Green

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/success/light` | `#C5E8E2` · `theme.color.success` | Alert success background | — |
| `color/success/chip` | `rgba(67, 180, 161, 0.2)` | Chip background for success / compliance / green status | — |

### Error — Red

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/error/default` | `#ED696C` · `theme.color.error` | Error-color contained button fill; error icons | Do not use for non-error interactive elements |
| `color/error/light` | `#F9D1D1` | Alert error background, error button hover | — |
| `color/error/chip` | `rgba(237, 105, 108, 0.2)` | Chip background for error / high-risk status | — |

### Warning — Yellow

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/warning/light` | `#FAF6DA` · `theme.color.warning` | Alert warning background | — |
| `color/warning/chip` | `rgba(240, 227, 135, 0.2)` | Chip background for warnings / medium risk | — |

### Neutral / Info — Light Blue

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/info/light` | `#F3FAFE` | Info note/callout background | — |
| `color/info/chip` | `rgba(131, 205, 240, 0.2)` | Chip background for info / secondary / to-do status; Tab hover background | — |

### AI / Purple

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/ai/chip` | `rgba(94, 53, 177, 0.2)` | AI probability chip background; AI-generated content labels | Do not use for non-AI features |

### Surface / Background

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/surface/white` | `#FFFFFF` | Card and panel background, modal surface, primary container background | — |
| `color/surface/page` | `#F5F7F9` | Page-level background, component set backgrounds, secondary surfaces | — |
| `color/surface/subtle` | `#FCFCFC` | Table row alternative fill, very light elevation surfaces | — |
| `color/surface/nested-row` | `#FCFDFD` | Nested DataGrid row background | — |
| `color/overlay` | `rgba(0, 32, 49, 0.2)` | Backdrop / modal overlay | — |

### Border / Divider

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/border/default` | `#DBDBDB` | Default border for cards, inputs, frames, table cell dividers | — |
| `color/border/disabled` | `#EAEAEA` | Border for disabled form fields, disabled buttons | — |
| `color/border/dashed` | `#BBBBBB` · dashed 4 4 | File dropzone border in default state | — |

### Priority Chip Palette

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `color/priority/very-low` | `#E6E9EB` | Very low priority chip background | — |
| `color/priority/low` | `#B0BABF` | Low priority chip background | — |
| `color/priority/medium` | `rgba(0, 32, 49, 0.6)` | Medium priority chip background | — |
| `color/priority/high` | `rgba(0, 32, 49, 0.8)` | High priority chip background | — |
| `color/priority/very-high` | `#002031` | Very high priority chip background | — |
| `color/status/neutral` | `rgba(0, 32, 49, 0.1)` | Status/neutral chip background | — |

---

## Elevation / Shadows

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `elevation/questionnaire-card` | `0px 2px 6px 0px rgba(0, 32, 49, 0.10)` | Assessment/questionnaire cards, autocomplete dropdowns, popovers | Do not apply to flat table rows or inline elements |
| `elevation/table` | `0px 2px 4px 0px rgba(219, 219, 219, 1)` | Data table container | — |
| `elevation/popovers` | `4px 4px 8px 0px rgba(0, 0, 0, 0.20)` | Menus, tooltips, autocomplete dropdowns, date picker calendar | Do not apply to cards that sit on page background |
| `elevation/modal` | `0px 4px 32px 24px rgba(0, 32, 49, 0.10)` | Dialog / modal surface shadow | — |
| `elevation/profile-container` | `0px 2px 6px 0px rgba(219, 219, 219, 1)` | Profile page card container | — |
| `elevation/modal-footer` | `0px -10px 20px 0px rgba(0, 32, 49, 0.10)` | Modal footer when content is scrollable — shadow separates footer from body | Do not use on non-scrollable modal footers |
| `elevation/filter-backdrop` | `backdrop-filter: blur(4px)` | Filters panel background blur | — |

---

## Spacing System

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `spacing/base` | `8px` (scale: x1, x2, x3, x4) | Foundation for all spacing decisions | Do not use arbitrary off-scale values like 5px, 7px, 11px |
| `spacing/xs` | `4px` | Chip inner gap, icon-to-label gap, tight inline spacing | — |
| `spacing/sm` | `8px` | Row spacing in tables and lists, button inner gap, icon padding | — |
| `spacing/md` | `16px` | Component internal padding, section gaps, column padding in tables, button vertical spacing, paragraph spacing | — |
| `spacing/lg` | `24px` | Card internal padding, gutter width between columns, spacing between buttons, spacing between cards | — |
| `spacing/xl` | `32px` | Card-like element padding (Deforestation Map, KPI), heading top margin | — |
| `spacing/2xl` | `48px` | Section margins, header padding from navigation bar, section-level separation | — |
| `spacing/grid/columns` | `12 columns` | All page-level grid layouts | — |
| `spacing/grid/gutter` | `24px` | Gutter between grid columns | — |
| `spacing/dropzone/between-items` | `8px` | Between consecutive file items in dropzone | — |
| `spacing/dropzone/to-first-item` | `16px` | Between upload area and first uploaded file item | — |

---

## Border Radius

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `radius/pill` | `256px` | All buttons (contained, outlined, text), icon buttons, chips, avatar circles | Do not use for rectangular containers or table rows |
| `radius/card` | `16px` | Component set containers in design, modal header, KPI cards, empty state | — |
| `radius/card-lg` | `30px` | Page-level sections (Typography frame, Color Guide frame) | Do not use for components inside pages |
| `radius/section` | `32px` | Responsive layout preview frames (grid mockups) | — |
| `radius/default` | `4px` | Modals, dialogs, alerts, autocomplete dropdown, menus, snackbars, chip (non-pill), file dropzone, table rows | — |
| `radius/input` | `4px` | TextField, Select, DatePicker inputs | — |
| `radius/avatar/rounded` | `4px` | Rounded variant avatars | — |
| `radius/avatar/circular` | `256px` | Circular variant avatars, avatar groups | — |
| `radius/modal-footer` | `0px 0px 4px 4px` | Modal footer component — bottom corners only | — |

---

## Component Variants & States

### Button

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Button/variant` | `contained` · `outlined` · `text` | **contained**: primary CTA per section (max 1). **outlined**: competing secondary action. **text**: local/low-emphasis actions and table rows | Do not use two contained buttons in one section; do not use text variant as primary CTA |
| `Button/color` | `primary` #83CDF0 · `secondary` #83CDF0 · `error` #ED696C | **primary/secondary**: default actions. **error**: destructive or irreversible actions only | Do not use error color for non-destructive actions |
| `Button/size` | `medium` h=48px min-w=110px max-w=300px · `small` h=32px min-w=90px max-w=240px | **medium**: default for all page/modal CTAs. **small**: table row actions only | Do not use medium inside table rows |
| `Button/state` | `default` · `hover` · `disabled` · `loading` | Apply **loading** when async action is in-progress — disables button, shows spinner, preserves width | Disabled buttons must not be focusable; do not remove label during loading |
| `Button/isLoading` | `true` / `false` | Set to true to prevent duplicate form submissions while awaiting response | — |
| `Button/icon` | `startIcon` or `endIcon` (optional, max 1) | Use one icon to reinforce the label's meaning. Either start or end — never both. | Do not use both startIcon and endIcon simultaneously; not for icon-only buttons |
| `Button/layout/horizontal` | Order: outlined then contained · gap 24px · right-aligned | Default layout for paired actions | — |
| `Button/layout/stacked` | Order: contained then outlined/text · gap 16px vertical | Responsive/mobile layouts | — |

#### React app implementation

| Implementation | Path | When to use | When to avoid |
|---|---|---|---|
| **design-system Button** | `src/design-system/components/Button/Button.tsx` | New or redesigned flows that must match Design Library specs. Incremental adoption on screens you own. | MuiModal save/cancel rows. Icon-only actions. Replacing every MUI Button import without a planned migration. |
| **MuiButton wrappers** | `src/common/components/new/MuiButton/` | Modal primary/secondary pairs. CSV export, underlined link actions, pagination circles, PageHeader text actions. | Branding a whole-page CTA when design asks for design-system Button only. |
| **Raw `@mui/material/Button`** | via `theme.jsx` overrides | Existing modules already using MUI Button. Small local triggers. | New modal footers. New Figma-critical CTAs. |

**Import:** `import { Button } from 'src/design-system/components/Button/Button'`

### IconButton

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `IconButton/size` | `large` 32px · `medium` 24px · `small` 20px | Space-constrained contexts where action is familiar without label | Do not use when the action label is essential for clarity |
| `IconButton/color` | `primary` · `secondary` | — | — |
| `IconButton/hasBg` | `true` / `false` | hasBg=true when icon button sits on a colored or image surface needing contrast | — |
| `IconButton/state` | `default` · `hover` · `disabled` | — | — |

**React app:** Use `CircleIconButton` (`src/common/components/new/MuiButton/`) for icon-only actions.

### Checkbox

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Checkbox/size` | `large` · `medium` · `small` | — | — |
| `Checkbox/state` | `default` · `hover` · `disabled` · `indeterminate` | Use **indeterminate** when a parent checkbox has mixed child selections | — |
| `Checkbox/isSelected` | `true` / `false` | — | — |
| `CheckboxGroup/direction` | `vertical` / `horizontal` | vertical: long option lists. horizontal: 2-4 short options | — |

**React app:** `FormCheckbox` (`src/common/components/new/`) for form-bound usage with `InxForm`.

### RadioButton

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `RadioButton/state` | `default` · `hover` · `disabled` | Use for mutually exclusive single-selection | Do not use when multiple selections are allowed — use Checkbox instead |
| `RadioGroup/direction` | `vertical` / `horizontal` | — | — |

### TextField

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `TextField/state` | `Default` · `Hover` · `Focus` · `Error` · `Disabled` | Focus uses #83CDF0 dashed border. Error uses red border and helper text. | — |
| `TextField/multiline` | `true` / `false` | true for textarea/freeform long text; false for single-line inputs | Do not use multiline for short inputs like email or phone |
| `TextField/isFilled` | `true` / `false` | Represents whether field has user-entered content | — |

**React app:** Use `FormInput` (`src/common/components/new/FormInput/`) for form-bound text fields.

### Select & Autocomplete

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Select/type` | `MultiSelect` · `SingleSelect` | — | — |
| `Select/state` | `Default` · `Filled` · `Hover` · `Focus` | open=true when state=Focus (dropdown visible) | — |
| `Autocomplete/variant` | `MultiSelect` · `SingleSelect` | — | — |
| `Autocomplete/groupBy` | `true` / `false` | groupBy=true when options benefit from categorical grouping | — |

**React app:** `FormSelect` for form-bound selects. `MultiSelectAutocomplete` / `SingleFilterAutocomplete` under `DashboardFilters`. Do not rebuild filter dropdowns from raw Select when DashboardFilters already exists.

### Switch

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Switch/enabled` | `true` / `false` | Toggle between two binary states. Clear visual feedback of current state. | Do not use when multiple options available — use RadioGroup instead |
| `Switch/state` | `Default` · `Hover` · `Disabled` | — | — |

**React app:** `LabelledSwitch` for all toggle + label patterns. `FormSwitch` for form-bound usage.

### Slider

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Slider/state` | `default` · `hover` · `disabled` | Range selection from continuous values | Do not use for discrete choice from small sets |
| `Slider/percent` | `20-80` / `50-50` / `80-20` | Split-rail slider positions | — |

**React app:** `FormSlider` (`src/common/components/new/`) for form-bound sliders.

### Chip

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Chip/type` | `default` · `priority` · `status` · `probability` · `textStatus` · `textRisk` · `value` | Always configure via semantic meaning (type+status) — never by visual color directly | Do not manually override background/text/border color; do not use for long text strings |
| `Chip/color` | `Error` · `Warning` · `Success` · `Neutral (to do)` · `Neutral (no data)` · `Secondary` · `AI` | Color derived automatically from type+status mapping | — |
| `Chip/priorityLevel` | `very low` · `low` · `medium` · `high` · `very high` | Only applies when type=priority | — |
| `Chip/size` | `sm` (tables) / `md` (cards, detail pages) | — | — |

**React app:** `TooltipChip` for chips with tooltip. `FormButtonGroup` for grouped chip-style toggles in forms.

### Avatar

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Avatar/size` | `Large` · `Medium` · `Small` | — | — |
| `Avatar/variant` | `Circular` · `Square` · `Rounded` | — | — |
| `Avatar/content` | `Image` · `Text` · `Icon` | Image when photo available; Text for initials fallback; Icon for non-person entities | — |
| `AvatarGroup/spacing` | `Medium` -8px overlap / `Small` -12px overlap | Use Small spacing for tighter layouts with many avatars | — |

### Alert

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Alert/Property1` | `Error` #F9D1D1 · `Warning` #FAF6DA · `Success` #C5E8E2 · `Info` rgba(131,205,240,0.2) | Inline page-level feedback messages; not interruptive, no user action required | Do not use Alert when a modal Dialog is required for decisions |

**React app:** `Toast` for transient feedback. `ApiError` / `GenericError` for error states. `MuiErrorTooltip` for inline field-level errors.

### Tooltip

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Tooltip/type` | `arrow` | — | — |
| `Tooltip/placement` | `top` · `top-start` · `top-end` · `bottom` · `bottom-start` · `bottom-end` · `left` · `right` | Appears on hover, focus, or touch; disappears after short duration | Do not use for critical or actionable content — use Popover/Dialog instead |
| `TooltipIcon/icon` | `Question` / `Info` | Standalone help icon that triggers tooltip on hover | — |

**React app:** `InfoPopoverHover` for hover-triggered info popovers.

### Dialog (Modal)

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Dialog/size` | `extraSmall` 320px · `small` 600px · `medium` 900px · `large` 1200px | Match size to content complexity. Small for confirmations, large for forms or embedded tables. | Do not use modal for non-critical or non-decision content |
| `ModalHeader/type` | `default` / `assessment` | assessment type adds assessment-specific controls and layout | — |
| `ModalFooter/verticalScroll` | `true` / `false` | verticalScroll=true adds sticky footer shadow to indicate scrollable content above | — |

**React app:** Use `MuiModal` (`src/common/components/new/MuiModal/`) for all standard dialogs. New modal footers must use `SaveButton` / `CancelButton` from `MuiButton/`.

### Tabs

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Tabs/behaviour` | `Fill` / `Left-Alligned` | Fill: tabs span full width. Left-Alligned: tabs cluster left. | — |
| `_Tab/state` | `enabled` · `disabled` · `hovered` | — | — |
| `_Tab/isSelected` | `true` (#83CDF0 bottom border) / `false` | — | — |
| `_Tab/size` | `M` · `S` | Mobile tabs are horizontally scrollable | — |

### Divider

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Divider/variant` | `fullWidth` · `middle` · `inset` | Thin visual separator for grouping UI elements. Reinforces visual hierarchy. | Do not use as primary structural spacing — prefer spacing tokens |
| `Divider/orientation` | `horizontal` / `vertical` | — | — |

### ListItem

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `ListItem/variant` | `Default` · `Hover` · `Selected` · `Disabled` | — | — |
| `ListItem/spacing` | `Default` / `Condensed` | Use Condensed for dense data lists or sidebar navigation | — |

### SnackBar

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `SnackBar/Type` | `Success` · `Warning` · `Error` · `Info` | Brief process notifications (toasts). Bottom of screen. Auto-dismisses. | Do not use for errors requiring user action — use Alert or Dialog instead |

**React app:** `Toast` (`src/common/components/new/`) is the React implementation.

### Stepper

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `StepperStep/position` | `start` · `middle` · `end` | — | — |
| `StepperStep/state` | `default` · `disabled` · `active` · `completed` | Guide users through multi-step flows | — |
| `Stepper/IsMobile` | `true` / `false` | — | — |

**React app:** `StepWizard` / `StepIcon` for multi-step wizard flows. `NavigationButtons` for back/next wizard controls.

### DatePicker

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `DatePicker/state` | `default` · `filled` · `error` · `hover` · `focus` | — | — |
| `DatePickerCalendar/type` | `singleSelect` / `dateRange` | — | — |
| `_DatePickerDate/state` | `today` · `active` · `disabled` · `hover` · `selected` · `selectedMiddle` | selectedMiddle applies to dates within a selected range (non-endpoint) | — |

**React app:** `DatePickerFormInput` + `@mui/x-date-pickers`.

### MultiFileDropzone

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `MultiFileDropzone/size` | `large` 700x309px / `medium` 700px wide | — | — |
| `MultiFileDropzone/state` | `default` · `focus` · `loading` · `uploaded` · `error` · `success` · `disabled` | Focus uses #83CDF0 dashed border and light blue bg | — |

### DataGrid

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `DataGridCell/type` | `Title` · `Text` · `Chip` · `Icon` · `Completion` · `Checkbox` · `Menu` | Match cell type to data: Text for strings, Chip for status, Checkbox for selection, Menu for row actions | — |
| `DataGridRow/type` | `Top` (header) / `Mid` (body row) | — | — |
| `DataGridRow/table` | `Default` / `Nested` | Nested applies slightly different bg (#FCFDFD) for child rows | — |

**React app:** `InxTable`, `FilterTable`, `DetailsPanelTable` + `@mui/x-data-grid-pro`. Do not reimplement tables with bare `<table>` for large data features.

### Navigation / Header / Footer

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Navbar/type` | `Desktop` / `Mobile` | — | — |
| `Navbar/activeSubmenu` | `None` · `SustainabilityMonitoring` · `Actions` · `UserProfile` | — | — |
| `Header/device` | `desktop` (1440px) / `mobile` (430px) | — | — |
| `Header/hasIndicator` | `true` / `false` | Show notification badge/indicator on header | — |
| `Breadcrumbs/device` | `Desktop` / `Mobile` | Secondary navigation showing page hierarchy | — |

**React app navigation module** (`src/modules/navigation/`):

| Component | Path | Notes |
|---|---|---|
| `Sidebar` | `components/Sidebar/Sidebar.tsx` | Rail width, collapse control, logo |
| `NavMenuItems` | `components/NavMenuItems/NavMenuItems.tsx` | Menu rows, collapsible group, active states (primary[20]), desktop flyout |
| `MainNavigationMenuItems` | `components/NavMenuItems/MainNavigationMenuItems.tsx` | — |
| `DashboardNavigationMenuItems` | `components/NavMenuItems/DashboardNavigationMenuItems.tsx` | — |

### PageHeader + DashboardFilters

| Component | Path | When to use | When to avoid |
|---|---|---|---|
| `PageHeader` | `src/common/components/new/PageHeader/` | Dashboard-style pages — PageHeader + PageContainer + DashboardFilters is the standard stack | — |
| `DashboardFilters` | `src/common/components/new/` | Filter rows on dashboard pages. Filters modal uses MuiModal + FilterSelects internally. | Do not rebuild filter UI from scratch with raw Select when DashboardFilters already exists |

### Forms

| Component | Path | When to use | When to avoid |
|---|---|---|---|
| `InxForm` | `src/common/components/new/` + react-final-form | Assessment flows, settings, and any pattern already on InxForm | Avoid parallel one-off form state without team agreement |
| `FormField` | `src/common/components/new/` | Generic field wrapper for InxForm | — |
| `FormSelect` | `src/common/components/new/` | Form-bound select/dropdown | — |
| `FormCheckbox` | `src/common/components/new/` | Form-bound checkbox | — |
| `FormSwitch` | `src/common/components/new/` | Form-bound toggle | — |
| `FormSlider` | `src/common/components/new/` | Form-bound slider | — |
| `DatePickerFormInput` | `src/common/components/new/` | Form-bound date picker | — |
| `FormButtonGroup` | `src/common/components/new/` | Grouped chip-style toggle buttons in forms | — |

### Pagination

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Pagination/position` | `Start` · `Middle` · `End` | Shows user location within content set; enables direct page access | — |

### IndicatorBar

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `IndicatorNew/Progress` | `0` to `5` (6 levels) | Visual completion/score indicator for assessment progress or compliance score | — |
| `IndicatorOld/Status` | `Red` · `Yellow` · `Green` | Legacy 3-state indicator for older assessments | Prefer IndicatorNew for new designs |

### Progress / Skeleton / Scrollbar

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Progress/Property1` | `Variant 1` · `Variant 2` · `Variant 3` | Spinners for unspecified wait times or process length display | — |
| `Skeleton/Property1` | `skeleton` rgba(211,211,211,0.1) / `darkerState` rgba(211,211,211,0.4) | Placeholder preview while content loads; reduces load-time frustration | Do not keep visible once data has loaded |
| `Scrollbar/Size` | `Small` 6x80px · `Medium` 6x263px · `Large` 6x512px | Vertical and horizontal scrollable content containers | — |

**React app:** `Loader` for full-page / section loading states.

### Filters

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Filters/isExpanded` | `true` / `false` | Allow users to narrow large datasets with structured criteria | — |
| `Filters/version` | `current` / `new` | — | — |
| `FilterTags/State` | `Default` (#002031 bg) / `State2` (rgba(131,205,240,0.1) bg) | Active filter tags shown below filter panel | — |

### EmptyState

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `EmptyState/size` | `medium` · `large` | Indicate no data in current view; often includes alternative action | Do not show EmptyState while data is still loading — use Skeleton |
| `EmptyState/hasSurface` | `yes` (white bg card) / `no` (transparent) | Use hasSurface=yes when empty state sits on a non-white background | — |

**React app:** `CustomNoRowsOverlay` for empty data grid states. `GenericError` / `ErrorPage` for error-level empty states.

### Link

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Link/state` | `default` · `hover` · `disabled` | Use `<a>` for navigation to another page/URL; use Button for in-page actions | Do not style a Button as a Link for page navigation |
| `Link/size` | `bodyLarge` / `bodySmall` | Match link size to surrounding body text | — |

### Backdrop

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `Backdrop` | `rgba(0, 32, 49, 0.2)` fill · 645x379px default | Narrows user focus to a foreground element (modal, dialog) | Do not use without a foreground surface/dialog on top |

---

## Responsive Breakpoints

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `breakpoint/xs` | `0 – 599dp` | Extra small mobile screens | — |
| `breakpoint/sm` | `600 – 904dp` | Small mobile/tablet | — |
| `breakpoint/md-low` | `905 – 1239dp` | Medium tablet/small desktop | — |
| `breakpoint/md-high` | `1240 – 1439dp` | Medium-large desktop | — |
| `breakpoint/lg` | `1440dp+` | Large desktop; primary design target | — |

---

## Icons

| Variable Name | Values | When to use | When to avoid |
|---|---|---|---|
| `icon/library` | Streamline Light 3.0 (Figma) · Phosphor wrappers (React app, `src/common/icons/`) | Figma: all design assets. React app: Phosphor-based wrappers for all product icons. | Do not mix icon families within the same surface |
| `icon/file-format` | `excel` · `excel(new)` · `doc` · `ppt` · `pdf` | File type indicators in attachment lists and upload contexts | — |
| `icon/indicator` | Type: `Error` · `Warning` · `Success` · Cross: `Yes` / `No` | Status badge icons for assessment responses | — |

---

## External UI Dependencies

| Package | Role |
|---|---|
| `@mui/material` | Core layout and inputs |
| `@mui/x-data-grid-pro` | Tables with column APIs, export, pro licence |
| `@mui/x-date-pickers` | Date picker components |
| `@emotion/react` / `styled` | Styling stack used by MUI |
| `react-intl` | Copy keys in `src/common/state/intl/langs.*.json` |
| `react-final-form` | Form state management via `InxForm` |
| `react-router` | Navigation via `NavLink` |

---

## Shared Components with Configuration Docs

| Area | Path (`src/common/components/new/...`) |
|---|---|
| MUI button wrappers (Cancel, Save, CSV, Underlined, actions, circle icon) | `MuiButton/` |
| Page masthead | `PageHeader/` |
| Modal dialog (title, content, footer, save/cancel) | `MuiModal/` |
| Text field | `FormInput/` |
| Toggle + label | `LabelledSwitch/` |
| Wizard back/next | `NavigationButtons/` |
| Pager | `Pagination/` |

---

## Other React App Components in Heavy Use

| Category | Components |
|---|---|
| **Layout / chrome** | `PageContainer`, `SectionContainer`, `Breadcrumb`, `CrumbMessages`, `InxLogo` |
| **Filters & modals** | `DashboardFilters`, `components/Filters`, `FilterSelects` |
| **Forms** | `InxForm`, `FormField`, `FormSelect`, `FormCheckbox`, `FormSwitch`, `FormSlider`, `DatePickerFormInput`, `FormButtonGroup` |
| **Tables & lists** | `InxTable`, `FilterTable`, `DetailsPanelTable`, `CustomNoRowsOverlay` + `@mui/x-data-grid-pro` |
| **Autocomplete & search** | `Autocomplete/MultiSelectAutocomplete`, `SearchField`, `SingleFilterAutocomplete` |
| **Feedback** | `Toast`, `ApiError`, `Loader`, `GenericError`, `ErrorPage`, `MuiErrorTooltip` |
| **Content** | `Instructions`, `PerformanceCard`, `StepWizard` / `StepIcon`, `TooltipChip`, `InfoPopoverHover` |

---

## Related Entry Points

| Doc | Purpose |
|---|---|
| [README.md](README.md) | Design-system folder overview and Button quick start |
| [COMPONENT_CATALOG.md](COMPONENT_CATALOG.md) | Index of all `COMPONENT_CONFIGURATION.md` files |
