# PRD — Photographer-Only Web Studio

**Market:** Georgia (Tbilisi) · **Currency:** GEL (₾) · **Timezone:** Asia/Tbilisi (UTC+4, no DST) · **Languages:** Georgian + English
**Status:** v1 · 21 July 2026

---

## 1 · What

A productized web studio that builds portfolio websites **for photographers only**. Not a generalist agency — no restaurants, no clinics, no crypto.

Three fixed packages with published prices and fixed timelines. Scope is a product, not an hourly estimate. Every site ships with a **booking spine**: an inquiry that reaches the photographer's WhatsApp within a minute, and a deposit link that actually gets paid. The deliverable is measured in bookings, not compliments.

Every site is bilingual KA + EN. Built on Webflow, so the photographer can update their own galleries after handoff without calling us.

---

## 2 · Who for

Photographers based in Georgia. The brief said 18–60, but **age is not the segment — career stage is.** Pricing to a single 42-year age band is exactly what would collapse the ladder.

| Segment | Typical age | Situation | Tier |
|---|---|---|---|
| **Emerging** | ~18–28 | Instagram-native, no website, thin budget | Launch |
| **Working professional** | ~25–45 | Weddings, commercial, editorial. Has real clients; loses inquiries in DMs | **Signature — core ICP, ~70% of revenue** |
| **Established studio** | ~35–60 | Already has a site. Wants a print shop, an education funnel, or a rebrand | Studio |

**Buying trigger:** they lost a specific inquiry, or they were embarrassed sending their current site to a brand or an agency. Nobody buys a website because it's Tuesday — sales copy should name the loss.

**Where they are:** Instagram (primary), Georgian photographer Facebook groups, workshops and meetups, wedding-vendor networks.

---

## 3 · Positioning

**Premium by specialization, not by price tag.**

Georgia's web market has a hard floor: Wix and Tilda freelancers at 500–1,500 ₾. Competing there is unwinnable and unescapable. The only defensible position is being the one studio that does this single thing — which lets us charge 4–10× the floor without ever arguing about it.

> **EN — Portfolio sites that book clients.**
> **KA — პორტფოლიო, რომელიც ჯავშნებს იღებს.**
>
> *For photographers in Georgia. Your work, an inquiry form that reaches your WhatsApp, and a deposit link that actually gets paid.*

> ⚠️ The Georgian line is a draft. Have a native speaker tighten it before it goes anywhere public.

**The honest gap:** an outcome promise requires evidence, and on day one there is none. A premium price with an empty logo wall reads as bluffing.

**Fix — the first-three-clients program.** The first three builds go at a reduced rate in exchange for: a published case study, a named testimonial, and permission to publish before/after inquiry numbers. That evidence is the asset that makes the pricing hold from client four onward. Budget for it; don't discover it.

**Anti-positioning, stated out loud:** we are not a template shop, not the cheapest, and not for photographers who want to "just get something online."

---

## 4 · Selections

### The offer ladder

| # | Service | Price | Timeline | What's in it |
|---|---|---|---|---|
| 1 | **Launch** | **2,500 ₾** | 10 working days | 5-section site on our own Webflow system. Client's photos, KA+EN, gallery + about + contact, inquiry → WhatsApp. 1 revision round. |
| 2 | **Signature** | **6,500 ₾** | 21 working days | Full portfolio: project/case pages, taxonomy chosen with the client, KA+EN CMS, inquiry → n8n → WhatsApp + Instagram, Payze deposit booking, proof blocks, CMS training. 2 revision rounds. |
| 3 | **Studio** | **13,000 ₾** | 6–8 weeks | Everything in Signature, plus custom design system, print shop, education/preset funnel, motion section, analytics + booking dashboard, 60-day post-launch optimization. 3 revision rounds. |

### Two attachments

- **Care plan — 350 ₾/month.** Hosting management, 2 gallery updates per month, automation monitoring, quarterly conversion report. Offered on every build; this is the recurring revenue that smooths a lumpy project business.
- **Portfolio Audit — 150 ₾.** A recorded 20-minute teardown of their current site and Instagram funnel. **Credited in full against any build.** This is the top of the funnel and the filter — it removes tire-kickers, earns money on day one, and demonstrates expertise before we've pitched anything.

