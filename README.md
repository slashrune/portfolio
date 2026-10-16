# Academic portfolio scaffold

A static Astro site with React components and plain CSS. Content and visual design
will be added later.

## Prerequisites and installation

Use Node.js 24 LTS (24.22.0 is recorded in `.nvmrc`) and npm 9.6.5 or newer.
The supported Node ranges are recorded in `package.json`; Astro requires at least
22.22.0. If you use nvm, run `nvm install` followed by `nvm use` in this folder.
This project does not change your global Node installation.

```sh
npm ci
npm run dev
```

Open the local address printed by Astro (normally `http://localhost:4321`). Stop
foreground servers with Ctrl+C. If Astro starts a background server (including
when run by an agent), use `npm run dev -- stop` or `npm run preview -- stop`.
`npm ci` installs the versions in the tracked lockfile;
use `npm install` when intentionally changing dependencies.

## Commands

| Command                | Purpose                                 |
| ---------------------- | --------------------------------------- |
| `npm run dev`          | Start the development server            |
| `npm run format`       | Format source and configuration files   |
| `npm run format:check` | Check formatting without changing files |
| `npm run build`        | Generate the static site in `dist/`     |
| `npm run preview`      | Serve the last production build locally |

Install the recommended Astro and Prettier VS Code extensions for editor support
and formatting on save. Generated files, the lockfile and the original setup
instructions are excluded from formatting.

## Structure

```text
src/
  pages/index.astro          Minimal homepage entry point
  layouts/BaseLayout.astro  HTML shell, metadata and global CSS imports
  components/SetupStatus.jsx Reusable React setup message
  styles/global.css         Minimal reset and document defaults
  styles/tokens.css         Placeholder for future CSS custom properties
  assets/images/            Images to import and process with Astro
  content/projects/         Future Markdown project descriptions
  data/publications.json    Empty publication data array
public/
  files/papers/             Future downloadable paper PDFs
  files/cv/                 Future CV PDFs
  images/                   Images served unchanged
```

Empty directories contain `.gitkeep` placeholders. No content collections or
project routes are configured yet. Files in `src/assets/` can be imported and
optimized using Astro's image tools. Files in `public/` are copied unchanged to
the build and referenced by URL (for example `/files/cv/example.pdf` once added).

Keep pages and layouts thin and reusable interface elements in React `.jsx`
components. React renders to static HTML by default; only add a `client:*`
directive when a component needs browser interaction. The setup message needs
no hydration or client React bundle.

Application code uses JavaScript ES modules, JSX and Astro templates.
`tsconfig.json` extends Astro's JavaScript-friendly `base` template and configures
React JSX for editor/tooling support; it does not require TypeScript application
code. Astro generates type declarations in `.astro/`, and npm installs React type
definitions required by the integration as peer dependencies.

## Future GitHub Pages hosting

`astro.config.mjs` explicitly selects static output. It currently leaves `site`
unset and `base` at its default `/` so local development works without an assumed
hosting address. When the destination is known, configure these in that file:

| Destination               | `site`                        | `base`                              |
| ------------------------- | ----------------------------- | ----------------------------------- |
| User or organization site | `https://<account>.github.io` | `/` (default)                       |
| Repository site           | `https://<account>.github.io` | `/<repository>`                     |
| Custom domain             | `https://<domain>`            | `/` (unless hosted under a subpath) |

For repository hosting, build internal links and public-file URLs using
`import.meta.env.BASE_URL` so they include the configured subpath. Rebuild after
changing hosting settings. Domain/DNS configuration and a deployment workflow
are future tasks; nothing is published by this scaffold.

Setup references: [Astro installation](https://docs.astro.build/en/install-and-setup/),
[React integration](https://docs.astro.build/en/guides/integrations-guide/react/),
[editor and formatting setup](https://docs.astro.build/en/editor-setup/), and
[GitHub Pages configuration](https://docs.astro.build/en/guides/deploy/github/).
