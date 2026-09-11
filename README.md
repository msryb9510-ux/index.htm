<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>مفاجأة النجاح! 🎓✨</title>

  <!-- مكتبة قصاصات الورق الاحتفالية -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      cursor: pointer;
      user-select: none;
      font-family: system-ui, -apple-system, sans-serif;
      color: #fff;
      overflow: hidden;
    }

    .header-text {
      position: absolute;
      top: 20px;
      text-align: center;
      font-size: 1.2rem;
      font-weight: bold;
      text-shadow: 0 2px 4px rgba(0,0,0,0.6);
      z-index: 10;
      padding: 0 10px;
    }

    .image-container {
      max-width: 90%;
      max-height: 75vh;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6);
      border-radius: 16px;
      overflow: hidden;
      border: 2px solid rgba(255, 255, 255, 0.2);
      transition: transform 0.2s ease;
    }

    .image-container:active {
      transform: scale(0.98);
    }

    img {
      max-width: 100%;
      max-height: 75vh;
      object-fit: contain;
      display: block;
    }

    .footer-hint {
      position: absolute;
      bottom: 20px;
      font-size: 0.9rem;
      opacity: 0.85;
      animation: pulse 1.5s infinite;
      z-index: 10;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.05); }
      100% { transform: scale(1); }
    }
  </style>
</head>
<body>

  <div class="header-text">🎉 ألف مبروك النجاح! اضغط لرؤية المفاجأة ✨</div>

  <div class="image-container">
    <img id="gallery" src="" alt="عرض المفاجأة">
  </div>

  <div class="footer-hint">اضغط في أي مكان للانتقال للهدية التالية 👈</div>

  <script>
    let images = [];
    let currentIndex = 0;
    const imgElement = document.getElementById("gallery");

    // دالة إطلاق قصاصات الورق الاحتفالية
    function launchConfetti() {
      confetti({
        particleCount: 80,
        spread: 70,
        origin: { y: 0.6 }
      });
    }

    async function loadGallery() {
      try {
        const response = await fetch('https://api.github.com/repos/msryb9510-ux/index.htm/contents');
        const data = await response.json();
        
        images = data
          .filter(file => file.name.endsWith('.jpg') || file.name.endsWith('.png') || file.name.endsWith('.jpeg'))
          .map(file => file.name);
          
        if (images.length > 0) {
          imgElement.src = images[0];
          launchConfetti(); // إطلاق الاحتفال عند فتح الصفحة
        }
      } catch (e) {
        console.error(e);
      }
    }

    document.body.addEventListener("click", () => {
      if (images.length > 0) {
        currentIndex = (currentIndex + 1) % images.length;
        imgElement.src = images[currentIndex];
        launchConfetti(); // إطلاق الاحتفال مع كل نقلة صورة
      }
    });

    loadGallery();
  </script>
</body>
</html>
