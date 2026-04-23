---
name: liquid-glassify
description: Generate a complete, production-ready single-file website with Apple Liquid Glass aesthetic. Translucent panels with backdrop blur, depth layers, vivid animated mesh-gradient backgrounds, soft light refraction, and spring motion. Use for landing pages, product launch sites, portfolios, SaaS marketing pages, event microsites, hackathon demos, and anywhere you want a site that feels like visionOS or an Apple keynote instead of another Bootstrap template. Trigger with "liquid glass," "glassify," "glass theme site," "Apple-style landing page," "visionOS landing page," or "make this look premium."
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

## When to Use

Use this skill any time a user asks for a website, landing page, portfolio, or marketing page and wants it to feel **premium without looking like a template**. Also use when the user mentions Apple, visionOS, Liquid Glass, glassmorphism, "glassy," "frosted," "make it look like Vision Pro," or "look like an Apple keynote."

Do NOT use for: admin dashboards (glass fatigues on dense data), forms-heavy apps (legibility), print output, or anything that needs to be fast on low-end Android devices (backdrop-filter has a perf cost).

## Design Principles (Enforce Strictly)

Liquid Glass is not "add blur and call it a day." It is a material system with rules. Every site this skill produces must follow all six.

1. **Translucency is conditional.** Glass panels must sit on a vivid, high-contrast background. A glass panel on a flat grey background is a dead panel. Always pair glass with a mesh gradient, photo, or animated color field.
2. **Depth is layered.** Stack at least two depths: background layer (mesh gradient), midground layer (glass cards), foreground layer (accent elements, CTA). Each layer gets a different blur intensity and shadow depth.
3. **Light refracts on edges.** Every glass panel gets a 1px inner border with `rgba(255,255,255,0.15-0.25)` and an inset highlight on the top edge. This is what separates real glass from cheap glassmorphism.
4. **Corner radius is soft.** Glass panels use `border-radius: 20-28px`. Buttons use 14-18px. Nothing uses 0 except full-bleed sections.
5. **Motion is spring, not linear.** All transitions use `cubic-bezier(0.34, 1.56, 0.64, 1)` or similar overshoot easing. Hover states scale by 1.02, not 1.1. Subtle.
6. **Backgrounds are alive.** The mesh gradient animates slowly (20-40s loop). Orbs drift. The site breathes. But it never distracts from the content, the motion stays below 0.3 intensity.

## Intake (Ask Before Building)

Ask these questions one at a time. Wait for each answer before the next.

1. **Site type.** Landing page, portfolio, product launch, event site, SaaS marketing, or something else?
2. **One-sentence pitch.** What does the site sell, promise, or communicate? This becomes the hero headline.
3. **Primary CTA.** What single action do you want visitors to take? (Sign up, buy, download, contact, RSVP, etc.)
4. **Vibe.** Three words. Examples: "serious, technical, confident" / "playful, bold, energetic" / "calm, premium, trustworthy." This drives the color palette.
5. **Sections needed.** Default is hero + features + CTA. Ask if they want: testimonials, pricing, FAQ, logos, team, stats, changelog, newsletter, or something else.
6. **Brand color (optional).** If they have one, use it as the primary accent. If not, pick based on vibe.

Do not ask about fonts, layout, or technical details. This skill has strong opinions and should apply them.

## Build Steps

1. **Scaffold the HTML.** Single file, semantic HTML5. `<header>`, `<main>` with section tags, `<footer>`.
2. **Apply the design tokens** (CSS variables, see below).
3. **Build the animated mesh background** (see Background Recipes).
4. **Compose the sections** using the glass component patterns.
5. **Add spring motion** on hover states, scroll-triggered reveals for cards, and background drift.
6. **Wire any interactive bits** with minimal vanilla JS (no frameworks, no build step).
7. **Test dark/light.** Default is dark. If the user wants light, flip the token set.
8. **Save** as `index.html` in the user's chosen directory. Default: `./liquid-glass-site/index.html`.

## Design Tokens (Use Verbatim)

Drop this `:root` block into every site. Tune accent colors per vibe.

```css
:root {
  /* Surfaces */
  --glass-bg: rgba(255, 255, 255, 0.06);
  --glass-bg-strong: rgba(255, 255, 255, 0.12);
  --glass-border: rgba(255, 255, 255, 0.18);
  --glass-border-strong: rgba(255, 255, 255, 0.28);
  --glass-highlight: rgba(255, 255, 255, 0.25);

  /* Depth */
  --shadow-glass: 0 8px 32px rgba(0, 0, 0, 0.25),
                  inset 0 1px 0 0 var(--glass-highlight);
  --shadow-glass-lg: 0 24px 64px rgba(0, 0, 0, 0.4),
                     inset 0 1px 0 0 var(--glass-highlight);

  /* Blur */
  --blur-soft: blur(12px) saturate(160%);
  --blur-med: blur(24px) saturate(180%);
  --blur-hard: blur(48px) saturate(200%);

  /* Radius */
  --r-sm: 12px;
  --r-md: 20px;
  --r-lg: 28px;
  --r-xl: 40px;

  /* Motion */
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --ease-smooth: cubic-bezier(0.4, 0, 0.2, 1);

  /* Text */
  --text: #ffffff;
  --text-soft: rgba(255, 255, 255, 0.72);
  --text-dim: rgba(255, 255, 255, 0.5);

  /* Background base */
  --bg: #0a0a12;

  /* Accent palette (tune per vibe) */
  --accent-1: #7c3aed; /* violet */
  --accent-2: #ec4899; /* pink */
  --accent-3: #06b6d4; /* cyan */
}

* { box-sizing: border-box; margin: 0; padding: 0; }
html, body { background: var(--bg); color: var(--text); overflow-x: hidden; }
body { font: 16px/1.6 -apple-system, BlinkMacSystemFont, "SF Pro Display", "Inter", system-ui, sans-serif; }
```

