---
name: liquid-glassify
description: Generate a complete, production-ready single-file website with Apple Liquid Glass aesthetic (NOT glassmorphism). Thin refractive blur, multi-layer specular edge highlights, radial top-light reflections, vivid content refraction through near-transparent panels, spring motion. The aesthetic is iOS 26 / macOS 26 / visionOS, not Frosty 2019 glassmorphism. Use for landing pages, product launch sites, portfolios, SaaS marketing, event microsites, hackathon demos, and anywhere you want a site that feels like an Apple keynote instead of a Bootstrap template. Trigger with "liquid glass," "glassify," "Apple glass," "visionOS landing page," "iOS 26 style," or "make this look premium."
best_for:
  - Landing pages (product, startup, waitlist)
  - Portfolio and personal sites
  - SaaS marketing pages
  - Event and conference microsites
  - Hackathon and demo day sites
  - Product launch announcements
estimated_time: "3-7 min"
---

# Liquid-Glassify

Ship websites that look like Apple designed them. Single-file HTML, zero build step, one `open index.html` away from a site that makes people ask "who did your design?"

## Apple Liquid Glass vs Glassmorphism (Critical)

Most AI-generated "glass" sites produce **glassmorphism**, which is the 2019 frosted-glass trend: heavy blur, thick white tint overlay, everything looks milky. This is **wrong** for the Liquid Glass aesthetic.

Apple's **Liquid Glass** (iOS 26, macOS 26, visionOS) looks different:

| | Glassmorphism (wrong) | Apple Liquid Glass (right) |
|---|---|---|
| Blur amount | 20-40px heavy | 8-16px thin |
| Background tint | `rgba(255,255,255,0.08-0.15)` opaque | `rgba(255,255,255,0.02-0.05)` barely visible |
| Saturation | 150-180% | 180-220% (vivid refraction) |
| Content behind | Washed out, milky | Clearly visible, color-refracted |
| Edges | Single 1px border | Multi-layer specular (top bright, sides subtle, bottom faint) |
| Top highlight | None | Radial specular gradient (like light on curved glass) |
| Feel | Frosted bathroom window | 3D piece of polished crystal |

**The Liquid Glass signature: content behind a Liquid Glass panel is sharper and more saturated than content NOT behind it.** Think of real glass: it catches light at the edges, magnifies and saturates what's behind it, and has a subtle specular shine. Glassmorphism just blurs everything into milky paste.

## When to Use

Use any time a user asks for a website, landing page, portfolio, or marketing page and wants it to feel **premium without looking like a template**. Also use on "Apple," "visionOS," "Liquid Glass," "iOS 26 style," "frosted," "make it look like Vision Pro," or "look like an Apple keynote."

Do NOT use for: admin dashboards (glass fatigues on dense data), forms-heavy apps (legibility), print output, or sites that must run on low-end Android (backdrop-filter has a perf cost).

## Design Principles (Enforce Strictly)

1. **Thin blur, high saturation.** Default `blur(14px) saturate(190%)`. Never go above 22px blur. The goal is "transparent crystal," not "shower door."
2. **Near-zero tint.** Background at `rgba(255,255,255,0.028)` to `rgba(255,255,255,0.055)`. If you can see white washing out the content behind, the tint is too high.
3. **Multi-layer specular edges (signature move).** Use a composite box-shadow with:
   - Strong top inset highlight: `inset 0 1px 0.5px rgba(255,255,255,0.35-0.45)`
   - Soft top falloff: `inset 0 2px 6px -2px rgba(255,255,255,0.08-0.1)`
   - Subtle side inset: `inset ±1px 0 0 rgba(255,255,255,0.06-0.08)`
   - Faint bottom: `inset 0 -1px 0 rgba(255,255,255,0.02-0.03)`
   - Outer ambient: `0 8px 24px -8px rgba(0,0,0,0.4)`
