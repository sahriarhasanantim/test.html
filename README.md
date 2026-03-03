<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SAHRIAR ANTIM - PRO DRIVING 3D</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #000; font-family: 'Segoe UI', sans-serif; }
        canvas { display: block; }

        /* UI Overlay */
        #ui-layer {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; display: flex; flex-direction: column; justify-content: space-between;
        }

        .stats-top {
            padding: 20px; display: flex; justify-content: space-between;
            background: linear-gradient(to bottom, rgba(0,0,0,0.8), transparent);
        }

        .stat-box {
            color: #00f2ff; text-align: center; text-shadow: 0 0 10px #00f2ff;
        }

        .stat-label { font-size: 12px; text-transform: uppercase; letter-spacing: 2px; opacity: 0.8; }
        .stat-value { font-size: 28px; font-weight: 900; }

        /* Steering & Controls */
        .controls-bottom {
            padding: 40px 20px; display: flex; justify-content: space-around;
            pointer-events: auto; background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
        }

        .btn-drive {
            width: 90px; height: 90px; border: 4px solid #00f2ff; border-radius: 50%;
            background: rgba(0, 242, 255, 0.1); color: #fff; font-size: 40px;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 0 20px rgba(0, 242, 255, 0.4);
            transition: 0.1s; -webkit-tap-highlight-color: transparent;
        }

        .btn-drive:active { background: #00f2ff; transform: scale(0.9); }

        #game-over {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
            background: rgba(0,0,0,0.9); padding: 40px; border: 2px solid #ff0044;
            color: #ff0044; text-align: center; display: none; pointer-events: auto;
            border-radius: 20px; box-shadow: 0 0 50px #ff0044;
        }

        .restart-btn {
            margin-top: 20px; padding: 10px 30px; background: #ff0044;
            color: #fff; border: none; border-radius: 5px; font-weight: bold;
        }
    </style>
