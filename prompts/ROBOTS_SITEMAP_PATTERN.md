# Robots.txt and Sitemap Pattern

This document captures the `robots.txt` and sitemap implementation currently used in this project, along with a reusable prompt for recreating the same setup in another Next.js App Router codebase.

## Current Implementation

The project uses Next.js App Router route handlers and metadata routes for SEO crawl control:

- `src/app/robots.ts`
- `src/app/sitemap.xml/route.ts`
- `src/app/page.xml/route.ts`
- `src/app/collections.xml/route.ts`
- `src/apis/sitemapApis.ts`
- `src/constant.ts`

### 1. `robots.txt`

`src/app/robots.ts` exports a `MetadataRoute.Robots` object.

Behavior:

- Allows all crawlers on `/`
- Disallows framework internals and backend/admin paths:
  - `/_next/static/`
  - `/_next/image/`
  - `/_next/server/`
  - `/_next/data/`
  - `/api/`
  - `/Icons/`
  - `/wp-content/`
  - `/wp-admin/`
- Declares sitemap location as `${SITE_URL}/sitemap.xml`

The base site URL comes from `SITE_URL` in `src/constant.ts`, which is derived from `NEXT_PUBLIC_PROJECT_ENV`.

### 2. Sitemap Index

`src/app/sitemap.xml/route.ts` returns a sitemap index XML response.

Behavior:

- Uses `export const dynamic = "force-dynamic"`
- Builds the index at `/sitemap.xml`
- Includes:
  - `${baseUrl}/page.xml`
  - `${baseUrl}/collections.xml`
- Sets `<lastmod>` to `new Date().toISOString()` at request time
- Resolves the base URL from `SITE_URL`, falling back to `new URL(request.url).origin`

### 3. Main Page Sitemap

`src/app/page.xml/route.ts` generates the primary content sitemap.

Behavior:

- Uses `export const dynamic = "force-dynamic"`
- Fetches three CMS datasets in parallel:
  - collections
  - founders
  - static pages
- Emits `<url>` nodes for:
  - home page
  - hardcoded static routes
  - CMS-driven static pages
  - collection pages
  - founder pages

Current hardcoded static routes:

- `/our-collections`
- `/about-us`
- `/csr`
- `/upcoming-events`
- `/become-a-distributor`
- `/contact-us`

Current SEO metadata in XML:

- Home: priority `1.0`, changefreq `daily`
- Hardcoded static pages: priority `0.8`, changefreq `monthly`
- CMS static pages: priority `0.5`, changefreq `monthly`
- Collections: priority `0.8`, changefreq `weekly`
- Founders: priority `0.7`, changefreq `monthly`

### 4. Sub-Collection Sitemap

`src/app/collections.xml/route.ts` generates a second sitemap for sub-collection pages.

Behavior:

- Uses `export const dynamic = "force-dynamic"`
- Fetches `SubCollectionPageSitemapApi` with `cache: "no-store"`
- Emits URLs in the form:
  - `${baseUrl}/our-collections/${Slug}`
- Adds `<lastmod>` from the CMS `updatedAt` field

### 5. CMS Endpoints Used

`src/apis/sitemapApis.ts` centralizes the CMS endpoints:

- `CollectionPageSitemapApi`
- `SubCollectionPageSitemapApi`
- `FounderPageSitemapApi`
- `StaticPageSitemapApi`

The pattern is:

- request only the fields needed for sitemap generation
- currently `Slug` and `updatedAt`

### 6. Environment Dependency

The implementation depends on `src/constant.ts`.

Relevant values:

- `SITE_URL`
- `API_URL`
- `NEXT_PUBLIC_PROJECT_ENV`

This project currently derives `SITE_URL` and `API_URL` from environment mode instead of reading the final values directly from `NEXT_PUBLIC_SITE_URL` and `NEXT_PUBLIC_API_URL`.

## Flow Summary

1. Search engines request `/robots.txt`
2. `robots.ts` points them to `/sitemap.xml`
3. `/sitemap.xml` returns a sitemap index
4. The index points to:
   - `/page.xml`
   - `/collections.xml`
5. Those endpoints fetch CMS data and return XML URL sets

## Recreate This Pattern in Another Project

Use this when recreating the same behavior:

