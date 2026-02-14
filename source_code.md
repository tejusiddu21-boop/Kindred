# Source Code Guide

> A human-readable walkthrough of every file in Kindred, what it does, and why it exists.
> This isn't auto-generated docs. It's written so a real person can sit down and understand how the whole thing fits together.

---

## Table of Contents

1. [The Big Picture](#the-big-picture)
2. [Project Structure](#project-structure)
3. [Core Files](#core-files)
   - [app/layout.tsx](#applayouttsx)
   - [app/page.tsx](#apppagetsx)
   - [app/globals.css](#appglobalscss)
   - [tailwind.config.ts](#tailwindconfigts)
4. [Components](#components)
   - [Login](#login)
   - [Dashboard Header](#dashboard-header)
   - [Moon Button](#moon-button)
   - [Time Capsule](#time-capsule)
   - [Creator](#creator)
   - [Mood Check-in](#mood-check-in)
   - [Gratitude Wall](#gratitude-wall)
5. [Design System](#design-system)
6. [Dependencies](#dependencies)
7. [How Everything Connects](#how-everything-connects)

---

## The Big Picture

Kindred is a single-page Next.js application. There's no backend, no database, no API routes. Everything lives in the browser. The app has two states: **logged out** (you see the login screen) and **logged in** (you see the dashboard). Framer Motion handles all the transitions between them.

The entire UI is built around a "deep space" aesthetic -- dark midnight blues, soft lavender glows, neon mint accents, glassmorphism cards, and subtle star-field backgrounds. Every interaction has a purpose: to make a student feel a little less alone.

---

## Project Structure

```
kindred/
  app/
    layout.tsx          -- Root layout, fonts, metadata
    page.tsx            -- Main page, state machine (login vs dashboard)
    globals.css         -- Design tokens, glassmorphism, animations
  components/
    kindred/
      login.tsx         -- Login screen with email + secret code
      dashboard-header.tsx  -- Sticky header with rotating support lines
      moon-button.tsx   -- The glowing encouragement button
      time-capsule.tsx  -- Three sealed messages with typewriter reveal
      creator.tsx       -- Write kind notes to peers
      mood-checkin.tsx  -- Emoji mood selector with validation messages
      gratitude-wall.tsx -- Masonry wall of anonymous kindness
  tailwind.config.ts    -- Custom fonts, extended theme
  package.json          -- Dependencies and scripts
```

---

## Core Files

### app/layout.tsx

This is the root of the application. It does three things:

1. **Loads two fonts** from Google Fonts:
   - **Inter** (`--font-inter`) -- Clean, modern sans-serif used for body text. Applied via the `font-sans` Tailwind class.
   - **Space Grotesk** (`--font-space-grotesk`) -- A geometric display font with personality. Applied via the `font-display` Tailwind class.
2. **Sets metadata** for SEO: the page title ("Kindred | Emotional Wellness & Connection") and a description that's universal, not tied to any specific university.
3. **Sets the viewport theme color** to `#0a0a23` (the deep midnight blue) so the browser chrome matches the app.

Both font CSS variables are injected into the `<html>` tag so Tailwind can pick them up.

---

### app/page.tsx

This is the heart of the app. It's a client component (needs `useState` for the login state) that acts as a simple state machine:

- **State:** `isLoggedIn` (boolean, starts `false`)
- **When `false`:** Renders the `<Login>` component. Passes an `onEnter` callback that flips the state.
- **When `true`:** Renders the full dashboard -- header, moon button, time capsule, creator, mood check-in, and gratitude wall. All stacked vertically in a `max-w-4xl` centered container.

The background has two layers:
- A repeating `stars-bg` pattern (tiny radial gradients that simulate distant stars)
- A gradient overlay that fades to the background color at the bottom

`AnimatePresence` from Framer Motion handles the crossfade between login and dashboard. The `mode="wait"` prop ensures the login fully exits before the dashboard enters.

---

### app/globals.css

This file does a lot. Here's what lives in it:

**Design Tokens (CSS Custom Properties):**
- `--background: 234 78% 8%` -- The deep midnight blue
- `--primary: 263 70% 70%` -- Soft lavender (the signature Kindred purple)
- `--accent: 160 80% 55%` -- Neon mint green (used for highlights and success states)
- Plus all the standard semantic tokens (card, muted, border, input, ring, etc.)
- `--radius: 1rem` -- Generous rounding for that soft, approachable feel

**Glassmorphism Classes:**
- `.glass` -- Semi-transparent dark background with 16px blur and a faint lavender border
- `.glass-strong` -- Same thing but more opaque and blurrier (used for the header and login card)

**Animations:**
- `moon-glow` -- A pulsing box-shadow that makes the moon button breathe
- `float` -- A gentle up-and-down bob
- `blink-cursor` -- The blinking typewriter cursor for the time capsule reveal

**Stars Background:**
- `.stars-bg` -- A repeating pattern of tiny radial gradients in lavender, mint, and white. Creates the illusion of a starfield without any JavaScript or canvas.

**Typewriter Cursor:**
- `.typewriter-cursor::after` -- Appends a blinking `|` character in mint green after the text being typed

**Custom Scrollbar:**
- Thin (6px), dark track, lavender thumb with hover state

---

### tailwind.config.ts

Extends the default Tailwind config with:

- **Custom font families:** `font-sans` maps to Inter, `font-display` maps to Space Grotesk
- **All the HSL color tokens** from globals.css, wrapped in `hsl(var(--token))` so they work with Tailwind's opacity modifiers (like `bg-primary/20`)
- **Generous border radius** from the `--radius` custom property
- **tailwindcss-animate** plugin for additional animation utilities

---

## Components

### Login
**File:** `components/kindred/login.tsx`

A centered glassmorphism card with:
- A pulsing Sparkles icon that breathes (scale animation, 3 second loop)
- "Kindred" title in Space Grotesk
- "Your emotional wellness space" subtitle
- **Email input** with placeholder "yourname@university.edu"
- **Secret code input** (password type)
- **"Enter Kindred" button** that calls `onEnter()` -- no actual auth, it just transitions to the dashboard
- A footer line: "A safe space for every student, everywhere"

The whole card slides up from 30px below with a staggered entrance (0.2s delay after the page fade-in).

**Props:**
- `onEnter: () => void` -- Called when the user clicks "Enter Kindred"

---

### Dashboard Header
**File:** `components/kindred/dashboard-header.tsx`

A sticky, strongly-glassed header that stays at the top as you scroll. Contains:

- **Left side:** Heart icon + "Kindred | For Every Student"
- **Right side (desktop only):** A rotating support line that changes every 4 seconds with a smooth fade + slide animation

The 5 support lines:
1. "You are more than your GPA."
2. "Take a deep breath."
3. "A kind word is waiting for you."
4. "You belong here, and you matter."
5. "Progress, not perfection."

Uses `setInterval` in a `useEffect` to cycle through them, with `AnimatePresence` handling the transitions.

---

### Moon Button
**File:** `components/kindred/moon-button.tsx`

The centrepiece interaction. A large (144px) circular button with:
- The `animate-moon-glow` CSS animation (pulsing lavender box-shadow)
- A Moon icon from Lucide that tilts 12 degrees on hover
- "I need encouragement" label

**On click:** Picks a random message from 10 handwritten encouragements and displays it in a glass card below. The card springs in with Framer Motion's spring physics (damping: 25, stiffness: 300). Has a close button (X icon) in the corner.

Some of the messages:
- "You don't have to have it all figured out today. You are doing enough."
- "You've survived 100% of your worst days so far."
- "The fact that you're here, trying, says everything."

---

### Time Capsule
**File:** `components/kindred/time-capsule.tsx`

A grid of 3 "sealed message" cards. Each card goes through three states:

1. **Sealed** -- Shows an envelope icon and an "Open Message" button
2. **Loading** -- Shows a spinner with "Syncing emotions..." text and an animated progress bar (fills over 1.5 seconds using 30 discrete steps)
3. **Revealed** -- The message appears letter-by-letter with a typewriter effect (20-50ms per character, randomised for natural feel)

The `TypewriterText` component is a standalone piece:
- Uses `useState` for the displayed text and current character index
- A `useEffect` with `setTimeout` adds one character at a time
- Shows a blinking cursor (via CSS class) until the text is complete

The three messages are:
1. **"From Your Future Self"** -- About trusting the process
2. **"A Gentle Reminder"** -- About not being behind
3. **"Words of Warmth"** -- About the impact of existing

---

### Creator
**File:** `components/kindred/creator.tsx`

A note-writing section where students can write kind messages. Contains:

- A `<textarea>` with placeholder "Write something kind..."
- **Vibe selector** -- Three pill buttons:
  - Support (Heart icon, lavender)
  - Celebration (PartyPopper icon, mint)
  - Just Because (Coffee icon, muted)
- **Send button** that transforms into a "Sent with love" confirmation (with a checkmark) for 2.5 seconds before resetting

The send button is disabled when the textarea is empty. The vibe selector highlights the active option with a lavender background.

**Note:** Currently client-side only. Notes aren't persisted anywhere -- this is the demo/prototype version.

---

### Mood Check-in
**File:** `components/kindred/mood-checkin.tsx`

Five emoji buttons in a row, each representing a mood:

| Emoji | Label | Validation Message |
|-------|-------|--------------------|
| Happy | "Your joy is contagious! Keep spreading that beautiful energy." |
| Sad | "It's okay to feel this way. Your feelings are valid, and brighter days are ahead." |
| Frustrated | "Take a moment. Breathe. You have the strength to get through this." |
| Tired | "Rest is not laziness. You deserve a break. Recharge and come back stronger." |
| Grateful | "Gratitude is a superpower. The world is better because you notice the good in it." |

Each emoji button scales up and lifts slightly on hover (`scale: 1.15, y: -4`). When selected, it gets a lavender ring highlight. The validation message appears below in a glass card with spring animation.

---

### Gratitude Wall
**File:** `components/kindred/gratitude-wall.tsx`

A masonry-style wall (CSS `columns-1 sm:columns-2`) of 8 pre-written anonymous gratitude cards. Each card has:

- A `MessageCircle` icon colour-coded by vibe type (support = lavender, celebration = mint, just-because = muted)
- An "Anonymous" label
- The gratitude message

The cards stagger their entrance (80ms apart) for a cascading reveal effect. Messages are universal -- about exam halls, lab partners, roommates, professors, library staff, and strangers. No campus-specific references.

---

## Design System

### Colours (3 core + neutrals)

| Role | HSL | What it looks like |
|------|-----|--------------------|
| Background | `234 78% 8%` | Deep midnight blue, almost black |
| Primary | `263 70% 70%` | Soft lavender purple |
| Accent | `160 80% 55%` | Neon mint green |
| Foreground | `240 20% 92%` | Near-white with a cool tint |
| Muted | `234 40% 16%` | Dark blue-grey |

### Typography

| Use | Font | Tailwind Class |
|-----|------|----------------|
| Body text | Inter | `font-sans` |
| Headings, buttons, titles | Space Grotesk | `font-display` |

### Visual Patterns

- **Glassmorphism** everywhere -- cards, header, popups
- **Generous rounding** (`rounded-2xl` on most elements)
- **Spring physics** for interactive animations (Framer Motion)
- **Staggered entrances** for lists and grids
- **No sharp edges, no flat surfaces** -- everything has depth through blur and transparency

---

## Dependencies

The ones that actually matter for Kindred:

| Package | Why |
|---------|-----|
| `next` (16.1.6) | The framework. App Router, server components, font optimisation. |
| `react` (19.2.3) | UI library. |
| `framer-motion` (11.15+) | Every animation in the app -- entrances, exits, hover states, springs, presence. |
| `lucide-react` (0.544+) | All icons -- Moon, Heart, Sparkles, Mail, Lock, Send, Coffee, PartyPopper, etc. |
| `tailwindcss` (3.4+) | All styling. No separate CSS files per component. |
| `tailwindcss-animate` | Extra animation utilities for Tailwind. |

Everything else in `package.json` (Radix UI primitives, Recharts, etc.) comes from the shadcn/ui base template and isn't actively used by Kindred's custom components.

---

## How Everything Connects

Here's the flow, start to finish:

```
User opens the app
       |
  layout.tsx loads fonts + sets metadata
       |
  page.tsx renders (isLoggedIn = false)
       |
  <Login /> appears with fade-in
       |
  User clicks "Enter Kindred"
       |
  onEnter() fires -> isLoggedIn = true
       |
  AnimatePresence crossfades to dashboard
       |
  Dashboard renders top-to-bottom:
    1. <DashboardHeader />  -- sticky, rotating messages
    2. <MoonButton />       -- tap for encouragement
    3. <TimeCapsule />      -- open sealed letters
    4. <Creator />          -- write kind notes
    5. <MoodCheckin />      -- pick your mood
    6. <GratitudeWall />    -- read anonymous kindness
```

There's no routing. No navigation. No back button. It's intentionally simple -- one scroll, one flow, one experience. You land, you enter, and you're held.

---

*Built with care for every student who just needs to know they're not alone.*
