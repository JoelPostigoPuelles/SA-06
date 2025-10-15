<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Integración de Herramientas</title>
    <style>
      body {
        margin: 0;
        background: radial-gradient(circle at center, #0a0a12, #050510);
        color: #e0e0e0;
        font-family: "Segoe UI", Tahoma, sans-serif;
        overflow: hidden;
      }

      h1 {
        text-align: center;
        margin-top: 40px;
        font-size: 2.5rem;
        color: #4dd0e1;
        letter-spacing: 1px;
      }

      canvas {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 0;
      }

      .tools {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 100px;
        margin-top: 120px;
        z-index: 1;
      }

      .tool {
        position: relative;
        text-align: center;
        cursor: pointer;
        transition: transform 0.4s;
      }

      .tool img {
        width: 80px;
        height: 80px;
        border-radius: 20%;
        transition: transform 0.5s ease;
        filter: drop-shadow(0 0 10px rgba(77, 208, 225, 0.6));
      }

      .tool:hover img {
        transform: scale(1.15);
        filter: drop-shadow(0 0 15px rgba(77, 208, 225, 1));
      }

      .tooltip {
        position: absolute;
        bottom: -40px;
        left: 50%;
        transform: translateX(-50%);
        background: rgba(20, 20, 40, 0.9);
        color: #fff;
        padding: 6px 12px;
        border-radius: 8px;
        font-size: 0.8rem;
        opacity: 0;
        transition: opacity 0.3s ease;
        pointer-events: none;
        white-space: nowrap;
      }

      .tool:hover .tooltip {
        opacity: 1;
      }

      footer {
        text-align: center;
        margin-top: 80px;
        color: #999;
        font-size: 0.9rem;
      }
    </style>
  </head>
  <body>
    <canvas id="lines"></canvas>
    <h1>Integración de Herramientas</h1>

    <div class="tools" id="tools">
      <div class="tool" data-x="100" data-y="150">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg"
          alt="VS Code"
        />
        <div class="tooltip">
          Visual Studio Code: Editor principal de desarrollo
        </div>
      </div>
      <div class="tool" data-x="400" data-y="300">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg"
          alt="GitHub"
        />
        <div class="tooltip">GitHub: Control de versiones y colaboración</div>
      </div>
      <div class="tool" data-x="700" data-y="150">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg"
          alt="Figma"
        />
        <div class="tooltip">Figma: Diseño colaborativo UI/UX</div>
      </div>
      <div class="tool" data-x="250" data-y="500">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg"
          alt="Node.js"
        />
        <div class="tooltip">Node.js: Entorno de ejecución backend</div>
      </div>
      <div class="tool" data-x="600" data-y="480">
        <img
          src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg"
          alt="Docker"
        />
        <div class="tooltip">Docker: Contenedores e implementación</div>
      </div>
    </div>

    <footer>
      © 2025 Proyecto: Integración de Herramientas — Creado con HTML, CSS y
      JavaScript
    </footer>

    <script>
      const canvas = document.getElementById("lines");
      const ctx = canvas.getContext("2d");
      const tools = document.querySelectorAll(".tool");
      let positions = [];

      function resizeCanvas() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        updatePositions();
      }

      function updatePositions() {
        positions = [];
        tools.forEach((tool) => {
          const rect = tool.getBoundingClientRect();
          positions.push({
            x: rect.left + rect.width / 2,
            y: rect.top + rect.height / 2,
          });
        });
      }

      function drawLines() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.strokeStyle = "rgba(77,208,225,0.4)";
        ctx.lineWidth = 2;

        for (let i = 0; i < positions.length; i++) {
          for (let j = i + 1; j < positions.length; j++) {
            ctx.beginPath();
            ctx.moveTo(positions[i].x, positions[i].y);
            ctx.lineTo(positions[j].x, positions[j].y);
            ctx.stroke();
          }
        }
      }

      function animate() {
        drawLines();
        requestAnimationFrame(animate);
      }

      window.addEventListener("resize", resizeCanvas);
      resizeCanvas();
      animate();
    </script>
  </body>
</html>
