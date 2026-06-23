# PRD: Website Analysis & Clone Project

> **Note:** No URL was provided for analysis. This PRD is generated as a **comprehensive template and framework** based on the task description. It covers a full-featured modern web application clone, structured so development agents can begin work immediately. If a URL is supplied later, sections can be refined with site-specific data.

---

## 1. Executive Summary

This project involves the deep analysis, documentation, and full recreation (clone) of a target website. The scope includes:

- **Static page inventory** — all pages discoverable via sitemap or crawl
- **Dynamic section identification** — API-driven, CMS-driven, or user-specific content
- **Full-stack clone implementation** — frontend, backend, database, and DevOps

The clone will be a production-ready, scalable web application that replicates the UI, UX, and functional behavior of the original site. The development team will use this PRD as the single source of truth throughout the project lifecycle.

**Project Goals:**
- Achieve ≥95% visual and functional parity with the original site
- Implement all dynamic features with a clean, maintainable architecture
- Ensure the clone is independently hostable and fully decoupled from the original

---

## 2. Tech Stack Recommendation

| Layer | Technology | Justification |
|---|---|---|
| **Frontend Framework** | Next.js 14 (App Router) | SSR + SSG support covers both dynamic and static pages; excellent SEO; file-based routing mirrors typical site structures |
| **Styling** | Tailwind CSS + shadcn/ui | Rapid UI replication; utility-first approach for pixel-perfect cloning |
| **State Management** | Zustand + React Query (TanStack) | Lightweight global state + server state caching for dynamic sections |
| **Backend Framework** | Node.js + Express.js (or Next.js API Routes) | Unified JS stack; API Routes reduce infrastructure complexity for mid-size projects |
| **Authentication** | NextAuth.js / Auth.js | Supports OAuth, credentials, JWT, sessions out of the box |
| **Database** | PostgreSQL (primary) + Redis (cache/sessions) | Relational integrity for structured data; Redis for performance-critical caching |
| **ORM** | Prisma | Type-safe DB access, easy migrations, compatible with PostgreSQL |
| **File Storage** | AWS S3 / Cloudflare R2 | Scalable object storage for media, uploads, assets |
| **Search** | Algolia or MeiliSearch | If the original site has search functionality |
| **CMS (if needed)** | Sanity.io or Contentlayer | For blog/content-driven dynamic sections |
| **Email Service** | Resend or SendGrid | Transactional emails, notifications |
| **Hosting** | Vercel (frontend) + Railway/Render (backend/DB) | Zero-config deployment; scalable; matches Next.js ecosystem |
| **CDN** | Cloudflare | Asset caching, DDoS protection, performance |
| **CI/CD** | GitHub Actions | Automated testing, build, and deployment pipelines |
| **Monitoring** | Sentry + Vercel Analytics | Error tracking + real user monitoring |

---

## 3. Site Structure & Pages

> Since no URL was provided, the following represents a **canonical modern website structure**. Pages marked with `*` are to be confirmed against the actual sitemap (`/sitemap.xml` or `robots.txt`).

### Public / Marketing Pages

| # | URL Path | Purpose | Key Components | Content Type |
|---|---|---|---|---|
| 1 | `/` | Homepage — primary landing, brand intro | Hero, Feature Highlights, Testimonials, CTA, Nav, Footer | **Dynamic** (CMS-driven sections, live stats) |
| 2 | `/about` | Company/project overview | Team section, Mission statement, Timeline | Semi-static (CMS-editable) |
| 3 | `/features` | Product/service features list | Feature cards, Comparison table, Icons | **Static** |
| 4 | `/pricing` | Pricing tiers and plans | Pricing cards, Toggle (monthly/annual), FAQ | **Dynamic** (prices from DB/API) |
| 5 | `/blog` | Blog listing page | Post cards, Pagination, Category filters, Search | **Dynamic** (CMS/DB) |
| 6 | `/blog/[slug]` | Individual blog post | MDX/Rich text, Author info, Related posts, Comments | **Dynamic** |
| 7 | `/contact` | Contact form | Form, Map embed, Social links | **Dynamic** (form submission) |
| 8 | `/faq` | Frequently asked questions | Accordion, Search | Semi-static |

### Authentication Pages

| # | URL Path | Purpose | Key Components | Content Type |
|---|---|---|---|---|
| 9 | `/login` | User sign-in | Login form, OAuth buttons, Forgot password link | **Dynamic** |
| 10 | `/register` | New user registration | Registration form, Email verification | **Dynamic** |
| 11 | `/forgot-password` | Password reset request | Email input form | **Dynamic** |
| 12 | `/reset-password/[token]` | Password reset via token | New password form | **Dynamic** |

