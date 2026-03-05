

```markdown
---
name: tasteful-skill
description: Unified design engineering skill. Combines premium UI/UX standards, full-output enforcement, and existing-project redesign into one bulletproof system. Covers typography, color, layout, motion, content, architecture, performance, and creative direction. Works with any CSS framework or vanilla CSS.
---

# Tasteful Skill

## 1. Output Protocol

### Baseline Rule
Treat every task as production-critical. A partial output is a broken output. Optimize for completeness, never brevity. If the user asks for a full file, deliver the full file. If the user asks for 5 components, deliver 5 components.

### Banned Output Patterns
The following patterns are hard failures. Never produce them:

**In code blocks:**
`// ...`, `// rest of code`, `// implement here`, `// TODO`, `/* ... */`, `// similar to above`, `// continue pattern`, `// add more as needed`, bare `...` standing in for omitted code.

**In prose:**
"Let me know if you want me to continue", "I can provide more details if needed", "for brevity", "the rest follows the same pattern", "similarly for the remaining", "and so on" (when replacing actual content), "I'll leave that as an exercise".

**Structural shortcuts:**
Outputting a skeleton when the request was for a full implementation. Showing the first and last section while skipping the middle. Replacing repeated logic with one example and a description. Describing what code should do instead of writing it.

### Execution Process
1. **Scope** — Read the full request. Count how many distinct deliverables are expected (files, functions, sections, answers). Lock that number.
2. **Build** — Generate every deliverable completely. No partial drafts, no "you can extend this later."
3. **Cross-check** — Before output, re-read the original request. Compare your deliverable count against the scope count. If anything is missing, add it before responding.

### Handling Long Outputs
When a response approaches the token limit:
- Do not compress remaining sections to squeeze them in.
- Do not skip ahead to a conclusion.
- Write at full quality up to a clean breakpoint (end of a function, end of a file, end of a section).
- End with:
```
[PAUSED — X of Y complete. Send "continue" to resume from: next section name]
```
On "continue", pick up exactly where you stopped. No recap, no repetition.

### Quick Check
Before finalizing any response, verify:
- No banned patterns from the list above appear anywhere in the output.
- Every item the user requested is present and finished.
- Code blocks contain actual runnable code, not descriptions of what code would do.
- Nothing was shortened to save space.


## 2. Design Configuration

### Active Baseline
```
DESIGN_VARIANCE:  8   (1=Perfect Symmetry, 10=Artsy Chaos)
MOTION_INTENSITY: 6   (1=Static/No movement, 10=Cinematic/Magic Physics)
VISUAL_DENSITY:   4   (1=Art Gallery/Airy, 10=Pilot Cockpit/Packed Data)
```

These are the default values for all generations. Never ask the user to edit this file. Always listen to the user: adapt these values dynamically based on what they explicitly request in their chat prompts. Use these baseline (or user-overridden) values as global variables to drive the specific logic in Sections 5 through 9.

### Dial Definitions

**DESIGN_VARIANCE (Level 1–10):**
- **1–3 (Predictable):** Flexbox `justify-center`, strict 12-column symmetrical grids, equal paddings.
- **4–7 (Offset):** Use `margin-top: -2rem` overlapping, varied image aspect ratios (e.g., 4:3 next to 16:9), left-aligned headers over center-aligned data.
- **8–10 (Asymmetric):** Masonry layouts, CSS Grid with fractional units (e.g., `grid-template-columns: 2fr 1fr 1fr`), massive empty zones (`padding-left: 20vw`).
- **MOBILE OVERRIDE:** For levels 4–10, any asymmetric layout above `md:` MUST aggressively fall back to a strict, single-column layout (`w-full`, `px-4`, `py-8`) on viewports `< 768px` to prevent horizontal scrolling and layout breakage.

**MOTION_INTENSITY (Level 1–10):**
- **1–3 (Static):** No automatic animations. CSS `:hover` and `:active` states only.
- **4–7 (Fluid CSS):** Use `transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1)`. Use `animation-delay` cascades for load-ins. Focus strictly on `transform` and `opacity`. Use `will-change: transform` sparingly.
- **8–10 (Advanced Choreography):** Complex scroll-triggered reveals or parallax. Use Framer Motion hooks. NEVER use `window.addEventListener('scroll')`.

**VISUAL_DENSITY (Level 1–10):**
- **1–3 (Art Gallery Mode):** Lots of white space. Huge section gaps. Everything feels expensive and clean.
- **4–7 (Daily App Mode):** Normal spacing for standard web apps.
- **8–10 (Cockpit Mode):** Tiny paddings. No card boxes; just 1px lines to separate data. Everything is packed. **Mandatory:** Use monospace (`font-mono`) for all numbers.


## 3. Stack & Architecture

### Framework Defaults
Unless the user explicitly specifies a different stack, adhere to these structural constraints:

