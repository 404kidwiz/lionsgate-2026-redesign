# Lionsgate.com 2026 Redesign – Implementation
## Built by 404 Technologies

## 1. Architecture & Tech Stack

- **Frontend:** Next.js 15 (App Router), React Server Components, TypeScript
- **Styling:** Tailwind CSS + custom 404 Technologies design system tokens
- **CMS:** Headless (Contentful / Sanity / Storyblok / Strapi) – joint selection with Lionsgate
- **Search:** Algolia or Meilisearch for title, franchise, and article search
- **Hosting:** Vercel (primary) or AWS CloudFront + S3 + Lambda (optional per IT)
- **Media:** CDN-backed image and video delivery via `next/image` for responsive assets
- **Analytics:** GA4 + event tracking for conversions and user behavior
- **Forms & Email:** Existing ESP integration (Mailchimp, Braze, etc.) for newsletter signup

## 2. Routing & URLs

### Core Routes
```
/                           Homepage
/movies, /movies/[slug]    Movie index and detail pages
/shows, /shows/[slug]      Show index and detail pages
/games, /games/[slug]      Games index and detail pages
/experiences, /experiences/[slug]  Experiences
/channels, /podcasts       External or internal links
/franchises/[slug]         Franchise hub pages
/news, /news/[slug]        News index and article detail
/about, /inclusion, /investor-relations, /canada  Corporate pages
/careers, /contact, /licensing  
Legal, /legal/terms-of-use, /legal/privacy-policy, /redeem, /shop
/search                    Search results page
/sitemap, /accessibility-for-ontarians-with-disabilities-act  Static pages
```

### Redirect Strategy
- 301 redirects for legacy URLs that change
- Mapping document created during content audit phase
- Verify SEO impact via Google Search Console

## 3. Data Modeling (CMS)

### Content Types

**Movie**
- title, slug, logline, synopsis, poster (16:9), heroImage (cinematic)
- trailerVideo (URL or embedded), genres[], rating, runtime, releaseDate
- status (In Theaters, Digital, Streaming, Upcoming), cast[], crew[]
- franchise (reference), tags[], externalLinks (tickets, streaming partners)

**Show**
- Extends Movie with: seasons[], episodes[], network

**Game, Experience**
- platforms[], location, dates, similar fields to Movie

**Franchise**
- title, slug, description, heroArt, heroImage
- entries[] (linked Movies/Shows/Games/Experiences with order)
- campaign modules (optional for upcoming releases)

**NewsArticle**
- headline, slug, heroImage (16:9), bodyRichText (supports embeds)
- publishedAt (ISO date), sourceLink (external or internal URL)
- relatedTitles[] (references for context links)

**LayoutConfig** (Homepage configuration)
- heroItems[] (array of title references or custom campaigns)
- sections[] (ordered list of content strip configs)
- featuredNews (reference to top news story)

**NavConfig, FooterConfig**
- Allows marketing to reorder links without code deployment

## 4. Key Features & Implementation Details

### 4.1 Homepage Hero Carousel
- **Implementation:** Next.js server component fetching LayoutConfig from CMS
- **Features:**
  - Swiper.js or custom React carousel for touch/keyboard nav
  - Auto-rotate every 5 seconds, pause on user interaction
  - Full accessibility: arrow keys, Enter to navigate, dot indicators
  - Muted autoplay video as background for featured campaigns
- **Performance:** Hero images lazy-loaded with blur-up placeholders

### 4.2 Dynamic Content Strips
- **Implementation:** Map CMS sections array to card grid components
- **Cards:** Poster, title, badge (New, In Theaters, Streaming), CTA
- **Carousel:** Swipe left/right on mobile, arrow buttons on desktop
- **Reusability:** Single component accepts titles[] and section name

### 4.3 Title Detail Pages
- **Dynamic Route:** `/movies/[slug]`, `/shows/[slug]`, etc.
- **Content:** Hero with overlay, trailer player, metadata (rating, runtime, genre), synopsis, cast/crew, "Where to Watch" module, related titles, reviews/ratings (optional phase 2)
- **Trailer Player:** Embedded video with controls, captions, responsive 16:9 layout, floating mini-player on scroll
- **Where to Watch:** Links to ticketing partners, streaming platforms, digital purchase (hardcoded or CMS-driven)

### 4.4 Franchise Hubs
- **Route:** `/franchises/[slug]`
- **Content:** Franchise overview, key art, timeline of entries (Movies, Shows, Games, Experiences) with release dates
- **Timeline:** Interactive or static card grid sorted by release date
- **Campaign modules:** Featured upcoming entry with hero image and CTA

### 4.5 News/Press Hub
- **Route:** `/news` and `/news/[slug]`
- **Features:** Article list with filtering (tags, franchises), full article detail with rich text, related articles
- **SEO:** JSON-LD ArticleSchema with author, publish date, image
- **External integration:** Option to link to third-party press release site or pull via API

### 4.6 Search
- **Pipeline:**
  - On CMS publish/update, webhook triggers index update (Algolia / Meilisearch)
  - Index includes titles, franchises, news articles, corporate content
- **Typeahead:** Debounced API call to search service, top 5 suggestions grouped by type
- **Results Page:** 
  - Server-side rendering for initial query (SEO benefit)
  - Client-side pagination and filtering (type, genre, availability)
  - Sort by relevance or release date

### 4.7 Email Signup (Lionsgate Insider)
- **Implementation:** Form component with email field, optional franchise/genre checkboxes
- **Validation:** Client-side (basic) + server-side
- **Submission:** Secure API endpoint that:
  - Validates email + honeypot
  - Calls ESP API (Mailchimp, Braze, etc.) with list ID and preferences
  - Returns success/error to client
