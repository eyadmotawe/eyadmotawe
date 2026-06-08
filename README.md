<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Eyad Motawea — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Mono:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #080B10;
    --bg2: #0D1117;
    --bg3: #111820;
    --surface: #141C26;
    --border: rgba(99,160,255,0.12);
    --border2: rgba(99,160,255,0.22);
    --accent: #4A9EFF;
    --accent2: #00E5C3;
    --accent3: #FF6B6B;
    --text: #E8EDF5;
    --muted: #6B7B91;
    --muted2: #8FA3BF;
    --glow: rgba(74,158,255,0.18);
    --glow2: rgba(0,229,195,0.12);
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

  /* Custom cursor */
  #cursor {
    position: fixed; width: 10px; height: 10px;
    background: var(--accent); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: screen;
  }
  #cursor-ring {
    position: fixed; width: 36px; height: 36px;
    border: 1px solid rgba(74,158,255,0.5);
    border-radius: 50%; pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.08s linear, width 0.2s, height 0.2s, border-color 0.2s;
  }
  body:has(a:hover) #cursor, body:has(button:hover) #cursor { width: 18px; height: 18px; background: var(--accent2); }
  body:has(a:hover) #cursor-ring, body:has(button:hover) #cursor-ring { width: 54px; height: 54px; border-color: var(--accent2); }

  /* Grid overlay */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(74,158,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(74,158,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
  }

  /* Noise texture overlay */
  body::after {
    content: '';
    position: fixed; inset: 0; z-index: 0;
    opacity: 0.025;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    pointer-events: none;
  }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 3rem;
    background: rgba(8,11,16,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    animation: slideDown 0.6s ease both;
  }
  @keyframes slideDown { from { transform: translateY(-100%); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
  .logo {
    font-size: 1.1rem; font-weight: 700; letter-spacing: 0.05em;
    color: var(--accent); text-decoration: none;
  }
  .logo span { color: var(--text); }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    color: var(--muted2); text-decoration: none; font-size: 0.85rem;
    font-weight: 500; letter-spacing: 0.08em; text-transform: uppercase;
    transition: color 0.2s; position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px; background: var(--accent);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { width: 100%; }

  /* ─── SECTIONS ─── */
  section { position: relative; z-index: 1; }

  /* ─── HERO ─── */
  #hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: flex-start;
    padding: 8rem 3rem 4rem;
    overflow: hidden;
  }

  .hero-glow {
    position: absolute; width: 600px; height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(74,158,255,0.12) 0%, transparent 70%);
    top: -100px; right: -100px; pointer-events: none;
    animation: pulse 6s ease-in-out infinite;
  }
  .hero-glow2 {
    position: absolute; width: 400px; height: 400px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,229,195,0.08) 0%, transparent 70%);
    bottom: 0; left: 30%; pointer-events: none;
    animation: pulse 8s ease-in-out infinite reverse;
  }
  @keyframes pulse { 0%,100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.15); opacity: 0.7; } }

  .hero-tag {
    display: inline-flex; align-items: center; gap: 8px;
    font-family: 'DM Mono', monospace; font-size: 0.78rem;
    color: var(--accent2); letter-spacing: 0.1em;
    border: 1px solid rgba(0,229,195,0.25);
    padding: 6px 14px; border-radius: 2px;
    margin-bottom: 2rem;
    animation: fadeUp 0.7s 0.2s ease both;
  }
  .hero-tag::before { content: '//'; opacity: 0.5; }

  .hero-name {
    font-size: clamp(3.5rem, 9vw, 7rem);
    font-weight: 800; line-height: 0.95;
    letter-spacing: -0.03em;
    animation: fadeUp 0.7s 0.35s ease both;
    position: relative;
  }
  .hero-name .line1 { display: block; color: var(--text); }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-desc {
    margin-top: 2rem; max-width: 520px;
    font-size: 1.05rem; color: var(--muted2); line-height: 1.7;
    animation: fadeUp 0.7s 0.5s ease both;
  }

  .hero-cta {
    margin-top: 2.5rem; display: flex; gap: 1rem; flex-wrap: wrap;
    animation: fadeUp 0.7s 0.65s ease both;
  }
  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 12px 28px; border-radius: 3px;
    font-family: 'Syne', sans-serif; font-size: 0.9rem; font-weight: 600;
    letter-spacing: 0.04em; text-decoration: none; cursor: none;
    transition: all 0.25s;
  }
  .btn-primary {
    background: var(--accent); color: #000;
    border: 1px solid var(--accent);
    box-shadow: 0 0 28px rgba(74,158,255,0.35);
  }
  .btn-primary:hover { background: var(--accent2); border-color: var(--accent2); box-shadow: 0 0 38px rgba(0,229,195,0.4); transform: translateY(-2px); }
  .btn-ghost {
    background: transparent; color: var(--text);
    border: 1px solid var(--border2);
  }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  .hero-scroll {
    position: absolute; bottom: 2.5rem; left: 3rem;
    display: flex; align-items: center; gap: 12px;
    color: var(--muted); font-size: 0.75rem; letter-spacing: 0.12em;
    text-transform: uppercase; font-family: 'DM Mono', monospace;
    animation: fadeUp 0.7s 0.9s ease both;
  }
  .scroll-line {
    width: 40px; height: 1px; background: var(--muted);
    animation: scrollLine 2s ease-in-out infinite;
  }
  @keyframes scrollLine { 0%,100% { width: 40px; } 50% { width: 70px; } }

  @keyframes fadeUp { from { transform: translateY(28px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

  /* ─── SECTION HEADER ─── */
  .section-header {
    margin-bottom: 3.5rem;
  }
  .section-num {
    font-family: 'DM Mono', monospace; font-size: 0.75rem;
    color: var(--accent); letter-spacing: 0.15em; margin-bottom: 0.6rem;
  }
  .section-title {
    font-size: clamp(2rem, 5vw, 3rem); font-weight: 800;
    letter-spacing: -0.02em; color: var(--text);
    line-height: 1;
  }
  .section-title span {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .container { max-width: 1100px; margin: 0 auto; padding: 6rem 3rem; }

  /* ─── ABOUT ─── */
  #about { background: var(--bg2); }
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center;
  }
  .about-text p {
    color: var(--muted2); line-height: 1.8; font-size: 1rem; margin-bottom: 1.2rem;
  }
  .about-text p:last-child { margin-bottom: 0; }
  .about-text strong { color: var(--accent); font-weight: 600; }
  .stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
  .stat-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 4px; padding: 1.5rem;
    transition: border-color 0.3s, transform 0.3s;
  }
  .stat-card:hover { border-color: var(--accent); transform: translateY(-4px); }
  .stat-num {
    font-size: 2.2rem; font-weight: 800; color: var(--accent);
    line-height: 1; margin-bottom: 4px;
  }
  .stat-label { font-size: 0.8rem; color: var(--muted); letter-spacing: 0.08em; text-transform: uppercase; }

  /* ─── SKILLS ─── */
  #skills { background: var(--bg); }
  .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem; }
  .skill-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 4px; padding: 2rem;
    transition: all 0.3s; position: relative; overflow: hidden;
  }
  .skill-card::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0); transition: transform 0.3s;
    transform-origin: left;
  }
  .skill-card:hover::before { transform: scaleX(1); }
  .skill-card:hover { border-color: var(--border2); transform: translateY(-4px); box-shadow: 0 20px 60px rgba(0,0,0,0.5); }
  .skill-icon { font-size: 2rem; margin-bottom: 1rem; }
  .skill-title { font-size: 1.05rem; font-weight: 700; margin-bottom: 0.6rem; color: var(--text); }
  .skill-desc { font-size: 0.88rem; color: var(--muted2); line-height: 1.6; margin-bottom: 1.2rem; }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .tag {
    font-family: 'DM Mono', monospace; font-size: 0.72rem;
    padding: 3px 10px; border-radius: 2px;
    background: rgba(74,158,255,0.08); color: var(--accent);
    border: 1px solid rgba(74,158,255,0.2);
    letter-spacing: 0.05em;
  }
  .tag.teal { background: rgba(0,229,195,0.08); color: var(--accent2); border-color: rgba(0,229,195,0.2); }

  /* ─── TECH STACK ─── */
  .tech-stack {
    margin-top: 4rem;
    display: flex; flex-wrap: wrap; gap: 12px; align-items: center;
  }
  .tech-label {
    font-family: 'DM Mono', monospace; font-size: 0.75rem;
    color: var(--muted); letter-spacing: 0.1em; margin-right: 8px;
  }
  .tech-pill {
    display: flex; align-items: center; gap: 7px;
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 3px; padding: 8px 14px;
    font-size: 0.85rem; font-weight: 600; color: var(--text);
    transition: all 0.25s;
  }
  .tech-pill:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }
  .tech-pill .dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--accent2); flex-shrink: 0;
  }

  /* ─── PROJECTS ─── */
  #projects { background: var(--bg2); }
  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
  .project-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 4px; padding: 2rem;
    transition: all 0.3s; position: relative; overflow: hidden;
    display: flex; flex-direction: column;
  }
  .project-card::after {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(74,158,255,0.04), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .project-card:hover::after { opacity: 1; }
  .project-card:hover { border-color: var(--border2); transform: translateY(-5px); box-shadow: 0 24px 64px rgba(0,0,0,0.6); }
  .project-top {
    display: flex; justify-content: space-between; align-items: flex-start;
    margin-bottom: 1rem;
  }
  .project-icon { font-size: 1.8rem; }
  .project-links { display: flex; gap: 10px; }
  .project-link {
    color: var(--muted); font-size: 1.1rem; text-decoration: none;
    transition: color 0.2s;
  }
  .project-link:hover { color: var(--accent); }
  .project-title {
    font-size: 1.15rem; font-weight: 700; margin-bottom: 0.6rem; color: var(--text);
  }
  .project-desc {
    font-size: 0.88rem; color: var(--muted2); line-height: 1.65; flex: 1; margin-bottom: 1.5rem;
  }
  .project-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .project-featured {
    grid-column: 1 / -1;
    display: grid; grid-template-columns: 1fr 1fr; gap: 2rem;
    padding: 2.5rem;
  }
  .project-featured .project-desc { font-size: 0.95rem; }
  .featured-badge {
    display: inline-block; font-family: 'DM Mono', monospace;
    font-size: 0.7rem; letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--accent2); background: rgba(0,229,195,0.1);
    border: 1px solid rgba(0,229,195,0.2);
    padding: 3px 10px; border-radius: 2px; margin-bottom: 1rem;
  }
  .project-img-placeholder {
    background: linear-gradient(135deg, rgba(74,158,255,0.1), rgba(0,229,195,0.08));
    border: 1px solid var(--border); border-radius: 4px;
    display: flex; align-items: center; justify-content: center;
    font-size: 4rem; min-height: 200px;
    position: relative; overflow: hidden;
  }
  .project-img-placeholder::before {
    content: ''; position: absolute; inset: 0;
    background: repeating-linear-gradient(
      45deg, transparent, transparent 20px,
      rgba(74,158,255,0.03) 20px, rgba(74,158,255,0.03) 21px
    );
  }

  /* ─── CONTACT ─── */
  #contact { background: var(--bg); }
  .contact-inner {
    max-width: 640px; margin: 0 auto; text-align: center;
  }
  .contact-email {
    display: inline-block; margin: 2.5rem 0;
    font-size: clamp(1.1rem, 3vw, 1.6rem); font-weight: 700;
    color: var(--text); text-decoration: none;
    border-bottom: 2px solid var(--accent);
    padding-bottom: 4px; transition: color 0.2s;
  }
  .contact-email:hover { color: var(--accent); }
  .social-links { display: flex; justify-content: center; gap: 1.5rem; margin-top: 2rem; }
  .social-link {
    display: flex; align-items: center; gap: 8px;
    color: var(--muted2); text-decoration: none; font-size: 0.9rem;
    font-weight: 600; padding: 10px 20px;
    border: 1px solid var(--border); border-radius: 3px;
    transition: all 0.25s;
  }
  .social-link:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  /* ─── FOOTER ─── */
  footer {
    background: var(--bg2); border-top: 1px solid var(--border);
    padding: 2rem 3rem;
    display: flex; align-items: center; justify-content: space-between;
    font-size: 0.8rem; color: var(--muted); font-family: 'DM Mono', monospace;
  }

  /* ─── REVEAL ANIMATIONS ─── */
  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }

  /* ─── SCANLINE HERO EFFECT ─── */
  .scanline {
    position: absolute; inset: 0; pointer-events: none;
    background: repeating-linear-gradient(
      0deg, transparent, transparent 2px,
      rgba(0,0,0,0.04) 2px, rgba(0,0,0,0.04) 4px
    );
  }

  /* ─── BLINKING CURSOR ─── */
  .blink {
    display: inline-block; width: 3px; height: 0.85em;
    background: var(--accent); margin-left: 4px; vertical-align: middle;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0; } }

  /* Responsive */
  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    #hero { padding: 6rem 1.5rem 3rem; }
    .container { padding: 4rem 1.5rem; }
    .about-grid { grid-template-columns: 1fr; gap: 3rem; }
    .projects-grid { grid-template-columns: 1fr; }
    .project-featured { grid-column: 1; grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 0.5rem; text-align: center; }
    body { cursor: auto; }
    #cursor, #cursor-ring { display: none; }
  }
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- NAV -->
<nav>
  <a class="logo" href="#hero">EM<span>.</span></a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a class="btn btn-primary" href="mailto:eyadmotawe@gmail.com" style="padding:9px 20px;font-size:0.82rem">Hire me</a>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-glow"></div>
  <div class="hero-glow2"></div>
  <div class="scanline"></div>

  <div class="hero-tag">Computer Engineering · Alexandria University</div>

  <h1 class="hero-name">
    <span class="line1">Eyad</span>
    <span class="line2">Motawea<span class="blink"></span></span>
  </h1>

  <p class="hero-desc">
    Software engineer who loves solving hard problems and building clean, fast applications — from efficient algorithms to full-stack web apps and hardware architecture.
  </p>

  <div class="hero-cta">
    <a class="btn btn-primary" href="#projects">View Projects</a>
    <a class="btn btn-ghost" href="#contact">Get in Touch</a>
  </div>

  <div class="hero-scroll">
    <div class="scroll-line"></div>
    scroll
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-num">01 // ABOUT</div>
      <h2 class="section-title">Who I <span>Am</span></h2>
    </div>
    <div class="about-grid">
      <div class="about-text">
        <p class="reveal">I'm a <strong>Computer Engineering student</strong> at Alexandria University with a deep passion for understanding systems at every layer — from writing optimized C++ algorithms to architecting web applications and studying digital hardware.</p>
        <p class="reveal reveal-delay-1">I believe the best engineers understand the full stack: the metal underneath, the OS on top, and everything in between. That systems-level thinking shapes how I approach every problem I tackle.</p>
        <p class="reveal reveal-delay-2">When I'm not writing code or studying circuits, I'm sharpening my problem-solving edge through competitive programming challenges.</p>
      </div>
      <div class="stat-grid">
        <div class="stat-card reveal">
          <div class="stat-num">C++</div>
          <div class="stat-label">Primary Language</div>
        </div>
        <div class="stat-card reveal reveal-delay-1">
          <div class="stat-num">Full</div>
          <div class="stat-label">Stack Capable</div>
        </div>
        <div class="stat-card reveal reveal-delay-2">
          <div class="stat-num">HW</div>
          <div class="stat-label">Systems Knowledge</div>
        </div>
        <div class="stat-card reveal reveal-delay-3">
          <div class="stat-num">ALX</div>
          <div class="stat-label">University · Egypt</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-num">02 // SKILLS</div>
      <h2 class="section-title">What I <span>Build</span></h2>
    </div>

    <div class="skills-grid">
      <div class="skill-card reveal">
        <div class="skill-icon">⚡</div>
        <div class="skill-title">Algorithms & Problem Solving</div>
        <div class="skill-desc">Hard coding puzzles and competitive programming in C++. Optimized data structures, time complexity analysis, and clean algorithmic thinking.</div>
        <div class="skill-tags">
          <span class="tag">C++</span>
          <span class="tag">Data Structures</span>
          <span class="tag">Algorithms</span>
        </div>
      </div>
      <div class="skill-card reveal reveal-delay-1">
        <div class="skill-icon">🌐</div>
        <div class="skill-title">Full-Stack Web Development</div>
        <div class="skill-desc">Building interactive web applications and browser tools using modern frameworks. Component-driven UIs, REST API integration, and clean architecture.</div>
        <div class="skill-tags">
          <span class="tag teal">React.js</span>
          <span class="tag teal">JavaScript</span>
          <span class="tag teal">APIs</span>
        </div>
      </div>
      <div class="skill-card reveal reveal-delay-2">
        <div class="skill-icon">🔩</div>
        <div class="skill-title">Hardware & Computer Architecture</div>
        <div class="skill-desc">Understanding how computers work under the hood — from logic gates and digital circuits to CPU architecture and memory systems.</div>
        <div class="skill-tags">
          <span class="tag">Digital Logic</span>
          <span class="tag">Architecture</span>
          <span class="tag">Systems</span>
        </div>
      </div>
      <div class="skill-card reveal reveal-delay-3">
        <div class="skill-icon">🛠</div>
        <div class="skill-title">Software Engineering Tools</div>
        <div class="skill-desc">Using industry-standard tools for version control, collaboration, and development workflows. Clean code practices and project organization.</div>
        <div class="skill-tags">
          <span class="tag">Git</span>
          <span class="tag">GitHub</span>
          <span class="tag">Java</span>
          <span class="tag">Python</span>
        </div>
      </div>
    </div>

    <div class="tech-stack reveal">
      <span class="tech-label">stack //</span>
      <div class="tech-pill"><span class="dot"></span>C++</div>
      <div class="tech-pill"><span class="dot"></span>JavaScript</div>
      <div class="tech-pill"><span class="dot"></span>React.js</div>
      <div class="tech-pill"><span class="dot"></span>Java</div>
      <div class="tech-pill"><span class="dot"></span>Python</div>
      <div class="tech-pill"><span class="dot"></span>Git</div>
      <div class="tech-pill"><span class="dot"></span>REST APIs</div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-num">03 // PROJECTS</div>
      <h2 class="section-title">What I've <span>Made</span></h2>
    </div>

    <div class="projects-grid">
      <!-- Featured -->
      <div class="project-card project-featured reveal">
        <div>
          <div class="featured-badge">✦ Featured Project</div>
          <div class="project-top">
            <div class="project-icon">🧠</div>
            <div class="project-links">
              <a class="project-link" href="#" title="GitHub">⬡</a>
              <a class="project-link" href="#" title="Live demo">↗</a>
            </div>
          </div>
          <div class="project-title">Algorithm Visualizer</div>
          <div class="project-desc">An interactive tool for visualizing classic sorting and pathfinding algorithms in real-time. Built to help students understand algorithmic complexity through animation — because seeing is understanding.</div>
          <div class="project-tags">
            <span class="tag teal">React.js</span>
            <span class="tag teal">JavaScript</span>
            <span class="tag">Algorithms</span>
            <span class="tag">CSS Animations</span>
          </div>
        </div>
        <div class="project-img-placeholder">🔬</div>
      </div>

      <!-- Other projects -->
      <div class="project-card reveal">
        <div class="project-top">
          <div class="project-icon">💻</div>
          <div class="project-links">
            <a class="project-link" href="#" title="GitHub">⬡</a>
          </div>
        </div>
        <div class="project-title">C++ Data Structures Library</div>
        <div class="project-desc">A clean, well-documented implementation of core data structures — linked lists, trees, graphs, heaps — written in modern C++ with performance benchmarks.</div>
        <div class="project-tags">
          <span class="tag">C++</span>
          <span class="tag">STL</span>
          <span class="tag">Performance</span>
        </div>
      </div>

      <div class="project-card reveal reveal-delay-1">
        <div class="project-top">
          <div class="project-icon">🌍</div>
          <div class="project-links">
            <a class="project-link" href="#" title="GitHub">⬡</a>
            <a class="project-link" href="#" title="Live demo">↗</a>
          </div>
        </div>
        <div class="project-title">React Web Application</div>
        <div class="project-desc">A modern single-page application with API integration, responsive design, and clean component architecture built with React hooks and best practices.</div>
        <div class="project-tags">
          <span class="tag teal">React.js</span>
          <span class="tag teal">REST API</span>
          <span class="tag">JavaScript</span>
        </div>
      </div>

      <div class="project-card reveal reveal-delay-2">
        <div class="project-top">
          <div class="project-icon">🔧</div>
          <div class="project-links">
            <a class="project-link" href="#" title="GitHub">⬡</a>
          </div>
        </div>
        <div class="project-title">CPU Design Simulation</div>
        <div class="project-desc">A digital hardware project simulating a simple CPU architecture — fetch, decode, execute cycle — with register file, ALU, and control unit implemented at the logic level.</div>
        <div class="project-tags">
          <span class="tag">Digital Logic</span>
          <span class="tag">Architecture</span>
          <span class="tag">Simulation</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="container">
    <div class="contact-inner">
      <div class="section-header reveal" style="text-align:center">
        <div class="section-num" style="justify-content:center;display:flex">04 // CONTACT</div>
        <h2 class="section-title">Let's <span>Connect</span></h2>
      </div>
      <p class="reveal" style="color:var(--muted2);line-height:1.8">Whether you have a project in mind, want to collaborate, or just want to talk about algorithms and systems — my inbox is always open.</p>
      <a class="contact-email reveal" href="mailto:eyadmotawe@gmail.com">eyadmotawe@gmail.com</a>
      <div class="social-links reveal">
        <a class="social-link" href="https://www.linkedin.com/in/eyad-motawea-a7266121a/" target="_blank">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
          LinkedIn
        </a>
        <a class="social-link" href="https://github.com/" target="_blank">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
          GitHub
        </a>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span>© 2025 Eyad Motawea</span>
  <span>Built with HTML · CSS · JS</span>
  <span style="color:var(--accent)">Alexandria, Egypt</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursor-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animateCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animateCursor);
  }
  animateCursor();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.12 });
  reveals.forEach(r => observer.observe(r));

  // Nav active state on scroll
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');
  window.addEventListener('scroll', () => {
    let cur = '';
    sections.forEach(s => { if (window.scrollY >= s.offsetTop - 120) cur = s.id; });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#'+cur ? 'var(--accent)' : '';
    });
  });
</script>
</body>
</html>