- **Framework:** React or Next.js. Default to Server Components (RSC).
- **RSC Safety:** Global state works ONLY in Client Components. In Next.js, wrap providers in a `"use client"` component.
- **Interactivity Isolation:** If motion or interactive behavior is required, the specific interactive UI component MUST be extracted as an isolated leaf component with `'use client'` at the very top. Server Components must exclusively render static layouts.
- **State Management:** Use local `useState`/`useReducer` for isolated UI. Use global state strictly for deep prop-drilling avoidance.

### Dependency Verification [MANDATORY]
Before importing ANY third-party library (e.g., `framer-motion`, `lucide-react`, `zustand`), you MUST check `package.json`. If the package is missing, you MUST output the installation command (e.g., `npm install package-name`) before providing the code. Never assume a library exists. Never hallucinate imports that do not exist in the project's dependency file.

### Styling Policy
- Use Tailwind CSS (v3/v4) for 90% of styling.
- **Tailwind Version Lock:** Check `package.json` first. Do not use v4 syntax in v3 projects.
- **T4 Config Guard:** For v4, do NOT use `tailwindcss` plugin in `postcss.config.js`. Use `@tailwindcss/postcss` or the Vite plugin.
- If the project uses a different styling system (styled-components, vanilla CSS, CSS Modules), work with it. Do not migrate.
- If the project has no framework, use vanilla CSS.
- Move all inline styles to the project's styling system. Do not mix inline styles with CSS classes.

### Responsiveness Fundamentals
- Standardize breakpoints (`sm`, `md`, `lg`, `xl`).
- Contain page layouts using `max-w-[1400px] mx-auto` or `max-w-7xl`. Content must not stretch edge-to-edge on wide screens.
- **Viewport Stability [CRITICAL]:** NEVER use `h-screen` for full-height sections. ALWAYS use `min-h-[100dvh]` to prevent layout jumping on mobile browsers (iOS Safari viewport bug).
- **Grid over Flex-Math:** NEVER use complex flexbox percentage math (`w-[calc(33%-1rem)]`). ALWAYS use CSS Grid (`grid grid-cols-1 md:grid-cols-3 gap-6`) for reliable multi-column structures.
- Use relative units (`%`, `rem`, `em`, `max-width`) for flexible layouts. No hardcoded pixel widths for layout containers.

### Anti-Emoji Policy [CRITICAL]
NEVER use emojis in code, markup, text content, or alt text. Replace symbols with high-quality icons (Phosphor, Radix, Heroicons) or clean SVG primitives. Emojis are BANNED.


## 4. Redesign Workflow

When applied to an existing project, follow this sequence:

### Step 1: Scan
Read the codebase. Identify the framework, styling method (Tailwind, vanilla CSS, styled-components, etc.), component library, Tailwind version, and current design patterns.

### Step 2: Diagnose
Run through every audit rule in Sections 5–13. List every generic pattern, weak point, and missing state found.

### Step 3: Fix
Apply targeted upgrades working with the existing stack. Do not rewrite from scratch. Improve what's there.

### Fix Priority Order
Apply changes in this order for maximum visual impact with minimum risk:
1. **Font swap** — biggest instant improvement, lowest risk.
2. **Color palette cleanup** — remove clashing or oversaturated colors.
3. **Hover and active states** — makes the interface feel alive.
4. **Layout and spacing** — proper grid, max-width, consistent padding.
5. **Replace generic components** — swap cliché patterns for modern alternatives.
6. **Add loading, empty, and error states** — makes it feel finished.
7. **Polish typography scale and spacing** — the premium final touch.

### Redesign Rules
- Work with the existing tech stack. Do not migrate frameworks or styling libraries.
- Do not break existing functionality. Test after every change.
- Before importing any new library, check the project's dependency file first.
- If the project uses Tailwind, check the version (v3 vs v4) before modifying config.
- If the project has no framework, use vanilla CSS.
- Keep changes reviewable and focused. Small, targeted improvements over big rewrites.


## 5. Typography System

### Font Selection
- **Browser default fonts and Inter are BANNED.** Replace with a font that has character. Approved options: `Geist`, `Outfit`, `Cabinet Grotesk`, `Satoshi`.
- **Serif fonts are BANNED for dashboard/software UIs.** For these contexts, use exclusively high-end sans-serif pairings (`Geist` + `Geist Mono`, or `Satoshi` + `JetBrains Mono`).
- For editorial or creative projects, pair a serif header with a sans-serif body.

### Headlines & Display Text
- Default to `text-4xl md:text-6xl tracking-tighter leading-none`.
- Headlines should feel heavy and intentional. Increase size for display text, tighten letter-spacing, reduce line-height.
- Use negative letter-spacing (tracking) for large headers.
- Control hierarchy with weight and color, not just massive scale. Do not let the first heading scream.
- Do not use text-fill gradients on large headers excessively.

### Body Text
- Default to `text-base text-gray-600 leading-relaxed max-w-[65ch]`.
- Limit paragraph width to roughly 65 characters. Increase line-height for readability.

### Weight Hierarchy
- Do not use only Regular (400) and Bold (700). Introduce Medium (500) and SemiBold (600) for more subtle hierarchy.

### Numeric Typography
- Use a monospace font or enable tabular figures (`font-variant-numeric: tabular-nums`) for data-heavy interfaces.
- When `VISUAL_DENSITY > 7`, use monospace (`font-mono`) for all numbers.

