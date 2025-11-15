<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Happy Birthday</title>
  <style>
    body{margin:0;font-family:Inter,Arial;background:#0f1220;color:white;display:flex;align-items:center;justify-content:center;height:100vh;overflow:hidden}
    .card{background:rgba(255,255,255,0.06);padding:40px;border-radius:20px;max-width:700px;text-align:center;box-shadow:0 0 40px rgba(0,0,0,0.4)}
    h1{font-size:36px;margin-bottom:10px;background:linear-gradient(90deg,#ff7bd5,#7ab8ff);-webkit-background-clip:text;color:transparent}
    .typing{white-space:pre-wrap;font-size:18px;min-height:150px;margin-top:20px}
    .btn{margin-top:20px;padding:12px 20px;border:none;border-radius:10px;background:linear-gradient(90deg,#ff7bd5,#7ab8ff);color:#0e1020;font-weight:bold;cursor:pointer;font-size:16px}
    .popup{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(0,0,0,0.6)}
    .popup-box{background:#12182c;padding:30px;border:1px solid rgba(255,255,255,0.1);border-radius:18px;text-align:center;max-width:500px}
    .popup-box h2{font-size:28px;margin:0;background:linear-gradient(90deg,#ff7bd5,#7ab8ff);-webkit-background-clip:text;color:transparent}
    canvas{position:fixed;inset:0;pointer-events:none}
    /* Balloons */
    .balloons{position:fixed;left:0;right:0;bottom:-100px;display:flex;justify-content:center;gap:40px;pointer-events:none}
    .balloon{font-size:48px;animation:floatUp 6s infinite ease-in-out}
    @keyframes floatUp{0%{transform:translateY(0)}100%{transform:translateY(-120vh)}}

    /* Cake */
    .cake{position:fixed;bottom:20px;right:20px;font-size:60px;animation:bounce 1.5s infinite ease-in-out}
    @keyframes bounce{0%,100%{transform:translateY(0)}50%{transform:translateY(-12px)}}

    /* Sparkles */
    .sparkles{position:fixed;inset:0;pointer-events:none;background-image:radial-gradient(circle,#fff 2px,transparent 2px);background-size:80px 80px;animation:twinkle 2s infinite ease-in-out;opacity:0.5}
    @keyframes twinkle{0%,100%{opacity:0.3}50%{opacity:0.7}}

</style>
</head>
<body>

  <canvas id="confetti"></canvas>

  <div class="card">
    <h1>Happy Birthday, <span id="bname">Vanshika</span> 🎉</h1>
    <div class="typing" id="typing"></div>
    <button class="btn" id="openWish">Open Birthday Surprise</button>
  </div>

  <div class="popup" id="popup">
    <div class="popup-box">
      <h2>Many Many Happy Returns of the Day ❤️</h2>
      <p id="finalMsg" style="margin-top:10px;color:#cbd5e1"></p>
    </div>
  </div>

<script>
  const herName = "Vanshika";
  const fromName = "Kartik";
  const message = `Dear ${herName},\n\nAnother year, another reason for me to fall even more in love with you.\nYou make life brighter, softer, and so much more beautiful.\n\nWishing you endless happiness, love, and magic today. 💖`;

  document.getElementById("bname").textContent = herName;

  // typing effect
  const typingEl = document.getElementById('typing');
  function typeText(text){
    let i=0;
    function step(){
      if(i<=text.length){
        typingEl.textContent = text.slice(0,i);
        i++;
        setTimeout(step,28);
      }
    }
    step();
  }
  typeText(message);

  document.getElementById('openWish').addEventListener('click', ()=>{
    document.getElementById('popup').style.display='flex';
    document.getElementById('finalMsg').textContent = `With all my love, ${fromName}`;
    celebrate();
  });

  // confetti animation
  const canvas=document.getElementById('confetti');
  const ctx=canvas.getContext('2d');
  let W=canvas.width=innerWidth;
  let H=canvas.height=innerHeight;

  const confetti=[];
  function spawn(n){
    for(let i=0;i<n;i++){
      confetti.push({x:Math.random()*W,y:Math.random()*H,vx:(Math.random()*4)-2,vy:(Math.random()*-8),r:5+Math.random()*5,color:`hsl(${Math.random()*360} 80% 60%)`});
    }
  }

  function draw(){
    ctx.clearRect(0,0,W,H);
    confetti.forEach((p,i)=>{
      p.x+=p.vx;
      p.y+=p.vy;
      p.vy+=0.1;
      ctx.fillStyle=p.color;
      ctx.fillRect(p.x,p.y,p.r,p.r);
      if(p.y>H) confetti.splice(i,1);
    });
    requestAnimationFrame(draw);
  }
  draw();

  function celebrate(){
    spawn(150);
  }

  window.addEventListener('resize',()=>{
    W=canvas.width=innerWidth;
    H=canvas.height=innerHeight;
  });
</script>

  <!-- Balloons -->
  <div class="balloons">
    <div class="balloon">🎈</div>
    <div class="balloon">🎈</div>
    <div class="balloon">🎈</div>
  </div>

  <!-- Cake -->
  <div class="cake">🎂</div>

  <!-- Sparkles -->
  <div class="sparkles"></div>

</body>
</html>
