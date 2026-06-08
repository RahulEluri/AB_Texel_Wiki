# AB Texel Wiki Repository

Welcome to the AB Texel Wiki repository! This is a comprehensive documentation system for AB Texel's reporting infrastructure, data sources, and available reports.

## Repository Structure

This repository is organized into two main parts:

### 1. Content Folder (`content/`)

All wiki content is stored as markdown files organized hierarchically:

```
content/
├── _TEMPLATE.md              # Template for new pages
├── 00-overview.md            # Main overview page
├── 01-reporting-process.md   # Reporting workflow
├── 02-data-sources.md        # Data refresh schedules
├── 03-access-permissions.md  # User roles and access
├── 06-system-integration.md  # CBS & BigMile integration
├── 07-glossary.md            # Terminology definitions
├── 08-requesting-changes.md  # How to request changes
├── 09-faqs.md                # Frequently asked questions
├── 10-contact-support.md     # Support contacts
├── reports/                  # Power BI reports sub-section
│   ├── 00-reports-overview.md
│   ├── 01-financial-operations.md
│   ├── 02-fleet-hours.md
│   ├── 03-customer-reporting.md
│   ├── 04-fuel-reporting.md
│   ├── 05-anomaly-reporting.md
│   └── 06-how-to-use.md
└── client-reporting/         # Excel reporting sub-section
    └── 00-client-reporting.md
```

### 2. Frontend Folder (`frontend/`)

The frontend folder contains the skeleton structure for developers to build the wiki website:

```
frontend/
├── components/               # UI component stubs
├── config/                   # Configuration files
├── utils/                    # Utility functions
└── INSTRUCTIONS.md          # Detailed build instructions for developers
```

## Quick Start

### For Content Contributors

1. **Edit existing pages:** Modify markdown files in `content/`
2. **Create new pages:** 
   - Copy `content/_TEMPLATE.md`
   - Update frontmatter (title, description, order, breadcrumb)
   - Add your content
   - Update `docs-config.json` with new page metadata

3. **Naming Convention:** Use numbered prefixes (00, 01, 02) for automatic sorting
4. **Frontmatter:** Every markdown file must include YAML frontmatter:
   ```yaml
   ---
   title: "Page Title"
   description: "Brief description"
   category: "Category Name"
   order: 1
   breadcrumb: []
   ---
   ```

### For Frontend Developers

1. **Read:** [frontend/INSTRUCTIONS.md](frontend/INSTRUCTIONS.md) for detailed build guide
2. **Key Steps:**
   - Parse `docs-config.json` for navigation structure
   - Read markdown files from paths in `content/`
   - Build UI components (sidebar, content renderer, breadcrumbs)
   - Generate static site or dynamic routes
   - Deploy to hosting platform

3. **Recommended Tech Stacks:**
   - **Next.js** (easiest, best for scaling)
   - **Astro** (best performance for static content)
   - **Vue/Nuxt** (good alternative to React)
   - **Static HTML** (simplest approach)

## Key Files

| File | Purpose |
|------|---------|
| `docs-config.json` | Navigation structure and page metadata (use this to build sidebar) |
| `content/_TEMPLATE.md` | Template for creating new pages |
| `content/00-overview.md` | Main landing page of the wiki |
| `frontend/INSTRUCTIONS.md` | Complete guide for frontend implementation |
| `.gitignore` | Git ignore rules for build artifacts |

## Navigation Structure

The wiki has a **mixed hierarchical structure**:

- **Main pages** (9 pages at root level, numbered 00-10)
- **Reports section** (1 parent page with 6 child pages)
- **Client Reporting section** (1 parent page with 1 child page)

Example navigation tree:
```
Overview
Reporting Process & Ownership
Data Sources & Refresh Schedule
Access & Permissions
Reports (Parent)
  ├─ Financial Operations
  ├─ Fleet Hours
  ├─ Customer Reporting
  ├─ Fuel Reporting
  ├─ Anomaly Reporting
  └─ How to Use?
Client Reporting (Parent)
  └─ Excel
System Integration
Glossary
Requesting Changes
FAQs
Contact & Support
```