## Vibe-to-Palette Mapping

| Vibe keywords | Accent 1 | Accent 2 | Accent 3 | Base |
|---------------|----------|----------|----------|------|
| serious, technical, confident | `#0ea5e9` (sky) | `#6366f1` (indigo) | `#06b6d4` (cyan) | `#030712` |
| playful, bold, energetic | `#f43f5e` (rose) | `#f59e0b` (amber) | `#a855f7` (violet) | `#0a0a12` |
| calm, premium, trustworthy | `#6366f1` (indigo) | `#0ea5e9` (sky) | `#14b8a6` (teal) | `#0c0a1a` |
| warm, human, approachable | `#f97316` (orange) | `#ec4899` (pink) | `#eab308` (yellow) | `#1a0a0a` |
| futuristic, AI, edge | `#a855f7` (violet) | `#06b6d4` (cyan) | `#22d3ee` (bright cyan) | `#050010` |

## Background Recipes (Pick One)

### Recipe A: Animated Mesh Gradient (default, broadest appeal)

```css
.mesh-bg {
  position: fixed;
  inset: 0;
  z-index: -1;
  background:
    radial-gradient(circle at 15% 20%, var(--accent-1), transparent 45%),
    radial-gradient(circle at 85% 15%, var(--accent-2), transparent 45%),
    radial-gradient(circle at 50% 90%, var(--accent-3), transparent 45%),
    var(--bg);
  filter: blur(80px) saturate(140%);
  animation: mesh-drift 30s ease-in-out infinite;
}
@keyframes mesh-drift {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(-3%, 2%) scale(1.05); }
  66% { transform: translate(2%, -3%) scale(0.98); }
}
```

```html
<div class="mesh-bg" aria-hidden="true"></div>
```

### Recipe B: Floating Orbs (more playful)

```css
.orbs { position: fixed; inset: 0; z-index: -1; overflow: hidden; background: var(--bg); }
.orbs::before, .orbs::after {
  content: ""; position: absolute; width: 50vmax; height: 50vmax; border-radius: 50%;
  filter: blur(120px); opacity: 0.6;
}
.orbs::before { background: var(--accent-1); top: -20vmax; left: -15vmax; animation: orb-a 24s ease-in-out infinite; }
.orbs::after { background: var(--accent-2); bottom: -20vmax; right: -15vmax; animation: orb-b 28s ease-in-out infinite; }
@keyframes orb-a { 50% { transform: translate(20vw, 30vh); } }
@keyframes orb-b { 50% { transform: translate(-20vw, -30vh); } }
```

### Recipe C: Conic Aurora (for futuristic vibe)

```css
.aurora { position: fixed; inset: -20%; z-index: -1; background: var(--bg); }
.aurora::before {
  content: ""; position: absolute; inset: 0;
  background: conic-gradient(from 0deg at 50% 50%, var(--accent-1), var(--accent-2), var(--accent-3), var(--accent-1));
  filter: blur(100px); opacity: 0.5; animation: spin 40s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
```

## Glass Component Library

### Glass Card (the workhorse)

```css
.glass-card {
  background: var(--glass-bg);
  backdrop-filter: var(--blur-med);
  -webkit-backdrop-filter: var(--blur-med);
  border: 1px solid var(--glass-border);
  border-radius: var(--r-lg);
  box-shadow: var(--shadow-glass);
  padding: 32px;
  transition: all 0.4s var(--ease-spring);
}
.glass-card:hover {
  transform: translateY(-4px) scale(1.01);
  background: var(--glass-bg-strong);
  border-color: var(--glass-border-strong);
  box-shadow: var(--shadow-glass-lg);
}
```

### Primary CTA Button

```css
.cta {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 14px 28px;
  background: linear-gradient(135deg, var(--accent-1), var(--accent-2));
  border: 1px solid var(--glass-border-strong);
  border-radius: var(--r-sm);
  color: white; font-weight: 600; text-decoration: none;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.3);
  transition: all 0.3s var(--ease-spring);
}
.cta:hover { transform: translateY(-2px) scale(1.02); box-shadow: 0 12px 32px rgba(0, 0, 0, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.4); }
.cta:active { transform: translateY(0) scale(0.99); }
```

