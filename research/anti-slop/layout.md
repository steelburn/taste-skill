# Layout and Component Slop in AI-Generated Websites

*Assembled 2026-07-18. This report synthesizes nineteen scoped web-research briefs on the layout and component defaults of AI-generated websites, covering landing pages, marketing websites, portfolios, editorial sites, and product websites. Section 1 states the executive findings; Section 2 audits full-page architecture; Section 3 walks the page section by section; Section 4 ledgers twenty recurring components; Section 5 measures repetition and saturation; Section 6 lists the research gaps. The nineteen briefs are the layout-scoped series written for this report (`briefs/01_hero.md`–`briefs/19_meta_discourse.md`, the underscore-named family); the same workspace contains a separate, parallel dash-named research family on accessibility/interaction slop that this report does not draw on.*

## Contents

1. Executive Findings
2. Full-Page Architecture Failures
3. Section-by-Section Failure Patterns — 3.1 Hero · 3.2 Navigation · 3.3 Feature presentation · 3.4 Product demonstrations · 3.5 Social proof · 3.6 Comparison · 3.7 Process / "How it works" · 3.8 Pricing · 3.9 Testimonials · 3.10 FAQ · 3.11 Calls to action · 3.12 Contact · 3.13 Footers
4. Component-Level Failure Ledger — 4.1 Uniform card trio · 4.2 Bento feature grid · 4.3 Hover-lift cards · 4.4 Icon + title + text card formula · 4.5 Checkmark bullet lists · 4.6 Tabbed feature panels · 4.7 Auto-advancing carousels · 4.8 Logo walls and marquees · 4.9 Stat bars · 4.10 Testimonial three-card grids · 4.11 Pricing tier cards · 4.12 FAQ accordions · 4.13 Fake-chronology timelines · 4.14 Sticky-scroll split sections · 4.15 50/50 zigzag rows · 4.16 Faux browser-chrome frames and device mockups · 4.17 CTA bands · 4.18 Announcement pills · 4.19 Gradient-text keywords · 4.20 Vestigial newsletter boxes
5. Repetition and Saturation Findings
6. Research Gaps
Appendix: Source Index

## 1. Executive Findings

This report audits the layout and component defaults that AI website generators (v0, Lovable, Bolt, Cursor, and the prompt-driven builders built on them) emit for landing pages, marketing sites, portfolios, editorial sites, and product websites. Nineteen research briefs examined the page element by element, from hero to footer, plus the meta-discourse around the "AI look." The cross-cutting conclusions:

1. **The "AI look" is a measurable statistical fingerprint, not a vibe.** In a study of roughly 1,400 Show HN pages, 67% carried AI-generated fingerprints (Krebs Show HN study, via slop-detect). When CoffeeBytes gave Bolt, Lovable, and v0 the same prompt, all three emitted the identical page skeleton: logo-left nav, centered hero, three to four sections. The fingerprint is lint-able at the class level: `bg-clip-text text-transparent` gradient headlines, `from-indigo-* to-purple-*` accents, `backdrop-blur` navs, `rounded-2xl shadow-xl` card stacks.

2. **The mechanism is averaging, and it is documented.** LLMs return the mode of 2019–2024 scraped Tailwind tutorials, and RLHF sharpens that mode further: alignment measurably reduces output diversity (Kirk et al., ICLR 2024), and over 70 models produce strikingly similar outputs (NeurIPS 2025 "Artificial Hivemind"). Deployed AI sites are then scraped into the next training corpus, narrowing the distribution further (Shumailov et al., Nature 2024).

3. **Sameness predates AI; AI industrialized it.** Measured layout distance between websites fell 44% from 2010 to 2019, before any LLM shipped a page (Goree et al., CHI 2021, via saschb2b). CRO culture A/B-tested its way to the same template first. This matters because it means the problem is not "AI patterns are bad" but "patterns are emitted unchosen."

4. **The core diagnostic is the brand-swap test: does the layout survive changing the logo?** Earned convention (nav logo-left, hero-first, card scannability) improves comprehension and wayfinding under Jakob's Law and processing-fluency research (Reber/Schwarz/Winkielman 2004). Unearned default is structure emitted regardless of brand, audience, or content. A feature grid of three icon cards whose copy works unchanged for any company is slop; the same grid carrying brand-specific claims is convention.

5. **Hero and CTA conventions are earned; their stock fillings are not.** Front-loading the value proposition and first CTA is justified by attention data: 57% of viewing time goes to the first screenful, 74% to the first two, 81% to the first three (NN/g). Repeating one CTA at two to three decision points lifted conversion from 7% to 12.8% in a GoodUI test (via Metrifi). Slop is the pill badge plus gradient-text H1 plus two buttons plus fake dashboard screenshot, and the identical gradient "Ready to get started?" band re-emitted after every section.

6. **Sections included "because pages have them" are the most widespread page-level failure.** Invented stats bands ("10,000+ teams, 99.9% uptime"), logo clouds of unrecognizable wordmarks, three-step "How it works" blocks hard-coded into generators, and FAQs answering rhetorical non-questions appear regardless of whether the content exists. Weak or decorative proof does not merely fail to help; it makes visitors more skeptical (Mantasauk).

7. **Social proof is flipping into an anti-signal.** Logo walls and stat-bar quartets are now purchasable filler: fakelogo.com sells the exact quartet AI emits, and fake reviews carry legal exposure under the FTC rule of October 2024 (up to roughly $51,744 per violation). Uniform five-star testimonial cards backfire; purchase likelihood peaks at ratings of 4.2–4.7, not 5.0 (Spiegel Research Center).

8. **The default containers hide content.** Cards lose to lists for scanning and comparison tasks (NN/g), the bento grid is the self-declared "layout of 2024," and carousels get roughly 1% click-through with 84% of clicks on slide one (Notre Dame data). In the Web Anatomy dataset of 286 sections, 79% showed no persona grouping and 72% were dead-end cards.

9. **Mobile is where slop compounds.** AI generators are structurally desktop-first; the mobile render is a mechanical `grid-cols-1` byproduct, not a redesign. Hidden navigation cuts discoverability by over 20% (NN/g, 179-user study), and on a phone the duplicated CTA bands and decorative stats blocks consume the highest-attention viewport, accelerating abandonment.

10. **The market now treats slop as a defect class.** Anthropic's `frontend_aesthetics` prompt bans Inter, purple-on-white gradients, and three-boxes-with-icons outright; Paul Bakaus's "Impeccable" skill codifies 37 anti-patterns; slop-detect ships 27 lint rules. The remedies converge on constraint rather than better adjectives: design tokens before generation, exclusion lists, generating five directions and discarding the most conventional, and at least one hand-made element per page.

The through-line: nothing in this report bans a familiar layout. Every flagged pattern has a legitimate, earned form. The failure mode is always the same: the pattern emitted as the unchosen statistical default, filled with content that would work for any brand, which is to say for none.

## 2. Full-Page Architecture Failures

### The canonical skeleton and where it came from

AI builders have converged on one page: sticky nav (logo left, links center, pill CTA right), centered hero (pill badge, gradient-text headline, two buttons, framed product screenshot), logo cloud, three-column icon feature grid, bento grid, three-step "How it works," stats counter, testimonial marquee, three-tier pricing with a highlighted middle plan, FAQ accordion, a centered gradient CTA band, mega footer. Tailwind Plus sells blocks in exactly these categories: Heroes (12), Feature Sections (15), CTA Sections (11), Bento Grids (3), Pricing (12), Stats (8), Testimonials (8), Logo Clouds (6), FAQs (7), Footers (7). shadcn libraries ship the identical taxonomy, and templates sell the whole chain: HugoBlox's demo AI prompt is literally "Generate a landing page for my SaaS with hero, pricing, and testimonials."

The mechanism is averaging. The model returns the mode of 2019–2024 scraped Tailwind tutorials; RLHF sharpens that mode (Kirk et al., ICLR 2024; NeurIPS 2025 "Artificial Hivemind"). Sameness predates the models: measured layout distance between websites fell 44% from 2010 to 2019 (Goree et al., CHI 2021). AI industrialized an existing disease.

### Sections included "because pages have them"

The canonical order mirrors a real decision journey: what is this, is it for me, do I believe it, what does it cost, what now. CRO guidance: "every section has to earn its place" (Growform, 2025). The AI failure is emitting the slots with no content to fill them: a stats band with invented round numbers ("10,000+ teams", "99.9% uptime"); a logo cloud of greyed-out wordmarks resolving to no real company; a testimonial slab of three generic quotes; an FAQ of self-congratulatory non-questions ("Why is X the best choice?"). Weak proof is worse than no proof: "visitors notice the lack of substance and become more skeptical" (Mantasauk); the earned form distributes four to eight proofs against the objections each section raises. A related failure is message drift: clear hero, technical middle, vague closing CTA (Veza Digital); each section is an independent block with no memory of the page's claim.

### Duplicated CTAs as a pacing failure

CTA repetition is earned: a GoodUI test found repeated CTAs lower on the page lifted conversion from 7% to 12.8% (via Metrifi), and CRO consensus is one primary action at two to three decision points. The slop version is the metronome band: the identical full-width gradient CTA after every section, four to six times per page. First, banner blindness: a full-width gradient band with centered text and a button looks exactly like a display ad; Benway and Lane found users located banner-style links only 58% of the time versus 94% for standard links (NN/g). Second, the same CTA visible twice within one viewport reads as nagging (Metrifi). The finale is a stock component: "Ready to get started? / Join 10,000+ customers / Start Free" appears verbatim in the Tailwind CTA catalog (ctaexamples.com). Lint rule: >3 visually identical CTA bands per page, or the same button label ≥4 times across nav, hero, bands, footer.

### Narrative pacing and information scent

Attention data justifies the skeleton's priorities: 57% of viewing time lands in the first screenful, 74% in the first two, 81% in the first three (NN/g). The template's rhythm sabotages the rest. Every section opens with the same triad (centered eyebrow pill, H2, gray subheading) on strictly alternating white and `bg-slate-50` backgrounds. This metronome destroys information scent: nothing signals which section matters. Spool's "Iceberg Syndrome" research shows that when early sections give no scent of what follows, users assume below-fold content repeats what is above and stop scrolling (Interaction Design Foundation). The lint-able signature: four or more consecutive sections with identical header anatomy, plus headings that name the component rather than say something ("Features", "Frequently asked questions" as literal H2s; Flow Agency flags these as useless headings).

### Site-type mismatch

AI applies the SaaS spine to everything because it is the modal "webpage" in the training distribution. A portfolio forced through the funnel (hero, "features" of the designer, pricing) is absurd; portfolio guidance demands case-study narrative (context, decisions, trade-offs, outcomes) and warns against reusing one structure across projects (Open Doors, 2025). An editorial site needs typographic pacing, not a bento grid and a pricing table. An event, waitlist, or local-business page should run three to five sections: what, when, who, one form. Multi-audience product sites should be hub-and-spoke routers, not twelve-section mega-pages. Detection rule: a portfolio, editorial, event, or local-business page containing a pricing section, a stats counter band, or a "How it works" three-stepper is architecture emitted without a decision journey to serve.

### The brand-swap interchangeability test

The report's core diagnostic: swap the logo and brand name; if nothing breaks, the layout is unearned default. Applied at page level, the test flags the feature grid of exactly 3, 6, or 8 icon cards with copy interchangeable across brands, the unverifiable stats band, the FAQ no buyer asked. Heuristics: the section sequence matching `nav → hero → logo-cloud → features → how-it-works → stats → testimonials → pricing → faq → cta → footer` with eight or more of eleven present regardless of site type; a proof-to-claim ratio below 1:3; more than eight sections on a single-offer landing page (lead pages typically earn three to five, long sales pages seven to ten, per Growform).

### When the canonical skeleton IS the right answer

The skeleton is earned for product marketing. For SaaS, that sequence demonstrably reduces cognitive load and converts; Dave Benton's line, keep the backbone standard while making your unique elements shine, captures the defensible core (Overpass Studio). Jakob's Law argues users arrive productive when patterns match the rest of the web, without advocating sameness. For prototypes, MVPs, and internal tools, the median is a gift, not a defect (saschb2b). The failure is never the spine. It is the spine emitted with no argument inside it: the same eleven sections, in the same order, with the same fill, for a restaurant and a Series B developer tool alike.

## 3. Section-by-Section Failure Patterns

Each section type below has a legitimate job and conventions that earn their familiarity. The failure pattern is never the convention itself; it is the unearned default — structure emitted regardless of brand, audience, or content, passing the "swap the logo, nothing breaks" interchangeability test.

### 3.1 Hero

**Legitimate job.** The hero is the highest-attention region of the page: eye-tracking and viewability data put the above/below-fold attention gap at ~84%, and visitors judge stay/leave in under a second (NN/g, Page Fold Manifesto). Its jobs: orientation ("what is this, who is it for" inside a 5-second test), one unmissable primary action, scroll signposting that avoids the "false floor," and a brand signal no one else could own. The headline + subhead + CTA + visual unit is an earned convention; unearned sameness is the slop.

**Common AI-generated defaults.** Independent detectors converge on one default (uislop, slop-detect): a centered stack — pill badge ("✨ v2.0 is live") above a centered H1 with one keyword in gradient text, muted subhead, exactly two buttons ("Get started" filled + "Learn more" ghost) — over a wide dashboard screenshot in fake browser chrome, `blur-3xl` aurora blobs behind. Inter/Geist/Space Grotesk throughout; `text-7xl` regardless of headline length; `h-screen` hero-as-whole-page. Variants: split hero, WebGL-orb portfolio hero, post-2025 editorial hero (cream background, Instrument Serif/Fraunces italic accent word).

**Why those defaults fail.** Statistical averaging, not design: Tailwind's `bg-indigo-500` propagated into training data and LLMs emit its median (dev.to, "Blame Tailwind's Indigo-500"); ~67% of ~1,400 Show HN submissions carried AI fingerprints (Krebs study, via slop-detect), and visitors pattern-match "AI-built" in under a second — a trust tax. Decoration does no orientation work in the highest-attention zone; "Get started" duplicates across nav, hero, footer; the pill hijacks the first fixation; `text-7xl` compresses headlines into 3–5 interchangeable slogans. Swap test: any competitor's name fits.

**Detection signals.**