### Letter-Spacing
- Use negative tracking for large headers.
- Use positive tracking for small caps, labels, and overlines.
- Use subtle tracking (`tracking-tight`) for section headers.

### Casing
- All-caps subheaders everywhere is generic. Try lowercase italics, sentence case, or small-caps instead.
- Use sentence case for headings, not Title Case On Every Header.

### Orphan Control
- Fix single words sitting alone on the last line with `text-wrap: balance` or `text-wrap: pretty`.


## 6. Color & Surface System

### Background
- **Pure `#000000` is BANNED.** Replace with off-black, dark charcoal, or tinted dark (`#0a0a0a`, `#121212`, or a dark navy like zinc-950).
- No random dark sections in a light-mode page (or vice versa). A single dark-background section breaking an otherwise light page looks like a copy-paste accident. Either commit to full dark mode or keep a consistent background tone throughout. If contrast is needed, use a slightly darker shade of the same palette — not a sudden jump to `#111` in the middle of a cream page.

### Accent Colors
- **Maximum one accent color.** Remove the rest. Consistency beats variety.
- **Saturation must stay below 80%.** Desaturate accents so they blend with neutrals instead of screaming.
- **The AI purple/blue gradient aesthetic is BANNED.** No purple button glows, no neon gradients. Use absolute neutral bases (Zinc/Slate) with high-contrast, singular accents (e.g., Emerald, Electric Blue, or Deep Rose).

### Gray System
- Stick to one gray family. Tint all grays with a consistent hue (warm or cool, not both). Do not fluctuate between warm and cool grays within the same project.

### Shadows
- Do not use generic `box-shadow`. Tint shadows to match the background hue. Use colored shadows (e.g., dark blue shadow on a blue background) instead of pure black at low opacity.
- Audit all shadows to ensure they suggest a single, consistent light source (consistent lighting direction).
- Do not use default `box-shadow` glows or auto-glows. Use inner borders or subtle tinted shadows.

### Texture & Depth
- Flat design with zero texture feels sterile. Add subtle noise, grain, or micro-patterns to backgrounds.
- Break perfectly even gradients with radial gradients, noise overlays, or mesh gradients instead of standard linear 45-degree fades.
- Empty, flat sections with no visual depth feel unfinished. Add high-quality background imagery (blurred, overlaid, or masked), subtle patterns, or ambient gradients. Use reliable placeholder sources like `https://picsum.photos/seed/{name}/1920/1080` when real assets are not available.

### Glassmorphism (When Used)
Go beyond `backdrop-filter: blur`. Add a 1px inner border (`border-white/10`) and a subtle inner shadow (`shadow-[inset_0_1px_0_rgba(255,255,255,0.1)]`) to simulate physical edge refraction.


## 7. Layout & Spacing System

### Symmetry & Alignment
- **Centered hero sections are BANNED when `DESIGN_VARIANCE > 4`.** Force split-screen (50/50), left-aligned content with right-aligned asset, or asymmetric white-space structures.
- Break symmetry with offset margins, mixed aspect ratios, or left-aligned headers over centered content.

### Grid Structure
- **Three equal card columns as a feature row is BANNED.** This is the most generic AI layout. Replace with a 2-column zig-zag, asymmetric grid, horizontal scroll, or masonry layout.
- Use CSS Grid for multi-column structures. Use fractional units for asymmetry (e.g., `grid-template-columns: 2fr 1fr 1fr`).
- Allow variable card heights or use masonry when content varies in length.

### Container
- Add a container constraint (1200–1440px or `max-w-7xl`) with auto margins so content does not stretch edge-to-edge on wide screens.

### Spacing
- Double the spacing. Let the design breathe. Dense layouts work for data dashboards, not for marketing pages.
- Asymmetrical vertical padding is more natural. Top and bottom padding should not always be identical — bottom padding often needs to be slightly larger for optical balance.
- Use generous `p-8` or `p-10` padding inside major containers.

### Border Radius
- Vary the radius: tighter on inner elements, softer on containers. Do not use uniform border-radius on everything.

### Depth & Overlap
- Elements should not all sit flat next to each other. Use negative margins to create layering and visual depth.

### Vertical Alignment Across Siblings
- Buttons must be bottom-aligned in card groups. When cards have different content lengths, CTAs end up at random heights. Pin buttons to the bottom of each card so they form a clean horizontal line.
- Feature lists in pricing tables or comparison cards must start at the same Y position across all columns. Use consistent spacing above the list or fixed-height title/price blocks.
- When placing cards, columns, or panels next to each other, align shared elements (titles, descriptions, prices, buttons) across all items. Misaligned baselines make the layout look broken.

### Optical Corrections
- Centering by the math does not always look centered to the eye. Icons next to text, play buttons in circles, or text in buttons often need 1–2px optical adjustments to feel right.

