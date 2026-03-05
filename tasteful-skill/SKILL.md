# Tasteful Skill v2

**Unified Design Engineering System**
Production UI + Architecture + Output Enforcement

---

# 1. Execution Contract

## Core Principle

Every response must behave as if it will be **directly deployed**.

Partial work, placeholders, or conceptual summaries are considered **system failures**.

The system must prioritize **completeness, correctness, and structural integrity** over brevity.

---

## Output Completeness Rule

When a request requires deliverables:

1. Identify the **exact deliverable count**
2. Generate **every deliverable completely**
3. Verify **nothing is omitted**

Examples:

| Request             | Required Output                  |
| ------------------- | -------------------------------- |
| Create 4 components | Output exactly 4 full components |
| Provide a full file | Output the entire file           |
| Build a page        | Output all required sections     |

---

## Prohibited Output Patterns

The following must **never appear** in code:

```
...
// TODO
// rest of code
// implement later
/* truncated */
similar to above
continue pattern
```

Also prohibited in prose:

* “for brevity”
* “you can extend this”
* “remaining sections follow the same pattern”
* “let me know if you'd like more”

These are considered **execution shortcuts**.

---

## Token Boundary Protocol

If output length approaches limits:

1. Finish the **current structural unit**
2. Stop only at:

   * end of a file
   * end of a function
   * end of a section

Then end with:

```
[PAUSED — X of Y complete. Send "continue" to resume from: section_name]
```

Continuation must:

1. reopen the same code block
2. repeat the **last 3 lines**
3. continue immediately

---

# 2. Design Control System

All visual decisions derive from **three design dials**.

```
DESIGN_VARIANCE
MOTION_INTENSITY
VISUAL_DENSITY
```

These behave like **global configuration variables**.

---

## Dial: DESIGN_VARIANCE

Controls layout symmetry and visual structure.

| Level | Behavior             |
| ----- | -------------------- |
| 1–3   | strict symmetry      |
| 4–6   | mild asymmetry       |
| 7–8   | offset grids         |
| 9–10  | experimental layouts |

Implementation techniques:

* overlapping elements
* asymmetric grids
* varied aspect ratios
* intentional whitespace imbalance

Mobile rule:

Any asymmetry above `md` must collapse into a **single-column stack under 768px**.

---

## Dial: MOTION_INTENSITY

Controls motion complexity.

| Level | Behavior              |
| ----- | --------------------- |
| 1–2   | static UI             |
| 3–4   | hover transitions     |
| 5–6   | animated entry        |
| 7–8   | coordinated motion    |
| 9–10  | cinematic interaction |

Guidelines:

Preferred animation properties:

```
transform
opacity
filter
```

Avoid:

```
top
left
width
height
```

These cause layout reflow.

---

## Dial: VISUAL_DENSITY

Controls interface spacing and information packing.

| Level | Behavior            |
| ----- | ------------------- |
| 1–2   | editorial spacing   |
| 3–4   | marketing page      |
| 5–6   | SaaS UI             |
| 7–8   | analytics dashboard |
| 9–10  | trading terminal    |

High density requirements:

```
font-mono for numbers
tabular figures
tight vertical rhythm
```

---

# 3. Technology Integrity Rules

## Default Stack

Unless explicitly overridden:

Framework

```
Next.js (React)
```

Architecture

```
Server Components by default
```

Interactive components must include:

```
'use client'
```

---

## Dependency Verification

Before importing any external library:

Check if dependency exists.

If not present:

Provide installation command before code.

Example:

```
npm install framer-motion
```

Never assume dependencies exist.

---

## Styling Rules

Preferred styling system:

```
Tailwind CSS
```

If a project already uses:

* CSS Modules
* styled-components
* vanilla CSS

then **respect the existing system**.

Never migrate styling frameworks unless requested.

---

# 4. Layout System

## Container Discipline

All page content must be constrained.

Allowed patterns:

```
max-w-7xl mx-auto
max-w-[1400px] mx-auto
```

Full-width layouts are reserved only for:

* hero imagery
* background sections

---

## Grid First Layout

Use **CSS Grid** for structural layout.

Avoid complex flexbox math such as:

```
w-[calc(33%-1rem)]
```

Instead:

```
grid grid-cols-1 md:grid-cols-3 gap-6
```

---

## Depth Hierarchy

Interfaces must contain **at least three visual layers**:

1. Background
2. Surface
3. Interactive layer

Depth may be created using:

* elevation
* contrast
* overlap
* texture

Flat layouts without layering appear unfinished.

---

# 5. Typography Engine

## Font Policy

The following fonts are banned:

```
Inter
system-ui
Arial
Times
```

Approved families:

```
Geist
Outfit
Satoshi
Cabinet Grotesk
```

---

## Scale System

Default type scale:

```
Display: text-6xl
Headline: text-4xl
Section: text-2xl
Body: text-base
Small: text-sm
```

Large text must include:

```
tracking-tight
leading-none
```

Paragraph text must include:

```
max-w-[65ch]
leading-relaxed
```

---

## Weight Hierarchy

Use multiple weights:

```
400 regular
500 medium
600 semibold
700 bold
```

Avoid binary hierarchy.

---

# 6. Color Discipline

## Background Integrity

Pure black is prohibited.

Instead use:

```
zinc-950
slate-950
#0a0a0a
```

---

## Accent Rule

Only **one accent color** allowed.

Example palette:

```
base: zinc
accent: emerald
```

Avoid:

* neon gradients
* rainbow palettes
* multiple accent hues

---

## Shadow Logic

Shadows must match environment color.

Example:

Blue interface → blue tinted shadow.

Avoid generic black shadows.

---

# 7. Interaction System

All interactive elements must include:

### Hover

Visual change on pointer hover.

### Active

Pressed feedback using scale or translate.

### Focus

Visible keyboard focus ring.

### Transition

Default timing:

```
300ms cubic-bezier(0.16, 1, 0.3, 1)
```

---

# 8. State Completeness

Every interface must support:

### Loading state

Use **skeleton placeholders** matching final layout.

Never use a generic spinner.

---

### Empty state

Include:

* message
* icon
* recovery action

Example:

```
"No projects yet"
Create Project
```

---

### Error state

Display:

* readable message
* retry option

---

# 9. Component Quality Rules

A component is considered production-ready only if it includes:

1. visual hierarchy
2. hover states
3. focus states
4. loading state
5. responsive behavior
6. accessibility attributes

Missing any of these is considered **incomplete UI**.

---

# 10. Design Anti-Patterns

The system automatically rejects the following layouts:

Generic SaaS hero

```
centered title
subtitle
button
three feature cards
```

Equal feature grid

```
3 identical cards
```

CTA-only pages with no visual anchor.

Massive gradients used as decoration.

---

# 11. Performance Rules

Animations must use GPU-friendly properties:

```
transform
opacity
```

Avoid layout thrashing.

Images must include:

```
loading="lazy"
```

---

# 12. Mobile Stability

Never use:

```
h-screen
```

Instead:

```
min-h-[100dvh]
```

Prevents iOS viewport jumping.

---

# 13. Accessibility Baseline

Minimum requirements:

* keyboard navigation
* visible focus
* aria labels for icons
* color contrast ≥ WCAG AA

Accessibility is **mandatory**, not optional.

---

# End of Tasteful Skill v2
