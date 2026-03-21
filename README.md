<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim | Interactive Universe</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            background: radial-gradient(circle at center, #0f172a 0%, #020617 100%); 
            color: white; height: 100vh; overflow: hidden; 
            font-family: 'Courier New', Courier, monospace;
        }

        /* Instructions */
        .hint { position: fixed; bottom: 20px; width: 100%; text-align: center; color: #64748b; font-size: 0.8rem; pointer-events: none; }

        /* The Sun (Center Profile) */
        .sun {
            position: absolute; top: 50%; left: 50%;
            transform: translate(-50%, -50%);
            width: 120px; height: 120px; border-radius: 50%;
            background: url('https://i.ibb.co/23T6CCtB/Picsart-25-11-01-01-10-20-887.jpg') center/cover;
            box-shadow: 0 0 50px #38bdf8; border: 2px solid #38bdf8;
            z-index: 10; cursor: pointer; transition: 0.5s;
        }
        .sun:hover { box-shadow: 0 0 100px #38bdf8; transform: translate(-50%, -50%) scale(1.1); }

        /* Planets (Floating Items) */
        .planet {
            position: absolute; width: 80px; height: 80px;
            border-radius: 50%; display: flex; align-items: center;
            justify-content: center; font-weight: bold; font-size: 0.7rem;
            text-align: center; cursor: move; border: 1px solid rgba(255,255,255,0.2);
            backdrop-filter: blur(5px); user-select: none;
        }

        #planet-1 { top: 20%; left: 20%; background: rgba(255, 99, 132, 0.2); border-color: #ff6384; }
        #planet-2 { top: 20%; right: 20%; background: rgba(54, 162, 235, 0.2); border-color: #36a2eb; }
        #planet-3 { bottom: 20%; left: 25%; background: rgba(255, 206, 86, 0.2); border-color: #ffce56; }
        #planet-4 { bottom: 20%; right: 25%; background: rgba(75, 192, 192, 0.2); border-color: #4bc0c0; }

        /* Data Modal */
        #info-box {
            display: none; position: fixed; top: 50%; left: 50%;
            transform: translate(-50%, -50%); width: 80%; max-width: 350px;
            background: rgba(15, 23, 42, 0.95); padding: 30px; border-radius: 20px;
            border: 1px solid #38bdf8; z-index: 100; text-align: center;
        }
        .close { color: #38bdf8; cursor: pointer; margin-top: 15px; display: block; font-weight: bold; }

    </style>
</head>
<body>

    <div class="sun" onclick="showInfo('Sahriar Hossain Antim', 'Exploring the boundaries of AI & Web Design. Vision 2026.')"></div>

    <div id="planet-1" class="planet" onmousedown="dragElement(this)">PHOTOGRAPHY</div>
    <div id="planet-2" class="planet" onmousedown="dragElement(this)">AI DEV</div>
    <div id="planet-3" class="planet" onmousedown="dragElement(this)">GALLERY</div>
    <div id="planet-4" class="planet" onmousedown="dragElement(this)">CONNECT</div>

    <div class="hint">গ্রহগুলোকে টেনে দেখুন (Drag the planets) | মাঝখানে ক্লিক করুন</div>

    <div id="info-box">
        <h2 id="title" style="color:#38bdf8"></h2>
        <p id="desc" style="margin-top:15px; line-height:1.5;"></p>
        <span class="close" onclick="closeBox()">[ CLOSE SYSTEM ]</span>
    </div>

    <script>
        // --- Drag Function ---
        function dragElement(elmnt) {
            let pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;
            elmnt.onmousedown = dragMouseDown;
            elmnt.ontouchstart = dragMouseDown; // For Mobile

            function dragMouseDown(e) {
                e = e || window.event;
                e.preventDefault();
                pos3 = e.clientX || e.touches[0].clientX;
                pos4 = e.clientY || e.touches[0].clientY;
                document.onmouseup = closeDragElement;
                document.ontouchend = closeDragElement;
                document.onmousemove = elementDrag;
                document.ontouchmove = elementDrag;
            }

            function elementDrag(e) {
                e = e || window.event;
                let clientX = e.clientX || e.touches[0].clientX;
                let clientY = e.clientY || e.touches[0].clientY;
                pos1 = pos3 - clientX;
                pos2 = pos4 - clientY;
                pos3 = clientX;
                pos4 = clientY;
                elmnt.style.top = (elmnt.offsetTop - pos2) + "px";
                elmnt.style.left = (elmnt.offsetLeft - pos1) + "px";
            }

            function closeDragElement() {
                document.onmouseup = null;
                document.onmousemove = null;
                document.ontouchend = null;
                document.ontouchmove = null;
            }
        }

        // --- Info Box ---
        function showInfo(t, d) {
            document.getElementById('title').innerText = t;
            document.getElementById('desc').innerText = d;
            document.getElementById('info-box').style.display = 'block';
        }

        function closeBox() {
            document.getElementById('info-box').style.display = 'none';
        }

        // Planet Clicks
        document.getElementById('planet-1').onclick = () => showInfo('Photography', 'Capturing the world through a 20-year-old lens. Specializing in cinematic portraits.');
        document.getElementById('planet-2').onclick = () => showInfo('AI Development', 'Integrating Gemini & Python to build the next generation of web apps.');
        document.getElementById('planet-3').onclick = () => showInfo('Visual Gallery', 'A collection of AI-enhanced imagery and personal travel memories.');
        document.getElementById('planet-4').onclick = () => window.open('https://facebook.com/sahriarantim', '_blank');

    </script>
</body>
</html>