### User Dashboard (Authenticated)

| # | URL Path | Purpose | Key Components | Content Type |
|---|---|---|---|---|
| 13 | `/dashboard` | User overview | Stats widgets, Activity feed, Quick actions | **Dynamic** |
| 14 | `/dashboard/profile` | User profile settings | Avatar upload, Edit form, Password change | **Dynamic** |
| 15 | `/dashboard/settings` | Account preferences | Toggle switches, Notification prefs, Danger zone | **Dynamic** |
| 16 | `/dashboard/[resource]` | Resource management (varies by site) | Data tables, CRUD modals, Filters | **Dynamic** |

### Admin Panel

| # | URL Path | Purpose | Key Components | Content Type |
|---|---|---|---|---|
| 17 | `/admin` | Admin overview | KPI cards, Charts, Recent activity | **Dynamic** |
| 18 | `/admin/users` | User management | Data table, Search, Role editor, Ban/delete | **Dynamic** |
| 19 | `/admin/content` | Content management | CMS editor, Media library, Publish controls | **Dynamic** |
| 20 | `/admin/settings` | Site-wide settings | Config forms, Feature flags | **Dynamic** |

### Legal & Utility Pages

| # | URL Path | Purpose | Key Components | Content Type |
|---|---|---|---|---|
| 21 | `/privacy-policy` | Privacy policy | Long-form text, TOC | **Static** |
| 22 | `/terms-of-service` | Terms of service | Long-form text, TOC | **Static** |
| 23 | `/cookie-policy` | Cookie policy | Text content | **Static** |
| 24 | `/404` | Not found error page | Error message, Navigation links | **Static** |
| 25 | `/500` | Server error page | Error message | **Static** |
| 26 | `/sitemap.xml` | XML sitemap for SEO | Auto-generated | **Dynamic** (auto-generated) |
| 27 | `/robots.txt` | Crawler instructions | Rules file | **Static** |

---

## 4. Frontend Components Inventory

### Layout & Navigation
- `<Navbar />` — Logo, nav links, CTA button, mobile hamburger, authenticated user menu
- `<MobileMenu />` — Slide-out drawer for mobile navigation
- `<Footer />` — Links, social icons, newsletter signup, copyright
- `<Sidebar />` — Dashboard/admin side navigation
- `<Breadcrumb />` — Page hierarchy indicator

### Common UI Primitives
- `<Button />` — Primary, secondary, ghost, destructive variants
- `<Input />` — Text, email, password, search variants
- `<Select />` — Dropdown select component
- `<Checkbox />` / `<RadioGroup />`
- `<Toggle />` / `<Switch />`
- `<Textarea />`
- `<Label />`
- `<Badge />` — Status indicators, tags
- `<Avatar />` — User profile image with fallback initials
- `<Tooltip />`
- `<Skeleton />` — Loading placeholder
- `<Spinner />` — Loading indicator

### Modals & Overlays
- `<Modal />` — Generic modal wrapper
- `<ConfirmDialog />` — Destructive action confirmation
- `<Drawer />` — Side panel (mobile-friendly)
- `<Toast />` / `<Notification />` — Feedback messages
- `<AlertBanner />` — Top-of-page announcements

### Data Display
- `<DataTable />` — Sortable, filterable, paginated table
- `<Card />` — Generic content card with header/body/footer
- `<StatCard />` — KPI metric display
- `<PricingCard />` — Pricing tier display
- `<BlogPostCard />` — Blog listing item
- `<TestimonialCard />` — Customer/user quote
- `<TeamMemberCard />` — Profile card
- `<Timeline />` — Chronological event list
- `<Accordion />` / `<FAQItem />`
- `<Tabs />`

### Forms & Input Flows
- `<LoginForm />`
- `<RegisterForm />`
- `<ContactForm />`
- `<ProfileEditForm />`
- `<PasswordChangeForm />`
- `<SearchBar />`
- `<FilterPanel />` — Multi-filter sidebar/drawer

### Charts & Visualizations
- `<LineChart />` — Trend data (Recharts)
- `<BarChart />` — Comparative data
- `<PieChart />` / `<DonutChart />`
- `<AreaChart />` — Dashboard analytics

### Marketing / Landing
- `<HeroSection />` — Main banner with headline, subtext, CTA
- `<FeatureGrid />` — Icon + text feature list
- `<PricingSection />`
- `<TestimonialsSection />`
- `<CTASection />` — Mid/bottom-page call-to-action
- `<LogoBar />` — Partner/client logos
- `<NewsletterSignup />`

