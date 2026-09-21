<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heart Animation</title>
  <style>
    body { margin: 0; background: black; display: flex; justify-content: center; align-items: center; height: 100vh; overflow: hidden; }
    canvas { background: black; }
  </style>
</head>
<body>
<canvas id="canvas"></canvas>
<script>
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const totalPoints = 320;
  let i = 0;

  function draw() {
    if (i >= totalPoints) return;
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const scale = Math.min(canvas.width, canvas.height) / 40;

    const a = 2 * Math.PI * i / totalPoints;
    const xo = 16 * Math.pow(Math.sin(a), 3) * scale;
    const yo = -(13 * Math.cos(a) - 5 * Math.cos(2 * a) - 2 * Math.cos(3 * a) - Math.cos(4 * a)) * scale;

    const L = 0.15 + Math.random() * 0.35;
    const xi = xo * (1 - L);
    const yi = yo * (1 - L);

    for (let j = 0; j < 10; j++) {
      const f = j / 10;
      const r = Math.floor((1 - 0.6 * f) * 255);
      const g = Math.floor((0.7 * (1 - f)) * 255);
      const b = Math.floor((0.8 * (1 - f)) * 255);

      ctx.strokeStyle = `rgb(${r}, ${g}, ${b})`;
      ctx.lineWidth = 2;
      ctx.beginPath();
      ctx.moveTo(centerX + xo + (xi - xo) * f, centerY + yo + (yi - yo) * f);
      ctx.lineTo(centerX + xo + (xi - xo) * (f + 0.1), centerY + yo + (yi - yo) * (f + 0.1));
      ctx.stroke();
    }
    i++;
    setTimeout(draw, 20);
  }
  draw();
</script>
</body>
</html>
