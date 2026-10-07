---
name: Academic Matte Dark
colors:
  surface: '#051424'
  surface-dim: '#051424'
  surface-bright: '#2c3a4c'
  surface-container-lowest: '#010f1f'
  surface-container-low: '#0d1c2d'
  surface-container: '#122131'
  surface-container-high: '#1c2b3c'
  surface-container-highest: '#273647'
  on-surface: '#d4e4fa'
  on-surface-variant: '#c3c6d7'
  inverse-surface: '#d4e4fa'
  inverse-on-surface: '#233143'
  outline: '#8d90a0'
  outline-variant: '#434655'
  surface-tint: '#b4c5ff'
  primary: '#b4c5ff'
  on-primary: '#002a78'
  primary-container: '#2563eb'
  on-primary-container: '#eeefff'
  inverse-primary: '#0053db'
  secondary: '#4edea3'
  on-secondary: '#003824'
  secondary-container: '#00a572'
  on-secondary-container: '#00311f'
  tertiary: '#ffb95f'
  on-tertiary: '#472a00'
  tertiary-container: '#996100'
  on-tertiary-container: '#ffeedd'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#dbe1ff'
  primary-fixed-dim: '#b4c5ff'
  on-primary-fixed: '#00174b'
  on-primary-fixed-variant: '#003ea8'
  secondary-fixed: '#6ffbbe'
  secondary-fixed-dim: '#4edea3'
  on-secondary-fixed: '#002113'
  on-secondary-fixed-variant: '#005236'
  tertiary-fixed: '#ffddb8'
  tertiary-fixed-dim: '#ffb95f'
  on-tertiary-fixed: '#2a1700'
  on-tertiary-fixed-variant: '#653e00'
  background: '#051424'
  on-background: '#d4e4fa'
  surface-variant: '#273647'
typography:
  headline-lg:
    fontFamily: Inter
    fontSize: 30px
    fontWeight: '700'
    lineHeight: 38px
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
    letterSpacing: -0.015em
  headline-sm:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 26px
    letterSpacing: -0.01em
  title-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 22px
    letterSpacing: -0.005em
  title-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
    letterSpacing: 0em
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
    letterSpacing: 0em
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
    letterSpacing: 0em
  body-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
    letterSpacing: 0.01em
  label-lg:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
    letterSpacing: 0.01em
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.02em
  label-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '600'
    lineHeight: 14px
    letterSpacing: 0.04em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1rem
  margin: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 0.75rem
  space-lg: 1rem
  space-xl: 1.5rem
---

## Brand & Style

This design system delivers a focused, utilitarian, and high-legibility dark interface tailored for academic planning, timetable management, and institutional workflows on Android. Engineered specifically for concentrated educational sessions and dense scheduling, the design language rejects distracting neon glows, saturated cyan highlights, or heavy glassmorphism in favor of a restrained, matte-slate aesthetic.

Key brand attributes:
- **Discipline & Clarity:** Academic information takes immediate precedence. Visual noise is stripped down so that course schedules, attendance states, and conflict alerts are parseable at a glance under harsh or low-light conditions.
- **Architectural & Grounded:** Rooted in deep slate tones with crisp structural borders, evoking precision, dependability, and academic rigor.
- **Calm Authority:** Status signals are distinct and purposeful, preventing cognitive fatigue during prolonged operational use.

## Colors

The palette establishes strict contrast hierarchy through layered matte surfaces rather than lighting effects or decorative gradients.

### Core Surfaces
- **Global Canvas / Surface Dim:** `#0B0F17` — Deep neutral slate base. Strictly zero saturated navy tinting or chromatic aberration.
- **Surface Container Low:** `#111827` — Recessed zones, empty slate placeholders, and grouped list backings.
- **Surface / Card Surface:** `#161F30` — Primary matte elevated surface for scheduling tiles, cards, and bottom sheets.
- **Surface Container High:** `#1E293B` — Active elevated headers, floating dialog surfaces, and dropdown layers.
- **Structural Stroke:** `#26334D` — Uniform 1px border applied to containers and card dividers to preserve separation against `#0B0F17`.

### Typography Colors
- **Text Primary:** `#F8FAFC` — High-contrast white for course titles, time markers, and key headings.
- **Text Secondary:** `#94A3B8` — Neutral slate gray for meta tags, instructor labels, and structural captions.
- **Text Disabled:** `#475569` — Low-contrast slate for inactive terms and locked modules.

### Functional & Semantic Accents
- **Primary Accent:** `#2563EB` (Royal Blue) — Reserved strictly for focused tabs, primary actions, and current-time indicators.
- **Success / Present:** `#10B981` with container `#064E3B` and border `#047857` (used for verified attendance states such as "Có mặt" and open enrollment periods like "Đang mở").
- **Danger / Conflict:** `#EF4444` with container `#450A0A` and border `#DC2626` (used for overlapping class schedules, room collisions, and overdue submissions).
- **Warning / Offline:** `#F59E0B` with container `#451A03` and border `#B45309` (used for pending prerequisites, unconfirmed room assignments, and offline statuses).

## Typography

Typography is powered entirely by **Inter**, leveraging its tall x-height, neutral geometric forms, and high legibility for dense technical interfaces.

