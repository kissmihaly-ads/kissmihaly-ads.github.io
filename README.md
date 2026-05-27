<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Portfolio — Content Studio</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #080808;
    --surface: #111111;
    --surface2: #1a1a1a;
    --border: #222222;
    --border2: #2e2e2e;
    --gold: #c9a84c;
    --gold-dim: #7a6230;
    --gold-glow: rgba(201,168,76,0.12);
    --white: #f0ede8;
    --muted: #666666;
    --muted2: #444444;
    --red: #e05252;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* grain overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 999;
    opacity: 0.4;
  }

  /* nav */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px 48px;
    background: linear-gradient(to bottom, rgba(8,8,8,0.95) 0%, transparent 100%);
    backdrop-filter: blur(8px);
  }
  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 22px;
    letter-spacing: 0.15em;
    color: var(--white);
  }
  .nav-logo span { color: var(--gold); }
  .nav-cta {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--gold);
    border: 0.5px solid var(--gold-dim);
    padding: 8px 18px;
    cursor: pointer;
    text-decoration: none;
    transition: all 0.2s;
    background: var(--gold-glow);
  }
  .nav-cta:hover { background: rgba(201,168,76,0.2); border-color: var(--gold); }

  /* hero */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 120px 48px 80px;
    position: relative;
    overflow: hidden;
  }
  .hero::after {
    content: '';
    position: absolute;
    bottom: -200px; right: -200px;
    width: 600px; height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(201,168,76,0.07) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.7s 0.1s ease forwards;
  }
  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(64px, 9vw, 130px);
    line-height: 0.92;
    letter-spacing: 0.02em;
    color: var(--white);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.7s 0.25s ease forwards;
  }
  .hero-title .line2 { color: var(--gold); display: block; }
  .hero-sub {
    font-size: 16px;
    font-weight: 300;
    color: var(--muted);
    max-width: 480px;
    line-height: 1.7;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.7s 0.4s ease forwards;
  }
  .hero-stats {
    display: flex;
    gap: 48px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.7s 0.55s ease forwards;
  }
  .hero-stat-val {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 36px;
    color: var(--white);
    letter-spacing: 0.05em;
  }
  .hero-stat-label {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
    text-transform: uppercase;
    font-family: 'DM Mono', monospace;
  }

  /* scroll indicator */
  .scroll-hint {
    position: absolute;
    bottom: 40px; left: 48px;
    display: flex;
    align-items: center;
    gap: 12px;
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted2);
    opacity: 0;
    animation: fadeUp 0.7s 0.8s ease forwards;
  }
  .scroll-line {
    width: 40px;
    height: 0.5px;
    background: var(--muted2);
    position: relative;
    overflow: hidden;
  }
  .scroll-line::after {
    content: '';
    position: absolute;
    left: -100%; top: 0;
    width: 100%; height: 100%;
    background: var(--gold);
    animation: slide 2s infinite;
  }

  /* section */
  .section {
    padding: 80px 48px;
    max-width: 1400px;
    margin: 0 auto;
  }
  .section-header {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    margin-bottom: 48px;
    border-bottom: 0.5px solid var(--border);
    padding-bottom: 20px;
  }
  .section-num {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--gold);
    letter-spacing: 0.15em;
    margin-bottom: 6px;
  }
  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 42px;
    letter-spacing: 0.05em;
    color: var(--white);
    line-height: 1;
  }
  .section-count {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
  }

  /* portfolio grid */
  .portfolio-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 2px;
  }

  /* video card */
  .video-card {
    background: var(--surface);
    position: relative;
    overflow: hidden;
    cursor: pointer;
    group: true;
  }
  .video-card:hover .card-overlay { opacity: 1; }
  .video-card:hover .card-thumb { transform: scale(1.03); }

  .card-thumb-wrap {
    aspect-ratio: 9/16;
    overflow: hidden;
    background: var(--surface2);
    position: relative;
  }
  .card-thumb {
    width: 100%; height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
    display: block;
  }
  .card-video {
    width: 100%; height: 100%;
    object-fit: cover;
    display: block;
  }
  .card-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.2) 50%, transparent 100%);
    opacity: 0;
    transition: opacity 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .play-btn {
    width: 56px; height: 56px;
    border-radius: 50%;
    background: rgba(201,168,76,0.9);
    display: flex; align-items: center; justify-content: center;
    transition: transform 0.2s;
  }
  .play-btn:hover { transform: scale(1.1); }
  .play-btn svg { margin-left: 4px; }

  .card-placeholder {
    aspect-ratio: 9/16;
    background: var(--surface2);
    border: 1px dashed var(--border2);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 12px;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
  }
  .card-placeholder:hover {
    border-color: var(--gold-dim);
    background: var(--gold-glow);
  }
  .card-placeholder input[type="file"] {
    position: absolute;
    inset: 0;
    opacity: 0;
    cursor: pointer;
    width: 100%;
    height: 100%;
  }
  .upload-icon { color: var(--muted2); transition: color 0.2s; }
  .card-placeholder:hover .upload-icon { color: var(--gold); }
  .upload-text {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted2);
    text-align: center;
    transition: color 0.2s;
  }
  .card-placeholder:hover .upload-text { color: var(--gold-dim); }

  .card-info {
    padding: 16px 18px 20px;
    border-top: 0.5px solid var(--border);
  }
  .card-type {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 6px;
  }
  .card-title {
    font-size: 15px;
    font-weight: 500;
    color: var(--white);
    margin-bottom: 6px;
    line-height: 1.3;
  }
  .card-desc {
    font-size: 12px;
    font-weight: 300;
    color: var(--muted);
    line-height: 1.6;
  }
  .card-tag-row {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
    margin-top: 10px;
  }
  .card-tag {
    font-size: 10px;
    padding: 2px 8px;
    border: 0.5px solid var(--border2);
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.06em;
  }

  /* lightbox */
  .lightbox {
    position: fixed;
    inset: 0;
    z-index: 200;
    background: rgba(0,0,0,0.95);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s;
  }
  .lightbox.open {
    opacity: 1;
    pointer-events: all;
  }
  .lightbox-inner {
    position: relative;
    max-width: 420px;
    width: 90%;
  }
  .lightbox-inner video {
    width: 100%;
    border-radius: 2px;
    display: block;
  }
  .lightbox-close {
    position: absolute;
    top: -40px; right: 0;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.12em;
    color: var(--muted);
    cursor: pointer;
    text-transform: uppercase;
  }
  .lightbox-close:hover { color: var(--white); }
  .lightbox-info {
    margin-top: 16px;
  }
  .lightbox-type {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 6px;
  }
  .lightbox-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 0.05em;
    color: var(--white);
    margin-bottom: 6px;
  }
  .lightbox-desc {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.6;
  }

  /* services strip */
  .services-strip {
    border-top: 0.5px solid var(--border);
    border-bottom: 0.5px solid var(--border);
    padding: 48px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 40px;
  }
  .service-item {}
  .service-num {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--gold);
    letter-spacing: 0.12em;
    margin-bottom: 10px;
  }
  .service-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 22px;
    letter-spacing: 0.06em;
    color: var(--white);
    margin-bottom: 8px;
  }
  .service-desc {
    font-size: 12px;
    font-weight: 300;
    color: var(--muted);
    line-height: 1.6;
  }

  /* CTA section */
  .cta-section {
    padding: 120px 48px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .cta-section::before {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 300px;
    background: radial-gradient(ellipse, rgba(201,168,76,0.06) 0%, transparent 70%);
    pointer-events: none;
  }
  .cta-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 20px;
  }
  .cta-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(48px, 7vw, 96px);
    letter-spacing: 0.03em;
    color: var(--white);
    line-height: 0.95;
    margin-bottom: 24px;
  }
  .cta-sub {
    font-size: 15px;
    color: var(--muted);
    max-width: 400px;
    margin: 0 auto 40px;
    line-height: 1.7;
  }
  .cta-btn {
    display: inline-block;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--black);
    background: var(--gold);
    padding: 16px 40px;
    cursor: pointer;
    text-decoration: none;
    transition: all 0.2s;
  }
  .cta-btn:hover { background: #d4b566; transform: translateY(-1px); }

  /* edit mode overlay */
  .edit-bar {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 150;
    background: var(--surface);
    border: 0.5px solid var(--border2);
    padding: 10px 20px;
    display: flex;
    align-items: center;
    gap: 16px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
    box-shadow: 0 8px 32px rgba(0,0,0,0.5);
  }
  .edit-toggle {
    color: var(--gold);
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 0.12em;
  }
  .edit-toggle:hover { color: #d4b566; }
  .edit-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--gold); animation: pulse 2s infinite; }

  /* name editor */
  .editable {
    outline: none;
    border-bottom: 0.5px solid transparent;
    transition: border-color 0.2s;
  }
  body.edit-mode .editable {
    border-bottom-color: var(--gold-dim);
  }
  body.edit-mode .editable:focus {
    border-bottom-color: var(--gold);
  }

  /* footer */
  footer {
    padding: 32px 48px;
    border-top: 0.5px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 12px;
  }
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 18px;
    letter-spacing: 0.15em;
    color: var(--muted2);
  }
  .footer-copy {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--muted2);
    letter-spacing: 0.08em;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes slide {
    0% { left: -100%; }
    100% { left: 100%; }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  @media (max-width: 640px) {
    nav, .hero, .section, .services-strip, .cta-section, footer { padding-left: 20px; padding-right: 20px; }
    .hero-stats { gap: 28px; }
    .portfolio-grid { grid-template-columns: 1fr 1fr; gap: 2px; }
  }
</style>
</head>
<body>

<nav>
  <div class="nav-logo"><span contenteditable="true" class="editable" id="studio-name">STUDIO</span> <span>✦</span></div>
  <a class="nav-cta" href="#contact">Book a call</a>
</nav>

<section class="hero">
  <div class="hero-eyebrow">Content production studio</div>
  <h1 class="hero-title">
    We make content<br>
    <span class="line2">that converts.</span>
  </h1>
  <p class="hero-sub">Video ads, UGC, AI content, and organic social — all produced remotely. We handle everything except the camera.</p>
  <div class="hero-stats">
    <div>
      <div class="hero-stat-val" contenteditable="true" class="editable">9</div>
      <div class="hero-stat-label">Portfolio pieces</div>
    </div>
    <div>
      <div class="hero-stat-val" contenteditable="true" class="editable">3</div>
      <div class="hero-stat-label">Content formats</div>
    </div>
    <div>
      <div class="hero-stat-val" contenteditable="true" class="editable">100%</div>
      <div class="hero-stat-label">Remote delivery</div>
    </div>
  </div>
  <div class="scroll-hint">
    <div class="scroll-line"></div>
    Scroll to work
  </div>
</section>

<div class="services-strip">
  <div class="service-item">
    <div class="service-num">01</div>
    <div class="service-name">Video Ad Creative</div>
    <div class="service-desc">Performance-driven scripts, UGC production, and AI content built to convert on Meta and TikTok.</div>
  </div>
  <div class="service-item">
    <div class="service-num">02</div>
    <div class="service-name">Organic Content</div>
    <div class="service-desc">Full-service organic social management — strategy, scripts, creators, editing, and posting.</div>
  </div>
  <div class="service-item">
    <div class="service-num">03</div>
    <div class="service-name">AI UGC</div>
    <div class="service-desc">AI avatar videos for hook testing, testimonials, and volume — at a fraction of the cost of real creators.</div>
  </div>
  <div class="service-item">
    <div class="service-num">04</div>
    <div class="service-name">Hook Testing</div>
    <div class="service-desc">Multiple hook variants per brief — find what converts before scaling your ad spend.</div>
  </div>
</div>

<section class="section">
  <div class="section-header">
    <div>
      <div class="section-num">02 — WORK</div>
      <div class="section-title">Selected Work</div>
    </div>
    <div class="section-count" id="count-label">0 / 9 uploaded</div>
  </div>
  <div class="portfolio-grid" id="grid"></div>
</section>

<section class="cta-section" id="contact">
  <div class="cta-eyebrow">Ready to grow?</div>
  <div class="cta-title">Let's build<br>something.</div>
  <p class="cta-sub">We work with a small number of brands at a time. If you're serious about organic and paid content, let's talk.</p>
  <a class="cta-btn" href="mailto:your@email.com" id="contact-email">Get in touch</a>
</section>

<footer>
  <div class="footer-logo" contenteditable="true" class="editable">STUDIO ✦</div>
  <div class="footer-copy">© 2025 — All rights reserved</div>
</footer>

<div class="edit-bar">
  <div class="edit-dot"></div>
  <span>Edit mode</span>
  <span class="edit-toggle" onclick="toggleEdit()">Enable</span>
  <span style="color:var(--border2)">|</span>
  <span style="color:var(--muted2)">Click fields to customise</span>
</div>

<div class="lightbox" id="lightbox" onclick="closeLightbox(event)">
  <div class="lightbox-inner" id="lightbox-inner">
    <div class="lightbox-close" onclick="closeLightboxBtn()">Close ×</div>
    <video id="lightbox-video" controls playsinline></video>
    <div class="lightbox-info">
      <div class="lightbox-type" id="lb-type"></div>
      <div class="lightbox-title" id="lb-title"></div>
      <div class="lightbox-desc" id="lb-desc"></div>
    </div>
  </div>
</div>

<script>
const slots = [
  { type: "AI UGC", title: "Benefit Explainer", desc: "AI avatar walking through key product benefits. Hook-tested format optimised for cold audiences.", tags: ["Paid Ad", "AI UGC", "Top of Funnel"] },
  { type: "AI UGC", title: "Testimonial Format", desc: "AI-generated testimonial-style video. Ideal for social proof and retargeting campaigns.", tags: ["Paid Ad", "AI UGC", "Retargeting"] },
  { type: "AI Animated", title: "Product Character — Origin", desc: "The product becomes the hero. Animated origin story format for brand awareness.", tags: ["Organic", "AI Animated", "Brand Story"] },
  { type: "AI Animated", title: "Product Character — CTA", desc: "Animated product character driving a direct call to action. High memorability format.", tags: ["Paid Ad", "AI Animated", "Conversion"] },
  { type: "Hook Variation Set", title: "3 Hooks — Same Product", desc: "Problem/solution, curiosity, and bold claim hooks for the same product. Shows creative range.", tags: ["Paid Ad", "Strategy", "Testing"] },
  { type: "Real UGC", title: "Authentic Testimonial", desc: "Real person, real product, authentic delivery. The highest-trust format for cold traffic.", tags: ["Paid Ad", "Real UGC", "Trust"] },
  { type: "Organic Short-Form", title: "Trending Audio Cut", desc: "Native TikTok/Reels format — aesthetic shots cut to trending sound. Built for organic reach.", tags: ["Organic", "Short-Form", "Viral"] },
  { type: "Narrative Ad", title: "Before / After Arc", desc: "Tension and resolution structure. Problem introduced, product delivers transformation.", tags: ["Paid Ad", "Narrative", "Mid-Funnel"] },
  { type: "Educational", title: "Ingredient Explainer", desc: "Fast-cut educational format. Builds trust and authority. Performs on both paid and organic.", tags: ["Organic", "Education", "Trust"] },
];

let videos = {};
let editMode = false;

function renderGrid() {
  const grid = document.getElementById('grid');
  const uploaded = Object.keys(videos).length;
  document.getElementById('count-label').textContent = `${uploaded} / ${slots.length} uploaded`;

  grid.innerHTML = slots.map((s, i) => {
    const hasVideo = videos[i];
    return `
    <div class="video-card">
      ${hasVideo ? `
        <div class="card-thumb-wrap" onclick="openLightbox(${i})">
          <video class="card-video" src="${hasVideo}" muted loop playsinline
            onmouseenter="this.play()" onmouseleave="this.pause();this.currentTime=0"></video>
          <div class="card-overlay">
            <div class="play-btn">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="white"><path d="M8 5v14l11-7z"/></svg>
            </div>
          </div>
        </div>
      ` : `
        <div class="card-placeholder" onclick="triggerUpload(${i})">
          <input type="file" accept="video/*" onchange="handleUpload(event, ${i})" onclick="event.stopPropagation()">
          <svg class="upload-icon" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
            <polyline points="17 8 12 3 7 8"/>
            <line x1="12" y1="3" x2="12" y2="15"/>
          </svg>
          <div class="upload-text">Upload video</div>
        </div>
      `}
      <div class="card-info">
        <div class="card-type">${s.type}</div>
        <div class="card-title" contenteditable="${editMode}" class="editable">${s.title}</div>
        <div class="card-desc" contenteditable="${editMode}" class="editable">${s.desc}</div>
        <div class="card-tag-row">${s.tags.map(t => `<span class="card-tag">${t}</span>`).join('')}</div>
      </div>
    </div>`;
  }).join('');
}

function triggerUpload(i) {
  const inputs = document.querySelectorAll('.card-placeholder input[type="file"]');
  if (inputs[i]) inputs[i].click();
}

function handleUpload(event, i) {
  const file = event.target.files[0];
  if (!file) return;
  const url = URL.createObjectURL(file);
  videos[i] = url;
  renderGrid();
}

function openLightbox(i) {
  const s = slots[i];
  const url = videos[i];
  if (!url) return;
  document.getElementById('lightbox-video').src = url;
  document.getElementById('lightbox-video').play();
  document.getElementById('lb-type').textContent = s.type;
  document.getElementById('lb-title').textContent = s.title;
  document.getElementById('lb-desc').textContent = s.desc;
  document.getElementById('lightbox').classList.add('open');
}

function closeLightboxBtn() {
  document.getElementById('lightbox-video').pause();
  document.getElementById('lightbox').classList.remove('open');
}

function closeLightbox(e) {
  if (e.target === document.getElementById('lightbox')) closeLightboxBtn();
}

function toggleEdit() {
  editMode = !editMode;
  document.body.classList.toggle('edit-mode', editMode);
  document.querySelector('.edit-toggle').textContent = editMode ? 'Disable' : 'Enable';
  document.querySelector('.edit-dot').style.background = editMode ? '#e05252' : 'var(--gold)';
  renderGrid();
  if (editMode) {
    document.querySelectorAll('[contenteditable="true"]').forEach(el => {
      el.style.borderBottom = '0.5px solid var(--gold-dim)';
    });
  }
}

document.addEventListener('keydown', e => {
  if (e.key === 'Escape') closeLightboxBtn();
});

renderGrid();
</script>
</body>
</html>
