---
sync:
  type: doc
  layer: Website — Portfolio & Creative
build:
  status: todo
  phase: 1
  priority: P0
  depends_on: []
  started_at: null
  completed_at: null
---

# Phase 1: Build Portfolio & Creative Website

**Goal:** A complete, deployed portfolio website with all sections — hero/introduction, work/projects grid, about, process, contact. Mobile-first, semantic HTML, performance-optimised.

**PRD Reference:** `docs/01-planning/product-requirements/website-portfolio-prd.md`

---

## Build Path Detection

Detect your environment:

- **IDE Path** (Claude Code, Cursor, Codex) — you have filesystem access, can create files, run dev servers
- **Conversational Path** (Claude Desktop, Host Direct) — you have MCP tools, build in conversation, deploy via `host_app_upload`

Both paths produce the same output — a deployed website. Follow the instructions for your environment below.

---

## IDE Path

### 1. Project Setup

Create a single-page website project:

```
website-portfolio/
├── index.html
├── styles.css
├── script.js
└── assets/
    ├── projects/          # Project images (optimised WebP/JPG)
    ├── headshot.jpg       # Portrait photo
    └── favicon.svg        # Simple monogram or icon
```

### 2. HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Portfolio of [Name] — [discipline]. Selected work in [categories].">
  <title>[Name] — [Discipline]</title>
  <link rel="icon" href="assets/favicon.svg" type="image/svg+xml">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Inter:wght@400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">

  <!-- Structured Data: Person -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "[Full Name]",
    "jobTitle": "[Title / Discipline]",
    "url": "[website URL]",
    "sameAs": [
      "https://instagram.com/[handle]",
      "https://dribbble.com/[handle]",
      "https://behance.net/[handle]",
      "https://linkedin.com/in/[handle]"
    ],
    "image": "[headshot URL]",
    "description": "[One-line description]"
  }
  </script>
</head>
<body>
  <nav id="navbar"><!-- Sticky nav with name/logo + links + CTA --></nav>
  <main>
    <section id="hero"><!-- Name, discipline, one-liner, CTA --></section>
    <section id="work"><!-- Category filter tabs + project grid --></section>
    <section id="about"><!-- Bio, photo, skills, clients/awards --></section>
    <section id="process"><!-- Process timeline/steps --></section>
    <section id="contact"><!-- Availability status, email, social links --></section>
  </main>
  <footer><!-- Copyright, back to top --></footer>

  <!-- Lightbox overlay (hidden by default) -->
  <div id="lightbox" class="lightbox" role="dialog" aria-label="Project image viewer" hidden>
    <button class="lightbox-close" aria-label="Close">&times;</button>
    <img class="lightbox-img" src="" alt="">
    <button class="lightbox-prev" aria-label="Previous">&lsaquo;</button>
    <button class="lightbox-next" aria-label="Next">&rsaquo;</button>
  </div>

  <script src="script.js"></script>
</body>
</html>
```

### 3. Build Sections

#### 3.1 Navigation

Sticky top nav bar. Transparent on hero, gains background on scroll.

```html
<nav id="navbar" class="navbar">
  <div class="nav-inner container">
    <a href="#hero" class="nav-logo">[Name]</a>
    <button class="nav-toggle" aria-label="Toggle menu" aria-expanded="false">
      <span class="hamburger"></span>
    </button>
    <ul class="nav-links">
      <li><a href="#work">Work</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#process">Process</a></li>
      <li><a href="#contact" class="nav-cta">Get in Touch</a></li>
    </ul>
  </div>
</nav>
```

- On mobile, `nav-toggle` opens a full-screen or slide-down overlay with links.
- Active link highlight based on scroll position.

#### 3.2 Hero / Introduction

Full viewport height. Minimal and bold.

```html
<section id="hero" class="hero">
  <div class="container hero-content">
    <p class="hero-eyebrow">[Discipline] — [Location]</p>
    <h1 class="hero-title">[Name]</h1>
    <p class="hero-subtitle">[One-line description of what you do and who you do it for]</p>
    <a href="#work" class="btn btn-primary">View Work</a>
  </div>