4. **Radial specular via `::before` pseudo-element.** Every glass panel gets a `::before` with a radial gradient from top-center, emulating light hitting curved glass. This is what sells "3D crystal" over "flat pane."
5. **Border-top is brighter than sides.** Top edge catches more light. Use `border: 1px solid rgba(255,255,255,0.08); border-top-color: rgba(255,255,255,0.12);`
6. **Spring motion, subtle.** All transitions use `cubic-bezier(0.34, 1.56, 0.64, 1)`. Hover scales cap at 1.02. Lift by 4-6px translateY max.
7. **Backgrounds are vivid but monochromatic-accent.** Mesh gradients should use ONE accent color family (Linear's indigo family, Anthropic's rust, etc), not a rainbow.

## Intake (Ask Before Building)

Ask these questions one at a time. Wait for each answer.

1. **Site type.** Landing page, portfolio, product launch, event site, SaaS marketing, or something else?
2. **One-sentence pitch.** What does the site sell, promise, or communicate?
3. **Primary CTA.** What single action do you want visitors to take?
4. **Vibe.** Three words. Drives the palette.
5. **Sections needed.** Default is hero + features + CTA. Offer: testimonials, pricing, FAQ, logos, team, stats.
6. **Brand color (optional).** If they have one, use it as the primary accent. Otherwise pick based on vibe.

Do not ask about fonts or layout. This skill has strong opinions.

## Build Steps

1. Scaffold semantic HTML5 (`<header>`, `<main>` with `<section>` tags, `<footer>`).
2. Apply the design tokens below.
3. Build the animated background (see Recipes).
4. Compose sections using the glass component patterns.
5. Add `::before` specular highlights on every glass panel.
6. Wire spring motion on hover and scroll-reveal on sections.
7. Test: open in browser, check that content behind glass is sharper and more saturated than content not behind glass. If it looks milky, the blur is too high or the tint is too opaque.
8. Save as `./liquid-glass-site/index.html` by default.

## Design Tokens (Linear + Liquid Glass, use verbatim)

```css
:root {
  /* Base palette (swap for your theme) */
  --bg: #08090a;
  --text: #f7f8f8;
  --text-soft: #d0d6e0;
  --text-dim: #8a8f98;

  /* Borders (wireframes-in-moonlight) */
  --border-faint: rgba(255, 255, 255, 0.05);
  --border: rgba(255, 255, 255, 0.08);
  --border-strong: rgba(255, 255, 255, 0.12);

  /* Accent (pick one family, not a rainbow) */
  --accent: #5e6ad2;
  --accent-bright: #7170ff;
  --accent-hover: #828fff;

  /* LIQUID GLASS values (NOT glassmorphism) */
  --liquid-tint: rgba(255, 255, 255, 0.028);
  --liquid-tint-strong: rgba(255, 255, 255, 0.055);
  --liquid-blur: blur(14px) saturate(190%);
  --liquid-blur-soft: blur(8px) saturate(170%);
  --liquid-blur-deep: blur(22px) saturate(200%);

  /* The signature: multi-layer specular edges */
  --liquid-shadow:
    inset 0 1px 0.5px 0 rgba(255, 255, 255, 0.35),
    inset 0 2px 6px -2px rgba(255, 255, 255, 0.08),
    inset 1px 0 0 0 rgba(255, 255, 255, 0.06),
    inset -1px 0 0 0 rgba(255, 255, 255, 0.06),
    inset 0 -1px 0 0 rgba(255, 255, 255, 0.02),
    0 1px 2px rgba(0, 0, 0, 0.3),
    0 8px 24px -8px rgba(0, 0, 0, 0.4);

  --liquid-shadow-lg:
    inset 0 1px 1px 0 rgba(255, 255, 255, 0.45),
    inset 0 2px 10px -2px rgba(255, 255, 255, 0.1),
    inset 1px 0 0 0 rgba(255, 255, 255, 0.08),
    inset -1px 0 0 0 rgba(255, 255, 255, 0.08),
    inset 0 -1px 0 0 rgba(255, 255, 255, 0.03),
    0 2px 4px rgba(0, 0, 0, 0.35),
    0 24px 48px -12px rgba(0, 0, 0, 0.5);

  /* Radius */
  --r-xs: 6px;
  --r-sm: 10px;
  --r-md: 14px;
  --r-lg: 20px;
  --r-xl: 28px;

  /* Motion */
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --ease-smooth: cubic-bezier(0.4, 0, 0.2, 1);
}

* { box-sizing: border-box; margin: 0; padding: 0; }
html, body { background: var(--bg); color: var(--text); overflow-x: hidden; }
body {
  font-family: "Inter Variable", "Inter", -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
  font-feature-settings: "cv01", "ss03";
  font-size: 16px; line-height: 1.5; font-weight: 400;
  -webkit-font-smoothing: antialiased;
}
```