- Structural: `h1.text-center` + `p.max-w-2xl.mx-auto` + exactly two button siblings + screenshot in a browser-frame wrapper; rounded-full bordered pill before the `h1` matching "New|Beta|Introducing|v\d"; `min-h-screen` hero with no scroll signpost; ≥1 `blur-3xl` div behind content; >4 hero text elements.
- Class/style: `bg-clip-text text-transparent` + `from-indigo-500 to-purple-600` on an h1 `<span>`; `backdrop-blur` glass nav; WebGL canvas for a non-3D product; Instrument Serif/Fraunces italic single-word accent (2025–26 editorial tell).
- Copy: "Unlock the power of…", "Supercharge your…", "X, reimagined"; subhead template "The [adjective] platform that helps [audience] [verb] [outcome]"; CTA pair exactly "Get started" + "Learn more".
- Quantitative: H1 ≥60px with >8 words or ≤4 words; ≥3 gradient-filled elements; same CTA intent under ≥3 labels across nav/hero/footer.

**Valid exceptions.** Earned bigness for launches, studios, and portfolios where typography is the deliverable; proof-native visuals for dev tools; brand-owned gradients (Stripe, Vercel); a pill linking to an actual changelog; disposable pages where uniqueness has near-zero ROI.

**Better layout families.** Split with real product UI; hero-with-form for high-intent services; content-forward editorial hero; proof-first hero for unknown brands; interactive demo hero; wayfinding hero (statement + search + task links); asymmetric broken-grid for studios. One hero, one job, one primary CTA.

**Mobile-specific risks.** `h-screen` jumps as browser chrome collapses — missing `min-h-[100dvh]` is itself an AI tell; `text-6xl+` wraps one word per line at 375px; stacked full-width buttons can push the CTA below the mobile fold; the screenshot shrinks to unreadable texture; aurora/WebGL burns LCP and battery on first-visit devices.

### 3.2 Navigation