</section>
```

- Large display heading (clamp between 3rem and 6rem).
- Subtle entrance animation (fade-up on load, CSS only).
- Optional: background texture, gradient, or a single hero image with overlay.

#### 3.3 Work / Projects Grid

The centrepiece. A filterable grid of 6-12 projects.

```html
<section id="work" class="work">
  <div class="container">
    <h2 class="section-title">Selected Work</h2>

    <!-- Category Filter Tabs -->
    <div class="filter-tabs" role="tablist" aria-label="Filter projects by category">
      <button class="filter-tab active" role="tab" data-filter="all" aria-selected="true">All</button>
      <button class="filter-tab" role="tab" data-filter="branding">Branding</button>
      <button class="filter-tab" role="tab" data-filter="web">Web</button>
      <button class="filter-tab" role="tab" data-filter="photography">Photography</button>
      <!-- Add categories as needed -->
    </div>

    <!-- Project Grid -->
    <div class="project-grid">
      <article class="project-card" data-category="branding">
        <div class="project-image-wrap">
          <img src="assets/projects/project-1.jpg" alt="[Project title] — [brief description]" loading="lazy">
          <div class="project-overlay">
            <h3 class="project-title">[Project Title]</h3>
            <p class="project-category">[Category]</p>
            <button class="project-view" data-index="0" aria-label="View [Project Title]">View</button>
          </div>
        </div>
      </article>
      <!-- Repeat for each project -->
    </div>
  </div>
</section>
```

- **Grid layout**: Use CSS Grid with `auto-fill` and `minmax(300px, 1fr)` for responsive columns. For a true masonry effect, use CSS `columns` property or `grid-template-rows: masonry` (with fallback).
- **Filter tabs**: JS filters cards by `data-category`. "All" shows everything. Animate with fade/scale transition.
- **Hover effect**: On desktop, hovering a card reveals the overlay with title, category, and "View" button. On mobile, overlay is always visible or toggled by tap.
- **Lightbox**: Clicking "View" opens the lightbox with the full-size image. Prev/next arrows cycle through projects. Close on Escape key or close button.

#### 3.4 About

Two-column layout (photo + text) on desktop, stacked on mobile.

```html
<section id="about" class="about">
  <div class="container about-grid">
    <div class="about-image">
      <img src="assets/headshot.jpg" alt="[Name]" loading="lazy">
    </div>
    <div class="about-content">
      <h2 class="section-title">About</h2>
      <p class="about-bio">[2-3 paragraph bio covering background, philosophy, and approach]</p>

      <div class="about-details">
        <div class="about-detail">
          <h3>Skills</h3>
          <ul class="tag-list">
            <li>Brand Identity</li>
            <li>UI/UX Design</li>
            <!-- ... -->
          </ul>
        </div>
        <div class="about-detail">
          <h3>Notable Clients</h3>
          <ul class="client-list">
            <li>[Client 1]</li>
            <li>[Client 2]</li>
            <!-- ... -->
          </ul>
        </div>
        <div class="about-detail" data-if="awards">
          <h3>Awards</h3>
          <ul>
            <li>[Award — Year]</li>
            <!-- ... -->
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>
```

#### 3.5 Process

A horizontal timeline on desktop, vertical on mobile. 3-5 steps.

```html
<section id="process" class="process">
  <div class="container">
    <h2 class="section-title">Process</h2>
    <p class="section-subtitle">How I work with clients from brief to delivery.</p>

    <div class="process-timeline">
      <div class="process-step">
        <div class="step-number">01</div>
        <h3 class="step-title">Discovery</h3>
        <p class="step-desc">Understanding your brand, audience, and goals through research and conversation.</p>
      </div>
      <div class="process-step">
        <div class="step-number">02</div>
        <h3 class="step-title">Concept</h3>
        <p class="step-desc">Exploring directions, mood boards, and initial concepts for your feedback.</p>
      </div>
      <div class="process-step">
        <div class="step-number">03</div>
        <h3 class="step-title">Design</h3>
        <p class="step-desc">Refining the chosen direction into polished deliverables with iterative reviews.</p>
      </div>
      <div class="process-step">
        <div class="step-number">04</div>
        <h3 class="step-title">Deliver</h3>
        <p class="step-desc">Final assets, guidelines, and handover — plus ongoing support if you need it.</p>
      </div>
    </div>
  </div>
