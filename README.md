<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thunyakorn Piamanboontee — 3D Product Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #060605;
    --bg-alt: #0E0D0A;
    --tile: #0C0B08;
    --ink: #F4F0E4;
    --ink-dim: #948C7B;
    --gold: #E8B84B;
    --gold-dim: #7A6329;
    --line: #201C13;
  }
  *{ margin:0; padding:0; box-sizing:border-box; }
  html{ scroll-behavior:smooth; }
  body{
    background:var(--bg);
    color:var(--ink);
    font-family:'Inter', sans-serif;
    overflow-x:hidden;
  }
  h1,h2,h3,.display{
    font-family:'Space Grotesk', sans-serif;
    font-weight:600;
    letter-spacing:-0.01em;
    line-height:1;
  }
  a{ color:inherit; text-decoration:none; }
  ::selection{ background:var(--gold); color:#000; }

  /* ---------- nav ---------- */
  nav{
    position:fixed; top:0; left:0; right:0; z-index:60;
    display:flex; justify-content:space-between; align-items:center;
    padding:24px clamp(20px,4.5vw,56px);
    mix-blend-mode:difference;
  }
  .nav-mark{ font-family:'Space Grotesk', sans-serif; font-weight:600; font-size:15px; }
  .nav-mark span{ color:var(--gold); }
  .nav-links{ display:flex; gap:32px; }
  .nav-links a{ font-size:13px; color:var(--ink); opacity:.75; transition:opacity .25s ease; }
  .nav-links a:hover{ opacity:1; color:var(--gold); }

  /* ---------- hero ---------- */
  .hero{
    position:relative;
    height:100svh;
    overflow:hidden;
    border-bottom:1px solid var(--line);
  }
  #hero-canvas{ position:absolute; inset:0; width:100%; height:100%; display:block; }
  .hero-vignette{
    position:absolute; inset:0; pointer-events:none;
    background:
      radial-gradient(ellipse 60% 50% at 50% 55%, rgba(6,6,5,0) 0%, rgba(6,6,5,0.55) 60%, rgba(6,6,5,0.95) 100%),
      linear-gradient(180deg, rgba(6,6,5,0.55) 0%, rgba(6,6,5,0.05) 22%, rgba(6,6,5,0.15) 70%, rgba(6,6,5,0.9) 100%);
  }

  .hero-top{
    position:absolute; top:0; left:0; right:0; z-index:3;
    display:flex; justify-content:space-between; align-items:flex-start;
    padding:96px clamp(20px,4.5vw,56px) 0;
    opacity:0; animation:fadeIn 1s ease .2s forwards;
  }
  .hero-id{ font-size:14px; color:var(--ink-dim); letter-spacing:.02em; }
  .hero-id b{ color:var(--ink); font-weight:600; }
  .hero-year{
    font-family:'Space Grotesk', sans-serif;
    font-size:clamp(34px,5vw,58px);
    font-weight:700;
    color:transparent;
    -webkit-text-stroke:1px var(--gold-dim);
  }

  .hero-title{
    position:absolute; left:0; right:0; top:50%; transform:translateY(-46%);
    z-index:2;
    text-align:center;
    font-size:clamp(72px, 15vw, 220px);
    color:var(--ink);
    white-space:nowrap;
    opacity:0; animation:fadeIn 1.1s ease .4s forwards;
  }
  .hero-title .thin{
    -webkit-text-stroke:1px var(--ink);
    color:transparent;
  }

  .hero-bottom{
    position:absolute; bottom:0; left:0; right:0; z-index:3;
    display:flex; justify-content:space-between; align-items:flex-end;
    padding:0 clamp(20px,4.5vw,56px) 44px;
    opacity:0; animation:fadeIn 1s ease .6s forwards;
  }
  .hero-cta{
    display:inline-flex; align-items:center; gap:10px;
    font-size:14px; color:var(--ink);
    padding:14px 22px;
    border:1px solid rgba(244,240,228,0.2);
    border-radius:100px;
    backdrop-filter:blur(6px);
    background:rgba(255,255,255,0.03);
    transition:border-color .25s ease, background .25s ease;
  }
  .hero-cta:hover{ border-color:var(--gold); background:rgba(232,184,75,0.08); }
  .hero-cta svg{ width:14px; height:14px; transform:rotate(-45deg); }

  .hero-replay{
    width:46px; height:46px; border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    border:1px solid rgba(244,240,228,0.2);
    background:rgba(255,255,255,0.03);
    cursor:pointer;
    transition:border-color .25s ease, transform .5s ease;
  }
  .hero-replay:hover{ border-color:var(--gold); }
  .hero-replay.spin svg{ animation:spin .7s ease; }
  .hero-replay svg{ width:18px; height:18px; stroke:var(--ink); }
  @keyframes spin{ to{ transform:rotate(180deg); } }
  @keyframes fadeIn{ from{ opacity:0; transform:translateY(10px);} to{ opacity:1; transform:translateY(0);} }
  .hero-top.opacity-fix, .hero-bottom.opacity-fix{ transform:none; }

  /* ---------- sections ---------- */
  section{ padding:clamp(84px,12vh,140px) clamp(20px,4.5vw,56px); border-top:1px solid var(--line); }
  .section-label{ font-size:13px; color:var(--gold); margin-bottom:24px; }
  .section-head{
    display:flex; justify-content:space-between; align-items:flex-end;
    gap:32px; flex-wrap:wrap; margin-bottom:52px;
  }
  .section-head h2{ font-size:clamp(28px,3.8vw,46px); max-width:16ch; }
  .section-head p{ color:var(--ink-dim); max-width:38ch; font-size:14.5px; line-height:1.6; }

  /* ---------- about ---------- */
  .about{ display:grid; grid-template-columns:1.3fr .9fr; gap:60px; align-items:center; }
  .about-text p{ font-size:clamp(17px,1.9vw,22px); line-height:1.55; color:var(--ink); max-width:38ch; }
  .about-text p + p{ margin-top:20px; color:var(--ink-dim); font-size:14.5px; max-width:44ch; font-weight:400; }
  .about-shape{ position:relative; aspect-ratio:1/1; max-width:320px; justify-self:end; }
  .about-shape canvas{ width:100%; height:100%; display:block; }

  /* ---------- bento work grid ---------- */
  .bento{
    display:grid;
    grid-template-columns:repeat(6, 1fr);
    grid-template-rows:repeat(4, 150px);
    gap:2px;
    background:var(--line);
    border:1px solid var(--line);
  }
  .bento-item{
    position:relative;
    background:var(--tile);
    overflow:hidden;
  }
  .bento-item canvas{ position:absolute; inset:0; width:100%; height:100%; display:block; }
  .b-gem{ grid-column:1 / 4; grid-row:1 / 3; }
  .b-bottle{ grid-column:4 / 6; grid-row:1 / 3; }
  .b-console{ grid-column:6 / 7; grid-row:1 / 3; }
  .b-capsule{ grid-column:1 / 3; grid-row:3 / 5; }
  .b-rover{ grid-column:3 / 5; grid-row:3 / 5; }
  .b-gold{ grid-column:5 / 7; grid-row:3 / 5; }

  .b-chip{
    position:absolute; top:14px; left:14px; z-index:2;
    font-size:10px; letter-spacing:.05em;
    color:var(--ink-dim);
    border:1px solid rgba(244,240,228,0.15);
    padding:4px 9px; border-radius:100px;
    background:rgba(6,6,5,0.5);
  }
  .b-label{
    position:absolute; left:16px; right:16px; bottom:14px; z-index:2;
    display:flex; justify-content:space-between; align-items:flex-end; gap:12px;
  }
  .b-label h3{ font-size:16px; font-weight:600; color:var(--ink); }
  .b-label span{ font-size:11px; color:var(--gold); white-space:nowrap; }
  .bento-item::after{
    content:'';
    position:absolute; inset:0;
    background:linear-gradient(180deg, rgba(6,6,5,0) 45%, rgba(6,6,5,0.85) 100%);
    pointer-events:none; z-index:1;
  }

  /* ---------- process ---------- */
  .process{ display:grid; grid-template-columns:.9fr 1.4fr; gap:60px; }
  .process-list{ display:flex; flex-wrap:wrap; gap:12px 28px; }
  .process-list li{
    list-style:none; font-family:'Space Grotesk', sans-serif; font-weight:500;
    font-size:clamp(18px,2.2vw,26px); color:var(--ink-dim); transition:color .25s ease;
  }
  .process-list li:hover{ color:var(--gold); }

  /* ---------- contact ---------- */
  .contact{ display:flex; flex-direction:column; align-items:flex-start; gap:24px; }
  .contact h2{ font-size:clamp(30px,5.2vw,70px); max-width:16ch; }
  .contact-link{
    font-size:clamp(15px,1.7vw,19px); color:var(--ink); padding-bottom:6px;
    border-bottom:1px solid var(--gold-dim); transition:border-color .25s ease, color .25s ease;
  }
  .contact-link:hover{ border-color:var(--gold); color:var(--gold); }
  .contact-socials{ display:flex; gap:22px; margin-top:6px; font-size:13.5px; color:var(--ink-dim); }
  .contact-socials a:hover{ color:var(--gold); }
  footer{
    padding:24px clamp(20px,4.5vw,56px); display:flex; justify-content:space-between;
    font-size:12px; color:var(--ink-dim); border-top:1px solid var(--line);
  }

  @media (max-width:900px){
    .about, .process{ grid-template-columns:1fr; }
    .about-shape{ justify-self:start; max-width:200px; }
    .bento{ grid-template-columns:1fr; grid-template-rows:none; }
    .b-gem,.b-bottle,.b-console,.b-capsule,.b-rover,.b-gold{ grid-column:1; grid-row:auto; aspect-ratio:4/3; }
    .hero-title{ font-size:clamp(48px, 17vw, 96px); }
    .hero-top{ padding-top:80px; }
  }

  @media (prefers-reduced-motion: reduce){
    *{ animation-duration:0.01ms !important; scroll-behavior:auto !important; }
  }
</style>
</head>
<body>

<nav>
  <span class="nav-mark">Thunyakorn <span>Piamanboontee</span></span>
  <div class="nav-links">
    <a href="#work">ผลงาน</a>
    <a href="#about">เกี่ยวกับ</a>
    <a href="#contact">ติดต่อ</a>
  </div>
</nav>

<section class="hero">
  <canvas id="hero-canvas"></canvas>
  <div class="hero-vignette"></div>

  <div class="hero-top">
    <div class="hero-id">Thunyakorn Piamanboontee <br><b>3D Product Artist</b></div>
    <div class="hero-year">2026</div>
  </div>

  <h1 class="hero-title">PORT<span class="thin">FOLIO</span></h1>

  <div class="hero-bottom">
    <a class="hero-cta" href="#work">
      ดูผลงานทั้งหมด
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M7 17L17 7M17 7H8M17 7V16"/></svg>
    </a>
    <div class="hero-replay" id="replay-btn" title="สุ่มมุมมองใหม่">
      <svg viewBox="0 0 24 24" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"><path d="M21 12a9 9 0 1 1-3-6.7M21 3v6h-6"/></svg>
    </div>
  </div>
</section>

<section class="about" id="about">
  <div class="about-text">
    <p>ผมออกแบบและขึ้นโมเดล 3 มิติให้กับผลิตภัณฑ์ ตั้งแต่ของใช้ในชีวิตประจำวันไปจนถึงอุปกรณ์ไซไฟ เน้นพื้นผิวและแสงที่ให้ความรู้สึกพรีเมียม</p>
    <p>ทำงานด้วย Blender เป็นหลัก ตั้งแต่บล็อกฟอร์มไปจนถึงจัดแสงเรนเดอร์ ก่อนนำไปพัฒนาต่อเป็นวัตถุที่เคลื่อนไหวได้จริงบนเว็บด้วย Three.js</p>
  </div>
  <div class="about-shape"><canvas id="about-canvas"></canvas></div>
</section>

<section id="work">
  <div class="section-head">
    <h2>ผลิตภัณฑ์ 3 มิติที่ผ่านมา</h2>
    <p>ผลงานสร้างวัตถุและผลิตภัณฑ์ 3 มิติ คัดเลือกจากงานสตูดิโอและงานทดลองส่วนตัว</p>
  </div>

  <div class="bento">
    <div class="bento-item b-gem">
      <canvas data-shape="gem"></canvas>
      <span class="b-chip">3D · Render</span>
      <div class="b-label"><h3>อัญมณีหรู</h3><span>Product Study · 2026</span></div>
    </div>
    <div class="bento-item b-bottle">
      <canvas data-shape="bottle"></canvas>
      <span class="b-chip">3D · Render</span>
      <div class="b-label"><h3>ขวดน้ำหอม</h3><span>Packaging · 2025</span></div>
    </div>
    <div class="bento-item b-console">
      <canvas data-shape="console"></canvas>
      <span class="b-chip">3D</span>
      <div class="b-label"><h3>คอมพิวเตอร์เรโทร</h3><span>Prop · 2025</span></div>
    </div>
    <div class="bento-item b-capsule">
      <canvas data-shape="capsule"></canvas>
      <span class="b-chip">3D · Render</span>
      <div class="b-label"><h3>ยานสำรวจ</h3><span>Sci-fi · 2024</span></div>
    </div>
    <div class="bento-item b-rover">
      <canvas data-shape="rover"></canvas>
      <span class="b-chip">3D · Render</span>
      <div class="b-label"><h3>โรเวอร์สำรวจ</h3><span>Vehicle · 2024</span></div>
    </div>
    <div class="bento-item b-gold">
      <canvas data-shape="gold"></canvas>
      <span class="b-chip">3D · Render</span>
      <div class="b-label"><h3>แท่งทองคำ</h3><span>Material Study · 2023</span></div>
    </div>
  </div>
</section>

<section class="process">
  <div class="section-head" style="margin-bottom:0;">
    <h2>เครื่องมือที่ใช้</h2>
    <p>ซอฟต์แวร์และเทคนิคที่ใช้ประจำในงานผลิตภัณฑ์ 3 มิติ</p>
  </div>
  <ul class="process-list">
    <li>Blender</li><li>Three.js</li><li>WebGL</li><li>Substance Painter</li><li>Cinema 4D</li><li>Figma</li>
  </ul>
</section>

<section class="contact" id="contact">
  <div class="section-label">ติดต่องาน</div>
  <h2>สนใจงานออกแบบผลิตภัณฑ์ 3 มิติ ทักมาคุยกันได้เลย</h2>
  <a class="contact-link" href="mailto:hello@thunyakorn.studio">hello@thunyakorn.studio</a>
  <div class="contact-socials">
    <a href="#">Instagram</a>
    <a href="#">Behance</a>
    <a href="#">ArtStation</a>
  </div>
</section>

<footer>
  <span>© 2026 Thunyakorn Piamanboontee</span>
  <span>สร้างด้วย Three.js</span>
</footer>

<script src="https://unpkg.com/three@0.160.0/build/three.min.js"></script>
<script>
(function(){
  const GOLD = 0xE8B84B;
  const GOLD_DIM = 0x7A6329;
  const scenes = [];

  function renderer(canvas){
    const r = new THREE.WebGLRenderer({ canvas, antialias:true, alpha:true });
    r.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    return r;
  }

  function facetMat(opacity){
    return new THREE.MeshStandardMaterial({
      color:0x0A0906, flatShading:true, metalness:0.35, roughness:0.3,
      transparent:true, opacity: opacity!==undefined?opacity:0.9,
      emissive:0x1C1508, emissiveIntensity:0.35
    });
  }
  function edgeMat(color, opacity){
    return new THREE.LineBasicMaterial({ color, transparent:true, opacity: opacity!==undefined?opacity:0.95 });
  }
  function facetMesh(geo, color, opacity){
    const g = new THREE.Group();
    g.add(new THREE.Mesh(geo, facetMat(opacity)));
    g.add(new THREE.LineSegments(new THREE.EdgesGeometry(geo), edgeMat(color)));
    return g;
  }

  /* ---------------- hero: centerpiece gem in a soft studio void ---------------- */
  function initHero(){
    const canvas = document.getElementById('hero-canvas');
    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x060605, 0.05);
    const camera = new THREE.PerspectiveCamera(42, window.innerWidth/window.innerHeight, 0.1, 100);
    camera.position.set(0, 0.4, 8);

    const r = renderer(canvas);
    function size(){
      r.setSize(window.innerWidth, window.innerHeight);
      camera.aspect = window.innerWidth/window.innerHeight;
      camera.updateProjectionMatrix();
    }
    size();
    window.addEventListener('resize', size);

    scene.add(new THREE.AmbientLight(0x14100a, 1.3));
    const key = new THREE.PointLight(GOLD, 10, 30);
    key.position.set(4, 4, 6);
    const rim = new THREE.PointLight(0x2a3550, 6, 30);
    rim.position.set(-5, -2, -4);
    scene.add(key, rim);

    const gemGeo = new THREE.IcosahedronGeometry(2.3, 1);
    const gem = facetMesh(gemGeo, GOLD, 0.7);
    scene.add(gem);

    // orbiting fragments for depth and motion
    const frags = new THREE.Group();
    for(let i=0;i<10;i++){
      const s = 0.12 + Math.random()*0.22;
      const f = facetMesh(new THREE.OctahedronGeometry(s,0), i%3===0?GOLD:GOLD_DIM, 0.6);
      const a = (i/10) * Math.PI*2;
      const rad = 3.6 + Math.random()*1.6;
      f.position.set(Math.cos(a)*rad, (Math.random()-0.5)*2.4, Math.sin(a)*rad - 1);
      f.userData.a = a; f.userData.rad = rad; f.userData.speed = 0.00006 + Math.random()*0.00008;
      frags.add(f);
    }
    scene.add(frags);

    let mouseX=0, mouseY=0, targetSpeed=1;
    window.addEventListener('mousemove', e=>{
      mouseX = e.clientX/window.innerWidth - 0.5;
      mouseY = e.clientY/window.innerHeight - 0.5;
    });

    const replayBtn = document.getElementById('replay-btn');
    replayBtn.addEventListener('click', ()=>{
      replayBtn.classList.add('spin');
      targetSpeed = 6;
      setTimeout(()=>{ replayBtn.classList.remove('spin'); targetSpeed = 1; }, 650);
    });

    scenes.push(function(t, dt){
      gem.rotation.y = t*0.00018*targetSpeed + mouseX*0.6;
      gem.rotation.x = t*0.00010*targetSpeed + mouseY*0.35;
      frags.children.forEach(f=>{
        f.userData.a += f.userData.speed*dt*targetSpeed;
        f.position.x = Math.cos(f.userData.a)*f.userData.rad;
        f.position.z = Math.sin(f.userData.a)*f.userData.rad - 1;
        f.rotation.y += 0.0006*dt*targetSpeed;
      });
      r.render(scene, camera);
    });
  }

  /* ---------------- reusable small scene ---------------- */
  function initSmall(canvas, build){
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(38, 1, 0.1, 30);
    camera.position.set(2.4, 1.6, 4.4);
    camera.lookAt(0,0,0);
    const r = renderer(canvas);

    function size(){
      const rect = canvas.getBoundingClientRect();
      const w = Math.max(rect.width, 1), h = Math.max(rect.height, 1);
      r.setSize(w, h, false);
      camera.aspect = w/h;
      camera.updateProjectionMatrix();
    }
    size();
    window.addEventListener('resize', size);

    scene.add(new THREE.AmbientLight(0x1a140a, 1.5));
    const light = new THREE.PointLight(GOLD, 7, 22);
    light.position.set(3,4,4);
    scene.add(light);
    const rim = new THREE.PointLight(0x3a4560, 3, 22);
    rim.position.set(-3,-1,-3);
    scene.add(rim);

    const group = new THREE.Group();
    build(group);
    scene.add(group);

    scenes.push(function(t){
      group.rotation.y = t*0.00022;
      r.render(scene, camera);
    });
  }

  function addPart(group, geo, color, opacity, pos, rot, scale){
    const m = facetMesh(geo, color, opacity);
    if(pos) m.position.set(pos[0],pos[1],pos[2]);
    if(rot) m.rotation.set(rot[0],rot[1],rot[2]);
    if(scale) m.scale.set(scale[0],scale[1],scale[2]);
    group.add(m);
    return m;
  }

  const builders = {
    gem: (g)=>{ addPart(g, new THREE.IcosahedronGeometry(1.5,0), GOLD, 0.85); },

    bottle: (g)=>{
      addPart(g, new THREE.CylinderGeometry(0.85,1.0,1.9,6), GOLD, 0.85, [0,-0.3,0]);
      addPart(g, new THREE.CylinderGeometry(0.32,0.5,0.7,6), GOLD_DIM, 0.85, [0,1.0,0]);
      addPart(g, new THREE.SphereGeometry(0.36,6,4), GOLD, 0.9, [0,1.55,0]);
    },

    console: (g)=>{
      addPart(g, new THREE.BoxGeometry(2.0,1.5,1.5), GOLD_DIM, 0.85, [0,0.2,0]);
      addPart(g, new THREE.BoxGeometry(1.5,1.0,0.15), GOLD, 0.9, [0,0.35,0.78]);
      addPart(g, new THREE.BoxGeometry(1.9,0.15,1.3), GOLD_DIM, 0.85, [0,-0.62,0.1], null, null);
    },

    capsule: (g)=>{
      addPart(g, new THREE.ConeGeometry(0.55,1.6,6), GOLD, 0.85, [0,0,0], [0,0,Math.PI/2]);
      addPart(g, new THREE.CylinderGeometry(0.55,0.55,0.9,6), GOLD_DIM, 0.85, [0.7,0,0], [0,0,Math.PI/2]);
      addPart(g, new THREE.ConeGeometry(0.55,0.9,6), GOLD, 0.85, [1.55,0,0], [0,0,-Math.PI/2]);
    },

    rover: (g)=>{
      addPart(g, new THREE.BoxGeometry(2.2,0.8,1.3), GOLD_DIM, 0.85, [0,0.35,0]);
      addPart(g, new THREE.BoxGeometry(1.0,0.5,1.0), GOLD, 0.9, [0,0.95,0]);
      const wheelGeo = new THREE.TorusGeometry(0.42,0.2,5,7);
      [[-0.9,0,0.75],[0.9,0,0.75],[-0.9,0,-0.75],[0.9,0,-0.75]].forEach(p=>{
        addPart(g, wheelGeo, GOLD, 0.85, p, [Math.PI/2,0,0]);
      });
    },

    gold: (g)=>{
      const barGeo = new THREE.BoxGeometry(1.5,0.55,0.85);
      const positions = [[-0.8,0.3,0],[0.8,0.3,0.05],[0,0.3,-0.85],[-0.4,-0.3,-0.4],[0.6,-0.3,-0.4]];
      positions.forEach((p,i)=> addPart(g, barGeo, i%2===0?GOLD:GOLD_DIM, 0.9, p, [0,i*0.15,0]));
    }
  };

  window.addEventListener('DOMContentLoaded', ()=>{
    initHero();
    initSmall(document.getElementById('about-canvas'), (g)=> addPart(g, new THREE.DodecahedronGeometry(1.1,0), GOLD, 0.85));
    document.querySelectorAll('[data-shape]').forEach(c=>{
      const fn = builders[c.dataset.shape];
      if(fn) initSmall(c, fn);
    });

    let lastT = performance.now();
    function loop(t){
      const dt = t - lastT;
      lastT = t;
      scenes.forEach(fn => fn(t, dt));
      requestAnimationFrame(loop);
    }
    requestAnimationFrame(loop);
  });
})();
</script>

</body>
</html>
