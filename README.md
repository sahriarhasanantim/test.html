<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim Dynamic Hub 2026</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --accent: #00ff88; --bg: #050810; --card: rgba(15, 23, 42, 0.8); }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Poppins', sans-serif; }
        
        body { background: var(--bg); color: white; min-height: 100vh; overflow-x: hidden; }

        /* Animated Background */
        .bg-glow { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: radial-gradient(circle at 50% 50%, #1e293b 0%, #050810 100%); z-index: -1; }

        .container { max-width: 500px; margin: 0 auto; padding: 20px; }

        /* Dynamic Header */
        .header { text-align: center; padding: 30px 0; }
        .profile-img { width: 100px; height: 100px; border-radius: 50%; border: 3px solid var(--accent); margin-bottom: 15px; box-shadow: 0 0 20px rgba(0, 255, 136, 0.3); }
        h1 { font-size: 1.5rem; margin-bottom: 5px; }
        #greeting { color: var(--accent); font-weight: bold; font-size: 1.1rem; }

        /* Dynamic Weather Card */
        .card { background: var(--card); border-radius: 20px; padding: 20px; margin-bottom: 20px; border: 1px solid rgba(255,255,255,0.05); backdrop-filter: blur(10px); }
        .weather-info { display: flex; justify-content: space-between; align-items: center; }
        .temp { font-size: 2rem; font-weight: bold; }

        /* News Ticker */
        .ticker-wrap { background: rgba(0, 255, 136, 0.1); padding: 10px; border-radius: 10px; overflow: hidden; white-space: nowrap; margin-bottom: 20px; border: 1px solid var(--accent); }
        .ticker { display: inline-block; animation: ticker 15s linear infinite; color: var(--accent); font-weight: bold; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        /* Dynamic Projects/Links */
        .link-item { background: rgba(255, 255, 255, 0.03); padding: 15px; border-radius: 12px; margin-bottom: 10px; display: flex; align-items: center; gap: 15px; transition: 0.3s; cursor: pointer; text-decoration: none; color: white; border: 1px solid rgba(255,255,255,0.05); }
        .link-item:hover { background: var(--accent); color: black; transform: scale(1.02); }
        .link-item i { font-size: 1.5rem; }

        footer { text-align: center; padding: 20px; font-size: 0.8rem; color: #64748b; }
    </style>
</head>
<body>

    <div class="bg-glow"></div>

    <div class="container">
        <div class="header">
            <img src="https://i.ibb.co/23T6CCtB/Picsart-25-11-01-01-10-20-887.jpg" class="profile-img">
            <h1>Sahriar Hossain Antim</h1>
            <div id="greeting">Loading...</div>
        </div>

        <div class="ticker-wrap">
            <div class="ticker" id="news-ticker">
                🚀 Welcome to the Future | AI is changing the world | Check out my latest AI News Summary | Stay tuned for more...
            </div>
        </div>

        <div class="card">
            <div class="weather-info">
                <div>
                    <h3 id="location">Dhaka, BD</h3>
                    <p id="weather-desc">Sunny</p>
                </div>
                <div class="temp" id="temp">28°C</div>
            </div>
        </div>

        <h2>Explore My World</h2>
        <div style="margin-top: 15px;">
            <a href="#" class="link-item">
                <i class="fas fa-brain"></i>
                <div>
                    <strong>AI News Portal</strong>
                    <p style="font-size: 0.8rem; opacity: 0.7;">প্রতিদিনের সেরা এআই নিউজ সামারি।</p>
                </div>
            </a>
            <a href="https://facebook.com/sahriarantim" class="link-item">
                <i class="fab fa-facebook"></i>
                <div>
                    <strong>Official Facebook</strong>
                    <p style="font-size: 0.8rem; opacity: 0.7;">Connect with me on Social Media.</p>
                </div>
            </a>
            <a href="#" class="link-item">
                <i class="fas fa-camera-retro"></i>
                <div>
                    <strong>Creative Gallery</strong>
                    <p style="font-size: 0.8rem; opacity: 0.7;">My photography & design works.</p>
                </div>
            </a>
        </div>

        <footer>
            &copy; 2026 Antim Dynamics. <br>
            System Local Time: <span id="clock">00:00</span>
        </footer>
    </div>

    <script>
        // 1. Dynamic Greeting & Clock
        function updateDynamicInfo() {
            const now = new Date();
            const hour = now.getHours();
            const clock = document.getElementById('clock');
            clock.innerText = now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});

            let greet = "";
            if (hour < 12) greet = "শুভ সকাল, শাহরিয়ার ভাই! ☀️";
            else if (hour < 16) greet = "শুভ দুপুর, শাহরিয়ার ভাই! 🌤️";
            else if (hour < 20) greet = "শুভ সন্ধ্যা, শাহরিয়ার ভাই! 🌅";
            else greet = "শুভ রাত্রি, শাহরিয়ার ভাই! 🌙";
            
            document.getElementById('greeting').innerText = greet;
        }

        // 2. Mock Weather Data (Dynamic Feel)
        function updateWeather() {
            // ২০২৬ সালে এপিআই ছাড়াও আমরা রেন্ডমলি ডেটা আপডেট করে ডায়নামিক ফিল দিতে পারি
            const temps = ['26°C', '28°C', '30°C', '27°C'];
            const descs = ['Clear Sky', 'Mostly Cloudy', 'Sunny', 'Light Breeze'];
            const random = Math.floor(Math.random() * temps.length);
            
            document.getElementById('temp').innerText = temps[random];
            document.getElementById('weather-desc').innerText = descs[random];
        }

        setInterval(updateDynamicInfo, 1000);
        setInterval(updateWeather, 10000); // প্রতি ১০ সেকেন্ডে আবহাওয়া পাল্টাবে (সিমুলেশন)
        updateDynamicInfo();
        updateWeather();
    </script>
</body>
</html>