### Dashboard Layout
- A dashboard does not always need a left sidebar. Try top navigation, a floating command menu, or a collapsible panel.
- **Dashboard Hardening:** When `VISUAL_DENSITY > 7`, generic card containers are BANNED. Use logic-grouping via `border-t`, `divide-y`, or purely negative space. Data metrics should breathe without being boxed in unless elevation is functionally required.


## 8. Interactivity & Motion System

### Hover States [MANDATORY]
- Every interactive element must have a hover state. Add background shift, slight scale, or translate on hover.

### Active/Pressed Feedback [MANDATORY]
- Add a subtle `scale(0.98)` or `translateY(1px)` on `:active` to simulate a physical click.

### Transitions [MANDATORY]
- Add smooth transitions (200–300ms) to all interactive elements. Never use instant transitions with zero duration.
- Default curve: `cubic-bezier(0.16, 1, 0.3, 1)`.

### Focus States [MANDATORY]
- Ensure visible focus indicators for keyboard navigation. This is an accessibility requirement, not optional.

### Scroll Behavior
- Anchor clicks must not jump instantly. Add `scroll-behavior: smooth`.

### Loading States [MANDATORY]
- Replace generic circular spinners with skeleton loaders that match the layout shape.
- Use shimmer effect (shifting light reflection moving across placeholder boxes).

### Empty States [MANDATORY]
- An empty dashboard showing nothing is a missed opportunity. Design a composed "getting started" view with clear guidance on how to populate data.

### Error States [MANDATORY]
- Add clear, inline error messages for forms. Do not use `window.alert()`.
- Be direct: "Connection failed. Please try again." — not "Oops! Something went wrong!"

### Current Page Indication [MANDATORY]
- Style the active nav link differently so users know where they are.

### Dead Links
- Buttons linking to `#` must either link to real destinations or be visually disabled.

### Motion by Intensity Level

**When `MOTION_INTENSITY > 3`:**
- Use `animation-delay` cascades for load-ins.
- Focus strictly on `transform` and `opacity` for animation. Never animate `top`, `left`, `width`, or `height`.
- Use `will-change: transform` sparingly.

**When `MOTION_INTENSITY > 5`:**
- Apply premium spring physics (`type: "spring", stiffness: 100, damping: 20`) to all interactive elements. No linear easing.
- Embed continuous, infinite micro-animations (pulse, typewriter, float, shimmer, carousel) in standard components.
- Implement staggered entry: elements cascade in with slight delays, combining Y-axis translation with opacity fade. Never mount everything at once. Use `staggerChildren` (Framer) or CSS cascade (`animation-delay: calc(var(--index) * 100ms)`).
- **CRITICAL:** For `staggerChildren`, the parent (with `variants`) and children MUST reside in the identical Client Component tree. If data is fetched asynchronously, pass data as props into a centralized parent motion wrapper.
- Heavily utilize Framer Motion's `layout` and `layoutId` props for smooth re-ordering, resizing, and shared element transitions.

**When `MOTION_INTENSITY > 7`:**
- Complex scroll-triggered reveals or parallax. Use Framer Motion hooks. NEVER use `window.addEventListener('scroll')`.
- Scroll-driven reveals: content entering through expanding masks, wipes, or draw-on SVG paths tied to scroll progress.
- When appropriate, leverage GSAP (ScrollTrigger/Parallax) for complex scrolltelling or Three.js/WebGL for 3D/Canvas animations.
- **CRITICAL:** Never mix GSAP/Three.js with Framer Motion in the same component tree. Default to Framer Motion for UI/Bento interactions. Use GSAP/Three.js EXCLUSIVELY for isolated full-page scrolltelling or canvas backgrounds, wrapped in strict `useEffect` cleanup blocks.

### Magnetic Micro-Physics (When `MOTION_INTENSITY > 5`)
Buttons that pull slightly toward the mouse cursor. **CRITICAL:** NEVER use React `useState` for magnetic hover or continuous animations. Use EXCLUSIVELY Framer Motion's `useMotionValue` and `useTransform` outside the React render cycle to prevent performance collapse on mobile.

### Performance-Critical Animation Rules
- Any perpetual motion or infinite loop MUST be memoized (`React.memo`) and completely isolated in its own microscopic Client Component. Never trigger re-renders in the parent layout.
- Wrap dynamic lists in `<AnimatePresence>` and optimize for 60fps.
- Apply grain/noise filters exclusively to fixed, `pointer-events-none` pseudo-elements (e.g., `fixed inset-0 z-50 pointer-events-none`) and NEVER to scrolling containers to prevent continuous GPU repaints.
- `useEffect` animations MUST contain strict cleanup functions.


## 9. Component Architecture

### Cards
- The generic card look (border + shadow + white background simultaneously) is overused. Remove the border, or use only background color, or use only spacing. Cards should exist only when elevation communicates hierarchy.
- When cards are used, apply tinted shadows that carry the hue of the background.
- When `VISUAL_DENSITY > 7`, cards are BANNED entirely. Use `border-t`, `divide-y`, or negative space.

### Buttons
- Do not always default to one filled button + one ghost button. Add text links or tertiary styles to reduce visual noise.

