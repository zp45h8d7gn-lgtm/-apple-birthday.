<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Happy Birthday apple_wannabe3</title>

<style>

* {

    box-sizing: border-box;

    -webkit-tap-highlight-color: transparent;

}

body {

    margin: 0;

    background: #17182f;

    color: #fff0df;

    font-family: monospace;

    overflow: hidden;

}

#game {

    min-height: 100dvh;

    display: flex;

    flex-direction: column;

    justify-content: center;

    align-items: center;

    padding: 12px;

    gap: 12px;

    background: radial-gradient(#39314f, #17182f);

}

h1 {

    color: #f5bfd7;

    font-size: clamp(17px, 4vw, 27px);

    text-align: center;

    margin: 0;

    text-shadow: 3px 3px #654c76;

}

.subtitle {

    color: #d9c2f0;

    font-size: 11px;

    text-align: center;

    margin: 0;

}

#screen {

    width: min(960px, 96vw);

    aspect-ratio: 16 / 10;

    position: relative;

    border: 7px solid #b89acb;

    box-shadow: 0 0 25px #9b7caf;

    background: #49415f;

}

canvas {

    width: 100%;

    height: 100%;

    display: block;

    image-rendering: pixelated;

    image-rendering: crisp-edges;

}

.controls {

    display: flex;

    align-items: center;

    justify-content: center;

    gap: 10px;

}

.controls button {

    width: 53px;

    height: 47px;

    background: #d7b6e8;

    color: #29213c;

    border: 3px solid #fff0df;

    border-radius: 9px;

    font-size: 20px;

    font-weight: bold;

    touch-action: none;

}

.controls button:active {

    background: #ffb6d0;

    transform: scale(.94);

}

.hint {

    font-size: 10px;

    color: #d9c2f0;

    text-align: center;

}

#message {

    position: fixed;

    inset: 0;

    background: #17182fe8;

    display: none;

    align-items: center;

    justify-content: center;

    z-index: 20;

    padding: 20px;

}

.paper {

    width: min(390px, 100%);

    padding: 25px;

    background: #fff0df;

    color: #51405f;

    border: 7px solid #d7b6e8;

    box-shadow: 8px 8px #765a91;

    text-align: center;

    line-height: 1.8;

}

.paper h2 {

    color: #d47fa9;

}

.paper button {

    background: #d7b6e8;

    color: #29213c;

    border: 2px solid #765a91;

    padding: 10px 20px;

    font-family: monospace;

}

</style>

</head>

<body>

<div id="game">

<h1>Happy Birthday apple_wannabe3 ♡</h1>

<p class="subtitle">A little birthday room made with love ✦</p>

<div id="screen">

<canvas id="world" width="320" height="200"></canvas>

</div>

<div class="controls">

<button data-move="left">◀</button>

<button data-move="up">▲</button>

<button data-move="down">▼</button>

<button data-move="right">▶</button>

</div>

<p class="hint">

HELP HER FIND THE BIRTHDAY CAKE ✧

</p>

</div>

<div id="message">

<div class="paper">

<h2>Happy Birthday ♡</h2>

<p>

Dear apple_wannabe3

<br><br>

I hope your life is filled with

beautiful little moments

endless happiness and warm memories.

<br><br>

May every little wish come true

and may your days always shine

as beautifully as these stars.

<br><br>

You deserve all the happiness

in the universe.

<br><br>

With love ♡

</p>

<button onclick="closeLetter()">Close letter</button>

</div>

</div>

<script>

const canvas = document.getElementById("world");

const ctx = canvas.getContext("2d");

const W = 320;

const H = 200;

let frame = 0;

let girl = {

    x: 65,

    y: 143,

    direction: 1,

    walking: false

};

let cakeTaken = false;

const keys = {

    left: false,

    right: false,

    up: false,

    down: false

};

function rect(x,y,w,h,color) {

    ctx.fillStyle = color;

    ctx.fillRect(Math.round(x),Math.round(y),w,h);

}

function text(t,x,y,color,size=7) {

    ctx.fillStyle = color;

    ctx.font = size + "px monospace";

    ctx.fillText(t,x,y);

}

/* TWINKLING STARS */

const stars = [];

for(let i=0;i<38;i++) {

    stars.push({

        x: 15 + Math.random()*145,

        y: 8 + Math.random()*66,

        size: Math.random()>0.6 ? 2 : 1,

        phase: Math.random()*6

    });

}

function drawStars() {

    stars.forEach(s=>{

        let brightness = Math.sin(frame*.07+s.phase);

        rect(

            s.x,

            s.y,

            s.size,

            s.size,

            brightness>0 ? "#fff0df" : "#aa91c9"

        );

        if(brightness>.85) {

            rect(s.x-2,s.y+1,5,1,"#d7b6e8");

            rect(s.x+1,s.y-2,1,5,"#d7b6e8");

        }

    });

}

/* ROOM */

