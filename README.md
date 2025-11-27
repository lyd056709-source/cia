<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>M-0 // ULTRA INTELLIGENCE TERMINAL</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body { margin:0; background:black; color:#00ffc8; font-family:Consolas,monospace; overflow:hidden; }
*{text-shadow:0 0 6px #00ffc8;}
#matrix{position:fixed;top:0;left:0;width:100%;height:100%;opacity:0.2;pointer-events:none;}

/* NAV BUTTONS */
#navButtons{position:fixed;top:10px;left:50%;transform:translateX(-50%);z-index:9999;display:flex;gap:12px;}
.navBtn{padding:8px 18px;background:#00ffc8;color:#000;border:none;cursor:pointer;font-weight:bold;transition:0.2s;}
.navBtn:hover{background:#00ffde;}

/* PAGES */
.page{display:none; width:100%; height:100%; padding:20px; box-sizing:border-box;}
.activePage{display:block;}

/* LOGIN */
#loginScreen{display:flex;flex-direction:column;justify-content:center;align-items:center;position:fixed;width:100%;height:100%;background:black;z-index:9999;}
#loginTitle{font-size:42px;margin-bottom:25px;letter-spacing:6px;}
#phoneInput{width:260px;padding:14px;border:1px solid #00ffc8;background:rgba(0,0,0,0.45);color:#00ffc8;font-size:18px;text-align:center;outline:none;}
#loginBtn{margin-top:20px;padding:10px 30px;background:#00ffc8;color:#000;border:none;cursor:pointer;font-size:16px;font-weight:bold;letter-spacing:2px;transition:0.2s;}
#loginBtn:hover{background:#00ffde;}

/* TERMINAL */
#terminalBox{border:1px solid #00ffc8;background:rgba(0,0,0,0.35);padding:10px;overflow-y:hidden;height:42%;width:48%;}
#terminalText{font-size:14px;line-height:1.6;}

/* CAMERAS */
#camGrid{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;margin-top:10px;}
.camBox{height:180px;border:1px solid #00ffc8;position:relative;background:rgba(0,0,0,0.25);overflow:hidden;}
.camTitle{position:absolute;top:5px;left:10px;font-weight:bold;}
.camImg{width:100%;height:100%;object-fit:cover;filter:contrast(1.3) brightness(0.65);}

/* FLASH */
#warnFlash{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,255,180,0.12);opacity:0;mix-blend-mode:screen;pointer-events:none;transition:0.1s;}

/* DASHBOARD */
.dashboardBox{display:flex;gap:20px;margin-top:20px;}
.dashboardBox > div{flex:1;border:1px solid #00ffc8;padding:10px;background:rgba(0,0,0,0.3);}

/* PAGE3 */
#page3{display:flex;flex-direction:column;gap:20px;}
#page3Content{display:flex;gap:20px;}
#page3Left{flex:1;border:1px solid #00ffd5;padding:15px;background:rgba(0,0,0,0.3);height:260px;}
#page3Right{width:280px;display:flex;flex-direction:column;gap:20px;}
#page3Right div{border:1px solid #00ffd5;padding:10px;background:rgba(0,0,0,0.3);flex:1;}

/* PAGE4 (GTA map) small adjustments */
#mapWrapper{width:100%;height:520px;border:1px solid #00ffd5;position:relative;overflow:hidden;background:#000;}
#gtaMap{position:absolute; top:0; left:0; transition:transform 0.8s ease;}
#m0Point, #soldierPoint { position:absolute; transform:translate(-50%,-50%); transition:left 0.8s ease, top 0.8s ease; border-radius:50%; box-shadow:0 0 10px; }
#m0Point{ width:18px;height:18px;background:#00ffd5; box-shadow:0 0 10px #00ffd5; }
#soldierPoint{ width:18px;height:18px;background:#00aaff; box-shadow:0 0 10px #00aaff; border:2px solid #fff; }
</style>
</head>
<body>
<canvas id="matrix"></canvas>

<!-- LOGIN -->
<div id="loginScreen">
  <div id="loginTitle">M-0 SECURE INTELLIGENCE ACCESS</div>
  <input id="phoneInput" maxlength="30" placeholder="ENTER PHONE NUMBER">
  <button id="loginBtn">ACCESS</button>
</div>

<div id="warnFlash"></div>

<!-- NAV -->
<div id="navButtons">
  <button class="navBtn" data-target="page1">PAGE 1</button>
  <button class="navBtn" data-target="page2">PAGE 2</button>
  <button class="navBtn" data-target="page3">PAGE 3</button>
  <button class="navBtn" data-target="page4">PAGE 4</button> <!-- ثابت وليس مضاف عبر سكربت -->
</div>

<!-- PAGE 1 -->
<div id="page1" class="page activePage">
  <div id="terminalBox"><div id="terminalText"></div></div>
  <div id="camGrid">
    <div class="camBox"><div class="camTitle">CAM-1</div><img class="camImg" src="IMAGE1.jpg" alt=""></div>
    <div class="camBox"><div class="camTitle">CAM-2</div><img class="camImg" src="IMAGE2.jpg" alt=""></div>
    <div class="camBox"><div class="camTitle">CAM-3</div><img class="camImg" src="IMAGE3.jpg" alt=""></div>
    <div class="camBox"><div class="camTitle">CAM-4</div><img class="camImg" src="IMAGE4.jpg" alt=""></div>
  </div>
</div>

<!-- PAGE 2 -->
<div id="page2" class="page">
  <div class="dashboardBox">
    <div>
      <b>GPS TRACKER</b>
      <div id="gpsBox" style="margin-top:10px;font-size:14px;"></div>
    </div>
    <div>
      <b>M-0 SCENARIO FEED</b>
      <div style="margin-top:10px;font-size:13px;line-height:16px;">
        &gt; M-0 detected in blackout zone.<br>&gt; Shadow signal confirmed.<br>&gt; Tunnel interference active.<br>&gt; Tracking anomaly…
      </div>
    </div>
  </div>

  <div style="margin-top:20px;">
    <b>CAMERA FEED</b>
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:15px;margin-top:10px;">
      <img src="IMAGE1.jpg" style="width:100%;height:160px;object-fit:cover;" alt="">
      <img src="IMAGE2.jpg" style="width:100%;height:160px;object-fit:cover;" alt="">
      <img src="IMAGE3.jpg" style="width:100%;height:160px;object-fit:cover;" alt="">
    </div>
  </div>
</div>

<!-- PAGE 3 -->
<div id="page3" class="page">
  <div id="page3Content">
    <div id="page3Left">
      <h3>M-0 LIVE PULSE MAP</h3>
      <div id="m0Map" style="width:100%;height:100%;background:#000;color:#00ffd5;padding:20px;"></div>
    </div>
    <div id="page3Right">
      <div>
        <h3>TARGET SIGNAL</h3>
        <div id="m0Status" style="margin-top:10px;font-size:15px;line-height:18px;"></div>
      </div>
      <div>
        <h3>SATELLITE RADAR</h3>
        <div id="satRadar" style="height:160px;background:#000;color:#00ffd5;padding:10px;"></div>
      </div>
    </div>
  </div>
</div>

<!-- PAGE 4 (GTA ocean tracking) -->
<div id="page4" class="page">
  <h2 style="text-align:center;color:#00ffd5;margin-bottom:12px;">M-0 —OCEAN TRACKING</h2>

  <div id="mapWrapper">
    <!-- file:///C:/Users/user/Pictures/%D8%AE%D8%B1%D9%8A%D8%B7%D8%A9-%D8%A7%D9%84%D8%A3%D9%82%D9%85%D8%A7%D8%B1-%D8%A7%D9%84%D8%B5%D9%86%D8%A7%D8%B9%D9%8A%D8%A9.webp -->
    <!-- اختر صورة كبيرة (مثال: 1400×1400) حتى التحريك يعمل بشكل جيد -->
    <img id="gtaMap" src="GTA5_MAP.jpg" width="1400" height="1400" alt="GTA map">

    <!-- M-0 and soldier markers -->
    <div id="m0Point"></div>
    <div id="soldierPoint"></div>
  </div>

  <div id="m0LiveStatus" style="margin-top:14px;text-align:center;color:#00ffd5;font-size:16px;"></div>
</div>

<script>
/* ------------------ MATRIX BACKDROP ------------------ */
let can=document.getElementById('matrix');let ctx=can.getContext('2d');
function resizeCanvas(){ can.width = window.innerWidth; can.height = window.innerHeight; columns = Math.floor(can.width/font); drops = Array(columns).fill(1); }
let chars="01XM0A".split('');let font=18;let columns=Math.floor(window.innerWidth/font);let drops=Array(columns).fill(1);
resizeCanvas();
window.addEventListener('resize', resizeCanvas);
function draw(){ctx.fillStyle='rgba(0,0,0,0.06)';ctx.fillRect(0,0,can.width,can.height);ctx.fillStyle='#00ffc8';ctx.font=font+'px monospace';for(let i=0;i<drops.length;i++){let text=chars[Math.floor(Math.random()*chars.length)];ctx.fillText(text,i*font,drops[i]*font);if(drops[i]*font>can.height&&Math.random()>0.975)drops[i]=0;drops[i]++;}}
setInterval(draw,35);

/* ------------------ NAVIGATION (single handler) ------------------ */
document.querySelectorAll('.navBtn').forEach(b=>{
  b.addEventListener('click', ()=> {
    const tgt = b.dataset.target;
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('activePage'));
    const el = document.getElementById(tgt);
    if(el) el.classList.add('activePage');
  });
});

/* ------------------ LOGIN ------------------ */
const requiredPhone="55667788";
let phoneInput=document.getElementById('phoneInput');
if(phoneInput){
  phoneInput.addEventListener('input', ()=> { phoneInput.value = phoneInput.value.replace(/[^0-9]/g,''); });
  document.getElementById('loginBtn').addEventListener('click', ()=> {
    if(phoneInput.value !== requiredPhone){ alert('ACCESS DENIED — INVALID NUMBER'); return; }
    document.getElementById('loginScreen').style.display='none';
  });
}

/* ------------------ TERMINAL PAGE1 ------------------ */
let termLines=["> Initializing BLACKSITE uplink…","> Routing encrypted channels…","> Fetching last known trace of M-0…","WARNING: M-0 signal unstable.","Decoding quantum residue…","Foreign interference detected.","Cross-checking intelligence nodes…","Entity M-0 classified as LEVEL-5 SHADOW.","Prediction model running…","Unstable coordinates triangulated.","Ghost signature confirmed."];
let tIndex=0;
function startTerminal(){
  let term=document.getElementById('terminalText');
  function write(){
    if(tIndex<termLines.length){ term.innerHTML += '<br>' + termLines[tIndex]; tIndex++; setTimeout(write,1200); }
  }
  write();
}
startTerminal();

/* ------------------ PAGE2 GPS ------------------ */
setInterval(()=>{
  let x=(Math.random()*180-90).toFixed(5);
  let y=(Math.random()*360-180).toFixed(5);
  let box=document.getElementById('gpsBox');
  if(box) box.innerHTML=`LAT: ${x}<br>LONG: ${y}`;
},3000);

/* ------------------ PAGE3 LIVE MAP ------------------ */
setInterval(()=>{
  let x=(Math.random()*180-90).toFixed(4);
  let y=(Math.random()*360-180).toFixed(4);
  let st=["Weak Pulse","Moderate Pulse","Strong Pulse","Shadow Spike","NULL Zone Detected"];
  let status=st[Math.floor(Math.random()*st.length)];
  const sEl = document.getElementById('m0Status'); if(sEl) sEl.innerHTML = `STATUS: ${status}`;
  const mapEl = document.getElementById('m0Map'); if(mapEl) mapEl.innerHTML = `LIVE COORD: ${x}, ${y}`;
},2500);

/* ------------------ COMMAND CENTER ------------------ */
let feedLog=[];
setInterval(()=>{
  let msgs=["M-0 crossing encrypted zone…","Thermal anomaly detected…","Ghost signal appears briefly…","Satellite relay shift — recalibrating…","Unknown interference spike…"];
  let msg=msgs[Math.floor(Math.random()*msgs.length)];
  feedLog.unshift(`> ${msg}`);
  if(feedLog.length>20) feedLog.pop();
  const sat = document.getElementById('satRadar');
  if(sat) sat.innerHTML = feedLog.join('<br>');
},1800);

/* ------------------ PAGE4: GTA OCEAN TRACKING (fixed unified) ------------------ */
/* seaPositions: coordinates on the image (px) — tune to fit your map image */
const seaPositions = [
  {x: 300,  y: 900},
  {x: 450,  y: 950},
  {x: 620,  y: 1050},
  {x: 800,  y: 1100},
  {x: 1000, y: 1200},
  {x: 1200, y: 1150},
  {x: 900,  y: 1080},
  {x: 700,  y: 980}
];

const mapImg = document.getElementById('gtaMap');
const wrapper = document.getElementById('mapWrapper');
const m0Point = document.getElementById('m0Point');
const soldierPoint = document.getElementById('soldierPoint');
const statusBox = document.getElementById('m0LiveStatus');

/* Ensure image has explicit size so calculations are stable.
   If your image is responsive, you can compute scale. Here we assume image natural size (1400x1400)
*/
function placeInitial() {
  // set map image size to its natural dimensions for predictable coordinates
  // if you use a different image size, adjust seaPositions accordingly or scale.
  mapImg.style.width = mapImg.naturalWidth + 'px';
  mapImg.style.height = mapImg.naturalHeight + 'px';
  // center map initially
  const cx = wrapper.offsetWidth / 2;
  const cy = wrapper.offsetHeight / 2;
  // place off-screen until update runs
  m0Point.style.left = '0px'; m0Point.style.top = '0px';
  soldierPoint.style.left = '0px'; soldierPoint.style.top = '0px';
}
if (mapImg.complete) placeInitial(); else mapImg.onload = placeInitial;

let diveToggle = false;
const statuses = ["Weak Pulse","Swimming","Diving","Shadow Spike","NULL SEA ZONE"];

function updateSeaMovement(){
  // choose position
  const pos = seaPositions[Math.floor(Math.random()*seaPositions.length)];
  diveToggle = !diveToggle;
  const diveOffset = diveToggle ? 15 : -15;

  // place M-0 and soldier
  m0Point.style.left = (pos.x) + 'px';
  m0Point.style.top  = (pos.y + diveOffset) + 'px';

  soldierPoint.style.left = (pos.x + 36) + 'px';
  soldierPoint.style.top  = (pos.y + diveOffset + 10) + 'px';

  // pan map by translating image so pos is centered in wrapper
  const centerX = wrapper.offsetWidth / 2;
  const centerY = wrapper.offsetHeight / 2;
  const translateX = centerX - pos.x;
  const translateY = centerY - pos.y;
  mapImg.style.transform = `translate(${translateX}px, ${translateY}px)`;

  // update status text
  statusBox.innerHTML = `STATUS: ${statuses[Math.floor(Math.random()*statuses.length)]}<br>COORD: ${Math.round(pos.x)}, ${Math.round(pos.y)}`;
}

// run every 2 seconds
setInterval(updateSeaMovement, 2000);
updateSeaMovement();

</script>
<div id="camGrid"> <div class="camBox"> <div class="camTitle">CAM-1</div> <img class="camImg" src="IMAGE1.jpg" alt=""> <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo"> </div> <div class="camBox"> <div class="camTitle">CAM-2</div> <img class="camImg" src="IMAGE2.jpg" alt=""> <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo"> </div> <div class="camBox"> <div class="camTitle">CAM-3</div> <img class="camImg" src="IMAGE3.jpg" alt=""> <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo"> </div> <div class="camBox"> <div class="camTitle">CAM-4</div> <img class="camImg" src="IMAGE4.jpg" alt=""> <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo"> </div> </div>

</body>
<body>
  <!-- كل شيء آخر مثل canvas و login و nav … -->

  <!-- آخر شيء داخل البودي -->
  <div id="camGrid">
    <div class="camBox">
      <div class="camTitle">CAM-1</div>
      <img class="camImg" src="IMAGE1.jpg" alt="">
      <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo">
    </div>
    <div class="camBox">
      <div class="camTitle">CAM-2</div>
      <img class="camImg" src="IMAGE2.jpg" alt="">
      <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo">
    </div>
    <div class="camBox">
      <div class="camTitle">CAM-3</div>
      <img class="camImg" src="IMAGE3.jpg" alt="">
      <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo">
    </div>
    <div class="camBox">
      <div class="camTitle">CAM-4</div>
      <img class="camImg" src="IMAGE4.jpg" alt="">
      <img class="camOverlay" src="6074de00-3a28-4983-9c9a-869a739bdf36.png" alt="CIA Logo">
    </div>
  </div>
</body>

</html>
