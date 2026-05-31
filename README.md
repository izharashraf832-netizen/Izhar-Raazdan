<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Izhar Raazdan</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Poppins:wght@300;400;500;600&display=swap');

  :root {
    --gold: #f5c518;
    --blue: #00d4ff;
    --dark: #050a12;
    --card-bg: rgba(255,255,255,0.04);
    --border: rgba(0,212,255,0.2);
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--dark);
    color: #fff;
    font-family: 'Poppins', sans-serif;
    overflow-x: hidden;
  }

  /* CANVAS */
  #particles { position:fixed; top:0; left:0; width:100%; height:100%; z-index:0; pointer-events:none; }

  /* NAV */
  nav {
    position: fixed; top:0; width:100%; z-index:100;
    padding: 18px 40px;
    display: flex; justify-content: space-between; align-items: center;
    background: rgba(5,10,18,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }
  .logo {
    font-family: 'Orbitron', sans-serif;
    font-size: 1.4rem;
    font-weight: 900;
    background: linear-gradient(90deg, var(--blue), var(--gold));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .nav-links { display:flex; gap:28px; list-style:none; }
  .nav-links a {
    color: rgba(255,255,255,0.7);
    text-decoration: none;
    font-size: 0.85rem;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: color 0.3s;
  }
  .nav-links a:hover { color: var(--blue); }

  /* HERO */
  .hero {
    position: relative; z-index:1;
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: center;
    text-align: center;
    padding: 100px 20px 60px;
  }
  .hero-badge {
    display: inline-block;
    border: 1px solid var(--blue);
    color: var(--blue);
    font-size: 0.75rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    padding: 6px 18px;
    border-radius: 100px;
    margin-bottom: 28px;
    animation: fadeUp 1s ease forwards;
    opacity:0;
  }
  .hero h1 {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(2.5rem, 7vw, 6rem);
    font-weight: 900;
    line-height: 1.1;
    animation: fadeUp 1s 0.2s ease forwards;
    opacity:0;
  }
  .hero h1 span {
    background: linear-gradient(90deg, var(--blue), var(--gold));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .hero-sub {
    margin-top: 20px;
    font-size: clamp(1rem, 2vw, 1.25rem);
    color: rgba(255,255,255,0.55);
    letter-spacing: 2px;
    animation: fadeUp 1s 0.4s ease forwards;
    opacity:0;
  }
  .hero-tags {
    display: flex; gap:12px; flex-wrap:wrap; justify-content:center;
    margin-top: 30px;
    animation: fadeUp 1s 0.6s ease forwards;
    opacity:0;
  }
  .tag {
    padding: 8px 18px;
    border-radius: 100px;
    font-size: 0.8rem;
    letter-spacing: 1px;
    border: 1px solid;
  }
  .tag.blue { border-color: var(--blue); color: var(--blue); background: rgba(0,212,255,0.08); }
  .tag.gold { border-color: var(--gold); color: var(--gold); background: rgba(245,197,24,0.08); }
  .hero-btns {
    margin-top: 40px; display:flex; gap:16px; flex-wrap:wrap; justify-content:center;
    animation: fadeUp 1s 0.8s ease forwards;
    opacity:0;
  }
  .btn-primary {
    padding: 14px 32px;
    background: linear-gradient(135deg, var(--blue), #0066ff);
    border: none; border-radius: 8px;
    color: #fff; font-size: 0.9rem; font-weight: 600;
    cursor: pointer; text-decoration: none;
    transition: transform 0.2s, box-shadow 0.2s;
    box-shadow: 0 0 20px rgba(0,212,255,0.3);
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 0 35px rgba(0,212,255,0.5); }
  .btn-outline {
    padding: 14px 32px;
    background: transparent;
    border: 1px solid var(--gold); border-radius: 8px;
    color: var(--gold); font-size: 0.9rem; font-weight: 600;
    cursor: pointer; text-decoration: none;
    transition: all 0.2s;
  }
  .btn-outline:hover { background: rgba(245,197,24,0.1); transform: translateY(-2px); }

  .scroll-indicator {
    position: absolute; bottom: 30px;
    display: flex; flex-direction: column; align-items: center; gap:6px;
    color: rgba(255,255,255,0.3); font-size:0.75rem; letter-spacing:2px;
    animation: bounce 2s infinite;
  }
  .scroll-indicator::after {
    content:''; width:1px; height:40px;
    background: linear-gradient(to bottom, rgba(0,212,255,0.6), transparent);
  }

  /* SECTIONS */
  section { position:relative; z-index:1; padding: 90px 40px; }
  .section-label {
    text-align:center;
    color: var(--blue);
    font-size: 0.75rem;
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 12px;
  }
  .section-title {
    text-align:center;
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(1.6rem, 3vw, 2.4rem);
    font-weight: 700;
    margin-bottom: 60px;
  }
  .section-title span { color: var(--gold); }

  /* ABOUT */
  .about-grid {
    max-width: 900px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1fr; gap: 40px;
    align-items: center;
  }
  .about-img-wrap {
    position:relative;
    border-radius: 16px;
    overflow:hidden;
  }
  .about-avatar {
    width:100%; aspect-ratio:1;
    background: linear-gradient(135deg, rgba(0,212,255,0.15), rgba(245,197,24,0.15));
    border-radius: 16px;
    border: 1px solid var(--border);
    display:flex; align-items:center; justify-content:center;
    font-size: 6rem;
  }
  .about-glow {
    position:absolute; inset:0;
    background: radial-gradient(circle at 50% 50%, rgba(0,212,255,0.1), transparent 70%);
    border-radius:16px;
  }
  .about-text h3 {
    font-family:'Orbitron',sans-serif;
    font-size:1.5rem; margin-bottom:16px;
    background: linear-gradient(90deg, #fff, var(--blue));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .about-text p { color:rgba(255,255,255,0.6); line-height:1.8; font-size:0.95rem; }
  .about-text p + p { margin-top:12px; }

  /* WHAT I COVER */
  .covers-grid {
    max-width: 1000px; margin:0 auto;
    display: grid; grid-template-columns: repeat(auto-fit, minmax(210px,1fr)); gap:24px;
  }
  .cover-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 36px 24px;
    text-align:center;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    cursor:default;
  }
  .cover-card:hover {
    transform: translateY(-8px);
    border-color: var(--blue);
    box-shadow: 0 0 30px rgba(0,212,255,0.15);
  }
  .cover-icon { font-size:2.5rem; margin-bottom:16px; }
  .cover-card h4 { font-family:'Orbitron',sans-serif; font-size:0.9rem; letter-spacing:1px; margin-bottom:10px; color: var(--blue); }
  .cover-card p { font-size:0.82rem; color:rgba(255,255,255,0.5); line-height:1.6; }

  /* STATS */
  .stats-section {
    background: linear-gradient(135deg, rgba(0,212,255,0.05), rgba(245,197,24,0.05));
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 70px 40px;
  }
  .stats-grid {
    max-width:800px; margin:0 auto;
    display:grid; grid-template-columns: repeat(auto-fit, minmax(160px,1fr)); gap:40px;
    text-align:center;
  }
  .stat-num {
    font-family:'Orbitron',sans-serif;
    font-size:2.4rem; font-weight:900;
    background: linear-gradient(90deg, var(--blue), var(--gold));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .stat-label { font-size:0.8rem; letter-spacing:2px; color:rgba(255,255,255,0.4); margin-top:6px; text-transform:uppercase; }

  /* VIDEOS */
  .videos-grid {
    max-width:1000px; margin:0 auto;
    display:grid; grid-template-columns: repeat(auto-fit, minmax(280px,1fr)); gap:24px;
  }
  .video-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 14px;
    overflow:hidden;
    transition: transform 0.3s, box-shadow 0.3s;
    cursor:pointer;
  }
  .video-card:hover { transform:translateY(-6px); box-shadow:0 20px 50px rgba(0,0,0,0.4); }
  .video-thumb {
    width:100%; aspect-ratio:16/9;
    display:flex; align-items:center; justify-content:center;
    font-size:2.5rem;
    position:relative;
  }
  .video-thumb.t1 { background: linear-gradient(135deg, #0a1628, #001a3a); }
  .video-thumb.t2 { background: linear-gradient(135deg, #0d0a1e, #1a0033); }
  .video-thumb.t3 { background: linear-gradient(135deg, #0a1a0a, #001a0d); }
  .play-btn {
    position:absolute;
    width:48px; height:48px;
    background:rgba(0,212,255,0.2);
    border:2px solid var(--blue);
    border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    font-size:1.2rem;
    transition: background 0.2s;
  }
  .video-card:hover .play-btn { background:rgba(0,212,255,0.4); }
  .video-info { padding:18px; }
  .video-info .vtag { font-size:0.7rem; color:var(--blue); letter-spacing:2px; text-transform:uppercase; margin-bottom:6px; }
  .video-info h4 { font-size:0.92rem; line-height:1.5; color:rgba(255,255,255,0.9); }

  /* CONTACT */
  .contact-wrap {
    max-width:600px; margin:0 auto; text-align:center;
  }
  .contact-wrap p { color:rgba(255,255,255,0.55); margin-bottom:40px; line-height:1.8; }
  .socials { display:flex; gap:16px; justify-content:center; flex-wrap:wrap; margin-bottom:40px; }
  .social-btn {
    display:flex; align-items:center; gap:8px;
    padding:12px 22px;
    border-radius:10px;
    border:1px solid var(--border);
    background:var(--card-bg);
    color:#fff; font-size:0.85rem;
    text-decoration:none;
    transition: all 0.2s;
  }
  .social-btn:hover { border-color:var(--blue); background:rgba(0,212,255,0.08); transform:translateY(-2px); }
  .contact-box {
    background:var(--card-bg);
    border:1px solid var(--border);
    border-radius:16px;
    padding:32px;
    text-align:left;
  }
  .contact-box input, .contact-box textarea {
    width:100%; padding:12px 16px;
    background:rgba(255,255,255,0.05);
    border:1px solid var(--border);
    border-radius:8px;
    color:#fff; font-family:'Poppins',sans-serif; font-size:0.9rem;
    margin-bottom:14px; resize:none;
    outline:none; transition: border-color 0.2s;
  }
  .contact-box input:focus, .contact-box textarea:focus { border-color:var(--blue); }
  .contact-box textarea { height:100px; }

  /* FOOTER */
  footer {
    position:relative; z-index:1;
    text-align:center; padding:30px;
    border-top:1px solid var(--border);
    color:rgba(255,255,255,0.3); font-size:0.8rem;
  }
  footer span { color:var(--blue); }

  /* GLOW LINE */
  .glow-line {
    width:80px; height:2px;
    background:linear-gradient(90deg, var(--blue), var(--gold));
    margin: 0 auto 20px;
    border-radius:2px;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(30px); }
    to { opacity:1; transform:translateY(0); }
  }
  @keyframes bounce {
    0%,100% { transform:translateY(0); }
    50% { transform:translateY(8px); }
  }

  .reveal { opacity:0; transform:translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity:1; transform:translateY(0); }

  @media(max-width:640px) {
    nav { padding:14px 20px; }
    .nav-links { display:none; }
    section { padding:70px 20px; }
    .about-grid { grid-template-columns:1fr; }
  }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<!-- NAV -->
<nav>
  <div class="logo">IZHAR RAAZDAN</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#covers">Topics</a></li>
    <li><a href="#videos">Videos</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-badge">✦ Content Creator & Digital Educator</div>
  <h1>IZHAR<br><span>RAAZDAN</span></h1>
  <p class="hero-sub">AI • TECH • CONTENT CREATION • ONLINE EARNING</p>
  <div class="hero-tags">
    <span class="tag blue">🤖 AI Tools</span>
    <span class="tag gold">💰 Online Earning</span>
    <span class="tag blue">💻 Tech Reviews</span>
    <span class="tag gold">🎬 Content Creation</span>
  </div>
  <div class="hero-btns">
    <a href="https://youtube.com" class="btn-primary" target="_blank">▶ Watch on YouTube</a>
    <a href="#contact" class="btn-outline">✉ Get in Touch</a>
  </div>
  <div class="scroll-indicator">SCROLL</div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-label">Who Am I</div>
  <div class="glow-line"></div>
  <h2 class="section-title">About <span>Me</span></h2>
  <div class="about-grid reveal">
    <div class="about-img-wrap">
      <div class="about-avatar">🎙️</div>
      <div class="about-glow"></div>
    </div>
    <div class="about-text">
      <h3>Izhar Raazdan</h3>
      <p>Main ek passionate content creator aur digital educator hoon jo AI tools, tech, aur online earning ke baare mein Urdu mein simple aur effective andaaz mein sikhata hoon.</p>
      <p>Mera mission hai ke har Pakistani aur Urdu speaking banda digital skills seekh sake aur apni life better bana sake — chahe woh AI se ho, content se ho, ya online earning se.</p>
      <p style="margin-top:16px; color:var(--blue); font-size:0.85rem; letter-spacing:1px;">🔥 Passionate about Tech & AI Education</p>
    </div>
  </div>
</section>

<!-- WHAT I COVER -->
<section id="covers">
  <div class="section-label">My Content</div>
  <div class="glow-line"></div>
  <h2 class="section-title">What I <span>Cover</span></h2>
  <div class="covers-grid">
    <div class="cover-card reveal">
      <div class="cover-icon">🤖</div>
      <h4>AI Tools</h4>
      <p>Latest AI tools aur apps ke tutorials jo aapki life aur kaam ko easy banate hain.</p>
    </div>
    <div class="cover-card reveal">
      <div class="cover-icon">💻</div>
      <h4>Tech Reviews</h4>
      <p>Technology ki duniya ke naye updates, gadgets aur software reviews.</p>
    </div>
    <div class="cover-card reveal">
      <div class="cover-icon">🎬</div>
      <h4>Content Creation</h4>
      <p>YouTube, short-form content aur digital media creation ke pro tips aur tricks.</p>
    </div>
    <div class="cover-card reveal">
      <div class="cover-icon">💰</div>
      <h4>Online Earning</h4>
      <p>Ghar baithe online paise kamane ke proven aur trusted tarikey.</p>
    </div>
  </div>
</section>

<!-- STATS -->
<div class="stats-section reveal">
  <div class="stats-grid">
    <div>
      <div class="stat-num" data-target="50">0</div>
      <div class="stat-label">Videos Published</div>
    </div>
    <div>
      <div class="stat-num" data-target="10">0</div>
      <div class="stat-label">K+ Subscribers</div>
    </div>
    <div>
      <div class="stat-num" data-target="4">0</div>
      <div class="stat-label">Content Categories</div>
    </div>
    <div>
      <div class="stat-num" data-target="100">0</div>
      <div class="stat-label">% Urdu Content</div>
    </div>
  </div>
</div>

<!-- VIDEOS -->
<section id="videos">
  <div class="section-label">My Work</div>
  <div class="glow-line"></div>
  <h2 class="section-title">Featured <span>Videos</span></h2>
  <div class="videos-grid">
    <div class="video-card reveal">
      <div class="video-thumb t1"><div class="play-btn">▶</div></div>
      <div class="video-info">
        <div class="vtag">🤖 AI Tools</div>
        <h4>Top 5 AI Tools Jo Aapki Life Change Kar Dein 2024 Mein</h4>
      </div>
    </div>
    <div class="video-card reveal">
      <div class="video-thumb t2"><div class="play-btn">▶</div></div>
      <div class="video-info">
        <div class="vtag">💰 Online Earning</div>
        <h4>Ghar Baithe Online Paise Kamane Ke 3 Asaan Tarike</h4>
      </div>
    </div>
    <div class="video-card reveal">
      <div class="video-thumb t3"><div class="play-btn">▶</div></div>
      <div class="video-info">
        <div class="vtag">🎬 Content Creation</div>
        <h4>YouTube Channel Kaise Grow Karein — Complete Guide</h4>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-label">Let's Connect</div>
  <div class="glow-line"></div>
  <h2 class="section-title">Get in <span>Touch</span></h2>
  <div class="contact-wrap reveal">
    <p>Business inquiries, collaborations, ya koi bhi sawal ke liye mujhse rabta karein. Main hamesha available hoon!</p>
    <div class="socials">
      <a href="#" class="social-btn">▶ YouTube</a>
      <a href="#" class="social-btn">📸 Instagram</a>
      <a href="#" class="social-btn">✉ Email</a>
    </div>
    <div class="contact-box">
      <input type="text" placeholder="Aapka Naam" />
      <input type="email" placeholder="Email Address" />
      <textarea placeholder="Apna message likhein..."></textarea>
      <button class="btn-primary" style="width:100%; border:none; font-family:'Poppins',sans-serif;">Send Message ✉</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p>© 2024 <span>Izhar Raazdan</span> — All Rights Reserved | Made with ❤️ for the Urdu-speaking world</p>
</footer>

<script>
// PARTICLES
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let particles = [];

function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

function Particle() {
  this.x = Math.random() * canvas.width;
  this.y = Math.random() * canvas.height;
  this.size = Math.random() * 1.5 + 0.3;
  this.speedX = (Math.random() - 0.5) * 0.4;
  this.speedY = (Math.random() - 0.5) * 0.4;
  this.opacity = Math.random() * 0.5 + 0.1;
  this.color = Math.random() > 0.5 ? '0,212,255' : '245,197,24';
}

for (let i = 0; i < 120; i++) particles.push(new Particle());

function animateParticles() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  particles.forEach(p => {
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(${p.color},${p.opacity})`;
    ctx.fill();
    p.x += p.speedX;
    p.y += p.speedY;
    if (p.x < 0 || p.x > canvas.width) p.speedX *= -1;
    if (p.y < 0 || p.y > canvas.height) p.speedY *= -1;
  });
  requestAnimationFrame(animateParticles);
}
animateParticles();

// SCROLL REVEAL
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 100);
    }
  });
}, { threshold: 0.1 });
reveals.forEach(r => observer.observe(r));

// COUNTER ANIMATION
const counters = document.querySelectorAll('.stat-num[data-target]');
const countObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const target = +e.target.dataset.target;
      let count = 0;
      const step = target / 60;
      const timer = setInterval(() => {
        count += step;
        if (count >= target) { count = target; clearInterval(timer); }
        e.target.textContent = Math.floor(count);
      }, 25);
      countObserver.unobserve(e.target);
    }
  });
}, { threshold: 0.5 });
counters.forEach(c => countObserver.observe(c));
</script>
</body>
</html>
