# Sujit Bhandari — Portfolio

A fast, responsive, single-page developer portfolio built with vanilla HTML, CSS, and
JavaScript (no build step). Features a dark/light theme, scroll-reveal animations,
a terminal-style hero, a dedicated **Publications & Patents** section, and a fully
responsive layout.

## Project structure

```
portfolio-webst/
├── index.html              # Page markup / all content
├── styles.css              # Styles + theming + dev-themed UI + responsive rules
├── script.js               # Nav, theme toggle, scroll reveal
├── resume.pdf              # Downloadable résumé (linked from nav + hero + contact)
├── CNAME                   # Custom domain for GitHub Pages
├── .nojekyll               # Disables Jekyll processing on Pages
└── .github/workflows/
    └── deploy.yml          # GitHub Actions deploy workflow
```