</head>
<body>

    <div id="ui-layer">
        <div class="stats-top">
            <div class="stat-box">
                <div class="stat-label">Speed</div>
                <div class="stat-value"><span id="speed-val">0</span> <small style="font-size:14px">KM/H</small></div>
            </div>
            <div class="stat-box">
                <div class="stat-label">Score</div>
                <div class="stat-value" id="score-val">0</div>
            </div>
        </div>

        <div id="game-over">
            <h1>CRASHED!</h1>
            <p>Your driving skills need work.</p>
            <button class="restart-btn" onclick="location.reload()">TRY AGAIN</button>
        </div>

        <div class="controls-bottom">
            <div class="btn-drive" id="left-ctrl">❮</div>
            <div class="btn-drive" id="right-ctrl">❯</div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        // --- 3D ENGINE START ---
        let scene, camera, renderer, playerCar, clock;
        let road, trafficCars = [];
        let speed = 0, score = 0, isGameOver = false;
        let targetLane = 0; // -1: Left, 0: Center, 1: Right
        const lanes = [-2.5, 0, 2.5];

        function init() {
            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x02050a);
            scene.fog = new THREE.FogExp2(0x02050a, 0.04);

            camera = new THREE.PerspectiveCamera(60, window.innerWidth/window.innerHeight, 0.1, 1000);
            camera.position.set(0, 3.5, 9);
            camera.lookAt(0, 1, -5);

            renderer = new THREE.WebGLRenderer({ antialias: true });
            renderer.setPixelRatio(window.devicePixelRatio);
            renderer.setSize(window.innerWidth, window.innerHeight);
            document.body.appendChild(renderer.domElement);

            clock = new THREE.Clock();

            // Lights
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
            scene.add(ambientLight);

            const hemiLight = new THREE.HemisphereLight(0x00f2ff, 0xff0044, 0.6);
            scene.add(hemiLight);

            createRoad();
            createPlayerCar();
            
            // Spawn traffic periodically
            setInterval(spawnTraffic, 1500);

            animate();
        }

        function createRoad() {
            const roadGeo = new THREE.PlaneGeometry(10, 1000);
            const roadMat = new THREE.MeshStandardMaterial({ 
                color: 0x111111, 
                roughness: 0.7,
                metalness: 0.1
            });
            road = new THREE.Mesh(roadGeo, roadMat);
            road.rotation.x = -Math.PI / 2;
            scene.add(road);

            // Center Lines
            const lineGeo = new THREE.PlaneGeometry(0.2, 1000);
            const lineMat = new THREE.MeshBasicMaterial({ color: 0xffffff });
            const line = new THREE.Mesh(lineGeo, lineMat);
            line.rotation.x = -Math.PI / 2;
            line.position.y = 0.02;
            scene.add(line);
        }

        function createPlayerCar() {
            const group = new THREE.Group();
            
            // Car Base
            const bodyGeo = new THREE.BoxGeometry(1.2, 0.6, 2.8);
            const bodyMat = new THREE.MeshStandardMaterial({ color: 0x00f2ff, metalness: 0.8, roughness: 0.2 });
            const body = new THREE.Mesh(bodyGeo, bodyMat);
            group.add(body);

            // Car Cabin
            const cabinGeo = new THREE.BoxGeometry(1, 0.5, 1.2);
            const cabinMat = new THREE.MeshStandardMaterial({ color: 0x111111 });
            const cabin = new THREE.Mesh(cabinGeo, cabinMat);
            cabin.position.set(0, 0.45, 0.2);
            group.add(cabin);

            // Headlights
            const headGeo = new THREE.BoxGeometry(0.3, 0.1, 0.1);
            const headMat = new THREE.MeshBasicMaterial({ color: 0xffffff });
            const hLeft = new THREE.Mesh(headGeo, headMat);
            hLeft.position.set(-0.4, 0, -1.4);
            group.add(hLeft);
            const hRight = hLeft.clone();
            hRight.position.set(0.4, 0, -1.4);
            group.add(hRight);

            playerCar = group;
            playerCar.position.y = 0.5;
            scene.add(playerCar);
        }

        function spawnTraffic() {
            if(isGameOver) return;
            const group = new THREE.Group();
            const bodyGeo = new THREE.BoxGeometry(1.2, 0.6, 2.5);
            const bodyMat = new THREE.MeshStandardMaterial({ color: 0xff0044 });
            const body = new THREE.Mesh(bodyGeo, bodyMat);
            group.add(body);

            const laneIdx = Math.floor(Math.random() * 3);
            group.position.set(lanes[laneIdx], 0.5, -100);
            
            scene.add(group);
            trafficCars.push(group);
        }

        function animate() {
            if(isGameOver) return;
            requestAnimationFrame(animate);

            const delta = clock.getDelta();
            speed = 140; // Static speed for effect
            document.getElementById('speed-val').innerText = speed + Math.floor(Math.random()*5);

            // Move Road
            road.position.z += 1.5;
            if(road.position.z > 50) road.position.z = 0;

            // Player Horizontal Movement
            const targetPosX = lanes[targetLane + 1];
            playerCar.position.x += (targetPosX - playerCar.position.x) * 0.15;
            playerCar.rotation.z = (playerCar.position.x - targetPosX) * 0.3;
            playerCar.rotation.y = (targetPosX - playerCar.position.x) * 0.2;

            // Traffic Movement & Collision
            trafficCars.forEach((tc, idx) => {
                tc.position.z += 1.2;
                
                // Collision Detection
                const distZ = Math.abs(playerCar.position.z - tc.position.z);
                const distX = Math.abs(playerCar.position.x - tc.position.x);
                if(distZ < 2.5 && distX < 1.1) {
                    gameOver();
                }

                if(tc.position.z > 20) {
                    scene.remove(tc);
                    trafficCars.splice(idx, 1);
                    score += 10;
                    document.getElementById('score-val').innerText = score;
                }
            });

            renderer.render(scene, camera);
        }

        function gameOver() {
            isGameOver = true;
            document.getElementById('game-over').style.display = 'block';
        }

        // --- Controls ---
        document.getElementById('left-ctrl').addEventListener('touchstart', (e) => {
            e.preventDefault();
            if(targetLane > -1) targetLane--;
        });

        document.getElementById('right-ctrl').addEventListener('touchstart', (e) => {
            e.preventDefault();
            if(targetLane < 1) targetLane++;
        });

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        init();
        // --- 3D ENGINE END ---
    </script>
</body>
</html>
