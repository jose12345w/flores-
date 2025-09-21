<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Perdón & Amistad — Sorpresa</title>
<style>
  :root{
    --bg-deep:#081226;
    --bg-mid:#1a2b44;
    --accent:#ffd24a; /* amarillo flor */
    --text:#fffce8;
  }
  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0;
    font-family: "Segoe UI", Arial, sans-serif;
    color:var(--text);
    background:
      radial-gradient(circle at 20% 10%, rgba(255,210,90,0.06), transparent 8%),
      radial-gradient(circle at 80% 85%, rgba(255,200,60,0.04), transparent 8%),
      linear-gradient(180deg,var(--bg-deep), var(--bg-mid));
    overflow:hidden;
  }

  /* moving light layers to get cosmic-yellow glow */
  .light-layer{
    position:fixed; inset:0; pointer-events:none; z-index:0;
    background:
      radial-gradient(circle at 10% 10%, rgba(255,235,150,0.10), transparent 6%),
      radial-gradient(circle at 90% 80%, rgba(255,200,80,0.07), transparent 6%);
    mix-blend-mode: screen;
    animation: floatLight 16s linear infinite;
  }
  @keyframes floatLight{ from{transform:translate(0,0)} to{transform:translate(-80px,-40px)} }

  /* subtle star grid */
  .stars {
    position:fixed; inset:0; z-index:0; pointer-events:none;
    background-image:
      radial-gradient(rgba(255,240,200,0.12) 1px, transparent 1px),
      radial-gradient(rgba(255,240,200,0.06) 1px, transparent 1px);
    background-size: 60px 60px, 120px 120px;
    opacity:0.18;
    animation: moveStars 40s linear infinite;
    mix-blend-mode: screen;
  }
  @keyframes moveStars{ from{background-position:0 0,0 0} to{background-position:-800px -600px,-400px -300px} }

  /* layout card */
  .stage { position:relative; width:100%; height:100vh; display:flex; align-items:center; justify-content:center; z-index:1; }
  .card{
    width:95%; max-width:980px; border-radius:14px; padding:16px; z-index:2;
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    box-shadow: 0 12px 40px rgba(0,0,0,0.6);
  }
  header.top{ display:flex; justify-content:space-between; align-items:center; gap:12px; margin-bottom:10px; }
  .logo{ display:flex; gap:10px; align-items:center; font-weight:700 }
  .badge{ width:48px; height:48px; border-radius:10px; background:linear-gradient(#fff7d6,#ffd24a); display:flex; align-items:center; justify-content:center; color:#6b3e00; font-weight:800; box-shadow:0 6px 12px rgba(0,0,0,0.2) }
  .start-btn{ background:var(--accent); color:#111; border:none; padding:10px 14px; border-radius:10px; font-weight:800; cursor:pointer; box-shadow:0 8px 18px rgba(255,200,40,0.16) }

  .main{ display:flex; gap:18px; align-items:stretch; justify-content:space-between; flex-wrap:wrap }
  .left{ flex:1 1 360px; min-width:260px }
  .title{ font-size:26px; color:var(--accent); margin-bottom:8px; text-shadow:0 6px 16px rgba(255,190,60,0.08) }
  .poem{ background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); padding:12px; border-radius:10px; box-shadow: inset 0 6px 14px rgba(0,0,0,0.18); min-height:170px }

  .lines p{ margin:8px 0; font-size:16px; opacity:0.95 }

  .right{ flex:0 1 360px; min-width:260px; display:flex; align-items:center; justify-content:center; position:relative }
  .center-flower{ width:320px; height:320px; display:flex; align-items:center; justify-content:center; position:relative }

  /* Petals animation classes */
  .petal{ fill:transparent; stroke:#b66d00; stroke-width:2.2; stroke-dasharray:900; stroke-dashoffset:900; }
  .petal.drawn{ stroke-dashoffset:0; transition: stroke-dashoffset 1s linear; }
  .petal.filled{ fill:var(--accent); transition: fill 0.6s ease; }

  /* falling wrappers */
  .falling{ position:fixed; top:-140px; width:68px; height:68px; pointer-events:none; z-index:3; will-change: transform,opacity; }
  .falling .sway{ width:100%; height:100%; display:block; transform-origin:center; animation: sway 3s ease-in-out infinite; }
  @keyframes sway{ 0%{transform:translateX(0)}50%{transform:translateX(18px)}100%{transform:translateX(0)} }

  /* fall animation uses translateY and rotate on wrapper */
  @keyframes drop{
    0%{ transform: translateY(-160vh) rotate(0deg); opacity:1 }
    80%{ opacity:1 }
    100%{ transform: translateY(120vh) rotate(720deg); opacity:0.92 }
  }

  /* overlay to ask start */
  #overlay{ position:fixed; inset:0; background:linear-gradient(180deg, rgba(2,6,23,0.66), rgba(2,6,23,0.46)); z-index:40; display:flex; align-items:center; justify-content:center; flex-direction:column; gap:12px }
  #overlay h2{ color:var(--accent); font-size:24px; margin:0 }
  #overlay p{ color:var(--text); opacity:0.95; margin:0; text-align:center; max-width:620px }

  .foot{ margin-top:12px; text-align:center; color:rgba(255,255,255,0.6); font-size:13px }

  /* responsive */
  @media (max-width:720px){
    .right{ order:2 }
    .left{ order:1 }
    .center-flower{ width:260px; height:260px }
    .falling{ width:44px; height:44px }
  }

</style>
</head>
<body>

  <div class="light-layer"></div>
  <div class="stars"></div>

  <div class="stage">
    <div class="card" role="main">
      <header class="top">
        <div class="logo"><div class="badge">🌼</div>Adopta una Joya</div>
        <div style="opacity:0.9"> • Amistad • Flores</div>
        <button id="startBtn" class="start-btn">Haz clic para tu sorpresa 🌻</button>
      </header>

      <section class="main">
        <div class="left">
          <div class="title">Para mi amiga, con cariño</div>
          <div class="poem">
            <div class="lines" id="lines"></div>
          </div>
          <div class="foot"></div>
        </div>

        <div class="right">
          <div class="center-flower" id="centerFlower">
            <!-- SVG container: JS dibuja los pétalos y anima -->
            <svg id="svgFlower" viewBox="0 0 200 200" width="280" height="280" aria-hidden="true">
              <g id="petalGroup" transform="translate(100,100)"></g>
              <circle id="centerDot" cx="100" cy="100" r="0" fill="#b45f00" opacity="0.95"></circle>
            </svg>
          </div>
        </div>
      </section>
    </div>
  </div>

  <!-- overlay until user starts -->
  <div id="overlay">
    <h2>Un regalo — Amistad</h2>
    <p>Nuestra amistad traspasa fronteras, no importa donde 
        estes, siempre seras mi mejor amiga
    </p>
    <button id="overlayBtn" class="start-btn">Empezar</button>
  </div>

  <!-- AUDIO: cambia la URL por tu mp3 (ej. Google Drive directo o nombre local 'musica.mp3') -->
  <audio id="bgAudio" preload="auto">
    <source id="audioSrc" src="flores.mp3" type="audio/mpeg">
  </audio>

<script>
/* ------------- CONFIGURAR AQUI ------------- */
/* NOMBRES DE ARCHIVOS LOCALES (pon tus fotos en la MISMA CARPETA que este index.html) */
const photoFiles = ['amigr.jpg','amigo.jpg','amirr.webp']; // reemplaza por tus fotos o deja vacío []

/* Control lluvia */
const FALL_INTERVAL_MS = 350;
const FALL_MIN = 6;
const FALL_MAX = 12;
/* ------------------------------------------- */

const overlay = document.getElementById('overlay');
const overlayBtn = document.getElementById('overlayBtn');
const startBtn = document.getElementById('startBtn');
const audioEl = document.getElementById('bgAudio');
const linesContainer = document.getElementById('lines');
const petalGroup = document.getElementById('petalGroup');
const centerDot = document.getElementById('centerDot');

const poemLines = [
  "Gracias, amiga, por tu risa y por todo,",
  "por los secretos compartidos y los planes en verano.",
  "Si alguna vez fallé con palabras o silencio, lo siento,",
  "hoy te traigo flores y perdón, y un abrazo sincero.",
  "Que nuestra amistad florezca cada día más fuerte,",
  "porque a tu lado aprendí lo que es la verdadera suerte.",
  " — gracias por ser tú."
];

/* ====== Construir flor central con pétalos elípticos ====== */
function buildCenterFlower(){
  petalGroup.innerHTML = '';
  const count = 8;
  for(let i=0;i<count;i++){
    const angle = (360/count) * i;
    const svgNS = 'http://www.w3.org/2000/svg';
    const el = document.createElementNS(svgNS,'ellipse');
    el.setAttribute('cx','0'); el.setAttribute('cy','-56'); el.setAttribute('rx','22'); el.setAttribute('ry','48');
    el.setAttribute('transform', `rotate(${angle})`);
    el.setAttribute('class','petal');
    // add slight stagger
    el.style.transition = 'stroke-dashoffset 0.9s linear';
    el.style.strokeDashoffset = '900';
    el.style.strokeDasharray = '900';
    el.style.animationDelay = (i * 0.22) + 's';
    petalGroup.appendChild(el);
    // trigger draw with timeout per petal
    setTimeout(()=>{ el.style.strokeDashoffset = '0'; }, 200 + i*220);
  }
  // fill petals slightly after draw
  setTimeout(()=>{ document.querySelectorAll('.petal').forEach(p=> p.classList.add('filled')); revealCenterDot(); }, 200 + count*220 + 500);
}

function revealCenterDot(){
  let r = 0; const target = 26;
  const id = setInterval(()=>{ r += 1.2; centerDot.setAttribute('r', r); if(r>=target) clearInterval(id); }, 18);
}

/* ===== typing poem ===== */
async function typePoem(){
  linesContainer.innerHTML = '';
  for(let i=0;i<poemLines.length;i++){
    await typeLine(poemLines[i]);
    await wait(400);
  }
}
function typeLine(text){
  return new Promise(resolve=>{
    const p = document.createElement('p'); linesContainer.appendChild(p);
    let idx=0;
    const speed = 28;
    function step(){ if(idx<=text.length){ p.textContent = text.slice(0,idx); idx++; setTimeout(step,speed); } else resolve(); }
    step();
  });
}
function wait(ms){ return new Promise(r=>setTimeout(r,ms)); }

/* ===== create falling element (flower or photo) ===== */
function createFalling(){
  const wrapper = document.createElement('div');
  wrapper.className = 'falling';
  // size
  const size = 40 + Math.random()*44;
  wrapper.style.width = size+'px'; wrapper.style.height = size+'px';
  // left position
  wrapper.style.left = Math.random()*(window.innerWidth - size) + 'px';
  // duration
  const dur = FALL_MIN + Math.random()*(FALL_MAX - FALL_MIN);
  wrapper.style.animationDuration = dur + 's';
  wrapper.style.animationName = 'drop';
  // inner sway container
  const sway = document.createElement('div'); sway.className = 'sway';
  // decide photo or svg-flower (flowers more likely)
  const usePhoto = photoFiles.length>0 && Math.random() < 0.28;
  if(usePhoto){
    const img = document.createElement('img');
    img.src = photoFiles[Math.floor(Math.random()*photoFiles.length)];
    img.style.width='100%'; img.style.height='100%'; img.style.objectFit='cover'; img.style.borderRadius='8px';
    img.onerror = ()=>{ img.style.display='none'; }; // hide if not found
    sway.appendChild(img);
  } else {
    // inline SVG flower (6 petals + center)
    const svgNS = 'http://www.w3.org/2000/svg';
    const svg = document.createElementNS(svgNS,'svg');
    svg.setAttribute('viewBox','0 0 100 100');
    svg.setAttribute('width','100%'); svg.setAttribute('height','100%');
    for(let i=0;i<6;i++){
      const pet = document.createElementNS(svgNS,'ellipse');
      pet.setAttribute('cx','50'); pet.setAttribute('cy','22'); pet.setAttribute('rx','8'); pet.setAttribute('ry','18');
      pet.setAttribute('transform',`rotate(${i*60} 50 50) translate(0,-5)`);
      pet.setAttribute('fill','#ffd24a'); pet.setAttribute('stroke','#b66d00'); pet.setAttribute('stroke-width','1');
      svg.appendChild(pet);
    }
    const c = document.createElementNS(svgNS,'circle'); c.setAttribute('cx','50'); c.setAttribute('cy','50'); c.setAttribute('r','9');
    c.setAttribute('fill','#ffda66'); c.setAttribute('stroke','#b66d00'); svg.appendChild(c);
    sway.appendChild(svg);
  }
  wrapper.appendChild(sway);
  document.body.appendChild(wrapper);
  // random cluster sometimes: spawn small group near this x
  if(Math.random()<0.18){
    for(let k=0;k<2;k++){
      setTimeout(()=>{ createTinyClusterAt(parseFloat(wrapper.style.left)); }, 120 + k*160);
    }
  }
  // remove after animation
  setTimeout(()=> wrapper.remove(), (dur + 0.6)*1000);
}

function createTinyClusterAt(leftPx){
  const count = 2 + Math.floor(Math.random()*3);
  for(let i=0;i<count;i++){
    const w = document.createElement('div'); w.className='falling';
    const sz = 24 + Math.random()*22; w.style.width=sz+'px'; w.style.height=sz+'px';
    const offset = (Math.random()*40 - 20);
    w.style.left = Math.max(6, Math.min(window.innerWidth - sz -6, leftPx + offset)) + 'px';
    const d = FALL_MIN + Math.random()*(FALL_MAX - FALL_MIN);
    w.style.animationDuration = d + 's';
    const sway = document.createElement('div'); sway.className='sway';
    // small flower svg
    const svgNS = 'http://www.w3.org/2000/svg';
    const svg = document.createElementNS(svgNS,'svg'); svg.setAttribute('viewBox','0 0 100 100');
    svg.setAttribute('width','100%'); svg.setAttribute('height','100%');
    for(let p=0;p<5;p++){
      const pet = document.createElementNS(svgNS,'ellipse'); pet.setAttribute('cx','50'); pet.setAttribute('cy','22'); pet.setAttribute('rx','6'); pet.setAttribute('ry','12');
      pet.setAttribute('transform',`rotate(${p*72} 50 50) translate(0,-5)`); pet.setAttribute('fill','#ffd24a'); pet.setAttribute('stroke','#b66d00'); pet.setAttribute('stroke-width','0.8');
      svg.appendChild(pet);
    }
    const c = document.createElementNS(svgNS,'circle'); c.setAttribute('cx','50'); c.setAttribute('cy','50'); c.setAttribute('r','6'); c.setAttribute('fill','#ffda66'); c.setAttribute('stroke','#b66d00');
    svg.appendChild(c);
    sway.appendChild(svg); w.appendChild(sway); document.body.appendChild(w);
    setTimeout(()=> w.remove(), (d+0.6)*1000);
  }
}

/* start the falling interval */
let fallTimer = null;
function startFalling(){
  if(fallTimer) return;
  createFalling(); // immediate
  fallTimer = setInterval(createFalling, FALL_INTERVAL_MS);
}

/* main starter: audio, poem, flower drawing and fall */
function startExperience(){
  overlay.style.display = 'none';
  // play audio (user interaction allowed)
  if(audioEl) audioEl.play().catch(()=>{ /* ignore */ });
  // build and show center flower
  buildCenterFlower();
  // type poem
  typePoem();
  // begin fall
  startFalling();
}

overlayBtn.addEventListener('click', startExperience);
startBtn.addEventListener('click', startExperience);

/* allow Enter key */
document.addEventListener('keydown', e => { if(e.key==='Enter') startExperience(); });

/* ensure audio source can be changed by user later */
document.getElementById('audioSrc').src = document.getElementById('audioSrc').src; // no-op to ensure element exists

</script>
</body>
</html>
