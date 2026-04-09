---
name: build-page
description: "Build a stunning, production-ready landing page from a single topic description. Outputs a single HTML file with animated effects (aurora streaks, particles, glassmorphism), dark theme, responsive layout, and bento grid sections. Use when asked to build a website, landing page, or homepage. No project context needed."
---

# Build Page

Generate a visually impressive, single-file landing page from just a topic description. Zero dependencies. One HTML file. Maximum visual impact.

---

## Quick Start

```
/build-page "AI-powered fitness coaching app"
/build-page "crypto portfolio tracker for beginners"
/build-page "freelance design studio"
```

---

## Arguments

The skill takes a single argument: **what the website is about**.

This can be:
- A product or service description: `"AI tutoring platform for high school students"`
- A business name + what they do: `"NightOwl Labs - developer tools for indie hackers"`
- A bold headline to use: `"We replaced our entire marketing team with one AI agent"`
- A vague idea: `"coffee subscription box"` (Claude will flesh it out)

If no argument is provided, ask the user: "What is this website about?"

---

## What Gets Built

A single `index.html` file with everything inline (CSS + JS). No frameworks, no build tools, no npm. Just open it in a browser.

### Required Visual Elements

Every page MUST include all of these. This is what makes it look premium:

1. **Animated aurora/light streaks** - Canvas-drawn rainbow light trails flowing across the page. 3-5 overlapping sine-wave streaks with rainbow color interpolation and glow layers. See `references/template.html` for the exact implementation.

2. **Floating particles** - 40-60 small white dots drifting upward with pulsing opacity. Adds depth and life to the dark background.

3. **Film grain overlay** - Subtle SVG noise texture at 3% opacity over the entire page. One line of CSS.

4. **Glassmorphism nav** - Fixed top nav with `backdrop-filter: blur(20px)`, semi-transparent background, subtle bottom border.

5. **Massive hero typography** - `clamp(48px, 8vw, 120px)` font-size, weight 900, tight letter-spacing (-3px), gradient text (white to 50% white). The headline should hit hard.

6. **Staggered fade-up animations** - Each section element fades up with increasing delay (0.2s increments). CSS-only, no JS needed.

7. **Bento grid section** - CSS grid with mixed `span 2` and `span 1` cards. Dark glass cards with hover lift effect. Use for stats, features, or key points.

8. **Gradient accent metrics** - Large numbers (48px+, weight 900) with `background: linear-gradient(135deg, #a78bfa, #60a5fa)` and `background-clip: text`.

### Required Sections (in order)

1. **Nav** - Logo/brand name (with glowing dot), 3-4 text links, CTA button
2. **Hero** - Badge pill, massive headline, subtitle (1-2 sentences), two buttons (primary solid white, secondary ghost)
3. **Features** - 3-column grid of feature cards with colored icon boxes, title, description
4. **Bento showcase** - Mixed-size grid with stats, testimonials, or key selling points
5. **CTA** - Final call to action with large gradient text headline and primary button
6. **Footer** - Single line, subtle

---

## Step-by-Step Process

### Step 1: Parse the Topic

From the user's argument, determine:
- **Brand/product name** (invent one if not provided)
- **Headline** (bold, provocative, short - 6-10 words max)
- **Subtitle** (one sentence explaining the value)
- **3 features** with titles and one-line descriptions
- **3 metrics/stats** (can be approximate or aspirational - e.g., "10x faster", "50K+ users", "$0 setup")
- **CTA text** (what should the button say?)
- **Nav links** (3-4 relevant section names)

### Step 2: Read the Reference Template

Read `~/.claude/skills/build-page/references/template.html` for the exact CSS patterns, canvas animation code, and HTML structure. This is the proven blueprint. Follow it closely.

### Step 3: Build the Page

Write the complete HTML file. Key implementation details:

