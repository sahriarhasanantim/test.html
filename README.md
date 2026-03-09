<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim AI Hub | Dynamic News</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --accent: #00ff88; --bg: #050810; --card: #111827; }
        body { font-family: 'Poppins', sans-serif; background: var(--bg); color: white; margin: 0; padding: 20px; }
        
        .header { text-align: center; margin-bottom: 30px; }
        .header h1 { color: var(--accent); margin-bottom: 5px; }

        /* News Card */
        .news-card { background: var(--card); padding: 20px; border-radius: 15px; border-left: 5px solid var(--accent); cursor: pointer; transition: 0.3s; margin-bottom: 15px; }
        .news-card:hover { transform: translateY(-5px); background: #1e293b; }
        .news-card h3 { margin: 0 0 10px; font-size: 1.1rem; }
        .news-card p { font-size: 0.85rem; color: #94a3b8; }

        /* --- Dynamic Modal (The Interface) --- */
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 1000; justify-content: center; align-items: center; padding: 20px; }
        .modal-content { background: #1e293b; width: 100%; max-width: 500px; padding: 30px; border-radius: 20px; position: relative; border: 1px solid var(--accent); animation: slideUp 0.3s ease; }
        @keyframes slideUp { from { transform: translateY(50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        
        .close-btn { position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; color: var(--accent); }
        .modal h2 { color: var(--accent); margin-bottom: 15px; font-size: 1.4rem; }
        .modal p { line-height: 1.6; color: #e2e8f0; }

        footer { text-align: center; margin-top: 50px; font-size: 0.8rem; color: #64748b; }
    </style>
</head>
<body>

    <div class="header">
        <h1>AI News Hub 2026</h1>
        <p>Click any news to read summary</p>
    </div>

    <div id="news-container">
        <div class="news-card" onclick="openNews(1)">
            <h3>🚀 OpenAI-এর নতুন ভিডিও মডেল</h3>
            <p>২০২৬ সালের সবচেয়ে শক্তিশালী ভিডিও জেনারেটর নিয়ে এলো ওপেনএআই...</p>
            <small style="color:var(--accent)">Read Summary →</small>
        </div>

        <div class="news-card" onclick="openNews(2)">
            <h3>🤖 হিউম্যানয়েড রোবট এখন ঘরে ঘরে</h3>
            <p>টেসলার নতুন রোবট এখন রান্নার কাজেও পারদর্শী হয়ে উঠছে...</p>
            <small style="color:var(--accent)">Read Summary →</small>
        </div>
    </div>

    <div id="newsModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeNews()">&times;</span>
            <h2 id="modalTitle">News Title</h2>
            <hr style="border: 0.5px solid #334155; margin-bottom: 20px;">
            <p id="modalBody">News details will appear here...</p>
            <button onclick="closeNews()" style="margin-top: 20px; width: 100%; padding: 10px; background: var(--accent); border: none; border-radius: 10px; font-weight: bold; cursor: pointer;">Close Reading</button>
        </div>
    </div>

    <footer>
        &copy; 2026 Sahriar Hossain Antim. Developed for Dynamic Experience.
    </footer>

    <script>
        // --- Dynamic Content Data ---
        const newsData = {
            1: {
                title: "OpenAI-এর নতুন ভিডিও মডেল",
                body: "২০২৬ সালের এই নতুন মডেলটি দিয়ে এখন ১ ঘণ্টার পূর্ণাঙ্গ সিনেমা বানানো সম্ভব। এটি বাস্তব পৃথিবীর ফিজিক্স বুঝতে পারে এবং একশ শতাংশ রিয়েলিস্টিক ভিডিও আউটপুট দেয়। এটি এআই জগতের এক নতুন বিপ্লব।"
            },
            2: {
                title: "হিউম্যানয়েড রোবট এখন ঘরে ঘরে",
                body: "টেসলার অপ্টিমাস রোবট এখন সাধারণ মানুষের সাধ্যের মধ্যে চলে এসেছে। এটি ঘর পরিষ্কার করা থেকে শুরু করে আপনার সাথে গল্প করা পর্যন্ত সব কাজ করতে পারে। এটি সম্পূর্ণ ভয়েস কমান্ডে চলে।"
            }
        };

        // --- Functions to handle Interface ---
        function openNews(id) {
            const news = newsData[id];
            document.getElementById('modalTitle').innerText = news.title;
            document.getElementById('modalBody').innerText = news.body;
            document.getElementById('newsModal').style.display = 'flex';
        }

        function closeNews() {
            document.getElementById('newsModal').style.display = 'none';
        }

        // Close modal if user clicks outside of it
        window.onclick = function(event) {
            if (event.target == document.getElementById('newsModal')) {
                closeNews();
            }
        }
    </script>
</body>
</html>
