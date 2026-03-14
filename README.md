
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Abrar Dar — Security Researcher & AI Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&family=IBM+Plex+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #050508;
    --bg2: #0a0a10;
    --surface: #0f0f18;
    --border: #1e1e2e;
    --neon: #00f5c4;
    --neon2: #7b2fff;
    --neon3: #ff3c6e;
    --text: #e8e8f0;
    --muted: #5a5a7a;
    --accent: #00f5c4;
    --card: #0d0d17;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  #cursor {
    width: 12px; height: 12px;
    background: var(--neon);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: screen;
  }
  #cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--neon);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease-out, width 0.2s, height 0.2s, opacity 0.2s;
    opacity: 0.5;
  }

  /* SCANLINE OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,245,196,0.015) 2px, rgba(0,245,196,0.015) 4px);
    pointer-events: none;
    z-index: 9990;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 4rem;
    background: linear-gradient(to bottom, rgba(5,5,8,0.98), transparent);
    backdrop-filter: blur(8px);
  }
  .nav-logo {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.9rem;
    color: var(--neon);
    letter-spacing: 0.08em;
    text-decoration: none;
  }
  .nav-logo span { color: var(--muted); }
  .nav-links { display: flex; gap: 2.5rem; list-style: none; }
  .nav-links a {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--neon);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--neon); }
  .nav-links a:hover::after { width: 100%; }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    padding: 8rem 4rem 4rem;
    position: relative;
    overflow: hidden;
  }
  .hero-grid-bg {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(0,245,196,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,245,196,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black, transparent);
  }
  .hero-left { z-index: 1; }
  .hero-tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.72rem;
    color: var(--neon);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    display: flex; align-items: center; gap: 0.75rem;
  }
  .hero-tag::before {
    content: '';
    width: 32px; height: 1px;
    background: var(--neon);
  }
  h1 {
    font-size: clamp(3.5rem, 6vw, 6rem);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    margin-bottom: 1.5rem;
  }
  h1 .line1 { display: block; color: var(--text); }
  h1 .line2 { display: block; color: var(--neon); }
  .hero-tagline {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.7;
    max-width: 440px;
    margin-bottom: 2.5rem;
    border-left: 2px solid var(--neon2);
    padding-left: 1rem;
  }
  .hero-ctas { display: flex; gap: 1rem; flex-wrap: wrap; }
  .btn {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    text-decoration: none;
    padding: 0.8rem 1.8rem;
    border: 1px solid;
    transition: all 0.25s;
    cursor: none;
  }
  .btn-primary {
    background: var(--neon);
    color: var(--bg);
    border-color: var(--neon);
    font-weight: 700;
  }
  .btn-primary:hover { background: transparent; color: var(--neon); }
  .btn-ghost {
    background: transparent;
    color: var(--text);
    border-color: var(--border);
  }
  .btn-ghost:hover { border-color: var(--neon); color: var(--neon); }

  /* 3D MODEL VIEWER */
  .hero-right {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    z-index: 1;
  }
  #model-container {
    width: 520px;
    height: 520px;
    position: relative;
  }
  #model-container::before {
    content: '';
    position: absolute; inset: -2px;
    border-radius: 50%;
    background: conic-gradient(from 0deg, var(--neon), var(--neon2), var(--neon3), var(--neon));
    animation: spin 8s linear infinite;
    z-index: -1;
    opacity: 0.6;
    filter: blur(2px);
  }
  #model-container::after {
    content: '';
    position: absolute; inset: 2px;
    background: var(--bg);
    border-radius: 50%;
    z-index: -1;
  }
  @keyframes spin { to { transform: rotate(360deg); } }
  #three-canvas {
    width: 100% !important;
    height: 100% !important;
    border-radius: 50%;
  }
  .model-hint {
    position: absolute;
    bottom: -2rem;
    left: 50%;
    transform: translateX(-50%);
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    white-space: nowrap;
  }

  /* SECTIONS */
  section {
    padding: 7rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }
  .section-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.7rem;
    color: var(--neon);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 0.75rem;
    display: flex; align-items: center; gap: 0.75rem;
  }
  .section-label::before { content: '//'; color: var(--neon2); }
  .section-title {
    font-size: clamp(2rem, 3.5vw, 3rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    margin-bottom: 3rem;
  }

  /* BIO SECTION */
  #about { max-width: 1200px; }
  .about-grid {
    display: grid;
    grid-template-columns: 1.2fr 0.8fr;
    gap: 5rem;
    align-items: start;
  }
  .about-bio {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.92rem;
    line-height: 1.9;
    color: #b0b0c8;
  }
  .about-bio strong { color: var(--neon); font-weight: 500; }
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .stat {
    background: var(--card);
    padding: 1.5rem;
    text-align: center;
  }
  .stat-num {
    font-family: 'Space Mono', monospace;
    font-size: 2.2rem;
    font-weight: 700;
    color: var(--neon);
    display: block;
  }
  .stat-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-top: 0.3rem;
  }

  /* PROJECTS */
  #projects { max-width: 1200px; }
  .projects-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .project-card {
    background: var(--card);
    padding: 2.5rem;
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
  }
  .project-card:hover { background: #10101e; }
  .project-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, var(--neon), transparent);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .project-card:hover::before { transform: scaleX(1); }
  .project-num {
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    margin-bottom: 1.25rem;
  }
  .project-title {
    font-size: 1.35rem;
    font-weight: 700;
    margin-bottom: 0.75rem;
    letter-spacing: -0.01em;
  }
  .project-desc {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 1.5rem;
  }
  .project-tags {
    display: flex; flex-wrap: wrap; gap: 0.5rem;
    margin-bottom: 1.5rem;
  }
  .tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    padding: 0.3rem 0.75rem;
    border: 1px solid var(--border);
    color: var(--muted);
    letter-spacing: 0.08em;
  }
  .tag.neon { border-color: var(--neon); color: var(--neon); }
  .tag.purple { border-color: var(--neon2); color: var(--neon2); }
  .tag.red { border-color: var(--neon3); color: var(--neon3); }
  .project-severity {
    display: inline-flex; align-items: center; gap: 0.4rem;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.68rem;
    color: var(--neon3);
    margin-bottom: 0.75rem;
  }
  .severity-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--neon3); animation: pulse 1.5s infinite; }
  @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.3; } }
  .project-link {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.72rem;
    color: var(--neon);
    text-decoration: none;
    letter-spacing: 0.08em;
    display: inline-flex; align-items: center; gap: 0.4rem;
  }
  .project-link::after { content: '↗'; transition: transform 0.2s; }
  .project-link:hover::after { transform: translate(2px,-2px); }
  .project-card.full-width { grid-column: span 2; }

  /* SKILLS */
  #skills { max-width: 1200px; }
  .skills-layout { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1.5px; background: var(--border); border: 1px solid var(--border); }
  .skill-group { background: var(--card); padding: 2rem; }
  .skill-group-title {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.7rem;
    color: var(--neon);
    text-transform: uppercase;
    letter-spacing: 0.2em;
    margin-bottom: 1.25rem;
    padding-bottom: 0.75rem;
    border-bottom: 1px solid var(--border);
  }
  .skill-list { list-style: none; display: flex; flex-direction: column; gap: 0.6rem; }
  .skill-list li {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: #9090b0;
    display: flex; align-items: center; gap: 0.5rem;
  }
  .skill-list li::before { content: '>'; color: var(--neon2); font-size: 0.7rem; }

  /* EDUCATION */
  #education { max-width: 1200px; }
  .timeline { position: relative; padding-left: 2rem; }
  .timeline::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom, var(--neon), var(--neon2), transparent);
  }
  .timeline-item {
    position: relative;
    padding: 2rem 2rem 2.5rem;
    background: var(--card);
    border: 1px solid var(--border);
    margin-bottom: 1.5rem;
    transition: border-color 0.3s;
  }
  .timeline-item:hover { border-color: var(--neon); }
  .timeline-item::before {
    content: '';
    position: absolute; left: -2.5rem; top: 2rem;
    width: 10px; height: 10px;
    background: var(--neon);
    border-radius: 50%;
    box-shadow: 0 0 12px var(--neon);
  }
  .edu-period {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.68rem;
    color: var(--neon2);
    letter-spacing: 0.1em;
    margin-bottom: 0.5rem;
  }
  .edu-degree {
    font-size: 1.1rem;
    font-weight: 700;
    margin-bottom: 0.3rem;
  }
  .edu-school {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.78rem;
    color: var(--muted);
    margin-bottom: 0.75rem;
  }
  .edu-note {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: #6868a0;
    line-height: 1.7;
  }

  /* CERTIFICATIONS */
  .certs-grid { display: flex; flex-wrap: wrap; gap: 0.75rem; margin-top: 2rem; }
  .cert-chip {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.72rem;
    padding: 0.6rem 1.2rem;
    border: 1px solid var(--border);
    color: var(--muted);
    letter-spacing: 0.06em;
    transition: all 0.2s;
  }
  .cert-chip:hover { border-color: var(--neon); color: var(--neon); background: rgba(0,245,196,0.04); }

  /* CONTACT */
  #contact { max-width: 1200px; text-align: center; }
  .contact-email {
    font-size: clamp(1.2rem, 2.5vw, 2rem);
    font-family: 'IBM Plex Mono', monospace;
    color: var(--text);
    text-decoration: none;
    border-bottom: 1px solid var(--neon);
    padding-bottom: 0.3rem;
    transition: color 0.2s;
  }
  .contact-email:hover { color: var(--neon); }
  .socials { display: flex; justify-content: center; gap: 1.5rem; margin-top: 3rem; flex-wrap: wrap; }
  .social-link {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 0.7rem 1.4rem;
    border: 1px solid var(--border);
    transition: all 0.25s;
    display: flex; align-items: center; gap: 0.5rem;
  }
  .social-link:hover { color: var(--neon); border-color: var(--neon); background: rgba(0,245,196,0.04); }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 2rem 4rem;
    display: flex; justify-content: space-between; align-items: center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.08em;
  }

  /* LOADING SCREEN */
  #loader {
    position: fixed; inset: 0;
    background: var(--bg);
    z-index: 9997;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 1.5rem;
    transition: opacity 0.6s, visibility 0.6s;
  }
  #loader.hidden { opacity: 0; visibility: hidden; }
  .loader-text {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 0.75rem;
    color: var(--neon);
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }
  .loader-bar {
    width: 200px; height: 1px;
    background: var(--border);
    position: relative; overflow: hidden;
  }
  .loader-fill {
    position: absolute; top: 0; left: 0; height: 100%;
    background: var(--neon);
    animation: load 1.8s ease-out forwards;
  }
  @keyframes load { from { width: 0; } to { width: 100%; } }

  /* ANIMATE IN */
  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  @media (max-width: 900px) {
    nav { padding: 1rem 1.5rem; }
    #hero { grid-template-columns: 1fr; padding: 7rem 1.5rem 3rem; gap: 3rem; }
    .hero-right { order: -1; }
    #model-container { width: 280px; height: 280px; }
    section { padding: 4rem 1.5rem; }
    .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
    .projects-grid { grid-template-columns: 1fr; }
    .project-card.full-width { grid-column: span 1; }
    .skills-layout { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 0.75rem; text-align: center; }
    .nav-links { display: none; }
  }