**CSS:**
- Dark background: `#000` or `#0a0a0f`
- Text: `#fff` primary, `rgba(255,255,255,0.4)` secondary
- Accent: `#a78bfa` (purple) as primary accent, `#60a5fa` (blue) and `#f472b6` (pink) as secondary
- Glass cards: `rgba(255,255,255,0.03)` bg, `rgba(255,255,255,0.06)` border, `border-radius: 20px`
- Font: Inter from Google Fonts, weights 400-900
- All spacing on 8px grid
- Mobile breakpoint at 768px, tablet at 1024px
- `prefers-reduced-motion` media query disabling all animations

**Canvas (aurora streaks):**
- Full-viewport fixed canvas behind content
- `LightStreak` class with sine-wave path, rainbow color interpolation, glow layer
- `Particle` class with upward drift and pulsing opacity
- `requestAnimationFrame` loop
- Resize handler updating canvas dimensions and streak positions

**Animations:**
- `fadeUp` keyframe: translateY(24px) + opacity 0 to translateY(0) + opacity 1
- Stagger via `animation-delay` on nth-child or manual classes
- `pulse` keyframe for badge indicator
- Hover transforms: `translateY(-2px)` for cards, `translateY(-4px)` for feature cards
- Transition timing: 150-300ms, ease or ease-out

### Step 4: Customize Colors (Optional)

If the topic suggests a specific color scheme, adjust the accent colors:
- Tech/AI/SaaS: Purple (#a78bfa) + Blue (#60a5fa) [default]
- Finance/Crypto: Green (#34d399) + Blue (#60a5fa)
- Health/Fitness: Green (#34d399) + Teal (#2dd4bf)
- Creative/Design: Pink (#f472b6) + Purple (#a78bfa)
- Food/Lifestyle: Orange (#fb923c) + Yellow (#fbbf24)
- Education: Blue (#60a5fa) + Indigo (#818cf8)

Update the aurora streak colors to match. Replace the rainbow array with 4-5 colors from the chosen palette.

### Step 5: Save and Open

Save to `./landing-page/index.html` in the current working directory (create the directory if needed).

Then run: `open ./landing-page/index.html` to preview in browser.

### Step 6: Report

Tell the user:
- Where the file was saved
- The headline and brand name used
- That they can open it directly in any browser
- Suggest 2-3 tweaks they might want (swap headline, add real stats, change CTA link)

---

## Content Rules

- Headlines should be bold and provocative, not corporate. "We made accountants obsolete" > "Streamlining financial workflows"
- Subtitles are one sentence max. Clear and specific.
- Feature descriptions are 1-2 sentences. No filler.
- Stats can be aspirational but should feel believable.
- No lorem ipsum anywhere. Every word should be real copy.
- No emoji in the page content. SVG icons only.

---

## Technical Rules

- Single HTML file. All CSS in `<style>`, all JS in `<script>`. No external files except Google Fonts.
- No frameworks. No React, no Tailwind classes, no npm packages.
- Semantic HTML: `<nav>`, `<section>`, `<footer>`, `<h1>`-`<h3>`
- Accessible: alt text on images, aria-labels on icon-only elements, visible focus states, `prefers-reduced-motion` support
- Mobile-first responsive. Columns collapse to single column on mobile. Nav links hide on mobile.
- Performance: canvas animation uses `requestAnimationFrame`, no setInterval. Resize handler debounced by browser.

---

## If the Magic MCP is Available

If the `21st_magic_component_inspiration` tool is available, use it to search for additional component ideas:
- Search for `"hero dark animated"` for hero section inspiration
- Search for `"aurora light animation"` for background effect ideas
- Search for `"bento grid cards"` for layout patterns

Incorporate any useful patterns into the build while keeping the single-file HTML constraint.

---

## If the ui-ux-pro-max Skill is Available

Reference it for:
- Typography scale and font pairing decisions
- Color palette selection based on product type
- Accessibility checks (contrast ratios, touch targets)
- Animation timing (150-300ms for micro-interactions)

The build-page skill handles the actual construction. ui-ux-pro-max provides the design intelligence.