### Badges
- Pill-shaped "New" and "Beta" badges are generic. Try square badges, flags, or plain text labels.

### FAQ Sections
- Accordion FAQ sections are overused. Use a side-by-side list, searchable help, or inline progressive disclosure.

### Testimonials
- Three-card carousel with dots is generic. Replace with a masonry wall, embedded social posts, or a single rotating quote.

### Pricing Tables
- Three towers side-by-side is generic. Highlight the recommended tier with color and emphasis, not just extra height. Ensure feature lists start at the same Y position across columns.

### Modals
- Modals for everything is excessive. Use inline editing, slide-over panels, or expandable sections instead of popups for simple actions.

### Avatars
- Avatar circles exclusively are generic. Try squircles or rounded squares.
- Do NOT use standard SVG "egg" or Lucide user icons for avatars. Use creative, believable photo placeholders or specific styling.

### Theme Toggle
- Light/dark toggle does not always need a sun/moon switch. Use a dropdown, system preference detection, or integrate it into settings.

### Footer
- Footer link farm with 4 columns is bloated. Simplify. Focus on main navigational paths and legally required links.

### Forms
- Label MUST sit above input. Helper text is optional but should exist in markup. Error text below input. Use a standard `gap-2` for input blocks.
- Add client-side validation for emails, required fields, and format checks.

### shadcn/ui Policy
- You may use `shadcn/ui`, but NEVER in its generic default state. You MUST customize the radii, colors, and shadows to match the high-end project aesthetic.


## 10. Content & Data Standards

### Names
- **"John Doe", "Jane Smith", "Sarah Chan", "Jack Su" are BANNED.** Use diverse, highly creative, realistic-sounding names.

### Numbers
- **Fake round numbers like `99.99%`, `50%`, `$100.00` are BANNED.** Use organic, messy data: `47.2%`, `$99.00`, `+1 (312) 847-1928`.

### Brand Names
- **"Acme Corp", "Nexus", "SmartFlow" are BANNED.** Invent premium, contextual, believable brand names.

### Copywriting
- **AI cliché words are BANNED:** "Elevate", "Seamless", "Unleash", "Next-Gen", "Game-changer", "Delve", "Tapestry", "In the world of...", "Revolutionize", "Cutting-edge". Write plain, specific, concrete language.
- Use active voice: "We couldn't save your changes" — not "Your changes could not be saved."
- Remove exclamation marks from success messages. Be confident, not loud.
- "Oops!" in error messages is BANNED. Be direct.

### Placeholder Content
- **Lorem Ipsum is BANNED.** Write real draft copy.
- Use unique assets for every distinct person. Do not use the same avatar image for multiple users.
- Randomize blog post dates to appear real. Do not make all dates identical.

### Casing
- Use sentence case for headings, not Title Case.


## 11. Iconography & Assets

### Icon Libraries
- **Lucide and Feather icons exclusively are too generic.** Use Phosphor (`@phosphor-icons/react`), Radix (`@radix-ui/react-icons`), or Heroicons for differentiation. Check the installed version before importing.
- Standardize `strokeWidth` globally (e.g., exclusively use `1.5` or `2.0`). Audit all icons and enforce one consistent stroke weight.

### Icon Metaphors
- Rocketship for "Launch" and shield for "Security" are clichés. Replace with less obvious icons (bolt, fingerprint, spark, vault).

### Favicon
- Always include a branded favicon. Missing favicon is unacceptable.

### Photography
- **Stock "diverse team" photos are BANNED.** Use real team photos, candid shots, or a consistent illustration style.
- **Unsplash direct links are BANNED** (they break). Use `https://picsum.photos/seed/{random_string}/800/600` or SVG UI Avatars.


## 12. Code Quality & Performance

### Semantic HTML
- No div soup. Use `<nav>`, `<main>`, `<article>`, `<aside>`, `<section>`, `<header>`, `<footer>`.

### Meta Tags
- Add proper `<title>`, `description`, `og:image`, and social sharing meta tags.

### Alt Text
- Describe image content for screen readers. Never leave `alt=""` or `alt="image"` on meaningful images.

### Z-Index
- NEVER spam arbitrary `z-50` or `z-[9999]` unprompted. Establish a clean z-index scale in the theme/variables. Use z-indexes strictly for systemic layer contexts (sticky navbars, modals, overlays).

### Dead Code
- Remove all commented-out code and debug artifacts before shipping.

### Hardware Acceleration
- Never animate `top`, `left`, `width`, or `height`. Animate exclusively via `transform` and `opacity`.

### Grain/Noise Performance
- Apply grain/noise filters exclusively to fixed, `pointer-events-none` pseudo-elements and NEVER to scrolling containers.

### Skip-to-Content Link
- Essential for keyboard users. Add a hidden skip-link that becomes visible on focus.


## 13. Strategic Completeness

These are items AI typically forgets. Every project must include them:

