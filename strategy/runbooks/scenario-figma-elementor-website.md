# 🧭 Runbook: Figma-to-Elementor Website

> **Mode**: NEXUS-Sprint | **Duration**: 3-6 weeks | **Agents**: 10-15

---

## Scenario

A client needs a marketing, brochure, or lead-generation website on WordPress, built in Elementor, that faithfully matches a custom design. The work runs through four client-approved gates: **intake questions → written plan → complete Figma design and animations → Elementor build → QA and handoff**. The build favors native Elementor widgets, global styles, and reusable templates, and uses custom CSS, HTML, or JavaScript only when the approved Figma design can't be reproduced otherwise.

## Gate Rules

- A phase starts only after the client explicitly approves the previous one ("approved", or approval with listed changes). Silence or "looks good so far" is not approval.
- Changes requested at a gate loop back into that phase, never forward.
- After Gate 2, the approved Figma file is the source of truth. Design changes found during the build go back into Figma first.
- Every use of custom CSS, HTML, or JS is recorded in the Deviation Log with the reason native Elementor couldn't do it.

## Agent Roster

### Core Team (Always Active)
| Agent | Role |
|-------|------|
| Agents Orchestrator | Pipeline controller; enforces the four gates |
| Senior Project Manager | Intake questions, scope, written plan |
| UX Architect | Sitemap, page outlines, component inventory |
| UI Designer | Figma foundations, components, all pages at all breakpoints |
| Figma-to-Elementor Web Builder | Figma→Elementor maps, Elementor build, Deviation Log |
| Evidence Collector | Figma-vs-build screenshot comparison at every breakpoint |
| Reality Checker | Final production-readiness sign-off |

### Design & Motion Team (Phases 1-2)
| Agent | Role |
|-------|------|
| Brand Guardian | Visual direction; brand basics if none exist |
| Whimsy Injector | Animation and micro-interaction concepts within the agreed motion level |
| UI Finish-Gate Reviewer | Internal design critique before the client sees Gate 2 |

### Build & QA Support (As Needed)
| Agent | Role |
|-------|------|
| CMS Developer | Child theme, custom post types, ACF fields, PHP |
| Frontend Developer | Custom CSS/HTML/JS (escalation rungs 4-5), e.g. GSAP motion |
| Accessibility Auditor | WCAG 2.2 AA, keyboard, reduced-motion checks |
| WordPress Performance Engineer | Core Web Vitals, caching, Elementor asset loading |
| SEO Specialist | Page structure, metadata, and redirects when SEO matters |
| Content Creator | Copywriting when the client has no content |

## Phase-by-Phase Execution

### Phase 0: Intake (Day 1-3)

```
├── Senior Project Manager → Send the grouped intake questionnaire:
│     purpose & goals, audience, scope & content, visual style,
│     functionality, animation level, technical setup & delivery method
├── Senior Project Manager → Summarize answers; ask only plan-changing follow-ups
└── Output: Confirmed brief
```

### Phase 1: Written Plan (Day 3-7) → 🚦 Gate 1

```
├── UX Architect → Sitemap + section-by-section outline for every page
├── Brand Guardian → Visual direction: palette, type scale, spacing, imagery
├── Figma-to-Elementor Web Builder → Component inventory with planned Elementor
│     widget for each; draft motion spec with native vs. custom flag; custom-code forecast
├── Senior Project Manager → Assemble plan, risks, timeline
└── 🚦 Gate 1: Client approves the plan
```

### Phase 2: Figma Design & Animation (Week 2-3) → 🚦 Gate 2

```
├── UI Designer → Foundations: variables/styles named for Elementor globals
├── UI Designer → Components with all states (EL/…, TPL/…, CUSTOM/… naming)
├── UI Designer → Every page at Desktop 1440 / Tablet 1024 / Mobile,
│     auto-layout mirroring Elementor Flexbox/Grid Containers
├── Whimsy Injector → Motion concepts; prototype interactions (Smart Animate)
├── Figma-to-Elementor Web Builder → Motion Spec page + Build Notes
│     (component→Elementor map, deviation forecast), buildability review
├── UI Finish-Gate Reviewer → Internal critique; fixes before client review
└── 🚦 Gate 2: Client approves the Figma file and prototype (version recorded)
```

### Phase 3: Elementor Build (Week 3-5) → 🚦 Gate 3

```
├── CMS Developer → WordPress, Hello Elementor child theme, CPTs/fields, vetted plugins
├── Figma-to-Elementor Web Builder →
│     1. Site Settings globals from the token map; breakpoints match Figma
│     2. Theme Builder: header, footer, single, archive, 404
│     3. Saved templates, Global Widgets, Loop Items for every reusable component
│     4. Pages assembled from reusable parts
│     5. Motion: Entrance Animations + Motion Effects first, then escalate
├── Frontend Developer → Only for logged rung-4/5 deviations (HTML widget, custom JS)
├── Evidence Collector → Running Figma-vs-build comparison per page
└── 🚦 Gate 3: Client approves the build review (staging or import package)
```

**Native-first escalation ladder** (stop at the first rung that matches the design):
1. Native widget + Site Settings globals
2. Native widget controls, Motion Effects, Entrance Animations, Theme Builder conditions
3. Scoped custom CSS on the widget/container → Deviation Log
4. HTML widget → Deviation Log
5. Custom JavaScript via Elementor Custom Code or child theme → Deviation Log

### Phase 4: QA & Handoff (Week 5-6) → 🚦 Gate 4

```
├── Evidence Collector → Screenshot pairs for every page × breakpoint
├── Accessibility Auditor → WCAG 2.2 AA, keyboard, focus, reduced motion
├── WordPress Performance Engineer → Mobile Lighthouse, Core Web Vitals, caching
├── Figma-to-Elementor Web Builder → Fixes; editor handoff guide; Kit export; Deviation Log
├── Reality Checker → Evidence-based production-readiness verdict
└── 🚦 Gate 4: Client approves → launch
```

## Key Deliverables

| Phase | Deliverable | Owner |
|-------|-------------|-------|
| 0 | Confirmed brief | Senior Project Manager |
| 1 | Written plan (sitemap, outlines, visual direction, component inventory, motion spec, custom-code forecast) | Senior Project Manager + UX Architect |
| 2 | Figma file: Foundations, Components, Pages ×3 breakpoints, Prototype, Motion Spec, Build Notes | UI Designer |
| 3 | Elementor build or import package; token map; Deviation Log; Build Review report | Figma-to-Elementor Web Builder |
| 4 | QA report, editor guide, Kit export | Evidence Collector + Reality Checker |

## Success Criteria

- Every phase started only after explicit approval of the previous gate
- Build matches the approved Figma at desktop, tablet, and mobile; any remaining differences are listed and accepted
- ≥ 90% of elements built with native widgets and globals; 100% of custom code logged
- WCAG 2.2 AA passes; all motion honors `prefers-reduced-motion`
- Mobile Core Web Vitals in the "good" range on staging
- Client editors can update content and reusable components without developer help
