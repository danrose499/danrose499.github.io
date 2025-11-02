# Daniel Rosenthal — Portfolio

A small, fast, and friendly personal site built with Svelte and Vite. It highlights my journey on a scrollable timeline and showcases a few side projects. Routing is hash-based and minimal by design, the UI stays lightweight, and deploys go out via GitHub Pages.

## Features

- **Timeline view**
- **Projects gallery** with cards, screenshots, and links
- **Simple hash routing** between `#/timeline` and `#/projects`
- **Clean toolbar** with links to LinkedIn and GitHub
- **Lightweight build** with Vite and vanilla CSS

## Tech stack

- **Svelte 5** for components
- **Vite** for dev server and bundling
- **GSAP** for small animations
- **GitHub Pages** for hosting (via `gh-pages`)

## Getting started

Prereqs: Node 18+ and npm.

```bash
npm install
npm run dev
```

Then visit http://localhost:5173.

## Scripts

- `npm run dev` — Start the Vite dev server
- `npm run build` — Create a production build in `dist/`
- `npm run preview` — Preview the production build locally
- `npm run deploy` — Build and publish `dist/` to the `gh-pages` branch

## Project structure

```
my-portfolio/
├─ index.html
├─ src/
│  ├─ main.js
│  ├─ App.svelte
│  ├─ app.css
│  └─ components/
│     ├─ Timeline.svelte
│     ├─ TimelineItem.svelte
│     ├─ Projects.svelte
│     └─ ProjectCard.svelte
├─ vite.config.js
├─ svelte.config.js
├─ package.json
└─ README.md
```

## Routing

This app uses a tiny hash-based approach. The toolbar buttons set `window.location.hash` and the app renders either the timeline or the projects view.

Routes:

- `#/timeline`
- `#/projects`

## Deployment (GitHub Pages)

This is a user site: https://danrose499.github.io/

Recommended setup:

1. Enable Pages: Settings → Pages.
2. Source: GitHub Actions (build from `main`).
3. Use the official "Deploy to GitHub Pages" workflow for static sites (Vite). It will build from source and publish automatically on push to `main`.

Alternative (using the existing script):

1. If you prefer branch deploys, configure Pages to "Deploy from a branch" and select the branch you publish to.
2. Run:

   ```bash
   npm run deploy
   ```

   This builds the site and pushes `dist/` to the configured branch (currently `gh-pages`).

Notes:

- Keep `base: '/'` in `vite.config.js` (already set for a user site).
- Ensure the Pages source matches how you deploy (Actions from `main`, or branch deploy from `gh-pages`).

## Notes

- Images live under `src/assets/` and are imported directly into components.
- Styles are kept simple and local to components; no global CSS frameworks.
- Accessibility basics: semantic headings, focus states, `aria-label`s for icons.

## Contact

- LinkedIn: https://www.linkedin.com/in/daniel--rosenthal/
- GitHub: https://github.com/danrose499

