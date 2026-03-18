<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim | Digital Time Capsule</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #ffd700; --bg: #030712; }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cinzel', serif; }
        
        body { background: var(--bg); color: white; display: flex; flex-direction: column; align-items: center; min-height: 100vh; overflow-x: hidden; }

        /* Space/Galaxy Background Effect */
        .stars { position: fixed; width: 100%; height: 100%; background: radial-gradient(circle, #111827 0%, #030712 100%); z-index: -1; }

        .header { text-align: center; margin-top: 50px; }
        .header h1 { font-size: 2.5rem; color: var(--gold); letter-spacing: 5px; text-shadow: 0 0 20px rgba(255, 215, 0, 0.5); }
        .header p { color: #94a3b8; font-family: sans-serif; margin-top: 10px; }

        .capsule-container { width: 90%; max-width: 500px; background: rgba(255, 255, 255, 0.02); padding: 30px; border-radius: 30px; border: 1px solid rgba(255, 215, 0, 0.2); margin-top: 40px; backdrop-filter: blur(15px); text-align: center; }

        /* The Animated Capsule */
        .capsule-icon { font-size: 4rem; color: var(--gold); animation: float 3s ease-in-out infinite; margin-bottom: 20px; }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }

        textarea { width: 100%; height: 120px; background: #0f172a; border: 1px solid #1e293b; color: white; border-radius: 15px; padding: 15px; margin-top: 20px; outline: none; font-family: sans-serif; font-size: 1rem; }
        
        button { background: transparent; border: 2px solid var(--gold); color: var(--gold); padding: 12px 30px; border-radius: 50px; font-weight: bold; cursor: pointer; margin-top: 20px; transition: 0.4s; text-transform: uppercase; }
        button:hover { background: var(--gold); color: black; box-shadow: 0 0 30px var(--gold); }

        /* Lock Interface */
        .locked-msg { display: none; margin-top: 30px; padding: 20px; border-top: 1px solid rgba(255, 215, 0, 0.1); }
        .timer { font-size: 2rem; color: var(--gold); margin: 10px 0; font-family: monospace; }
        
        footer { margin-top: auto; padding: 40px; color: #475569; font-size: 0.7rem; font-family: sans-serif; letter-spacing: 2px; }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&display=swap" rel="stylesheet">
</head>
<body>

    <div class="stars"></div>

    <div class="header">
        <h1>TIME CAPSULE</h1>
        <p>ভবিষ্যতের নিজের জন্য একটি বার্তা লিখে রাখুন...</p>
    </div>

    <div class="capsule-container">
        <i class="fas fa-hourglass-half capsule-icon"></i>
        
        <div id="input-area">
            <textarea id="message" placeholder="আপনার বার্তাটি এখানে লিখুন যা ১ মিনিট পর আনলক হবে..."></textarea>
            <button onclick="sealCapsule()">Seal Message</button>
        </div>

        <div id="locked-area" class="locked-msg">
            <h3 style="color: #94a3b8;">MESSAGE SEALED!</h3>
            <p style="font-size: 0.8rem; margin-top: 5px;">আনলক হতে বাকি আছে:</p>
            <div class="timer" id="countdown">00:00:60</div>
            <p id="unlock-text" style="display: none; color: #00ff88; font-weight: bold;">ক্যাপসুল এখন ওপেন! 🔓</p>
            <div id="final-message" style="display: none; margin-top: 20px; padding: 15px; background: rgba(0, 255, 136, 0.1); border-radius: 10px;"></div>
        </div>
    </div>

    <footer>
        DESIGNED BY SAHRIAR ANTIM • GEN-2026
    </footer>

    <script>
        let timeLeft = 60; // আপাতত ১ মিনিটের জন্য সেট করা
        let timerId;

        function sealCapsule() {
            const msg = document.getElementById('message').value;
            if (!msg) { alert("কিছু তো লিখুন শাহরিয়ার ভাই!"); return; }

            document.getElementById('input-area').style.display = 'none';
            document.getElementById('locked-area').style.display = 'block';
            document.getElementById('final-message').innerText = msg;

            timerId = setInterval(updateTimer, 1000);
        }

        function updateTimer() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('countdown').innerText = 
                `00:${minutes < 10 ? '0' : ''}${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

            if (timeLeft <= 0) {
                clearInterval(timerId);
                document.getElementById('countdown').style.display = 'none';
                document.getElementById('unlock-text').style.display = 'block';
                document.getElementById('final-message').style.display = 'block';
                document.body.style.boxShadow = "inset 0 0 100px #00ff8844";
            }
            timeLeft--;
        }
    </script>
</body>
</html>
