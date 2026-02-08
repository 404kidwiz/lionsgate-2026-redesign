# Lionsgate.com Design Spec – 404 Technologies

## 1. Design Principles

- **Cinematic:** Large-format imagery, rich color, and immersive trailers that reflect Lionsgate's slate and franchises.
- **Clear:** Simple paths to core actions: watch trailers, get tickets, watch now, learn more.
- **Fast:** Design with performance in mind (smart use of imagery, motion used sparingly).
- **Accessible:** Visual and interaction design that supports all users.

## 2. Visual Language

### Color
- **Base:** Dark, cinematic background (charcoal/near-black, #0F0F0F).
- **Accents:** Per-franchise accent colors applied via tokens (e.g., Hunger Games ember orange #FF8C00, thriller blues, etc.).
- **Text:** Primary #FFFFFF, Secondary #CCCCCC

### Typography
- **Display type:** Strong, modern typeface for headings and key art titles (56px / 40px / 32px).
- **Body:** Highly legible sans-serif for body copy and metadata (Inter, Geist, or system fonts at 18px / 16px).

### Imagery
- Hero art and poster imagery prioritized above decorative visuals.
- Use of subtle gradients and overlays for text over imagery.
- Edge-optimized delivery via CDN with responsive sizing.

## 3. Layout & Components

### 3.1 Global Layout

- **Grid:** 12-column responsive grid with consistent spacing for mobile, tablet, desktop.
- **Sections:** Clear visual separation between hero, strips, news, and footer.
- **Spacing:** Base unit 8px increments (8, 16, 24, 32, 48, 64px).

### 3.2 Key Components

#### Hero Carousel
- Full-width module with 1–5 campaigns.
- Contains: Title logo/typography, short tagline or release status (e.g., "In Theaters and IMAX® November 20, 2026").
- CTAs: primary (Get Tickets/Watch Now) and secondary (More Info).
- Dot/thumbnail navigation with full keyboard accessibility.
- Auto-rotation with pause control.

#### Content Strips
- Horizontal carousels for: Now Playing, Coming Soon, Streaming Now, Trending Franchises.
- Cards: Poster, title, status badge (New, In Theaters, Streaming, Upcoming), quick CTA.
- Swipe-friendly on mobile, arrow navigation on desktop.

#### Title Page Hero
- Background hero art with gradient overlay for readability.
- Trailer play button (centered, prominent) above the fold.
- Key metadata cluster: rating, runtime, genre, release date, status.

#### Trailer Player
- Embedded video player with:
  - Captions and playback controls.
  - Responsive layout (16:9 or cinematic aspect ratio).
  - Floating mini-player on scroll (optional, sticky).

#### News Card
- Image (16:9 or custom aspect), headline, 1-2 line description, "Read More" CTA.
- Hover state: subtle scale and shadow.

#### Email Signup
- Clean text field and button.
- Short value prop: "Become a Lionsgate Insider."
- Clear privacy text: "See our [Privacy Notice](link)"
- Optional: Checkbox for franchise/genre preferences.

#### Footer
- Consolidated, responsive groupings:
  - **Explore:** Home, Movies, Shows, Games, Experiences, Channels, Podcasts, Shop, Redeem.
  - **Corporate:** Inclusion, Investor Relations, Lionsgate Canada, About, Careers, Contact, Licensing.
  - **Legal:** Sitemap, Terms of Use, Privacy Notice, Do Not Sell / Share, California Privacy Rights, AODA, Privacy Rights Manager.
- Social links (optional).

## 4. UX Flows

- **Homepage → Title page → Where to Watch:** Max 2–3 clicks from landing to "Get Tickets / Watch Now" for any featured title.
- **Homepage → News:** Click through from teaser to full article on internal or external news site.
- **Footer → Corporate/Legal:** Users find any corporate or legal document in 1–2 clicks.

## 5. Interaction & Motion

- **Hover states:** Slight scale (1.02–1.05) and shadow (subtle to medium) on cards, underline or color shift on text links.
- **Focus states:** Highly visible focus rings (2–4px, contrasting color) for keyboard navigation.
- **Transitions:** 150–250ms ease-out transitions for hover, route, and element transitions.
- **Motion:** Limit animated backgrounds to hero and key campaign modules to preserve performance (< 150ms animations).
- **Gestures:** Swipe left/right for carousels on mobile, arrow keys for desktop.

## 6. Design Tokens (Figma / Code Integration)

### Core Colors
```
- Primary Dark: #0F0F0F (base background)
- Primary Dark Lighter: #1A1A1A (cards, sections)
- Accent Primary: Dynamic per franchise
- Text Primary: #FFFFFF
- Text Secondary: #CCCCCC
- Success: #4CAF50
- Error: #FF6B6B
- Link: #6B9FFF
```

### Typography
```
- Display XL: 56px / 1.1 leading (h1)
- Display L: 40px / 1.2 leading (h2)
- Display M: 32px / 1.2 leading (h3)
- Body L: 18px / 1.6 leading (body)
- Body M: 16px / 1.6 leading (standard)
- Label: 12px / 1.4 leading (metadata)
```

### Shadows
```
- Subtle: 0 2px 8px rgba(0,0,0,0.15)
- Medium: 0 4px 16px rgba(0,0,0,0.25)
- Large: 0 8px 32px rgba(0,0,0,0.35)
```

## 7. Accessibility Requirements

- **WCAG 2.2 AA** compliance across all pages.
- Color contrast ratios ≥ 4.5:1 for text.
- Keyboard navigation for all interactive elements.
- Semantic HTML, ARIA labels where needed.
- Video captions and transcripts.
- Focus indicators clearly visible.

## 8. Responsive Design

- **Mobile (< 640px):** Single-column layout, drawer nav, larger touch targets (48px minimum).
- **Tablet (640px–1024px):** Two-column grid, simplified mega-menu.
- **Desktop (> 1024px):** Full mega-menu, multi-column layouts, optimized imagery.

## 9. Design Deliverables

- Figma file with design system (colors, typography, components, tokens).
- Page templates: Homepage, Movies index, Title detail, Franchise hub, News index/detail, Corporate pages, Search results, 404.
- Mobile, tablet, desktop variants for each page.
- Component library for dev handoff.
- Design QA checklist against WCAG 2.2 AA and performance guidelines.
