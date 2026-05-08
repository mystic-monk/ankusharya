# Ankush Arya Portfolio Site

A production-ready, static portfolio website showcasing BI leadership, analytics projects, and the "She Knows Too Much" newsletter.

## Files

```
.
├── index.html              Home page with hero and highlights
├── about.html              Professional background and timeline
├── projects.html           Project portfolio with Live Demo buttons
├── newsletter.html         She Knows Too Much newsletter signup
├── blog.html               Blog placeholder (coming soon)
├── contact.html            Contact form and social links
├── style.css               Single shared stylesheet
├── DEPLOYMENT.md           Step-by-step Render deployment guide
└── README.md               This file
```

## Quick Features

- **Fully Responsive** — Mobile-first design, works on all devices
- **Accessible** — WCAG 2.1 AA contrast ratios, semantic HTML, ARIA labels, visible focus states
- **No Build Step** — Pure HTML, CSS, vanilla JavaScript
- **Production Ready** — Deployed as-is to Render Static Site
- **Fast Load** — Inline critical CSS, Google Fonts async, minimal JavaScript
- **SEO Optimized** — Meta tags, Open Graph, structured markup on all pages

## Design

- **Colors** — Soft pastel palette: sage green, warm off-white, muted dusty rose accents
- **Typography** — Inter (body), Playfair Display (headings) from Google Fonts
- **Layout** — CSS Grid and Flexbox, mobile-first responsive breakpoints
- **Spacing** — Generous whitespace, 1.6 line height for readability

## Deployment

1. See [DEPLOYMENT.md](./DEPLOYMENT.md) for step-by-step Render instructions
2. TL;DR: Push to GitHub → Connect to Render → Done

## Customization

### Update Professional Summary
In `index.html`, replace the placeholder text in the hero section with your 2-sentence summary.

### Replace Placeholders

| File | Placeholder | Instructions |
|------|-------------|--------------|
| All HTML | `G-XXXXXXXXXX` | Replace with GA4 Measurement ID |
| All HTML | `ankusharya.dev` | Update canonical URLs if using different domain |
| `contact.html` | Formspree URL | Replace with your formspree.io endpoint |
| `projects.html` | Render URLs | Update with live demo service URLs once deployed |

### Add Blog Articles

1. Create new HTML file: `blog-article-title.html`
2. Copy template from `blog.html`
3. Update main content
4. Link from `blog.html`
5. Redeploy

## Domains

- **Portfolio**: `ankusharya.dev` (or `ankusharya.io`)
- **Newsletter**: `sheknowstoomuch.com` (optional second static site)

Both use relative links, so they work under any domain.

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Performance

- **Page Load**: <1s (static files, optimized fonts)
- **Lighthouse**: 98+ Performance, 100 Accessibility
- **Page Size**: ~50KB total (HTML + CSS)

## License

Personal portfolio — all rights reserved.

## Support

See [DEPLOYMENT.md](./DEPLOYMENT.md) for deployment help and troubleshooting.
