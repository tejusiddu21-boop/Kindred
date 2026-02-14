# Dependencies

> A plain-English breakdown of every package Kindred relies on -- what it does, why we need it, and how it fits into the bigger picture.

---

## The Short Version

Kindred is a Next.js 16 app built with React 19, styled with Tailwind CSS, animated with Framer Motion, and using shadcn/ui (powered by Radix UI) for accessible, well-built interface components. That's the core. Everything else supports those pillars.

---

## Core Framework

| Package | Version | What It Does |
|---------|---------|--------------|
| `next` | 16.1.6 | The framework that runs everything. Handles routing, server-side rendering, bundling (Turbopack), and deployment. Kindred is a Next.js App Router project. |
| `react` | 19.2.3 | The UI library. Every component you see -- the Moon Button, the Time Capsule cards, the Gratitude Wall -- is a React component. Version 19 brings improved performance and new hooks. |
| `react-dom` | 19.2.3 | The bridge between React and the browser. Takes our React components and actually puts them on the screen. Always matches the React version. |

---

## Animation

| Package | Version | What It Does |
|---------|---------|--------------|
| `framer-motion` | ^11.15.0 | **This is the soul of Kindred's feel.** Every fade-in, every slide-up, the Moon Button's scale pulse, the login transition, the Time Capsule card reveals -- all Framer Motion. It makes the app feel alive without us writing raw CSS keyframes for everything. |

---

## Styling

| Package | Version | What It Does |
|---------|---------|--------------|
| `tailwindcss` | ^3.4.17 | Utility-first CSS framework. Instead of writing separate CSS files, we style directly in our JSX with classes like `bg-background`, `text-foreground`, `rounded-lg`. Keeps everything consistent and fast. |
| `tailwindcss-animate` | ^1.0.7 | Adds animation utilities to Tailwind. Things like `animate-in`, `fade-in`, `slide-in` become available as simple class names. |
| `tailwind-merge` | ^2.5.5 | Smartly merges Tailwind classes when they conflict. If a component has `p-4` by default but you pass `p-8`, this makes sure `p-8` wins instead of both fighting each other. |
| `class-variance-authority` | ^0.7.1 | Helps build component variants cleanly. When a Button needs `default`, `outline`, and `ghost` variants, CVA handles the logic of which classes apply when. |
| `clsx` | ^2.1.1 | A tiny utility for conditionally joining class names. `clsx("base", isActive && "active")` -- simple and clean. |
| `autoprefixer` | ^10.4.20 | Automatically adds vendor prefixes to CSS so things like `backdrop-filter` work across all browsers without us manually writing `-webkit-backdrop-filter`. |

---

## UI Components (shadcn/ui + Radix UI)

shadcn/ui gives us beautifully designed, accessible components. Under the hood, each one is powered by a Radix UI primitive -- headless, WAI-ARIA compliant building blocks. We don't use every single one of these in Kindred right now, but they come as part of the shadcn/ui setup and are ready when we need them.

| Package | What It Provides |
|---------|-----------------|
| `@radix-ui/react-accordion` | Expandable/collapsible content sections |
| `@radix-ui/react-alert-dialog` | Modal dialogs that require user acknowledgment |
| `@radix-ui/react-aspect-ratio` | Maintains consistent width/height ratios |
| `@radix-ui/react-avatar` | User profile images with fallback initials |
| `@radix-ui/react-checkbox` | Accessible checkboxes with custom styling |
| `@radix-ui/react-collapsible` | Show/hide content with smooth transitions |
| `@radix-ui/react-context-menu` | Right-click context menus |
| `@radix-ui/react-dialog` | Modal dialogs and overlays |
| `@radix-ui/react-dropdown-menu` | Dropdown menus with keyboard navigation |
| `@radix-ui/react-hover-card` | Content that appears on hover |
| `@radix-ui/react-label` | Accessible form labels |
| `@radix-ui/react-menubar` | Application menu bars |
| `@radix-ui/react-navigation-menu` | Site navigation with submenus |
| `@radix-ui/react-popover` | Floating content panels |
| `@radix-ui/react-progress` | Progress bars (used in the Time Capsule "Syncing emotions..." animation) |
| `@radix-ui/react-radio-group` | Radio button groups |
| `@radix-ui/react-scroll-area` | Custom scrollbars that look consistent across browsers |
| `@radix-ui/react-select` | Custom select dropdowns |
| `@radix-ui/react-separator` | Visual dividers between content |
| `@radix-ui/react-slider` | Range sliders |
| `@radix-ui/react-slot` | Polymorphic component rendering (lets components render as different HTML elements) |
| `@radix-ui/react-switch` | Toggle switches |
| `@radix-ui/react-tabs` | Tabbed interfaces |
| `@radix-ui/react-toast` | Notification toasts |
| `@radix-ui/react-toggle` | Toggle buttons |
| `@radix-ui/react-toggle-group` | Groups of toggle buttons |
| `@radix-ui/react-tooltip` | Hover tooltips |

