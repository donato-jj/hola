<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Experiencia Visual Profesional</title>

<style>
/* ===== RESET PROFESIONAL ===== */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', sans-serif;
}

body {
    background: linear-gradient(135deg, #0f0f0f, #1b1b1b);
    color: white;
    overflow-x: hidden;
}

/* ===== HEADER ===== */
header {
    position: relative;
    text-align: center;
    padding: 60px 20px;
}

header h1 {
    font-size: 3rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    font-weight: 700;
    background: linear-gradient(90deg, #ffffff, #aaaaaa);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

/* ===== IMAGEN HERO ===== */
.hero {
    position: relative;
    width: 100%;
    height: 90vh;
    overflow: hidden;
}

.hero img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: brightness(70%) contrast(110%);
    transition: 0.5s ease;
}

.hero:hover img {
    transform: scale(1.05);
    filter: brightness(80%);
}

/* ===== OVERLAY ===== */
.overlay {
    position: absolute;
    bottom: 40px;
    left: 40px;
    max-width: 500px;
}

.overlay h2 {
    font-size: 2rem;
    margin-bottom: 10px;
}

.overlay p {
    font-size: 1rem;
    line-height: 1.6;
    opacity: 0.8;
}

/* ===== SECCIÓN PROFESIONAL ===== */
.section {
    padding: 80px 10%;
    text-align: center;
}

.section h3 {
    font-size: 2rem;
    margin-bottom: 20px;
}

.section p {
    max-width: 700px;
    margin: auto;
    line-height: 1.8;
    opacity: 0.8;
}

/* ===== CANVAS PROFESIONAL ===== */
canvas {
    position: fixed;
    top: 0;
    left: 0;
    z-index: -1;
}

/* ===== FOOTER ===== */
footer {
    text-align: center;
    padding: 30px;
    opacity: 0.4;
    font-size: 0.9rem;
}
</style>
</head>

<body>

<canvas id="bgCanvas"></canvas>

<header>
    <h1>Composición Visual Estratégica</h1>
</header>

<section class="hero">
    <img src="20260214_141641.jpg" alt="Imagen Profesional">
    <div class="overlay">
        <h2>Presencia. Actitud. Desafío.</h2>
        <p>
            Una narrativa visual construida desde la seguridad, el control y la postura.
            La imagen comunica carácter, equilibrio emocional y una intención ambigua
            que desafía al observador.
        </p>
    </div>
</section>

<section class="section">
    <h3>Lectura Visual Profesional</h3>
    <p>
        La iluminación tenue enfatiza el contraste, mientras que la postura transmite
        determinación. La expresión proyecta confianza y una invitación implícita
        al enfrentamiento simbólico.
    </p>
</section>

<footer>
    2026 © Diseño Visual Estratégico
</footer>

<script>
// ===== CANVAS ANIMADO PROFESIONAL =====
const canvas = document.getElementById("bgCanvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];

for (let i = 0; i < 100; i++) {
    particles.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: Math.random() * 2,
        speedX: (Math.random() - 0.5) * 0.5,
        speedY: (Math.random() - 0.5) * 0.5
    });
}

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "rgba(255,255,255,0.2)";
    
    particles.forEach(p => {
        p.x += p.speedX;
        p.y += p.speedY;

        if (p.x < 0 || p.x > canvas.width) p.speedX *= -1;
        if (p.y < 0 || p.y > canvas.height) p.speedY *= -1;

        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fill();
    });

    requestAnimationFrame(animate);
}

animate();

// ===== MENSAJE OCULTO =====
document.addEventListener("keydown", function(e) {
    if (e.key === "v") {
        console.log("vení intenta lastimarme");
    }
});
</script>

</body>
</html>
