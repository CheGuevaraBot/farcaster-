# Farcaster Raffle Bot - Design Guidelines

## Design Approach: Utility-First with Modern Web3 Aesthetics

**Selected Approach**: Design System (Tailwind-based) with inspiration from Linear and Material Design
**Justification**: This is a utility-focused application requiring clear information hierarchy, efficient workflows, and technical precision. The design should prioritize usability and clarity over decorative elements.

---

## Core Design Elements

### A. Color Palette

**Dark Mode (Primary)**
- Background: 12 8% 6% (deep charcoal)
- Surface: 12 8% 10% (elevated surface)
- Surface Elevated: 12 8% 14% (cards, panels)
- Border: 12 8% 20% (subtle dividers)
- Text Primary: 0 0% 98%
- Text Secondary: 0 0% 71%
- Text Muted: 0 0% 50%

**Brand Colors**
- Primary: 262 83% 58% (vibrant purple - Farcaster-inspired)
- Primary Hover: 262 83% 65%
- Success: 142 76% 36% (green for winners)
- Warning: 38 92% 50% (amber for pending states)
- Error: 0 84% 60% (red for errors/leave actions)

**Light Mode (Secondary)**
- Background: 0 0% 100%
- Surface: 0 0% 98%
- Surface Elevated: 0 0% 96%
- Border: 0 0% 90%
- Invert text values accordingly

### B. Typography

**Font Families**
- Primary: 'Inter' (via Google Fonts CDN)
- Monospace: 'JetBrains Mono' (for FIDs, transaction hashes)

**Type Scale**
- Display: text-4xl font-bold (raffle titles)
- Heading 1: text-3xl font-semibold (page titles)
- Heading 2: text-2xl font-semibold (section headers)
- Heading 3: text-xl font-medium (card headers)
- Body: text-base font-normal (default text)
- Body Small: text-sm font-normal (metadata, timestamps)
- Caption: text-xs font-medium uppercase tracking-wide (labels)
- Code: text-sm font-mono (technical data)

### C. Layout System

**Spacing Primitives**: Use Tailwind units of **2, 4, 6, 8, 12, 16, 24** exclusively
- Component padding: p-4 to p-6
- Section spacing: py-12 to py-16
- Card gaps: gap-4 to gap-6
- Element margins: m-2 to m-8

**Container Strategy**
- Max width: max-w-7xl for main containers
- Admin panel: max-w-6xl centered
- Frame view: max-w-md (mobile-optimized for Warpcast)
- Grid layouts: grid-cols-1 md:grid-cols-2 lg:grid-cols-3

### D. Component Library

**1. Frame Interface (Frog.js Generated)**
- Aspect ratio: 1.91:1 (Farcaster Frame standard)
- Background: Gradient from primary to primary-hover
- Raffle title: Large, bold, centered white text
- Metadata bar: Bottom-aligned, semi-transparent dark background
  - Participants count with user icon
  - Time remaining with clock icon
  - Prize display with gift icon
- Action buttons: Full-width, high contrast (Join/Leave)
- Button states: Disabled state for ended raffles, active state for live ones

**2. Admin Panel Navigation**
- Sidebar: w-64, fixed, dark surface with elevated bg
- Navigation items: px-4 py-2, rounded-lg, hover:bg-surface-elevated
- Active state: bg-primary/10 text-primary border-l-2 border-primary
- Logo/brand: pt-6 pb-8, centered

**3. Raffle Cards (Admin Dashboard)**
- Card container: bg-surface-elevated, rounded-xl, border border-border
- Padding: p-6
- Header: flex justify-between items-start
  - Title: text-xl font-semibold
  - Status badge: pill-shaped, uppercase text-xs
    - Active: bg-success/10 text-success
    - Ended: bg-border text-muted
    - Pending: bg-warning/10 text-warning
- Content grid: grid gap-4
  - Stat blocks: flex flex-col gap-1
    - Label: text-xs text-secondary uppercase
    - Value: text-2xl font-bold
- Footer actions: flex gap-2 pt-4 border-t border-border

