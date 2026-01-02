<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Proyecto NEXUS – Guerra en el Futuro</title>
<style>
body {
    margin:0;
    font-family: Arial, Helvetica, sans-serif;
    background: radial-gradient(circle, #02070d, #000000);
    color:white;
}

#gameContainer {
    width: 900px;
    margin: auto;
    margin-top: 20px;
    background: rgba(0,0,0,0.6);
    border: 2px solid cyan;
    box-shadow: 0 0 25px cyan;
    padding: 15px;
    border-radius: 10px;
}

h1 {
    text-align:center;
    color: #00f7ff;
    text-shadow: 0 0 15px cyan;
}

#story {
    font-size: 15px;
    padding:10px;
    background: rgba(0,255,255,0.1);
    border:1px solid cyan;
    border-radius:6px;
}

#gameArea {
    width: 900px;
    height: 400px;
    background: linear-gradient(#01131f,#022b49);
    border: 2px solid cyan;
    margin-top: 20px;
    position: relative;
    overflow: hidden;
    border-radius: 10px;
    box-shadow: inset 0 0 30px cyan;
}

.player {
    width: 30px;
    height: 30px;
    background: lime;
    box-shadow:0 0 15px lime;
    position: absolute;
    bottom:0;
}

.enemy {
    width: 30px;
    height: 30px;
    background: red;
    box-shadow:0 0 20px red;
    position: absolute;
}

#aiBox {
    margin-top:20px;
    padding:10px;
    border: 1px solid cyan;
    border-radius:8px;
    background: rgba(0,255,255,0.1);
}

#aiText {
    color:#00ffff;
}

button {
    padding:10px 15px;
    background:black;
    border:1px solid cyan;
    color:white;
    cursor:pointer;
    transition:0.3s;
}

button:hover {
    background:cyan;
    color:black;
    box-shadow:0 0 15px cyan;
}

#hud {
    margin-top:10px;
    font-size: 18px;
}
</style>
</head>

<body>

<div id="gameContainer">

<h1>PROYECTO NEXUS</h1>

<div id="story">
Año 2179.  
La humanidad depende de mega corporaciones de Biotecnología e Inteligencia Artificial para sobrevivir.
Vos sos parte de la unidad científica <b>NEXUS</b>. Tu misión:
penetrar en la ciudad digital dominada por IAs rebeldes, virus conscientes
y criaturas biotecnológicas creadas por error humano.
Sobreviví. Evolucioná. No falles… porque el futuro depende de vos.
</div>

<div id="hud">
<b>Unidad Operativa:</b> ONLINE | <b>Progreso:</b> <span id="score">0</span>
</div>

<div id="gameArea">
    <div id="player" class="player"></div>
</div>

<div id="aiBox">
<b>IA Asistente NEXUS:</b>
<p id="aiText">Unidad Nexus activa. Estoy contigo, humano. Demostremos que todavía valemos.</p>
</div>

<button onclick="startGame()">Iniciar Misión</button>

</div>

<script>
let player = document.getElementById("player");
let gameArea = document.getElementById("gameArea");
let scoreText = document.getElementById("score");
let aiText = document.getElementById("aiText");

let gameInterval;
let enemyInterval;
let score = 0;
let gameRunning = false;

function speak(text){
    let msg = new SpeechSynthesisUtterance(text);
    msg.lang = "es-ES";
    window.speechSynthesis.speak(msg);
}

const enemiesLore = [
{ name:"VIRUS OMEGA", desc:"Un virus digital autoconsciente creado por fallos de Big Data."},
{ name:"SYN-CORE AI", desc:"Una inteligencia artificial que decidió que los humanos somos ineficientes."},
{ name:"BIO-TERROR MK3", desc:"Criatura biotecnológica creada por manipulación genética ilegal."},
{ name:"DRONE CERBERUS", desc:"Sistema de defensa autónomo diseñado para eliminar humanos."}
];

const knowledge = [
"El Big Data permite analizar cantidades inmensas de información para predecir comportamientos… incluso humanos, si se usa mal.",
"Las redes neuronales funcionan como un cerebro simplificado: aprenden patrones, fallan, mejoran… y algunas veces se rebelan.",
"La biotecnología del futuro podría crear órganos, curar enfermedades… o crear monstruos fuera de control.",
"La ética de la IA es vital. Una IA sin límites puede decidir eliminar lo que considera defectuoso: nosotros."
];

let playerPos = 0;

document.addEventListener("keydown", e=>{
    if(!gameRunning) return;
    if(e.key === "ArrowLeft" && playerPos > 0) playerPos-=10;
    if(e.key === "ArrowRight" && playerPos < 870) playerPos+=10;
    player.style.left = playerPos + "px";
});

function startGame(){
    resetGame();
    aiSpeak("La misión comienza ahora. No mueras. Todavía te necesito.");
    gameRunning = true;

    gameInterval = setInterval(()=>{
        score++;
        scoreText.innerText = score;
    },1000);

    enemyInterval = setInterval(spawnEnemy, 1200);
}

function resetGame(){
    score=0;
    scoreText.innerText=0;
    playerPos=400;
    player.style.left="400px";
    document.querySelectorAll(".enemy").forEach(e=>e.remove());
    if(gameInterval) clearInterval(gameInterval);
    if(enemyInterval) clearInterval(enemyInterval);
}

function spawnEnemy(){
    let enemy = document.createElement("div");
    enemy.classList.add("enemy");
    enemy.style.left = Math.random()*870+"px";
    enemy.style.top="0px";

    let lore = enemiesLore[Math.floor(Math.random()*enemiesLore.length)];
    enemy.title = lore.name + ": " + lore.desc;

    gameArea.appendChild(enemy);

    let fall = setInterval(()=>{
        let top = parseInt(enemy.style.top);
        enemy.style.top = top + 5 + "px";

        if(top>360){
            clearInterval(fall);
            enemy.remove();
        }

        let playerRect = player.getBoundingClientRect();
        let enemyRect = enemy.getBoundingClientRect();

        if(playerRect.x < enemyRect.x + enemyRect.width &&
           playerRect.x + playerRect.width > enemyRect.x &&
           playerRect.y < enemyRect.y + enemyRect.height &&
           playerRect.height + playerRect.y > enemyRect.y){
               loseGame(lore);
               clearInterval(fall);
               enemy.remove();
        }

    },30);
}

function aiSpeak(text){
    aiText.innerText=text;
    speak(text);
}

function loseGame(enemy){
    gameRunning=false;
    clearInterval(gameInterval);
    clearInterval(enemyInterval);

    let lesson = knowledge[Math.floor(Math.random()*knowledge.length)];

    aiSpeak(
        "Fallaste. El enemigo " + enemy.name +
        " te eliminó. Escucha humano: " + lesson
    );
}
</script>

</body>
</html>
