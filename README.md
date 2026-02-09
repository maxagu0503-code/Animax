# Animax
Pagina donde subir los vídeos de animax
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>ANIME CORE</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<header>
  <h1>⚡ ANIME CORE ⚡</h1>
  <p>Animaciones 2D + 3D</p>
</header>

<section class="upload">
  <label class="btn">
    SUBIR VIDEO
    <input type="file" accept="video/*" id="videoInput" hidden>
  </label>
</section>

<section id="galeria"></section>

<footer>
  <p>© 2026 · Anime Core</p>
</footer>

<script src="script.js"></script>
</body>
</html>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: radial-gradient(circle at top, #1a1a2e, #000);
  color: #eaeaea;
  font-family: 'Segoe UI', sans-serif;
  overflow-x: hidden;
}

/* Scanlines anime */
body::after {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  background: repeating-linear-gradient(
    to bottom,
    rgba(255,255,255,0.03) 0px,
    rgba(255,255,255,0.03) 1px,
    transparent 2px,
    transparent 4px
  );
  z-index: 999;
}

/* Header */
header {
  text-align: center;
  padding: 35px 20px;
}

header h1 {
  position: relative;
  color: #ff2dfc;
  letter-spacing: 3px;
  text-shadow: 2px 0 #00fff9, -2px 0 #ff0055;
  animation: glitch 2s infinite;
}

header p {
  opacity: 0.8;
}

/* Glitch animation */
@keyframes glitch {
  0% { transform: translate(0); }
  20% { transform: translate(-2px, 2px); }
  40% { transform: translate(2px, -2px); }
  60% { transform: translate(-1px, 1px); }
  80% { transform: translate(1px, -1px); }
  100% { transform: translate(0); }
}

/* Upload button */
.upload {
  text-align: center;
  margin-bottom: 25px;
}

.btn {
  background: linear-gradient(45deg, #ff2dfc, #6a00ff);
  padding: 12px 30px;
  border-radius: 30px;
  cursor: pointer;
  font-weight: bold;
  box-shadow: 0 0 15px #6a00ff;
  transition: transform 0.2s;
}

.btn:hover {
  transform: scale(1.05);
}

/* Gallery */
#galeria {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
}

/* Video card */
.video-card {
  position: relative;
  background: #0f0f1a;
  border-radius: 15px;
  padding: 10px;
  box-shadow: 0 0 20px rgba(255,45,252,0.2);
  animation: fadeIn 0.6s ease;
  overflow: hidden;
}

.video-card::before {
  content: "▶ PLAY";
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.55);
  color: #00fff9;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  letter-spacing: 3px;
  opacity: 0;
  transition: 0.3s;
}

.video-card:hover::before {
  opacity: 1;
}

video {
  width: 100%;
  border-radius: 10px;
}

/* Footer */
footer {
  text-align: center;
  padding: 15px;
  opacity: 0.6;
}

/* Fade animation */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
const input = document.getElementById("videoInput");
const galeria = document.getElementById("galeria");

input.addEventListener("change", () => {
  const file = input.files[0];
  if (!file) return;

  const card = document.createElement("div");
  card.className = "video-card";

  const video = document.createElement("video");
  video.src = URL.createObjectURL(file);
  video.controls = true;

  card.appendChild(video);
  galeria.appendChild(card);
});
