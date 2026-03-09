<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim's Social Feed</title>
    <style>
        body { font-family: sans-serif; background: #0f172a; color: white; padding: 20px; max-width: 500px; margin: auto; }
        .post-input { background: #1e293b; padding: 15px; border-radius: 10px; margin-bottom: 20px; }
        textarea { width: 100%; height: 60px; background: #0f172a; color: white; border: 1px solid #334155; padding: 10px; border-radius: 5px; margin-top: 10px; outline: none; }
        button { background: #38bdf8; border: none; padding: 10px 20px; border-radius: 5px; font-weight: bold; margin-top: 10px; cursor: pointer; width: 100%; }
        #feed { display: flex; flex-direction: column; gap: 15px; }
        .post-card { background: #1e293b; padding: 15px; border-radius: 10px; border-left: 4px solid #38bdf8; }
        .post-card h4 { margin: 0; color: #38bdf8; }
        .post-card p { margin: 10px 0 0; font-size: 0.95rem; }
    </style>
</head>
<body>

    <h2>Antim's Feed 🌍</h2>

    <div class="post-input">
        <input type="text" id="username" placeholder="আপনার নাম..." style="width:100%; padding:8px; background:#0f172a; color:white; border:1px solid #334155; border-radius:5px;">
        <textarea id="post-text" placeholder="কী ভাবছেন?"></textarea>
        <button onclick="publishPost()">Post Now</button>
    </div>

    <div id="feed">
        </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, addDoc, onSnapshot, query, orderBy } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        // --- আপনার Firebase Config এখানে বসাতে হবে ---
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_PROJECT.firebaseapp.com",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_PROJECT.appspot.com",
            messagingSenderId: "YOUR_SENDER_ID",
            appId: "YOUR_APP_ID"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        // পোস্ট করার ফাংশন
        window.publishPost = async () => {
            const name = document.getElementById('username').value;
            const text = document.getElementById('post-text').value;

            if (name && text) {
                await addDoc(collection(db, "posts"), {
                    username: name,
                    content: text,
                    timestamp: new Date()
                });
                document.getElementById('post-text').value = "";
            } else { alert("দয়া করে নাম এবং লেখা দিন!"); }
        };

        // রিয়েল-টাইমে ডাটাবেস থেকে পোস্ট দেখানো
        const q = query(collection(db, "posts"), orderBy("timestamp", "desc"));
        onSnapshot(q, (snapshot) => {
            const feed = document.getElementById('feed');
            feed.innerHTML = "";
            snapshot.forEach((doc) => {
                const data = doc.data();
                feed.innerHTML += `
                    <div class="post-card">
                        <h4>${data.username}</h4>
                        <p>${data.content}</p>
                    </div>
                `;
            });
        });
    </script>
</body>
</html>