---

## Icons

| Package | Version | What It Does |
|---------|---------|--------------|
| `lucide-react` | ^0.544.0 | The icon library. Every icon in Kindred -- the moon, the lock, the heart, the sparkles, the send arrow -- comes from Lucide. Clean, consistent, and lightweight. |

---

## Forms and Validation

| Package | Version | What It Does |
|---------|---------|--------------|
| `react-hook-form` | ^7.54.1 | Manages form state without unnecessary re-renders. Used in the login form and the Creator note-writing form. |
| `@hookform/resolvers` | ^3.9.1 | Connects react-hook-form to validation libraries like Zod. |
| `zod` | ^3.24.1 | Schema validation. Defines what valid data looks like and rejects anything that doesn't match. Used to validate form inputs. |
| `input-otp` | 1.4.1 | One-time password input component. Available for verification code entry in the login flow. |

---

## Utilities

| Package | Version | What It Does |
|---------|---------|--------------|
| `date-fns` | 4.1.0 | Date formatting and manipulation. Lightweight alternative to Moment.js. Used for things like displaying when a Time Capsule was created. |
| `cmdk` | 1.1.1 | Command palette component. The search/command interface pattern (Cmd+K). Available for future navigation features. |
| `next-themes` | ^0.4.6 | Theme management for Next.js. Handles dark/light mode toggling and system preference detection. |
| `sonner` | ^1.7.1 | Beautiful toast notifications. When you send a note in Creator or complete a mood check-in, the confirmation toast comes from Sonner. |
| `vaul` | ^1.1.2 | Drawer component for mobile. Slides up from the bottom of the screen -- the mobile-friendly alternative to modals. |

---

## Layout

| Package | Version | What It Does |
|---------|---------|--------------|
| `react-resizable-panels` | ^2.1.7 | Draggable, resizable panel layouts. Available for future dashboard customization features. |
| `embla-carousel-react` | 8.5.1 | Carousel/slider component. Lightweight and touch-friendly. Available for future content browsing features. |
| `react-day-picker` | 8.10.1 | Calendar date picker. Available for scheduling Time Capsule deliveries in future versions. |

---

## Charts

| Package | Version | What It Does |
|---------|---------|--------------|
| `recharts` | 2.15.0 | React charting library built on D3. Available for future features like mood tracking trends over time, community wellness dashboards, etc. |

---

## Dev Dependencies

These only run during development and building -- they never ship to users.

| Package | Version | What It Does |
|---------|---------|--------------|
| `typescript` | 5.7.3 | Type safety for the entire codebase. Catches bugs before they happen. Every `.tsx` file is TypeScript. |
| `@types/node` | ^22 | TypeScript definitions for Node.js APIs. |
| `@types/react` | 19.2.7 | TypeScript definitions for React 19. Tells TypeScript what props each React API expects. |
| `@types/react-dom` | 19.2.3 | TypeScript definitions for ReactDOM. |
| `postcss` | ^8.5 | CSS processing pipeline. Tailwind runs as a PostCSS plugin. |
| `@tailwindcss/postcss` | ^4.1.13 | The PostCSS plugin that makes Tailwind CSS work in the build pipeline. |

---

## What's Actually Used vs. What's Available

To be transparent: not every package listed above is actively used in the current version of Kindred. The shadcn/ui setup installs a full component library, and packages like `recharts`, `react-day-picker`, and `embla-carousel-react` are available for upcoming features but aren't in the current UI.

**Actively powering Kindred right now:**
- `next`, `react`, `react-dom` -- the foundation
- `framer-motion` -- all animations
- `tailwindcss`, `tailwind-merge`, `clsx`, `class-variance-authority` -- all styling
- `lucide-react` -- all icons
- `@radix-ui/react-progress` -- Time Capsule progress bar
- `@radix-ui/react-slot` -- component polymorphism in shadcn/ui Button
- `sonner` -- toast notifications
- `typescript` -- type safety across the board

**Ready for the next iteration:**
- `recharts` -- mood tracking visualizations
- `react-day-picker` -- scheduling Time Capsules
- `zod` + `react-hook-form` -- robust form validation
- `cmdk` -- command palette navigation
- Everything else in the Radix UI family

---

## Installing Everything

```bash
pnpm install
```

That's it. One command. pnpm reads `package.json` and handles the rest.

---

## A Note on Bundle Size

We care about performance. Kindred should load fast, even on a phone with weak signal in a dorm room at 2am -- because that's exactly when someone might need it most.

- **Next.js** automatically tree-shakes unused code out of the production bundle
- **Radix UI** primitives are individually packaged -- importing one doesn't pull in all the others
- **Lucide** icons are individually tree-shakeable -- only the icons we actually use end up in the bundle
- **Framer Motion** is the heaviest library we use (~30KB gzipped), but the emotional experience it creates is worth every byte

---

*Last updated: February 2026*
