<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mika Solari — Interaction & 3D Design</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,600;1,9..144,400&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0A0D12;
    --bg-alt: #10141B;
    --ink: #EDEAE2;
    --ink-dim: #8D95A1;
    --accent: #C89B4A;
    --accent-dim: #6E5A30;
    --line: #23282F;
  }
  *{ margin:0; padding:0; box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:'Inter', sans-serif;
    font-weight:400;
    overflow-x:hidden;
  }
  h1,h2,h3,.display{
    font-family:'Fraunces', serif;
    font-weight:500;
    letter-spacing:-0.01em;
    line-height:1.05;
  }
  a{ color:inherit; text-decoration:none; }
  ::selection{ background:var(--accent); color:var(--bg); }

  /* ---------- nav ---------- */
  nav{
    position:fixed; top:0; left:0; right:0; z-index:50;
    display:flex; justify-content:space-between; align-items:center;
    padding:28px clamp(24px,5vw,64px);
    mix-blend-mode:difference;
  }
  .nav-mark{ font-family:'Fraunces', serif; font-size:18px; font-style:italic; }
  .nav-links{ display:flex; gap:36px; }
  .nav-links a{
    font-size:14px; color:var(--ink); opacity:.8;
    transition:opacity .25s ease;
  }
  .nav-links a:hover{ opacity:1; }

  /* ---------- hero ---------- */
  .hero{
    position:relative;
    height:100svh;
    display:flex;
    align-items:flex-end;
    overflow:hidden;
  }
  #hero-canvas{
    position:absolute; inset:0;
    width:100%; height:100%;
    display:block;
  }
  .hero-content{
    position:relative;
    z-index:2;
    padding:0 clamp(24px,5vw,64px) clamp(48px,8vh,96px);
    max-width:820px;
    opacity:0;
    transform:translateY(24px);
    animation:rise 1.1s cubic-bezier(.22,.68,.2,1) .3s forwards;
  }
  @keyframes rise{ to{ opacity:1; transform:translateY(0); } }
  .hero-label{
    font-size:13px; color:var(--accent); margin-bottom:18px;
    display:flex; align-items:center; gap:10px;
  }
  .hero-label::before{
    content:''; width:26px; height:1px; background:var(--accent);
  }
  .hero h1{
    font-size:clamp(48px, 8vw, 108px);
    color:var(--ink);
  }
  .hero h1 em{
    font-style:italic; color:var(--accent-dim);
    -webkit-text-stroke:1px var(--accent);
    color:transparent;
  }
  .hero p{
    margin-top:22px;
    font-size:clamp(15px,1.6vw,18px);
    color:var(--ink-dim);
    max-width:44ch;
    line-height:1.6;
  }
  .scroll-cue{
    position:absolute; bottom:28px; right:clamp(24px,5vw,64px);
    font-size:12px; color:var(--ink-dim); z-index:2;
    writing-mode:vertical-rl;
    display:flex; align-items:center; gap:10px;
  }
  .scroll-cue::after{
    content:''; width:1px; height:44px; background:var(--line);
  }

  /* ---------- shared section styling ---------- */
  section{
    padding:clamp(96px,14vh,160px) clamp(24px,5vw,64px);
    border-top:1px solid var(--line);
  }
  .section-label{
    font-size:13px; color:var(--accent);
    margin-bottom:28px;
  }
  .section-head{
    display:flex; justify-content:space-between; align-items:flex-end;
    gap:32px; flex-wrap:wrap;
    margin-bottom:64px;
  }
  .section-head h2{
    font-size:clamp(32px,4.2vw,52px);
    max-width:14ch;
  }
  .section-head p{
    color:var(--ink-dim);
    max-width:36ch;
    font-size:15px;
    line-height:1.6;
  }

  /* ---------- about ---------- */
  .about{
    display:grid;
    grid-template-columns:1.3fr .9fr;
    gap:64px;
    align-items:center;
  }
  .about-text p{
    font-size:clamp(18px,2vw,24px);
    line-height:1.55;
    color:var(--ink);
    font-family:'Fraunces', serif;
    font-weight:300;
    max-width:36ch;
  }
  .about-text p + p{ margin-top:22px; color:var(--ink-dim); font-size:15px; font-family:'Inter',sans-serif; max-width:42ch; }
  .about-shape{
    position:relative;
    aspect-ratio:1/1;
    max-width:360px;
    justify-self:end;
  }
  .about-shape canvas{ width:100%; height:100%; display:block; }

  /* ---------- work ---------- */
  .work-list{ display:flex; flex-direction:column; }
  .work-row{
    display:grid;
    grid-template-columns:120px 1fr auto;
    align-items:center;
    gap:36px;
    padding:32px 0;
    border-top:1px solid var(--line);
    transition:background .3s ease;
  }
  .work-row:last-child{ border-bottom:1px solid var(--line); }
  .work-row:hover{ background:rgba(200,155,74,0.04); }
  .work-thumb{
    width:120px; height:120px;
    background:var(--bg-alt);
    border-radius:4px;
    overflow:hidden;
  }
  .work-thumb canvas{ width:100%; height:100%; display:block; }
  .work-info h3{
    font-size:clamp(22px,2.6vw,32px);
    font-weight:500;
    color:var(--ink);
  }
  .work-info p{
    margin-top:8px; color:var(--ink-dim); font-size:14px; max-width:52ch;
  }
  .work-meta{
    text-align:right; color:var(--ink-dim); font-size:13px;
    display:flex; flex-direction:column; gap:6px;
  }
  .work-meta span:first-child{ color:var(--accent); }

  /* ---------- process ---------- */
  .process{
    display:grid;
    grid-template-columns:.9fr 1.4fr;
    gap:64px;
  }
  .process-list{
    display:flex; flex-wrap:wrap; gap:14px 28px;
  }
  .process-list li{
    list-style:none;
    font-family:'Fraunces', serif;
    font-style:italic;
    font-size:clamp(20px,2.6vw,30px);
    color:var(--ink-dim);
    transition:color .25s ease;
  }
  .process-list li:hover{ color:var(--accent); }

  /* ---------- contact ---------- */
  .contact{
    display:flex; flex-direction:column; align-items:flex-start; gap:28px;
  }
  .contact h2{
    font-size:clamp(36px,6.4vw,88px);
    max-width:14ch;
  }
  .contact-link{
    font-size:clamp(16px,1.8vw,20px);
    color:var(--ink);
    padding-bottom:6px;
    border-bottom:1px solid var(--accent-dim);
    transition:border-color .25s ease, color .25s ease;
  }
  .contact-link:hover{ border-color:var(--accent); color:var(--accent); }
  .contact-socials{
    display:flex; gap:24px; margin-top:12px;
    font-size:14px; color:var(--ink-dim);
  }
  footer{
    padding:28px clamp(24px,5vw,64px);
    display:flex; justify-content:space-between;
    font-size:12px; color:var(--ink-dim);
    border-top:1px solid var(--line);
  }

  @media (max-width:820px){
    .about, .process{ grid-template-columns:1fr; }
    .about-shape{ justify-self:start; max-width:220px; }
    .work-row{ grid-template-columns:72px 1fr; }
    .work-meta{ display:none; }
    .work-thumb{ width:72px; height:72px; }
  }

  @media (prefers-reduced-motion: reduce){
    .hero-content{ animation:none; opacity:1; transform:none; }
    *{ scroll-behavior:auto !important; }
  }
