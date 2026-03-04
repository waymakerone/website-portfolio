# Portfolio & Creative

A visually-driven portfolio for designers, photographers, artists, and creative professionals.

## Build Method

This blueprint supports two build paths:

| Path | Tool | How |
|------|------|-----|
| **IDE** | Claude Code, Cursor, Codex | Clone the template, follow the build prompt, deploy via `waymaker push` or Host |
| **Conversational** | Claude Desktop, Host Direct | Describe your business, AI builds + deploys via MCP `host_app_upload` |

Both paths produce the same output. The build prompt detects your environment and guides you accordingly.

## Documentation

| Folder | Contents |
|--------|----------|
| `docs/01-planning/product-requirements/` | PRD — sections, design spec, content requirements |
| `docs/02-working/prompts/active/` | Build prompt with YAML front matter |
| `docs/02-working/sessions/` | Session briefs as you build |
| `docs/03-knowledge/` | Patterns discovered during the build |

## Build Phases

| Phase | Prompt | Status |
|-------|--------|--------|
| 1 — Build Website | `docs/02-working/prompts/active/phase-1-build-website.md` | todo |

## Sections Quick Reference

| ID | Name | Purpose |
|----|------|---------|
| hero | Hero/Introduction | Name, creative discipline, and one striking visual |
| work | Work/Projects Grid | Visual grid of 6-12 projects showcasing range and quality |
| about | About | Background, creative philosophy, notable clients |
| process | Process | How you work — discovery through delivery |
| contact | Contact | Email, social links, and availability status |

## Design Tokens

| Token | Value |
|-------|-------|
| Primary | Black / white |
| Background | White or dark (dark mode option) |
| Accent | One accent colour |
| Headings | Space Grotesk / Syne / Outfit |
| Body | Clean sans-serif |
| Mood | Confident, minimal, visually-led |

## Critical Rules

- Mobile-first responsive design
- Semantic HTML (`nav`, `main`, `section`, `footer`)
- Performance: compress images, lazy load, minimal JS
- Accessibility: proper heading hierarchy, alt text, colour contrast
- SEO: meta tags, structured data, semantic markup
- Single-page layout with smooth scroll navigation
- The work IS the design — minimal UI, large images, generous whitespace
- Dark mode option for photographers and visual designers

## How to Build

1. Read the PRD: `docs/01-planning/product-requirements/website-portfolio-prd.md`
2. Open the build prompt: `docs/02-working/prompts/active/phase-1-build-website.md`
3. Follow the instructions for your build path (IDE or Conversational)
4. Update the YAML `status` field as you go: `todo` -> `in-progress` -> `review` -> `done`

## Quick Reference

| What | How |
|------|-----|
| Dev server | Open `index.html` in browser (IDE path) |
| Deploy | `waymaker push` or MCP `host_app_upload` |
| Design spec | See PRD — Design Specification section |
| Content needed | See PRD — Content Requirements section |
