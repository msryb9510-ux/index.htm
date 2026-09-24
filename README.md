<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>A Beautiful Responsive Rose 🌹</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body, html {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background-color: #050505;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>

<canvas id="canvas"></canvas>

<script>
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener('resize', resize);

  let progress = 0;
  const maxProgress = 1.0;

  function drawRose() {
    const cx = canvas.width / 2;
    // ضبط الموضع الرأسي ليكون متناسقاً تماماً في منتصف أي شاشة
    const cy = canvas.height * 0.52;
    
    // المقياس الديناميكي لتتناسب الوردة تلقائياً مع حجم الشاشة بالكامل
    const scale = Math.min(canvas.width, canvas.height) / 420;

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // 1. رسم الساق والأوراق
    if (progress > 0.05) {
      ctx.save();
      ctx.translate(cx, cy);
      
      // الساق
      ctx.beginPath();
      ctx.moveTo(0, 20 * scale);
      ctx.bezierCurveTo(-15 * scale, 140 * scale, 18 * scale, 260 * scale, 0, 360 * scale);
      ctx.lineWidth = Math.max(4, 9 * scale);
      ctx.strokeStyle = "#1b5e20";
      ctx.shadowColor = "rgba(27, 94, 32, 0.5)";
      ctx.shadowBlur = 12;
      ctx.stroke();

      // الورقة اليسرى
      if (progress > 0.18) {
        ctx.beginPath();
        ctx.moveTo(-6 * scale, 150 * scale);
        ctx.bezierCurveTo(-100 * scale, 100 * scale, -130 * scale, 190 * scale, -6 * scale, 210 * scale);
        ctx.fillStyle = "#2e7d32";
        ctx.shadowColor = "rgba(46, 125, 50, 0.4)";
        ctx.shadowBlur = 10;
        ctx.fill();
      }

      // الورقة اليمنى
      if (progress > 0.28) {
        ctx.beginPath();
        ctx.moveTo(6 * scale, 210 * scale);
        ctx.bezierCurveTo(100 * scale, 160 * scale, 130 * scale, 250 * scale, 6 * scale, 270 * scale);
        ctx.fillStyle = "#1b5e20";
        ctx.fill();
      }
      ctx.restore();
    }

    // 2. رسم الوردة الحمراء بملء الشاشة بتفاصيل مخملية
    if (progress > 0.08) {
      ctx.save();
      ctx.translate(cx, cy - 80 * scale);

      const petalCount = 1500;
      const currentPetals = Math.floor(petalCount * Math.min(progress, 1));

      for (let i = 0; i < currentPetals; i++) {
        const theta = i * 0.08;
        const r = (210 * scale) * Math.pow(Math.sin(theta * 0.45), 2) * (1 - 0.18 * Math.cos(theta * 3));
        
        const x = r * Math.cos(theta);
        const y = -r * Math.sin(theta) * 0.82 + (theta * 1.6 * scale);

        // تدرج أحمر مخملي عميق
        const red = Math.floor(215 + 40 * Math.sin(i * 0.04));
        const green = Math.floor(5 + 15 * Math.sin(i * 0.02));
        const blue = Math.floor(20 + 25 * Math.cos(i * 0.03));

        ctx.fillStyle = `rgb(${red}, ${green}, ${blue})`;
        ctx.beginPath();
        ctx.arc(x, y, (10 - (i / petalCount) * 7.5) * scale, 0, Math.PI * 2);
        ctx.fill();
      }
      ctx.restore();
    }

    if (progress < maxProgress) {
      progress += 0.007;
      requestAnimationFrame(drawRose);
    }
  }

  drawRose();
</script>
</body>
</html>
