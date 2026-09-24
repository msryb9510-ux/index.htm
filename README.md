<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>A Beautiful Rose 🌹</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body, html {
      width: 100%;
      height: 100%;
      background-color: #000000;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }
    .rose-container {
      position: relative;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .rose-img {
      max-width: 90%;
      max-height: 85vh;
      object-fit: contain;
      filter: drop-shadow(0 0 35px rgba(230, 0, 50, 0.45));
      animation: fadeInZoom 2s ease-out forwards;
    }
    @keyframes fadeInZoom {
      0% {
        opacity: 0;
        transform: scale(0.85);
      }
      100% {
        opacity: 1;
        transform: scale(1);
      }
    }
  </style>
</head>
<body>

<div class="rose-container">
  <img src="https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=1000&auto=format&fit=crop" alt="Rose" class="rose-img">
</div>

</body>
</html>