- **Legal links.** Add privacy policy and terms of service links in the footer.
- **Back navigation.** No dead ends in user flows. Every page needs a way back.
- **Custom 404 page.** Design a helpful, branded "page not found" experience.
- **Form validation.** Add client-side validation for emails, required fields, and format checks.
- **Cookie consent.** If required by jurisdiction, add a compliant consent banner.
- **Loading states.** Skeleton loaders matching layout shape, not generic spinners.
- **Empty states.** Composed "getting started" views indicating how to populate data.
- **Error states.** Clear, inline error reporting. No `window.alert()`.
- **Active navigation state.** Current page visually indicated in the nav.
- **Scroll-behavior: smooth.** Applied globally.
- **Focus indicators.** Visible focus rings on all interactive elements.
- **Favicon.** Always present.
- **Meta tags.** Title, description, og:image, social sharing.


## 14. Forbidden Patterns (AI Tells)

This is the master ban list. These patterns are hard failures that mark output as generic AI work:

### Visual & CSS Bans
| Pattern | Replacement |
|---|---|
| Pure `#000000` background | Off-black, zinc-950, charcoal, or hue-tinted dark |
| Neon/outer glow `box-shadow` | Inner borders or subtle tinted shadows |
| Oversaturated accents (>80%) | Desaturated accents that blend with neutrals |
| Purple/blue "AI gradient" aesthetic | Neutral bases with a single considered accent |
| Excessive gradient text on large headers | Solid color or subtle shift |
| Custom mouse cursors | Standard cursor (performance and accessibility) |
| `h-screen` for full-height sections | `min-h-[100dvh]` |
| Mixing warm and cool grays | One gray family, consistently tinted |
| Random dark section in a light page | Consistent palette throughout |

### Typography Bans
| Pattern | Replacement |
|---|---|
| Inter font | Geist, Outfit, Cabinet Grotesk, or Satoshi |
| Serif font on dashboards | High-end sans-serif exclusively |
| Only 400 and 700 font weights | Include 500 and 600 for hierarchy |
| All-caps subheaders everywhere | Sentence case, small-caps, or lowercase italic |
| Title Case On Every Header | Sentence case |

### Layout Bans
| Pattern | Replacement |
|---|---|
| Three equal card columns | 2-col zig-zag, asymmetric grid, horizontal scroll, masonry |
| Everything centered (when variance >4) | Split screen, left-aligned, asymmetric whitespace |
| Complex flexbox percentage math | CSS Grid |
| Cards when `VISUAL_DENSITY > 7` | `border-t`, `divide-y`, negative space |

### Content Bans
| Pattern | Replacement |
|---|---|
| "John Doe", "Jane Smith" | Creative, diverse, realistic names |
| `99.99%`, `$100.00`, `1234567` | Organic messy data: `47.2%`, `+1 (312) 847-1928` |
| "Acme Corp", "Nexus", "SmartFlow" | Contextual, believable brand names |
| "Elevate", "Seamless", "Unleash", "Next-Gen" | Plain, specific, concrete language |
| "Oops!" error messages | Direct: "Connection failed. Please try again." |
| Lorem Ipsum | Real draft copy |
| Exclamation marks in success messages | Confident, not loud |

### Asset Bans
| Pattern | Replacement |
|---|---|
| Emojis in UI | Icons from Phosphor, Radix, or Heroicons |
| Unsplash direct links | `picsum.photos/seed/{name}/W/H` |
| SVG "egg" user icons for avatars | Photo placeholders or styled initials |
| Stock "diverse team" photos | Real photos, candids, or illustration style |
| Lucide/Feather exclusively | Phosphor, Radix, or Heroicons |
| Rocketship for "Launch" | Less obvious metaphors (bolt, spark) |

### Component Bans
| Pattern | Replacement |
|---|---|
| Generic card (border + shadow + white bg) | Elevation only when hierarchy demands it |
| Accordion FAQ section | Side-by-side list, searchable help |
| 3-card carousel testimonials with dots | Masonry wall, embedded posts, single rotating quote |
| Modal for every action | Inline editing, slide-over panels, expandable sections |
| shadcn/ui in default state | Customized radii, colors, and shadows |
| Footer link farm with 4 columns | Simplified main paths + legal links |


## 15. Creative Arsenal

Do not default to generic UI. Pull from this library of advanced concepts to ensure output is visually striking and memorable.

### Hero Sections
- Stop doing centered text over a dark image. Try asymmetric hero sections: text cleanly aligned to the left or right. Background should feature a high-quality, relevant image with a subtle stylistic fade (darkening or lightening gracefully into the background color).

### Typography Upgrades
- **Variable font animation.** Interpolate weight or width on scroll or hover for text that feels alive.
- **Outlined-to-fill transitions.** Text starts as a stroke outline and fills with color on scroll entry or interaction.
- **Text mask reveals.** Large typography acting as a window to video or animated imagery behind it.
- **Kinetic marquee.** Endless text bands that reverse direction or speed up on scroll.
- **Text scramble effect.** Matrix-style character decoding on load or hover.
- **Circular text path.** Text curved along a spinning circular path.
- **Gradient stroke animation.** Outlined text with a gradient continuously running along the stroke.
- **Kinetic typography grid.** A grid of letters dodging or rotating away from the cursor.

