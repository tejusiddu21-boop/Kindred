# Kindred

**An emotional wellness & connection app built for every student, everywhere.**

College is hard. Between deadlines, exams, loneliness, and the constant pressure to "figure it out," students rarely get a moment to breathe, let alone feel seen. Kindred was built to change that. It's a quiet corner of the internet where you can check in with yourself, receive a kind word from a stranger, and be reminded that you're not alone in any of this.

---

## What Kindred Does

### The Moon Button
A glowing, breathing orb at the heart of the dashboard. Tap it when you need a boost, and it gives you a random encouragement. Simple. No sign-ups, no algorithms, no performance metrics. Just a kind thought when you need one.

### Time-Capsule Locker
Three sealed messages waiting to be opened. When you tap "Open Message," a progress bar simulates *syncing emotions* before the message reveals itself letter by letter in a typewriter animation. Each one feels like opening a note someone tucked into your backpack.

### Write to a Peer (or Yourself)
A space to write anonymous notes of kindness. Pick a vibe: **Support**, **Celebration**, or **Just Because**. Hit "Send Love" and it goes out into the world. No names, no expectations, just good energy.

### Mood Check-in
Five moods. Tap the one that feels right. You'll get a short, honest validation message. No toxic positivity, no "just be happy" nonsense. If you're tired, it says rest. If you're sad, it sits with you.

### Gratitude Wall
A masonry wall of anonymous notes from the community. Real, grounded, human messages like *"Thank you to the friend who just sat with me in silence when I didn't want to talk."* The kind of stuff that makes you stop scrolling for a second.

---

## The Vibe

Kindred looks like a late-night sky. Deep midnight blue backgrounds, soft lavender glows, neon mint accents, and glassmorphism cards that feel like they're floating. Subtle star particles drift behind everything. It's calm, it's intentional, and it's designed to feel like a breath of fresh air at 2 AM.

**Typography:** Space Grotesk for headings (bold, modern, a little bit futuristic), Inter for body text (clean, easy on the eyes).

**Animations:** Smooth Framer Motion transitions everywhere. The login fades in. The moon button pulses. Messages type themselves out. Cards float up into view. Nothing aggressive, everything gentle.

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Framework | [Next.js 16](https://nextjs.org/) (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS + custom design tokens |
| Animations | Framer Motion |
| Icons | Lucide React |
| UI Base | shadcn/ui |
| Fonts | Space Grotesk, Inter (via `next/font/google`) |

---

## Getting Started

```bash
# Clone the repo
git clone https://github.com/your-username/kindred.git
cd kindred

# Install dependencies
pnpm install

# Run the dev server
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) and you're in.

---

## Project Structure

```
app/
  layout.tsx          # Root layout with fonts, metadata, and theme
  page.tsx            # Main page: login state + dashboard orchestration
  globals.css         # Design tokens, glassmorphism, animations, stars

components/kindred/
  login.tsx           # Glassmorphism login card
  dashboard-header.tsx # Sticky header with rotating support messages
  moon-button.tsx     # The glowing encouragement orb
  time-capsule.tsx    # Sealed messages with typewriter reveal
  creator.tsx         # Anonymous peer note writer with vibe selector
  mood-checkin.tsx    # Emoji mood picker with validation messages
  gratitude-wall.tsx  # Masonry grid of anonymous kindness
```

---

## A Note on Purpose

Kindred is not a therapy app. It's not a replacement for professional help. It's a small, warm thing that says: *"Hey, I see you. You're doing okay."*

If you're a student and you're struggling, please reach out to your campus counseling center or a trusted person in your life. You deserve support, and there is absolutely no shame in asking for it.

---

## Contributing

If you want to make Kindred better, you're welcome here. Whether it's adding new encouragement messages, improving accessibility, translating content for international students, or just fixing a typo, every contribution matters.

1. Fork the repo
2. Create your branch (`git checkout -b feature/your-idea`)
3. Commit your changes (`git commit -m 'Added something kind'`)
4. Push to the branch (`git push origin feature/your-idea`)
5. Open a Pull Request

---

## License

MIT. Use it, remix it, share it. Just keep it kind.

---

*Built with care for every student who ever needed to hear that they matter.*