function drawRoom() {

    // Wall

    rect(0,0,320,155,"#49415f");

    // Wallpaper

    for(let x=8;x<320;x+=22) {

        for(let y=8;y<145;y+=22) {

            rect(x,y,1,1,"#796687");

        }

    }

    // Window

    rect(14,14,111,83,"#d5a8bd");

    rect(19,19,101,73,"#191c3c");

    drawStars();

    // Moon

    rect(91,30,15,15,"#f4d8b5");

    rect(98,25,14,14,"#191c3c");

    // Window frame

    rect(65,19,3,73,"#d5a8bd");

    rect(19,55,101,3,"#d5a8bd");

    // Curtains

    rect(12,12,9,89,"#b77c9e");

    rect(118,12,9,89,"#b77c9e");

    // Wall decorations

    rect(160,19,35,29,"#d7b6e8");

    rect(164,23,27,21,"#29213c");

    text("♡",173,37,"#ffb6d0",11);

    // Hanging lights

    for(let i=0;i<7;i++) {

        let x=145+i*23;

        rect(x,0,1,10,"#d7b6e8");

        rect(x-2,10,5,5,

            Math.sin(frame*.1+i)>0 ? "#fff0df":"#d7b6e8");

    }

    // Floor

    rect(0,155,320,45,"#98728d");

    for(let y=158;y<200;y+=10) {

        rect(0,y,320,1,"#bd91a7");

    }

    for(let x=15;x<320;x+=43) {

        rect(x,155,1,45,"#805d7d");

    }

    // Rug

    rect(48,166,226,25,"#a98bbd");

    rect(55,169,212,19,"#d1b0d7");

    rect(62,172,198,13,"#b89acb");

    // Rug details

    for(let x=65;x<260;x+=12) {

        rect(x,176,3,2,"#f2c8dc");

    }

    // Plant

    rect(289,137,15,18,"#b77e9a");

    rect(293,122,5,16,"#8aa18a");

    rect(284,130,10,5,"#91ad91");

    rect(297,126,10,5,"#91ad91");

    // Bookshelf

    rect(235,60,67,5,"#bd91a7");

    rect(235,65,4,32,"#805d7d");

    rect(298,65,4,32,"#805d7d");

    rect(244,48,9,12,"#d7b6e8");

    rect(255,43,9,17,"#ed9fbe");

    rect(268,50,8,10,"#f4d8b5");

    // Small wall garland

    for(let i=0;i<5;i++) {

        rect(145+i*15,37+Math.abs(2-i)*3,3,3,"#ffb6d0");

    }

}

/* PIXEL CAKE */

function drawCake() {

    // Plate

    rect(226,119,48,4,"#fff0df");

    rect(231,123,38,2,"#d7b6e8");

    if(cakeTaken) return;

    // Cake body

    rect(234,103,33,15,"#ed9fbe");

    rect(230,108,41,10,"#f5bfd7");

    // Cake frosting

    rect(230,104,41,5,"#fff0df");

    rect(233,109,5,5,"#fff0df");

    rect(244,109,5,5,"#fff0df");

    rect(259,109,5,5,"#fff0df");

    // Cake decoration

    rect(239,113,3,3,"#d7b6e8");

    rect(252,113,3,3,"#d7b6e8");

    // Candles

    rect(239,96,3,8,"#f4d8b5");

    rect(248,94,3,10,"#f4d8b5");

    rect(258,96,3,8,"#f4d8b5");

    // Flames

    let glow = frame%30<15 ? "#fff0df":"#f5bfd7";

    rect(239,92,3,4,glow);

    rect(248,90,3,4,glow);

    rect(258,92,3,4,glow);

    // Cake shadow

    rect(236,125,31,2,"#765a91");

}

/* TABLE */

function drawTable() {

    // Legs

    rect(218,126,5,25,"#765a91");

    rect(270,126,5,25,"#765a91");

    // Table

    rect(211,119,72,7,"#bd91a7");

    rect(214,119,66,3,"#f0c5ce");

    // Table cloth

    rect(216,126,62,3,"#ed9fbe");

    // Gift

    rect(282,113,16,12,"#d7b6e8");

    rect(288,109,4,4,"#ffb6d0");

    rect(289,113,2,12,"#f4d8b5");

}

/* PIXEL CAT */

function drawCat(x,y,color,variant) {

    let bounce = Math.sin(frame*.13+variant)*2;

    y += bounce;

    // Tail

    rect(x+1,y+13,3,5,color);

    rect(x-2,y+10,4,3,color);

    // Body

    rect(x+5,y+12,15,9,color);

    rect(x+7,y+10,11,3,color);

    // Head

    rect(x+5,y+2,15,12,color);

    // Ears

    rect(x+5,y,5,5,color);

    rect(x+15,y,5,5,color);

    rect(x+7,y+1,2,3,"#f5bfd7");

    rect(x+17,y+1,2,3,"#f5bfd7");

    // Face

    rect(x+8,y+7,2,2,"#fff0df");

    rect(x+15,y+7,2,2,"#fff0df");

    rect(x+11,y+10,3,2,"#ed9fbe");

    // Legs

    rect(x+7,y+19,4,4,color);

    rect(x+15,y+19,4,4,color);

    // Whiskers

    rect(x+2,y+11,4,1,"#fff0df");

    rect(x+19,y+11,4,1,"#fff0df");

}