## Vibe-to-Palette Mapping

Pick ONE family. Do not mix families.

| Vibe keywords | Base | Accent | Accent-bright | Accent-hover |
|---------------|------|--------|---------------|--------------|
| serious, technical, confident | `#08090a` | `#5e6ad2` (Linear indigo) | `#7170ff` | `#828fff` |
| playful, bold, energetic | `#0a0a12` | `#ec4899` (rose) | `#f472b6` | `#f9a8d4` |
| calm, premium, trustworthy | `#0c0a1a` | `#6366f1` (indigo) | `#818cf8` | `#a5b4fc` |
| warm, human, approachable | `#1a0a08` | `#f97316` (orange) | `#fb923c` | `#fdba74` |
| futuristic, AI, edge | `#050010` | `#a855f7` (violet) | `#c084fc` | `#d8b4fe` |
| monochrome, editorial | `#0a0a0a` | `#e5e5e5` (silver) | `#ffffff` | `#fafafa` |

## Background Recipes (Pick One)

### Recipe A: Monochromatic Mesh (default, on-brand)

```css
.mesh-bg {
  position: fixed; inset: -15%; z-index: -1;
  background:
    radial-gradient(circle at 22% 28%, var(--accent), transparent 50%),
    radial-gradient(circle at 78% 18%, var(--accent-bright), transparent 45%),
    radial-gradient(circle at 48% 88%, #3a2e6b, transparent 50%),
    var(--bg);
  filter: blur(120px) saturate(130%);
  opacity: 0.55;
  animation: mesh-drift 34s ease-in-out infinite;
}
@keyframes mesh-drift {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(-2%, 1.5%) scale(1.04); }
  66% { transform: translate(1.5%, -2%) scale(0.98); }
}
```

### Recipe B: Floating Accent Orbs

```css
.orbs { position: fixed; inset: 0; z-index: -1; overflow: hidden; background: var(--bg); }
.orbs::before, .orbs::after {
  content: ""; position: absolute; width: 50vmax; height: 50vmax; border-radius: 50%;
  filter: blur(140px); opacity: 0.45;
}
.orbs::before { background: var(--accent); top: -20vmax; left: -15vmax; animation: orb-a 24s ease-in-out infinite; }
.orbs::after { background: var(--accent-bright); bottom: -20vmax; right: -15vmax; animation: orb-b 28s ease-in-out infinite; }
@keyframes orb-a { 50% { transform: translate(20vw, 30vh); } }
@keyframes orb-b { 50% { transform: translate(-20vw, -30vh); } }
```

### Recipe C: Conic Aurora

```css
.aurora { position: fixed; inset: -20%; z-index: -1; background: var(--bg); }
.aurora::before {
  content: ""; position: absolute; inset: 0;
  background: conic-gradient(from 0deg at 50% 50%, var(--accent), var(--accent-bright), var(--accent-hover), var(--accent));
  filter: blur(120px); opacity: 0.4; animation: spin 50s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
```

## Glass Component Library

### Liquid Glass Card (the workhorse)

Always ships with the `::before` specular pseudo-element. That is non-negotiable.