</style>
</head>
<body>

<nav>
  <span class="nav-mark">Mika Solari</span>
  <div class="nav-links">
    <a href="#work">Work</a>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<section class="hero">
  <canvas id="hero-canvas"></canvas>
  <div class="hero-content">
    <div class="hero-label">interaction &amp; 3D design</div>
    <h1>Form, built<br>in <em>light.</em></h1>
    <p>I design and build spatial interfaces — geometry, material and motion assembled in the browser, for products that ask to be looked at from more than one side.</p>
  </div>
  <div class="scroll-cue">scroll</div>
</section>

<section class="about" id="about">
  <div class="about-text">
    <p>I work at the seam between design and code — sketching in Blender, then rebuilding the result as light, responsive geometry in WebGL.</p>
    <p>Six years across product studios and independent commissions, based between Bangkok and remote studios worldwide. I care about restraint: one idea, rendered precisely, outlasts a dozen effects.</p>
  </div>
  <div class="about-shape"><canvas id="about-canvas"></canvas></div>
</section>

<section id="work">
  <div class="section-head">
    <h2>Selected work</h2>
    <p>A short list of studies and commissions — each one a single geometric idea, carried through to production.</p>
  </div>
  <div class="work-list">

    <div class="work-row">
      <div class="work-thumb"><canvas data-shape="torusKnot"></canvas></div>
      <div class="work-info">
        <h3>Woven Catalogue</h3>
        <p>A product configurator built around a single continuous surface — knots and folds standing in for material choice.</p>
      </div>
      <div class="work-meta"><span>Commerce</span><span>2025</span></div>
    </div>

    <div class="work-row">
      <div class="work-thumb"><canvas data-shape="dodecahedron"></canvas></div>
      <div class="work-info">
        <h3>Faceted Archive</h3>
        <p>A spatial index for a photography archive — each facet a folder, rotated open with a glance.</p>
      </div>
      <div class="work-meta"><span>Editorial</span><span>2024</span></div>
    </div>

    <div class="work-row">
      <div class="work-thumb"><canvas data-shape="octahedron"></canvas></div>
      <div class="work-info">
        <h3>Quiet Instrument</h3>
        <p>A generative sound toy — geometry deforms with pitch, giving the ear something to watch.</p>
      </div>
      <div class="work-meta"><span>Installation</span><span>2023</span></div>
    </div>

    <div class="work-row">
      <div class="work-thumb"><canvas data-shape="icosahedron"></canvas></div>
      <div class="work-info">
        <h3>Terrain Study</h3>
        <p>A procedural landscape renderer used to storyboard a climate-data documentary.</p>
      </div>
      <div class="work-meta"><span>Research</span><span>2022</span></div>
    </div>

  </div>