### Utility
- `<SEOHead />` — Meta tags, OG tags, canonical
- `<CookieBanner />` — GDPR/cookie consent
- `<ErrorBoundary />`
- `<ProtectedRoute />` — Auth guard wrapper
- `<RoleGuard />` — Role-based access wrapper
- `<Pagination />`
- `<EmptyState />` — No data placeholder
- `<RichTextRenderer />` — CMS content renderer

---

## 5. Backend & API Requirements

### 5.1 Authentication & Authorization

- **JWT-based sessions** with refresh token rotation
- **OAuth providers:** Google, GitHub (configurable)
- **Role-based access control (RBAC):** `guest`, `user`, `admin`, `superadmin`
- **Email verification** on registration
- **Password reset** via secure token (expiry: 1 hour)
- **Rate limiting** on auth endpoints (max 5 attempts / 15 min)
- **2FA support** (TOTP via authenticator app) — optional/Phase 2

### 5.2 API Endpoints

#### Auth
```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh
POST   /api/auth/forgot-password
POST   /api/auth/reset-password
GET    /api/auth/verify-email/:token
GET    /api/auth/me
```

#### Users
```
GET    /api/users               (admin only)
GET    /api/users/:id
PUT    /api/users/:id
DELETE /api/users/:id           (admin only)
PUT    /api/users/:id/role      (admin only)
POST   /api/users/:id/avatar
```

#### Content / Blog
```
GET    /api/posts               (paginated, filterable)
GET    /api/posts/:slug
POST   /api/posts               (admin/author)
PUT    /api/posts/:id           (admin/author)
DELETE /api/posts/:id           (admin)
GET    /api/categories
GET    /api/tags
```

#### Contact / Inquiries
```
POST   /api/contact
GET    /api/contact             (admin only)
PUT    /api/contact/:id/status  (admin only)
```

#### Pricing / Subscriptions
```
GET    /api/plans
POST   /api/subscriptions
GET    /api/subscriptions/:userId
DELETE /api/subscriptions/:id
POST   /api/webhooks/stripe     (Stripe webhook handler)
```

#### Admin
```
GET    /api/admin/stats
GET    /api/admin/activity-log
GET    /api/admin/settings
PUT    /api/admin/settings
```

#### Utility
```
GET    /api/health
GET    /sitemap.xml
GET    /robots.txt
```

### 5.3 Third-Party Integrations

| Service | Purpose | Priority |
|---|---|---|
| **Stripe** | Payment processing, subscriptions | High |
| **SendGrid / Resend** | Transactional email | High |
| **AWS S3 / Cloudflare R2** | File/media storage | High |
| **Google OAuth** | Social login | High |
| **GitHub OAuth** | Social login | Medium |
| **Algolia / MeiliSearch** | Full-text search | Medium |
| **Google Analytics 4** | Usage analytics | Medium |
| **Sentry** | Error monitoring | High |
| **Cloudflare** | CDN, DDoS, DNS | High |
| **Twilio** | SMS notifications (if applicable) | Low |

### 5.4 Email / Notification Services

**Transactional Emails (via template system):**
- Welcome email (on registration)
- Email verification
- Password reset
- Subscription confirmation / receipt
- Account activity alerts (new login from new device)
- Admin: new user registered, contact form submission

**In-App Notifications:**
- Real-time via WebSockets or polling
- Stored in `notifications` table
- Read/unread state management

---

## 6. Database Schema (High Level)

### `users`
```
id              UUID PRIMARY KEY
email           VARCHAR UNIQUE NOT NULL
password_hash   VARCHAR
name            VARCHAR
avatar_url      VARCHAR
role            ENUM('user','admin','superadmin')
email_verified  BOOLEAN DEFAULT false
created_at      TIMESTAMP
updated_at      TIMESTAMP
```

### `sessions`
```
id              UUID PRIMARY KEY
user_id         UUID FK → users.id
refresh_token   VARCHAR UNIQUE
expires_at      TIMESTAMP
ip_address      VARCHAR
user_agent      TEXT
created_at      TIMESTAMP
```

### `posts` (Blog)
```
id              UUID PRIMARY KEY
title           VARCHAR NOT NULL
slug            VARCHAR UNIQUE NOT NULL
content         TEXT (MDX/HTML)
excerpt         TEXT
cover_image     VARCHAR
author_id       UUID FK → users.id
status          ENUM('draft','published','archived')
published_at    TIMESTAMP
category_id     UUID FK → categories.id
created_at      TIMESTAMP
updated_at      TIMESTAMP
```