### Why these numbers

Entry sits at roughly **one wedding fee** (Tbilisi wedding photographers charge ~1,500–4,000 ₾), so a photographer can rationalize it inside a single job. The flagship is 3–4 fees — reachable for an established shooter. **~2 builds per month at a mixed ladder sustains the studio.** The prices trace to a capacity target, not to a feeling.

### Our own portfolio taxonomy

Organized **by client project / case study** — matching the benchmark finding that every strong portfolio site commits to one deliberate taxonomy rather than a flat stream. Each completed build gets a case-study page carrying the before/after and the booking numbers. Our proof and our portfolio are the same artifact.

---

## 5 · Function

**Public site.** Hero, work grid, project pages, about, packages with visible prices, process, FAQ, testimonials, contact, KA/EN switch.

**Audit checkout.** Payze one-off 150 ₾ → n8n → slot reserved → recorded audit delivered.

**Lead spine (n8n).** Three triggers feed one pipeline:

1. Site inquiry form → webhook
2. Instagram DM → Instagram Messaging API
3. WhatsApp inbound → WhatsApp Cloud API

All three normalize into a **single lead record**, then: auto-reply within 60 seconds *in the channel the lead arrived on* → notify owner → follow up at 24h and 72h if the lead goes silent.

**Payments.** Payze checkout, GEL, cards + Apple/Google Pay. On `payment.succeeded` → n8n marks paid, reserves the build slot, sends receipt + intake form + calendar invite. Keep this behind **one generic payment event** so the gateway can be swapped later without rebuilding the flows.

**Deposit schedule.** Launch 50% up front · Signature 50% up front · Studio 40/30/30.

**Non-functional requirements.**

- Every timestamp, calendar hold, and follow-up delay in **Asia/Tbilisi**. Get this wrong and bookings land on the wrong day.
- Mobile-first. LCP under 2.5s on 4G *with heavy galleries loaded* — the hard case, not the empty homepage.
- **Georgian glyph coverage in the typeface.** Most Latin display fonts have none. This is a blocking constraint on the design system, not a detail to sort out later.
- hreflang for KA/EN.

---

## 6 · Design preferences

Derived from the 8-site benchmark, with the Refolio template's selling blocks grafted on:

- **Dark, image-led, full-bleed opening.** Work visible immediately — the Porodina and Kelley approach.
- **Lean top nav.** Depth by drill-down into rich project pages, never menu sprawl.
- **Hero is one short line.** Never a paragraph. All 8 benchmark sites hold this.
- **One grotesque carrying both scripts**, so Georgian and English read as a single system rather than two fonts sharing a page.
- **Conversion blocks rebuilt to studio quality** — process, priced packages, FAQ, testimonials, closing CTA — with the stock-template tells visible in Refolio stripped out.
- **Proof sits next to the work.** Client names, testimonials, numbers.
- **No blog.** None of the 8 benchmark sites run one. The site's only jobs are showing work and capturing an inquiry.
- **Our own site is the sales demo.** It has to be the single best example of the thing we sell. Nothing else we say survives a weak homepage.

---

## Risks

| Risk | Impact | Response |
|---|---|---|
| **Meta verification lead time** — WhatsApp Cloud API and Instagram Messaging both require a verified Meta Business account | **Gates launch.** Can be weeks. | Start verification before anything else in the build. |
| Webflow commerce is thin for a genuine print shop | Studio tier can't deliver as promised | Flag before selling a Studio tier; plan a Shopify embed. |
| 2,500 ₾ still exceeds much of the emerging segment | Lose the youngest buyers entirely | The 150 ₾ audit is their on-ramp; convert them later. |
| Georgian font licensing | Design system rework | Resolve before the type system is fixed. |
| No proof on day one | Premium price won't hold | First-three-clients program (§3). |

---

*Sources: 8-site photographer portfolio benchmark (`photography-portfolio-benchmark.pdf`), Refolio conversion template, McKinnon shop and Porodina reference captures.*