</section>
```

- Connect steps with a line (horizontal on desktop via `::before` pseudo-element, vertical on mobile).
- Step numbers use the accent colour.
- Optional: reveal on scroll with `IntersectionObserver`.

#### 3.6 Contact

```html
<section id="contact" class="contact">
  <div class="container contact-content">
    <h2 class="section-title">Get in Touch</h2>

    <div class="availability-status">
      <span class="status-dot available"></span>
      <span>Currently available for new projects</span>
    </div>

    <p class="contact-lead">Have a project in mind? I'd love to hear about it.</p>

    <a href="mailto:[email]" class="contact-email">[email@example.com]</a>

    <div class="social-links">
      <a href="https://instagram.com/[handle]" target="_blank" rel="noopener" aria-label="Instagram">
        <!-- Instagram SVG icon -->
      </a>
      <a href="https://dribbble.com/[handle]" target="_blank" rel="noopener" aria-label="Dribbble">
        <!-- Dribbble SVG icon -->
      </a>
      <a href="https://behance.net/[handle]" target="_blank" rel="noopener" aria-label="Behance">
        <!-- Behance SVG icon -->
      </a>
      <a href="https://linkedin.com/in/[handle]" target="_blank" rel="noopener" aria-label="LinkedIn">
        <!-- LinkedIn SVG icon -->
      </a>
    </div>
  </div>
</section>
```

- `availability-status`: green dot = available, amber = limited, red = unavailable. Set via a class.
- Social icons as inline SVGs for crisp rendering and easy colour control.
- Centre-aligned layout for impact.

#### 3.7 Footer

```html
<footer class="footer">
  <div class="container footer-inner">
    <p>&copy; [Year] [Name]. All rights reserved.</p>
    <a href="#hero" class="back-to-top" aria-label="Back to top">&uarr;</a>
  </div>
</footer>
```

### 4. CSS Architecture

Mobile-first with breakpoints at 768px and 1024px.

```css
/* ============================================
   Design Tokens
   ============================================ */
:root {
  /* Colours — Light Mode (default) */
  --color-primary: #1a1a1a;
  --color-background: #ffffff;
  --color-surface: #f5f5f5;
  --color-text: #1a1a1a;
  --color-text-muted: #666666;
  --color-accent: #2563eb;       /* User's chosen accent */
  --color-accent-hover: #1d4ed8;
  --color-border: #e5e5e5;

  /* Typography */
  --font-heading: 'Space Grotesk', sans-serif;
  --font-body: 'Inter', sans-serif;

  /* Spacing */
  --space-xs: 0.5rem;
  --space-sm: 1rem;
  --space-md: 2rem;
  --space-lg: 4rem;
  --space-xl: 6rem;
  --space-section: 8rem;

  /* Sizing */
  --container-max: 1200px;
  --nav-height: 64px;
  --border-radius: 8px;

  /* Transitions */
  --transition-fast: 150ms ease;
  --transition-base: 300ms ease;
}

/* Dark Mode Variant */
[data-theme="dark"] {
  --color-primary: #ffffff;
  --color-background: #0a0a0a;
  --color-surface: #141414;
  --color-text: #f0f0f0;
  --color-text-muted: #999999;
  --color-border: #2a2a2a;
}

/* ============================================
   Reset & Base
   ============================================ */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; scroll-padding-top: var(--nav-height); }
body {
  font-family: var(--font-body);
  color: var(--color-text);
  background: var(--color-background);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}
img { max-width: 100%; height: auto; display: block; }
a { color: inherit; text-decoration: none; }
ul { list-style: none; }

.container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--space-sm);
}

@media (min-width: 768px) {
  .container { padding: 0 var(--space-md); }
}

/* ============================================
   Key Patterns
   ============================================ */

/* Section spacing */
section { padding: var(--space-xl) 0; }
@media (min-width: 768px) { section { padding: var(--space-section) 0; } }

.section-title {
  font-family: var(--font-heading);
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  margin-bottom: var(--space-sm);
}

/* Project grid — responsive with masonry-like layout */
.project-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-sm);
}
@media (min-width: 768px) {
  .project-grid { grid-template-columns: repeat(2, 1fr); gap: var(--space-md); }
}
@media (min-width: 1024px) {
  .project-grid { grid-template-columns: repeat(3, 1fr); }
}