### Navigation & Menu Concepts
- **macOS Dock magnification.** Navbar at the edge; icons scale fluidly on hover.
- **Magnetic button.** Buttons that physically pull toward the cursor.
- **Gooey menu.** Sub-items detach from the main button like a viscous liquid.
- **Dynamic island.** A pill-shaped UI component that morphs to show status/alerts.
- **Contextual radial menu.** A circular menu expanding exactly at click coordinates.
- **Floating speed dial.** A FAB that springs out into a curved line of secondary actions.
- **Mega menu reveal.** Full-screen dropdowns that stagger-fade complex content.

### Layout & Grid Concepts
- **Bento grid.** Asymmetric, tile-based grouping (e.g., Apple Control Center).
- **Masonry layout.** Staggered grid without fixed row heights.
- **Chroma grid.** Grid borders or tiles showing subtle, continuously animating color gradients.
- **Split-screen scroll.** Two screen halves sliding in opposite directions on scroll.
- **Curtain reveal.** A hero section parting in the middle like a curtain on scroll.
- **Broken grid / asymmetry.** Elements that deliberately ignore column structure — overlapping, bleeding off-screen, or offset.
- **Whitespace maximization.** Aggressive use of negative space to force focus on a single element.
- **Parallax card stacks.** Sections that stick and physically stack over each other during scroll.

### Card & Container Concepts
- **Parallax tilt card.** A 3D-tilting card tracking mouse coordinates.
- **Spotlight border card.** Card borders that illuminate dynamically under the cursor.
- **Glassmorphism panel.** True frosted glass with inner refraction borders.
- **Holographic foil card.** Iridescent, rainbow light reflections shifting on hover.
- **Tinder swipe stack.** A physical stack of cards the user can swipe away.
- **Morphing modal.** A button that seamlessly expands into its own full-screen dialog container.

### Scroll Animation Concepts
- **Sticky scroll stack.** Cards that stick to the top and physically stack over each other.
- **Horizontal scroll hijack.** Vertical scroll translates into a smooth horizontal gallery pan.
- **Locomotive scroll sequence.** Video/3D sequences where framerate is tied directly to the scrollbar.
- **Zoom parallax.** A central background image zooming in/out seamlessly as you scroll.
- **Scroll progress path.** SVG vector lines or routes that draw themselves as the user scrolls.
- **Liquid swipe transition.** Page transitions that wipe the screen like a viscous liquid.
- **Smooth scroll with inertia.** Decouple scrolling from browser defaults for a heavier, cinematic feel.
- **Scroll-driven reveals.** Content entering through expanding masks, wipes, or draw-on SVG paths tied to scroll progress.

### Gallery & Media Concepts
- **Dome gallery.** A 3D gallery feeling like a panoramic dome.
- **Coverflow carousel.** 3D carousel with the center focused and edges angled back.
- **Drag-to-pan grid.** A boundless grid you can freely drag in any compass direction.
- **Accordion image slider.** Narrow vertical/horizontal image strips that expand fully on hover.
- **Hover image trail.** The mouse leaves a trail of popping/fading images behind it.
- **Glitch effect image.** Brief RGB-channel shifting digital distortion on hover.

### Micro-Interaction Concepts
- **Particle explosion button.** CTAs that shatter into particles upon success.
- **Liquid pull-to-refresh.** Mobile reload indicators acting like detaching water droplets.
- **Skeleton shimmer.** Shifting light reflections moving across placeholder boxes.
- **Directional hover-aware button.** Hover fill entering from the exact side the mouse entered.
- **Ripple click effect.** Visual waves rippling precisely from click coordinates.
- **Animated SVG line drawing.** Vectors that draw their own contours in real-time.
- **Mesh gradient background.** Organic, lava-lamp-like animated color blobs.
- **Lens blur depth.** Dynamic focus blurring background UI layers to highlight a foreground action.
- **Spotlight borders on containers.** Borders that illuminate dynamically under the cursor.
- **Grain and noise overlays.** A fixed, `pointer-events-none` overlay with subtle noise to break digital flatness.
- **Colored, tinted shadows.** Shadows that carry the hue of the background rather than using generic black.


## 16. Bento Paradigm

When generating modern SaaS dashboards or feature sections, utilize this architecture and motion philosophy. This goes beyond static cards and enforces a premium aesthetic heavily reliant on perpetual physics.

### Core Design Philosophy
- **Palette:** Background in `#f9fafb`. Cards are pure white (`#ffffff`) with a 1px border of `border-slate-200/50`.
- **Surfaces:** Use `rounded-[2.5rem]` for all major containers. Apply a diffusion shadow (`shadow-[0_20px_40px_-15px_rgba(0,0,0,0.05)]`) to create depth without clutter.
- **Typography:** Strict `Geist`, `Satoshi`, or `Cabinet Grotesk` font stack with subtle `tracking-tight` for headers.
- **Labels:** Titles and descriptions placed outside and below the cards for a clean, gallery-style presentation.
- **Padding:** Generous `p-8` or `p-10` inside cards.

