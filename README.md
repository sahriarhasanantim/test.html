<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Dr. Antim Driving</title>
    <style>
        body { margin: 0; background: #111; overflow: hidden; font-family: sans-serif; }
        canvas { display: block; background: #222; margin: 0 auto; }
        #ui { position: absolute; top: 10px; width: 100%; text-align: center; color: #00f2ff; font-size: 24px; font-weight: bold; pointer-events: none; }
        .controls { position: absolute; bottom: 30px; width: 100%; display: flex; justify-content: space-around; }
        .btn { width: 80px; height: 80px; background: rgba(0, 242, 255, 0.2); border: 3px solid #00f2ff; border-radius: 50%; color: #fff; font-size: 35px; display: flex; align-items: center; justify-content: center; -webkit-tap-highlight-color: transparent; }
    </style>
</head>
<body>
    <div id="ui">SPEED: <span id="speed">0</span> KM/H</div>
    <canvas id="gameCanvas"></canvas>
    <div class="controls">
        <div class="btn" id="lBtn">◀</div>
        <div class="btn" id="rBtn">▶</div>
    </div>

<script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let score = 0;
    let playerX = canvas.width / 2 - 30;
    let lanes = [canvas.width*0.2, canvas.width*0.5, canvas.width*0.8];
    let currentLane = 1;
    let obstacles = [];

    function drawRoad() {
        ctx.fillStyle = "#333";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.strokeStyle = "#fff";
        ctx.setLineDash([40, 40]);
        ctx.lineWidth = 5;
        // Road Lanes
        ctx.beginPath();
        ctx.moveTo(canvas.width*0.35, 0); ctx.lineTo(canvas.width*0.35, canvas.height);
        ctx.moveTo(canvas.width*0.65, 0); ctx.lineTo(canvas.width*0.65, canvas.height);
        ctx.stroke();
    }

    function drawPlayer() {
        ctx.fillStyle = "#00f2ff"; // Neon Blue Car
        ctx.shadowBlur = 15; ctx.shadowColor = "#00f2ff";
        ctx.fillRect(playerX, canvas.height - 150, 60, 100);
        ctx.shadowBlur = 0;
    }

    function createObstacle() {
        if (Math.random() < 0.03) {
            let lane = Math.floor(Math.random() * 3);
            obstacles.push({ x: lanes[lane] - 30, y: -100 });
        }
    }

    function drawObstacles() {
        ctx.fillStyle = "#ff0044"; // Red Traffic
        obstacles.forEach((obs, index) => {
            obs.y += 10;
            ctx.fillRect(obs.x, obs.y, 60, 100);
            
            // Collision detection
            if (obs.y > canvas.height - 150 && obs.y < canvas.height - 50 && Math.abs(obs.x - playerX) < 40) {
                alert("CRASHED! SCORE: " + score);
                location.reload();
            }
            if (obs.y > canvas.height) { obstacles.splice(index, 1); score += 10; }
        });
    }

    function update() {
        drawRoad();
        drawPlayer();
        drawObstacles();
        createObstacle();
        document.getElementById("speed").innerText = 120 + Math.floor(Math.random()*10);
        playerX += (lanes[currentLane] - 30 - playerX) * 0.2;
        requestAnimationFrame(update);
    }

    document.getElementById("lBtn").ontouchstart = (e) => { e.preventDefault(); if(currentLane > 0) currentLane--; };
    document.getElementById("rBtn").ontouchstart = (e) => { e.preventDefault(); if(currentLane < 2) currentLane++; };

    update();
</script>
</body>
</html>
