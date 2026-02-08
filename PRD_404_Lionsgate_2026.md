# Lionsgate.com Next-Generation Experience – PRD
## Prepared by 404 Technologies

## 1. Overview

Lionsgate.com will be redesigned into a cinematic, high-performance, and extensible platform that showcases Lionsgate's movies, TV shows, games, experiences, channels, and podcasts in a unified, modern experience, while driving conversions to tickets, streaming, and owned channels.

## 2. Objectives & KPIs

- Increase click-through to ticketing/streaming partners from homepage and title pages by 15–30% within 6 months of launch.
- Increase email signups for "Lionsgate Insider" by 20% via better placement, copy, and UX.
- Improve Lighthouse performance scores to 90+ on mobile and desktop for key pages (home, movies index, title pages).
- Reduce bounce rate from homepage and key campaign landers by 10–20%.
- Establish a flexible content and design system that allows marketing to launch new campaigns and titles without dev involvement.

## 3. Target Users

- Entertainment fans discovering or revisiting Lionsgate movies, TV shows, games, and experiences.
- Visitors coming from trailers, ads, or search who want trailers, synopsis, cast, and where-to-watch info.
- Corporate visitors (press, investors, partners, job seekers) seeking About, Inclusion, Investor Relations, Careers, Licensing, Legal, and regional sites.

## 4. Current Site Assessment (2026)

### Strengths:
- Strong slate of prominent campaigns on homepage (e.g., Hunger Games 2026, The Strangers, Michael, Greenland 2).
- Clear section links for Movies, TV Shows, Games, Experiences, Channels, Podcasts, Shop, Redeem, Inclusion, Investor Relations, and more.
- Existing news hook (e.g., "Lionsgate Hires First Chief AI Officer") that signals AI-forward brand positioning.

### Pain points:
- Layout and hierarchy feel cluttered, with multiple repeating CTAs ("More Info" blocks) and visually similar modules.
- Navigation taxonomy is slightly inconsistent (TV Shows vs Shows vs Channels), and the footer is link-dense and overwhelming.
- Limited sense of personalized discovery or smart recommendations across franchises and formats.
- Performance, accessibility, and structured data can be improved to meet modern Core Web Vitals and SEO standards.

## 5. Scope (MVP)

### In Scope

1. **Information Architecture & Navigation**
   - Redesign global header and footer, unifying entry points for Movies, Shows, Games, Experiences, Channels, Podcasts, Shop, Redeem, Inclusion, Investor Relations, Corporate pages, and Search.
   - Clarify taxonomy and reduce duplication across media types.

2. **Homepage Redesign**
   - Cinematic hero carousel featuring top campaigns with clear CTAs (Get Tickets, Watch Now, More Info).
   - Dynamic content strips: Now In Theaters, Coming Soon, Streaming Now, Trending Franchises, News.
   - Prominent "Become a Lionsgate Insider" section with improved UX and consent handling.

3. **Title & Franchise Templates**
   - New templates for: Movie, Show, Game, Experience, and Franchise hub pages tying together all related entries across formats.
   - Each template includes hero art, trailer, synopsis, cast, crew, where-to-watch, and related content.

4. **News & Corporate Content**
   - Modernized News hub for articles with tagging and search.
   - Refined corporate pages for About, Inclusion, Investor Relations, Careers, Licensing, Legal, Privacy, regional (Lionsgate Canada).

5. **Search & Discovery**
   - Autocomplete search across titles, franchises, news, and corporate content.
   - Filterable search results (type, genre, availability).

6. **Performance, Accessibility, SEO**
   - Core Web Vitals optimization, WCAG 2.2 AA accessibility, and complete structured data for media entities and articles.

### Out of Scope (Phase 2+)

- Logged-in user accounts, watchlists, or cross-device sync.
- Deep ticketing or streaming API integration beyond link-outs.
- Advanced AI personalization and on-site chat/agent experiences.
- Full localization and multi-region rollout (beyond groundwork).

## 6. Functional Requirements

### 6.1 Global Navigation

- Sticky global header with:
  - Logo (Lionsgate).
  - Primary links: Movies, Shows, Games, Experiences, Channels, Podcasts, Shop, Redeem, News, Inclusion, Investor Relations, More.
  - Search icon with typeahead.
- Responsive behavior: Mobile drawer nav with clear grouping; Desktop mega-menu-style sections.

### 6.2 Homepage

- Hero Carousel: CMS-driven list of key campaigns with title art, release/status, and 2–3 CTAs.
- Content Strips: "Now in Theaters," "Coming Soon," "Streaming/Digital Now."
- News: Surface latest news stories with image, headline, and CTA.
- Email Capture: "Become a Lionsgate Insider" block with clear copy and legal/consent text.

### 6.3 Title Pages

Required fields: Title, poster, hero art, logline, synopsis, release dates, genres, rating, runtime, cast, crew, trailer, "Where to Watch" section.

### 6.4 Franchise Hubs

Unified page with franchise overview, key art, timeline of titles, and campaign modules.

### 6.5 Corporate & Legal

Structured access to: About, Inclusion, Investor Relations, Lionsgate Canada, Careers, Contact, Licensing, Sitemap, Legal, Privacy.

### 6.6 Search

Typeahead search in header with suggestions by category. Full results page with filters and sorting.

## 7. Non-Functional Requirements

- **Performance:** FCP < 2s on mobile 4G, LCP < 2.5s for hero content.
- **Accessibility:** WCAG 2.2 AA compliance across pages.
- **SEO:** JSON-LD for Movie, TVSeries, Episode, VideoObject, Article.
- **Security & Privacy:** Continued integration with Privacy Rights Manager and legal flows.

## 8. Dependencies & Risks

- **Dependencies:** CMS selection, media assets, legal/marketing/IT alignment.
- **Risks:** SEO impact, content migration complexity, scope creep.

## 9. Timeline (Indicative)

- Weeks 0–2: Discovery, IA, content audit.
- Weeks 3–6: UX & UI design, design system.
- Weeks 4–10: Frontend build, CMS integration, search.
- Weeks 8–12: QA, performance, accessibility, SEO.
- Weeks 12–14: Soft launch, A/B test, full cutover.