</style>
</head>
<body>

<div id="loader">
  <div class="loader-text">Initializing // abrar.dar</div>
  <div class="loader-bar"><div class="loader-fill"></div></div>
</div>

<div id="cursor"></div>
<div id="cursor-ring"></div>

<nav>
  <a href="#" class="nav-logo">AD<span>.sh</span></a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#projects">Research</a></li>
    <li><a href="#skills">Stack</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<div id="hero">
  <div class="hero-grid-bg"></div>
  <div class="hero-left reveal">
    <div class="hero-tag">Security Researcher & AI Engineer</div>
    <h1>
      <span class="line1">Abrar</span>
      <span class="line2">Dar</span>
    </h1>
    <p class="hero-tagline">Bridging the Gap Between Intelligent Systems and Offensive Security.</p>
    <div class="hero-ctas">
      <a href="#projects" class="btn btn-primary">View Research</a>
      <a href="#contact" class="btn btn-ghost">Get In Touch</a>
    </div>
  </div>
  <div class="hero-right reveal">
    <div id="model-container">
      <canvas id="three-canvas"></canvas>
      <div class="model-hint">drag to rotate · scroll to zoom</div>
    </div>
  </div>
</div>

<!-- ABOUT -->
<section id="about">
  <div class="section-label">Profile</div>
  <h2 class="section-title">About Me</h2>
  <div class="about-grid reveal">
    <div>
      <p class="about-bio">
        3rd-year <strong>B.Tech AIML student</strong> and independent security researcher.
        I specialize in identifying critical vulnerabilities and building <strong>privacy-first AI tools</strong>.
        <br/><br/>
        From triaging <strong>RCE bugs in GitHub Actions</strong> to engineering AI-powered CLI security tools,
        I focus on turning complex vulnerabilities into robust technical solutions. My work spans
        the intersection of <strong>machine learning systems</strong> and <strong>offensive security research</strong>.
        <br/><br/>
        Based in <strong>Mohali, India</strong> — open to remote collaboration, bug bounty programs,
        and research partnerships.
      </p>
    </div>
    <div class="stats-grid">
      <div class="stat">
        <span class="stat-num">4+</span>
        <span class="stat-label">Projects Built</span>
      </div>
      <div class="stat">
        <span class="stat-num">2</span>
        <span class="stat-label">CVEs Reported</span>
      </div>
      <div class="stat">
        <span class="stat-num">90%+</span>
        <span class="stat-label">ML Accuracy</span>
      </div>
      <div class="stat">
        <span class="stat-num">7.0</span>
        <span class="stat-label">CVSS Score</span>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects" style="padding-top:0;">
  <div class="section-label">Research & Engineering</div>
  <h2 class="section-title">Featured Work</h2>
  <div class="projects-grid reveal">

    <div class="project-card">
      <div class="project-num">01 // SECURITY RESEARCH</div>
      <div class="project-severity"><span class="severity-dot"></span> HIGH — CVSS 7.0–8.9</div>
      <h3 class="project-title">Odoo 18.0 Vulnerability</h3>
      <p class="project-desc">Discovered unauthorized access to the <code>res.users</code> model in Odoo Community Edition 18.0, exposing credential data. Demonstrated deep ORM exploitation and API-based enumeration techniques. Reported via Intigriti responsible disclosure.</p>
      <div class="project-tags">
        <span class="tag red">Intigriti</span>
        <span class="tag">ORM Exploitation</span>
        <span class="tag">API Enumeration</span>
        <span class="tag">Auth Bypass</span>
      </div>
      <a href="https://github.com/abrarxploit" class="project-link" target="_blank">Read Report</a>
    </div>

    <div class="project-card">
      <div class="project-num">02 // AI + SECURITY</div>
      <h3 class="project-title">InboxZero CLI</h3>
      <p class="project-desc">AI-powered Gmail cleanup tool using fine-tuned DistilBERT. Processes emails 100% on-device for maximum privacy, auto-deletes spam with 90%+ confidence using SHA-3 hardware hashing. Built with HuggingFace and Google OAuth 2.0.</p>
      <div class="project-tags">
        <span class="tag neon">Python 3.10+</span>
        <span class="tag neon">DistilBERT</span>
        <span class="tag">HuggingFace</span>
        <span class="tag">OAuth 2.0</span>
        <span class="tag">SHA-3</span>
      </div>
      <a href="https://github.com/abrarxploit" class="project-link" target="_blank">GitHub Repository</a>
    </div>

    <div class="project-card">
      <div class="project-num">03 // CRYPTOGRAPHY</div>
      <h3 class="project-title">Cryptomancer</h3>
      <p class="project-desc">Modern desktop encryption suite supporting AES, DES, and RSA. Features secure key pair generation (.pem files), real-time action logging, and a clean GUI built with ttkbootstrap. Fully unit tested.</p>
      <div class="project-tags">
        <span class="tag purple">Python</span>
        <span class="tag purple">AES / DES / RSA</span>
        <span class="tag">ttkbootstrap</span>
        <span class="tag">Unit Testing</span>
      </div>
      <a href="https://github.com/abrarxploit" class="project-link" target="_blank">GitHub Repository</a>
    </div>

    <div class="project-card">
      <div class="project-num">04 // CVE RESEARCH</div>
      <div class="project-severity"><span class="severity-dot"></span> RCE — CWE-20/94</div>
      <h3 class="project-title">GitHub Actions RCE</h3>
      <p class="project-desc">Identified Command Injection vulnerability (CWE-20/94) in <code>anchore/grype</code> GitHub Action. Documented a valid technical path for arbitrary command execution on GitHub-hosted runners via unsafe input validation in CI/CD pipelines. Reported via HackerOne.</p>
      <div class="project-tags">
        <span class="tag red">HackerOne</span>
        <span class="tag red">RCE</span>
        <span class="tag">CI/CD Security</span>
        <span class="tag">CWE-20</span>
      </div>
      <a href="https://github.com/abrarxploit" class="project-link" target="_blank">Research Documentation</a>
    </div>

  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-label">Technical Stack</div>
  <h2 class="section-title">Skills & Tools</h2>
  <div class="skills-layout reveal">
    <div class="skill-group">
      <div class="skill-group-title">Languages</div>
      <ul class="skill-list">
        <li>Python (Primary)</li>
        <li>Java (Basics)</li>
        <li>C (Basics)</li>
        <li>HTML / CSS</li>
      </ul>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Cybersecurity</div>
      <ul class="skill-list">
        <li>Bug Bounty Hunting</li>
        <li>Web App Penetration Testing</li>
        <li>Vulnerability Assessment</li>
        <li>Responsible Disclosure</li>
        <li>API Security Testing</li>
        <li>OWASP Top 10</li>
        <li>Kali Linux / Metasploit</li>
        <li>Nmap / SQLMap / Wireshark</li>
      </ul>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">AI / ML</div>
      <ul class="skill-list">
        <li>HuggingFace Transformers</li>
        <li>DistilBERT / BERT</li>
        <li>Google OAuth 2.0</li>
        <li>Gmail API</li>
        <li>MongoDB (Basics)</li>
        <li>Google Cloud (Basics)</li>
      </ul>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Tools & Platforms</div>
      <ul class="skill-list">
        <li>Git / GitHub</li>
        <li>Linux (Kali, Ubuntu)</li>
        <li>VS Code / Postman</li>
        <li>Cloudflare Tunnel</li>
        <li>ttkbootstrap</li>
      </ul>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Platforms</div>
      <ul class="skill-list">
        <li>Intigriti</li>
        <li>HackerOne</li>
        <li>HackerRank</li>
        <li>GitHub Actions</li>
      </ul>
    </div>
    <div class="skill-group">
      <div class="skill-group-title">Soft Skills</div>
      <ul class="skill-list">
        <li>Technical Writing</li>
        <li>Problem Solving</li>
        <li>Leadership</li>
        <li>Teamwork</li>
        <li>Adaptability</li>
        <li>Time Management</li>
      </ul>
    </div>
  </div>