**4. Data Tables (Participants List)**
- Table container: bg-surface rounded-lg border border-border
- Header row: bg-surface-elevated text-secondary text-xs uppercase font-medium
- Body rows: hover:bg-surface-elevated transition
- Cell padding: px-4 py-3
- Alternating rows: optional subtle stripe
- Column widths: FID (15%), Username (25%), Join Time (25%), Status (20%), Actions (15%)

**5. Forms (Create/Edit Raffle)**
- Input groups: space-y-6
- Labels: text-sm font-medium mb-2 block
- Text inputs: bg-surface border border-border rounded-lg px-4 py-2.5
  - Focus: ring-2 ring-primary/20 border-primary
- Textareas: Same styling, min-h-[120px]
- Select dropdowns: Same as text inputs with chevron icon
- Date/time pickers: Inline with calendar icon
- Error states: border-error text-error text-sm mt-1

**6. Buttons**
- Primary: bg-primary hover:bg-primary-hover text-white px-6 py-2.5 rounded-lg font-medium
- Secondary: bg-surface-elevated border border-border hover:bg-surface text-primary
- Destructive: bg-error hover:bg-error/90 text-white
- Ghost: hover:bg-surface-elevated text-secondary
- Icon buttons: p-2.5 rounded-lg (for actions)
- Loading state: opacity-70 cursor-not-allowed with spinner

**7. Modals/Dialogs**
- Overlay: bg-black/60 backdrop-blur-sm
- Content: bg-surface rounded-2xl shadow-2xl max-w-lg p-6
- Header: flex justify-between items-center pb-4 border-b border-border
- Footer: pt-6 border-t border-border flex justify-end gap-3

**8. Toasts/Notifications**
- Position: top-right, fixed
- Container: bg-surface-elevated border border-border rounded-lg shadow-lg p-4
- Success: border-l-4 border-success
- Error: border-l-4 border-error
- Auto-dismiss: 5 seconds with progress bar

**9. Empty States**
- Icon: text-6xl text-muted mb-4
- Heading: text-xl font-semibold mb-2
- Description: text-secondary mb-6
- CTA button: Primary style

**10. Loading States**
- Skeleton screens: bg-surface-elevated animate-pulse rounded
- Spinners: border-primary/20 border-t-primary (circular)
- Progress bars: bg-surface-elevated with bg-primary fill

### E. Animations

Use sparingly for functional feedback only:
- Hover transitions: transition-colors duration-200
- Modal entrance: fade + scale-95 to scale-100 (150ms)
- Toast slide-in: translate-x-full to translate-x-0 (300ms)
- Loading spinners: animate-spin
- NO scroll animations or parallax effects

---

## Page-Specific Layouts

### Frame View (Public)
- Single-column, mobile-first
- Raffle image/visual at top (if available)
- Title + description: centered, max-w-prose
- Stats row: grid grid-cols-3 gap-4 (participants/time/prize)
- Action buttons: mt-6, full-width or side-by-side
- Footer: Powered by branding, text-xs text-muted

### Admin Dashboard
- Grid: grid-cols-1 lg:grid-cols-3 gap-6
- Quick stats cards: 3 columns (total raffles, active, total participants)
- Active raffles section: full-width below stats
- Recent winners: sidebar widget (if space allows)

### Admin Raffle Management
- Two-column layout: md:grid-cols-[300px_1fr]
- Left: Filters + quick actions sidebar
- Right: Raffle cards or table view toggle
- Top bar: Search + Create button + Export CSV

### Admin Create/Edit Form
- Single column: max-w-2xl mx-auto
- Step indicator if multi-step
- Sections with clear headings
- Save/Cancel sticky footer on scroll

---

## Images

**Hero/Featured Images**: Not applicable for this utility application
**Raffle Thumbnails**: Admin can upload optional 1.91:1 images for Frame display
**Empty State Illustrations**: Use Heroicons or simple icon-based graphics
**Profile Pictures**: Circular FID-based avatars from Neynar (32px default, 48px for winners)