1. Add `app/robots.ts` using `MetadataRoute.Robots`
2. Add `app/sitemap.xml/route.ts` as the sitemap index
3. Add one or more XML route handlers for each sitemap segment
4. Centralize sitemap API URLs in one module
5. Build XML manually with:
   - `<urlset>`
   - `<sitemapindex>`
   - `<loc>`
   - `<lastmod>`
   - optional `<changefreq>`
   - optional `<priority>`
6. Use a single source of truth for the site base URL
7. Fetch only the fields required for sitemap generation

## Important Project-Specific Issues To Verify Before Reuse

This section describes the current implementation as it exists, including inconsistencies that should be checked if you copy the pattern.

### Route naming mismatches

- The app route for collection pages is `src/app/our-collections/[collection]/page.tsx`
- But `src/app/page.xml/route.ts` currently emits collection URLs under `/collections/${item.Slug}`

- The app route for founder pages is `src/app/founder/[slug]/page.tsx`
- But `src/app/page.xml/route.ts` currently emits founder URLs under `/founders/${item.Slug}`

### Static page API string looks incorrect

`StaticPageSitemapApi` is currently:

```ts
`${API_URL}/api/static-pages,updatedAt`;
```

That looks like a typo and likely should be reviewed before reuse.

### Naming mismatch in README

The README mentions `/our-collections.xml`, while the implemented route file is `src/app/collections.xml/route.ts`, which maps to `/collections.xml`.

## Recommended Cleanup If You Reuse It

If you want the same architecture but cleaner behavior, use these adjustments:

- Align sitemap URLs to actual frontend routes
- Fix the static page API endpoint
- Prefer environment variables like `NEXT_PUBLIC_SITE_URL` and `API_URL` as the direct source of truth
- Consider a single reusable XML builder helper
- Add XML escaping if any slug or URL segment can contain special characters
- Decide whether `force-dynamic` is required everywhere or whether timed revalidation is enough

## Reusable Prompt

Use the prompt below in another project.

```text
Inspect this Next.js App Router project and implement the same robots.txt and sitemap pattern used in the ORO frontend.

Requirements:

1. Create a `robots.txt` implementation using `app/robots.ts` and `MetadataRoute.Robots`.
2. Allow `/` and disallow framework/internal paths like `/_next/static/`, `/_next/image/`, `/_next/server/`, `/_next/data/`, `/api/`, and any admin/CMS-only paths if present.
3. Point the robots config to `${SITE_URL}/sitemap.xml`.
4. Create a sitemap index route at `app/sitemap.xml/route.ts`.
5. The sitemap index should return XML with `<sitemapindex>` and reference at least two sitemap segments if the project has multiple content groups.
6. Create XML route handlers for the sitemap segments, similar to:
   - one sitemap for static pages and primary CMS pages
   - one sitemap for collection/detail pages or another large content group
7. Build the XML manually in the route handlers and return `Content-Type: text/xml`.
8. Use a shared site base URL constant or environment variable with a request-origin fallback.
9. Fetch sitemap data from the project’s CMS/API layer using centralized endpoint definitions.
10. Only request the fields needed for the sitemap, ideally slug and updated timestamp.
11. Include `<lastmod>` everywhere possible, and add `<changefreq>` and `<priority>` where useful.
12. Use `export const dynamic = "force-dynamic"` if the current project pattern relies on fully dynamic sitemap generation; otherwise use the project’s existing caching/revalidation strategy.
13. Match sitemap URLs to the actual frontend routes exactly.
14. Add a short markdown doc in `docs/` explaining:
    - which files implement robots and sitemap
    - which routes are generated
    - which API sources are used
    - which environment variables/base URL values are required
15. If you find route or endpoint mismatches, fix them instead of reproducing broken paths.

Before editing, inspect the current routing structure and API modules so the sitemap URLs reflect the real pages in the project.
```

## Short Prompt Version

```text
Create the robots.txt and sitemap setup for this Next.js App Router project using the ORO pattern: `app/robots.ts`, `app/sitemap.xml/route.ts`, segmented XML sitemaps, centralized sitemap API endpoints, `text/xml` responses, and a shared `SITE_URL`. Make the sitemap URLs match the real routes, include `lastmod`, and add a doc in `docs/` explaining the implementation.
```
