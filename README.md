<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Kiran Kumar Gajula – Senior iOS Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
:root {
  --bg:       #060B17;
  --surface:  #0C1426;
  --card:     #101C30;
  --border:   #1E3050;
  --blue:     #3B82F6;
  --cyan:     #22D3EE;
  --glow:     rgba(59,130,246,0.15);
  --text:     #E2E8F0;
  --muted:    #64748B;
  --subtle:   #94A3B8;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 16px;
  line-height: 1.6;
  overflow-x: hidden;
}

/* ── CANVAS / STARFIELD ─────────────────────────────── */
#canvas {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  opacity: 0.5;
}

/* ── GRID OVERLAY ───────────────────────────────────── */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(59,130,246,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(59,130,246,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  z-index: 0;
  pointer-events: none;
}

/* ── NOISE GRAIN ────────────────────────────────────── */
body::after {
  content: '';
  position: fixed;
  inset: -50%;
  width: 200%;
  height: 200%;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.05'/%3E%3C/svg%3E");
  opacity: 0.03;
  z-index: 0;
  pointer-events: none;
  animation: grain 8s steps(10) infinite;
}

@keyframes grain {
  0%,100% { transform: translate(0,0); }
  10% { transform: translate(-3%,-3%); }
  20% { transform: translate(3%,1%); }
  30% { transform: translate(-1%,2%); }
  40% { transform: translate(2%,-2%); }
  50% { transform: translate(-2%,3%); }
  60% { transform: translate(1%,-1%); }
  70% { transform: translate(-3%,2%); }
  80% { transform: translate(2%,1%); }
  90% { transform: translate(-1%,-3%); }
}

/* ── WRAPPER ────────────────────────────────────────── */
.wrap { position: relative; z-index: 1; }

/* ── NAV ────────────────────────────────────────────── */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 48px;
  border-bottom: 1px solid transparent;
  transition: all 0.4s ease;
}

nav.scrolled {
  background: rgba(6,11,23,0.85);
  backdrop-filter: blur(20px);
  border-color: var(--border);
}

.nav-logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  color: var(--blue);
  letter-spacing: 0.05em;
  text-decoration: none;
}

.nav-links { display: flex; gap: 36px; }

.nav-links a {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.78rem;
  color: var(--muted);
  text-decoration: none;
  letter-spacing: 0.08em;
  transition: color 0.3s;
}

.nav-links a:hover { color: var(--cyan); }

/* ── HERO ────────────────────────────────────────────── */
#hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 120px 48px 80px;
  max-width: 1200px;
  margin: 0 auto;
}

.hero-tag {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.78rem;
  color: var(--cyan);
  letter-spacing: 0.15em;
  margin-bottom: 24px;
  opacity: 0;
  transform: translateY(20px);
  animation: fadeUp 0.8s 0.2s forwards;
}

.hero-name {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(3rem, 7vw, 6rem);
  line-height: 1.0;
  letter-spacing: -0.03em;
  margin-bottom: 16px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeUp 0.9s 0.4s forwards;
}

.hero-name span {
  background: linear-gradient(135deg, var(--blue), var(--cyan));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-typed {
  font-family: 'JetBrains Mono', monospace;
  font-size: clamp(1rem, 2vw, 1.25rem);
  color: var(--subtle);
  margin-bottom: 32px;
  min-height: 2em;
  opacity: 0;
  animation: fadeUp 0.9s 0.6s forwards;
}

.hero-typed .cursor {
  display: inline-block;
  width: 2px;
  height: 1.1em;
  background: var(--cyan);
  margin-left: 2px;
  vertical-align: middle;
  animation: blink 1s steps(1) infinite;
}

@keyframes blink { 50% { opacity: 0; } }

.hero-desc {
  max-width: 560px;
  color: var(--muted);
  font-size: 1.05rem;
  line-height: 1.7;
  margin-bottom: 48px;
  opacity: 0;
  animation: fadeUp 0.9s 0.8s forwards;
}

.hero-ctas {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  opacity: 0;
  animation: fadeUp 0.9s 1s forwards;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 28px;
  background: var(--blue);
  color: #fff;
  text-decoration: none;
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 0.04em;
  border-radius: 4px;
  transition: all 0.3s;
  box-shadow: 0 0 30px rgba(59,130,246,0.3);
}

.btn-primary:hover {
  background: var(--cyan);
  box-shadow: 0 0 40px rgba(34,211,238,0.4);
  transform: translateY(-2px);
}

.btn-outline {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 13px 28px;
  border: 1px solid var(--border);
  color: var(--subtle);
  text-decoration: none;
  font-family: 'Syne', sans-serif;
  font-weight: 600;
  font-size: 0.9rem;
  letter-spacing: 0.04em;
  border-radius: 4px;
  transition: all 0.3s;
}

.btn-outline:hover {
  border-color: var(--blue);
  color: var(--blue);
  background: var(--glow);
}

.hero-stats {
  display: flex;
  gap: 48px;
  margin-top: 72px;
  padding-top: 40px;
  border-top: 1px solid var(--border);
  opacity: 0;
  animation: fadeUp 0.9s 1.2s forwards;
}

.stat-num {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 2.4rem;
  background: linear-gradient(135deg, var(--blue), var(--cyan));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1;
}

.stat-label {
  font-size: 0.8rem;
  color: var(--muted);
  letter-spacing: 0.05em;
  margin-top: 4px;
}

/* ── SECTIONS ───────────────────────────────────────── */
section {
  padding: 100px 48px;
  max-width: 1200px;
  margin: 0 auto;
}

.section-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  color: var(--cyan);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 12px;
}