- **Privacy:** Clear notice linking to Privacy Policy, consent checkbox if required by jurisdiction

### 4.8 Corporate & Legal Pages
- **Routes:** About, Inclusion, Investor Relations, Careers, Licensing, Contact, etc.
- **Content:** CMS-backed rich text or external links
- **Legal:** Preserve existing Privacy Notice, Terms, Do Not Sell, Privacy Rights Manager link
- **Accessibility (AODA):** Ensure full WCAG 2.2 AA compliance, special care for PDFs/docs

## 5. Performance & Accessibility

### Performance Targets
- **Core Web Vitals:**
  - FCP (First Contentful Paint): < 2s on mobile 4G
  - LCP (Largest Contentful Paint): < 2.5s
  - CLS (Cumulative Layout Shift): < 0.1
  - INP (Interaction to Next Paint): < 200ms
- **Image Optimization:** 
  - `next/image` with responsive sizes and AVIF/WebP fallbacks
  - Lazy-load below-the-fold sections (Intersection Observer)
- **Code Splitting:** Dynamic imports for route transitions
- **Monitoring:** Sentry for frontend errors, Web Vitals tracking in GA4

### Accessibility (WCAG 2.2 AA)
- **Semantic HTML:** Proper heading hierarchy, landmark regions
- **Keyboard Navigation:** Tab order, focus indicators, skip links
- **ARIA:** Labels, live regions for dynamic content, roles where needed
- **Color Contrast:** ≥ 4.5:1 for normal text, ≥ 3:1 for large text
- **Video:** Captions and transcripts for all trailers
- **Forms:** Labels, error messages, validation
- **Testing:** axe-core automated + manual keyboard/screen reader testing

## 6. SEO & Structured Data

### JSON-LD Schema
```json
// Movies
{
  "@context": "https://schema.org",
  "@type": "Movie",
  "name": "I Can Only Imagine 2",
  "image": "[hero image URL]",
  "description": "[synopsis]",
  "datePublished": "2026-02-20",
  "genre": ["Drama", "Family"],
  "actor": [{"@type": "Person", "name": "John Michael Finley"}],
  "director": [{"@type": "Person", "name": "..."}]
}

// TVSeries
{
  "@type": "TVSeries",
  "name": "...",
  "episode": [...]
}

// Articles
{
  "@type": "NewsArticle",
  "headline": "...",
  "image": "...",
  "datePublished": "...",
  "author": {"@type": "Person", "name": "..."}
}
```

### Meta Tags
- Title, description, Open Graph (og:title, og:image, og:url)
- Twitter Card tags
- Canonical URLs
- Mobile viewport + no-zoom for accessibility

## 7. Security & Compliance

- **HTTPS:** Enforced site-wide
- **Privacy:** Integration with existing Privacy Rights Manager, Do Not Sell / Share flow
- **Forms:** Server-side validation, CSRF protection, rate limiting
- **Rate Limiting:** On newsletter signup, contact forms to prevent abuse
- **Data Minimization:** Only collect email + optional preferences, no unnecessary tracking

## 8. DevOps & Deployment

### Environment Setup
```
dev     - local development, feature branches
staging - integrated testing, pre-launch preview
prod    - live site
```

### CI/CD Pipeline (GitHub Actions)
```yaml
Trigger: push to main or PR
Steps:
  1. Lint (ESLint, Prettier)
  2. Type-check (TypeScript)
  3. Test (Jest + React Testing Library)
  4. Build (Next.js)
  5. Deploy (Vercel automatic or manual AWS cloudformation)
Artifacts: Build cache, deployment URLs
```

### Monitoring
- **Sentry:** Frontend error tracking and source map uploads
- **UptimeRobot:** Site uptime + alert on downtime
- **Vercel Analytics:** Built-in Web Vitals + traffic metrics
- **GA4:** Custom events for CTAs, signups, external clicks

## 9. Rollout Plan

### Phase 0: Foundation (Weeks 0–2)
- Content audit and migration planning
- CMS selection and setup
- Design system finalization in Figma
- Tech stack confirmation, dev environment setup

### Phase 1: Core Experience (Weeks 3–6)
- Global nav/footer on staging behind feature flag
- New homepage template (hero carousel, content strips)
- A/B test vs. current homepage (50/50 traffic split)
- Soft launch to 10% of traffic

### Phase 2: Title & Content (Weeks 4–10)
- Movie, Show, Game, Experience detail page templates
- Franchise hub pages
- Content migration for featured titles
- Full launch to 100% traffic

### Phase 3: Discovery & Polish (Weeks 8–12)
- News hub and article detail
- Search functionality
- Corporate pages redesign
- Performance, accessibility, SEO hardening
- QA and bug fixes

### Phase 4: Optimization (Weeks 12–14)
- Full cutover from old site
- URL migration and redirect verification
- Post-launch monitoring and analytics review
- Iteration based on KPI data (conversion rate, bounce rate, engagement)

## 10. Maintenance & Support

- **Post-Launch Support:** 2–4 weeks of bug fixes and refinements
- **Ongoing Retainer (Optional):** 8–15 hours/month for:
  - New campaign landing pages
  - CMS content management support
  - Performance optimization
  - Security updates
  - Minor feature requests

## 11. Success Criteria

- Lighthouse score ≥ 90 on mobile and desktop
- WCAG 2.2 AA compliance verified
- Click-through to ticketing/streaming up 15–30%
- Email signups up 20%
- Bounce rate down 10–20%
- No critical bugs 2 weeks post-launch
- Site fully migrated and legacy URLs redirected
