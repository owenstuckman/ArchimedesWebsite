# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static marketing website for the Archimedes Society at Virginia Tech. Built with SvelteKit 2 and Svelte 5, deployed to Vercel.

## Commands

```bash
npm run dev          # Start Vite dev server
npm run build        # Production build (vite build + svelte-package)
npm run preview      # Preview production build
npm run check        # TypeScript type checking (svelte-check)
npm run check:watch  # Type checking in watch mode
npm run lint         # Prettier check + ESLint
npm run format       # Auto-format with Prettier
```

> Note: `npm run build` runs both `vite build` and `svelte-package` (the latter is a component-library step that is vestigial here). Vercel only needs the `vite build` output; the `prepack` step can be ignored for deployment purposes.

There are no automated tests. `npm run check` is the closest equivalent — it runs `svelte-check` for type errors.

## Architecture

### Routing

File-based routing in `src/routes/`. Each folder with `+page.svelte` is a route. `+layout.svelte` wraps every page with `<Header>` and `<Footer>`, and imports `src/lib/styles/global.css`.

Pages: Home (`/`), About, Design Teams, Apply, FAQ, Sponsor, Contact.

### Components (`src/lib/components/`)

- **Header.svelte**: Sticky nav with hamburger menu below 900px. Uses `$page.url.pathname` to highlight the active link.
- **Footer.svelte**: Multi-column footer with social links.
- **Hero.svelte**: Full-width hero section. Props: `title`, `subtitle`, `image`, `dark`. Accepts a `<slot>` for CTA buttons.
- **TeamCard.svelte**: Design team info card. Props: `name`, `competition`, `description`, `members`, `duration`, `travel`, `link`, `linkText`.

> The layout still uses Svelte 4 `<slot />` syntax (not Svelte 5 `{@render children()}`). Follow the same pattern when editing existing components; new components may use either, but be consistent within a file.

### Styling

- **Tailwind CSS 4** — no `tailwind.config.js`. Configuration is done entirely via CSS: `@import 'tailwindcss'` and `@plugin` directives in `src/app.css`.
- **`src/lib/styles/global.css`** defines all brand CSS variables and utility classes. This is the source of truth for colors, spacing tokens, and shared classes.
- Brand palette: `--archimedes-yellow` (#ffb800), `--archimedes-yellow-bright` (#ffd000), `--steel` (#192b2e, page background), `--halogen-haze` (#fffcf2).
- Shared utility classes: `.section`, `.section--light`, `.section--dark`, `.container`, `.card`, `.btn`, `.btn--primary`, `.btn--outline`, `.overline`.
- Responsive breakpoints: 768px (mobile layout), 900px (desktop nav).
- Scoped component styles use BEM-like naming (`.nav__inner`, `.faq-item`, etc.).
- For per-item accent colors (e.g., team colors on the About page), set a `--tc` CSS custom property via inline `style` on the parent element and reference it in scoped CSS.

### Static Assets

- `static/images/` — hero and general page images.
- `static/members/` — member photo files referenced by the About page (named as listed in `static/members.csv`).
- `static/members.csv` — source of truth for member data used to populate the About page's team cards.

### External Integrations

- **EmailJS**: Contact and sponsor forms POST directly to the EmailJS API. Credentials are in client-side code.
- **Google Forms**: The Apply page links out to an external Google Form.
- No backend or database — all content is hardcoded in page components.

### Key Patterns

- **SSR safety**: Use `if (browser)` from `$app/environment` for any browser-only logic.
- **Content as data**: Page content (teams, FAQs, member lists) is declared as plain JS arrays inside each `+page.svelte` `<script>` block — no CMS or external data fetching.
- **Forms**: Use `event.preventDefault()`, build `FormData`, POST via `fetch`, and use `alert()` for feedback.
- **mdsvex**: Configured in `svelte.config.js`; `.svx` files are supported alongside `.svelte`.

## Code Style

Tabs for indentation, single quotes, no trailing commas, 100-char print width. See `.prettierrc`. Prettier plugins: `prettier-plugin-svelte`, `prettier-plugin-tailwindcss`.
