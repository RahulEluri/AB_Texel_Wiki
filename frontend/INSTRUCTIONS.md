# Frontend Build Instructions

This folder is reserved for the frontend implementation. Developers can use this structure to build the wiki website.

## Overview

The `frontend/` folder contains the skeleton structure and suggested organization for building the wiki UI. The actual content comes from the `content/` folder (markdown files).

## Folder Structure

```
frontend/
├── components/          # Reusable UI components
│   ├── NavigationSidebar.tsx
│   ├── ContentRenderer.tsx
│   ├── Breadcrumb.tsx
│   ├── SearchBar.tsx
│   └── Footer.tsx
├── config/             # Configuration files
│   ├── navigationConfig.ts  # Import from ../docs-config.json
│   └── siteConfig.ts
├── utils/              # Utility functions
│   ├── markdownParser.ts    # Markdown to HTML converter
│   └── navigationHelper.ts  # Build navigation tree from config
└── README.md           # Your frontend README
```

## Getting Started for Developers

### Step 1: Understand the Content Structure

All content is in the `../content/` folder as markdown files:
- **Main pages:** `content/00-overview.md`, `content/01-reporting-process.md`, etc.
- **Sub-pages:** `content/reports/*.md`, `content/client-reporting/*.md`
- **Config:** `../docs-config.json` (Navigation structure in JSON)

### Step 2: Parse the Navigation Config

The `docs-config.json` contains:
- All page metadata (title, path, order, breadcrumb)
- Hierarchical structure (parent pages with children)
- Site-wide metadata

Example structure in config:
```json
{
  "navigation": [
    {
      "id": "overview",
      "title": "AB Texel Reporting Overview",
      "path": "content/00-overview.md",
      "order": 0,
      "children": []
    },
    {
      "id": "reports",
      "title": "Reports - Power BI",
      "path": "content/reports/00-reports-overview.md",
      "order": 4,
      "children": [
        {
          "id": "financial-operations",
          "title": "Financial Operations",
          "path": "content/reports/01-financial-operations.md"
        }
        // ... more children
      ]
    }
  ]
}
```

### Step 3: Build Key Components

#### 1. Markdown Parser
- Parse markdown files from `../content/`
- Extract YAML frontmatter (metadata at top of file)
- Convert markdown to HTML for display
- Recommended libraries: `gray-matter` (YAML), `marked` or `remark` (markdown)

#### 2. Navigation Sidebar
- Read `docs-config.json`
- Build hierarchical navigation tree
- Show parent pages with collapsible children
- Highlight current page

#### 3. Content Renderer
- Load markdown file from path
- Parse frontmatter for metadata
- Render markdown as HTML
- Display breadcrumbs from frontmatter

#### 4. Breadcrumb Navigation
- Extract from frontmatter: `breadcrumb: ["Reports", "Financial Operations"]`
- Build clickable breadcrumb trail
- Link to parent pages

### Step 4: Choose Your Tech Stack

**Recommended Options:**

1. **Next.js (React)** - Best for scalability and ease
   - Built-in static generation (SSG) for markdown
   - Easy deployment (Vercel)
   - Good markdown libraries available
   
2. **Vue.js + Nuxt** - Good alternative to Next.js
   - Similar static generation approach
   - Lighter than React if performance matters
   
3. **Astro** - Excellent for static content / wikis
   - Built for markdown-heavy sites
   - Best performance
   - Minimal JavaScript
   
4. **Static HTML + JavaScript** - Simplest approach
   - Build markdown to HTML offline
   - Serve static files
   - Use vanilla JS or lightweight library (Alpine.js, htmx)

### Step 5: Development Workflow

1. **Read config:** Load `docs-config.json` on app start
2. **Build navigation:** Create sidebar from config structure
3. **Generate pages:** For each page in config:
   - Read markdown from path
   - Parse frontmatter and content
   - Render with layout template