.section-title {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(1.8rem, 3.5vw, 2.8rem);
  letter-spacing: -0.02em;
  margin-bottom: 16px;
}

.section-line {
  width: 48px;
  height: 3px;
  background: linear-gradient(to right, var(--blue), var(--cyan));
  margin-bottom: 56px;
  border-radius: 2px;
}

/* ── SKILLS ─────────────────────────────────────────── */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.skill-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 28px;
  transition: all 0.4s;
  position: relative;
  overflow: hidden;
}

.skill-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(to right, var(--blue), var(--cyan));
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.4s;
}

.skill-card:hover { border-color: rgba(59,130,246,0.4); background: #13213A; transform: translateY(-4px); }
.skill-card:hover::before { transform: scaleX(1); }

.skill-cat {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.85rem;
  color: var(--blue);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.skill-tags { display: flex; flex-wrap: wrap; gap: 8px; }

.tag {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  padding: 4px 10px;
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--subtle);
  transition: all 0.2s;
}

.tag:hover { border-color: var(--cyan); color: var(--cyan); background: rgba(34,211,238,0.05); }

/* ── EXPERIENCE TIMELINE ────────────────────────────── */
.timeline { position: relative; padding-left: 32px; }

.timeline::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 1px;
  background: linear-gradient(to bottom, var(--blue), transparent);
}

.tl-item {
  position: relative;
  margin-bottom: 52px;
  opacity: 0;
  transform: translateX(-20px);
  transition: all 0.6s ease;
}

.tl-item.visible { opacity: 1; transform: translateX(0); }

.tl-dot {
  position: absolute;
  left: -38px;
  top: 6px;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--blue);
  border: 2px solid var(--bg);
  box-shadow: 0 0 12px rgba(59,130,246,0.6);
  transition: all 0.3s;
}

.tl-item:hover .tl-dot {
  background: var(--cyan);
  box-shadow: 0 0 20px rgba(34,211,238,0.7);
  transform: scale(1.3);
}

.tl-header { display: flex; flex-wrap: wrap; align-items: flex-start; gap: 12px; margin-bottom: 8px; }

.tl-company {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--text);
}

.tl-badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  padding: 3px 10px;
  border: 1px solid rgba(59,130,246,0.4);
  color: var(--blue);
  border-radius: 50px;
  white-space: nowrap;
}

.tl-role {
  font-size: 0.9rem;
  color: var(--cyan);
  margin-bottom: 4px;
}

.tl-meta {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  color: var(--muted);
  margin-bottom: 16px;
}

.tl-bullets { list-style: none; }

.tl-bullets li {
  font-size: 0.9rem;
  color: var(--muted);
  padding: 5px 0 5px 18px;
  position: relative;
  line-height: 1.55;
}

.tl-bullets li::before {
  content: '›';
  position: absolute;
  left: 0;
  color: var(--blue);
  font-size: 1rem;
}

.highlight { color: var(--text); font-weight: 500; }

/* ── PORTFOLIO CARDS ─────────────────────────────────── */
.apps-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}

.app-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 32px 28px;
  transition: all 0.4s;
  position: relative;
  overflow: hidden;
  text-decoration: none;
  color: inherit;
  display: block;
}

.app-card::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 70% 20%, rgba(59,130,246,0.07), transparent 60%);
  opacity: 0;
  transition: opacity 0.4s;
}