```css
.card {
  background: var(--liquid-tint);
  backdrop-filter: var(--liquid-blur);
  -webkit-backdrop-filter: var(--liquid-blur);
  border: 1px solid var(--border);
  border-top-color: var(--border-strong);
  border-radius: var(--r-lg);
  box-shadow: var(--liquid-shadow);
  padding: 32px;
  transition: all 0.5s var(--ease-spring);
  position: relative;
  overflow: hidden;
}
/* THE signature (radial specular at top, like light hitting curved glass) */
.card::before {
  content: "";
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 55%;
  background: radial-gradient(
    ellipse 80% 100% at 50% 0%,
    rgba(255, 255, 255, 0.07) 0%,
    rgba(255, 255, 255, 0.02) 40%,
    transparent 70%
  );
  pointer-events: none;
  border-radius: inherit;
}
.card > * { position: relative; z-index: 1; }
.card:hover {
  transform: translateY(-4px);
  background: var(--liquid-tint-strong);
  border-color: var(--border-strong);
  box-shadow: var(--liquid-shadow-lg);
}
```

### Primary CTA (solid accent, not gradient)

Linear/Apple style: solid color, strong but subtle inset highlight, accent glow outer shadow.

```css
.cta {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 12px 22px;
  background: var(--accent);
  border: 1px solid rgba(255,255,255,0.08);
  border-top-color: rgba(255,255,255,0.18);
  border-radius: var(--r-xs);
  color: #ffffff; font-weight: 590; font-size: 14.5px;
  letter-spacing: -0.01em;
  box-shadow:
    inset 0 1px 0 0 rgba(255, 255, 255, 0.22),
    inset 0 -1px 0 0 rgba(0, 0, 0, 0.15),
    0 4px 16px rgba(94, 106, 210, 0.35),
    0 1px 2px rgba(0, 0, 0, 0.25);
  transition: all 0.3s var(--ease-spring);
}
.cta:hover {
  background: var(--accent-hover);
  transform: translateY(-1px);
  box-shadow:
    inset 0 1px 0 0 rgba(255, 255, 255, 0.3),
    0 8px 24px rgba(113, 112, 255, 0.45);
}
```

### Secondary CTA (Liquid Glass)

```css
.cta-secondary {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 12px 22px;
  background: var(--liquid-tint);
  backdrop-filter: var(--liquid-blur-soft);
  -webkit-backdrop-filter: var(--liquid-blur-soft);
  border: 1px solid var(--border);
  border-top-color: var(--border-strong);
  border-radius: var(--r-xs);
  color: var(--text); font-weight: 510; font-size: 14.5px;
  box-shadow: var(--liquid-shadow);
  transition: all 0.3s var(--ease-spring);
}
.cta-secondary:hover { background: var(--liquid-tint-strong); transform: translateY(-1px); border-color: var(--border-strong); }
```

### Glass Nav (sticky dock)

```css
.nav {
  position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
  display: flex; gap: 2px; padding: 6px;
  background: var(--liquid-tint);
  backdrop-filter: var(--liquid-blur);
  -webkit-backdrop-filter: var(--liquid-blur);
  border: 1px solid var(--border);
  border-top-color: var(--border-strong);
  border-radius: 100px;
  box-shadow: var(--liquid-shadow);
  z-index: 100;
}
.nav a { padding: 7px 16px; border-radius: 100px; color: var(--text-soft); font-size: 14px; font-weight: 510; transition: all 0.2s var(--ease-smooth); }
.nav a:hover { background: rgba(255, 255, 255, 0.04); color: var(--text); }
.nav .nav-cta {
  background: var(--accent); color: #fff; font-weight: 590;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.2), 0 2px 8px rgba(94, 106, 210, 0.3);
}
```

### Scroll Reveal (one JS hook, no library)

```html
<script>
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => e.isIntersecting && e.target.classList.add("in"));
}, { threshold: 0.1 });
document.querySelectorAll("[data-reveal]").forEach(el => io.observe(el));
</script>
<style>
[data-reveal] { opacity: 0; transform: translateY(20px); transition: opacity 0.8s var(--ease-smooth), transform 0.9s var(--ease-spring); }
[data-reveal].in { opacity: 1; transform: none; }
</style>
<noscript><style>[data-reveal] { opacity: 1 !important; transform: none !important; }</style></noscript>
```

