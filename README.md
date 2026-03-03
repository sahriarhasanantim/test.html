<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Sahriar 3D Racing</title>
    <style>
        body { margin: 0; background: #000; overflow: hidden; font-family: 'Arial', sans-serif; }
        #game-container { position: relative; width: 100vw; height: 100vh; perspective: 800px; }
        
        /* 3D Road */
        .road {
            position: absolute; width: 100%; height: 200%; top: -100%;
            background: linear-gradient(#333, #111);
            background-image: 
                linear-gradient(90deg, transparent 48%, #fff 50%, transparent 52%),
                linear-gradient(90deg, #555 2%, transparent 2%, transparent 98%, #555 98%);
            background-size: 100% 100px;
            transform: rotateX(60deg);
            transform-origin: bottom;
            animation: moveRoad 0.5s linear infinite;
        }

        @keyframes moveRoad {
            from { background-position: 0 0; }
            to { background-position: 0 100px; }
        }

        /* The Car */
        #player {
            position: absolute; bottom: 100px; left: 50%;
            width: 60px; height: 100px;
            background: #38bdf8;
            border-radius: 10px;
            transform: translateX(-50%);
            box-shadow: 0 10px 20px rgba(56, 189, 248, 0.5), inset 0 0 20px rgba(0,0,0,0.5);
            transition: left 0.2s ease-out;
            z-index: 10;
        }

        /* Car Windows & Details */
        #player::after {
            content: ''; position: absolute; top: 20px; left: 5px;
            width: 50px; height: 30px; background: #1e293b; border-radius: 5px;
        }

        /* Enemies */
        .enemy {
            position: absolute; width: 60px; height: 100px;
            background: #ff4444; border-radius: 10px;
            z-index: 5; box-shadow: 0 5px 15px rgba(255, 68, 68, 0.4);
        }

        /* UI */
        .score { position: absolute; top: 20px; left: 20px; color: #fff; font-size: 24px; font-weight: bold; }
        .controls { position: absolute; bottom: 30px; width: 100%; display: flex; justify-content: space-around; }
        .btn { width: 80px; height: 80px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; align-items: center; justify-content: center; color: white; font-size: 30px; border: 2px solid #fff; -webkit-user-select: none; }
    </style>
</head>
<body>

    <div id="game-container">
        <div class="score">SCORE: <span id="scoreVal">0</span></div>
        <div class="road"></div>
        <div id="player"></div>
        <div id="enemies-container"></div>
    </div>

    <div class="controls">
        <div class="btn" id="lBtn">◀</div>
        <div class="btn" id="rBtn">▶</div>
    </div>

<script>
    const player = document.getElementById('player');
    const enemiesContainer = document.getElementById('enemies-container');
    const scoreVal = document.getElementById('scoreVal');
    
    let score = 0;
    let playerPos = 50; // percentage
    let gameActive = true;

    // Move Player
    document.getElementById('lBtn').ontouchstart = () => { if(playerPos > 20) playerPos -= 30; updatePlayer(); };
    document.getElementById('rBtn').ontouchstart = () => { if(playerPos < 80) playerPos += 30; updatePlayer(); };

    function updatePlayer() {
        player.style.left = playerPos + '%';
    }

    // Spawn Enemies
    function spawnEnemy() {
        if(!gameActive) return;
        
        const enemy = document.createElement('div');
        enemy.className = 'enemy';
        const lanes = [20, 50, 80];
        const lane = lanes[Math.floor(Math.random() * lanes.length)];
        
        enemy.style.left = lane + '%';
        enemy.style.top = '-150px';
        enemiesContainer.appendChild(enemy);

        let top = -150;
        const interval = setInterval(() => {
            top += 8;
            enemy.style.top = top + 'px';

            // Collision detection
            if (top > window.innerHeight - 220 && top < window.innerHeight - 100) {
                if (lane === playerPos) {
                    gameActive = false;
                    alert("CRASHED! FINAL SCORE: " + score);
                    location.reload();
                }
            }

            if (top > window.innerHeight) {
                clearInterval(interval);
                enemy.remove();
                score += 10;
                scoreVal.innerText = score;
            }
        }, 20);
    }

    setInterval(spawnEnemy, 1500);

    // Keyboard support
    window.onkeydown = (e) => {
        if(e.key === "ArrowLeft" && playerPos > 20) playerPos -= 30;
        if(e.key === "ArrowRight" && playerPos < 80) playerPos += 30;
        updatePlayer();
    };

</script>
</body>
</html>