.app-card:hover { border-color: rgba(59,130,246,0.5); transform: translateY(-6px); box-shadow: 0 20px 60px rgba(0,0,0,0.5); }
.app-card:hover::after { opacity: 1; }

.app-icon {
  width: 52px;
  height: 52px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.6rem;
  margin-bottom: 20px;
}

.app-name {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.05rem;
  margin-bottom: 8px;
}

.app-desc { font-size: 0.87rem; color: var(--muted); line-height: 1.6; margin-bottom: 20px; }

.app-tech { display: flex; flex-wrap: wrap; gap: 6px; }

.app-tag {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  padding: 3px 8px;
  background: rgba(59,130,246,0.1);
  color: var(--blue);
  border-radius: 3px;
}

/* ── CONTACT ─────────────────────────────────────────── */
.contact-box {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 60px;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.contact-box::before {
  content: '';
  position: absolute;
  top: -80px; left: 50%;
  transform: translateX(-50%);
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(59,130,246,0.12), transparent 70%);
  pointer-events: none;
}

.contact-title {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 2rem;
  margin-bottom: 12px;
}

.contact-sub { color: var(--muted); margin-bottom: 36px; font-size: 1rem; }

.contact-links { display: flex; justify-content: center; flex-wrap: wrap; gap: 16px; }

.contact-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 12px 24px;
  border: 1px solid var(--border);
  border-radius: 6px;
  text-decoration: none;
  color: var(--subtle);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.82rem;
  transition: all 0.3s;
}

.contact-link:hover { border-color: var(--blue); color: var(--blue); background: var(--glow); }
.contact-link svg { width: 16px; height: 16px; }

/* ── FOOTER ──────────────────────────────────────────── */
footer {
  border-top: 1px solid var(--border);
  padding: 28px 48px;
  text-align: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  color: var(--muted);
  position: relative;
  z-index: 1;
}

