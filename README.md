<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Antim Drive Pro | Cockpit Edition</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; font-family: 'Courier New', Courier, monospace; }
        
        /* 3D Environment Container */
        #world { width: 100vw; height: 100vh; perspective: 1000px; background: linear-gradient(#1a1a2e, #16213e); }

        /* Road */
        #road {
            position: absolute; bottom: 0; left: 50%; width: 2000px; height: 3000px;
            background: repeating-linear-gradient(#333 0, #333 100px, #444 100px, #444 200px);
            transform: translateX(-50%) rotateX(75deg);
            transform-origin: bottom;
            animation: drive 1s linear infinite;
        }

        @keyframes drive {
            from { transform: translateX(-50%) rotateX(75deg) translateY(0); }
            to { transform: translateX(-50%) rotateX(75deg) translateY(200px); }
        }

        /* Cockpit View (Dashboard) */
        #cockpit {
            position: absolute; bottom: 0; width: 100%; height: 50%;
            background: linear-gradient(transparent, #000);
            z-index: 100; pointer-events: none;
        }

        .dashboard {
            position: absolute; bottom: 0; width: 100%; height: 180px;
            background: #111; border-top: 5px solid #222;
            display: flex; justify-content: center; align-items: flex-end;
            padding-bottom: 20px;
        }

        .speedometer {
            width: 120px; height: 120px; border: 4px solid #00f2ff;
            border-radius: 50%; display: flex; flex-direction: column;
            align-items: center; justify-content: center; color: #00f2ff;
            box-shadow: 0 0 15px #00f2ff; margin: 0 50px;
        }

        /* Steering Wheel */
        .steering-wheel {
            width: 150px; height: 150px; border: 15px solid #333;
            border-radius: 50%; border-top-color: #00f2ff;
            transition: transform 0.2s; position: absolute; bottom: 60px;
        }

        /* Controls */
        .controls { position: absolute; bottom: 20px; width: 100%; display: flex; justify-content: space-between; padding: 0 30px; box-sizing: border-box; z-index: 200; }
        .btn { width: 80px; height: 80px; background: rgba(0, 242, 255, 0.2); border: 2px solid #00f2ff; border-radius: 50%; color: #fff; font-size: 30px; display: flex; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="world">
        <div id="road"></div>
        
        <div id="traffic" style="position: absolute; top: 30%; left: 45%; width: 100px; height: 150px; background: #ff0044; transform: rotateX(75deg); border-radius: 10px;"></div>
    </div>

    <div id="cockpit">
        <div style="display: flex; justify-content: center;">
            <div id="wheel" class="steering-wheel"></div>
        </div>
        <div class="dashboard">
            <div class="speedometer">
                <div style="font-size: 10px;">KM/H</div>
                <div id="speed" style="font-size: 30px; font-weight: bold;">85</div>
            </div>
        </div>
    </div>

    <div class="controls">
        <div class="btn" id="lBtn">❮</div>
        <div class="btn" id="rBtn">❯</div>
    </div>

    <script>
        const road = document.getElementById('road');
        const wheel = document.getElementById('wheel');
        const speedText = document.getElementById('speed');
        const traffic = document.getElementById('traffic');

        let posX = -50; // Road centering
        let rotation = 0;
        let speed = 85;

        // Steering Logic
        document.getElementById('lBtn').addEventListener('touchstart', (e) => {
            e.preventDefault();
            posX += 5;
            rotation -= 30;
            updateDrive();
        });

        document.getElementById('rBtn').addEventListener('touchstart', (e) => {
            e.preventDefault();
            posX -= 5;
            rotation += 30;
            updateDrive();
        });

        function updateDrive() {
            road.style.transform = `translateX(${posX}%) rotateX(75deg)`;
            wheel.style.transform = `rotate(${rotation}deg)`;
            
            // Random speed fluctuations
            speed = 80 + Math.floor(Math.random() * 20);
            speedText.innerText = speed;
        }

        // Simple Traffic AI
        let trafficPos = 30;
        setInterval(() => {
            trafficPos += 1;
            if(trafficPos > 100) trafficPos = -20;
            traffic.style.top = trafficPos + '%';
        }, 30);

    </script>
</body>
</html>