</section>

<section class="process">
  <div class="section-head" style="margin-bottom:0;">
    <h2>Working set</h2>
    <p>The tools I return to, in no particular order.</p>
  </div>
  <ul class="process-list">
    <li>Three.js</li><li>GLSL</li><li>Blender</li><li>React</li><li>WebGPU</li><li>Figma</li><li>TouchDesigner</li><li>Rust</li>
  </ul>
</section>

<section class="contact" id="contact">
  <div class="section-label">get in touch</div>
  <h2>Working on something spatial? Let's talk.</h2>
  <a class="contact-link" href="mailto:hello@mikasolari.studio">hello@mikasolari.studio</a>
  <div class="contact-socials">
    <a href="#">Instagram</a>
    <a href="#">Are.na</a>
    <a href="#">GitHub</a>
  </div>
</section>

<footer>
  <span>© 2026 Mika Solari</span>
  <span>Built with Three.js</span>
</footer>

<script src="https://unpkg.com/three@0.160.0/build/three.min.js"></script>
<script>
(function(){
  const accent = 0xC89B4A;
  const accentDim = 0x6E5A30;
  const scenes = [];

  function makeRenderer(canvas, alpha){
    const r = new THREE.WebGLRenderer({ canvas, antialias:true, alpha:true });
    r.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    return r;
  }

  function wireMesh(geo, color){
    const group = new THREE.Group();
    const solid = new THREE.Mesh(
      geo,
      new THREE.MeshStandardMaterial({ color:0x10141B, metalness:0.2, roughness:0.6, transparent:true, opacity:0.55 })
    );
    const wire = new THREE.LineSegments(
      new THREE.EdgesGeometry(geo),
      new THREE.LineBasicMaterial({ color, transparent:true, opacity:0.9 })
    );
    group.add(solid, wire);
    return group;
  }

  /* ---------------- hero scene ---------------- */
  function initHero(){
    const canvas = document.getElementById('hero-canvas');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, 0.1, 100);
    camera.position.set(0, 0, 7);

    const renderer = makeRenderer(canvas);
    function size(){
      renderer.setSize(window.innerWidth, window.innerHeight);
      camera.aspect = window.innerWidth/window.innerHeight;
      camera.updateProjectionMatrix();
    }
    size();

    const key = new THREE.PointLight(0xC89B4A, 6, 30);
    key.position.set(4, 3, 5);
    const fill = new THREE.PointLight(0x2E4058, 4, 30);
    fill.position.set(-5, -2, -3);
    scene.add(key, fill, new THREE.AmbientLight(0x1a1f27, 1.2));

    const geo = new THREE.IcosahedronGeometry(2.1, 1);
    const mesh = wireMesh(geo, accent);
    scene.add(mesh);

    // scattered points for depth
    const ptGeo = new THREE.BufferGeometry();
    const count = 180;
    const pos = new Float32Array(count*3);
    for(let i=0;i<count;i++){
      pos[i*3] = (Math.random()-0.5)*14;
      pos[i*3+1] = (Math.random()-0.5)*14;
      pos[i*3+2] = (Math.random()-0.5)*14 - 4;
    }
    ptGeo.setAttribute('position', new THREE.BufferAttribute(pos,3));
    const points = new THREE.Points(ptGeo, new THREE.PointsMaterial({ color:0x3A4250, size:0.02 }));
    scene.add(points);

    let mouseX = 0, mouseY = 0;
    window.addEventListener('mousemove', (e)=>{
      mouseX = (e.clientX/window.innerWidth - 0.5);
      mouseY = (e.clientY/window.innerHeight - 0.5);
    });

    window.addEventListener('resize', size);

    scenes.push(function(t){
      mesh.rotation.y = t*0.00012 + mouseX*0.5;
      mesh.rotation.x = t*0.00007 + mouseY*0.3;
      points.rotation.y = t*0.00003;
      renderer.render(scene, camera);
    });
  }

  /* ---------------- small reusable scene for thumbnails ---------------- */
  function initSmall(canvas, geo){
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(40, 1, 0.1, 20);
    camera.position.set(0,0,4.6);
    const renderer = makeRenderer(canvas);

    function size(){
      const w = canvas.clientWidth || canvas.parentElement.clientWidth;
      renderer.setSize(w, w, false);
      camera.aspect = 1;
      camera.updateProjectionMatrix();
    }
    size();
    window.addEventListener('resize', size);

    scene.add(new THREE.AmbientLight(0x222831,1.4));
    const light = new THREE.PointLight(accent, 5, 20);
    light.position.set(3,3,4);
    scene.add(light);

    const mesh = wireMesh(geo, accent);
    scene.add(mesh);

    scenes.push(function(t){
      mesh.rotation.y = t*0.00025;
      mesh.rotation.x = t*0.00016;
      renderer.render(scene, camera);
    });
  }

  function geoFor(name){
    switch(name){
      case 'torusKnot': return new THREE.TorusKnotGeometry(1.1, 0.32, 90, 12);
      case 'dodecahedron': return new THREE.DodecahedronGeometry(1.3, 0);
      case 'octahedron': return new THREE.OctahedronGeometry(1.5, 0);
      case 'icosahedron': return new THREE.IcosahedronGeometry(1.4, 0);
      default: return new THREE.BoxGeometry(1.6,1.6,1.6);
    }
  }

  window.addEventListener('DOMContentLoaded', ()=>{
    initHero();
    initSmall(document.getElementById('about-canvas'), new THREE.TorusKnotGeometry(0.95,0.28,110,14));
    document.querySelectorAll('[data-shape]').forEach(c=>{
      initSmall(c, geoFor(c.dataset.shape));
    });

    function loop(t){
      scenes.forEach(fn => fn(t));
      requestAnimationFrame(loop);
    }
    requestAnimationFrame(loop);
  });
})();
</script>

</body>
</html>
