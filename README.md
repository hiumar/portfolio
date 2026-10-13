# Umar Faraz — Developer Portfolio

A responsive Next.js portfolio featuring .NET full stack development, government and healthcare platforms, fintech, CRM, NopCommerce B2B/B2C commerce, and agentic AI projects.

## Included

- Responsive portfolio, categorized skills, project detail dialogs, career timeline, and printable CV
- Server-side live content loading, with no browser-exposed content-service credential
- `/admin` redirects to the existing owner-only content editor
- Error screen and retry support when the content service is unavailable

## Architecture

This repository is the Vercel frontend. The existing private ChatGPT Site hosts the content database and secure admin editor. Keep that Site active. Changes saved in the admin editor appear on the next portfolio request without rebuilding the Vercel deployment.

Content backend: https://fullstack-developer-portfolio.tealbirch32.chatgpt.site
Admin editor: https://fullstack-developer-portfolio.tealbirch32.chatgpt.site/admin

This is not a standalone backend migration. Authentication, database migrations, and the admin editor implementation remain in the original Site source repository.

## Local development

Requires Node.js 22.

```sh
npm install
cp .env.example .env.local
npm run dev
```

Set `PORTFOLIO_SOURCE_TOKEN` in `.env.local` using the private Site's authorized service-access credential. Never commit the value or prefix it with `NEXT_PUBLIC_`. There is no token in this repository.

## Deploy to Vercel

1. Import `hiumar/portfolio` into the intended Vercel account/team.
2. Choose **Next.js** and keep the repository root as the Root Directory.
3. Add `PORTFOLIO_SOURCE_TOKEN` as a sensitive environment variable for Production and Preview.
4. Deploy with `npm run build` (`next build --webpack`).

The source URL is fixed in `lib/content-store.ts`. Requests reject redirects and use `cache: 'no-store'` so updates are loaded on every page request.

## Checks

```sh
npm run typecheck
npm run build
```

TypeScript checks passed in the authoring environment. A local native Next.js build could not finish there because the restricted runtime could not read a memory-usage metric (`uv_resident_set_memory`). A successful Vercel build still needs verification.