### Glass Nav (sticky dock style)

```css
.nav {
  position: fixed; top: 16px; left: 50%; transform: translateX(-50%);
  display: flex; gap: 4px; padding: 8px;
  background: var(--glass-bg);
  backdrop-filter: var(--blur-med);
  -webkit-backdrop-filter: var(--blur-med);
  border: 1px solid var(--glass-border);
  border-radius: 100px;
  box-shadow: var(--shadow-glass);
  z-index: 100;
}
.nav a { padding: 8px 16px; border-radius: 100px; color: var(--text-soft); text-decoration: none; transition: all 0.2s var(--ease-smooth); }
.nav a:hover { background: var(--glass-bg-strong); color: var(--text); }
```

### Section Scaffold

```css
section { padding: 96px 24px; max-width: 1200px; margin: 0 auto; }
.hero { min-height: 90vh; display: flex; flex-direction: column; justify-content: center; }
h1 { font-size: clamp(42px, 7vw, 88px); font-weight: 700; line-height: 1.05; letter-spacing: -0.02em; margin-bottom: 24px; }
h2 { font-size: clamp(32px, 4vw, 56px); font-weight: 600; letter-spacing: -0.01em; margin-bottom: 20px; }
p.lead { font-size: clamp(18px, 2vw, 22px); color: var(--text-soft); max-width: 60ch; margin-bottom: 40px; }
.grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 24px; }
```

### Scroll Reveal (one JS hook, no library)

```html
<script>
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => e.isIntersecting && e.target.classList.add("in"));
}, { threshold: 0.15 });
document.querySelectorAll("[data-reveal]").forEach(el => io.observe(el));
</script>
<style>
[data-reveal] { opacity: 0; transform: translateY(24px); transition: opacity 0.8s var(--ease-smooth), transform 0.8s var(--ease-spring); }
[data-reveal].in { opacity: 1; transform: none; }
</style>
```

## Section Templates (Compose As Needed)

**Hero**
```html
<section class="hero">
  <h1 data-reveal>[one-sentence pitch, break over 2 lines]</h1>
  <p class="lead" data-reveal>[subheadline, 1-2 sentences, concrete benefit]</p>
  <div data-reveal><a class="cta" href="#cta">[CTA label] →</a></div>
</section>
```

**Feature Grid**
```html
<section>
  <h2 data-reveal>[section headline]</h2>
  <div class="grid-3">
    <div class="glass-card" data-reveal><h3>[feature]</h3><p>[benefit]</p></div>
    <!-- repeat 3-6 cards -->
  </div>
</section>
```

**CTA Section**
```html
<section style="text-align: center;">
  <div class="glass-card" data-reveal style="padding: 64px; max-width: 640px; margin: 0 auto;">
    <h2>[final pitch line]</h2>
    <p class="lead">[reinforcement]</p>
    <a class="cta" href="[link]">[CTA]</a>
  </div>
</section>
```

## Anti-Patterns (Do Not Ship These)

- Glass cards on a flat background. Dead panels. Always pair with vivid backgrounds.
- Over-blurred text (text should be at 100% opacity against glass, never translucent).
- Low contrast accent colors that disappear on the mesh background.
- More than three accent colors in the palette. Becomes clownish.
- Hover scales above 1.05. Breaks the "premium restraint" feel.
- Linear transitions on interactive elements. Always use the spring curve.
- Backdrop-filter without `-webkit-backdrop-filter` fallback (Safari still needs it).
- More than one full-bleed animated element. The eye has nowhere to rest.
- Generic stock icons or emoji as feature bullets. Use minimal SVG line icons or skip icons entirely.
- Lorem ipsum in the final output. Always write real copy from the intake answers.

## Verification Before Shipping

Check each before reporting the site as done:

- [ ] Single HTML file, opens in browser with no build step, no network calls for dependencies.
- [ ] Background is animated (mesh, orbs, or aurora).
- [ ] Every glass panel has: backdrop-filter, 1px inner border, inset highlight shadow, 20-28px corner radius.
- [ ] Primary CTA uses the accent gradient, not a flat color.
- [ ] Nav is a floating dock at the top, not a full-width bar.
- [ ] Hero headline is readable on the animated background (check contrast).
- [ ] At least one scroll-reveal element (the `data-reveal` hook).
- [ ] No lorem ipsum. All copy derived from intake answers.
- [ ] Works on mobile (viewport meta tag, responsive grid, no horizontal scroll).
- [ ] File size under 40KB. If above, the skill is generating too much, trim.

## Output

Save to `./liquid-glass-site/index.html` by default, or the user's chosen path. Report the absolute path and one line on what to tune if they want a different vibe.

Offer to open it in the browser for them: `open ./liquid-glass-site/index.html` (macOS) or `xdg-open` (Linux).

## Extending

To add more sections (pricing, testimonials, FAQ), reuse the glass-card pattern with different content structures. The design system is consistent, so new sections drop in without breaking the aesthetic.
