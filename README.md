<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Antim Pro Racing 3D</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; font-family: 'Arial', sans-serif; }
        #container { width: 100vw; height: 100vh; }
        #ui { position: absolute; top: 20px; left: 20px; color: #00d4ff; font-size: 24px; font-weight: bold; text-shadow: 0 0 10px #00d4ff; }
        
        /* Mobile Controls */
        .controls { position: absolute; bottom: 40px; width: 100%; display: flex; justify-content: space-around; pointer-events: none; }
        .btn { 
            width: 80px; height: 80px; background: rgba(0, 212, 255, 0.2); 
            border: 2px solid #00d4ff; border-radius: 50%; color: white; 
            font-size: 30px; display: flex; align-items: center; justify-content: center;
            pointer-events: auto; -webkit-user-select: none;
        }
        .btn:active { background: #00d4ff; }
    </style>
</head>
<body>

    <div id="ui">SPEED: <span id="speed">0</span> KM/H</div>
    <div id="container"></div>

    <div class="controls">
        <div class="btn" id="left">◀</div>
        <div class="btn" id="right">▶</div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        let scene, camera, renderer, car, road;
        let speed = 0;
        let targetX = 0;
        let score = 0;

        function init() {
            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x020205);
            scene.fog = new THREE.Fog(0x020205, 10, 50);

            camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
            camera.position.set(0, 2, 6);
            camera.rotation.x = -0.2;

            renderer = new THREE.WebGLRenderer({ antialias: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            document.getElementById('container').appendChild(renderer.domElement);

            // Lighting
            const light = new THREE.DirectionalLight(0xffffff, 1);
            light.position.set(0, 10, 10);
            scene.add(light);
            scene.add(new THREE.AmbientLight(0x404040, 2));

            // Road Construction
            const roadGeo = new THREE.PlaneGeometry(10, 1000);
            const roadMat = new THREE.MeshStandardMaterial({ color: 0x111111 });
            road = new THREE.Mesh(roadGeo, roadMat);
            road.rotation.x = -Math.PI / 2;
            scene.add(road);

            // Road Lines
            const lineGeo = new THREE.PlaneGeometry(0.2, 1000);
            const lineMat = new THREE.MeshBasicMaterial({ color: 0xffffff });
            const line = new THREE.Mesh(lineGeo, lineMat);
            line.rotation.x = -Math.PI / 2;
            line.position.y = 0.01;
            scene.add(line);

            // Player Car (3D Box Model)
            const carBody = new THREE.BoxGeometry(1, 0.5, 2);
            const carMat = new THREE.MeshStandardMaterial({ color: 0x00d4ff, metalness: 0.8, roughness: 0.2 });
            car = new THREE.Mesh(carBody, carMat);
            car.position.y = 0.3;
            scene.add(car);

            animate();
        }

        function animate() {
            requestAnimationFrame(animate);

            // Speed & Score
            speed = 120;
            document.getElementById('speed').innerText = speed;

            // Move Road
            road.position.z += 1;
            if(road.position.z > 50) road.position.z = 0;

            // Car Movement Smoothing
            car.position.x += (targetX - car.position.x) * 0.1;
            car.rotation.z = (car.position.x - targetX) * 0.5; // Tilting effect

            renderer.render(scene, camera);
        }

        // Controls
        document.getElementById('left').ontouchstart = () => { if(targetX > -4) targetX -= 2; };
        document.getElementById('right').ontouchstart = () => { if(targetX < 4) targetX += 2; };

        // Handle Resize
        window.onresize = () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        };

        init();
    </script>
</body>
</html>
