# CLAUDE.md

## What This Is
Immigration law firm website for Pombo, Horowitz & Espinosa (PHE Abogados). Provides information about immigration law services, blog articles, FAQs, and promotes tuspapeles2026.es for Spain's 2026 extraordinary regularization.

## Stack
- HTML/CSS/JS (static, no framework)
- Client-side dynamic content loading via JavaScript
- content.json (single source of truth for articles, FAQs, updates, pricing, stats)
- Google Fonts

## Hosting
- GitHub Pages
- Custom domain: pombohorowitz.es
- Auto-merge workflow: pushes to `claude/**` branches auto-merge to main

## Env Vars
None. All configuration is in content.json.

## Key Files
| File | Purpose |
|------|---------|
| `index.html` | Landing page with dynamic blog preview and FAQs |
| `blog.html` | Full blog listing |
| `content.json` | Dynamic content data |
| `servicios.html` | Services page |
| `contacto.html` | Contact page |
| `sobre-nosotros.html` | About page |
| `.github/workflows/auto-merge.yml` | Auto-merge CI/CD |
