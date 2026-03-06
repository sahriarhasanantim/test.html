<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sahriar Hossain Antim | Vision 2026</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/0libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #38bdf8;
            --secondary: #818cf8;
            --bg: #0b0f1a;
            --card-bg: rgba(30, 41, 59, 0.5);
        }

        * { box-sizing: border-box; scroll-behavior: smooth; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: var(--bg); color: #e2e8f0; margin: 0; line-height: 1.6; }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: radial-gradient(circle at center, #1e293b 0%, #0b0f1a 100%);
            padding: 20px;
        }

        .hero h1 { font-size: 3rem; margin: 0; background: linear-gradient(to right, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hero p { font-size: 1.2rem; color: #94a3b8; margin: 20px 0; max-width: 600px; }
        .cta-btns { display: flex; gap: 15px; }
        .btn { padding: 12px 25px; border-radius: 30px; text-decoration: none; font-weight: bold; transition: 0.3s; }
        .btn-primary { background: var(--primary); color: #000; }
        .btn-secondary { border: 2px solid var(--primary); color: var(--primary); }
        .btn:hover { opacity: 0.8; transform: translateY(-3px); }

        /* Section Styling */
        section { padding: 80px 20px; max-width: 1000px; margin: 0 auto; }
        h2 { text-align: center; font-size: 2rem; margin-bottom: 40px; color: var(--primary); border-bottom: 2px solid #1e293b; display: inline-block; width: 100%; padding-bottom: 10px; }

        /* About & Grid */
        .about-text { background: var(--card-bg); padding: 30px; border-radius: 20px; backdrop-filter: blur(10px); border: 1px solid rgba(255,255,255,0.1); }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 30px; }
        .card { background: var(--card-bg); padding: 25px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.05); }
        .card i { font-size: 2rem; color: var(--primary); margin-bottom: 15px; }

        /* Gallery */
        .gallery { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; }
        .gallery img { width: 100%; height: 250px; object-fit: cover; border-radius: 10px; transition: 0.4s; cursor: pointer; border: 2px solid transparent; }
        .gallery img:hover { transform: scale(1.05); border-color: var(--primary); box-shadow: 0 10px 20px rgba(0,0,0,0.5); }

        /* Social Media */
        .social-box { text-align: center; background: var(--card-bg); padding: 40px; border-radius: 20px; margin-top: 20px; }
        .social-links { display: flex; justify-content: center; gap: 25px; flex-wrap: wrap; margin-top: 20px; }
        .social-icon { font-size: 2.5rem; transition: 0.3s; color: #fff; text-decoration: none; }
        .fa-facebook { color: #1877f2; }
        .fa-instagram { color: #e4405f; }
        .fa-linkedin { color: #0a66c2; }
        .social-icon:hover { transform: translateY(-5px); filter: brightness(1.2); }
        .social-item { display: flex; flex-direction: column; align-items: center; gap: 10px; }
        .social-item span { font-size: 0.8rem; color: #94a3b8; }

        /* Contact Footer */
        .footer { text-align: center; padding: 40px; background: #05070a; margin-top: 50px; }
        .address { color: #94a3b8; font-style: normal; margin-top: 10px; font-size: 0.9rem; }

        @media (max-width: 600px) {
            .hero h1 { font-size: 2.2rem; }
            .gallery { grid-template-columns: repeat(2, 1fr); }
        }
    </style>
</head>
<body>

    <header class="hero">
        <h1>Hi, I'm Sahriar Hossain Antim</h1>
        <p>A Creative Thinker | Aspiring Visionary | Lifelong Learner</p>
        <div class="cta-btns">
            <a href="#gallery" class="btn btn-primary">View My Work</a>
            <a href="#connect" class="btn btn-secondary">Contact Me</a>
        </div>
    </header>

    <section id="about">
        <h2>About Me</h2>
        <div class="about-text">
            "I am a driven and curious individual who has recently completed my Higher Secondary Education (HSC). Rather than following the traditional path, my goal is to pursue 'something different'—to innovate, challenge the status quo, and leave a unique mark on the world."
        </div>
        
        <div class="grid">
            <div class="card">
                <i class="fas fa-user-graduate"></i>
                <h3>Education</h3>
                <p>Successfully completed HSC. Currently preparing for specialized fields to merge academic knowledge with unconventional thinking.</p>
            </div>
            <div class="card">
                <i class="fas fa-bullseye"></i>
                <h3>The Goal</h3>
                <p>To build a career that is impactful and unique, challenging the standard norms of society.</p>
            </div>
        </div>
    </section>

    <section>
        <h2>My World</h2>
        <div class="grid">
            <div class="card"><i class="fas fa-music"></i><h3>Vocals</h3><p>I live music; it's my ultimate escape and expression.</p></div>
            <div class="card"><i class="fas fa-camera"></i><h3>Photography</h3><p>Capturing story-telling moments through my lens.</p></div>
            <div class="card"><i class="fas fa-book"></i><h3>Reading</h3><p>Finding new perspectives in every book.</p></div>
            <div class="card"><i class="fas fa-plane"></i><h3>Traveling</h3><p>Exploring cultures and finding inspiration in the unknown.</p></div>
        </div>
    </section>

    <section id="gallery">
        <h2>Sahriar's Photo Gallery</h2>
        <div class="gallery">
            <img src="https://i.ibb.co/84jpmXWJ/Picsart-25-11-02-22-51-15-923.jpg" alt="Antim">
            <img src="https://i.ibb.co/rR0XHfSh/Picsart-25-10-27-12-31-00-384.jpg" alt="Antim">
            <img src="https://i.ibb.co/gM5K0GdN/Picsart-25-10-27-12-56-02-287.jpg" alt="Antim">
            <img src="https://i.ibb.co/hxVB2br6/Picsart-25-12-04-21-52-41-889.jpg" alt="Antim">
            <img src="https://i.ibb.co/fY4WYrF1/Picsart-25-11-02-22-39-03-977.jpg" alt="Antim">
            <img src="https://i.ibb.co/v6z1j1nP/Picsart-25-11-02-22-38-02-750.jpg" alt="Antim">
            <img src="https://i.ibb.co/W4jPvdkB/Picsart-25-11-02-22-45-20-935.jpg" alt="Antim">
            <img src="https://i.ibb.co/RkYg8MQx/Picsart-25-10-26-00-30-51-706.jpg" alt="Antim">
            <img src="https://i.ibb.co/23T6CCtB/Picsart-25-11-01-01-10-20-887.jpg" alt="Antim">
            <img src="https://i.ibb.co/7NgxCRK9/IMG-20260208-224245.jpg" alt="Antim">
            <img src="https://i.ibb.co/wrCnDqGz/Gemini-Generated-Image-ihonayihonayihon.png" alt="Antim">
            <img src="https://i.ibb.co/hRmTPgRg/IMG-20260222-151319.jpg" alt="Antim">
            <img src="https://i.ibb.co/277WFNGN/IMG-20260222-105723.jpg" alt="Antim">
            <img src="https://i.ibb.co/7xQ0fLS8/IMG-20260223-055200.jpg" alt="Antim">
            <img src="https://i.ibb.co/Wp0zg9dh/Picsart-26-02-26-11-04-24-748.jpg" alt="Antim">
            <img src="https://i.ibb.co/S47bHS8D/Picsart-26-02-26-10-51-31-055.jpg" alt="Antim">
            <img src="https://i.ibb.co/YFryKzpY/Picsart-26-02-24-14-14-12-719.jpg" alt="Antim">
            <img src="https://i.ibb.co/s9kRm78J/Picsart-26-02-23-14-39-20-566.jpg" alt="Antim">
        </div>
    </section>

    <section id="connect">
        <h2>Let’s Connect</h2>
        <div class="social-box">
            <p>Follow me on my digital journey</p>
            <div class="social-links">
                <div class="social-item">
                    <a href="https://www.facebook.com/sahriarantim" target="_blank" class="social-icon"><i class="fab fa-facebook"></i></a>
                    <span>Profile</span>
                </div>
                <div class="social-item">
                    <a href="https://www.facebook.com/Sahriarhassanantim" target="_blank" class="social-icon"><i class="fab fa-facebook-f"></i></a>
                    <span>Page</span>
                </div>
                <div class="social-item">
                    <a href="https://www.instagram.com/sahriarhassanantim?igsh=emg3c29odGhnNjIz" target="_blank" class="social-icon"><i class="fab fa-instagram"></i></a>
                    <span>Instagram</span>
                </div>
                <div class="social-item">
                    <a href="https://bd.linkedin.com/in/sahriar-antim" target="_blank" class="social-icon"><i class="fab fa-linkedin"></i></a>
                    <span>LinkedIn</span>
                </div>
            </div>
        </div>
    </section>

    <footer class="footer">
        <p>Email: <strong>sahriarantim@gmail.com</strong></p>
        <address class="address">
            Village: Gonderdiya, Upazila: Monohardi<br>
            District: Narsingdi, Division: Dhaka
        </address>
        <p style="margin-top: 20px; font-size: 0.8rem; opacity: 0.5;">&copy; 2026 Sahriar Hossain Antim. All Rights Reserved.</p>
    </footer>

</body>
</html>
