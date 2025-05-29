# Chitita
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Te Amo Paula 💖</title>
  <style>
    body {
      margin: 0;
      background: black;
      overflow: hidden;
      font-family: 'Arial', sans-serif;
    }

    canvas {
      display: block;
    }

    .explosion {
      position: absolute;
      color: pink;
      font-size: 40px;
      font-weight: bold;
      pointer-events: none;
      opacity: 0;
      animation: firework 1s ease-out forwards;
      white-space: nowrap;
    }

    @keyframes firework {
      0% {
        transform: scale(0.5) translate(-50%, -50%);
        opacity: 1;
      }
      100% {
        transform: scale(3) translate(-50%, -50%);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <canvas id="canvas"></canvas>

  <script>
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");

    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;

    const fontSize = 22;
    const columns = Math.floor(canvas.width / 100);
    const drops = Array.from({ length: columns }).map(() => ({
      y: Math.random() * canvas.height,
      speed: Math.random() * 2 + 1
    }));

    function draw() {
      ctx.fillStyle = "rgba(0, 0, 0, 0.1)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = "#ff69b4";
      ctx.font = fontSize + "px Arial";

      for (let i = 0; i < drops.length; i++) {
        const x = i * 100;
        const y = drops[i].y;

        ctx.fillText("Te amo", x, y);

        drops[i].y += fontSize * drops[i].speed;
        if (drops[i].y > canvas.height) {
          drops[i].y = -fontSize;
          drops[i].speed = Math.random() * 2 + 1;
        }
      }
    }

    setInterval(draw, 50);

    const palabras = ["PAULA", "TE AMO", "CHITITA", "HERMOSA", "ESPOSA", "PRINCESA"];
    const usadas = new Set();

    function palabraAleatoria() {
      if (usadas.size === palabras.length) usadas.clear();
      let palabra;
      do {
        palabra = palabras[Math.floor(Math.random() * palabras.length)];
      } while (usadas.has(palabra));
      usadas.add(palabra);
      return palabra;
    }

    document.addEventListener("click", function (e) {
      for (let i = 0; i < 5; i++) {
        const explosion = document.createElement("div");
        explosion.className = "explosion";
        explosion.textContent = palabraAleatoria();
        explosion.style.left = `${e.pageX + (Math.random() * 100 - 50)}px`;
        explosion.style.top = `${e.pageY + (Math.random() * 100 - 50)}px`;
        explosion.style.color = `hsl(${Math.random() * 360}, 100%, 75%)`;
        document.body.appendChild(explosion);

        setTimeout(() => {
          explosion.remove();
        }, 1000);
      }
    });

    window.addEventListener("resize", () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