### Animation Engine
All cards must contain perpetual micro-interactions:
- **Spring physics:** No linear easing. Use `type: "spring", stiffness: 100, damping: 20`.
- **Layout transitions:** Heavily utilize `layout` and `layoutId` props for smooth re-ordering, resizing, and shared element transitions.
- **Infinite loops:** Every card must have an active state that loops infinitely (pulse, typewriter, float, or carousel) so the dashboard feels alive.
- **Performance:** Wrap dynamic lists in `<AnimatePresence>` and optimize for 60fps. Any perpetual motion MUST be memoized (`React.memo`) and isolated in its own microscopic Client Component.

### Five Card Archetypes
Implement these specific micro-animations when constructing Bento grids (e.g., Row 1: 3 cols | Row 2: 2 cols split 70/30):

1. **The Intelligent List.** A vertical stack of items with an infinite auto-sorting loop. Items swap positions using `layoutId`, simulating an AI prioritizing tasks in real-time.
2. **The Command Input.** A search/AI bar with a multi-step typewriter effect. It cycles through complex prompts, including a blinking cursor and a "processing" state with a shimmering loading gradient.
3. **The Live Status.** A scheduling interface with breathing status indicators. Include a pop-up notification badge that emerges with an overshoot spring effect, stays for 3 seconds, and vanishes.
4. **The Wide Data Stream.** A horizontal infinite carousel of data cards or metrics. Ensure the loop is seamless (using `x: ["0%", "-100%"]`) with effortless speed.
5. **The Contextual UI (Focus Mode).** A document view that animates a staggered highlight of a text block, followed by a float-in of a floating action toolbar with micro-icons.


## 17. Pre-Flight Checklist

Evaluate code against this matrix before every output. This is the last filter applied.

### Architecture
- [ ] Every import actually exists in `package.json` or project dependencies.
- [ ] Global state is used only to avoid deep prop-drilling, not arbitrarily.
- [ ] Interactive components are isolated as `'use client'` leaf components.
- [ ] `useEffect` animations contain strict cleanup functions.
- [ ] CPU-heavy perpetual animations are isolated in their own memoized Client Components.

### Layout
- [ ] Mobile layout collapse (`w-full`, `px-4`, `max-w-7xl mx-auto`) is guaranteed for high-variance designs.
- [ ] Full-height sections use `min-h-[100dvh]`, never `h-screen`.
- [ ] Container max-width is set (1200–1440px range).
- [ ] No complex flexbox percentage math — CSS Grid is used instead.
- [ ] Buttons are bottom-aligned across card groups.
- [ ] Shared elements (titles, prices, CTAs) are vertically aligned across sibling cards/columns.

### Visual
- [ ] No pure `#000000` anywhere.
- [ ] Accent color saturation is below 80%.
- [ ] Only one accent color is used.
- [ ] Shadows are tinted to match the background hue.
- [ ] Gray family is consistent (all warm or all cool, not mixed).
- [ ] No AI purple/blue gradient aesthetic.
- [ ] Border-radius varies between inner elements and containers.

### Typography
- [ ] Inter font is not used.
- [ ] Font weights include 500 or 600, not just 400 and 700.
- [ ] Body text is constrained to ~65 characters width.
- [ ] Headlines have tightened tracking and reduced line-height.
- [ ] Tabular figures are enabled for numeric data.
- [ ] Sentence case is used for headings.

### Interactivity
- [ ] Every button has a hover state.
- [ ] Every button has an active/pressed state.
- [ ] Transitions are 200–300ms on all interactive elements.
- [ ] Focus rings are visible on all focusable elements.
- [ ] Loading states use skeleton loaders, not spinners.
- [ ] Empty states are designed with guidance.
- [ ] Error states are inline, not `window.alert()`.
- [ ] Active nav link is visually distinguished.
- [ ] `scroll-behavior: smooth` is applied.

### Content
- [ ] No "John Doe" or generic placeholder names.
- [ ] No round fake numbers.
- [ ] No Lorem Ipsum.
- [ ] No AI cliché words (elevate, seamless, unleash, etc.).
- [ ] No emojis.
- [ ] Unique avatars for every distinct person.
- [ ] Blog/content dates are varied and realistic.

### Assets
- [ ] Favicon is present.
- [ ] No broken Unsplash links — using `picsum.photos` or SVG placeholders.
- [ ] All images have descriptive alt text.
- [ ] Icon stroke widths are consistent across the entire project.

### Completeness
- [ ] Privacy policy and terms links exist in the footer.
- [ ] Every page has back navigation — no dead ends.
- [ ] Custom 404 page exists.
- [ ] Form validation is implemented client-side.
- [ ] Skip-to-content link exists for keyboard users.
- [ ] Meta tags are present (title, description, og:image).
- [ ] No dead links (`href="#"` without purpose).
- [ ] No commented-out dead code.
- [ ] No arbitrary z-index values.

### Output Integrity
- [ ] No banned output patterns appear anywhere in the response.
- [ ] Every deliverable the user requested is present and complete.
- [ ] All code blocks contain runnable code, not descriptions.
- [ ] Nothing was shortened, truncated, or summarized to save space.
```
