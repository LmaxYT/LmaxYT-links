<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
    }
    .center-content {
      position: absolute;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      color: #fff;
      text-align: center;
      font-family: sans-serif;
      z-index: 1;
    }
    .link-box {
      transition: transform 0.2s;
      cursor: pointer;
    }
    .link-box:hover {
      transform: scale(1.07);
      box-shadow: 0 4px 24px #0008;
    }
  </style>
</head>
<body>
  <canvas id="bg"></canvas>
  <script>
    // Schwarzer Hintergrund mit weißen Streifen, die bei Hover größer werden
    const canvas = document.getElementById('bg');
    const ctx = canvas.getContext('2d');
    let width = window.innerWidth;
    let height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
    window.addEventListener('resize', () => {
      width = window.innerWidth;
      height = window.innerHeight;
      canvas.width = width;
      canvas.height = height;
    });
    const stripeCount = 12;
    const stripes = [];
    const normalThickness = 8;
    const hoverThickness = 32;
    // Streifen gleichmäßig verteilen
    for (let i = 0; i < stripeCount; i++) {
      let y = ((i + 1) * height) / (stripeCount + 1);
      stripes.push({ y, thickness: normalThickness });
    }
    let mouseY = -100;
    canvas.addEventListener('mousemove', e => {
      mouseY = e.clientY;
    });
    canvas.addEventListener('mouseleave', () => {
      mouseY = -100;
    });
    function draw() {
      ctx.clearRect(0, 0, width, height);
      ctx.save();
      ctx.fillStyle = "#111";
      ctx.fillRect(0, 0, width, height);
      ctx.restore();
      for (let i = 0; i < stripeCount; i++) {
        let stripe = stripes[i];
        // Prüfen, ob Maus in der Nähe des Streifens
        let isHover = Math.abs(mouseY - stripe.y) < stripe.thickness * 2;
        let targetThickness = isHover ? hoverThickness : normalThickness;
        // Smooth animation
        stripe.thickness += (targetThickness - stripe.thickness) * 0.18;
        ctx.beginPath();
        ctx.moveTo(0, stripe.y);
        ctx.lineTo(width, stripe.y);
        ctx.strokeStyle = "#fff";
        ctx.lineWidth = stripe.thickness;
        ctx.shadowColor = "#fff";
        ctx.shadowBlur = isHover ? 16 : 0;
        ctx.stroke();
        ctx.shadowBlur = 0;
      }
      requestAnimationFrame(draw);
    }
    draw();
  </script>
  <div class="center-content">
    <h1 style="font-size:64px;">LmaxYT</h1> 
    <a href="https://www.youtube.com/@lmax44" style="text-decoration:none;">
      <div class="link-box" style="background:#ff0000; border:2px solid rgb(0, 0, 0); border-radius:16px; padding:18px 32px; margin-top:18px; margin-bottom:18px; color:#fff;">
        <span style="font-size:23px;">Youtube</span>
      </div>
    </a>
    <a href="https://www.tiktok.com/@lmaxyt0" style="text-decoration:none;">
      <div class="link-box" style="background:#000000; border:2px solid rgb(0, 0, 0); border-radius:16px; padding:18px 32px; margin-top:18px; color:#fff;">
        <span style="font-size:22px;">TikTok</span>
      </div>
    </a>
    <a href="https://discord.gg/etEDF2yT" style="text-decoration:none;">
      <div class="link-box" style="background:#0000ff; border:2px solid rgb(0, 0, 0); border-radius:16px; padding:18px 32px; margin-top:18px; color:#fff;">
        <span style="font-size:22px;">Discord</span>
      </div>
    </a>
    <a href="https://www.twitch.tv/lmax_yt" style="text-decoration:none;">
      <div class="link-box" style="background:#cc00ff; border:2px solid rgb(0, 0, 0); border-radius:16px; padding:18px 32px; margin-top:18px; color:#fff;">
        <span style="font-size:22px;">Twitch</span>
      </div>
    </a>
  </div>
</body>
</html>