**Legitimate job.** Orientation (logo as home link), wayfinding (the 3–7 destinations users actually need, matching mental models from other sites — Jakob's Law), and one persistent primary action. Sticky headers are earned on long pages, saving ~22% of navigation time (NN/g-derived). The familiar bar — logo left, links middle, CTA right — is an earned convention; breaking it is what fails (centered logos produce 6× more navigation failures, NN/g).

**Common AI-generated defaults.** One statistically average header for every brand: the glass pill bar (`fixed top-0 backdrop-blur-md bg-white/70 border-b`) regardless of what scrolls beneath; the SaaS link set "Features · Pricing · Docs · Blog · Login" + "Get Started" even on non-SaaS sites; centered-logo symmetric bars; hamburger on desktop at 1440px despite four links; a mega-menu housing 2–3 links; a scroll-triggered transparent-to-solid costume change; the same "Get Started" repeated in header, hero, band, footer.

**Why those defaults fail.** Glass blur is a readability hazard: in a 2024 OsloMet usability thesis, higher transparency produced longer task times and lower readability. Desktop hamburgers cut discoverability by up to ~50% (NN/g). Template links often point nowhere (`href="#"`) — decorative wayfinding signaling structure the product lacks. Hover mega menus fail touch and keyboard. Scroll restyles violate NN/g sticky-header guidance (motion minimal; a header that needs shrinking was too big). Duplicated CTA chains dilute each other; CRO wants one dominant action per view.

**Detection signals.**

- Structural/class: `position: fixed|sticky` header + `backdrop-blur*` + translucent background (`rgba(..., <0.95)`); 3-column grid with logo in the middle column; hamburger toggle at ≥1024px viewport with ≤6 links; dropdown panel containing ≤3 links; nav set matching `/(features|pricing|docs|blog|about)\b/i` plus "Login" plus "Get Started" on a non-SaaS site; nav `href="#"` or 404 targets; a `scroll`/`scrollY` listener toggling header classes; transparent header over hero imagery with no scrim; sticky header >80px desktop.
- Copy: "Get Started" as the universal CTA; nav labels describing template sections rather than the site's real pages.
- Quantitative: identical CTA label+href ≥3 times in the document; footer links an exact subset of header links; >5 nav items on a site with <5 real pages.

**Valid exceptions.** Slim (60–80px), opaque, low-motion sticky headers on docs, e-commerce, and pricing; mega menus for genuinely deep IA with click activation and keyboard support; hybrid overflow (3–5 visible links + a labeled "Menu" — the label raised interactions ~61%); transparent-over-hero on art-directed pages; removing nav entirely on campaign landing pages (+15–25% conversion, Unbounce-cited).

**Better layout families.** Slim opaque bar with a specific CTA ("Get a quote" beats "Get started"); hybrid/overflow nav; landing-page minimal (logo + one CTA); hub pages over dropdowns; docs sidebar trees; editorial section nav + breadcrumbs; mobile bottom bar with 3–5 labeled destinations. Differentiate through labels and CTA specificity; keep the backbone conventional.

**Mobile-specific risks.** Sticky glass headers consume 30%+ of the viewport and obscure focus targets; translucency over scrolling photos collapses contrast; hover-only dropdowns are dead on touch; a CTA hidden inside the hamburger kills mobile conversion; `100vh` hero + fixed header + mobile browser chrome clips content.

### 3.3 Feature presentation

**Legitimate job.** Confirm within ~30 seconds what the product does; let visitor types self-locate; route interested visitors deeper. NN/g supports grids for browsing heterogeneous items; grids aid scanning when items are parallel, few, and distinct — earned when copy is benefit-led and outcome-mapped.

**Common AI-generated defaults.** Section header "Everything you need" + muted subtitle; a 3-column icon grid (lucide Zap/Shield/BarChart3 in a `bg-primary/10` chip + bold title + one generic sentence, or 🚀⚡🔒 emoji as the only graphic); alternating zigzag rows (`md:flex-row-reverse`) ending in "Learn more →" to nowhere; checkmark lists of 4–6 equally weighted ✓ items. Anthropic's own frontend-design cookbook bans the "three-boxes-with-icons cliché" (prg.sh).

**Why those defaults fail.** Flat weighting kills scanning: Web Anatomy's analysis of 286 SaaS feature sections found 79% skip persona grouping, 72% are dead ends with no internal links, 56% give every feature equal weight — "a wall of cards nobody reads past the third row." Cards are wrong for comparison tasks (NN/g eyetracking: lists scan better). Icon + title + one-liner carries ~zero information scent. The swap test fails outright — "Fast, Secure, Scalable" fits any SaaS. Zigzag rows pad page length with one repeated rhetorical beat; checkmark lists imply rigor while asserting nothing; volume hides the decisive feature (40→6 features lifted trial conversion 127%, dnsk.work).

**Detection signals.**

- Structural: `h2` matching /everything you need|powerful features|why choose us|built for/i followed by a grid with exactly 3, 6, or 9 children; repeated `[icon-box] + [title ≤4 words] + [1–2 line description]` motif with description lengths varying <50% (LLM length-matching); lucide classes or emoji as the section's only graphic; ≥2 consecutive rows alternating `flex-row`/`flex-row-reverse` with "Learn more →"; a `<ul>` where every `<li>` begins with ✓/CheckCircle and holds <8 words; zero internal links out of a ≥6-feature grid.
- Class/style: `bg-primary/10` icon chips; `rounded-xl shadow-lg hover:scale-105`; `text-muted-foreground`.
- Copy: "seamless", "robust", "intuitive", "and much more"; card titles that are bare adjectives.
- Quantitative: >6 equal-weight cards on one screen; feature count exactly divisible by the column count (3n); ≥3 CTA links per features block.

**Valid exceptions.** Pricing/tier matrices and "what's included" lists (checkmarks are the correct binary idiom); integration directories of parallel items; docs and versus-competitor pages; zigzag for narrative case studies with unique-information images; small (≤4) benefit-led grids where every card links to a feature page — internal linking is the rarest differentiator (28% adoption).

**Better layout families.** Hero-feature + de-prioritized tail (1–3 decisive features at full weight, the rest in an accordion); persona grouping ("For marketers / For developers" — only 21–23% adoption); three-beat cards (outcome headline, mechanism sentence, proof line, ≤40 words); annotated real screenshots instead of icon chips; job-labeled entry cards; a comparison table when that is the task; numbered process steps for workflows.

**Mobile-specific risks.** A 6–9 card grid collapses into a monotonous single-column wall of identical cards; zigzag alternation breaks DOM order on mobile (image-image runs; screen-reader order diverges); icon chips shrink to ambiguity; equal weighting buries the decisive feature mid-scroll; dead `hover:` affordances make non-link cards feign tappability.

### 3.4 Product demonstrations

**Legitimate job.** Answer two questions: what does this actually look like, and how does it work. Screenshot, clip, or live demo is the only proof of existence an intangible product can offer; real UI outperforms abstract illustration (classic Crazy Egg case, via WeGrowth). Secondary jobs: self-qualification and platform signaling (browser frame = web app, phone frame = mobile app — earned when frame matches reality).

**Common AI-generated defaults.** The faux-browser hero shot: a dashboard screenshot in fake chrome (traffic-light dots, fake URL bar), `rounded-2xl shadow-2xl ring-1`, tilted, with 2–4 floating KPI cards orbiting (prescribed verbatim by template systems — designmd.app, heroprompts.io). The screenshot itself is often hallucinated — "Test Customer," identical users, balanced charts (UXMagic, Screenhance). Plus autoplay muted loops, "See it in action" Loom embeds, MacBook-on-gradient mockups, the same shot reused in every zigzag row, multiple demo CTAs resolving to one embed.

**Why those defaults fail.** The pattern's one job is proof, and the AI default fakes it. Hallucinated data breaks comprehension and trust (Screenhance); screenshot inflation has degraded the signal (DevBio). Tilted perspective shrinks UI text to unreadable texture. Autoplay muted loops violate NN/g video guidance (no control, unscannable, caption-less, LCP). Fake interactive demos invert a real earned convention (18% of ~5,000 B2B SaaS sites, +40% YoY — Navattic via Prospeo); a stale canned demo is worse than none. Phone-in-hand mockups waste ~60–70% of pixels on bezel and lie about platform when no app exists.

**Detection signals.**

- Structural: hero = h1 + dual CTA + image in faux browser chrome with `perspective`/`rotateX/Y`/`-rotate-3`; floating KPI cards offset from the mockup; same screenshot reused ≥3 times.
- Class/style: `rounded-2xl shadow-2xl ring-1 ring-black/10`; gradient glow behind the mockup.
- Content forensics: garbled chart labels, "Test Customer," all-zero sparklines; stretched aspect ratio.
- Media/copy: `<video autoplay muted loop playsinline>` with no controls or captions; >1 autoplaying element; Loom/YouTube iframe above the fold; ≥2 demo CTA labels on the same href.
- Platform mismatch: device frame but no app-store link anywhere. Fake interactivity: `cursor: pointer` elements with no href/handler.

**Valid exceptions.** Real, current, seeded screenshots at legible size, annotated; consistent frame systems as deliberate brand identity (Vercel, Linear); short captioned clips below the fold, one per feature claim (Figma's task GIFs); real HTML-capture demos with an owner keeping them in sync; store-mandated device screenshots; Loom for docs and warm audiences (stated length).

**Better layout families.** Annotated single screenshot with 2–3 numbered callouts; workflow slices (1:1 zoomed crops, one screen per claim); live artifacts over depiction (sandbox, template gallery); task clips with controls at the section they explain; native-format demos (terminal for dev tools); an honest front-on hero still captioned with the screen name.

**Mobile-specific risks.** Tilted mockups become illegible at 375px, chrome and bezel consuming >50% of width; floating KPI cards overflow horizontally; autoplay burns mobile data and battery; aspect-ratio-padding iframes break out of text columns; hotspot demos rely on hover that touch lacks; device frames force UI text below 8px — crop to the UI, drop the frame.

### 3.5 Social proof

**Legitimate job.** Answer the visitor's fastest silent question — "is this a real, safe company?" Verifiable external validation is a genuine trust input (Fogg's reputed credibility; NN/g credibility factors); Baymard traces 18–25% of cart abandonments to distrust. Recognized logos, linked ratings, real compliance certifications, and linked press rows are earned conventions: due diligence compressed into a glance.

**Common AI-generated defaults.** The grayscale "Trusted by" logo row under the hero — 5–8 uniform logos, `grayscale opacity-60`, sometimes an `animate-marquee` (the shipped Tailwind UI/shadcn logo-cloud block). Fictional logos: fakelogo.com sells 200 fake logos via API for placeholder walls. The stat-bar quartet: `10,247 Active Teams · 2.4M API Calls/Day · 99.97% Uptime · 4.9 Star Rating`. "As seen in" press rows earned via listicles; app-store badges with `href="#"`; static five-star SVGs, no source. AI tooling now bans these by policy (skills.ws, 2026): fabrication is the default behavior.

**Why those defaults fail.** Recognition is the entire mechanism: unknown logos transfer zero trust (Mavan); one real person beats 15+ logos (Stacked Marketer). Ubiquity flipped the signal: the row now reads "low-investment template" (AYDesign), failing the swap test cleanly. Self-curated proof is discounted (NN/g "healthy skepticism"). Implausible precision backfires: 5.0 ratings underperform 4.2–4.5 (Specflux); "99.9% uptime" is self-measured marketing theater. Baymard: a DIY seal outperformed real SSL vendors; >3–4 badge types can cut conversion 5–8%. The FTC Consumer Reviews Rule (Oct 2024) bans fake reviews and influence indicators, up to ~$51,744 per violation.

**Detection signals.**

- Structural: hero → immediately a centered grayscale logo row; 5–8 logos at uniform ~24–32px height, no links; >3 proof bands per page; proof before the product is explained; same logo set reused across unrelated sites.
- Copy: "Trusted by 10,000+ teams", "As seen in", "Backed by" sans named investors.
- Stat bar: 3–4 inline stats combining a percentage, a rating, and rounded big numbers, no source link.
- Class/style: `grayscale`, `opacity-50/60`, `hover:opacity-100`, `animate-marquee`; hard-coded star SVGs, no outbound anchor.
- Verifiability: plain-text wordmarks in a generic sans; no case-study page reachable from any logo; badge `href="#"` or 404; press logo with no article link; rating matching no G2/Capterra/Trustpilot profile.

**Valid exceptions.** Recognized, real, recent logos placed after the value proposition, with case-study links — three known names beat fifteen unknowns; real compliance badges (SOC 2, ISO 27001) for enterprise; payment/security marks at checkout for unknown brands; linked third-party ratings; press rows linking to real articles; honestly labeled "Integrates with" rows.

**Better layout families.** One deep proof (named case-study card with a metric) over fifteen shallow ones; relationship-segmented rows (customers / partners / integrations / press — the label is the claim); stat modules with every number linked to its source; proof-at-point-of-doubt placement; a 3–5 element proof budget; plain-text client lists with years for portfolios.

**Mobile-specific risks.** Logo walls collapse to ~80px smudges — recognition, the only mechanism, dies; infinite marquees fail WCAG 2.2.2.2 (no pause) and spam screen readers; 4-stat bars wrap into cramped 2×2 grids; stacked proof can consume the first 2–3 mobile viewports before any product information.

### 3.6 Comparison

**Legitimate job.** Comparison is often a necessary step before conversion (NN/g). A section is earned when the decision is compensatory — few alternatives (~5–7) weighed across multiple attributes. Earned uses: decision compression (rows-as-attributes, columns-as-options — the most scannable format); high-intent "vs" and "alternatives" queries; internal defense (what champions forward); status-quo reframing (Slack vs email); honesty — conceding competitor wins outperforms all-win tables (Team4; seomatic).

**Common AI-generated defaults.** The rigged scoreboard: header `["", "Us", "Them"]`, 5–10 rows, brand all green checks, rival all red X's, zero competitor wins. Adjective rows — "Fast", "AI-powered" — as binary glyphs. The strawman column ("Other tools", "Legacy software") — nothing is checkable. Cartoon before/after: gray spreadsheet chaos vs glowing "New way." Parity rows ("Intuitive dashboard ✓ ✓"). Template tells: `rounded-2xl shadow-xl` cards, highlighted brand column, "Most popular" badge, bare ✅/❌ cells.

**Why those defaults fail.** Zero-sum asymmetry reads as propaganda (Mettevo); conceding wins converts better (seomatic). LLMs have no competitor data, so they fabricate — each invented X is a factual error with legal exposure (UK claims must be verifiable, Team4). Adjective rows carry no decision value: "Setup: 2 min guided vs multi-week implementation" informs; "Fast ✓" does not. Parity rows dilute signal (Baymard: hide identical, highlight differences). The strawman insults the reader's actual workflow. No named rival, verifiable criteria, or concessions — reusable for any product: pure unearned default.

**Detection signals.**

- Structural: header `["", brand, "Them"|"Others"|"Traditional…"]`; brand column ≥90% ✓ with 0 ✗; rival column ≥70% ✗; >30% parity rows (all columns same glyph); >12 rows; single-adjective row labels (<4 words); cells only ✅/❌/✓/✗/—, no numbers or links; unnamed rival ("other tools", "legacy", "traditional solutions"); hero-duplicating CTA band immediately after.
- Copy: "Why switch?", "Unlike other tools…", "The old way vs the new way".
- Style/provenance: brand-tinted highlighted column in a supposedly neutral comparison; emoji glyphs with no sr-only text; zero citations or dates on any claim.

**Valid exceptions.** Own-lineup matrices (pricing tiers, real attribute data — the canonical NN/g case); named-competitor pages with verifiable criteria, ≥1 genuine competitor win, and a "who each is best for" verdict (HubSpot's Zoho page concedes features HubSpot lacks — Unkover); spec-level measurable cells; real before/after with actual artifacts; migration content addressing switching costs (Raze).

**Better layout families.** Decision page, not scoreboard (Raze): named comparison → "who each is best for" cards → criteria table stating why rows matter → objections → staged CTA. Difference-highlighted matrix (Baymard): group attributes, hide identical rows, highlight differences. Theme-grouped narrative (Federico Jorge). Status-quo story with named pains. Verdict box ("Choose X if… / Choose Y if…", including when to stay). Quantified cells — numbers over glyphs. Dynamic tables above ~5–7 alternatives; static below (NN/g).

**Mobile-specific risks.** Matrices collapse into `overflow-x` scroll with no sticky first column — row labels detach from glyphs, or the rival column goes unseen, hiding the asymmetry; stacked-card fallbacks repeat labels per card, tripling length; bare ✅/❌ mean nothing to screen readers; side-by-side before/after stacks vertically, destroying the juxtaposition — use a slider or sequential reveal.

### 3.7 Process / "How it works"

**Legitimate job.** A process section earns its place when it reduces a named uncertainty: what happens after I click, how much effort this takes, and how long until value. NN/g's visibility-of-system-status heuristic supplies the psychology: predictability and control let people decide what to do next, and stepper research shows known effort converts better than unknown effort (Babich/UX Planet). The convention is earned for genuine multi-stage services (99designs' numbered flow), setup or migration anxiety, B2B buyers who must explain "the mechanism" internally, and time-to-value claims proven step by step. In every earned case the steps carry specifics: durations, deliverables, inputs, outputs.

**Common AI-generated defaults.** A centered eyebrow ("How it works"), an h2 ("Get started in 3 simple steps"), and exactly three equal-width cards: Lucide icon in a tinted rounded square, ghost numeral ("01"), a 1–3-word imperative heading, a sub-20-word description. Variants: dashed connector lines, vertical gradient-rail timelines, scroll-jacked sticky steppers. The copy is drawn from a tiny universal vocabulary — "Sign up → Connect your tools → Get insights" — because prompt templates literally hard-code it ("HOW IT WORKS (3 steps)… action verbs: Connect, Configure, Done"). The extreme case is faux-process for a self-evident product: a notes app restating its UI as a journey.

**Why those defaults fail.** Content-free certainty reduces zero uncertainty and leaves the real questions (setup time? data required?) untouched. The section fails the swap test — it survives a brand-name change unchanged, which AI generator quality checks now treat as an explicit lint rule. High-converting homepage anatomies (Rudo) omit the 3-step row entirely; the padded section displaces a demo or proof that would actually convert. And steppers are designed for completion flows; borrowing their visual grammar for a marketing section is decoration wearing a functional pattern's clothes.

**Detection signals.**

- Structural: heading matching `/how it works|three (simple|easy) steps/i` followed by exactly 3 equal-width cards of icon + numeral + h3 + short paragraph.
- Copy: step headings from {Sign up, Connect, Configure, Launch, Automate, Track, Enjoy}; final step a benefit, not an action; no durations, inputs, or deliverables; >60% product-agnostic copy.
- Class/style: ghost numerals (`text-6xl`+`opacity-10`), `bg-primary/10 rounded-xl` icon squares, `border-dashed` connectors, `bg-gradient-to-b` rails.
- Quantitative: exactly 3 steps on a one-click product; identical CTA band before and after the section; step copy near-paraphrasing the features grid.

**Valid exceptions.** True process services (agencies, marketplaces, logistics); setup as the #1 objection, with real substeps; non-obvious differentiating mechanisms; regulated onboarding; provable "live in 5 minutes" claims — always with per-step specifics.

**Better layout families.** Annotated product walkthroughs; 10–60s micro-demo loops; expectation strips attached to the CTA ("No credit card · 5-minute setup"); PAS before/after narratives; developer quickstarts with copyable snippets; detailed timelines for real services; moving process education into in-product onboarding.

**Mobile-specific risks.** Horizontal rows collapse into stacked cards where connectors and ghost numerals lose relational meaning. Scroll-jacked steppers hog small viewports and break on touch. Guidance prefers vertical steppers on narrow screens; mobile CRO recommends collapsing secondary sections — a padded how-it-works section on mobile is pure scroll tax.

### 3.8 Pricing

**Legitimate job.** Answer three questions in under 30 seconds: what does it cost, what do I get, which option is for me. The famous conventions are earned when business reality supports them: tiered cards when a value metric genuinely segments customers (decoy and center-stage effects are documented, with reported ARPU gains; getmonetizely, NetSuite); a highlighted plan when it reflects actual sales; a monthly/annual toggle when both cadences exist; "Contact sales" when procurement, SSO, and volume negotiation are real; strikethrough anchors for genuine time-bound promos (10–30% reported lift when the anchor is real, customfit.ai); money-back guarantees when a policy exists (+14% average conversion in one A/B panel, visionary-marketing). The sin is using these as decoration severed from any real pricing structure.

**Common AI-generated defaults.** Exactly three cards — Starter/Pro/Enterprise — middle card `scale-105` with gradient ring and a "Most Popular" pill. A Monthly/Annual toggle defaulting to Annual with a green "Save 20%" chip and per-month pricing for annual billing. Five-to-eight checkmark rows per card. A third card priced "Custom" with "Contact Sales" emitted even for a $9/mo indie tool or a waitlist. Permanent "launch pricing" strikethroughs. A trust cluster ("30-Day Money-Back Guarantee", "Secure checkout", "No credit card required") regardless of whether refunds or checkout exist. Scaffold copy: "Simple, transparent pricing" / "Choose the plan that's right for you." v0's canonical example prompt literally includes "Pricing table with 3 tiers."

**Why those defaults fail.** Cargo-culted tiers around one real plan force comparison of non-differences and trigger choice overload. "Most Popular" with zero sales is fake social proof. Annual-default toggles showing per-month numbers are drip pricing's cousin. "Contact us" walls are among the most hated SaaS patterns (painonsocial). Permanent strikethroughs carry misleading-reference-price compliance exposure. Badge cosplay reduces trust; CRO guidance caps badges at 3–5. Checklist filler with >60% row overlap signals fake segmentation.

**Detection signals.**

- Structural: exactly 3 cards; middle with `scale-105`/`border-primary` ring and `/most popular|best value/i` pill; toggle with `/save \d+%/i` chip.
- Copy/style: `line-through` price with no date or "was" context; ≥3 trust phrases; h2 matching `/simple, transparent pricing/i`.
- Quantitative: the highest-signal test — card count ≠ purchasable-plan count; annual toggle with only one billing interval implemented; "Most Popular" on a domain under 6 months old; strikethrough discount >50%; guarantee badge with no linked refund policy.

**Valid exceptions.** Genuine multi-segment SaaS; real enterprise procurement (ideally "from $X" anchors); dated launch promos; honored guarantees — one badge, specific duration.

**Better layout families.** Single flat price ("$49/month. Flat rate." — Rechurn); honest Free + Paid two-card; usage-based calculator; a real comparison table when the matrix is wide; pay-once licenses; no pricing section at all when there is no price; transparent hybrid tiers with "from $X/mo" enterprise cards.

**Mobile-specific risks.** Stacked cards destroy center-stage; the cheapest plan gets the first viewport. Toggles hide prices behind a tap and cause layout jumps. Strikethrough + sale + "/mo billed annually" wraps into chaotic lines at 360px. Long checklists push the CTA dozens of rows from its price. Badge clusters look actively scammy stacked on a phone.

### 3.9 Testimonials

**Legitimate job.** Borrowed trust: answer "does this work for someone like me?" with evidence the brand cannot manufacture — a named person, a specific problem, a specific outcome. CRO literature is consistent that specificity is the persuasion mechanism; "This product is amazing" is "useless in a conversion context" (marketful). Testimonials also pace the page between feature claims and de-risk the moment before pricing. Social proof is an earned convention; the assumption that every page needs a testimonial section, regardless of whether real quotes exist, is not.

**Common AI-generated defaults.** The three-card row: heading ("Loved by teams worldwide"), exactly three identical cards with 5 gold stars, a short quote, circular avatar, first name + last name, job title. One prompt guide admits it bluntly: ask an AI for a testimonial section and it returns "three cards. Circular avatars. Quotes like 'Great service!'" (0xminds). Also: wall-of-love masonry grids (shadcnblocks lists 39+ testimonial blocks), auto-rotating carousels, giant decorative quote marks, uniform 5-star rows, fabricated counters ("Join 10,000+ happy customers"), and synthetic persona trios — "Alex Chen, Indie Hacker / Sarah Williams, Startup Founder" appears verbatim on live boilerplate sites. Avatars leak provenance: pravatar.cc, ui-avatars, randomuser.me, or uncanny identical-lighting AI headshots.

**Why those defaults fail.** Fabrication is now illegal: the FTC's 2024 rule bans fake testimonials "including those generated by AI," with civil penalties up to $51,744 per violation (InnReg; Sidley). Perfect uniformity reads as curation — purchase likelihood peaks at 4.2–4.7 stars and declines approaching 5.0; 46% of shoppers distrust perfect ratings (Spiegel/PowerReviews, via Foundry CRO). Carousels bury proof: ~1% of 3.7M tracked visitors clicked, 84–89% on slide one (Runyon). And AI-avatar aesthetics now pattern-match scam signatures documented in security literature.

**Detection signals.**

- Structural: heading `/loved by|what (our )?customers say/i` + exactly 3 identical-DOM cards with `img[rounded-full]`; auto-advancing slider with >3 slides; oversized `"` glyph on every card.
- Provenance: avatar URLs from placeholder services; zero outbound attribution links.
- Copy: quotes with no number, product name, or problem ("Game changer", "Highly recommend!").
- Quantitative: all cards exactly 5 stars; aggregate claims with no linked source; all quotes within ±20% character length.

**Valid exceptions.** Three cards are fine when content is real and varied — the crime is uniformity, not the number three. Walls of love fed by real collection pipelines with verifiable identities. Third-party star ratings (G2, Trustpilot) that link out. Manually controlled carousels for >6 items. Video testimonials, which are hard to fake. And for a brand-new product: no testimonial section at all beats fabrication every time.

**Better layout families.** Single featured pull-quote set editorially; case-study teasers with metric + link; metric-led proof ("cut deployment 4h → 20min — Sarah Chen, Eng Lead @ Dataflow"); live third-party embeds; real social posts with visible handles; distributed proof woven next to each feature claim; persona-segmented selectors.

**Mobile-specific risks.** Three-card grids become monotonous identical stacks. Auto-rotating carousels cause accidental swipes, banner blindness, and CLS. Masonry walls create enormous scroll depth. Small circular avatars lose the one authenticity cue the card had, and decorative quote marks waste the narrowest viewport on ornament.

### 3.10 FAQ

**Legitimate job.** Exactly one defensible job on a marketing page: resolve the purchase objections the main copy did not answer, so a hesitant visitor converts without leaving. Good questions are harvested from support tickets, sales calls, and search data — questions real users actually asked. Secondary jobs: deflecting repetitive support volume, and search/answer-engine visibility. The FAQ is last-resort placement: critical reassurance (refund, trial terms) belongs inline near the CTA; the FAQ holds the residual 5–7 questions.

**Common AI-generated defaults.** Centered eyebrow ("FAQ") + h2 ("Frequently asked questions") + 5–6 accordion rows (Radix/shadcn Accordion) sitting directly above the final CTA. The copy default is the generic question ladder: "What is [Product]?", "How does [Product] work?", "Is there a free trial?", "Can I cancel anytime?" — questions derivable from the template itself. Plus marketing-copy-as-questions ("Why is [Product] the best choice for teams?"), `FAQPage` JSON-LD auto-stuffed on every page, and the same 4–5 Q&A pairs duplicated across homepage, pricing, and blog.

**Why those defaults fail.** FAQs populated with questions the company wants to answer rather than questions visitors have train distrust (sitecritic.ai); a 20-question marathon "dilutes trust instead of building it." Restating hero copy as questions wastes the highest-intent scroll position — the visitor with a real objection finds nothing and leaves. Accordion-by-default compromises discoverability and adds interaction cost (NN/g); GOV.UK is blunter: "Test your content without an accordion first." FAQ-schema-as-SERP-hijack is a dead tactic — Google restricted FAQ rich results to authoritative sites in 2023 and, per 2026 SEO coverage, removed them from ordinary results; mismatched or duplicated schema is now a spam-signal risk. Thin machine-written FAQs actively hurt in answer-engine contexts: "AEO does not reward spam with question marks."

**Detection signals.**

- Structural: heading `/frequently asked|everything you need to know/i` + 4–8 accordion items in the last 20% of page height.
- Copy: ≥60% of questions matching the generic ladder with no product-specific nouns; superlative questions whose answers overlap hero copy (n-gram overlap >0.4); one-line answers (<25 words).
- Schema/provenance: `FAQPage` JSON-LD on marketing pages with <3 substantive visible Q&As or schema text not matching visible text; identical FAQ content on ≥2 pages.
- Quantitative: >10 questions on a landing page; ≥50% of questions answerable by content already above the FAQ.

**Valid exceptions.** Ecommerce product-detail FAQs (Baymard calls them "irreplaceable companions" most sites under-implement); regulated purchases (insurance, finance, B2B contracts); pricing pages with documented sales-call objections; genuine help-center pages. Accordions themselves are earned at 10+ questions or on mobile.

**Better layout families.** Inline objection placement at the CTA; short open-list FAQs (plain h3 + paragraph, fully visible) for under 1.5 viewport heights; earned accordions with first item open and multi-panel expansion; objection-seeded questions in customers' words, ordered by frequency; dedicated help centers; honest comparison or fit/unfit blocks instead of rhetorical "Why choose us?" entries.

**Mobile-specific risks.** Chevron-only hit areas under 44px; auto-closing accordions force rescrolling to compare answers; long accordions push the final CTA down dozens of scroll heights; client-rendered accordion bodies can be invisible to crawlers and answer engines; per-page JSON-LD inflates mobile payload.

### 3.11 Calls to action

**Legitimate job.** Give a decided — or nearly decided — visitor an obvious low-friction next step at the moment of readiness. Repetition is an earned convention: a GoodUI test found repeated CTAs lifted conversion 7% → 12.8% (Metrifi), and CRO consensus converges on one primary action at 2–3 natural decision points. A persistent nav CTA is earned wayfinding; a final CTA after the proof reaches the highest-intent segment. It fails when repetition is mechanical rather than decision-point-tied, or the ask ignores decision stage.

**Common AI-generated defaults.** The metronome band: an identical full-width CTA band re-emitted after every section, 4–6 times per page. The gradient finale: centered "Ready to get started?" + "Join 10,000+ teams…" + pill button on a purple-blue gradient — the stock Tailwind CTA component. Context-free button copy ("Get started", "Learn more") reusable for any brand. Carpet-bombing: the same button in nav, hero, mid-band, finale, footer. Competing hero asks at equal weight regardless of PLG or sales-led motion. The vestigial newsletter box with no value exchange, emitted even when none exists.

**Why those defaults fail.** Banner blindness is format-blindness: users filter anything ad-shaped, and a gradient band with centered text looks like a display ad; the third identical band is filtered before it is read (NN/g; Benway & Lane: banner-style links found 58% of the time vs 94% for standard links). Past saturation, repetition reads as nagging — same CTA twice in one viewport is over the line (Metrifi). Wrong-stage asks leak conversions; top-performing SaaS heroes show ONE action (Orbix, 50-site teardown). Footer newsletter forms convert 0.5–2% vs 5–15% with a specific exchange (Exmoor Web).

**Detection signals.**

- Structural: >3 full-width CTA bands per page, or the same band after ≥75% of sections; final section = centered h2 + p + 1–2 buttons + gradient background, nothing else; same label ≥4 times across nav/hero/bands/footer; hero with 2+ equal-weight buttons.
- Copy: labels ∈ {"Get started", "Learn more", "Start free trial"}; "Join 10,000+…" filler.
- Class/style: indigo-violet filled CTAs (slop-detect's "VibeCode Purple" rule), `bg-gradient-to-r from-purple` finale bands, `rounded-full` pills site-wide.
- Quantitative: same CTA twice within one 900px viewport; "Start free trial" with no existing trial.

**Valid exceptions.** Long-form and high-ticket pages legitimately repeat the same CTA every 2–3 sections; multi-audience homepages may carry 3–5 distinct CTAs; editorial sites earn newsletter boxes when the newsletter is the product; sticky nav and bottom CTAs are earned persistence; "Book a demo" everywhere is correct for genuinely sales-led products. The sin is emitting an ask without knowing the motion.

**Better layout families.** Decision-point repetition with escalating risk-reducers nearby; inline contextual text-level CTAs that bypass banner filtering; stage-laddered asks; specific verb + object + qualifier copy ("Start my free 30-day trial"); newsletter-as-exchange with named promise and frequency; the quiet finale — plain background, specific value restatement, one button.

**Mobile-specific risks.** Each band costs a full mobile viewport, accelerating pattern-ignore. Sticky bottom CTA + cookie banner + chat widget stack into content-obscuring chrome. Sub-44px pill targets, wrapping primary+ghost pairs, gradient bands failing WCAG contrast, peak "faux ad" filtering.

### 3.12 Contact

**Legitimate job.** Three distinct jobs. Trust proof: Stanford's Web Credibility guidelines list "make it easy to contact you" as a top-10 factor; contact information is consumed as a signal, and its absence reads as a scam tell. Routing: getting a specific inquiry to the right inbox with qualifying context — where a form legitimately beats a naked email link. Conversion: embedded scheduling reportedly beats "we'll be in touch" forms by 20–40%; in-session bookers show up 2–3× more (chrisjaeger.com; Splitforms). Portfolios often do fine with a footer email.

**Common AI-generated defaults.** One molecule everywhere: h2 "Get in touch" + "We'd love to hear from you" + a two-column grid — left, a three-field Name/Email/Message form; right, three icon rows with "123 Main Street, San Francisco, CA", "+1 (555) 123-4567", "hello@company.com". Optionally a markerless Maps iframe and a default chat bubble as sole channel, plus a "Contact us" band immediately above — three doors to the same room. Tailwind UI ships eight variants of this molecule; generators reproduce it.

**Why those defaults fail.** A context-free form cannot route; teardown guidance recommends either three minimal fields or a short qualifier set with a scheduler, never the shapeless middle. A form-only contact page on an unknown brand is a credibility negative: scam-detection practice treats unverifiable addresses as a red flag, and DoubleVerify's AI-content-farm analysis used "contact section refers to a different site name" as a template tell. Fake precision is worse than none — fictional addresses risk Google listing suspension. Form-only asymmetry is fatal for freelancers whose personal email is the trust signal. An unstaffed chat bubble is an unmanned doorbell.

**Detection signals.**

- Structural: the heading + sub + 2-col grid(form, info-list) molecule matching Tailwind UI near-verbatim; fields ⊆ {name, email, subject, message} with no topic select or SLA near submit; `<form>` with `action="#"` or toast-only handler; exactly 3 MapPin/Phone/Mail icon rows; chat widget with no other channel; >2 contact-equivalent CTAs on one page.
- Provenance: Maps iframe with generic or mismatched address; `123 Main St` / `(555)` patterns; contact text naming a different company.
- Copy: "We'd love to hear from you", "responds within 24 hours".

**Valid exceptions.** A labeled "Contact" nav item is pure wayfinding — renaming it is a loss. Forms earn their keep when they genuinely route (topic dropdowns, order IDs, 2–4 intake qualifiers). Real local businesses should show address + map + phone prominently — the canonical earned use of the triad. Staffed or intent-mapped chat on pricing and checkout pages.

**Better layout families.** Channel chooser with expectations per door; inline scheduler embeds (outbound links lose a reported 30–40%); routed intake forms whose success state names the next step; direct human contact for portfolios; self-serve help-center search above contact options; real NAP blocks for local business.

**Mobile-specific risks.** Chat bubbles collide with sticky CTAs and cookie banners; proactive pop-ups on small screens are the highest-annoyance configuration. Map iframes trap scroll gestures. Missing `type="email"`/`tel:` markup degrades mobile keyboards. "Form left, info right" stacks into info-below-form, burying the phone number call-driven businesses need on top.

### 3.13 Footers

**Legitimate job.** The footer is a navigation component, not decoration. NN/g documents three genuine uses: a second chance to convince, a last resort for hard-to-find content (jobs, investors, press), and a deliberate destination for contact details. It is the expected home for non-primary personas. Baymard: a distinct subgroup treats the footer as "the place to go" for shipping and returns, scanning by keyword — 20% of e-commerce sites fail them behind generic "Help/FAQ" links. Secondary jobs: compliance and trust. Conventional labels are usability, not cliché.

**Common AI-generated defaults.** The template ecosystem converged first: Tailwind UI's footer set is almost entirely "4-column" variants. The emitted default: a Product/Company/Resources/Legal link farm (often `href="#"` on a one-pager); sitemap-mirroring of the anchors just scrolled; newsletter form plus 4–5 generic social SVGs regardless of whether accounts exist; the giant 100vw wordmark — a real agency trend (Wix's "Big Footer™") AI emits as filler; "Made with ♥ in San Francisco"; the © + Privacy/Terms/Cookies trio; and a pre-footer CTA band duplicating the third ask.

**Why those defaults fail.** Link farms without destinations train users to distrust the footer — the opposite of wayfinding — and keyword scanners are impeded by vague "Resources" headers. Sitemap mirroring adds zero routes. Newsletter forms and social icons with no audience are props; each dead icon is a broken promise. The giant wordmark, an editorial statement misapplied, spends 30–40% of mobile viewport on a second logo. "Made with ♥" is unearned intimacy. Fat footers are SEO cargo cult: footer links pass reduced weight; excessive ones are a spam signal.

**Detection signals.**

- Structural: `<footer>` with `grid md:grid-cols-4/5` whose headings are Product/Company/Resources/Legal; email input with no detectable ESP integration; brand name re-rendered ≥50vw wide; a CTA band as the immediately preceding sibling of `<footer>`.
- Link integrity: >30% of links resolving to `#`, self-anchors, or 404; ≥4 brand icons linking to `#` or root domains.
- Quantitative: footer–nav Jaccard overlap >0.7 on a ≤6-page site; footer height >25% of page height.
- Copy: "Made with ♥", "Join 10,000+ subscribers".

**Valid exceptions.** Four-column footers are earned on e-commerce/SaaS with real depth — direct Return Policy/Shipping links serve real users. Fat footers suit content-rich sites (NN/g: "an expected and obliging anchor"). Giant wordmarks are earned on brand-led sites (fashion, agencies, portfolios). Mini footers are a designed choice on app-like surfaces. "Made with ♥" is fine on genuine indie sites.

**Better layout families.** Task-based mini footer (contact email, 2–3 live links, legal line); persona-segmented columns (For developers / For investors / Press); support-keyword footers for e-commerce; contact-forward footers for services; contextual footers; brand-mark crescendo replacing, not stacked on, the link farm. Rule of thumb: every footer element should answer "which user, on which task, needs this here?"

**Mobile-specific risks.** Four columns collapse into a 3–4 screen scroll marathon; AI output stacks without restructuring. Giant wordmarks consume a full zero-information viewport. Icon rows wrap into sub-44px clusters. Inline newsletter forms break below ~360px. Hamburger menus hide the nav, so footers are used *more* on mobile — restructure with real-link accordions, do not amputate.

## 4. Component-Level Failure Ledger

This ledger audits the recurring components of AI-generated marketing pages one by one. Each entry classifies the pattern as **Unearned default**, **Earned convention — conditional**, **Context-dependent**, or **Decorative slop**, using the report's standing test: swap the logo for a competitor's, and if nothing breaks, the component was sampled from the training-data median rather than designed from content. Detection signals are stated so they can be linted from markup, class strings, or copy.

### 4.1 Uniform card trio

**Pattern name.** Uniform card trio (3-column equal-width feature grid).
**Section/category.** Features, benefits, "why us", process sections.
**Classification.** Unearned default: emitted for every section regardless of content; identical for any brand.
**Failure mechanism.** Cards de-emphasize ranking and are less scannable than lists, failing exactly where users compare or search (NN/g). Six identical cards assert six equally important features; hierarchy flattens and eyes zig-zag with no entry point. Web Anatomy's 286-section corpus: 56% weight every item equally, 72% are dead ends with no links.
**Detection signals.** `grid md:grid-cols-3` with ≥3 children sharing identical structure (svg + h3 + p ≤25 words); `rounded-2xl` plus `shadow-lg|xl` on ≥3 siblings; ≥2 card-grid sections per page; body word-count variance ≈ 0; header matching /everything you need|why choose us/i.
**Appropriate use cases.** Linked teasers to detail pages (blogs, catalogs, portfolios); integration directories of genuinely parallel items.
**Better alternatives.** Vertical or definition lists; a lead feature block plus compact 2-column secondary list; comparison tables.
**Sources.** NN/g, Cards: UI-Component Definition — https://www.nngroup.com/articles/cards-component/; Web Anatomy, 286 Features Sections — https://www.webanatomy.ai/best-landing-pages/sections/features; dev.to, Why AI Landing Pages Look the Same — https://dev.to/_46ea277e677b888e0cd13/why-every-ai-generated-landing-page-looks-the-same-and-how-to-fix-it-1kmo
**Confidence.** High: NN/g primary research plus a quantified corpus agree.

### 4.2 Bento feature grid

**Pattern name.** Bento grid (mixed-size tile layout).
**Section/category.** Feature showcases, product overviews.
**Classification.** Context-dependent: earned only when tiles genuinely differ in kind and size maps to importance.
**Failure mechanism.** The pattern's one rule is size = hierarchy (SaaSFrame, 43 implementations reviewed). AI output assigns `col-span-2`/`row-span-2` for visual variety while every tile holds the same icon+title+text formula, so heterogeneity is decorative and hierarchy is actively obscured. Sequential content (step 1 → 2 → 3) loses ordering; "no clear hierarchy" and "too many elements" are the top catalogued failure modes.
**Detection signals.** Grid with `col-span-`/`row-span-` where all tiles share one content template; largest tile's heading is not the primary value proposition; tile count outside 4–8; max tile <1.5× median area; `grid-auto-flow: dense` diverging visual from DOM order.
**Appropriate use cases.** Dashboards; genuinely mixed-media showcases with one clear hero tile (video vs. stat vs. quote); playful portfolio pages.
**Better alternatives.** Hero-feature block plus supporting list; numbered step rows for processes.
**Sources.** SaaSFrame, Designing Bento Grids That Work — https://www.saasframe.io/blog/designing-bento-grids-that-actually-work-a-2026-practical-guide; superfiles, The Bento Grid Era — https://superfiles.in/bento-grid-ui-design-trend.php; adminlte, shadcn/ui Block Libraries — https://adminlte.io/blog/shadcn-ui-block-libraries/
**Confidence.** Medium-high: consistent practitioner warnings; no large empirical study.

### 4.3 Hover-lift cards

**Pattern name.** Hover-lift (`hover:-translate-y-1 hover:shadow-xl transition`) on every card.
**Section/category.** Any card grid: features, testimonials, pricing.
**Classification.** Decorative slop: affordance theater applied to elements that lead nowhere.
**Failure mechanism.** Elevation on hover signals clickability; on non-interactive cards it lies. On touch devices the state does not exist, and `:hover` can stick after a tap, leaving cards permanently "lifted". When hover-lift is the page's only interaction, it is motion compensating for static content, and the heavy chrome (`shadow-xl` + `rounded-2xl`) pushes toward one card per mobile viewport.
**Detection signals.** `hover:-translate-y`, `hover:scale-`, or `hover:shadow-` on elements with no link, button, or click handler (lint: hover transform ∧ ¬interactive).
**Appropriate use cases.** Genuine whole-card links in teaser grids, with focus-visible equivalents.
**Better alternatives.** Make the card a real link with honest hover/focus styles, or drop the motion and spend the attention on hierarchy.
**Sources.** NN/g, Cards: UI-Component Definition — https://www.nngroup.com/articles/cards-component/; adminlte, shadcn/ui Block Libraries — https://adminlte.io/blog/shadcn-ui-block-libraries/
**Confidence.** Medium: sound interaction-design reasoning and observable template defaults; few dedicated studies.

### 4.4 Icon + title + text card formula

**Pattern name.** Icon chip + bold title + two muted lines (the Lucide card).
**Section/category.** Features and benefits grids.
**Classification.** Unearned default: Anthropic's own frontend-design cookbook bans the "three-boxes-with-icons cliché".
**Failure mechanism.** A decorative stroke icon, a bare noun ("Analytics"), and a vague sentence carry near-zero information scent; icons are assigned by keyword matching (Zap, Shield, Globe), not meaning. The formula passes the interchangeability test perfectly: "Fast, Secure, Scalable, Integrations" fits every SaaS ever made, so the section describes the category instead of the product.
**Detection signals.** ≥3 icons from the default lucide-react stroke set, no custom artwork; `bg-primary/10` icon chips; `text-muted-foreground` bodies; titles that are bare nouns or gerunds; emoji (🚀⚡🔒📊) as the only graphics; zero internal links out of a ≥6-feature grid.
**Appropriate use cases.** Conceptual features with no showable UI (security, API); ≤4 truly parallel benefit-led cards linking to feature pages.
**Better alternatives.** Annotated real screenshots; three-beat cards (outcome headline, mechanism sentence, proof line, ≤40 words).
**Sources.** prg.sh, Same Purple Gradient Website — https://prg.sh/ramblings/Why-Your-AI-Keeps-Building-the-Same-Purple-Gradient-Website; Web Anatomy, 286 Features Sections — https://www.webanatomy.ai/best-landing-pages/sections/features; shadcnblocks Feature13 — https://www.shadcnblocks.com/block/feature13
**Confidence.** High: independent 2025–2026 sources, including AI tooling's own documentation, converge.

### 4.5 Checkmark bullet lists

**Pattern name.** Green-check bullet list ("✓ Easy setup ✓ 24/7 support ✓ Cancel anytime").
**Section/category.** Feature lists beside screenshots; pricing tier inclusions.
**Classification.** Earned convention — conditional: the correct idiom for binary inclusion in pricing matrices; slop as vibe filler.
**Failure mechanism.** Table-stakes noun phrases with no outcome or proof imply rigor while asserting nothing differentiating; per Merge's teardown rule, a list that could be swapped onto a competitor's site describes the category, not the product. Inside pricing cards, rows repeated across all tiers fake segmentation.
**Detection signals.** ≥80% of `li` beginning with an identical Check SVG in a `rounded-full` badge; items that are bare noun phrases <5 words with no number; >60% checklist-row overlap across pricing tiers.
**Appropriate use cases.** Pricing "what's included" rows that genuinely differ and map to buyer segments; binary spec facts.
**Better alternatives.** Outcome-led bullets, each stating a result with a number; ruthless cutting (one documented case cut 40 features to 6 and lifted trial conversion 127%).
**Sources.** SaaSFrame, Pricing Page UI Patterns — https://www.saasframe.io/blog/10-ui-patterns-that-drive-pricing-pages-conversions-in-2026; Merge, SaaS Landing Page Mistakes — https://merge.rocks/blog/we-reviewed-dozens-of-saas-landing-pages-here-are-the-5-mistakes-we-keep-seeing; dnsk.work — https://dnsk.work/blog/who-are-you-designing-for
**Confidence.** Medium: pricing-UX guidance and teardowns agree; no isolated large-scale study.

### 4.6 Tabbed feature panels

**Pattern name.** Pill-tab feature switcher ("Analytics / Automation / Collaboration / Security").
**Section/category.** Product feature deep-dives on marketing pages.
**Classification.** Unearned default on marketing pages; earned in docs and settings.
**Failure mechanism.** NN/g: the default tab receives disproportionate attention and non-default tabs "may be ignored", so critical content must not live there. AI panels invert this, burying two-thirds of the feature copy behind undifferentiated generic-noun labels; only the first panel renders on load. Tabs also tax short-term memory when users need to compare across panels.
**Detection signals.** >50% of the page's feature text inside unselected tab panels; labels that are single generic nouns from {Analytics, Automation, Collaboration, Security, Integrations, Workflows}; `rounded-full` pill tab bar with sliding indicator.
**Appropriate use cases.** NN/g's criteria: 2–4 groupings, short labels, supplemental non-default content, no cross-tab comparison (per-OS install instructions, code samples).
**Better alternatives.** Anchor-linked long page with sticky section nav; accordions on mobile where tabs overflow.
**Sources.** NN/g, Tabs, Used Right — https://www.nngroup.com/articles/tabs-used-right/; 21st-frontend-design SKILL.md — https://github.com/sants2001/21st-frontend-design/blob/main/SKILL.md
**Confidence.** Medium-high: authoritative NN/g guidance resting on principles and observation more than large datasets.

### 4.7 Auto-advancing carousels

**Pattern name.** Interval-driven hero/feature/testimonial slider with dot pagination.
**Section/category.** Hero sliders, testimonial rotators, logo strips.
**Classification.** Unearned default: among the best-measured failures in interface design.
**Failure mechanism.** Runyon's Notre Dame tracking: ~1% of visitors clicked at all, 84% of clicks on slide 1. A/B tests show static images winning decisively (Conversionista: 40% vs 2% clicks). NN/g's Siemens case shows why: auto-rotation reads as advertisement (banner blindness) and strips control, hitting motor-impaired and non-native readers hardest. Brad Frost: carousels are organizational crutches avoiding the decision of what matters; an AI with no stakeholders still reproduces the appeasement.
**Detection signals.** `setInterval`/`setTimeout` driving slide state; `autoplay`/`loop` props on swiper/embla; dot-only pagination with dots <24px; ≥2 auto-rotating components on one page.
**Appropriate use cases.** Manual, user-controlled galleries with obvious controls (PDP images); mobile card rails with visible overflow hints.
**Better alternatives.** Static stacked sections (Baymard's recommendation); single hero panel plus sub-feature row.
**Sources.** Erik Runyon, Carousel Interaction Stats — https://erikrunyon.com/2013/01/carousel-interaction-stats/; NN/g, Auto-Forwarding Carousels — https://www.nngroup.com/articles/auto-forwarding/; Brad Frost, Carousels — https://bradfrost.com/blog/post/carousels/
**Confidence.** High: multiple independent datasets plus NN/g converge across a decade.

### 4.8 Logo walls and marquees

**Pattern name.** Grayscale "Trusted by" logo row, static or infinite marquee.
**Section/category.** Social proof band directly under the hero.
**Classification.** Context-dependent: earned peripheral proof when logos are recognized and linked; unearned default as decoration.
**Failure mechanism.** Recognition is the entire mechanism: unrecognized logos transfer zero trust and are skimmed reflexively. Ubiquity flipped the signal; the same row on every templated page now reads as "low-investment template" (AYDesign). Faking is industrialized: fakelogo.com sells 200 fictional logos via API for placeholder walls. Infinite marquees add WCAG 2.2.2 failures (no pause) and screen-reader noise.
**Detection signals.** Grayscale row ≤1 section below the hero; 5–8 uniform logos, `grayscale opacity-60`, zero outbound links; "Trusted by [round number]+ teams"; track rendered twice (one copy `aria-hidden`) with `animate-marquee` keyframes.
**Appropriate use cases.** Real, recognized, recent logos after the value proposition, linked to case studies; honestly labeled "Integrates with" rows.
**Better alternatives.** One named case study with a metric (auditors report 3.2× better conversion than logo rows); relationship-segmented groups.
**Sources.** fakelogo.com, Social Proof Examples — https://fakelogo.com/social-proof-examples; AYDesign, SaaS Patterns 2026 — https://www.aydesign.ai/blog/modern-saas-landing-page-design-patterns-2026; Stacked Marketer — https://www.stackedmarketer.com/the-crews-insights/should-you-use-client-logos-on-your-website/
**Confidence.** High for the default and mechanism; medium for the 3.2× figure (single auditor source).

### 4.9 Stat bars

**Pattern name.** Inline stat quartet ("10,247 Active Teams · 2.4M API Calls/Day · 99.97% Uptime · 4.9★").
**Section/category.** Social proof band, often paired with the logo wall.
**Classification.** Unearned default: self-asserted numbers with no source, often placed before the product is explained.
**Failure mechanism.** NN/g finds users read company-selected proof with "healthy skepticism"; unlinked numbers are assertions, not evidence. Implausible precision backfires: perfect 5.0 ratings underperform 4.2–4.5, and "99.9% uptime" is self-measured marketing (≈8.76 h/year at ping level). AI tooling now bans invented "10,000+ teams" claims by policy, an admission that fabrication is the default.
**Detection signals.** 3–4 inline stats mixing a percentage, a rating, and rounded big numbers with no source link; strings matching /99\.\d% uptime/, /[\d,]+\+ (teams|users)/; no status page, G2 profile, or dated report behind any number.
**Appropriate use cases.** Verifiable stat modules where every number links to its source.
**Better alternatives.** One deep metric-led proof ("cut deploy time 4h → 20min") attributed to a named customer; proof-at-point-of-doubt placement.
**Sources.** fakelogo.com, Social Proof Examples — https://fakelogo.com/social-proof-examples; Specflux, Social Proof Engineering — https://www.specflux.com/web-design/social-proof-web-design/; skills.ws, Landing Page Builder skill — https://www.skills.ws/skills/landing-page-builder
**Confidence.** Medium-high: strong consensus and policy evidence; sweet-spot figures are secondary CRO reporting.

### 4.10 Testimonial three-card grids

**Pattern name.** "Loved by teams worldwide" + exactly three identical quote cards (stars, avatar, name, title).
**Section/category.** Testimonial section.
**Classification.** Unearned default: emitted whether or not real quotes exist; content is reverse-engineered to fill slots.
**Failure mechanism.** Uniformity reads as curation: purchase likelihood peaks at 4.2–4.7 stars and declines approaching 5.0; 46% of shoppers distrust perfect ratings. Synthetic personas ("Sarah K., CEO at TechFlow") with pravatar.cc avatars are a scam-site signature. Fabrication is illegal: the FTC's 2024 rule bans fake testimonials "including those generated by AI", up to $51,744 per violation. Three cards plus stars fit any dentist's site unchanged.
**Detection signals.** /loved by|what (our )?customers say/i heading + exactly 3 identical-DOM cards, `rounded-full` avatars; avatar URLs from pravatar.cc/ui-avatars/randomuser; all cards exactly 5 stars; quotes with "game-changer" but no metric or linked identity; lengths within ±20%.
**Appropriate use cases.** Real, varied quotes with verifiable identities; walls of love from genuine collection pipelines.
**Better alternatives.** Single featured pull-quote set editorially; metric-led proof; third-party review embeds.
**Sources.** Foundry CRO, Proof Benchmarks 2026 — https://foundrycro.com/blog/landing-page-social-proof-benchmarks-2026/; InnReg, FTC Fake Reviews Rule — https://www.innreg.com/resources/regulatory-updates/ftc-implements-final-rule-banning-fake-reviews-and-testimonials; 0xminds, AI Testimonial Prompts — https://0xminds.com/de/blog/guides/ai-testimonial-section-prompts-guide
**Confidence.** High: large-sample ratings research plus primary regulatory sources.

### 4.11 Pricing tier cards, "Most Popular" pill, and billing toggle

**Pattern name.** Three pricing cards, middle scaled with gradient ring + "Most Popular" pill, plus annual-default billing toggle.
**Section/category.** Pricing section.
**Classification.** Earned convention — conditional: decoy and center-stage effects are real for truly segmented products; cargo-culted otherwise.
**Failure mechanism.** Three cards around one real plan force comparison of non-differences; overload reduces conversion. "Most Popular" with zero sales is fake social proof. "Enterprise / Contact Sales" on a $9/mo tool cosplays procurement. The annual-default toggle quoting per-month prices is drip-pricing's cousin: shown ≠ charged, often with one interval real.
**Detection signals.** Exactly 3 cards, middle `scale-105` + pill /most popular|best value/i; name → price/mo → ✓ rows → button anatomy ×3; card count ≠ purchasable-plan count (highest-signal test); annual-default toggle with /save \d+%/i chip; price without "billed annually" framing.
**Appropriate use cases.** Genuine multi-segment SaaS; real SSO/procurement enterprise tiers; honest dual cadences.
**Better alternatives.** Single flat price; free + paid two-card; usage calculator; comparison table; no section when no price exists.
**Sources.** GetMonetizely, The Decoy Effect — https://www.getmonetizely.com/articles/the-decoy-effect-how-strategic-pricing-tiers-can-maximize-revenue; PainOnSocial, Pricing Complaints — https://painonsocial.com/blog/saas-pricing-complaints-reddit; Codebrand, AI Website Builders — https://www.codebrand.us/blog/ai-website-builders-v0-cursor-2025/
**Confidence.** Medium-high: strong template/generator evidence; no systematic corpus measurement.

### 4.12 FAQ accordions (as component)

**Pattern name.** Accordion-by-default FAQ block (`<details>` or Radix accordion with chevrons).
**Section/category.** FAQ section, usually the last 20% of the page before the final CTA.
**Classification.** Earned convention — conditional: earned for genuinely long optional Q&A; unearned as a tidiness reflex for five short answers.
**Failure mechanism.** NN/g: collapsed panels compromise discoverability; each expansion adds interaction cost. GOV.UK: "test your content without an accordion first." AI fills the tidy accordion with the generic question ladder ("What is X?", "Is there a free trial?"), wasting the highest-intent scroll zone. Auto-emitted `FAQPage` JSON-LD on every page is now dead or risky; rich results were removed in 2026.
**Detection signals.** Heading /frequently asked|everything you need to know/i + 4–8 accordion items; ≥60% of questions on the generic ladder with no product-specific nouns; answers <25 words; schema duplicated across pages.
**Appropriate use cases.** 8+ real questions, mobile FAQs, regulated purchases, support centers; first item open, multiple panels allowed.
**Better alternatives.** Inline objection microcopy at the CTA/price; short open-list FAQ; questions seeded from support tickets.
**Sources.** NN/g, Accordions on Desktop — https://www.nngroup.com/articles/accordions-on-desktop/; GOV.UK Accordion — https://design-system.service.gov.uk/components/accordion/; SiteCritic, FAQ Design — https://www.sitecritic.ai/blog/website-faq-design-where-to-place-it-what-to-include
**Confidence.** High: NN/g, GOV.UK, and CRO literature converge.

### 4.13 Fake-chronology timelines

**Pattern name.** Vertical dotted-rail timeline with Step 1..N or year nodes labeling parallel features.
**Section/category.** "How it works", "Our Journey", feature storytelling.
**Classification.** Decorative slop when items are not temporal; earned for real chronology.
**Failure mechanism.** A timeline without time is a lie of form: the reader's pattern-matcher ("sequence matters here") is activated and then unrewarded, leaving rail, dots, and date badges as pure ornament. Block libraries encourage the decoupling; shadcnblocks markets "Feature Timeline" blocks explicitly "where feature content needs a distinct visual treatment". The company-history variant ("Founded 2021 → Seed → 10k users") on a two-year-old startup's homepage is credibility theater.
**Detection signals.** Vertical rail (`border-l` or `before:` pseudo-element) + dot nodes labeled with steps or years where items are undated parallel features; "Journey/Milestones" section with ≤5 entries of <20 words each on a company <5 years old.
**Appropriate use cases.** Changelogs, release notes, public roadmaps, genuine history pages.
**Better alternatives.** Numbered step cards for non-temporal processes; compact changelog lists; delete fake-history sections.
**Sources.** shadcnblocks, Feature Timeline Blocks — https://www.shadcnblocks.com/blocks/feature/timeline; Overpass Studio, Why SaaS Websites Look the Same — https://www.overpass.studio/blog/why-saas-websites-look-the-same
**Confidence.** Medium: strong form-without-content argument; no dedicated user-testing of timelines.

### 4.14 Sticky-scroll split sections

**Pattern name.** Text steps scroll on one side while a pinned mockup cross-fades on the other.
**Section/category.** Feature tours, product walkthroughs.
**Classification.** Context-dependent: earned when the pinned element is referential; scroll theater when decorative.
**Failure mechanism.** NN/g's scrolljacking research: the pattern is tolerated only with functional progressive disclosure; decorative scrolljacks disorient, task-oriented users were "highly annoyed", and altered scroll rate paired with reading text was the worst combination observed. A pinned laptop cross-fading between near-identical dashboards charges interaction cost and returns no information; long scrolljacks were interpreted as bugs. Mobile is worse: longer jacks, slower loads, no nav escape hatch.
**Detection signals.** `sticky top-0` on a media column plus ≥3 scrolling text blocks with opacity cross-fades; section height ≥300vh with a sticky viewport-height panel; GSAP ScrollTrigger pins; >50% of swapped images near-identical; identical CTA in pinned narrative and hero.
**Appropriate use cases.** Annotated product breakdowns, maps, data-viz scrollytelling where each step changes the pinned visual (Pudding/NYT tradition).
**Better alternatives.** User-controlled tab or accordion switchers; static annotated screenshots.
**Sources.** NN/g, Scrolljacking 101 — https://www.nngroup.com/articles/scrolljacking-101/; Pudding, Scrollytelling with Sticky — https://pudding.cool/process/scrollytelling-sticky/; Lovable, Scrolling Designs Guide — https://lovable.dev/guides/scrolling-designs-patterns-when-to-use
**Confidence.** High: NN/g primary usability research with named failing examples.

### 4.15 50/50 zigzag rows

**Pattern name.** Three to five alternating image-left/image-right rows at half width.
**Section/category.** Feature narrative sections.
**Classification.** Context-dependent: earned when imagery is informational; measurably harmful with decorative imagery.
**Failure mechanism.** NN/g eyetracking: with decorative images, zigzag made images harder to ignore, an "images as obstacle course" effect with stumble and residual fixations; aligned layouts let users skip decorative imagery efficiently. AI defaults to zigzag plus stock illustration, the worst cell of that 2×2. Each row repeats the same beat (feature → benefit → "Learn more →" to nowhere), and mobile DOM order frequently scrambles the alternation into image-image runs.
**Detection signals.** ≥3 consecutive rows alternating `flex-row`/`flex-row-reverse` at ~50/50 width with `rounded-2xl shadow-xl` images; every row ending in "Learn more →"; the same screenshot reused across ≥3 rows.
**Appropriate use cases.** Two to three rows maximum; informational images users need to study; narrative case studies.
**Better alternatives.** Aligned image-text lists for decorative brand texture (NN/g's direct recommendation); hero-feature block plus supporting list.
**Sources.** NN/g, Zigzag Image–Text Layouts — https://www.nngroup.com/articles/zigzag-page-layout/; Landy-ai, Landing Page Structure — https://www.landy-ai.com/blog/landing-page-structure
**Confidence.** High: NN/g eyetracking with ~30 participants per variant.

### 4.16 Faux browser-chrome frames and device mockups

**Pattern name.** Fake browser-chrome wrapper (traffic-light dots, URL bar), often tilted, or centered device renders.
**Section/category.** Hero product shot; demo sections.
**Classification.** Context-dependent: earned as platform signaling and consistent brand frame systems; slop as decoration around hallucinated UI.
**Failure mechanism.** The job is proof; the AI default fakes it: the "screenshot" is itself generated, with "Test Customer" data and balanced charts prospects pattern-match instantly. Tilted perspective shrinks UI text to unreadable texture. A MacBook on a flat gradient is "a tired pattern" (Screenhance); a phone render with no real app lies about platform and wastes 60–70% of pixels on bezel.
**Detection signals.** Three dots + URL-bar div with `rounded-2xl shadow-2xl ring-1` plus `perspective`/`rotateX`/`-rotate-3`; floating KPI cards; garbled chart labels or "Test Customer"; device frame but no App Store/Play link; same shot in ≥3 sections.
**Appropriate use cases.** Real, current screenshots at legible size; consistent frame systems as identity (Vercel/Linear); mockups when the device is the product.
**Better alternatives.** Flat front-on annotated screenshot at 100% scale; workflow-slice crops; live sandbox.
**Sources.** PostKit, Browser Mockup — https://www.getpostkit.com/glossary/browser-mockup; Screenhance — https://screenhance.com/macbook-mockup-generator; UXMagic, Mockup Tools — https://uxmagic.ai/blog/best-mockup-tools-2026-fast-ui-workflows
**Confidence.** Medium-high: documented across template ecosystems; sameness quantification anecdotal.

### 4.17 CTA bands

**Pattern name.** Full-width gradient band ("Ready to get started?" + button) re-emitted after multiple sections.
**Section/category.** Mid-page and final conversion bands.
**Classification.** Earned convention — conditional: repeating one action at 2–3 decision points is earned (GoodUI/Metrifi: 7% → 12.8%); mechanical re-emission is slop.
**Failure mechanism.** Banner blindness is driven by predictability: a full-width gradient band with centered text and button is indistinguishable from a display ad; the third identical band is filtered before reading (Benway & Lane: 58% vs 94% found). The stock copy ("Ready to get started? / Join 10,000+ teams / Start Free") is the catalog Tailwind component, duplicated across nav, hero, finale, and footer past the twice-per-viewport nag threshold.
**Detection signals.** >3 full-width CTA bands per page; finale = centered h2 + p + 1–2 buttons on `bg-gradient-to-r from-(purple|indigo|blue)`; same label ≥4 times; labels from {"Get started", "Learn more"}.
**Appropriate use cases.** Long sales pages repeating one action at real decision points; sticky nav CTA.
**Better alternatives.** Decision-point repetition with escalating risk-reducers; inline contextual CTAs; a quiet finale.
**Sources.** NN/g, Banner Blindness — https://www.nngroup.com/articles/banner-blindness-old-and-new-findings/; Metrifi, Repeat Your CTA — https://metrifi.com/blog/research-shows-if-you-repeat-your-call-to-action-more-people-will-convert/; CTAExamples catalog — https://ctaexamples.com/cta-section-examples
**Confidence.** High: NN/g eyetracking plus a quantified repetition test.

### 4.18 Announcement pills

**Pattern name.** Small rounded-full pill above the h1 ("✨ v2.0 is live", "Now in Beta").
**Section/category.** Hero eyebrow element.
**Classification.** Context-dependent: earned wayfinding when it carries real, linked news; decorative slop as a permanent fixture.
**Failure mechanism.** The pill hijacks the first read: positioned above the headline, it steals the first fixation for non-information while the h1 carries the persuasion load. It is sold as a purchasable component ("place in your hero, above the main headline"), so it ships whether or not news exists, and "Now in Beta" badges routinely never expire. Design-smell catalogs list the pill-with-dot as a recognizable AI tell.
**Detection signals.** `rounded-full` bordered pill immediately preceding the h1, text matching /new|beta|introducing|v\d/i; pill with no href or `href="#"`; hero text-element count >4 with the pill present; badge text unchanged across months of snapshots.
**Appropriate use cases.** Real launches linking to a changelog or release notes; time-bound badges removed when stale.
**Better alternatives.** Let the headline carry orientation; move news to the nav or a dated changelog link.
**Sources.** VersionBadge, Framer Marketplace — https://www.framer.com/community/marketplace/components/versionbadge/; slop-detect — https://github.com/ravidsrk/slop-detect; Figmalion newsletter — https://figmalion.com/newsletter
**Confidence.** Medium: documented in detector artifacts and component marketplaces; narrower evidence base.

### 4.19 Gradient-text keywords

**Pattern name.** One hero keyword rendered in gradient text (`bg-clip-text text-transparent` on an h1 span).
**Section/category.** Hero headline styling.
**Classification.** Decorative slop: the single most recognized AI fingerprint; earned only as brand-owned identity.
**Failure mechanism.** The mechanism is statistical averaging: Tailwind UI's `bg-indigo-500` placeholder propagated through tutorials into training data, and LLMs emit its median. Krebs' Playwright study of ~1,400 Show HN pages found ~67% carried AI-design fingerprints (via slop-detect). The gradient belongs to no brand, re-brands by find-and-replace, and co-occurs with interchangeable openers ("Unlock the power of…"); users pattern-match "AI-built" in under a second.
**Detection signals.** `bg-clip-text text-transparent` with `from-indigo-500 to-purple-600` (or violet→fuchsia) on an h1 `<span>`; ≥3 gradient-filled elements inside the hero; co-occurrence with "Unlock the power of…" openers.
**Appropriate use cases.** Brand-owned identity gradients in the Stripe/Vercel tradition; restrained single-accent use.
**Better alternatives.** Typographic contrast (weight, scale, serif/sans pairing); reserve brand color for the primary CTA.
**Sources.** slop-detect (Krebs Show HN study) — https://github.com/ravidsrk/slop-detect; dev.to, Blame Tailwind's Indigo-500 — https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p; Branding5, Claude Design On-Brand — https://www.branding5.com/claude-design-anthropic-labs-brand-guidelines
**Confidence.** High: independent detectors converge; the fingerprint is directly observable in template catalogs.

### 4.20 Vestigial newsletter boxes

**Pattern name.** "Subscribe to our newsletter" + email input + gray "Subscribe" button above the footer.
**Section/category.** Footer capture form.
**Classification.** Unearned default for product sites: a request with no exchange, often emitted for products with no newsletter.
**Failure mechanism.** Generic footer forms convert at noise level (≈0.5–2%) versus 5–15% for value-driven inline forms. The generated box carries no promise, frequency, incentive, or readership proof; it fills a slot because "landing pages end with a newsletter box" in the corpus, and on mobile it stacks with cookie banners and chat widgets.
**Detection signals.** Block matching `h3 ~ input[type=email] + button` with copy from {"Subscribe to our newsletter", "Stay up to date", "Join our mailing list"}, no value prop or frequency; no linked archive; emitted on a site with no blog.
**Appropriate use cases.** Editorial sites where the newsletter is the product; footer as evergreen secondary capture beside a stronger inline placement.
**Better alternatives.** Newsletter as exchange: named promise + frequency + incentive + subscriber count, placed inline where intent peaks.
**Sources.** Exmoor Web, Ignored Newsletter Forms — https://www.exmoorweb.co.uk/blog/posts/newsletter-signup-forms.php; Act-On, How Many CTAs? — https://act-on.com/learn/blog/how-many-ctas-should-i-use/
**Confidence.** Medium: agency-reported conversion figures are consistent but not peer-reviewed.

## 5. Repetition and Saturation Findings

**The saturation baseline.** Convergence predates AI. Goree et al. measured layout distance between websites falling 44% from 2010 to 2019, before LLM site builders existed (CHI 2021, via saschb2b). AI industrialized an existing disease: Adrian Krebs' Playwright audit found roughly 67% of about 1,400 Show HN submissions already carrying AI-design fingerprints (Krebs Show HN study, via slop-detect). The fingerprint is consistent enough across vendors that CoffeeBytes' Bolt/Lovable/v0 comparison got the identical page skeleton (logo-left nav, 3–4 sections) from one prompt.

**Most saturated patterns.** The canonical 11-section stack (nav → hero → logo cloud → features → how-it-works → stats → testimonials → pricing → FAQ → CTA → footer) is saturated at the supply level: it is the literal sellable inventory of the block ecosystems models train on. Tailwind Plus markets Heroes (12), Feature Sections (15), CTA Sections (11), Bento Grids (3), Pricing (12), Stats (8), Testimonials (8), Logo Clouds (6), FAQs (7); shadcn-ecosystem libraries (Launch UI, Tailark, Preline, UI Layouts, Landmark) ship the identical taxonomy, down to 39+ interchangeable testimonial blocks on one site and 19 "Steps & flows" variants in a single library. Within-section saturation is measurable: Web Anatomy's 286-section features dataset found 79% skip persona grouping, 72% are dead ends with no internal links, and 56% weight every card equally, with internal linking the rarest differentiator (28% adoption). Proof components show industrial-scale saturation: fakelogo.com sells 200 fictional logos via API, rating logo walls "Effectiveness 9/10, Ease of faking 10/10," and its demo stat bar is indistinguishable from v0/Lovable output. New conventions saturate fast: interactive-demo CTAs already appear on 18% of roughly 5,000 B2B SaaS sites, up 40% YoY (Navattic benchmark via Prospeo), so the fake variant of that pattern is arriving on schedule. Even declining patterns persist in AI output: measured carousel usage fell from 52% to 28% of sites (Baymard data, via the Oslomet thesis), and Erik Runyon's Notre Dame tracking found about 1% of visitors engage a carousel at all with 84% of clicks on slide 1, yet auto-rotating testimonial sliders remain a default AI emission.

**Cross-section repetition.** The same component grammar recurs across nominally different sections. The three-card formula appears as the features grid (3 icon cards), the testimonial row (3 starred quote cards with avatars), the pricing table (3 tiers, highlighted middle), and the how-it-works row (3 steps with ghost numerals). Section headers repeat one anatomy: centered eyebrow pill, h2, gray subheading; four or more consecutive instances produce the template metronome, a page with no hierarchy signal. The interchangeability test applies at every scale: a section that could be pasted onto a competitor's site unnoticed describes the category, not the product (Merge's teardown rule, via 15_lists_tabs_carousels).

**Intra-page repetition.** Within a single page, AI output duplicates rather than paces. Recurring quantitative flags across the briefs: "Get started" appearing more than 3 times; more than 3 visually identical full-width gradient CTA bands; CTA buttons exceeding 5 with 2 or fewer unique labels; the same dashboard screenshot reused 3+ times across zigzag rows; proof stacking of more than 3 bands (logo wall + stat bar + press row + badges + rating); section backgrounds alternating white/`bg-slate-50` down the entire page. Paced repetition is earned CRO practice (one CTA per 1–2 sections, consistent label, placed after trust-building content); identical repetition converts worse with each repeat, and Metrifi's rule of thumb marks any CTA visible twice in one viewport as overdone.

**Ecosystem feedback loops.** The loop is documented end to end: Tailwind UI's `bg-indigo-500` placeholder propagated through tutorials into training data; LLMs emit the median; deployed AI sites are scraped into the next corpus, shifting the distribution further each cycle (dev.to/alanwest). Model-collapse research shows the tails vanish first (Shumailov et al., Nature 2024), and alignment sharpens the mode: RLHF reduces output diversity (Kirk et al., ICLR 2024), and 70+ models produce strikingly similar outputs (NeurIPS 2025 "Artificial Hivemind"). A second, corrective loop has appeared: anti-slop tooling such as slop-detect's 27 rules, Paul Bakaus's 37 codified anti-patterns, and Anthropic's `frontend_aesthetics` exclusion prompt treats saturation as a lint-able defect class, and those critiques will themselves become training data.

**Saturation and user response.** Saturation converts familiar patterns from comprehension aids into filters. Banner blindness is mechanism-level: users ignore elements that look like ads, and the mechanism is predictability, not aesthetics (NN/g; Benway & Lane: banner-style links found 58% of the time vs 94% for standard links). A full-width gradient CTA band is visually indistinguishable from a display ad, and the third identical band is filtered before it is read. Ubiquity flips trust signals into anti-signals: the grayscale logo row now reads as "low-investment template" (AYDesign); "screenshot inflation" means every vendor has a big-number screenshot, so the signal is gone (DevBio); over-polished synthetic headshots sit one cue away from documented scam-site signatures (MalwareTips). Visitors pattern-match "AI-built" in under a second and read sameness as low effort, a trust tax (axe-web). Monotone pacing compounds the effect: Spool's Iceberg Syndrome shows users assume content below the fold repeats what is above, so a metronome page trains them to stop scrolling. The earned/unearned line survives saturation: the skeleton keeps its wayfinding value per Jakob's Law, but every surface element that could belong to any brand now subtracts trust instead of adding fluency.

## 6. Research Gaps

**Causal and conversion evidence**

- No controlled study isolates visual sameness from copy and clarity effects on conversion or trust. "Generic is worse than ugly" and the brand-recall harm claim rest on practitioner consensus (925Studios, axe-web), not experiments. Resolution: A/B designs holding copy and structure constant while varying surface distinctiveness, plus controlled brand-recall testing.
- Several component claims (zigzag rows as padding, checkmark lists as filler, centered MacBook mockups as a tired pattern, glass nav as an AI-emission default) rest on practitioner consensus, single consultant cases, or vendor blogs rather than large-sample data. Resolution: component-level eye-tracking and conversion studies.

**Corpus measurement**

- No formal published study of an AI-generated page corpus exists. The closest (Krebs, ~1,400 Show HN pages, 67% fingerprinted) was reached only through secondary citation (slop-detect), and no quantitative audit exists for generated nav, footer, or form output. Resolution: a labeled corpus of AI-built sites with fingerprint rules run against it, re-crawled over time to track saturation drift.
- Lint thresholds (>3 CTA bands, 4–8 testimonials, 3–5 vs 7–10 sections, ≥90% checkmark parity, >10 FAQ items, proof-to-claim ratios) are derived heuristics synthesized from CRO consensus, not validated on labeled data. Resolution: calibrate thresholds against pages with known outcomes and report precision and recall.

**Source access**

- Community discourse (Reddit/HN/X) was reachable mainly through secondary proxies (Overpass quoting Reddit; design-agency and dev.to blogs); direct threads on logo-wall fatigue did not surface. Resolution: archive primary threads with permalinks before they decay.
- Some primary sources were paywalled, JS-rendered, or not directly fetched: Baymard figures reached via secondary mirrors and CRO blogs, an NN/g centered-logo article via secondary citation, Google's FAQ rich-results documentation not fetched directly, and techdebt.works headline stats (GitClear/Stanford/Snyk attributions) whose primaries were not retrieved. Resolution: retrieve primaries and re-verify each figure before treating it as load-bearing.
- Single-vendor benchmarks with commercial interest (Navattic's 18% adoption; fakelogo's "87% of startups" claim) lack independent replication. Resolution: independent sampling.

**Coverage**

- Editorial and portfolio pacing is under-sourced; page-architecture evidence skews toward SaaS marketing pages. Resolution: dedicated sourcing on editorial rhythm and case-study architecture.
- Mobile-specific compounding of template slop is inferred from desktop evidence plus reviewer observation; few mobile-specific empirical studies exist. Resolution: mobile eye-tracking and viewport studies of templated pages.
- Behavioral sameness (missing validation, dead states, the "functional gap") is argued from observation but not yet quantified the way visual sameness is. Resolution: functional audits against an interactive-state checklist.

## Appendix: Source Index

Every distinct source cited anywhere in this report (§1–§2 and §5 inline citations, §3 inline name citations, §4 Sources fields), alphabetical by title. URLs were recovered from the report itself or from the nineteen layout-scoped briefs (`briefs/01_hero.md`–`briefs/19_meta_discourse.md`); sources whose URL appears in neither are marked `(URL not captured)`.

- 0xminds — AI Testimonial Section Prompts That Build Trust — https://0xminds.com/de/blog/guides/ai-testimonial-section-prompts-guide — §3.9, §4.10
- 21st-frontend-design SKILL.md — https://github.com/sants2001/21st-frontend-design/blob/main/SKILL.md — §4.6
- 925Studios — AI Slop Fonts and Gradients: The Tells That Give Away AI Design — https://www.925studios.co/blog/ai-slop-design-tells — §6
- 99designs — numbered-flow teardown (via Unbounce) — (URL not captured) — §3.7
- Act-On — How Many CTAs on a Landing Page, Email or Blog? — https://act-on.com/learn/blog/how-many-ctas-should-i-use/ — §4.20
- Anthropic — `frontend_aesthetics` anti-slop system prompt (reproduced verbatim in prg.sh) — (URL not captured) — §1, §5
- axe-web — Why AI Websites All Look the Same (And When It Matters) — https://axe-web.com/insights/ai-website-design-sameness/ — §5, §6
- AYDesign — Modern SaaS Landing Page Design Patterns 2026 — https://www.aydesign.ai/blog/modern-saas-landing-page-design-patterns-2026 — §3.5, §4.8, §5
- Babich, Nick — Progress Trackers in UX Design — https://babich.biz/blog/progress-trackers-in-ux-design/ — §3.7
- Bakaus, Paul — "Impeccable" anti-slop skill (This Tool Cures Ugly AI Websites) — https://www.stork.ai/blog/this-tool-cures-ugly-ai-websites — §1, §5
- Baymard Institute — cart-abandonment, trust-badge, FAQ, and carousel research (reached via secondary sources) — https://baymard.com/lp/ux-best-practice-guidelines — §3.5, §3.10, §5
- Baymard Institute — comparison-table scanning guidance (via UX Patterns Guide) — https://uxpatternsguide.com/sources/baymard-user-friendly-comparison-tools/ — §3.6
- Baymard Institute — Have Direct Links to 'Return Policy' and 'Shipping Info' in the Footer — https://baymard.com/blog/footer-needs-return-shipping-links — §3.13
- Brad Frost — Carousels — https://bradfrost.com/blog/post/carousels/ — §4.7
- Branding5 — Claude Design from Anthropic Labs: How to Make It On-Brand — https://www.branding5.com/claude-design-anthropic-labs-brand-guidelines — §4.19
- Bricx — 17 Essential Laws of UX (carries the NN/g centered-logo finding) — https://bricxlabs.com/blogs/laws-of-ux — §3.2
- Codebrand — AI Website Builders 2025: v0, Cursor & No-Code — https://www.codebrand.us/blog/ai-website-builders-v0-cursor-2025/ — §3.8, §4.11
- CoffeeBytes — My Bolt vs Lovable vs v0 Comparison — https://coffeebytes.dev/en/artificial-intelligence/bolt-vs-lovable-vs-v0-vercel-for-landing-pages-comparison/ — §1, §5
- CommerceGurus — Trust Badges on eCommerce Stores (Baymard DIY-seal study) — https://www.commercegurus.com/trust-badges/ — §3.5
- Conversionista — static-vs-carousel A/B test — (URL not captured) — §4.7
- CTAExamples — CTA Section Examples (Tailwind catalog) — https://ctaexamples.com/cta-section-examples — §2, §4.17
- CustomFit.ai — Strikethrough Pricing: Does It Work? — https://www.customfit.ai/blog/checkout-pricing/strikethrough-pricing-effectiveness — §3.8
- designmd.app — SaaS Enterprise Analytics DESIGN.md — https://designmd.app/library/saas-enterprise-analytics — §3.4
- DevBio — Live MRR Developer Profile — https://devbio.me/blogs/live-mrr-developer-profile — §3.4, §5
- dev.to (alanwest) — Why Every AI-Built Website Looks the Same — Blame Tailwind's Indigo-500 — https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p — §3.1, §4.19, §5
- dev.to — Why Every AI-Generated Landing Page Looks the Same — https://dev.to/_46ea277e677b888e0cd13/why-every-ai-generated-landing-page-looks-the-same-and-how-to-fix-it-1kmo — §4.1
- dnsk.work — SaaS Website Design Mistakes: Who Are You Actually Designing This Homepage For? — https://dnsk.work/blog/who-are-you-designing-for — §3.3, §4.5
- DoubleVerify — DV Deep Dive: AI Slop Recipe Sites — https://doubleverify.com/blog/web/verify/dv-deep-dive-serving-ai-slop-understanding-advertiser-risks-on-cooking-and-recipe-websites-with-ai-generated-content — §3.12
- Electric Copy — Federico Jorge: How to Write Comparison Pages for SaaS Products — https://www.electriccopy.tech/blog/federico-jorge-how-to-write-comparison-pages-for-saas-products — §3.6
- Exmoor Web — Why Your Newsletter Signup Forms Get Ignored — https://www.exmoorweb.co.uk/blog/posts/newsletter-signup-forms.php — §3.11, §4.20
- fakelogo.com — Social Proof Examples — https://fakelogo.com/social-proof-examples — §1, §3.5, §4.8, §4.9, §5, §6
- Figmalion newsletter — https://figmalion.com/newsletter — §4.18
- Flow Agency — High-Performing B2B SaaS Landing Page — https://www.flow-agency.com/blog/b2b-saas-landing-page-best-practices/ — §2
- Fogg, B.J. — reputed-credibility research — (URL not captured) — §3.5
- Foundry CRO — Landing Page Social Proof Benchmarks 2026 — https://foundrycro.com/blog/landing-page-social-proof-benchmarks-2026/ — §3.9, §4.10
- GetMonetizely — The Decoy Effect: How Strategic Pricing Tiers Can Maximize Revenue — https://www.getmonetizely.com/articles/the-decoy-effect-how-strategic-pricing-tiers-can-maximize-revenue — §3.8, §4.11
- Goree et al. — CHI 2021 layout-sameness study (reached via saschb2b) — (URL not captured) — §1, §2, §5
- GOV.UK Design System — Accordion — https://design-system.service.gov.uk/components/accordion/ — §3.10, §4.12
- Growform — 10 Landing Page Best Practices — https://www.growform.co/landing-page-best-practices/ — §2
- heroprompts.io — hero prompt marketplace — (URL not captured) — §3.4
- Hoplite Analytics — Google Removes FAQ Rich Results From Search in 2026 — https://hopliteanalytics.com/news/google-drops-faq-rich-results-from-search-results/ — §3.10, §4.12
- HugoBlox — demo AI landing-page prompt — (URL not captured) — §2
- InnReg — FTC Implements Final Rule Banning Fake Reviews and Testimonials — https://www.innreg.com/resources/regulatory-updates/ftc-implements-final-rule-banning-fake-reviews-and-testimonials — §3.9, §4.10
- Interaction Design Foundation — Web User Behaviour Directed by Information Scent (Spool's Iceberg Syndrome) — https://www.interaction-design.org/literature/article/web-user-behaviour-directed-by-information-scent — §2, §5
- Kirk et al. — ICLR 2024, alignment reduces output diversity — (URL not captured) — §1, §2, §5
- Krebs, Adrian — Show HN AI-fingerprint study, ~1,400 pages (via slop-detect) — https://github.com/ravidsrk/slop-detect — §1, §3.1, §4.19, §5, §6
- Landy-ai — Landing Page Structure: The Complete Anatomy — https://www.landy-ai.com/blog/landing-page-structure — §4.15
- Laws of UX — Jakob's Law — https://lawsofux.com — §1, §2, §3.2, §5
- Lovable — Scrolling Designs: 8 Patterns and When to Use Each — https://lovable.dev/guides/scrolling-designs-patterns-when-to-use — §4.14
- MalwareTips — Elon Musk Energy Saver Scam Exposed — https://malwaretips.com/blogs/elon-musk-device-energy-savings-scam/ — §5
- Mantasauk — Where to Position Social Proof — https://mantasauk.com/articles/social-proof-placement-testimonials-landing-pages — §1, §2
- Marketful — The Complete Guide to Social Proof in Marketing — https://marketful.com/social-proof — §3.9
- Mavan — Website Conversion Is a Trust Problem — https://www.mavan.com/website-conversion-is-a-trust-problem-seo-ux-messaging-fixes-growth-stage-teams-can-make-in-90-days/ — §3.5
- Mean CEO — Answer Engine Optimization News, June 2026 — https://blog.mean.ceo/answer-engine-optimization-news-june-2026/ — §3.10
- Merge — Top 5 SaaS Landing Page Mistakes — https://merge.rocks/blog/we-reviewed-dozens-of-saas-landing-pages-here-are-the-5-mistakes-we-keep-seeing — §4.5, §5
- Metrifi — If You Repeat Your Call to Action, More People Will Convert (incl. the GoodUI 7%→12.8% test) — https://metrifi.com/blog/research-shows-if-you-repeat-your-call-to-action-more-people-will-convert/ — §1, §2, §3.11, §4.17, §5
- Mettevo — comparison-table bias commentary — (URL not captured) — §3.6
- NetSuite — Your Playbook for a Profitable Subscription Offering — https://luxent.com/wp-content/uploads/2022/08/Your-Playbook-for-a-Profitable-Subscription-Offering.pdf — §3.8
- NeurIPS 2025 — "Artificial Hivemind" — (URL not captured) — §1, §2, §5
- Nielsen Norman Group — Accordions on Desktop: When and How to Use — https://www.nngroup.com/articles/accordions-on-desktop/ — §3.10, §4.12
- Nielsen Norman Group — attention data (57/74/81% of viewing time) — (URL not captured) — §1, §2
- Nielsen Norman Group — Auto-Forwarding Carousels and Accordions Annoy Users and Reduce Visibility — https://www.nngroup.com/articles/auto-forwarding/ — §4.7
- Nielsen Norman Group — Banner Blindness: Old and New Findings (incl. Benway & Lane) — https://www.nngroup.com/articles/banner-blindness-old-and-new-findings/ — §2, §3.11, §4.17, §5
- Nielsen Norman Group — Card View vs. List View — https://www.nngroup.com/videos/card-view-vs-list-view/ — §1, §3.3
- Nielsen Norman Group — Cards: UI-Component Definition — https://www.nngroup.com/articles/cards-component/ — §4.1, §4.3
- Nielsen Norman Group — centered-logo navigation finding (via Bricx) — (URL not captured) — §3.2
- Nielsen Norman Group — Comparison Tables for Products, Services, and Features — https://www.nngroup.com/articles/comparison-tables/ — §3.6
- Nielsen Norman Group — Footers 101 — https://www.nngroup.com/articles/footers/ — §3.13
- Nielsen Norman Group — Hamburger Menus and Hidden Navigation Hurt UX Metrics (179-user study) — https://www.nngroup.com/articles/hamburger-menus/ — §1, §3.2
- Nielsen Norman Group — Scrolljacking 101 — https://www.nngroup.com/articles/scrolljacking-101/ — §4.14
- Nielsen Norman Group — Sticky Headers: 5 Ways to Make Them Better — https://www.nngroup.com/articles/sticky-headers/ — §3.2
- Nielsen Norman Group — Tabs, Used Right — https://www.nngroup.com/articles/tabs-used-right/ — §4.6
- Nielsen Norman Group — The Page Fold Manifesto — https://www.nngroup.com/articles/page-fold-manifesto/ — §3.1
- Nielsen Norman Group — Trustworthiness in Web Design: 4 Credibility Factors — https://www.nngroup.com/articles/trustworthy-design/ — §3.5
- Nielsen Norman Group — Video Usability — https://www.nngroup.com/articles/video-usability/ — §3.4
- Nielsen Norman Group — Visibility of System Status (Usability Heuristic #1) — https://www.nngroup.com/articles/visibility-system-status/ — §3.7
- Nielsen Norman Group — Zigzag Image–Text Layouts Make Scanning Less Efficient — https://www.nngroup.com/articles/zigzag-page-layout/ — §4.15
- Open Doors — How to Write a Strong Case Study for Your Portfolio in 2025 — https://blog.opendoorscareers.com/p/how-to-write-a-strong-case-study-for-your-portfolio-in-2025-a14b — §2
- Orbix — SaaS Website Inspiration: What 50 Top Products Have in Common — https://www.orbix.studio/blogs/saas-website-inspiration — §3.11
- OsloMet thesis (2020) — Investigation into Carousel Interaction (summarizes Baymard usage-decline data) — https://oda.oslomet.no/oda-xmlui/bitstream/handle/10642/9250/keya_mauu2020.pdf — §5
- OsloMet thesis (2024) — Glassmorphism usability study — https://oda.oslomet.no/oda-xmlui/bitstream/handle/11250/3206174/no.oslomet:inspera:348177680:130368616.pdf — §3.2
- Overpass Studio — Why SaaS Websites Look the Same — https://www.overpass.studio/blog/why-saas-websites-look-the-same — §2, §4.13, §6
- PainOnSocial — SaaS Pricing Complaints on Reddit — https://painonsocial.com/blog/saas-pricing-complaints-reddit — §3.8, §4.11
- PostKit — What Is a Browser Mockup? — https://www.getpostkit.com/glossary/browser-mockup — §4.16
- PowerReviews — perfect-rating distrust data (reached via Foundry CRO) — (URL not captured) — §3.9
- pravatar.cc / ui-avatars / randomuser.me — placeholder avatar services — (URL not captured) — §3.9, §4.10
- prg.sh — Why Your AI Keeps Building the Same Purple Gradient Website — https://prg.sh/ramblings/Why-Your-AI-Keeps-Building-the-Same-Purple-Gradient-Website — §3.3, §4.4
- Prospeo — Navattic vs Storylane: The Honest Comparison (Navattic interactive-demo benchmark) — https://prospeo.io/s/navattic-vs-storylane — §3.4, §5, §6
- Raze — The Comparison Page Template That Displaces Legacy Competitors — https://razegrowth.com/templates/comparison-page-template-displaces-competitors — §3.6
- Reber, Schwarz & Winkielman (2004) — processing-fluency research — (URL not captured) — §1
- Rechurn — flat-rate pricing example — https://rechurn.io/ — §3.8
- Rudo — SaaS Homepage Design: What Works and Why — https://rudo.co.uk/insights/articles/saas-homepage-design/ — §3.7
- Runyon, Erik — Carousel Interaction Stats (Notre Dame) — https://erikrunyon.com/2013/01/carousel-interaction-stats/ — §1, §3.9, §4.7, §5
- SaaSFrame — 10 UI Patterns That Drive Pricing Page Conversions — https://www.saasframe.io/blog/10-ui-patterns-that-drive-pricing-pages-conversions-in-2026 — §4.5
- SaaSFrame — Designing Bento Grids That Actually Work — https://www.saasframe.io/blog/designing-bento-grids-that-actually-work-a-2026-practical-guide — §4.2
- saschb2b — Same Same but Different: The Anatomy of AI Design Sameness — https://saschb2b.com/ko/blog/same-same-but-different — §1, §2, §5
- Screenhance — MacBook Mockup Generator — https://screenhance.com/macbook-mockup-generator — §3.4, §4.16
- seomatic — Programmatic SEO for SaaS — https://seomatic.ai/blog/programmatic-seo-for-saas — §3.6
- shadcn/ui block libraries survey — 12 Best shadcn/ui Block Libraries 2026 (Launch UI, Tailark, Preline, UI Layouts, Landmark) — https://adminlte.io/blog/shadcn-ui-block-libraries/ — §2, §4.2, §4.3, §5
- Shadcnblocks — Feature Timeline Blocks — https://www.shadcnblocks.com/blocks/feature/timeline — §4.13
- Shadcnblocks — Feature13 — https://www.shadcnblocks.com/block/feature13 — §4.4
- Shadcnblocks — Testimonial Blocks — https://www.shadcnblocks.com/blocks/testimonial — §3.9, §5
- Shumailov et al. — Nature 2024, model collapse — (URL not captured) — §1, §5
- Sidley Data Matters — U.S. FTC's New Rule on Fake and AI-Generated Reviews — https://datamatters.sidley.com/2024/08/30/u-s-ftcs-new-rule-on-fake-and-ai-generated-reviews-and-social-media-bots/ — §3.9
- SiteCritic — Website FAQ Design: Where to Place It, What to Include — https://www.sitecritic.ai/blog/website-faq-design-where-to-place-it-what-to-include — §3.10, §4.12
- skills.ws — Landing Page Builder agent skill — https://www.skills.ws/skills/landing-page-builder — §3.5, §4.9
- slop-detect — 27-rule AI-slop linter (incl. the "VibeCode Purple" rule) — https://github.com/ravidsrk/slop-detect — §1, §3.1, §3.11, §4.18, §4.19, §5, §6
- Specflux — Social Proof Engineering in Web Design — https://www.specflux.com/web-design/social-proof-web-design/ — §3.5, §4.9
- Spiegel Research Center — rating sweet-spot research (reached via Foundry CRO) — (URL not captured) — §1, §3.9
- Stacked Marketer — Should You Use Client Logos on Your Website? — https://www.stackedmarketer.com/the-crews-insights/should-you-use-client-logos-on-your-website/ — §3.5, §4.8
- Stanford — Guidelines for Web Credibility — https://credibility.stanford.edu/guidelines/index.html — §3.12
- superfiles — The Bento Grid Era — https://superfiles.in/bento-grid-ui-design-trend.php — §4.2
- Tailwind Plus — Footer blocks — https://tailwindcss.com/plus/ui-blocks/marketing/sections/footers — §3.13
- Tailwind Plus — UI blocks catalog — https://tailwindcss.com/plus/ui-blocks — §2, §5
- Tailwind UI — Contact Sections — https://tailwindui.com/components/marketing/sections/contact-sections — §3.12
- Team4 — B2B SaaS SEO: The Definitive Guide — https://www.team4.agency/post/b2b-saas-seo — §3.6
- techdebt.works — AI Code Review Guide — https://techdebt.works/ai-code-review/ — §6
- uislop — AI-default hero detector — (URL not captured) — §3.1
- Unbounce — nav-removal conversion figure — (URL not captured) — §3.2
- Unkover — 13 Examples of Comparison Pages — https://unkover.com/blog/comparison-pages/ — §3.6
- U.S. FTC — Consumer Reviews Rule (October 2024) — (URL not captured; analyzed by InnReg and Sidley) — §1, §3.5, §3.9, §4.10
- UXMagic — Best Mockup Tools in 2026 — https://uxmagic.ai/blog/best-mockup-tools-2026-fast-ui-workflows — §3.4, §4.16
- VersionBadge (Framer Marketplace) — https://www.framer.com/community/marketplace/components/versionbadge/ — §4.18
- Veza Digital — Best SaaS Landing Page Design Examples — https://www.vezadigital.com/post/best-saas-landing-page-examples — §2
- Visionary Marketing — Pricing Page Conversion Statistics 2026 — https://visionary-marketing.co.uk/blog/pricing-page-conversion-statistics-2026 — §3.8
- WeGrowth — Improve Your Landing Page Conversions (classic Crazy Egg case) — https://www.wegrowth.com/blog/10-tactics-for-improving-landing-page-conversion-rates — §3.4
- Wix Studio — Website Footers Are (Literally) Bigger Than Ever — https://www.wix.com/studio/blog/big-website-footers — §3.13
