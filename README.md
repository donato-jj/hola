<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Silencio en la Habitación</title>

<style>
    * {
        margin: 0; padding: 0;
        box-sizing: border-box;
        font-family: "Inter", sans-serif;
    }

    body {
        background: #000;
        overflow: hidden;
    }

    /* Fondo oscuro con ruido */
    .background {
        position: fixed;
        inset: 0;
        background: url('conejo.jpg') center/cover no-repeat;
        filter: brightness(0.35) blur(2px);
        z-index: -2;
    }

    .noise {
        position: fixed;
        inset: 0;
        background: url('https://upload.wikimedia.org/wikipedia/commons/0/0c/NoiseTexture.png');
        opacity: 0.04;
        mix-blend-mode: overlay;
        animation: noiseMove 0.5s infinite;
        z-index: -1;
    }

    @keyframes noiseMove {
        0% {transform: translate(0,0);}
        100% {transform: translate(2px,-2px);}
    }

    /* Contenedor principal */
    .wrapper {
        width: 100%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        padding-top: 5vh;
        color: #e0e0e0;
        text-shadow: 0 0 10px #000;
    }

    .model {
        width: 280px;
        height: 380px;
        background: url('conejo.jpg') center/cover no-repeat;
        border-radius: 12px;
        box-shadow: 0 0 25px rgba(255,0,0,0.2);
        animation: subtleMove 6s infinite ease-in-out;
        transition: 0.3s;
    }

    @keyframes subtleMove {
        0% { transform: translateY(0); }
        50% { transform: translateY(-4px); }
        100% { transform: translateY(0); }
    }

    h1 {
        margin: 25px 0;
        font-size: 2rem;
        letter-spacing: 2px;
        color: #ffffffd2;
    }

    .dialog {
        width: 75%;
        height: 42vh;
        padding: 20px;
        background: rgba(0,0,0,0.55);
        backdrop-filter: blur(6px);
        border: 1px solid rgba(255,255,255,0.05);
        border-radius: 12px;
        overflow-y: auto;
        box-shadow: 0 0 20px rgba(255,255,255,0.08);
    }

    .dialog p {
        margin: 10px 0;
        font-size: 0.95rem;
        line-height: 1.5;
    }

    .input-box {
        margin-top: 20px;
        display: flex;
        justify-content: center;
        gap: 10px;
    }

    input {
        width: 60%;
        padding: 12px;
        border-radius: 10px;
        border: none;
        outline: none;
        background: rgba(255,255,255,0.08);
        color: white;
        font-size: 1rem;
        backdrop-filter: blur(4px);
    }

    button {
        padding: 12px 20px;
        background: #8b0000;
        border: none;
        border-radius: 10px;
        color: white;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
    }

    button:hover {
        background: #b30000;
    }

    /* Glitch visual */
    .glitch {
        animation: glitch 0.25s linear 2;
    }

    @keyframes glitch {
        0% { transform: translate(2px, -2px); }
        50% { transform: translate(-2px, 1px); }
        100% { transform: translate(0,0); }
    }
</style>
</head>
<body>

<div class="background"></div>
<div class="noise"></div>

<div class="wrapper">
    <div id="model" class="model"></div>

    <h1>Él Está Escuchando</h1>

    <div class="dialog" id="log"></div>

    <div class="input-box">
        <input id="question" type="text" placeholder="Habla... pero elegí bien tus palabras">
        <button onclick="ask()">Enviar</button>
    </div>
</div>

<script>
    let memory = [];
    let tension = 0; // Aumenta cuanto más personales sean las preguntas

    const darkPatterns = [
        "No deberías haber preguntado eso.",
        "Ese pensamiento no es tuyo… ¿o sí?",
        "La habitación se vuelve más fría cuando lo decís.",
        "Yo escucho más de lo que respondo.",
        "Lo repetiste en tu cabeza antes de pronunciarlo.",
        "No te conviene seguir por ese camino.",
        "Él te escuchó. Yo también."
    ];

    const personalTriggers = ["yo", "vos", "miedo", "morir", "ver", "siento", "sos", "soy", "quién"];

    function analyze(q) {
        let risk = personalTriggers.some(word => q.toLowerCase().includes(word));
        if (risk) tension++;

        let base = darkPatterns[Math.floor(Math.random()*darkPatterns.length)];

        return base + (tension > 2 ? " Y no estoy solo en esta respuesta." : "");
    }

    function ask() {
        const input = document.getElementById("question");
        const log = document.getElementById("log");
        const model = document.getElementById("model");

        if (!input.value.trim()) return;

        let q = input.value;
        memory.push(q);

        log.innerHTML += `<p><strong>Tú:</strong> ${q}</p>`;

        let answer = analyze(q);

        log.innerHTML += `<p><strong>Él:</strong> ${answer}</p>`;

        if (Math.random() < 0.25) {
            model.classList.add("glitch");
            setTimeout(()=> model.classList.remove("glitch"), 300);
        }

        speak(answer);

        input.value = "";
        log.scrollTop = log.scrollHeight;
    }

    function speak(text) {
        let msg = new SpeechSynthesisUtterance(text);
        msg.pitch = 0.5;
        msg.rate = 0.8;
        msg.volume = 0.7;
        msg.voice = speechSynthesis.getVoices().find(v => v.lang.includes("es"));
        speechSynthesis.speak(msg);
    }

    setTimeout(() => speechSynthesis.getVoices(), 1000);
</script>

</body>
</html>