4. **Build static site:** Generate HTML files for each page
5. **Deploy:** Push to hosting (Vercel, GitHub Pages, etc.)

## Content File Format

All markdown files use this format:

```markdown
---
title: "Page Title"
description: "Brief description"
category: "Category Name"
order: 1
breadcrumb: []
---

# Page Title

Your content here...
```

**Frontmatter Fields:**
- `title` - Page title (used in browser tab, breadcrumb)
- `description` - Meta description (SEO, page preview)
- `category` - Categorization (for grouping)
- `order` - Sort order within parent
- `breadcrumb` - Array of parent page titles

## Recommended Build Process

1. **On build time:**
   - Load `docs-config.json`
   - Read all markdown files from paths in config
   - Parse frontmatter and content
   - Generate static HTML files or routes
   
2. **On page load (client-side):**
   - Route to correct markdown file based on URL
   - Render breadcrumbs from config
   - Render sidebar navigation
   - Display parsed markdown content

## Key Implementation Tips

1. **Links in Content:** Markdown files contain links like `[Link](../path/to/file.md)` 
   - Convert relative markdown paths to your app routes
   - Pattern: `content/path/file.md` → `/path/file` or `/docs/path/file`

2. **Breadcrumbs:** Use `config.breadcrumb` + current page title
   - Build clickable links to parent pages
   - Add current page as text (not link)

3. **Navigation:**
   - Root level pages: Show in sidebar
   - Child pages: Nest under parent with collapse/expand
   - Current page: Highlight in sidebar

4. **Search (Optional Future Feature):**
   - Index all markdown files on build
   - Search across titles and content
   - Link to results

## Example: Next.js Implementation Outline

```typescript
// pages/[[...slug]].tsx
import { readFileSync } from 'fs'
import { join } from 'path'
import matter from 'gray-matter'
import marked from 'marked'

export async function getStaticPaths() {
  // Build paths from docs-config.json
  const config = JSON.parse(readFileSync(join(process.cwd(), 'docs-config.json'), 'utf-8'))
  const paths = config.navigation.flatMap(buildPaths)
  return { paths, fallback: false }
}

export async function getStaticProps({ params }) {
  // Read markdown file
  const filePath = join(process.cwd(), 'content', params.slug.join('/') + '.md')
  const content = readFileSync(filePath, 'utf-8')
  const { data, content: markdown } = matter(content)
  const html = marked(markdown)
  
  return {
    props: { frontmatter: data, html },
    revalidate: 3600 // ISR: revalidate every hour
  }
}

export default function Page({ frontmatter, html }) {
  return (
    <div>
      <Sidebar />
      <Breadcrumb breadcrumb={frontmatter.breadcrumb} />
      <article dangerouslySetInnerHTML={{ __html: html }} />
    </div>
  )
}
```

## FAQ for Developers

**Q: How do I handle internal links in markdown?**  
A: Markdown files use relative paths like `[link](../path/file.md)`. On build, convert these to app routes:
- Replace `.md` with your route format
- Use path resolver to get correct URL

**Q: Should I regenerate the site when content changes?**  
A: It depends on your tech:
- **Next.js/Astro:** Use ISR (Incremental Static Regeneration) or rebuild on push
- **Static HTML:** Rebuild and deploy on content changes
- **Dynamic:** Load markdown at runtime (slower but flexible)

**Q: How do I handle different screen sizes?**  
A: Standard web practices:
- Responsive sidebar (collapsible on mobile)
- Mobile-friendly markdown rendering
- Touch-friendly navigation

## Next Steps

1. **Choose framework** - Pick your tech stack
2. **Set up project** - Initialize project skeleton
3. **Build components** - Create sidebar, content renderer, breadcrumbs
4. **Create routes** - Build routes from `docs-config.json`
5. **Test locally** - Preview with sample content
6. **Deploy** - Push to hosting platform

---

**Questions?** Contact the Data Team or check the main README.md for project context.