/* ── SCROLL REVEAL ───────────────────────────────────── */
.reveal {
  opacity: 0;
  transform: translateY(32px);
  transition: all 0.7s ease;
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

@keyframes fadeUp {
  to { opacity: 1; transform: translateY(0); }
}

/* ── SCROLLBAR ───────────────────────────────────────── */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover { background: var(--blue); }

/* ── RESPONSIVE ──────────────────────────────────────── */
@media (max-width: 768px) {
  nav { padding: 16px 24px; }
  .nav-links { display: none; }
  #hero, section { padding-left: 24px; padding-right: 24px; }
  .hero-stats { gap: 28px; flex-wrap: wrap; }
  .contact-box { padding: 36px 24px; }
}
</style>
</head>
<body>

<canvas id="canvas"></canvas>

<!-- NAV -->
<nav id="nav">
  <a class="nav-logo" href="#">KKG.dev</a>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#experience">Experience</a>
    <a href="#portfolio">Portfolio</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<div class="wrap">

<!-- HERO -->
<section id="hero" style="padding-top:0;padding-bottom:0">
  <div class="hero-tag">// Abu Dhabi, UAE · Open to opportunities</div>
  <h1 class="hero-name">Kiran Kumar<br/><span>Gajula</span></h1>
  <div class="hero-typed">
    <span id="typed-text"></span><span class="cursor"></span>
  </div>
  <p class="hero-desc">
    Senior iOS Developer with <strong style="color:var(--text)">10+ years</strong> building production-grade apps across fintech, travel, healthcare & enterprise mobility. Expert in Swift, SwiftUI & scalable modular architecture.
  </p>
  <div class="hero-ctas">
    <a href="#portfolio" class="btn-primary">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8m-4-4v4"/></svg>
      View Portfolio
    </a>
    <a href="https://www.linkedin.com/in/kirankumarios/" target="_blank" class="btn-outline">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
      LinkedIn
    </a>
  </div>
  <div class="hero-stats">
    <div>
      <div class="stat-num">10+</div>
      <div class="stat-label">Years experience</div>
    </div>
    <div>
      <div class="stat-num">8+</div>
      <div class="stat-label">Products shipped</div>
    </div>
    <div>
      <div class="stat-num">100K+</div>
      <div class="stat-label">Early subscribers</div>
    </div>
    <div>
      <div class="stat-num">30%</div>
      <div class="stat-label">Code reduction</div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="reveal">
    <div class="section-label">// what I work with</div>
    <h2 class="section-title">Technical Stack</h2>
    <div class="section-line"></div>
  </div>
  <div class="skills-grid">
    <div class="skill-card reveal">
      <div class="skill-cat">Languages & Frameworks</div>
      <div class="skill-tags">
        <span class="tag">Swift</span><span class="tag">SwiftUI</span><span class="tag">Objective-C</span>
        <span class="tag">Combine</span><span class="tag">UIKit</span><span class="tag">Foundation</span>
        <span class="tag">AVFoundation</span><span class="tag">PDFKit</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-cat">Architecture</div>
      <div class="skill-tags">
        <span class="tag">MVVM</span><span class="tag">MVVM-C</span><span class="tag">VIPER</span>
        <span class="tag">Clean Architecture</span><span class="tag">Coordinator</span>
        <span class="tag">Modular</span><span class="tag">Dependency Injection</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-cat">Fintech & Security</div>
      <div class="skill-tags">
        <span class="tag">Apple Pay</span><span class="tag">3DS2</span><span class="tag">Tokenisation</span>
        <span class="tag">PCI-DSS</span><span class="tag">SSL Pinning</span><span class="tag">AES-256</span>
        <span class="tag">Face ID/Touch ID</span><span class="tag">Keychain</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-cat">Networking & APIs</div>
      <div class="skill-tags">
        <span class="tag">REST</span><span class="tag">GraphQL</span><span class="tag">SOAP</span>
        <span class="tag">URLSession</span><span class="tag">WebSockets</span>
        <span class="tag">Offline Caching</span><span class="tag">Background Sync</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-cat">DevOps & CI/CD</div>
      <div class="skill-tags">
        <span class="tag">Fastlane</span><span class="tag">GitHub Actions</span><span class="tag">Jenkins</span>
        <span class="tag">Bitrise</span><span class="tag">App Store Deployment</span>
        <span class="tag">TestFlight</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-cat">Testing & Monitoring</div>
      <div class="skill-tags">
        <span class="tag">XCTest</span><span class="tag">XCUITest</span><span class="tag">TDD</span>
        <span class="tag">Snapshot Testing</span><span class="tag">Firebase</span>
        <span class="tag">Sentry</span><span class="tag">Datadog</span>
      </div>
    </div>
  </div>
</section>

<!-- EXPERIENCE -->
<section id="experience">
  <div class="reveal">
    <div class="section-label">// where I've worked</div>
    <h2 class="section-title">Experience</h2>
    <div class="section-line"></div>
  </div>
  <div class="timeline">

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Comera</span>
        <span class="tl-badge">Oct 2025 – Present</span>
      </div>
      <div class="tl-role">Senior Software Engineer</div>
      <div class="tl-meta">Abu Dhabi, UAE · Mobile Banking</div>
      <ul class="tl-bullets">
        <li>Architected end-to-end <span class="highlight">mobile banking modules</span> — accounts, transfers, cards, transaction history, and statements.</li>
        <li>Engineered <span class="highlight">fraud-prevention workflows</span> with device fingerprinting, geo-behaviour analysis, and anomaly risk scoring.</li>
        <li>Built an internal <span class="highlight">feature-flag system</span> for controlled rollouts of high-risk banking features.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Backbase</span>
        <span class="tl-badge">Aug – Oct 2025</span>
      </div>
      <div class="tl-role">Senior Software Engineer</div>
      <div class="tl-meta">Hyderabad, India · White-label Digital Banking</div>
      <ul class="tl-bullets">
        <li>Delivered <span class="highlight">white-label banking solutions</span> for multiple bank partners using a shared modular codebase.</li>
        <li>Built reusable <span class="highlight">SwiftUI component libraries</span> (multi-step forms, consent screens, eligibility checks).</li>
        <li>Ensured 100% compliance with local banking regulations and audit requirements.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Single Point Solutions</span>
        <span class="tl-badge">Jan 2024 – Jul 2025</span>
      </div>
      <div class="tl-role">Senior Software Engineer</div>
      <div class="tl-meta">Hyderabad, India · E-commerce & Rewards</div>
      <ul class="tl-bullets">
        <li><span class="highlight">30% reduction in code duplication</span> via modularisation with unified Harmonised Framework.</li>
        <li><span class="highlight">20% increase in user engagement</span> through optimised reward redemption features.</li>
        <li>Automated build/release via Fastlane & GitHub Actions, reducing manual effort significantly.</li>
        <li>Mentored junior developers; conducted architecture documentation and code reviews.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Cue Health</span>
        <span class="tl-badge">Nov 2023 – Jan 2024</span>
      </div>
      <div class="tl-role">Senior Mobile Application Developer – iOS</div>
      <div class="tl-meta">Hyderabad, India · Healthcare / Medical Devices</div>
      <ul class="tl-bullets">
        <li>Migrated legacy UIKit flows to <span class="highlight">SwiftUI with MVVM-C</span>, improving testability and state management.</li>
        <li>Integrated real-time sensor data via <span class="highlight">Combine pipelines</span> with debouncing and thread-safe updates.</li>
        <li>Implemented secure, regulation-compliant health data storage.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Rehlat Online Services</span>
        <span class="tl-badge">Aug 2020 – Oct 2023</span>
      </div>
      <div class="tl-role">Team Lead – iOS</div>
      <div class="tl-meta">Hyderabad, India · Travel & Booking Platform</div>
      <ul class="tl-bullets">
        <li>Led iOS team — defined scalable architecture, standardised frameworks, mentored developers.</li>
        <li>Owned iOS platform for <span class="highlight">high-traffic booking journeys</span> with zero downtime during peak periods.</li>
        <li>Designed booking state machines for cancellations, rescheduling, add-ons, and dynamic fares.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">Conversion Bug</span>
        <span class="tl-badge">May 2017 – May 2019</span>
      </div>
      <div class="tl-role">iOS Developer</div>
      <div class="tl-meta">Hyderabad, India · Healthcare App</div>
      <ul class="tl-bullets">
        <li>Independently built a healthcare app from scratch to App Store — <span class="highlight">100,000+ subscribers</span> at launch.</li>
        <li>Integrated real-time chat (CallKit/PushKit) with VoIP calling and reconnection strategies.</li>
      </ul>
    </div>

    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-header">
        <span class="tl-company">IQM</span>
        <span class="tl-badge">Nov 2015 – Apr 2017</span>
      </div>
      <div class="tl-role">iOS Developer</div>
      <div class="tl-meta">Hyderabad, India · Enterprise Field Operations</div>
      <ul class="tl-bullets">
        <li>Built field-operations features for a US market Roofing Work Management app using UIKit + REST APIs.</li>
      </ul>
    </div>

  </div>
</section>

<!-- PORTFOLIO -->
<section id="portfolio">
  <div class="reveal">
    <div class="section-label">// shipped products</div>
    <h2 class="section-title">Portfolio</h2>
    <div class="section-line"></div>
  </div>
  <div class="apps-grid">

    <a href="#" class="app-card reveal">
      <div class="app-icon" style="background:linear-gradient(135deg,#1D4ED8,#06B6D4)">🏦</div>
      <div class="app-name">Mobile Banking App</div>
      <div class="app-desc">Full-featured banking platform with real-time fraud detection, card management, and secure payment flows.</div>
      <div class="app-tech">
        <span class="app-tag">SwiftUI</span><span class="app-tag">Combine</span>
        <span class="app-tag">MVVM-C</span><span class="app-tag">Apple Pay</span>
      </div>
    </a>

    <a href="#" class="app-card reveal">
      <div class="app-icon" style="background:linear-gradient(135deg,#7C3AED,#DB2777)">✈️</div>
      <div class="app-name">Travel Booking Platform</div>
      <div class="app-desc">High-traffic travel and booking app with advanced state machines for cancellations, loyalty, and wallet features.</div>
      <div class="app-tech">
        <span class="app-tag">Swift</span><span class="app-tag">UIKit</span>
        <span class="app-tag">VIPER</span><span class="app-tag">WebSockets</span>
      </div>
    </a>

    <a href="#" class="app-card reveal">
      <div class="app-icon" style="background:linear-gradient(135deg,#059669,#0891B2)">🏥</div>
      <div class="app-name">Healthcare App</div>
      <div class="app-desc">Built end-to-end: real-time chat, VoIP calling via CallKit, and medical device sensor integration. 100K+ users.</div>
      <div class="app-tech">
        <span class="app-tag">CallKit</span><span class="app-tag">PushKit</span>
        <span class="app-tag">Combine</span><span class="app-tag">SwiftUI</span>
      </div>
    </a>

    <a href="#" class="app-card reveal">
      <div class="app-icon" style="background:linear-gradient(135deg,#D97706,#DC2626)">🛍️</div>
      <div class="app-name">Rewards & E-commerce</div>
      <div class="app-desc">Optimised reward redemption flows resulting in 20% user engagement uplift and improved retention metrics.</div>
      <div class="app-tech">
        <span class="app-tag">Swift</span><span class="app-tag">MVVM</span>
        <span class="app-tag">Fastlane</span><span class="app-tag">Firebase</span>
      </div>
    </a>

    <a href="#" class="app-card reveal" style="border-style:dashed;opacity:0.6;cursor:default;">
      <div class="app-icon" style="background:var(--surface)">＋</div>
      <div class="app-name">Your App Here</div>
      <div class="app-desc">Add a direct App Store link to your published applications to make this section shine for recruiters.</div>
      <div class="app-tech"><span class="app-tag">App Store Link</span></div>
    </a>

    <a href="https://github.com/yourusername" target="_blank" class="app-card reveal">
      <div class="app-icon" style="background:var(--surface);font-size:1.4rem">
        <svg width="28" height="28" viewBox="0 0 24 24" fill="var(--subtle)"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
      </div>
      <div class="app-name">GitHub</div>
      <div class="app-desc">Open source contributions, side projects, and code samples. Add your GitHub URL to complete your profile.</div>
      <div class="app-tech"><span class="app-tag">github.com/yourusername</span></div>
    </a>

  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-box reveal">
    <div class="contact-title">Let's Build Something</div>
    <p class="contact-sub">Available for Senior iOS, Lead, and Architect roles across the UAE.</p>
    <div class="contact-links">
      <a href="mailto:kiranverse04@gmail.com" class="contact-link">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="M22 7l-10 7L2 7"/></svg>
        kiranverse04@gmail.com
      </a>
      <a href="tel:+971509792336" class="contact-link">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.11 19.79 19.79 0 01.0 .51 2 2 0 012 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.09 7.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 14.92"/></svg>
        +971 509 792 336
      </a>
      <a href="https://www.linkedin.com/in/kirankumarios/" target="_blank" class="contact-link">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/yourusername" target="_blank" class="contact-link">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
        GitHub
      </a>
    </div>
  </div>
</section>

<footer>
  <span style="color:var(--blue)">Kiran Kumar Gajula</span> · Senior iOS Developer · Abu Dhabi, UAE · Built with HTML/CSS/JS
</footer>

</div><!-- /wrap -->

<script>
// ── CANVAS STARFIELD ───────────────────────────────────────────────
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
let W, H, stars = [];

function initCanvas() {
  W = canvas.width  = window.innerWidth;
  H = canvas.height = window.innerHeight;
  stars = Array.from({ length: 120 }, () => ({
    x: Math.random() * W,
    y: Math.random() * H,
    r: Math.random() * 1.2 + 0.2,
    speed: Math.random() * 0.3 + 0.05,
    opacity: Math.random()
  }));
}

function drawStars() {
  ctx.clearRect(0, 0, W, H);
  for (const s of stars) {
    ctx.beginPath();
    ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(148,163,184,${s.opacity})`;
    ctx.fill();
    s.y += s.speed;
    s.opacity = 0.3 + 0.7 * Math.abs(Math.sin(Date.now() * 0.0005 + s.x));
    if (s.y > H) { s.y = 0; s.x = Math.random() * W; }
  }
  requestAnimationFrame(drawStars);
}

window.addEventListener('resize', initCanvas);
initCanvas();
drawStars();

// ── TYPING ANIMATION ──────────────────────────────────────────────
const phrases = [
  "Senior iOS Developer",
  "Lead iOS Developer",
  "iOS Architect",
  "Swift & SwiftUI Expert",
  "Fintech Mobile Specialist"
];
let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typed-text');

function type() {
  const word = phrases[pi];
  if (!deleting) {
    el.textContent = word.slice(0, ++ci);
    if (ci === word.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    el.textContent = word.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; }
  }
  setTimeout(type, deleting ? 45 : 80);
}
type();

// ── NAV SCROLL STYLE ──────────────────────────────────────────────
window.addEventListener('scroll', () => {
  document.getElementById('nav').classList.toggle('scrolled', window.scrollY > 60);
});

// ── SCROLL REVEAL ─────────────────────────────────────────────────
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); }
  });
}, { threshold: 0.12 });

document.querySelectorAll('.reveal, .tl-item').forEach(el => observer.observe(el));

// ── STAGGER SKILL CARDS ────────────────────────────────────────────
document.querySelectorAll('.skill-card.reveal').forEach((el, i) => {
  el.style.transitionDelay = `${i * 80}ms`;
});

document.querySelectorAll('.app-card.reveal').forEach((el, i) => {
  el.style.transitionDelay = `${i * 80}ms`;
});

document.querySelectorAll('.tl-item').forEach((el, i) => {
  el.style.transitionDelay = `${i * 100}ms`;
});
</script>
</body>
</html>