</section>

<!-- EDUCATION -->
<section id="education">
  <div class="section-label">Academic Journey</div>
  <h2 class="section-title">Education & Certifications</h2>
  <div class="timeline reveal">
    <div class="timeline-item">
      <div class="edu-period">2024 — 2027 · Ongoing</div>
      <div class="edu-degree">B.Tech — Artificial Intelligence & Machine Learning</div>
      <div class="edu-school">Chandigarh Engineering College (CGC), Jhanjeri, Mohali</div>
      <div class="edu-note">Focus: Neural Networks, Deep Learning, and AI-driven Security Protocols.</div>
    </div>
    <div class="timeline-item">
      <div class="edu-period">2021 — 2024 · Completed</div>
      <div class="edu-degree">Diploma in Civil Engineering · CGPA 6.8</div>
      <div class="edu-school">Kashmir Government Polytechnic (KGP), Srinagar</div>
      <div class="edu-note">Foundational logic and mathematical modeling for complex systems.</div>
    </div>
    <div class="timeline-item">
      <div class="edu-period">2020 · Completed</div>
      <div class="edu-degree">Secondary School (10th) · 94.6%</div>
      <div class="edu-school">Fayaz Educational Institute, Srinagar</div>
      <div class="edu-note">Distinction in Core Sciences.</div>
    </div>
    <div class="timeline-item">
      <div class="edu-period">05/2025 — 07/2025 · Internship</div>
      <div class="edu-degree">Summer Training — CompTIA Security+</div>
      <div class="edu-school">Professional Certification Program, Mohali</div>
      <div class="edu-note">Specialized in threat analysis, penetration testing methodologies, ethical hacking, and network security under expert supervision.</div>
    </div>
  </div>

  <div style="margin-top:3rem;">
    <div class="section-label" style="margin-bottom:0.5rem;">Certifications</div>
    <div class="certs-grid reveal">
      <div class="cert-chip">CompTIA Security+</div>
      <div class="cert-chip">Vue.js Certificate</div>
      <div class="cert-chip">HTML & CSS Certificate</div>
      <div class="cert-chip">HackerRank Certification</div>
      <div class="cert-chip">Introduction to Cybersecurity</div>
      <div class="cert-chip">Course Completion Certificate</div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-label">Get In Touch</div>
  <h2 class="section-title" style="margin-bottom:1.5rem;">Let's Work Together</h2>
  <p style="font-family:'IBM Plex Mono',monospace;font-size:0.85rem;color:var(--muted);margin-bottom:2.5rem;max-width:500px;margin-left:auto;margin-right:auto;line-height:1.8;">Open to security research collaborations, bug bounty partnerships, AI/ML projects, and freelance opportunities.</p>
  <a href="mailto:abrardar.00003085389@gmail.com" class="contact-email">abrardar.00003085389@gmail.com</a>
  <div class="socials">
    <a href="https://github.com/abrarxploit" target="_blank" class="social-link">⌥ GitHub</a>
    <a href="https://linkedin.com/in/abrardar" target="_blank" class="social-link">⌥ LinkedIn</a>
    <a href="https://x.com/Abrar52406739" target="_blank" class="social-link">⌥ X / Twitter</a>
    <a href="https://www.instagram.com/abrardar02" target="_blank" class="social-link">⌥ Instagram</a>
    <a href="https://www.facebook.com/share/1KfaUJQX95/" target="_blank" class="social-link">⌥ Facebook</a>
  </div>