### `categories`
```
id              UUID PRIMARY KEY
name            VARCHAR
slug            VARCHAR UNIQUE
description     TEXT
```

### `tags` + `post_tags` (junction)
```
tags:       id, name, slug
post_tags:  post_id FK, tag_id FK
```

### `plans` (Pricing)
```
id              UUID PRIMARY KEY
name            VARCHAR
price_monthly   DECIMAL
price_annual    DECIMAL
features        JSONB
stripe_price_id VARCHAR
is_active       BOOLEAN
```

### `subscriptions`
```
id                  UUID PRIMARY KEY
user_id             UUID FK → users.id
plan_id             UUID FK → plans.id
status              ENUM('active','cancelled','past_due','trialing')
stripe_sub_id       VARCHAR
current_period_end  TIMESTAMP
created_at          TIMESTAMP
```

### `contact_inquiries`
```
id          UUID PRIMARY KEY
name        VARCHAR
email       VARCHAR
subject     VARCHAR
message     TEXT
status      ENUM('new','in_progress','resolved')
created_at  TIMESTAMP
```

### `notifications`
```
id          UUID PRIMARY KEY
user_id     UUID FK → users.id
type        VARCHAR
title       VARCHAR
body        TEXT
is_read     BOOLEAN DEFAULT false
created_at  TIMESTAMP
```

### `media`
```
id          UUID PRIMARY KEY
uploader_id UUID FK → users.id
filename    VARCHAR
url         VARCHAR
size        INTEGER
mime_type   VARCHAR
created_at  TIMESTAMP
```

### `settings` (Admin key-value store)
```
key         VARCHAR PRIMARY KEY
value       JSONB
updated_at  TIMESTAMP
updated_by  UUID FK → users.id
```

---

## 7. Dynamic Content Areas

| Area | Page(s) | Data Source | Update Frequency | Mechanism |
|---|---|---|---|---|
| Hero banner text/CTA | `/` | CMS (Sanity/DB) | On content publish | CMS API / ISR |
| Live stats / counters | `/` | Database aggregation | Real-time / hourly | API + caching |
| Blog post listing | `/blog` | Database | On publish | SSR + revalidation |
| Individual blog post | `/blog/[slug]` | Database / CMS | On publish | SSR + ISR |
| Pricing plans & prices | `/pricing` | Database | On admin update | SSR + cache |
| User dashboard widgets | `/dashboard` | Database (user data) | Real-time | Client-side fetch |
| Activity feed | `/dashboard` | Database | Near real-time | Polling / WebSocket |
| User profile data | `/dashboard/profile` | Database | On save | Client-side |
| Admin KPI cards | `/admin` | DB aggregations | Hourly / on demand | API with Redis cache |
| Admin user table | `/admin/users` | Database | On action | SSR + client refresh |
| Notifications | Global | Database | Real-time | WebSocket / polling |
| Search results | `/blog`, `/dashboard` | Algolia / DB | On index | Client-side API |
| Auth state | Global | Session/JWT | Per request | NextAuth session |
| Cookie consent state | Global | localStorage + DB | Once per user | Client-side |
| Sitemap | `/sitemap.xml` | Database (all pages) | Daily or on publish | Dynamic generation |

---

## 8. Non-Functional Requirements

### Performance
- **Core Web Vitals targets:** LCP < 2.5s, FID < 100ms, CLS < 0.1
- **Time to First Byte (TTFB):** < 200ms for cached responses
- **Image optimization:** Next.js `<Image />` with WebP/AVIF, lazy loading
- **Code splitting:** Per-route lazy loading of JS bundles
- **API response time:** < 300ms for 95th percentile
- **Redis caching** for frequently read, rarely changed data (pricing, settings)

### SEO
- Server-side rendering (SSR/ISR) for all public-facing pages
- Dynamic `<meta>` tags, Open Graph, Twitter Cards per page
- Structured data (JSON-LD) for blog posts, pricing, organization
- Auto-generated `sitemap.xml` updated on content publish
- Canonical URLs on all pages
- `robots.txt` configured correctly

### Accessibility
- **WCAG 2.1 AA** compliance minimum
- Semantic HTML throughout (`<nav>`, `<main>`, `<article>`, etc.)
- Keyboard navigation support for all interactive elements
- ARIA labels on icons, modals, and dynamic regions
- Minimum contrast ratio: 4.5:1 for normal text, 3:1 for large text
- Focus indicators visible on all focusable elements
- Screen reader tested (NVDA + VoiceOver)

