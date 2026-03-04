# Portfolio & Creative Website — Product Requirements

**Status:** Approved
**Author:** Waymaker
**Date:** 2026-03-03

## Problem Statement

Creative professionals — designers, photographers, artists, filmmakers, illustrators — need to show their work, not describe it. A portfolio is the primary sales tool for anyone in a visual or creative field. Potential clients judge quality in seconds. If the work doesn't look exceptional on the first scroll, the visitor is gone.

Social media platforms like Instagram, Behance, and Dribbble serve as discovery channels, but they are rented ground. Algorithms change, feeds get cluttered, and every creative competes in an identical grid. A personal portfolio website is the destination — the place where a client moves from "interesting" to "I want to hire this person." It's the only channel where the creative controls the layout, the pacing, the narrative, and the brand.

Without a dedicated portfolio site, creatives lose credibility. Sending a potential client to an Instagram profile signals "I'm not serious enough to have my own site." Worse, it puts the client one scroll away from a competitor's work. A portfolio website is not optional — it's the difference between being discovered and being hired.

## Goals

1. Showcase work visually — let images and projects speak, not paragraphs of text
2. Establish professional credibility — a polished, personal brand presence
3. Convert visitors to inquiries — clear path from "I like this work" to "Let's talk"
4. Curate the experience — control what's shown, in what order, with what context
5. Perform fast — image-heavy sites must still load quickly on mobile

## Non-Goals

- This is NOT an e-commerce store — no shopping cart, product listings, or payment processing
- This is NOT a blog or content platform — no articles, RSS feeds, or comment systems
- This is NOT a CMS — content is baked into the build, not managed through a dashboard
- This is NOT a social network — no followers, likes, or public comments

## Sections

### Hero / Introduction

**Purpose:** Strong first impression. The visitor should immediately understand who this person is and what kind of work they do. No clutter, no navigation menus competing for attention — just the name, a single line, and one hero image or project that sets the tone.

**Content Questions:**
- What is your name or studio name?
- What do you do, described in one line? (e.g. "Visual designer based in Melbourne" or "Documentary photographer")
- What hero image or featured project should appear first?

**Design Notes:** Minimal hero — large typography for the name, one hero image that fills the viewport, dark or light theme based on the work. No navigation clutter above the fold. The hero IS the first impression. Consider a subtle scroll indicator.

---

### Work / Projects Grid

**Purpose:** The core of the entire site. This is what the visitor came to see. Every project should be presented at its best — consistent framing, high-quality images, enough context to understand the work without drowning it in text.

**Content Questions:**
- What are your best 6-12 projects?
- For each project: what is the title, client (if applicable), and 1-3 key images?
- Do any projects have written case studies or descriptions?
- Do your projects fall into categories (e.g. branding, web, photography, illustration)?

**Design Notes:** Masonry or uniform grid layout. Hover effects reveal project title and category. Click opens a detail view or lightbox with additional images and a brief description. If the creative works across categories, provide filter or tab navigation at the top of the section. Images must be consistently sized or use a masonry layout that handles mixed aspect ratios gracefully.

---

### About

**Purpose:** Personal connection. After the work impresses, the client wants to know who's behind it. The About section builds trust and relatability — a face, a philosophy, a sense of the person they'd be working with.

**Content Questions:**
- What is your background and experience? (2-3 paragraphs max)
- What is your design philosophy or creative approach?
- Do you have a portrait or professional photo?
- Any notable clients, awards, publications, or press features?

**Design Notes:** Split layout — portrait on one side, text on the other. Keep it concise; this isn't a biography, it's a trust signal. If there are notable clients, show a logo bar (grayscale logos, 4-8 max). Awards or press mentions as small badges or a simple list. The photo should be professional but not corporate — authentic to the creative's brand.

---

### Process

**Purpose:** Reduce friction for potential clients by explaining how you work. Clients who've never hired a creative don't know what to expect — timeline, deliverables, what they need to provide. A clear process section answers these questions before they're asked.

**Content Questions:**
- What are the typical steps in your process? (e.g. Discovery, Concept, Design, Delivery)
- How long does a typical project take?
- What does the client need to provide? (brief, assets, content, feedback)

**Design Notes:** Numbered steps or a horizontal timeline. Keep it to 3-5 steps — more than that and it feels bureaucratic. One icon per step (simple line icons). Clean and minimal — the process section should feel reassuring, not overwhelming.

---

### Contact

**Purpose:** Simple, clear way to reach out. After seeing the work, reading the about, understanding the process — this is where the visitor acts. Remove every barrier between "I want to hire this person" and "I've sent the message."

**Content Questions:**
- What is your email address?
- What social profiles should be linked? (Instagram, Behance, Dribbble, LinkedIn, etc.)
- Do you prefer a contact form or a direct email link?
- Are you currently available for new projects?

**Design Notes:** Minimal. Large "Let's work together" or similar heading. Email address displayed prominently (not hidden behind a form). Social media icons. If there's an availability status, show it clearly — "Available for projects starting May 2026" or "Currently booked — accepting briefs for Q3." A contact form is optional; many creatives prefer a direct email link.

## Design Specification

| Token | Value |
|-------|-------|
| Colour Palette | Minimal — black, white, and one accent colour. Let the work provide the colour. Dark mode works well for photographers and visual designers. |
| Typography | Modern, distinctive (e.g. Space Grotesk, Syne, Outfit). Name/headings in a display weight. Body in a clean sans-serif. |
| Mood | Confident, minimal, visually-led. The portfolio should feel curated, not cluttered. |
| Layout | Grid-heavy for work. Minimal navigation. Large images. Generous whitespace. Scroll-driven rather than click-heavy. |

## Content Requirements

What the user must provide:

- Name or studio name
- One-line description of what they do
- Hero image or featured project image
- 6-12 projects, each with: title, client name (optional), 1-3 high-quality images, brief description or case study (optional), category/tag
- About text (2-3 paragraphs)
- Portrait or professional photo
- Notable clients, awards, or press mentions (if any)
- Process steps (3-5 steps with titles and one-line descriptions)
- Typical project timeline
- Email address
- Social media profile URLs
- Availability status (optional)

## Technical Requirements

- Single-page layout with smooth scroll navigation
- Semantic HTML: `nav`, `main`, `section`, `footer`
- Mobile-first responsive design (375px → 768px → 1024px+)
- Performance: compressed images, lazy loading, minimal JS
- Accessibility: proper heading hierarchy, alt text, colour contrast (WCAG AA)
- SEO: meta title + description, Open Graph tags, semantic markup
- CSS Grid or Masonry layout for the projects section — handle mixed aspect ratios
- Lazy loading for all project images (portfolios are image-heavy, performance is critical)
- Lightbox or detail view for individual project deep-dives
- Filter/tab navigation for project categories (if the creative works across disciplines)
- Smooth scroll animations on section entry (subtle — parallax or fade-in, not distracting)
- Dark mode support (many photographers and visual designers prefer dark backgrounds)
- Image optimization: serve WebP where supported, provide fallback, use `srcset` for responsive images
- `Person` structured data (schema.org) for the creative professional

## Success Criteria

| Metric | Target |
|--------|--------|
| Mobile responsive | Works on 375px+ screens |
| Page load | < 3 seconds on 3G |
| Accessibility | WCAG AA compliant |
| SEO ready | Meta tags, semantic HTML, structured data |
| Build time (with AI) | < 30 minutes |
| Image lazy loading | All project images below the fold load on scroll |
| Project grid | Displays 6-12 projects without layout breaking |
| Contact conversion | Email or form link reachable within 2 clicks from any section |
