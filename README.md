<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>A Beautiful Elegant Rose 🌹</title>
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
      background-color: #000000;
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

  let t = 0;

  function draw() {
    ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    const cx = canvas.width / 2;
    const cy = canvas.height / 2 + 40;
    const scale = Math.min(canvas.width, canvas.height) / 360;

    // 1. رسم الساق والأوراق بنعومة
    ctx.save();
    ctx.translate(cx, cy);

    ctx.beginPath();
    ctx.moveTo(0, 10 * scale);
    ctx.bezierCurveTo(-10 * scale, 120 * scale, 15 * scale, 220 * scale, 0, 300 * scale);
    ctx.lineWidth = 6 * scale;
    ctx.strokeStyle = "#1b5e20";
    ctx.stroke();

    // ورقة يمين
    ctx.beginPath();
    ctx.moveTo(5 * scale, 140 * scale);
    ctx.bezierCurveTo(80 * scale, 100 * scale, 100 * scale, 180 * scale, 5 * scale, 190 * scale);
    ctx.fillStyle = "#2e7d32";
    ctx.fill();

    // ورقة يسار
    ctx.beginPath();
    ctx.moveTo(-5 * scale, 180 * scale);
    ctx.bezierCurveTo(-80 * scale, 140 * scale, -100 * scale, 220 * scale, -5 * scale, 230 * scale);
    ctx.fillStyle = "#1b5e20";
    ctx.fill();

    ctx.restore();

    // 2. رسم بتلات الوردة المخملية الحقيقية باستخدام منحنيات رياضية متناسقة
    ctx.save();
    ctx.translate(cx, cy - 60 * scale);

    for (let i = 0; i < 400; i++) {
      const angle = i * 0.1 + t;
      const r = (120 * scale) * Math.sin(angle * 0.4) * Math.cos(angle * 0.1);
      
      const x = r * Math.cos(angle);
      const y = r * Math.sin(angle) * 0.7 - (i * 0.3 * scale);

      const grad = ctx.createRadialGradient(x, y, 0, x, y, 15 * scale);
      grad.addColorStop(0, '#ff1744');
      grad.addColorStop(0.7, '#d50000');
      grad.addColorStop(1, '#880e4f');

      ctx.beginPath();
      ctx.ellipse(x, y, 14 * scale, 8 * scale, angle, 0, Math.PI * 2);
      ctx.fillStyle = grad;
      ctx.fill();
    }
    ctx.restore();

    if (t < Math.PI * 2) {
      t += 0.03;
      requestAnimationFrame(draw);
    }
  }

  draw();
</script>
</body>
</html>
