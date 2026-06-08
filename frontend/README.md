# AB Texel Wiki - Frontend Implementation

This folder contains the frontend skeleton and build instructions for the AB Texel Wiki website.

## Quick Links

- **Build Instructions:** [INSTRUCTIONS.md](INSTRUCTIONS.md) (Start here!)
- **Content Source:** [../content/](../content/) (All wiki content)
- **Navigation Config:** [../docs-config.json](../docs-config.json) (Use for building sidebar)
- **Main README:** [../README.md](../README.md) (Project overview)

## What to Build

Your task is to create a web application that:

1. **Reads** markdown files from `../content/`
2. **Parses** the navigation structure from `../docs-config.json`
3. **Renders** a wiki website with:
   - Sidebar navigation (hierarchical)
   - Content display area
   - Breadcrumb navigation
   - Internal linking between pages
   - Search functionality (optional)

## Folder Structure

```
frontend/
├── components/           # Create your UI components here
│   ├── NavigationSidebar.tsx
│   ├── ContentRenderer.tsx
│   ├── Breadcrumb.tsx
│   ├── SearchBar.tsx (optional)
│   └── Footer.tsx
├── config/              # Configuration and helpers
│   ├── navigationConfig.ts
│   └── siteConfig.ts
├── utils/               # Utility functions
│   ├── markdownParser.ts
│   └── navigationHelper.ts
├── INSTRUCTIONS.md      # Complete implementation guide
└── README.md           # This file
```

## Getting Started

1. **Read INSTRUCTIONS.md** - Complete step-by-step guide
2. **Choose your tech stack** - Recommended: Next.js, Astro, or Vue/Nuxt
3. **Set up the project** - Initialize with your chosen framework
4. **Build components** - Start with sidebar, then content renderer
5. **Generate pages** - Build routes/pages from docs-config.json
6. **Test locally** - Preview with sample content
7. **Deploy** - Push to your hosting platform

## Key Concepts

### Content Format

All content is markdown with YAML frontmatter:
```markdown
---
title: "Page Title"
description: "Description"
breadcrumb: ["Parent Page"]
---

# Page Title

Content here...
```

### Navigation Structure

Hierarchical navigation defined in `docs-config.json`:
- Parent pages can have children
- Children are nested in `children` array
- Use for building collapsible sidebar menu

### Routing

Map markdown file paths to app routes:
- `content/00-overview.md` → `/` or `/docs/`
- `content/01-reporting-process.md` → `/reporting-process/` or `/docs/reporting-process/`
- `content/reports/01-financial-operations.md` → `/reports/financial-operations/`

## Tech Stack Recommendations

| Option | Best For | Complexity | Performance |
|--------|----------|-----------|-------------|
| **Next.js** | Scaling, SSG support | Medium | Excellent |
| **Astro** | Static content, minimal JS | Low | Outstanding |
| **Vue/Nuxt** | Alternative to React | Medium | Good |
| **Static HTML** | Maximum simplicity | Low | Excellent |

See INSTRUCTIONS.md for detailed examples for each stack.

## Questions?

- **Implementation Details:** See [INSTRUCTIONS.md](INSTRUCTIONS.md)
- **Content Questions:** Contact Data Team
- **Project Context:** See [../README.md](../README.md)

---

**Ready to start?** Open [INSTRUCTIONS.md](INSTRUCTIONS.md) now!