## Working with Markdown Content

### File Format

Each markdown file has:
1. **Frontmatter** (YAML metadata at top)
2. **Title heading** (# Page Title)
3. **Content sections** (with ## subheadings)
4. **Links** (relative paths to other markdown files)

Example:
```markdown
---
title: "My Page"
description: "What this page is about"
category: "Main"
order: 5
breadcrumb: ["Parent Page"]
---

# My Page

## Section 1

Content here...

## Section 2

See [Related Page](../path/to/file.md) for more info.
```

### Linking Between Pages

Use relative markdown links. They'll be converted to routes by the frontend:
- Same folder: `[Link](./other-page.md)`
- Parent folder: `[Link](../other-page.md)`
- Sub-folder: `[Link](subfolder/other-page.md)`

### Adding Images

1. Create an `assets/` folder (optional)
2. Add images there
3. Link in markdown: `![Alt text](../assets/image.png)`

## Navigation Config (docs-config.json)

The `docs-config.json` file maps the complete navigation structure. **Important:** When adding new pages:

1. Create the markdown file in `content/`
2. Add entry to `docs-config.json` navigation array
3. Include proper metadata (id, title, path, order, breadcrumb)
4. For hierarchical pages, add `children` array

Example:
```json
{
  "id": "my-page",
  "title": "My Page",
  "path": "content/path/to/my-page.md",
  "order": 5,
  "breadcrumb": ["Parent Page"],
  "children": []
}
```

## Deployment & Hosting

### Recommended Options

1. **Vercel** (Best for Next.js)
   - Free tier available
   - Auto-deploy on push to main branch
   - Excellent performance

2. **GitHub Pages** (Best for static sites)
   - Free
   - Built-in CI/CD
   - Good for Astro projects

3. **Netlify** (Good all-purpose option)
   - Free tier
   - Easy deployment
   - Good build integrations

### Pre-Deployment Checklist

- [ ] All markdown files have proper frontmatter
- [ ] `docs-config.json` includes all pages
- [ ] Internal links use relative paths
- [ ] No broken links (local testing)
- [ ] Images are optimized
- [ ] SEO metadata is complete

## Contributing Guidelines

### Content Standards

- **Tone:** Professional, clear, and helpful
- **Length:** Keep sections concise; break long content into subsections
- **Format:** Use clear headings, bullet points, and tables where appropriate
- **Links:** Internal links should guide readers to related information
- **Updates:** Mark when content was last updated in frontmatter

### Git Workflow

1. Create a feature branch: `git checkout -b add/new-page`
2. Make changes to markdown files
3. Update `docs-config.json` if adding/removing pages
4. Commit with clear message: `git commit -m "Add new page: XYZ"`
5. Push and create pull request
6. Request review from team

### Naming Conventions

- **Files:** Use kebab-case: `my-new-page.md`
- **Folders:** Use kebab-case: `my-section/`
- **IDs:** Use kebab-case in config: `my-page-id`
- **Numbering:** Prefix with 00, 01, 02 for sorting

## Troubleshooting

### Common Issues

**Q: My new page isn't showing in the sidebar**  
A: Check that it's added to `docs-config.json` in the navigation array.

**Q: Links between pages aren't working**  
A: Verify relative paths are correct and frontend converts `.md` to app routes.

**Q: Formatting looks wrong**  
A: Check markdown syntax. Ensure proper spacing around headings and code blocks.

**Q: How do I fix a typo in published content?**  
A: Edit the markdown file, commit, and the frontend will auto-update on next build/deploy.

## Support & Questions

- **Content Questions:** Contact Data Team at support@abtexel.com
- **Frontend Questions:** See [frontend/INSTRUCTIONS.md](frontend/INSTRUCTIONS.md)
- **Git/Workflow Issues:** Contact your repository admin

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2024-06-08 | Initial wiki structure with 13 main pages |

---

**Last Updated:** June 8, 2024  
**Maintainer:** AB Texel Data Team  
**License:** Internal Use Only