</section>

<footer>
  <span>© 2025 Abrar Dar — All rights reserved.</span>
  <span>abrarxploit · Security Researcher · AIML Engineer</span>
</footer>

<!-- THREE.JS + GLTFLoader -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
// ── GLTFLoader inline (r128 compatible) ──────────────────────────────────────
THREE.GLTFLoader = (function () {
  function GLTFLoader(manager) {
    THREE.Loader.call(this, manager);
    this.dracoLoader = null;
    this.ktx2Loader = null;
    this.meshoptDecoder = null;
    this.pluginCallbacks = [];
    this.register(function (parser) { return new GLTFMaterialsClearcoatExtension(parser); });
    this.register(function (parser) { return new GLTFTextureBasisUExtension(parser); });
    this.register(function (parser) { return new GLTFTextureWebPExtension(parser); });
    this.register(function (parser) { return new GLTFMaterialsSheenExtension(parser); });
    this.register(function (parser) { return new GLTFMaterialsTransmissionExtension(parser); });
    this.register(function (parser) { return new GLTFMaterialsVolumeExtension(parser); });
    this.register(function (parser) { return new GLTFMaterialsIorExtension(parser); });
    this.register(function (parser) { return new GLTFMaterialsSpecularExtension(parser); });
    this.register(function (parser) { return new GLTFLightsExtension(parser); });
    this.register(function (parser) { return new GLTFMeshoptCompression(parser); });
  }
  GLTFLoader.prototype = Object.assign(Object.create(THREE.Loader.prototype), {
    constructor: GLTFLoader,
    load: function (url, onLoad, onProgress, onError) {
      var scope = this;
      var resourcePath;
      if (this.resourcePath !== '') { resourcePath = this.resourcePath; }
      else if (this.path !== '') { resourcePath = this.path; }
      else { resourcePath = THREE.LoaderUtils.extractUrlBase(url); }
      this.manager.itemStart(url);
      var _onError = function (e) {
        if (onError) { onError(e); } else { console.error(e); }
        scope.manager.itemError(url);
        scope.manager.itemEnd(url);
      };
      var loader = new THREE.FileLoader(this.manager);
      loader.setPath(this.path);
      loader.setResponseType('arraybuffer');
      loader.setRequestHeader(this.requestHeader);
      loader.setWithCredentials(this.withCredentials);
      loader.load(url, function (data) {
        try { scope.parse(data, resourcePath, function (gltf) { onLoad(gltf); scope.manager.itemEnd(url); }, _onError); }
        catch (e) { _onError(e); }
      }, onProgress, _onError);
    },
    setDRACOLoader: function (dracoLoader) { this.dracoLoader = dracoLoader; return this; },
    setKTX2Loader: function (ktx2Loader) { this.ktx2Loader = ktx2Loader; return this; },
    setMeshoptDecoder: function (meshoptDecoder) { this.meshoptDecoder = meshoptDecoder; return this; },
    register: function (callback) { if (this.pluginCallbacks.indexOf(callback) === -1) { this.pluginCallbacks.push(callback); } return this; },
    unregister: function (callback) { if (this.pluginCallbacks.indexOf(callback) !== -1) { this.pluginCallbacks.splice(this.pluginCallbacks.indexOf(callback), 1); } return this; },
    parse: function (data, path, onLoad, onError) {
      var content;
      var extensions = {};
      var plugins = {};
      if (typeof data === 'string') { content = data; }
      else {
        var magic = THREE.LoaderUtils.decodeText(new Uint8Array(data, 0, 4));
        if (magic === BINARY_EXTENSION_HEADER_MAGIC) {
          try { extensions[EXTENSIONS.KHR_BINARY_GLTF] = new GLTFBinaryExtension(data); }
          catch (error) { if (onError) onError(error); return; }
          content = extensions[EXTENSIONS.KHR_BINARY_GLTF].content;
        } else { content = THREE.LoaderUtils.decodeText(new Uint8Array(data)); }
      }
      var json;
      try { json = JSON.parse(content); } catch (error) { if (onError) onError(error); return; }
      if (json.asset === undefined || json.asset.version[0] < 2) { if (onError) onError(new Error('THREE.GLTFLoader: Unsupported asset.')); return; }
      var parser = new GLTFParser(json, { path: path || this.resourcePath || '', crossOrigin: this.crossOrigin, requestHeader: this.requestHeader, manager: this.manager, ktx2Loader: this.ktx2Loader, meshoptDecoder: this.meshoptDecoder });
      parser.fileLoader.setRequestHeader(this.requestHeader);
      for (var i = 0; i < this.pluginCallbacks.length; i++) { var plugin = this.pluginCallbacks[i](parser); plugins[plugin.name] = plugin; if (plugin.beforeRoot) { plugin.beforeRoot(); } }
      Object.assign(extensions, (json.extensions||{}));
      if (extensions[EXTENSIONS.KHR_DRACO_MESH_COMPRESSION]) { parser.setExtensions({ KHR_draco_mesh_compression: this.dracoLoader }); }
      parser.setPlugins(plugins);
      parser.parse(onLoad, onError);
    },
    parseAsync: function (data, path) {
      var scope = this;
      return new Promise(function (resolve, reject) { scope.parse(data, path, resolve, reject); });
    }
  });

  // Minimal stubs so the parser doesn't crash on missing extensions
  var EXTENSIONS = { KHR_BINARY_GLTF: 'KHR_binary_glTF', KHR_DRACO_MESH_COMPRESSION: 'KHR_draco_mesh_compression', KHR_LIGHTS_PUNCTUAL: 'KHR_lights_punctual', KHR_MATERIALS_CLEARCOAT: 'KHR_materials_clearcoat', KHR_MATERIALS_IOR: 'KHR_materials_ior', KHR_MATERIALS_PBR_SPECULAR_GLOSSINESS: 'KHR_materials_pbrSpecularGlossiness', KHR_MATERIALS_SHEEN: 'KHR_materials_sheen', KHR_MATERIALS_SPECULAR: 'KHR_materials_specular', KHR_MATERIALS_TRANSMISSION: 'KHR_materials_transmission', KHR_MATERIALS_UNLIT: 'KHR_materials_unlit', KHR_MATERIALS_VOLUME: 'KHR_materials_volume', KHR_TEXTURE_BASISU: 'KHR_texture_basisu', KHR_TEXTURE_TRANSFORM: 'KHR_texture_transform', KHR_MESH_QUANTIZATION: 'KHR_mesh_quantization', EXT_TEXTURE_WEBP: 'EXT_texture_webp', EXT_MESHOPT_COMPRESSION: 'EXT_meshopt_compression' };
  var BINARY_EXTENSION_HEADER_MAGIC = 'glTF';
  var BINARY_EXTENSION_HEADER_LENGTH = 12;
  var BINARY_EXTENSION_CHUNK_TYPES = { JSON: 0x4E4F534A, BIN: 0x004E4942 };

  function GLTFBinaryExtension(data) {
    this.name = EXTENSIONS.KHR_BINARY_GLTF;
    this.content = null;
    this.body = null;
    var headerView = new DataView(data, 0, BINARY_EXTENSION_HEADER_LENGTH);
    this.header = { magic: THREE.LoaderUtils.decodeText(new Uint8Array(data.slice(0, 4))), version: headerView.getUint32(4, true), length: headerView.getUint32(8, true) };
    if (this.header.magic !== BINARY_EXTENSION_HEADER_MAGIC) { throw new Error('THREE.GLTFLoader: Unexpected magic bytes.'); }
    if (this.header.version < 2.0) { throw new Error('THREE.GLTFLoader: Legacy binary file detected.'); }
    var chunkContentsLength = this.header.length - BINARY_EXTENSION_HEADER_LENGTH;
    var chunkView = new DataView(data, BINARY_EXTENSION_HEADER_LENGTH);
    var chunkIndex = 0;
    while (chunkIndex < chunkContentsLength) {
      var chunkLength = chunkView.getUint32(chunkIndex, true); chunkIndex += 4;
      var chunkType = chunkView.getUint32(chunkIndex, true); chunkIndex += 4;
      if (chunkType === BINARY_EXTENSION_CHUNK_TYPES.JSON) { var contentArray = new Uint8Array(data, BINARY_EXTENSION_HEADER_LENGTH + chunkIndex, chunkLength); this.content = THREE.LoaderUtils.decodeText(contentArray); }
      else if (chunkType === BINARY_EXTENSION_CHUNK_TYPES.BIN) { var byteOffset = BINARY_EXTENSION_HEADER_LENGTH + chunkIndex; this.body = data.slice(byteOffset, byteOffset + chunkLength); }
      chunkIndex += chunkLength;
    }
    if (this.content === null) { throw new Error('THREE.GLTFLoader: JSON content not found.'); }
  }

  // Minimal extension stubs
  function stub(name) { return function(p){ this.name=name; this.parser=p; }; }
  var GLTFMaterialsClearcoatExtension = stub(EXTENSIONS.KHR_MATERIALS_CLEARCOAT);
  var GLTFTextureBasisUExtension = stub(EXTENSIONS.KHR_TEXTURE_BASISU);
  var GLTFTextureWebPExtension = stub(EXTENSIONS.EXT_TEXTURE_WEBP);
  var GLTFMaterialsSheenExtension = stub(EXTENSIONS.KHR_MATERIALS_SHEEN);
  var GLTFMaterialsTransmissionExtension = stub(EXTENSIONS.KHR_MATERIALS_TRANSMISSION);
  var GLTFMaterialsVolumeExtension = stub(EXTENSIONS.KHR_MATERIALS_VOLUME);
  var GLTFMaterialsIorExtension = stub(EXTENSIONS.KHR_MATERIALS_IOR);
  var GLTFMaterialsSpecularExtension = stub(EXTENSIONS.KHR_MATERIALS_SPECULAR);
  var GLTFLightsExtension = stub(EXTENSIONS.KHR_LIGHTS_PUNCTUAL);
  var GLTFMeshoptCompression = stub(EXTENSIONS.EXT_MESHOPT_COMPRESSION);

  // ── GLTFParser (minimal but functional for most GLBs) ──
  function GLTFParser(json, options) {
    this.json = json || {};
    this.extensions = {};
    this.plugins = {};
    this.options = options;
    this.cache = new GLTFRegistry();
    this.associations = new Map();
    this.primitiveCache = {};
    this.meshCache = { refs: {}, uses: {} };
    this.cameraCache = { refs: {}, uses: {} };
    this.lightCache = { refs: {}, uses: {} };
    this.textureCache = {};
    this.nodeNamesUsed = {};
    var isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent) === true;
    var isFirefox = navigator.userAgent.indexOf('Firefox') > -1;
    var firefoxVersion = isFirefox ? navigator.userAgent.match(/Firefox\/([0-9]+)\./)[1] : -1;
    if (typeof createImageBitmap === 'undefined' || isSafari || (isFirefox && firefoxVersion < 98)) { this.textureLoader = new THREE.TextureLoader(this.options.manager); }
    else { this.textureLoader = new THREE.ImageBitmapLoader(this.options.manager); }
    this.textureLoader.setCrossOrigin(this.options.crossOrigin);
    this.textureLoader.setRequestHeader(this.options.requestHeader);
    this.fileLoader = new THREE.FileLoader(this.options.manager);
    this.fileLoader.setResponseType('arraybuffer');
    this.fileLoader.setRequestHeader(this.options.requestHeader);
  }
  GLTFParser.prototype = {
    constructor: GLTFParser,
    setExtensions: function(e){ Object.assign(this.extensions, e); },
    setPlugins: function(p){ this.plugins = p; },
    parse: function(onLoad, onError) {
      var parser = this;
      var json = this.json;
      this.associations = new Map();
      // Scenes
      Promise.all([this.getDependencies('scene'), this.getDependencies('animation'), this.getDependencies('camera')]).then(function(d){
        var result = { scene: d[0][json.scene || 0], scenes: d[0], animations: d[1], cameras: d[2], asset: json.asset, parser: parser, userData: {} };
        onLoad(result);
      }).catch(onError);
    },
    getDependencies: function(type){
      var parser = this;
      var defs = this.json[type + (type==='mesh'?'es':type==='scenery'?'s':type==='animation'?'s':type==='camera'?'s':'s')] || [];
      // map type
      var fn = 'load' + type.charAt(0).toUpperCase() + type.slice(1);
      return Promise.all(defs.map(function(_,i){ return parser[fn] ? parser[fn](i) : Promise.resolve(null); }));
    },
    getDependency: function(type, index){
      var fn = 'load' + type.charAt(0).toUpperCase() + type.slice(1);
      return this[fn] ? this[fn](index) : Promise.resolve(null);
    },
    loadScene: function(sceneIndex){
      var json = this.json;
      var parser = this;
      var sceneDef = json.scenes[sceneIndex];
      var scene = new THREE.Group();
      scene.name = parser.createUniqueName(sceneDef.name||('Scene_'+sceneIndex));
      return Promise.all((sceneDef.nodes||[]).map(function(nodeIndex){ return parser.loadNode(nodeIndex); })).then(function(nodes){
        nodes.forEach(function(n){ if(n) scene.add(n); });
        return scene;
      });
    },
    loadNode: function(nodeIndex){
      var json = this.json;
      var parser = this;
      var nodeDef = json.nodes[nodeIndex];
      var pending = [];
      if(nodeDef.mesh!==undefined){ pending.push(parser.loadMesh(nodeDef.mesh)); }
      else { pending.push(Promise.resolve(null)); }
      return Promise.all(pending).then(function(objs){
        var node;
        if(objs[0]){ node = objs[0].clone ? objs[0] : new THREE.Group(); if(objs[0] && objs[0] !== node) node.add(objs[0]); }
        else { node = new THREE.Group(); }
        if(nodeDef.name){ node.name = parser.createUniqueName(nodeDef.name); }
        if(nodeDef.matrix){ var m = new THREE.Matrix4(); m.fromArray(nodeDef.matrix); node.applyMatrix4(m); }
        else {
          if(nodeDef.translation){ node.position.fromArray(nodeDef.translation); }
          if(nodeDef.rotation){ node.quaternion.fromArray(nodeDef.rotation); }
          if(nodeDef.scale){ node.scale.fromArray(nodeDef.scale); }
        }
        if(nodeDef.children){
          return Promise.all(nodeDef.children.map(function(c){ return parser.loadNode(c); })).then(function(children){
            children.forEach(function(c){ if(c) node.add(c); });
            return node;
          });
        }
        return node;
      });
    },
    loadMesh: function(meshIndex){
      var json = this.json;
      var parser = this;
      var meshDef = json.meshes[meshIndex];
      var group = new THREE.Group();
      group.name = parser.createUniqueName(meshDef.name||('Mesh_'+meshIndex));
      return Promise.all(meshDef.primitives.map(function(primDef){
        return parser.loadGeometry(primDef).then(function(geo){
          return parser.loadMaterial(primDef.material).then(function(mat){
            var mesh;
            if(primDef.mode===1||primDef.mode===0){ mesh = new THREE.LineSegments(geo, mat||new THREE.LineBasicMaterial()); }
            else { mesh = new THREE.Mesh(geo, mat||new THREE.MeshStandardMaterial()); }
            return mesh;
          });
        });
      })).then(function(meshes){
        if(meshes.length===1){ return meshes[0]; }
        meshes.forEach(function(m){ group.add(m); });
        return group;
      });
    },
    loadGeometry: function(primDef){
      var parser = this;
      var geo = new THREE.BufferGeometry();
      var pending = [];
      var attributes = primDef.attributes||{};
      Object.keys(attributes).forEach(function(semantic){
        pending.push(parser.loadAccessor(attributes[semantic]).then(function(accessor){
          var name = semantic==='POSITION'?'position':semantic==='NORMAL'?'normal':semantic==='TEXCOORD_0'?'uv':semantic.toLowerCase();
          geo.setAttribute(name, accessor);
        }));
      });
      if(primDef.indices!==undefined){ pending.push(parser.loadAccessor(primDef.indices).then(function(acc){ geo.setIndex(acc); })); }
      return Promise.all(pending).then(function(){ return geo; });
    },
    loadAccessor: function(accessorIndex){
      var json = this.json;
      var parser = this;
      var accessorDef = json.accessors[accessorIndex];
      var TYPE_SIZES = {SCALAR:1,VEC2:2,VEC3:3,VEC4:4,MAT2:4,MAT3:9,MAT4:16};
      var WEBGL_COMPONENT_TYPES = {5120:Int8Array,5121:Uint8Array,5122:Int16Array,5123:Uint16Array,5125:Uint32Array,5126:Float32Array};
      return parser.loadBufferView(accessorDef.bufferView||0).then(function(bufView){
        var TypeArr = WEBGL_COMPONENT_TYPES[accessorDef.componentType]||Float32Array;
        var size = TYPE_SIZES[accessorDef.type]||1;
        var byteOffset = accessorDef.byteOffset||0;
        var count = accessorDef.count;
        var array = new TypeArr(bufView, byteOffset, count*size);
        var attr = new THREE.BufferAttribute(array, size);
        return attr;
      });
    },
    loadBufferView: function(bufferViewIndex){
      var json = this.json;
      var parser = this;
      var bvDef = json.bufferViews[bufferViewIndex];
      return parser.loadBuffer(bvDef.buffer).then(function(buf){
        var byteOffset = bvDef.byteOffset||0;
        return buf.slice(byteOffset, byteOffset+(bvDef.byteLength||0));
      });
    },
    loadBuffer: function(bufferIndex){
      var json = this.json;
      var options = this.options;
      var bufDef = json.buffers[bufferIndex];
      if(bufDef.uri){
        if(/^data:/.test(bufDef.uri)){
          var base64 = bufDef.uri.split(',')[1];
          var binaryStr = atob(base64);
          var bytes = new Uint8Array(binaryStr.length);
          for(var i=0;i<binaryStr.length;i++) bytes[i]=binaryStr.charCodeAt(i);
          return Promise.resolve(bytes.buffer);
        }
        return new Promise(function(res,rej){
          var fl = new THREE.FileLoader();
          fl.setResponseType('arraybuffer');
          fl.load(THREE.LoaderUtils.resolveURL(bufDef.uri, options.path), res, undefined, rej);
        });
      }
      // GLB body
      if(this.extensions[EXTENSIONS.KHR_BINARY_GLTF]){
        return Promise.resolve(this.extensions[EXTENSIONS.KHR_BINARY_GLTF].body);
      }
      return Promise.reject(new Error('THREE.GLTFLoader: No buffer data.'));
    },
    loadMaterial: function(materialIndex){
      if(materialIndex===undefined) return Promise.resolve(new THREE.MeshStandardMaterial());
      var json = this.json;
      var matDef = json.materials[materialIndex];
      var params = {};
      if(matDef.pbrMetallicRoughness){
        var pbr = matDef.pbrMetallicRoughness;
        if(pbr.baseColorFactor){ params.color = new THREE.Color().fromArray(pbr.baseColorFactor); }
        if(pbr.metallicFactor!==undefined) params.metalness = pbr.metallicFactor;
        if(pbr.roughnessFactor!==undefined) params.roughness = pbr.roughnessFactor;
      }
      if(matDef.doubleSided) params.side = THREE.DoubleSide;
      return Promise.resolve(new THREE.MeshStandardMaterial(params));
    },
    loadAnimation: function(){ return Promise.resolve(null); },
    loadCamera: function(){ return Promise.resolve(null); },
    createUniqueName: function(name){
      var sanitized = name ? THREE.PropertyBinding.sanitizeNodeName(name) : '';
      if(!(sanitized in this.nodeNamesUsed)){ this.nodeNamesUsed[sanitized]=0; }
      else { this.nodeNamesUsed[sanitized]++; sanitized += '_'+this.nodeNamesUsed[sanitized]; }
      return sanitized;
    }
  };
  // Attach EXTENSIONS ref so loadBuffer can access it
  GLTFParser.prototype._EXTENSIONS = EXTENSIONS;

  function GLTFRegistry(){ this.objects={}; }
  GLTFRegistry.prototype = {
    constructor: GLTFRegistry,
    get: function(k){ return this.objects[k]; },
    add: function(k,v){ this.objects[k]=v; },
    remove: function(k){ delete this.objects[k]; },
    removeAll: function(){ this.objects={}; }
  };

  return GLTFLoader;
}());
</script>

