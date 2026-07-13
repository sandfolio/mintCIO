# TechCircle Component Patterns

Copy-paste HTML + CSS. All assume `tokens.css` is loaded. Every card: sharp corners, hairline borders, the standard hover grammar (zoom + underline + fill).

## 1. Badges & meta row (used on every card)

```html
<div class="badges"><span class="badge">Cloud</span><span class="badge">AI</span></div>
<h3>Headline in Young Serif</h3>
<div class="meta">
  <span class="author">Priya Sharma</span>
  <span class="sep"></span>
  <span class="date">12 Jul 2026</span>
</div>
```
```css
.badges{display:flex;gap:16px;}
.badge{border:1px solid var(--border);padding:4px 8px;font-family:var(--font-mono);
  font-size:12px;font-weight:500;letter-spacing:1.44px;color:var(--caption);
  text-transform:uppercase;line-height:1.5;white-space:nowrap;}
.meta{display:flex;align-items:center;gap:8px;font-family:var(--font-mono);font-size:13px;}
.meta .author{color:var(--blue);font-weight:500;}
.meta .sep{width:1px;height:15px;background:var(--border);}
.meta .date{color:var(--caption);}
```
On dark/image backgrounds: badge `color:#fff;border-color:#fff;background:transparent`; author `#9eb4ff`; date `#c7cdda`; sep `rgba(255,255,255,.5)`.

## 2. Section head (orange bar)

```html
<div class="section-head">
  <div class="left">
    <div class="bar"></div>
    <div><h2>Opinion</h2><p class="sub">Sharp takes from the corner office</p></div>
  </div>
  <a class="view-all" href="#">View all</a>
</div>
```
```css
.section{padding-top:110px;}
.section-head{display:flex;align-items:flex-end;justify-content:space-between;padding-bottom:24px;}
.section-head .left{display:flex;gap:9px;}
.section-head .bar{width:3px;background:var(--mint);align-self:stretch;}
.section-head h2{font-size:40px;line-height:1.15;letter-spacing:-1px;}
.section-head .sub{font-size:14px;color:var(--caption);margin-top:14px;}
.view-all{border:1px solid var(--border);padding:8px 16px;font-size:15px;font-weight:600;color:var(--heading);}
.view-all:hover{background:var(--gray-100);}
```

## 3. Standard card hover grammar (apply to every interactive card)

```css
.card{cursor:pointer;position:relative;transition:border-color .2s ease;}
.card::before{content:"";position:absolute;inset:0 0 auto 0;height:0;
  background:var(--hover-fill);z-index:0;pointer-events:none;transition:height .35s ease;}
.card:hover::before{height:100%;}
.card > *{position:relative;z-index:1;}
.card:hover h3{text-decoration:underline;text-underline-offset:3px;text-decoration-thickness:1.5px;}
.card .thumb{overflow:hidden;}
.card .thumb img{width:100%;height:100%;object-fit:cover;transition:transform .35s ease;will-change:transform;}
.card:hover .thumb img{transform:scale(1.08);} /* 1.05 for large features */
@media (hover:none){.card:hover::before{height:0;}.card:hover .thumb img{transform:none;}}
@media (prefers-reduced-motion:reduce){.card::before,.card .thumb img{transition:none;}
  .card:hover .thumb img{transform:none;}}
```
Inside the events band, fill is `--band-events-fill` and hover border `--band-events-border`.

## 4. Header (black bar) + secondary mono nav

```html
<header>
  <div class="top-bar">
    <div class="brand"><span class="tc">techcircle</span></div>
    <nav class="primary-nav">
      <a class="nav-link" href="#">News</a>
      <div class="nav-item"><button class="nav-link">Topics <svg class="caret">…</svg></button>
        <div class="nav-dropdown"><a href="#">AI<span class="dd-sub">Models & policy</span></a></div>
      </div>
    </nav>
    <div class="top-right">
      <a class="insights-link" href="#">TC Insights</a>
      <form class="search"><input placeholder="Search"><button>🔍</button></form>
      <a class="login-link" href="#">Login</a>
    </div>
  </div>
</header>
<nav class="secondary-nav"><div class="secondary-nav-inner">
  <div class="snav-item"><a class="snav-link" href="#">Startups</a></div>
</div></nav>
```
Key styles: header `background:#000`; `.top-bar{max-width:1280px;padding:16px 0;display:flex;gap:32px}`; primary links Poppins 15/500 uppercase white, hover `--mint`; insights CTA `--navy` bg, mono 12 uppercase, 36px tall; search `#333` bg, 36px, 200px wide, no radius; secondary nav `--neutral-200` bg, links IBM Plex Mono 14/500 uppercase, `padding:14px 16px`, hover `--blue`; dropdowns white, `--shadow-dropdown`, slide 6px on open. ≤560px: hamburger + right slide-in drawer (`#0b0f14`, 300px, Poppins 16 uppercase links, accordion subgroups).

## 5. Hero v6 (image-backed grid — v6.3 flagship)

Layout: `grid-template-columns:575px 1fr; gap:24px; height:724px`. Left = tall feature; right = row of 2 cards (47%) over 1 wide card (53%).