/* Card hover */
.project-card { position: relative; overflow: hidden; border-radius: var(--border-radius); }
.project-overlay {
  position: absolute; inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  opacity: 0; transition: opacity var(--transition-base);
  color: #fff;
}
.project-card:hover .project-overlay,
.project-card:focus-within .project-overlay { opacity: 1; }

/* Lightbox */
.lightbox {
  position: fixed; inset: 0; z-index: 1000;
  background: rgba(0,0,0,0.95);
  display: flex; align-items: center; justify-content: center;
}
.lightbox[hidden] { display: none; }
.lightbox-img { max-width: 90vw; max-height: 85vh; object-fit: contain; }
.lightbox-close, .lightbox-prev, .lightbox-next {
  position: absolute; background: none; border: none;
  color: #fff; font-size: 2rem; cursor: pointer;
}
.lightbox-close { top: 1rem; right: 1rem; }
.lightbox-prev { left: 1rem; top: 50%; transform: translateY(-50%); }
.lightbox-next { right: 1rem; top: 50%; transform: translateY(-50%); }

/* Filter tabs */
.filter-tabs {
  display: flex; flex-wrap: wrap; gap: var(--space-xs);
  margin-bottom: var(--space-md);
}
.filter-tab {
  padding: var(--space-xs) var(--space-sm);
  border: 1px solid var(--color-border);
  border-radius: 999px; background: transparent;
  font-family: var(--font-body); cursor: pointer;
  transition: all var(--transition-fast);
}
.filter-tab.active,
.filter-tab:hover {
  background: var(--color-primary);
  color: var(--color-background);
  border-color: var(--color-primary);
}

/* Process timeline */
.process-timeline {
  display: grid; grid-template-columns: 1fr; gap: var(--space-md);
}
@media (min-width: 768px) {
  .process-timeline { grid-template-columns: repeat(4, 1fr); }
}
.step-number {
  font-family: var(--font-heading); font-size: 2rem;
  font-weight: 700; color: var(--color-accent);
  margin-bottom: var(--space-xs);
}