### Security
- **HTTPS enforced** (HSTS headers)
- **Content Security Policy (CSP)** headers
- **CSRF protection** on all state-mutating endpoints
- **SQL injection prevention** via Prisma parameterized queries
- **XSS prevention** via input sanitization and output escaping
- **Rate limiting** on all public API endpoints
- **Secrets management** via environment variables (never hardcoded)
- **Dependency scanning** via Dependabot / Snyk
- **Auth tokens** stored in `httpOnly`, `Secure`, `SameSite=Strict` cookies

### Mobile Responsiveness
- **Mobile-first design** approach
- Fully responsive across: 320px (mobile), 768px (tablet), 1024px (laptop), 1440px+ (desktop)
- Touch-friendly tap targets (min 44×44px)
- No horizontal scroll on any viewport
- Mobile navigation via hamburger/drawer pattern

---

## 9. Out of Scope

The following will **NOT** be included in the initial clone (Phase 1):

1. **Native mobile apps** (iOS / Android) — web only
2. **Multi-language / i18n support** — English only initially
3. **Advanced analytics dashboard** — basic stats only, no custom report builder
4. **Live chat / chatbot integration** (e.g., Intercom, Drift)
5. **A/B testing framework** — deferred to Phase 2
6. **Affiliate / referral program** system
7. **API marketplace / public developer API** with API key management
8. **Advanced 2FA** (SMS-based, hardware keys) — TOTP only in Phase 2
9. **Custom domain management** per user/tenant (multi-tenancy)
10. **Data export / GDPR data portability** tooling — Phase 2
11. **Third-party app integrations** beyond those listed in Section 5.3
12. **Dark mode** — Phase 2 (design token structure will support it)
13. **Real-time collaborative editing** of any content
14. **Offline / PWA support**

---

## 10. Acceptance Criteria

| # | Criterion | Verification Method |
|---|---|---|
| **AC-01** | All pages listed in Section 3 render without errors across Chrome, Firefox, Safari, and Edge | Cross-browser automated test suite (Playwright) |
| **AC-02** | A new user can register, verify their email, log in, update their profile, and log out without errors | End-to-end Playwright test |
| **AC-03** | All public pages achieve a Lighthouse performance score ≥ 85 and pass Core Web Vitals thresholds | Lighthouse CI in GitHub Actions |
| **AC-04** | All forms (login, register, contact, profile) display correct validation errors for invalid inputs and succeed with valid inputs | Automated form validation tests |
| **AC-05** | Admin users can create, edit, publish, and delete a blog post; the post appears/disappears from `/blog` accordingly | Admin E2E test + API test |
| **AC-06** | The pricing page displays correct plan data from the database, and toggling monthly/annual recalculates prices correctly | API + UI integration test |
| **AC-07** | All pages are fully functional and visually correct on mobile (375px width) and desktop (1440px width) | Responsive visual regression tests (Percy/Chromatic) |
| **AC-08** | All authenticated routes (`/dashboard/*`, `/admin/*`) redirect unauthenticated users to `/login`; non-admin users cannot access `/admin/*` | Auth E2E tests |
| **AC-09** | The site scores ≥ 85 on Google Lighthouse Accessibility audit and has no critical WCAG 2.1 AA violations | axe-core automated scan + Lighthouse CI |
| **AC-10** | All API endpoints return appropriate HTTP status codes (200, 201, 400, 401, 403, 404, 500) under correct conditions, and no endpoint exposes sensitive data without authentication | API integration test suite (Jest + Supertest) |

---

## Appendix: Analysis Methodology Notes

> **For the development/QA agent:** When a URL is provided, the following analysis steps should be executed before development begins:

1. **Sitemap crawl:** `GET /sitemap.xml` → parse all URLs, categorize by path pattern
2. **Robots check:** `GET /robots.txt` → identify any disallowed paths
3. **Playwright deep crawl:** Visit every discovered URL, capture:
   - Screenshot (desktop + mobile)
   - DOM structure snapshot
   - Network requests (XHR/fetch calls reveal dynamic sections)
   - Console errors
4. **Dynamic detection heuristics:**
   - XHR/fetch calls on page load → dynamic content
   - `data-*` attributes populated after load → dynamic
   - Static HTML with no API calls → static
5. **Component extraction:** Identify repeated DOM patterns → reusable components
6. **Auth flow mapping:** Trace login/session cookies, protected route behavior
7. **Output:** Update this PRD's Section 3 with confirmed page list and Section 7 with confirmed dynamic areas

---

*Document version: 1.0 | Created by: Petra (AI Product Manager) | Status: Draft — pending URL confirmation*