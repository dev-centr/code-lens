# code-lens GitHub Pages demo

Marketing + live demo site for [code-lens](https://github.com/dev-centr/code-lens), deployed to GitHub Pages via [`.github/workflows/pages.yml`](../.github/workflows/pages.yml).

**Stack:** [SolidJS](https://www.solidjs.com) · [solid-ui](https://www.solid-ui.com) (Kobalte + Tailwind) · `@code-lens/solid` · `@code-lens/vanilla` · [Vite](https://vite.dev) `^6.4.5`

## Develop locally

From the repo root:

```bash
pnpm install
pnpm dev
```

Opens Vite on port **5174** (see [`vite.config.ts`](vite.config.ts) — `server.port` only; no `server.host`, so the dev server is not network-exposed by default). The demo loads spec JSON5 from `../spec/` and renders the live `<code-lens>` block through the Solid wrapper.

If you run Vite with `--host` or set `server.host` so others on your LAN can reach the dev server, keep Vite at **6.4.5+** so denied paths cannot be read via loader query tricks ([GHSA-8g5g-mxqh-grgj](https://github.com/vitejs/vite/security/advisories/GHSA-8g5g-mxqh-grgj)). That advisory applies to dev mode only; the static `demo/dist/` bundle deployed to GitHub Pages is not affected.

## Build

```bash
pnpm --filter @code-lens/core build
pnpm --filter @code-lens/vanilla build
pnpm --filter @code-lens/demo build
```

Output: `demo/dist/` (uploaded by CI).

## solid-ui components

UI primitives live under `src/components/ui/` — copied from the [solid-ui](https://github.com/stefan-karger/solid-ui) registry (same copy-paste model as shadcn/ui). Config: `ui.config.json`.

To add more components (when the CLI works in your environment):

```bash
cd demo
pnpm dlx solidui-cli@latest add dialog tabs
```

## GitHub Pages URL

Published from [`dev-centr/code-lens`](https://github.com/dev-centr/code-lens) on the default branch, the live demo is at **[dev-centr.github.io/code-lens](https://dev-centr.github.io/code-lens/)** (CI: [`.github/workflows/pages.yml`](../.github/workflows/pages.yml)).

`vite.config.ts` uses `base: "./"` so asset paths work under a subdirectory.
