<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sahriar Hossain Antim | Visionary Portfolio</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --accent: #38bdf8;
            --bg-deep: #020617;
            --glass-bg: rgba(30, 41, 59, 0.4);
            --neon-shadow: 0 0 30px rgba(56, 189, 248, 0.3);
        }

        html { scroll-behavior: smooth; }

        body {
            background-color: var(--bg-deep);
            background-image: radial-gradient(circle at top right, #1e293b, #020617);
            color: #f1f5f9;
            font-family: 'Inter', sans-serif;
            margin: 0;
            overflow-x: hidden;
        }

        .container { max-width: 1200px; margin: 0 auto; padding: 0 25px; }

        header {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .profile-img {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            border: 4px solid var(--accent);
            padding: 8px;
            transition: 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            object-fit: cover;
            box-shadow: var(--neon-shadow);
            margin-bottom: 25px;
        }

        .profile-img:hover {
            transform: scale(1.1) rotate(5deg);
            box-shadow: 0 0 50px rgba(56, 189, 248, 0.6);
        }

        h1 {
            font-size: clamp(2.5rem, 8vw, 4.5rem);
            font-weight: 800;
            margin: 0;
            background: linear-gradient(to right, #ffffff, #38bdf8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -2px;
        }

        .sub-headline {
            font-size: 1.2rem;
            color: #94a3b8;
            margin-top: 15px;
        }

        .btn-main {
            padding: 16px 45px;
            border-radius: 100px;
            text-decoration: none;
            font-weight: 700;
            transition: 0.4s;
            display: inline-block;
            margin-top: 35px;
            text-transform: uppercase;
            font-size: 0.9rem;
            background: var(--accent);
            color: #000;
            box-shadow: 0 10px 25px rgba(56, 189, 248, 0.3);
        }

        .btn-main:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(56, 189, 248, 0.5);
        }

        /* Gallery Section */
        .gallery-section { padding: 100px 0; }

        .gallery-title {
            text-align: center;
            margin-bottom: 60px;
            font-size: 2.5rem;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 4px;
        }

        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
        }

        .gallery-grid img {
            width: 100%;
            height: 550px;
            object-fit: cover;
            border-radius: 30px;
            transition: 0.6s;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .gallery-grid img:hover {
            transform: scale(1.03);
            border-color: var(--accent);
            box-shadow: 0 25px 50px rgba(0,0,0,0.7);
        }

        /* Contact Section */
        .contact-card {
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            padding: 80px 20px;
            text-align: center;
            border-radius: 60px;
            margin: 100px 0;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .social-icons {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin-top: 40px;
        }

        .social-icons a { color: #fff; font-size: 40px; transition: 0.4s; opacity: 0.7; }
        .social-icons a:hover { color: var(--accent); transform: translateY(-10px); opacity: 1; }

        footer { text-align: center; padding: 50px 0; color: #475569; font-size: 0.9rem; }

        @media (max-width: 768px) {
            .gallery-grid { grid-template-columns: 1fr; }
            .gallery-grid img { height: 450px; }
            h1 { font-size: 3rem; }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <img src="https://i.ibb.co/YnXjRng/IMG-20260215-102021.jpg" alt="Sahriar" class="profile-img">
            <h1>Sahriar Hossain Antim</h1>
            <p class="sub-headline">Creative Thinker • Visionary Explorer • Digital Enthusiast</p>
            <a href="#gallery" class="btn-main">My Photo Gallery</a>
        </header>

        <div class="gallery-section" id="gallery">
            <h2 class="gallery-title">Captured Moments</h2>
            <div class="gallery-grid">
                <img src="https://i.ibb.co/84jpmXWJ/Picsart-25-11-02-22-51-15-923.jpg">
                <img src="https://i.ibb.co/rR0XHfSh/Picsart-25-10-27-12-31-00-384.jpg">
                <img src="https://i.ibb.co/gM5K0GdN/Picsart-25-10-27-12-56-02-287.jpg">
                <img src="https://i.ibb.co/hxVB2br6/Picsart-25-12-04-21-52-41-889.jpg">
                <img src="https://i.ibb.co/fY4WYrF1/Picsart-25-11-02-22-39-03-977.jpg">
                <img src="https://i.ibb.co/v6z1j1nP/Picsart-25-11-02-22-38-02-750.jpg">
                <img src="https://i.ibb.co/W4jPvdkB/Picsart-25-11-02-22-45-20-935.jpg">
                <img src="https://i.ibb.co/RkYg8MQx/Picsart-25-10-26-00-30-51-706.jpg">
                <img src="https://i.ibb.co/23T6CCtB/Picsart-25-11-01-01-10-20-887.jpg">
                <img src="https://i.ibb.co/7NgxCRK9/IMG-20260208-224245.jpg">
                <img src="https://i.ibb.co/wrCnDqGz/Gemini-Generated-Image-ihonayihonayihon.png">
                <img src="https://i.ibb.co/hRmTPgRg/IMG-20260222-151319.jpg">
                <img src="https://i.ibb.co/277WFNGN/IMG-20260222-105723.jpg">
                <img src="https://i.ibb.co/7xQ0fLS8/IMG-20260223-055200.jpg">
                <img src="https://i.ibb.co/Wp0zg9dh/Picsart-26-02-26-11-04-24-748.jpg">
                <img src="https://i.ibb.co/S47bHS8D/Picsart-26-02-26-10-51-31-055.jpg">
                <img src="https://i.ibb.co/YFryKzpY/Picsart-26-02-24-14-14-12-719.jpg">
                <img src="https://i.ibb.co/s9kRm78J/Picsart-26-02-23-14-39-20-566.jpg">
            </div>
        </div>

        <div class="contact-card" id="contact">
            <h2 style="font-size: 2.5rem; color: var(--accent);">Stay In Touch</h2>
            <p style="color: #94a3b8;">sahriarantim@gmail.com</p>
            <div class="social-icons">
                <a href="https://www.facebook.com/sahriarantim" target="_blank"><i class="fab fa-facebook"></i></a>
                <a href="https://www.instagram.com/sahriarhassanantim" target="_blank"><i class="fab fa-instagram"></i></a>
                <a href="https://bd.linkedin.com/in/sahriar-antim-3464b13464b13b4" target="_blank"><i class="fab fa-linkedin"></i></a>
            </div>
        </div>

        <footer>
            <p>&copy; 2026 Sahriar Hossain Antim.</p>
        </footer>
    </div>

    <script type="text/javascript">
    (function(d, m){
        var kSettings = {"appId":"2853755452f1b40212e3367807758367a","popupWidget":true,"automaticChatOpenOnNavigation":true};
        var s = document.createElement("script"); s.type = "text/javascript"; s.async = true;
        s.src = "https://widget.kommunicate.io/v2/kommunicate.app";
        var h = document.getElementsByTagName("head")[0]; h.appendChild(s);
        window.kommunicate = m; m._globals = kSettings;
    })(document, window.kommunicate || {});
    </script>
</body>
</html>