```html
<section class="hero-v6">
  <article class="hv6-main"><img src="…">
    <div class="hv6-shade"></div>
    <div class="hv6-cap"><span class="badge">Feature</span><h2>Headline</h2>
      <div class="meta">…</div></div>
  </article>
  <div class="hv6-right">
    <div class="hv6-row">
      <article class="hv6-card"><div class="play-badge">▶</div><img src="…">
        <div class="hv6-shade"></div><div class="hv6-cap">…<h3>…</h3>…</div></article>
      <article class="hv6-card">…</article>
    </div>
    <article class="hv6-wide">…</article>
  </div>
</section>
```
Shade: `linear-gradient(to bottom, rgba(0,0,0,0) 40%, rgba(0,0,0,.9) 92%)`. Caption 24px inset, white text, h2 36px / card h3 24px (clamp 3) / wide h3 30px (clamp 2). Play badge: 52px circle `rgba(0,0,0,.55)` top-left, hover `--mint`. Mobile: single column, main 3/4, cards 16/10.

## 6. Hero v5 (dark feature + thumbnail list — v5.7 variant)

`grid-template-columns:700px 1px 1fr`. Feature 700×632 dark (`--dark-0`) with shade `rgba(0,0,0,0) 35% → rgba(0,0,0,.92) 88%`, caption h2 42px white. Divider 1px `--border`. Right: `.hv5-item` rows `grid-template-columns:132px 1fr; gap:24px; padding:16px 0`, hairline separated, 132px square thumbs (centered 44px play badge when playable), h3 22px clamp-2.

## 7. Hero v3 (bordered frame + dark navy panel)

Flex, 600px tall, `border:1px solid var(--border)`, `--shadow-hero`. Left 850px image with bottom glass overlay: `rgba(255,255,255,.9)` + `backdrop-filter:blur(8px)`, h2 28px. Right panel `linear-gradient(180deg,#0b0f14,#111827)`, orange 3px bar + white h3 24 + mono sub `#cbd5e1`; items `#0f172a` separated by `rgba(255,255,255,.08)`, hover `#13203a`.

## 8. Event card (cream band)

```html
<section class="events-section"><div class="wrap">
  <article class="ev-card">
    <div class="ev-img"><img src="…">
      <div class="ev-date"><span class="ev-mon">Sep</span><span class="ev-day">18</span></div></div>
    <div class="ev-body">
      <div class="badges"><span class="badge">Summit</span></div>
      <h3>TechCircle CIO Summit 2026</h3>
      <div class="ev-meta"><span class="ev-metaitem">📍 Mumbai</span><span class="ev-metaitem">🕘 9:00 AM</span></div>
      <button class="ev-btn">Register →</button>
    </div>
  </article>
</div></section>
```
Band `--band-events` bg, 80px pad. Card `--band-events-card` bg, hairline, `grid-template-columns:360px 1fr`, hover shadow `--shadow-card-hover`. Date chip 56px square `--dark-0`, mono (mon 11px uppercase / day 22px 600). h3 32px. `.ev-btn`: transparent, `1px solid var(--heading)`, mono 13/600 uppercase, `padding:9px 18px`, hover inverts to black/white.

## 9. Report / outlined-orange CTA

```css
.report-play{display:inline-flex;align-items:center;gap:10px;border:1px solid var(--mint);
  color:var(--mint-600);background:#fff;font-family:var(--font-nav);font-size:14px;
  font-weight:600;padding:9px 18px;}
.report-play:hover{background:var(--mint);color:#fff;}
```
Report block: `grid-template-columns:744px 1fr`, hairline frame, body `padding:32px`, h2 40px, desc Inter 16/1.6 `--caption`.

## 10. Reader poll

Grid `1fr 300px`. Card hairline, `padding:40px`; question Young Serif 32. Options: white hairline buttons `padding:20px 22px`; title Young Serif 22; after vote → orange fill `rgba(249,157,28,.14)` animates `width 0→N%` with `.8s cubic-bezier(.22,.61,.36,1)`, 3px `--mint` baseline, mono pct + vote counts fade in; selected option `2px solid var(--mint)`. Sidebar: mono uppercase labels (ls 1.44px), Young Serif 44 total, mono share links in `--blue`, voted flag `rgba(249,157,28,.1)` bg + `--mint-600` text.

## 11. Other patterns (one-liners)

- **CIO video band:** bg `--band-video`, 500px square feature + list of `--band-video-card` rows (170px thumb), hover `--band-video-card-hover`.
- **Podcast:** `624px 1fr` grid, 640px tall; hero shade `rgba(0,0,0,0) 20% → #000 84.6%`, h2 42; 3-up hairline `.pod-card{padding:24px;min-height:185px}` text-only cards.
- **Opinion:** `600px 1fr`; square feature img, h3 28; rows `200px 1fr` with 200px square thumbs, h3 24.
- **Media/POV cards:** 3-up, hairline, square photo, white 56px play badge bottom-left, body `padding:28px`.
- **Minutes:** 2-col rows `200px 1fr`, `padding:24px`, odd rows right-hairline, h3 18.
- **Newsletter:** 2-col, rows `215px 1fr`, 215px square thumbs, `padding:30px 0`.
- **Hub grid:** 4-up (2-up ≤1024, 1-up ≤560), square img, body `padding:24px 16px 0`, h3 22.
- **Footer:** hairline top, `padding:40px 0`, Lato 800 wordmark (mint accent word), copy 13px `--caption`.
