# Lulo Card Web

## Project Overview

Lulo Card is a fintech credit card brand with a Colombian lulo fruit identity. This repo is the marketing landing page — a single-page static site with no build step or framework dependencies.

## Architecture

The entire site lives in `index.html`. There is no build tool, bundler, or framework. Styling and JavaScript are inline in the HTML file. The site uses Google Fonts (Montserrat) as its only external dependency.

### File Structure

- `index.html` — The full site (nav, hero, about, features, how-it-works, stats, contact, register, footer)
- `lulo-logo.png` — Brand logo (lulo fruit cross-section), also used as favicon
- `.github/workflows/deploy.yml` — GitHub Pages deployment (auto-deploys on push to main)

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

## Internationalization (i18n)

The site supports 6 languages: English, Spanish, French, Korean, Turkish, and Japanese. The system works as follows:

### How it works

All translatable text elements have `data-i18n` attributes with dot-notation keys (e.g. `data-i18n="hero.title"`). Placeholder text uses `data-i18n-ph`. Elements containing HTML (like the hero title with its `<span>`) use `data-i18n-html="true"` to allow innerHTML replacement.

The translations live in a single `T` object in the `<script>` block, keyed by language code (`en`, `es`, `fr`, `ko`, `tr`, `ja`). The `applyLang()` function iterates all `[data-i18n]` and `[data-i18n-ph]` elements and swaps their content.

### Language detection

1. Checks `localStorage` for a saved preference (`lulo-lang` key)
2. Falls back to `navigator.language` (browser setting)
3. Defaults to English if no match

### Adding a new language

1. Add a new key to the `T` object (e.g. `T.pt = { ... }`) with all the same keys as `T.en`
2. Add a new `<option>` to the `#langSwitcher` select element in the nav
3. That's it — the engine handles the rest

### Adding new translatable content

When adding new sections or text, add `data-i18n="section.key"` to the element, then add the corresponding key to every language in the `T` object.

### Language switcher

A dropdown in the nav bar (visible on desktop and mobile) lets users manually switch languages. The choice is persisted in `localStorage`.

## Forms

Both Contact and Register forms have client-side validation with inline error messages and success states with confetti animations. Currently data logs to `console.log()` only — no backend or form service is connected. All form labels, placeholders, error messages, and success messages are fully translated.

To connect forms to a real backend, update the form submit handlers in the `<script>` block at the bottom of `index.html`. Replace the `console.log` + success display with a `fetch()` call to your endpoint.

## Deployment

- Hosted on GitHub Pages at https://alworks.github.io/lulocard_web/
- Auto-deploys on every push to `main` via `.github/workflows/deploy.yml`
- No build step — the workflow uploads the repo root directly as a Pages artifact

## Next Steps

- Connect forms to a backend or form service (Formspree, Supabase, custom API)
- Add custom domain support
- Create dedicated privacy policy and terms of service pages (footer links currently point to #contact as interim)
- Add more languages if needed (see i18n section above)