/* Availability dot */
.status-dot {
  display: inline-block; width: 10px; height: 10px;
  border-radius: 50%; margin-right: 0.5rem;
}
.status-dot.available { background: #22c55e; }
.status-dot.limited { background: #f59e0b; }
.status-dot.unavailable { background: #ef4444; }
```

### 5. JavaScript (script.js)

Implement the following in vanilla JS (no frameworks):

1. **Smooth scroll** — handled by CSS `scroll-behavior: smooth`, but add JS fallback for anchor clicks with offset for the sticky nav.
2. **Mobile menu toggle** — toggle `nav-open` class on body, update `aria-expanded`.
3. **Navbar scroll effect** — add `scrolled` class to `#navbar` when `scrollY > 50`, changing background from transparent to solid.
4. **Category filter** — on tab click, filter `.project-card` elements by `data-category`. Animate with CSS transitions (opacity/transform). Update `aria-selected` on tabs.
5. **Lightbox** — on "View" button click, show `#lightbox` with the corresponding image. Prev/next cycle through visible (filtered) projects. Close on Escape, close button, or clicking backdrop. Trap focus inside lightbox when open.
6. **Scroll reveal** — use `IntersectionObserver` to add `.revealed` class to sections as they enter the viewport. CSS handles the animation (fade-up).

### 6. Deploy

```bash
# Via Waymaker CLI
cd website-portfolio
waymaker push

# Or via MCP tool
# Use host_app_upload with all files
```

---

## Conversational Path

### Step 1: Gather Business Details

Ask these questions in order. Move to the next question after each answer. Do not skip any.

**Essential (must have before building):**

1. What is your name or studio name?
2. What do you do in one line? (e.g., "Brand identity and web design for startups")
3. Please share 6-12 of your best projects. For each, I need: title, category, and an image URL or file.

**Content (ask after essentials):**

4. What categories should the filter tabs show? (e.g., Branding, Web Design, Photography, Illustration)
5. Tell me about yourself — a 2-3 sentence bio covering your background and design philosophy.
6. What does your process look like? Give me 3-5 steps (e.g., Discovery, Concept, Design, Deliver).
7. Any notable clients or awards you'd like to feature?
8. What is your contact email?
9. What social media links should I include? (Instagram, Dribbble, Behance, LinkedIn — provide handles or URLs)
10. Do you prefer a light or dark theme?
11. Do you have a preferred accent colour? (Default: electric blue)
12. Are you currently available for new projects? (Available / Limited Availability / Not Available)

### Step 2: Build the Website

Once you have the answers:

1. **Set the theme**: Apply light or dark mode tokens based on preference. Set the accent colour.
2. **Build index.html**: Create the full HTML with all sections populated with real content. Use the project data to build the grid, the bio for the about section, process steps for the timeline.
3. **Build styles.css**: Use the complete CSS architecture from the IDE path above, adjusting tokens for their colour choices.
4. **Build script.js**: Include all interactive features — mobile menu, filter tabs, lightbox, scroll effects.
5. **Populate structured data**: Fill in the Person schema with their real name, title, URL, and social links.
6. **Optimise images**: If provided as URLs, reference them directly. If files, include them in the upload.

### Step 3: Deploy

Deploy using the `host_app_upload` MCP tool:

```
Use host_app_upload with:
- files: [index.html, styles.css, script.js, plus any asset files]
- app_name: "[name]-portfolio" or custom slug
```

Confirm the live URL with the user and walk through each section to verify content accuracy.

---

## Design Tokens

| Token | Light Mode | Dark Mode |
|-------|-----------|-----------|
| Primary | `#1a1a1a` (charcoal) | `#ffffff` (white) |
| Background | `#ffffff` | `#0a0a0a` |
| Surface | `#f5f5f5` | `#141414` |
| Text | `#1a1a1a` | `#f0f0f0` |
| Text Muted | `#666666` | `#999999` |
| Accent | User's choice (default `#2563eb`) | Same |
| Border | `#e5e5e5` | `#2a2a2a` |
| Headings Font | Space Grotesk (alt: Syne, Outfit) | Same |
| Body Font | Inter (or any clean sans-serif) | Same |

## Technical Requirements

- **Performance**: All images lazy-loaded (`loading="lazy"`). Google Fonts loaded with `display=swap`. No render-blocking JS. Target < 2s LCP.
- **Accessibility**: All interactive elements keyboard-navigable. ARIA labels on icon-only buttons. Focus trap in lightbox. Colour contrast ratio >= 4.5:1 for body text, >= 3:1 for large text.
- **SEO**: Semantic HTML5 elements (`nav`, `main`, `section`, `article`, `footer`). Descriptive `alt` text on all images. `meta description` populated. Person structured data.
- **Responsive**: Mobile-first. Three breakpoints: base (mobile), 768px (tablet), 1024px (desktop). No horizontal scroll at any viewport.
- **Browser support**: Modern browsers (Chrome, Firefox, Safari, Edge — last 2 versions). No IE11 support needed.
- **No dependencies**: Vanilla HTML, CSS, JS only. No frameworks, no build tools, no npm packages.

## Acceptance Criteria

- [ ] Hero section loads with name, discipline, and one-liner. CTA scrolls to Work section.
- [ ] Work section displays all projects in a responsive grid (1 col mobile, 2 col tablet, 3 col desktop).
- [ ] Filter tabs work — clicking a category shows only matching projects, "All" shows everything.
- [ ] Lightbox opens on project click, displays full-size image, prev/next navigation works, closes on Escape.
- [ ] About section shows headshot, bio, skills, and notable clients/awards.
- [ ] Process section displays 3-5 steps in a timeline layout (vertical mobile, horizontal desktop).
- [ ] Contact section shows availability status, email link, and social media icons.
- [ ] Navigation is sticky, highlights active section on scroll, and toggles correctly on mobile.
- [ ] Light/dark mode applies consistently based on user preference.
- [ ] Structured data (Person schema) is valid — test at https://validator.schema.org/.
- [ ] Page scores 90+ on Lighthouse for Performance, Accessibility, Best Practices, and SEO.
- [ ] No console errors. No broken images. No layout shifts.

## Complexity Advisory

Both build paths work well for website blueprints. Websites are single-phase builds with straightforward HTML/CSS — conversational and IDE paths produce equivalent results.