- **Tabular Figures:** Timetable hours, room codes, credit counts, and numerical dates must be rendered using tabular numerical variants (`font-feature-settings: "tnum" on, "cv05" on`) to maintain column vertical alignment across schedule timelines.
- **Visual Hierarchy:** Headlines use tighter tracking (`-0.02em` to `-0.01em`) to maintain solidity in tight Android layouts. Status tags and micro metadata utilize `label-sm` with tracked uppercase letters (`+0.04em`) to remain sharp against dark semantic containers.

## Layout & Spacing

Targeted at Android devices with a base canvas of 360 × 800 dp, layout metrics respect standard Material Design 3 4dp/8dp spatial increments.

### Grid & Density Rules
- **Canvas Margins:** Fixed 16dp (`1rem`) on horizontal edges to maximize usable surface on standard 360dp screens.
- **Gutter:** 16dp (`1rem`) between card grids or timetable columns.
- **Timetable Track:** Vertical agenda lists use a rigid 8dp baseline grid. Schedule blocks match duration heights with strict min-height boundaries (e.g., 48dp per 45-minute lecture slot) to prevent label clipping.
- **Safe Areas:** 48dp minimum bottom navigation clearing; top app bars conform to a 56dp single-row or 96dp extended collapsible height.

## Elevation & Depth

This system intentionally eliminates blurred drop shadows, ambient glow halos, and diffuse lighting. Elevation is conveyed strictly through **tonal stacking** and **crisp 1px boundary strokes**.

1. **Base Tier (0dp):** Global background `#0B0F17`.
2. **Structural Tier 1 (Cards, Modules, Schedule Blocks):** Surface `#161F30` outlined with a solid `1px solid #26334D`. No shadow.
3. **Elevated Tier 2 (Bottom Sheets, Popovers, Modals):** Surface Container High `#1E293B` bounded by `1px solid #334155`. Accompanied by a 60% opacity `#000000` scrim for full focus trapping.
4. **Dividers & Insets:** Hairline `1px` lines tinted with `#1F293D` inside cards to compartmentalize lecture time, instructor name, and room locations without breaking structural unity.

## Shapes

The shape hierarchy establishes clear tactile differentiation across card blocks, clickable controls, and informative chips:

- **Schedule Cards & Content Modules:** `16px` (`rounded-2xl`). This softens large content boxes on the 360dp canvas without sacrificing edge efficiency.
- **Buttons, Inputs, & Form Fields:** `12px` (`rounded-xl`). Matches the interactive touch targets while remaining visually distinct from the larger structural cards.
- **Status Badges, Filter Chips, & Pills:** `9999px` (`rounded-full`). Unambiguously tags contextual states (attendance, credit chips, open badges) as metadata rather than tappable cards.

## Components

### Buttons
- **Primary Button:** `#2563EB` background with `#F8FAFC` label (`label-lg`). Height: 48dp, corner radius: 12dp. Pressed state shifts to `#1D4ED8`. Never use outer drop shadows.
- **Secondary / Surface Button:** `#161F30` background with `1px solid #26334D`, `#F8FAFC` label. Pressed state transitions to `#1E293B`.
- **Destructive Action:** `#450A0A` background with `1px solid #DC2626` and `#EF4444` label.

### Academic Cards & Schedule Modules
- **Container:** `#161F30` background with `1px solid #26334D` and 16dp rounded corners.
- **Left Accent Indicator:** For current or conflicting courses, include an internal 4dp solid left edge bar (`#2563EB` for active session, `#EF4444` for schedule conflict).
- **Padding:** 12dp vertical, 16dp horizontal to preserve screen space while maintaining touch comfort.

### Status Chips & Badges
- **Present / Open ("Có mặt" / "Đang mở"):** Container `#064E3B`, border `1px solid #047857`, label `#10B981` (`label-sm`).
- **Conflict / Urgent:** Container `#450A0A`, border `1px solid #DC2626`, label `#EF4444` (`label-sm`).
- **Pending / Offline:** Container `#451A03`, border `1px solid #B45309`, label `#F59E0B` (`label-sm`).
- **Shape:** Fully rounded pills (`rounded-full`) with 4dp vertical and 10dp horizontal internal padding.

### Input Fields & Selectors
- **Container:** `#111827` surface background, 12dp corner radius, 48dp height.
- **Resting Border:** `1px solid #26334D`.
- **Focused State:** `1px solid #2563EB` with an optional 1px outer stroke in `#2563EB` (no diffuse blur).
- **Text:** Input text `#F8FAFC`, placeholder `#475569`.

### Selection Controls (Checkbox & Radio)
- **Unchecked:** 20×20dp box/circle, `#111827` fill with `2px solid #334155`.
- **Checked:** Filled `#2563EB` with `#F8FAFC` checkmark icon or center dot. Radius: 6dp for checkbox, 9999px for radio.

### Bottom Navigation Bar (Android M3)
- **Container:** `#0B0F17` background with a continuous top border of `1px solid #1E293B`. Height: 64dp.
- **Active Tab:** Icon and text colored `#2563EB` sitting above an optional muted pill indicator (`#161F30`).
- **Inactive Tab:** Icon and text colored `#94A3B8`.