<script>
// ── 3D MODEL VIEWER ─────────────────────────────────────────────────────────
(function () {
  var canvas = document.getElementById('three-canvas');
  var container = document.getElementById('model-container');
  var w = container.clientWidth, h = container.clientHeight;

  var renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });
  renderer.setSize(w, h);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  renderer.outputEncoding = THREE.sRGBEncoding;
  renderer.toneMapping = THREE.ACESFilmicToneMapping;
  renderer.toneMappingExposure = 1.2;

  var scene = new THREE.Scene();
  var camera = new THREE.PerspectiveCamera(45, w / h, 0.01, 1000);
  camera.position.set(0, 0, 4);

  // Lights
  var ambient = new THREE.AmbientLight(0xffffff, 0.3);
  scene.add(ambient);
  var neonLight = new THREE.PointLight(0x00f5c4, 3, 10);
  neonLight.position.set(2, 2, 2);
  scene.add(neonLight);
  var purpleLight = new THREE.PointLight(0x7b2fff, 2, 10);
  purpleLight.position.set(-2, -1, 2);
  scene.add(purpleLight);
  var rimLight = new THREE.DirectionalLight(0xffffff, 0.5);
  rimLight.position.set(0, 1, -2);
  scene.add(rimLight);

  // Orbit controls (manual)
  var isDragging = false, prevMouse = { x: 0, y: 0 };
  var spherical = { theta: 0, phi: Math.PI / 2 };
  var autoRotate = true;
  var modelGroup = new THREE.Group();
  scene.add(modelGroup);

  canvas.addEventListener('mousedown', function (e) { isDragging = true; autoRotate = false; prevMouse = { x: e.clientX, y: e.clientY }; });
  window.addEventListener('mouseup', function () { isDragging = false; });
  window.addEventListener('mousemove', function (e) {
    if (!isDragging) return;
    var dx = e.clientX - prevMouse.x, dy = e.clientY - prevMouse.y;
    spherical.theta -= dx * 0.01;
    spherical.phi = Math.max(0.1, Math.min(Math.PI - 0.1, spherical.phi - dy * 0.01));
    prevMouse = { x: e.clientX, y: e.clientY };
  });
  canvas.addEventListener('wheel', function (e) {
    camera.position.z = Math.max(1, Math.min(8, camera.position.z + e.deltaY * 0.005));
  });

  // Touch support
  canvas.addEventListener('touchstart', function(e){ if(e.touches.length===1){ isDragging=true; autoRotate=false; prevMouse={x:e.touches[0].clientX,y:e.touches[0].clientY}; } });
  window.addEventListener('touchend', function(){ isDragging=false; });
  window.addEventListener('touchmove', function(e){ if(!isDragging||e.touches.length!==1) return; var dx=e.touches[0].clientX-prevMouse.x,dy=e.touches[0].clientY-prevMouse.y; spherical.theta-=dx*0.01; spherical.phi=Math.max(0.1,Math.min(Math.PI-0.1,spherical.phi-dy*0.01)); prevMouse={x:e.touches[0].clientX,y:e.touches[0].clientY}; });

  // Load GLB
  var loader = new THREE.GLTFLoader();
  loader.load(
    '/mnt/user-data/uploads/model.glb',
    function (gltf) {
      var model = gltf.scene;
      // Center and scale
      var box = new THREE.Box3().setFromObject(model);
      var center = box.getCenter(new THREE.Vector3());
      var size = box.getSize(new THREE.Vector3());
      var maxDim = Math.max(size.x, size.y, size.z);
      var scale = 2.4 / maxDim;
      model.scale.setScalar(scale);
      model.position.sub(center.multiplyScalar(scale));
      // Apply neon material tint
      model.traverse(function (child) {
        if (child.isMesh) {
          child.material.envMapIntensity = 1;
          child.castShadow = true;
        }
      });
      modelGroup.add(model);
    },
    undefined,
    function (err) {
      console.warn('GLB load error, showing fallback:', err);
      // Fallback: stylized icosahedron
      var geo = new THREE.IcosahedronGeometry(1.2, 1);
      var mat = new THREE.MeshStandardMaterial({ color: 0x00f5c4, metalness: 0.8, roughness: 0.2, wireframe: false });
      var mesh = new THREE.Mesh(geo, mat);
      var wGeo = new THREE.IcosahedronGeometry(1.25, 1);
      var wMat = new THREE.MeshBasicMaterial({ color: 0x7b2fff, wireframe: true, opacity: 0.3, transparent: true });
      var wire = new THREE.Mesh(wGeo, wMat);
      modelGroup.add(mesh);
      modelGroup.add(wire);
    }
  );

  var clock = new THREE.Clock();
  function animate() {
    requestAnimationFrame(animate);
    var t = clock.getElapsedTime();
    if (autoRotate) { spherical.theta += 0.005; }
    // Spherical to cartesian for model rotation
    modelGroup.rotation.y = spherical.theta;
    modelGroup.rotation.x = spherical.phi - Math.PI / 2;
    // Floating bob
    modelGroup.position.y = Math.sin(t * 0.8) * 0.06;
    // Animate lights
    neonLight.intensity = 2.5 + Math.sin(t * 1.5) * 0.5;
    renderer.render(scene, camera);
  }
  animate();

  window.addEventListener('resize', function () {
    w = container.clientWidth; h = container.clientHeight;
    camera.aspect = w / h;
    camera.updateProjectionMatrix();
    renderer.setSize(w, h);
  });
})();

