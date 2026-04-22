# Lulo Card Web

## Project Overview

Lulo Card is a fintech credit card brand with a Colombian lulo fruit identity. This repo is the marketing landing page — a single-page static site with no build step or framework dependencies.

## Architecture

The entire site lives in `index.html`. There is no build tool, bundler, or framework. Styling and JavaScript are inline in the HTML file. The site uses Google Fonts (Montserrat) as its only external dependency.

### File Structure

- `index.html` — The full site (nav, hero, about, features, how-it-works, stats, contact, register, footer)
- `lulo-logo.png` — Brand logo (lulo fruit cross-section)
- `.github/workflows/deploy.yml` — GitHub Pages deployment (auto-deploys on push to main)
- `test.html`, `webpage.html` — Legacy files, not in use

## Design System

All colors are CSS custom properties in `:root`, extracted from the lulo fruit logo. Use these variables for any new UI work — do not hardcode hex values.

### Color Palette

- `--green-dark: #1B3A1A` — Primary dark (nav, hero backgrounds, footer)
- `--green-mid: #2D6B1E` — Mid green (gradients, buttons)
- `--green-accent: #3D7A2A` — Accent green (labels, focus states)
- `--green-light: #E8F5E3` — Light green (icon backgrounds)
- `--orange: #E8941A` — Primary accent (CTAs, gradients)
- `--yellow: #F5C842` — Secondary accent (highlights, gradients)
- `--cream: #FEFDF5` — Page background
- `--white: #FFFFFF` — Card/section backgrounds

### Typography

Montserrat from Google Fonts, weights 400-800. Hero text uses `clamp()` for fluid responsive sizing.

### Animation Patterns

- Scroll-triggered fade-up animations via `IntersectionObserver` with staggered `.delay-1` through `.delay-5` classes
- Floating hero logo (`@keyframes float`)
- Shimmer gradient text on hero headline
- Icon wiggle on feature card hover
- 3D perspective tilt on card mockup hover
- Pulse animation on primary CTA
- Confetti burst on form submission success (Web Animations API)

### Section Layout Convention

Sections alternate between light and dark backgrounds: cream → white → cream → dark green (stats) → cream → white → dark green (footer). New sections should follow this rhythm.

## Forms

Both Contact and Register forms have client-side validation with inline error messages and success states with confetti animations. Currently data logs to `console.log()` only — no backend or form service is connected.

To connect forms to a real backend, update the form submit handlers in the `<script>` block at the bottom of `index.html`. Replace the `console.log` + success display with a `fetch()` call to your endpoint.

## Deployment

- Hosted on GitHub Pages at https://alworks.github.io/lulocard_web/
- Auto-deploys on every push to `main` via `.github/workflows/deploy.yml`
- No build step — the workflow uploads the repo root directly as a Pages artifact

## Next Steps

- Connect forms to a backend or form service (Formspree, Supabase, custom API)
- Add custom domain support
- Clean up legacy files (test.html, webpage.html)
- Consider adding a privacy policy and terms of service page
