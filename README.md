<!doctype html>
<html lang="mn">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Төрсөн өдрийн мэнд — Захиа</title>
<style>
  :root{
    --bg:#FFF7FB;
    --accent:#FF9BCB;
    --accent-2:#FFD7EA;
    --text:#2a2a2a;
    --card:#fff;
  }
  *{box-sizing:border-box;font-family:'Helvetica Neue',Arial,sans-serif}
  body{
    margin:0;
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    background: radial-gradient(circle at 10% 20%, #fff5fb 0%, var(--bg) 35%, #f7f3ff 100%);
    color:var(--text);
    padding:32px;
  }

  .envelope-wrap{
    perspective:1200px;
    display:flex;
    align-items:flex-start;
    justify-content:center;
    min-height:420px;
  }
  .envelope {
    width:520px;
    max-width:95vw;
    height:320px;
    position:relative;
    transform-style:preserve-3d;
    transition: transform 1s cubic-bezier(.2,.9,.3,1);
  }

  .env-back{
    position:absolute; inset:0;
    background: linear-gradient(180deg,var(--accent-2),#fff);
    border-radius:10px;
    box-shadow: 0 10px 30px rgba(0,0,0,.12);
    display:flex;
    align-items:center;
    justify-content:center;
  }

  .env-flap{
    position:absolute;
    left:0; right:0;
    top:0;
    height:50%;
    transform-origin: top center;
    background: linear-gradient(180deg,var(--accent), #ffedef 60%);
    border-top-left-radius:10px;
    border-top-right-radius:10px;
    clip-path: polygon(0 0, 100% 0, 50% 100%);
    box-shadow: 0 8px 18px rgba(0,0,0,.12);
    z-index:5;
    transform: rotateX(0deg);
    transition: transform 1s cubic-bezier(.15,.9,.3,1);
  }

  .paper {
    position:absolute;
    left:50%;
    transform:translateX(-50%);
    top:36%;
    width:84%;
    height:66%;
    background: linear-gradient(180deg,#fff 0%, #fffefc 100%);
    border-radius:6px;
    padding:28px;
    box-shadow: 0 12px 30px rgba(0,0,0,.12);
    z-index:2;
    opacity:0;
    transition: all 1.2s ease;
    overflow:auto;
  }

  .open .env-flap { transform: rotateX(-180deg); }
  .open .paper { top:8%; opacity:1; }

  .paper h1{ margin:0 0 8px 0; font-size:26px; color:#c33; }
  .paper p{ margin:10px 0; line-height:1.6; color:#333; }
  .paper .signature{ margin-top:18px; font-weight:600; color:#7a3b5b }

  .confetti{
    position:absolute; inset:0;
    pointer-events:none;
  }
</style>
</head>
<body>
  <div class="envelope-wrap">
    <div class="envelope closed" id="envelope">
      <div class="env-back">
        <div style="text-align:center;">
          <div style="font-weight:700;color:#8b3b5f;font-size:18px">Happy Birthday</div>
          <div style="font-size:12px;color:#b36b8b;margin-top:6px">A special letter for you</div>
        </div>
      </div>
      <div class="env-flap"></div>
      <div class="paper">
        <h1>Kira-д,</h1>
        <p>Хөөрхөн найздаа төрсөн өдрийн баярын мэнд хүргье. 🎂</p>
        <p>Хамгийн анх стори рэплэй хийж орж ирснээс 1 жил өнгөрчээ. Нууж хаах зүйлгүйгээр хүнтэй ярилцах чөлөөтэй байх вуаа үнэхээр гоё байдаг юм байна лээ. Магадгүй хүн алсан ч чамд хэлж болохоор санагддаг шүү ахх 😂</p>
        <p>Тийм л дотно чөлөөтэй найз маань байдагт баярлалаа. Жилд 1 удаа уулздаг биш зөндөө их уулзаж хөгжилддөг болцгооё!</p>
        <p>За тэгээд найздаа хайртай шүү, сайхан баярлаарай 🥰🫶🏻🍀</p>
      </div>
    </div>
  </div>
  <div class="confetti" id="confetti-root"></div>

<script>
const env = document.getElementById('envelope');
const confettiRoot = document.getElementById('confetti-root');

window.addEventListener('load', () => {
  setTimeout(() => {
    env.classList.add('open');
    startConfetti();
  }, 1200);
});

/* confetti animation */
let confettiTimer = null;
function startConfetti(){
  confettiTimer = setInterval(()=> {
    const dot = document.createElement('div');
    const size = Math.random()*10+6;
    dot.style.width = size+'px';
    dot.style.height = size+'px';
    dot.style.position='absolute';
    dot.style.left = (Math.random()*100)+'%';
    dot.style.top = '-10px';
    const colors = ['#ff9bbf','#ffd18b','#b6f0c3','#b0d8ff','#f2b9ff'];
    dot.style.background = colors[Math.floor(Math.random()*colors.length)];
    dot.style.borderRadius='50%';
    dot.style.opacity='0.95';
    dot.style.transition='transform 2.4s linear, opacity 2.4s linear';
    confettiRoot.appendChild(dot);
    requestAnimationFrame(()=> {
      const move = window.innerHeight*0.7 + Math.random()*200;
      dot.style.transform = 'translateY('+move+'px) rotate('+(Math.random()*80-40)+'deg)';
      dot.style.opacity='0';
    });
    setTimeout(()=> dot.remove(),2400);
  },120);
}
</script>
</body>
</html>
