# AGENTS.md - Permanent Rules & Guidelines for Master Website Template

This document defines the permanent engineering, architectural, and operational rules for any AI agent or human engineer working with or duplicating this Master Website Template.

---

## 1. Core Principles & Philosophy
1. **Master Template Integrity**: This repository is a reusable foundation for producing high-converting, performant, static/SSG client websites. Do NOT hardcode client-specific one-off logic into core components.
2. **French-First Architecture**: All content strings, schema defaults, date formats, legal templates, and SEO structures must be in proper French by default.
3. **No Unnecessary Dependencies**: Keep the bundle minimal and hyper-fast. Do NOT add heavy animation libraries (e.g., GSAP/Three.js) or bloated state management unless explicitly required.
4. **Single Source of Truth (`src/config/site.ts`)**: Every business detail (names, coordinates, phone numbers, opening hours, SIRET, testimonials, services, and color accents) MUST reside in `src/config/site.ts`.

---

## 2. Architecture & Tech Stack Rules
- **Framework**: Next.js (App Router) + TypeScript + Tailwind CSS
- **Icons**: `lucide-react` only.
- **Styling**: Tailwind CSS utility classes with CSS variables defined in `src/app/globals.css`.
- **Export Compatibility**: Every component and page must build cleanly in both `output: 'export'` (100% static HTML) and `output: 'standalone'` (Docker / Node server).
- **No Client State Bloat**: Use Server Components by default. Add `'use client'` only where user interactivity is strictly required (e.g., FAQ accordion toggle, mobile navigation drawer, form submission).

---

## 3. SEO & Structured Data Rules
- **Dynamic Metadata**: Every page must implement `generatePageMetadata()` from `@/lib/seo`.
- **JSON-LD Schema**: The root layout embeds `SchemaOrg.tsx`, which injects `LocalBusiness`, `Organization`, and `FAQPage` schemas.
- **Sitemap & Robots**: Next.js route handlers `sitemap.ts` and `robots.ts` dynamically read `siteConfig.url`.

---

## 4. Image Workflow Rules
- Place all static client images in `public/images/`:
  - `public/images/clients/`: Client logos, client badges, partner emblems.
  - `public/images/projects/`: Realization showcase images, photo galleries.
  - `public/images/optimized/`: WebP / AVIF compressed images.
- Use Next.js `<Image />` or semantic `<img>` tags with explicit `alt` text.

---

## 5. Deployment Rules
Support 4 target environments seamlessly:
1. **Hostinger VPS without Coolify**: Static build via `NEXT_OUTPUT=export npm run build` served through NGINX (`nginx.conf`).
2. **Coolify**: Standard deployment using the included multi-stage `Dockerfile`.
3. **Netlify**: Deploy static `/out` or Next.js runtime plugin.
4. **Vercel**: Zero-config deployment with native App Router support.

---

## 6. System Reorganization, Anti-AI & Workflow References
- **Master Plan & Architecture**: Always consult [`ProjectInfo/[PLAN]_SYSTEM_REORGANIZATION_AND_WORKFLOW.md`](file:///data/data/com.termux/files/home/website-template/ProjectInfo/%5BPLAN%5D_SYSTEM_REORGANIZATION_AND_WORKFLOW.md)
- **Anti-AI Design & Copywriting Guide**: Follow [`ProjectInfo/SpecialGuides/[GUIDE]_AVOIDING_AI_LOOK_AND_FEEL.md`](file:///data/data/com.termux/files/home/website-template/ProjectInfo/SpecialGuides/%5BGUIDE%5D_AVOIDING_AI_LOOK_AND_FEEL.md)
- **Projects Registry**: Keep [`ProjectInfo/PROJECTS_INDEX.md`](file:///data/data/com.termux/files/home/website-template/ProjectInfo/PROJECTS_INDEX.md) up to date.
- **Client Onboarding**: Use `new-client` command in Termux. Never start coding without proposing the Visual Foundation to the USER first.

---

## 7. Critical UI/UX Rules Learned & Anti-Repetitive Design Mandate
1. **Zero Blind Structural Copy-Paste (Anti-Repetitive Mandate)**:
   - **DO NOT blindly reuse the same layout, same generic hero split, or same header top-bar**.
   - Always rethink the structure from the client's actual business model (e.g. Catalog/Mixology Directory for bulk fragrances, Visual Portfolio for interior architects, Size-Scales for wholesale, etc.).
   - Header must be tailored (e.g. Floating Glass Pill, Minimalist Luxury, Modern Nav) rather than always stamping a generic address/phone bar on top.
2. **Harmonious Palette Extraction**: Always extract real colors directly from client logos and social media banners (exact gold hues, brand undertones, genuine contrast).
3. **White Product Backgrounds**: Any product photo container with a white source background MUST be `#FFFFFF` pure (`bg-white`) without harsh borders to blend seamlessly.
4. **Drawer Overlay Rule**: All navigation & cart drawers must be rendered at the root level with `!z-[999999]`, slide in from the **right side**, and lock background scroll.
5. **Multi-Page Architecture for E-commerce**: Large e-commerce stores must be structured across distinct pages (`/`, `/boutique`, `/a-propos`, `/livraison-faq`, `/contact`).
6. **No Raw Markdown in JSX**: Always use semantic HTML (`<strong>`, `<span>`) for bold and highlighted texts in code.
7. **Automatic GitHub Repo Creation & Push (Every Project & Template)**:
   - Always create the GitHub repository (`Weshmorayy/<project>-website`) and push the code automatically upon project completion.
   - Also commit and push any improvements to `~/website-template` (`Weshmorayy/glow-and-shine-website` or `Weshmorayy/website-template`).
   - Never wait for user prompt to push.
8. **Always Confirm Push & Vercel-Ready**: Always clearly state in final reports that the repository has been pushed to GitHub with its clickable URL and is 100% Vercel-ready.


