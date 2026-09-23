# SakuraGirl

An anime search and discovery site, built with React (Vite) and React Router.
Owner: **Mr. Supun Fernando**.

preview:- https://sakuragirl.vercel.app/

## What it does

- Search any anime by title, with results appearing as you type
- Browse "airing this season" and "trending now" rails on the home page
- Open a details page for full synopsis, score, rank, genres, studio, and main cast
- An About page with the site's focus areas (anime / 3D / UI-UX) and social links
- "Watch officially" links on each details page (Crunchyroll / Netflix search, MyAnimeList)
- Automatic fallback to AniList's API if Jikan is rate-limited or briefly down

## What it deliberately does *not* do

This project only reads public, free metadata from **Jikan** (an open, unofficial
MyAnimeList API — see https://docs.api.jikan.moe/). It does not scrape, mirror, host,
stream, or offer downloads of any copyrighted video content from any site. Adding
that kind of feature would mean redistributing anime without authorization from the
rights holders, so it's intentionally left out. If you want a legal watch button,
point it at official platforms (Crunchyroll, official streaming partners, etc.)
instead of hosting files yourself.

## Getting started

Requires [Node.js](https://nodejs.org) 18+.

```bash
npm install
npm run dev
```

Then open the local URL Vite prints (usually http://localhost:5173).

To build a production bundle:

```bash
npm run build
npm run preview
```

The build output lands in `dist/`, which you can deploy to any static host
(Vercel, Netlify, Cloudflare Pages, GitHub Pages, your own server, etc.).

## Project structure

```
sakuragirl/
├── index.html
├── package.json
├── vite.config.js
├── public/
│   └── favicon.svg
└── src/
    ├── main.jsx
    ├── App.jsx
    ├── api/
    │   ├── jikan.js          # Primary source (search, top, season, details, characters)
    │   └── anilist.js        # Fallback source, normalized to the same shape
    ├── components/
    │   ├── Navbar.jsx
    │   ├── Footer.jsx
    │   ├── AnimeCard.jsx
    │   ├── SkeletonGrid.jsx
    │   └── PetalField.jsx
    ├── pages/
    │   ├── Home.jsx
    │   ├── Details.jsx
    │   ├── About.jsx
    │   └── NotFound.jsx
    └── styles/
        └── index.css          # design tokens + all styling
```

## Customizing

- **Branding / colors / fonts**: edit the CSS variables at the top of
  `src/styles/index.css` (`--ink-900`, `--sakura-400`, `--font-display`, etc.).
- **Social links**: edit the `SOCIALS` array in `src/pages/About.jsx` and the
  links in `src/components/Footer.jsx`.
- **API rate limits**: Jikan is free and public but rate-limited (roughly
  3 requests/second, 60/minute). If you expect heavy traffic, consider adding
  simple response caching or your own backend proxy.

## Deploying

Any static host works since this is a client-side Vite app:

- **Vercel / Netlify**: import the repo, build command `npm run build`, output
  directory `dist`.
- **GitHub Pages**: run `npm run build`, then push the contents of `dist/` to
  a `gh-pages` branch (or use an action).