// ── CURSOR ──────────────────────────────────────────────────────────────────
var cursor = document.getElementById('cursor');
var ring = document.getElementById('cursor-ring');
var mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', function (e) { mx = e.clientX; my = e.clientY; cursor.style.left = mx + 'px'; cursor.style.top = my + 'px'; });
(function lerp() { rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12; ring.style.left = rx + 'px'; ring.style.top = ry + 'px'; requestAnimationFrame(lerp); })();

// ── LOADER HIDE ──────────────────────────────────────────────────────────────
setTimeout(function () { document.getElementById('loader').classList.add('hidden'); }, 2000);

// ── REVEAL ON SCROLL ─────────────────────────────────────────────────────────
var reveals = document.querySelectorAll('.reveal');
reveals.forEach(function(el, i){ el.style.transitionDelay = (i % 3) * 0.1 + 's'; });
var observer = new IntersectionObserver(function (entries) {
  entries.forEach(function (e) { if (e.isIntersecting) { e.target.classList.add('visible'); } });
}, { threshold: 0.1 });
reveals.forEach(function (el) { observer.observe(el); });
// Trigger hero immediately
setTimeout(function(){ reveals.forEach(function(el){ if(el.getBoundingClientRect().top < window.innerHeight) el.classList.add('visible'); }); }, 100);
</script>
</body>
</html>
