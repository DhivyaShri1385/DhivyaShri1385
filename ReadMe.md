<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Dhivya Shri — AI Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
  :root {
    --cyan: #00f5ff;
    --purple: #7b2ff7;
    --pink: #ff2d9b;
    --dark: #020510;
    --darker: #010308;
    --card: rgba(255,255,255,0.03);
    --glow-c: 0 0 20px rgba(0,245,255,0.4), 0 0 60px rgba(0,245,255,0.1);
    --glow-p: 0 0 20px rgba(123,47,247,0.5), 0 0 60px rgba(123,47,247,0.15);
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--dark);
    color: #e0e8ff;
    font-family: 'Rajdhani', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* ── CUSTOM CURSOR ── */
  .cursor {
    position: fixed; width: 12px; height: 12px;
    background: var(--cyan); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, opacity 0.2s;
    box-shadow: 0 0 15px var(--cyan), 0 0 40px rgba(0,245,255,0.3);
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed; width: 40px; height: 40px;
    border: 1px solid rgba(0,245,255,0.5); border-radius: 50%;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.15s ease, width 0.3s, height 0.3s, opacity 0.3s;
  }

  /* ── CANVAS BACKGROUND ── */
  #neural-canvas {
    position: fixed; top:0; left:0; width:100%; height:100%;
    z-index: 0; pointer-events: none;
  }

  /* ── FLOATING ORBS ── */
  .orb {
    position: fixed; border-radius: 50%;
    filter: blur(80px); opacity: 0.15;
    pointer-events: none; z-index: 0;
    animation: floatOrb linear infinite;
  }
  .orb-1 { width:600px; height:600px; background:var(--purple); top:-200px; right:-200px; animation-duration:25s; }
  .orb-2 { width:400px; height:400px; background:var(--cyan); bottom:-100px; left:-100px; animation-duration:20s; animation-delay:-10s; }
  .orb-3 { width:300px; height:300px; background:var(--pink); top:40%; right:10%; animation-duration:18s; animation-delay:-5s; }

  @keyframes floatOrb {
    0%,100% { transform: translate(0,0) scale(1); }
    33% { transform: translate(30px,-40px) scale(1.05); }
    66% { transform: translate(-20px,30px) scale(0.95); }
  }

  /* ── SCANLINES ── */
  .scanlines {
    position: fixed; top:0; left:0; width:100%; height:100%;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none; z-index: 1; animation: scanMove 8s linear infinite;
  }
  @keyframes scanMove { 0%{ background-position: 0 0; } 100%{ background-position: 0 100px; } }

  /* ── GRAIN OVERLAY ── */
  .grain {
    position: fixed; top:-50%; left:-50%; width:200%; height:200%;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
    opacity: 0.03; pointer-events: none; z-index: 2;
    animation: grainAnim 0.5s steps(2) infinite;
  }
  @keyframes grainAnim { 0%{transform:translate(0,0)} 25%{transform:translate(-2%,-2%)} 50%{transform:translate(2%,-1%)} 75%{transform:translate(-1%,2%)} 100%{transform:translate(2%,1%)} }

  /* ── LAYOUT ── */
  main { position: relative; z-index: 10; }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: grid; place-items: center;
    text-align: center; padding: 2rem;
    position: relative;
  }

  .hero-inner { position: relative; }

  .status-badge {
    display: inline-flex; align-items: center; gap: 8px;
    border: 1px solid rgba(0,245,255,0.3);
    background: rgba(0,245,255,0.05);
    padding: 6px 18px; border-radius: 100px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem; letter-spacing: 3px;
    color: var(--cyan); margin-bottom: 2rem;
    animation: fadeUp 1s ease 0.2s both;
  }
  .status-dot {
    width: 6px; height: 6px; background: var(--cyan);
    border-radius: 50%; animation: pulse 2s ease infinite;
  }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.4;transform:scale(0.8)} }

  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(3rem, 10vw, 8rem);
    font-weight: 900; line-height: 0.9;
    letter-spacing: -2px;
    animation: fadeUp 1s ease 0.4s both;
  }
  .hero-name span {
    display: block;
    background: linear-gradient(135deg, #fff 0%, var(--cyan) 40%, var(--purple) 80%, var(--pink) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    filter: drop-shadow(0 0 30px rgba(0,245,255,0.3));
  }

  .hero-sub {
    font-family: 'Share Tech Mono', monospace;
    font-size: clamp(0.8rem, 2vw, 1.1rem);
    color: rgba(255,255,255,0.5); letter-spacing: 6px;
    text-transform: uppercase; margin: 1.5rem 0;
    animation: fadeUp 1s ease 0.6s both;
  }

  .type-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: clamp(1rem, 2.5vw, 1.4rem);
    color: var(--cyan); margin: 1rem 0 2.5rem;
    animation: fadeUp 1s ease 0.8s both;
    min-height: 2em;
  }
  .type-cursor { animation: blink 1s step-end infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .hero-btns {
    display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;
    animation: fadeUp 1s ease 1s both;
  }
  .btn {
    padding: 14px 36px; border-radius: 6px; font-family: 'Rajdhani', sans-serif;
    font-size: 1rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase;
    text-decoration: none; cursor: pointer; border: none;
    transition: all 0.3s ease; position: relative; overflow: hidden;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--cyan), var(--purple));
    color: #000;
    box-shadow: 0 0 30px rgba(0,245,255,0.3);
  }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 0 50px rgba(0,245,255,0.5); }
  .btn-outline {
    background: transparent; color: var(--cyan);
    border: 1px solid rgba(0,245,255,0.4);
  }
  .btn-outline:hover { background: rgba(0,245,255,0.08); transform: translateY(-3px); border-color: var(--cyan); }

  .scroll-hint {
    position: absolute; bottom: 2rem; left: 50%;
    transform: translateX(-50%);
    animation: fadeUp 1s ease 1.5s both;
    display: flex; flex-direction: column; align-items: center; gap: 8px;
  }
  .scroll-hint span { font-family:'Share Tech Mono',monospace; font-size:0.65rem; letter-spacing:3px; color:rgba(255,255,255,0.3); }
  .scroll-line { width:1px; height:50px; background: linear-gradient(var(--cyan), transparent); animation: scrollDrop 2s ease infinite; }
  @keyframes scrollDrop { 0%{transform:scaleY(0);transform-origin:top} 50%{transform:scaleY(1);transform-origin:top} 51%{transform:scaleY(1);transform-origin:bottom} 100%{transform:scaleY(0);transform-origin:bottom} }

  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }

  /* ── SECTION ── */
  section { padding: 6rem 2rem; max-width: 1200px; margin: 0 auto; }

  .sec-label {
    font-family:'Share Tech Mono',monospace; font-size:0.7rem;
    letter-spacing:5px; color:var(--cyan); opacity:0.7; margin-bottom:0.5rem;
  }
  .sec-title {
    font-family:'Orbitron',monospace; font-size:clamp(1.8rem,4vw,3rem);
    font-weight:700; margin-bottom:3rem;
    background: linear-gradient(135deg,#fff,rgba(255,255,255,0.5));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text;
  }

  /* ── ABOUT GRID ── */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 2rem;
  }
  @media(max-width:700px){ .about-grid{ grid-template-columns:1fr; } }

  .terminal-card {
    background: rgba(0,0,0,0.5);
    border: 1px solid rgba(0,245,255,0.15);
    border-radius: 12px; overflow: hidden;
    box-shadow: 0 0 40px rgba(0,245,255,0.05);
    backdrop-filter: blur(10px);
  }
  .terminal-bar {
    background: rgba(0,245,255,0.08); padding: 10px 16px;
    display: flex; align-items: center; gap: 8px;
    border-bottom: 1px solid rgba(0,245,255,0.1);
  }
  .t-dot { width:10px;height:10px;border-radius:50%; }
  .t-dot:nth-child(1){background:#ff5f56}
  .t-dot:nth-child(2){background:#ffbd2e}
  .t-dot:nth-child(3){background:#27c93f}
  .terminal-title { font-family:'Share Tech Mono',monospace; font-size:0.7rem; color:rgba(255,255,255,0.4); margin-left:auto; letter-spacing:2px; }
  .terminal-body { padding: 1.5rem; font-family:'Share Tech Mono',monospace; font-size:0.85rem; line-height:2; }
  .t-key { color: var(--purple); }
  .t-val { color: var(--cyan); }
  .t-str { color: #a8ff78; }
  .t-comment { color: rgba(255,255,255,0.25); }

  .stat-grid { display:grid; grid-template-columns:1fr 1fr; gap:1rem; }
  .stat-box {
    background: rgba(0,0,0,0.4); border:1px solid rgba(123,47,247,0.2);
    border-radius:10px; padding:1.2rem; text-align:center;
    transition: all 0.3s; backdrop-filter:blur(10px);
  }
  .stat-box:hover { border-color:var(--cyan); transform:translateY(-4px); box-shadow: var(--glow-c); }
  .stat-num { font-family:'Orbitron',monospace; font-size:2rem; font-weight:900; color:var(--cyan); }
  .stat-lbl { font-size:0.75rem; letter-spacing:2px; color:rgba(255,255,255,0.4); margin-top:4px; }

  /* ── SKILLS ── */
  .skill-cats { display:flex; flex-direction:column; gap:2rem; }
  .skill-cat-label { font-family:'Share Tech Mono',monospace; font-size:0.7rem; letter-spacing:4px; color:var(--purple); margin-bottom:1rem; }
  .skill-pills { display:flex; flex-wrap:wrap; gap:0.75rem; }
  .pill {
    padding: 8px 18px; border-radius:6px; font-size:0.85rem; font-weight:600;
    letter-spacing:1px; border:1px solid rgba(255,255,255,0.08);
    background: rgba(255,255,255,0.03); color:rgba(255,255,255,0.8);
    transition:all 0.3s; position:relative; overflow:hidden;
    backdrop-filter: blur(5px);
  }
  .pill::before {
    content:''; position:absolute; inset:0;
    background:linear-gradient(135deg,var(--cyan),var(--purple));
    opacity:0; transition:opacity 0.3s;
  }
  .pill:hover::before { opacity:0.15; }
  .pill:hover { border-color:var(--cyan); color:#fff; transform:translateY(-2px); box-shadow: 0 4px 20px rgba(0,245,255,0.2); }
  .pill span { position:relative; z-index:1; }

  /* ── PROJECTS ── */
  .projects-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(320px,1fr)); gap:1.5rem; }
  .project-card {
    background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.07);
    border-radius:16px; padding:2rem; position:relative; overflow:hidden;
    transition:all 0.4s; backdrop-filter:blur(12px);
  }
  .project-card::before {
    content:''; position:absolute; top:0; left:0; right:0; height:1px;
    background:linear-gradient(90deg,transparent,var(--cyan),transparent);
    opacity:0; transition:opacity 0.4s;
  }
  .project-card:hover { transform:translateY(-6px); border-color:rgba(0,245,255,0.25); box-shadow: 0 20px 60px rgba(0,0,0,0.5), var(--glow-c); }
  .project-card:hover::before { opacity:1; }
  .project-icon { font-size:2.5rem; margin-bottom:1rem; }
  .project-title { font-family:'Orbitron',monospace; font-size:1rem; font-weight:700; margin-bottom:0.75rem; color:#fff; }
  .project-desc { font-size:0.9rem; color:rgba(255,255,255,0.5); line-height:1.7; margin-bottom:1.2rem; }
  .project-tags { display:flex; flex-wrap:wrap; gap:0.5rem; }
  .tag { font-family:'Share Tech Mono',monospace; font-size:0.65rem; letter-spacing:1px; padding:3px 10px; border-radius:4px; background:rgba(123,47,247,0.15); border:1px solid rgba(123,47,247,0.3); color:var(--purple); }
  .project-status { position:absolute; top:1.2rem; right:1.2rem; font-family:'Share Tech Mono',monospace; font-size:0.6rem; letter-spacing:2px; display:flex; align-items:center; gap:5px; }
  .ps-dot { width:5px;height:5px;border-radius:50%; }
  .ps-active .ps-dot { background:#27c93f; box-shadow:0 0 8px #27c93f; }
  .ps-active { color:#27c93f; }
  .ps-training .ps-dot { background:#ffbd2e; box-shadow:0 0 8px #ffbd2e; animation:pulse 1.5s ease infinite; }
  .ps-training { color:#ffbd2e; }

  /* ── CONNECT ── */
  .connect-wrap { text-align:center; }
  .social-row { display:flex; justify-content:center; gap:1rem; flex-wrap:wrap; margin-top:2rem; }
  .social-btn {
    display:flex; align-items:center; gap:10px;
    padding:14px 28px; border-radius:10px;
    border:1px solid rgba(255,255,255,0.1);
    background:rgba(255,255,255,0.03);
    color:#fff; text-decoration:none; font-weight:600;
    font-size:0.9rem; letter-spacing:1px;
    transition:all 0.3s; backdrop-filter:blur(8px);
  }
  .social-btn:hover { transform:translateY(-4px); background:rgba(255,255,255,0.07); }
  .social-btn.li:hover { border-color:#0077b5; box-shadow:0 0 30px rgba(0,119,181,0.3); }
  .social-btn.ig:hover { border-color:#e4405f; box-shadow:0 0 30px rgba(228,64,95,0.3); }
  .social-btn.gm:hover { border-color:#ea4335; box-shadow:0 0 30px rgba(234,67,53,0.3); }
  .social-btn svg { width:20px;height:20px; }

  /* ── QUOTE ── */
  .quote-block {
    text-align:center; padding:4rem 2rem;
    font-family:'Orbitron',monospace; font-size:clamp(1rem,2.5vw,1.6rem);
    font-weight:400; color:rgba(255,255,255,0.3);
    border-top:1px solid rgba(255,255,255,0.05);
    position:relative; z-index:10;
    max-width:900px; margin:0 auto;
    line-height:1.8;
  }
  .quote-block em { color:var(--cyan); font-style:normal; }

  /* ── FOOTER ── */
  footer {
    text-align:center; padding:2rem;
    font-family:'Share Tech Mono',monospace; font-size:0.7rem;
    letter-spacing:3px; color:rgba(255,255,255,0.2);
    border-top:1px solid rgba(255,255,255,0.05);
    position:relative; z-index:10;
  }

  /* ── NAV ── */
  nav {
    position:fixed; top:0; left:0; right:0; z-index:100;
    padding:1.2rem 3rem; display:flex; align-items:center; justify-content:space-between;
    background:rgba(2,5,16,0.7); backdrop-filter:blur(20px);
    border-bottom:1px solid rgba(255,255,255,0.05);
  }
  .nav-logo { font-family:'Orbitron',monospace; font-weight:900; font-size:1.2rem;
    background:linear-gradient(135deg,var(--cyan),var(--purple));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  .nav-links { display:flex; gap:2rem; list-style:none; }
  .nav-links a { font-family:'Share Tech Mono',monospace; font-size:0.75rem; letter-spacing:2px; color:rgba(255,255,255,0.5); text-decoration:none; transition:color 0.3s; }
  .nav-links a:hover { color:var(--cyan); }

  /* ── GLITCH ── */
  .glitch { position:relative; }
  .glitch::before,.glitch::after {
    content:attr(data-text); position:absolute; top:0; left:0;
    background:linear-gradient(135deg, #fff 0%, var(--cyan) 40%, var(--purple) 80%, var(--pink) 100%);
    -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text;
  }
  .glitch::before { animation:glitch1 4s infinite; clip-path:polygon(0 0,100% 0,100% 35%,0 35%); }
  .glitch::after { animation:glitch2 4s infinite; clip-path:polygon(0 65%,100% 65%,100% 100%,0 100%); }
  @keyframes glitch1 {
    0%,95%{transform:translate(0)} 96%{transform:translate(-3px,1px)} 97%{transform:translate(3px,-1px)} 98%{transform:translate(-1px,2px)} 100%{transform:translate(0)}
  }
  @keyframes glitch2 {
    0%,95%{transform:translate(0)} 96%{transform:translate(3px,-2px)} 97%{transform:translate(-3px,2px)} 98%{transform:translate(2px,-1px)} 100%{transform:translate(0)}
  }

  /* ── DIVIDER ── */
  .cyber-divider {
    max-width:1200px; margin:0 auto;
    height:1px; position:relative;
    background:linear-gradient(90deg,transparent,var(--cyan),transparent);
    opacity:0.3;
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Background effects -->
<canvas id="neural-canvas"></canvas>
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>
<div class="scanlines"></div>
<div class="grain"></div>

<!-- Navigation -->
<nav>
  <div class="nav-logo">DS.AI</div>
  <ul class="nav-links">
    <li><a href="#about">ABOUT</a></li>
    <li><a href="#skills">SKILLS</a></li>
    <li><a href="#projects">PROJECTS</a></li>
    <li><a href="#connect">CONNECT</a></li>
  </ul>
</nav>

<main>
  <!-- HERO -->
  <section class="hero">
    <div class="hero-inner">
      <div class="status-badge"><div class="status-dot"></div>SYSTEM ONLINE — READY TO BUILD</div>

      <div class="hero-name">
        <span class="glitch" data-text="DHIVYA">DHIVYA</span>
        <span class="glitch" data-text="SHRI">SHRI</span>
      </div>

      <div class="hero-sub">AI Engineer · ML Developer · Data Scientist</div>

      <div class="type-line" id="typewriter"></div>

      <div class="hero-btns">
        <a href="#projects" class="btn btn-primary">VIEW PROJECTS</a>
        <a href="#connect" class="btn btn-outline">CONNECT</a>
      </div>
    </div>
    <div class="scroll-hint">
      <span>SCROLL</span>
      <div class="scroll-line"></div>
    </div>
  </section>

  <div class="cyber-divider"></div>

  <!-- ABOUT -->
  <section id="about">
    <div class="sec-label">// AGENT PROFILE</div>
    <div class="sec-title">ABOUT ME</div>
    <div class="about-grid">
      <div class="terminal-card">
        <div class="terminal-bar">
          <div class="t-dot"></div><div class="t-dot"></div><div class="t-dot"></div>
          <div class="terminal-title">profile.py</div>
        </div>
        <div class="terminal-body">
          <div><span class="t-comment"># Agent initialized</span></div>
          <div><span class="t-key">class </span><span class="t-val">DhivyaShri</span>:</div>
          <div>&nbsp;&nbsp;<span class="t-key">name </span>= <span class="t-str">"Dhivya Shri"</span></div>
          <div>&nbsp;&nbsp;<span class="t-key">role </span>= <span class="t-str">"AI/ML Developer"</span></div>
          <div>&nbsp;&nbsp;<span class="t-key">base </span>= <span class="t-str">"India 🇮🇳"</span></div>
          <div>&nbsp;&nbsp;<span class="t-key">passion </span>= [</div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Neural Networks"</span>,</div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Data Science"</span>,</div>
          <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Smart Systems"</span></div>
          <div>&nbsp;&nbsp;]</div>
          <div>&nbsp;&nbsp;<span class="t-key">status </span>= <span class="t-str">"Always Learning 🚀"</span></div>
        </div>
      </div>

      <div class="stat-grid">
        <div class="stat-box">
          <div class="stat-num">5+</div>
          <div class="stat-lbl">LANGUAGES</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">10+</div>
          <div class="stat-lbl">FRAMEWORKS</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">AI</div>
          <div class="stat-lbl">FOCUS AREA</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">∞</div>
          <div class="stat-lbl">CURIOSITY</div>
        </div>
      </div>
    </div>
  </section>

  <div class="cyber-divider"></div>

  <!-- SKILLS -->
  <section id="skills">
    <div class="sec-label">// NEURAL CORE</div>
    <div class="sec-title">TECH STACK</div>
    <div class="skill-cats">
      <div>
        <div class="skill-cat-label">◈ LANGUAGES</div>
        <div class="skill-pills">
          <div class="pill"><span>Python</span></div><div class="pill"><span>Java</span></div>
          <div class="pill"><span>C</span></div><div class="pill"><span>C++</span></div>
          <div class="pill"><span>R</span></div>
        </div>
      </div>
      <div>
        <div class="skill-cat-label">◈ AI / ML STACK</div>
        <div class="skill-pills">
          <div class="pill"><span>TensorFlow</span></div><div class="pill"><span>PyTorch</span></div>
          <div class="pill"><span>Keras</span></div><div class="pill"><span>scikit-learn</span></div>
          <div class="pill"><span>OpenCV</span></div><div class="pill"><span>SciPy</span></div>
          <div class="pill"><span>NumPy</span></div><div class="pill"><span>Pandas</span></div>
        </div>
      </div>
      <div>
        <div class="skill-cat-label">◈ VISUALIZATION & BI</div>
        <div class="skill-pills">
          <div class="pill"><span>Power BI</span></div><div class="pill"><span>Matplotlib</span></div>
          <div class="pill"><span>Plotly</span></div><div class="pill"><span>Streamlit</span></div>
        </div>
      </div>
      <div>
        <div class="skill-cat-label">◈ WEB & BACKEND</div>
        <div class="skill-pills">
          <div class="pill"><span>Flask</span></div><div class="pill"><span>Node.js</span></div>
          <div class="pill"><span>HTML5</span></div><div class="pill"><span>CSS3</span></div>
          <div class="pill"><span>JavaScript</span></div><div class="pill"><span>MySQL</span></div>
        </div>
      </div>
      <div>
        <div class="skill-cat-label">◈ TOOLS & PLATFORMS</div>
        <div class="skill-pills">
          <div class="pill"><span>GitHub</span></div><div class="pill"><span>Anaconda</span></div>
          <div class="pill"><span>Figma</span></div><div class="pill"><span>Canva</span></div>
          <div class="pill"><span>Adobe</span></div>
        </div>
      </div>
    </div>
  </section>

  <div class="cyber-divider"></div>

  <!-- PROJECTS -->
  <section id="projects">
    <div class="sec-label">// ACTIVE DEPLOYMENTS</div>
    <div class="sec-title">PROJECTS</div>
    <div class="projects-grid">

      <div class="project-card">
        <div class="project-status ps-active"><div class="ps-dot"></div>ACTIVE</div>
        <div class="project-icon">🏫</div>
        <div class="project-title">SMART CLASSROOM MANAGER</div>
        <div class="project-desc">AI-powered classroom management system with automated attendance, behavior analysis, and performance tracking using computer vision.</div>
        <div class="project-tags">
          <span class="tag">Python</span><span class="tag">OpenCV</span><span class="tag">Flask</span><span class="tag">MySQL</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-status ps-training"><div class="ps-dot"></div>TRAINING</div>
        <div class="project-icon">🧠</div>
        <div class="project-title">NEURAL RESEARCH SUITE</div>
        <div class="project-desc">Deep learning research projects exploring CNN architectures, transfer learning, and custom model optimization techniques.</div>
        <div class="project-tags">
          <span class="tag">TensorFlow</span><span class="tag">PyTorch</span><span class="tag">Keras</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-status ps-active"><div class="ps-dot"></div>ACTIVE</div>
        <div class="project-icon">📊</div>
        <div class="project-title">DATA ANALYTICS ENGINE</div>
        <div class="project-desc">End-to-end data pipelines for cleaning, analysis, and visualization of complex datasets with interactive Power BI dashboards.</div>
        <div class="project-tags">
          <span class="tag">Pandas</span><span class="tag">R</span><span class="tag">Power BI</span><span class="tag">Plotly</span>
        </div>
      </div>

    </div>
  </section>

  <div class="cyber-divider"></div>

  <!-- CONNECT -->
  <section id="connect">
    <div class="connect-wrap">
      <div class="sec-label">// ESTABLISH CONNECTION</div>
      <div class="sec-title" style="margin-bottom:1rem">LET'S COLLABORATE</div>
      <p style="color:rgba(255,255,255,0.4);font-size:1rem;letter-spacing:1px">Open to AI/ML collabs, open-source projects & innovative ideas</p>
      <div class="social-row">
        <a href="https://www.linkedin.com/in/dhivya-shri-153441290/" class="social-btn li" target="_blank">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
          LinkedIn
        </a>
        <a href="https://instagram.com/_dhivyashrii_" class="social-btn ig" target="_blank">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="2" width="20" height="20" rx="5"/><path d="M16 11.37A4 4 0 1112.63 8 4 4 0 0116 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/></svg>
          Instagram
        </a>
        <a href="mailto:dhivyashri1385@gmail.com" class="social-btn gm">
          <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
          Gmail
        </a>
      </div>
    </div>
  </section>

  <!-- QUOTE -->
  <div class="quote-block">
    "The best way to predict the future is to <em>create it with AI.</em>"
  </div>

</main>

<footer>
  DHIVYA SHRI © 2025 &nbsp;·&nbsp; BUILT WITH INTELLIGENCE &nbsp;·&nbsp; ALL SYSTEMS OPERATIONAL
</footer>

<script>
// ── CURSOR ──
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX; my=e.clientY;
  cursor.style.left=mx+'px'; cursor.style.top=my+'px';
});
function animRing(){
  rx+=(mx-rx)*0.12; ry+=(my-ry)*0.12;
  ring.style.left=rx+'px'; ring.style.top=ry+'px';
  requestAnimationFrame(animRing);
}
animRing();
document.querySelectorAll('a,.btn,.pill,.social-btn,.stat-box,.project-card').forEach(el=>{
  el.addEventListener('mouseenter',()=>{ ring.style.width='60px'; ring.style.height='60px'; ring.style.opacity='0.4'; });
  el.addEventListener('mouseleave',()=>{ ring.style.width='40px'; ring.style.height='40px'; ring.style.opacity='1'; });
});

// ── NEURAL NETWORK CANVAS ──
const canvas = document.getElementById('neural-canvas');
const ctx = canvas.getContext('2d');
let W,H,nodes=[];
const NUM=80, CONN_DIST=160;

function resize(){ W=canvas.width=window.innerWidth; H=canvas.height=window.innerHeight; }
resize();
window.addEventListener('resize',()=>{ resize(); initNodes(); });

function initNodes(){
  nodes=[];
  for(let i=0;i<NUM;i++){
    nodes.push({
      x:Math.random()*W, y:Math.random()*H,
      vx:(Math.random()-0.5)*0.4, vy:(Math.random()-0.5)*0.4,
      r:Math.random()*2+1,
      pulse:Math.random()*Math.PI*2
    });
  }
}
initNodes();

// Mouse repulsion
let mouse={x:-9999,y:-9999};
document.addEventListener('mousemove',e=>{ mouse.x=e.clientX; mouse.y=e.clientY; });

function draw(){
  ctx.clearRect(0,0,W,H);
  const t=Date.now()*0.001;

  // Update
  nodes.forEach(n=>{
    n.pulse+=0.02;
    n.x+=n.vx; n.y+=n.vy;
    if(n.x<0||n.x>W) n.vx*=-1;
    if(n.y<0||n.y>H) n.vy*=-1;
    // Repel from mouse
    const dx=n.x-mouse.x, dy=n.y-mouse.y;
    const d=Math.sqrt(dx*dx+dy*dy);
    if(d<100){ n.vx+=dx/d*0.5; n.vy+=dy/d*0.5; }
    // Dampen speed
    const spd=Math.sqrt(n.vx*n.vx+n.vy*n.vy);
    if(spd>1.2){ n.vx*=0.98; n.vy*=0.98; }
  });

  // Connections
  for(let i=0;i<nodes.length;i++){
    for(let j=i+1;j<nodes.length;j++){
      const a=nodes[i],b=nodes[j];
      const dx=a.x-b.x, dy=a.y-b.y;
      const dist=Math.sqrt(dx*dx+dy*dy);
      if(dist<CONN_DIST){
        const alpha=(1-dist/CONN_DIST)*0.35;
        // Color shift along line
        const hue = (t*20 + i*5) % 360;
        ctx.beginPath();
        const grad=ctx.createLinearGradient(a.x,a.y,b.x,b.y);
        grad.addColorStop(0,`rgba(0,245,255,${alpha})`);
        grad.addColorStop(1,`rgba(123,47,247,${alpha})`);
        ctx.strokeStyle=grad;
        ctx.lineWidth=0.6;
        ctx.moveTo(a.x,a.y); ctx.lineTo(b.x,b.y);
        ctx.stroke();
      }
    }
  }

  // Nodes
  nodes.forEach((n,i)=>{
    const glow = 0.6+0.4*Math.sin(n.pulse);
    ctx.beginPath();
    ctx.arc(n.x,n.y,n.r*glow,0,Math.PI*2);
    const ng=ctx.createRadialGradient(n.x,n.y,0,n.x,n.y,n.r*3);
    ng.addColorStop(0,`rgba(0,245,255,${0.9*glow})`);
    ng.addColorStop(1,'rgba(0,245,255,0)');
    ctx.fillStyle=ng;
    ctx.fill();
  });

  // Pulse rings on random nodes occasionally
  requestAnimationFrame(draw);
}
draw();

// ── TYPEWRITER ──
const phrases=[
  'Building Neural Networks from Scratch 🧠',
  'Training Models → Deploying Solutions 🚀',
  'Data + Algorithms = Intelligence ⚡',
  'Smart Classroom AI Developer 🏫',
  'Open Source Contributor & Learner 🌐'
];
let pi=0,ci=0,deleting=false;
const tw=document.getElementById('typewriter');
function type(){
  const phrase=phrases[pi];
  if(!deleting){
    tw.innerHTML=phrase.slice(0,ci+1)+'<span class="type-cursor">▋</span>';
    ci++;
    if(ci===phrase.length){ deleting=true; setTimeout(type,2000); return; }
    setTimeout(type,70);
  } else {
    tw.innerHTML=phrase.slice(0,ci-1)+'<span class="type-cursor">▋</span>';
    ci--;
    if(ci===0){ deleting=false; pi=(pi+1)%phrases.length; setTimeout(type,400); return; }
    setTimeout(type,35);
  }
}
type();

// ── SCROLL REVEAL ──
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.style.opacity='1';
      e.target.style.transform='translateY(0)';
    }
  });
},{threshold:0.1});
document.querySelectorAll('.terminal-card,.stat-box,.project-card,.pill,.skill-cat-label').forEach(el=>{
  el.style.opacity='0';
  el.style.transform='translateY(30px)';
  el.style.transition='opacity 0.7s ease, transform 0.7s ease';
  observer.observe(el);
});
</script>
</body>
</html>