/* CROCHET BALL */

function drawYarn() {

    let y = 147 + Math.sin(frame*.15)*3;

    let x = 167 + Math.sin(frame*.07)*9;

    // Shadow

    rect(x-2,166,15,2,"#765a91");

    // Ball

    rect(x,y,11,11,"#ed9fbe");

    rect(x+2,y-2,7,2,"#f5bfd7");

    // Yarn lines

    rect(x+3,y+2,2,7,"#fff0df");

    rect(x+6,y+2,2,7,"#d7b6e8");

    rect(x+1,y+5,9,2,"#d7b6e8");

    // Thread

    rect(x+10,y+9,5,2,"#f5bfd7");

    rect(x+14,y+8,3,2,"#f5bfd7");

}

/* PIXEL GIRL */

function drawGirl() {

    let x = girl.x;

    let y = girl.y;

    let step = girl.walking && frame%12<6 ? 2:0;

    // Shadow

    rect(x-2,y+28,18,3,"#765a91");

    // Hair back

    rect(x+1,y+2,13,12,"#493044");

    rect(x-1,y+8,4,13,"#493044");

    rect(x+12,y+9,4,12,"#493044");

    // Face

    rect(x+3,y+5,10,10,"#f2c6ac");

    // Hair fringe

    rect(x+2,y+2,12,5,"#493044");

    rect(x+1,y+5,4,4,"#493044");

    // Eyes

    rect(x+5,y+9,2,2,"#493044");

    rect(x+10,y+9,2,2,"#493044");

    // Blush

    rect(x+3,y+12,2,1,"#ed9fbe");

    rect(x+12,y+12,2,1,"#ed9fbe");

    // Neck

    rect(x+7,y+15,4,3,"#f2c6ac");

    // Dress

    rect(x+4,y+17,10,3,"#f5bfd7");

    rect(x+2,y+20,14,7,"#ed9fbe");

    rect(x,y+27,18,3,"#d7b6e8");

    // Arms

    rect(x,y+19,3,7,"#f2c6ac");

    rect(x+15,y+19,3,7,"#f2c6ac");

    // Legs

    rect(x+4,y+29,4,5-step,"#f2c6ac");

    rect(x+12,y+29,4,5+step,"#f2c6ac");

    // Shoes

    rect(x+2,y+33-step,6,3,"#d7b6e8");

    rect(x+11,y+33+step,6,3,"#d7b6e8");

    // Hair ribbon

    rect(x+12,y+3,4,3,"#ffb6d0");

}

/* DRAW WORLD */

function draw() {

    frame++;

    ctx.clearRect(0,0,W,H);

    drawRoom();

    drawTable();

    drawCake();

    // Cats playing

    let cat1x = 132 + Math.sin(frame*.035)*9;

    let cat2x = 181 + Math.sin(frame*.04+2)*8;

    drawCat(cat1x,143,"#29213c",1);

    drawCat(cat2x,145,"#c7a5b9",3);

    drawYarn();

    drawGirl();

    // Instructions

    if(!cakeTaken) {

        text("✦ BIRTHDAY PARTY ✦",128,12,"#fff0df",6);

    }

    requestAnimationFrame(draw);

}

draw();

/* MOVEMENT */

function move(direction) {

    const speed = 3;

    girl.walking = true;

    if(direction==="left") {

        girl.x -= speed;

        girl.direction = -1;

    }

    if(direction==="right") {

        girl.x += speed;

        girl.direction = 1;

    }

    if(direction==="up") {

        girl.y -= speed;

    }

    if(direction==="down") {

        girl.y += speed;

    }

    girl.x = Math.max(5,Math.min(295,girl.x));

    girl.y = Math.max(105,Math.min(157,girl.y));

    checkCake();

}

function stop() {

    girl.walking = false;

}

document.addEventListener("keydown",e=>{

    const map = {

        ArrowLeft:"left",

        ArrowRight:"right",

        ArrowUp:"up",

        ArrowDown:"down"

    };

    if(map[e.key]) {

        e.preventDefault();

        move(map[e.key]);

    }

});

document.querySelectorAll("[data-move]").forEach(button=>{

    let timer;

    const direction = button.dataset.move;

    button.addEventListener("pointerdown",e=>{

        e.preventDefault();

        move(direction);

        timer=setInterval(()=>move(direction),110);

    });

    function release() {

        clearInterval(timer);

        stop();

    }

    button.addEventListener("pointerup",release);

    button.addEventListener("pointerleave",release);

    button.addEventListener("pointercancel",release);

});

/* CAKE INTERACTION */

function checkCake() {

    if(cakeTaken) return;

    const closeX = girl.x > 205 && girl.x < 270;

    const closeY = girl.y < 150;

    if(closeX && closeY) {

        cakeTaken = true;

        setTimeout(()=>{

            document.getElementById("message").style.display="flex";

        },400);

    }

}

function closeLetter() {

    document.getElementById("message").style.display="none";

}

</script>

</body>

</html>
