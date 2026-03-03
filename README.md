<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Dr. Antim Driving</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; }
        
        /* The Environment */
        #game-screen {
            position: relative; width: 100vw; height: 100vh;
            background: url('https://i.ibb.co/LzhYV8p/highway-night.jpg') bottom center;
            background-size: cover;
            animation: roadMove 2s linear infinite;
        }

        @keyframes roadMove {
            from { background-position: 50% 0%; }
            to { background-position: 50% 100%; }
        }

        /* Dr. Driving Dashboard - রিয়েল গাড়ির ফিল */
        #dashboard {
            position: absolute; bottom: 0; width: 100%; height: 220px;
            background: linear-gradient(to top, #111, #222);
            border-top: 4px solid #444; box-shadow: 0 -10px 30px rgba(0,0,0,0.8);
            display: flex; justify-content: center; align-items: center;
        }

        #steering-wheel {
            width: 180px; height: 180px;
            background: url('https://i.ibb.co/hZ7mZ4p/steering-wheel.png') no-repeat center;
            background-size: contain;
            transition: transform 0.2s;
            z-index: 10;
        }

        .speedo {
            position: absolute; right: 20px; bottom: 80px;
            color: #00f2ff; font-family: 'Orbitron', sans-serif;
            text-align: center; font-size: 20px; font-weight: bold;
        }

        /* Traffic Car */
        #traffic {
            position: absolute; top: -200px; left: 50%;
            width: 80px; height: 150px;
            background: url('https://i.ibb.co/vYm6z8H/red-car.png') no-repeat center;
            background-size: contain;
        }

        /* Controls */
        .controls { position: absolute; bottom: 30px; width: 100%; display: flex; justify-content: space-around; z-index: 100; }
        .btn { width: 80px; height: 80px; background: rgba(0, 242, 255, 0.1); border: 2px solid #00f2ff; border-radius: 50%; display: flex; align-items: center; justify-content: center; color: #fff; font-size: 30px; font-weight: bold; -webkit-tap-highlight-color: transparent; }
    </style>
</head>
<body>

    <div id="game-screen">
        <div id="traffic"></div>
        
        <div id="dashboard">
            <div id="steering-wheel"></div>
            <div class="speedo">
                <div id="km">110</div>
                <div style="font-size: 10px;">KM/H</div>
            </div>
        </div>
    </div>

    <div class="controls">
        <div class="btn" id="lBtn">❮</div>
        <div class="btn" id="rBtn">❯</div>
    </div>

    <script>
        const steering = document.getElementById('steering-wheel');
        const screen = document.getElementById('game-screen');
        const traffic = document.getElementById('traffic');
        const kmText = document.getElementById('km');

        let rot = 0;
        let roadPos = 50;

        document.getElementById('lBtn').ontouchstart = (e) => {
            e.preventDefault();
            rot -= 45; roadPos += 5; update();
        };

        document.getElementById('rBtn').ontouchstart = (e) => {
            e.preventDefault();
            rot += 45; roadPos -= 5; update();
        };

        function update() {
            steering.style.transform = `rotate(${rot}deg)`;
            screen.style.backgroundPosition = `${roadPos}% center`;
            kmText.innerText = 100 + Math.floor(Math.random()*20);
        }

        // Traffic System
        let tTop = -200;
        let tLeft = 40;
        setInterval(() => {
            tTop += 10;
            if(tTop > window.innerHeight) {
                tTop = -200;
                tLeft = 20 + Math.random() * 60;
            }
            traffic.style.top = tTop + 'px';
            traffic.style.left = tLeft + '%';
        }, 30);
    </script>
</body>
</html>
