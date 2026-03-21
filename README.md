<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SAHRIAR_ANTIM_OS_V2.6</title>
    <style>
        body {
            background-color: #000;
            color: #0f0;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            flex-direction: column;
            height: 100vh;
            margin: 0;
            padding: 20px;
            overflow: hidden;
            font-size: 14px;
        }

        #matrix-bg {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            z-index: -1; opacity: 0.15;
        }

        #output {
            flex-grow: 1;
            overflow-y: auto;
            white-space: pre-wrap;
            margin-bottom: 10px;
        }

        .input-line { display: flex; align-items: center; }
        .prompt { color: #0f0; margin-right: 10px; font-weight: bold; }
        input {
            background: transparent; border: none; color: #0f0;
            outline: none; flex-grow: 1; font-family: inherit; font-size: inherit;
        }

        .loading-bar { color: #0f0; margin: 10px 0; }
        .accent { color: #fff; text-shadow: 0 0 5px #0f0; }
    </style>
</head>
<body>

    <canvas id="matrix-bg"></canvas>

    <div id="output">
[SYSTEM INITIALIZING...]
[LOADING CORE MODULES...]
[ACCESS GRANTED: SAHRIAR ANTIM PORTFOLIO]

*****************************************************
* WELCOME TO <span class="accent">SAHRIAR_ANTIM.EXE</span> (VERSION 2026.1)  *
*****************************************************

টাইপ করুন <span class="accent">'help'</span> সব কমান্ড দেখতে।

    </div>

    <div class="input-line">
        <span class="prompt">antim@user:~$</span>
        <input type="text" id="cmd-input" autofocus autocomplete="off">
    </div>

    <script>
        const input = document.getElementById('cmd-input');
        const output = document.getElementById('output');

        const commands = {
            'help': "উপলব্ধ কমান্ডসমূহ:\n- <span class='accent'>about</span> : আমার সম্পর্কে জানুন\n- <span class='accent'>skills</span> : আমার স্কিলস\n- <span class='accent'>photo</span> : গ্যালারি লিঙ্ক\n- <span class='accent'>clear</span> : স্ক্রিন পরিষ্কার করুন\n- <span class='accent'>contact</span> : আমার সাথে যোগাযোগ",
            'about': "NAME: Sahriar Hossain Antim\nSTATUS: HSC Completed | Creative Visionary\nLOCATION: Monohardi, Narsingdi\nMISSION: Something different and unique in 2026.",
            'skills': "SYSTEM SKILLS:\n- Web UI Manipulation\n- AI Interaction (Gemini/GPT-4)\n- Creative Photography\n- Innovative Thinking",
            'photo': "নির্দেশনা: <a href='https://sahriarhasanantim.github.io/test.html' target='_blank' style='color:#0f0'>গ্যালারি দেখতে এখানে ক্লিক করুন</a>",
            'contact': "Facebook: facebook.com/sahriarantim\nEmail: sahriarantim@gmail.com",
            'clear': ""
        };

        input.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                const cmd = input.value.toLowerCase().trim();
                const line = `<div class="input-line"><span class="prompt">antim@user:~$</span> ${cmd}</div>`;
                
                if (cmd === 'clear') {
                    output.innerHTML = "[SYSTEM REBOOTED...]\nটাইপ করুন 'help'";
                } else if (commands[cmd]) {
                    output.innerHTML += line + `<div>${commands[cmd]}</div>\n`;
                } else if (cmd !== "") {
                    output.innerHTML += line + `<div>কমান্ড পাওয়া যায়নি: '${cmd}'. টাইপ করুন 'help'</div>\n`;
                }

                input.value = "";
                output.scrollTop = output.scrollHeight;
            }
        });

        // Matrix Background Effect
        const canvas = document.getElementById('matrix-bg');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        const fontSize = 16;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);

        function drawMatrix() {
            ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "#0f0";
            ctx.font = fontSize + "px monospace";
            for (let i = 0; i < drops.length; i++) {
                const text = letters.charAt(Math.floor(Math.random() * letters.length));
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
                drops[i]++;
            }
        }
        setInterval(drawMatrix, 50);
    </script>
</body>
</html>