### Typography (Linear-inspired)

```css
h1 { font-size: clamp(44px, 7vw, 84px); font-weight: 510; line-height: 1.02; letter-spacing: -0.034em; }
h2 { font-size: clamp(32px, 4vw, 48px); font-weight: 510; letter-spacing: -0.022em; }
h3 { font-size: 20px; font-weight: 590; letter-spacing: -0.012em; }
p.lead { font-size: clamp(17px, 1.8vw, 19px); color: var(--text-soft); max-width: 60ch; line-height: 1.55; }
```

Weight 510 is the Linear signature (between regular 400 and medium 500). Use it for displays and emphasized text. Weight 590 for strong emphasis.

## Section Templates

**Hero**
```html
<section class="hero">
  <span class="eyebrow" data-reveal>[tagline]</span>
  <h1 data-reveal>[pitch line 1]<br><span class="accent">[pitch line 2]</span></h1>
  <p class="lead" data-reveal>[subheadline]</p>
  <div class="cta-row" data-reveal>
    <a class="cta" href="#cta">[Primary CTA]</a>
    <a class="cta-secondary" href="#more">[Secondary CTA]</a>
  </div>
</section>
```

**Feature Grid**
```html
<section>
  <h2 data-reveal>[section headline]</h2>
  <p class="lead" data-reveal>[context]</p>
  <div class="grid-3">
    <div class="card" data-reveal><h3>[feature]</h3><p>[benefit]</p></div>
  </div>
</section>
```

## Anti-Patterns (Do Not Ship These)

- **Glassmorphism blur values** (20-40px). The #1 mistake. Keep blur 8-16px.
- **Opaque white tint** (rgba(255,255,255,0.1+)). Content gets washed out. Stay under 0.055.
- Glass panels without `::before` specular. Flat, fake-looking.
- Single border-color on all sides. Top must be brighter than sides/bottom.
- Rainbow backgrounds. Pick ONE accent family.
- Gradient text everywhere. Linear uses type weight and color contrast, not rainbows.
- Hover scales above 1.05. Breaks the restraint feel.
- Linear transitions on interactive elements. Always spring curve.
- Backdrop-filter without `-webkit-backdrop-filter`. Safari still needs the prefix.
- Lorem ipsum in the final output. Always write real copy.

## Verification Before Shipping

Every item must pass:

- [ ] Single HTML file, zero build, zero CDN dependencies (Inter font CDN is the only external load allowed).
- [ ] Background is animated and monochromatic-accent (one color family).
- [ ] Every glass panel has: `backdrop-filter` between 8-16px blur, saturate 170-220%, tint under 0.06, multi-layer `box-shadow`, `::before` radial specular.
- [ ] Border-top is brighter than border-sides/bottom.
- [ ] Primary CTA is solid accent (not gradient) with strong inset top highlight.
- [ ] Content behind glass panels is clearly visible and SHARPER than content not behind them. If it looks milky or frosted, reduce blur or tint.
- [ ] Typography uses weight 510 for displays, aggressive negative letter-spacing (-0.02 to -0.035em), Inter Variable if available.
- [ ] At least one `data-reveal` scroll-triggered element.
- [ ] No lorem ipsum; all copy from intake answers.
- [ ] File size under 40KB (excluding external font CSS).
- [ ] `@media (prefers-reduced-motion: reduce)` block disables animations.
- [ ] `<noscript>` fallback keeps reveal elements visible.

## Output

Save to `./liquid-glass-site/index.html` by default. Report the absolute path. Offer `open ./liquid-glass-site/index.html` (macOS) or `xdg-open` (Linux) to preview.

## Source Attribution

Apple's Liquid Glass design language debuted in iOS 26, macOS 26, and visionOS (2025). The multi-layer specular edges, radial top-highlight, and "refractive-not-frosted" aesthetic are the signature moves. This skill packages those specifications into reusable CSS patterns.
