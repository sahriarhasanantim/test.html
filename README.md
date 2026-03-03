<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim AI Pro</title>
    <style>
        body { font-family: sans-serif; background: #0b0f1a; color: white; margin: 0; display: flex; justify-content: center; height: 100vh; }
        #chat-container { width: 100%; max-width: 500px; display: flex; flex-direction: column; background: #161b22; }
        .header { background: #38bdf8; color: #000; padding: 15px; text-align: center; font-weight: bold; }
        #chat-box { flex: 1; overflow-y: auto; padding: 15px; display: flex; flex-direction: column; gap: 10px; }
        .msg { padding: 10px 15px; border-radius: 15px; max-width: 80%; line-height: 1.4; font-size: 15px; }
        .user { background: #38bdf8; color: #000; align-self: flex-end; }
        .ai { background: #2d333b; align-self: flex-start; white-space: pre-wrap; }
        .input-area { padding: 15px; background: #0b0f1a; display: flex; gap: 10px; align-items: center; }
        input[type="text"] { flex: 1; padding: 12px; border-radius: 20px; border: none; background: #2d333b; color: white; outline: none; }
        .cam-btn { cursor: pointer; font-size: 22px; }
        .send-btn { background: #38bdf8; border: none; padding: 10px 18px; border-radius: 20px; font-weight: bold; cursor: pointer; }
        #file-input { display: none; }
    </style>
</head>
<body>

<div id="chat-container">
    <div class="header">Your AI Assistant</div>
    <div id="chat-box">
        <div class="msg ai">আসসালামু আলাইকুম! আমি শাহরিয়ার ভাইয়ের বানানো AI। আপনি আমাকে লিখে বা ছবি দিয়ে যেকোনো প্রশ্ন করতে পারেন।</div>
    </div>
    <div class="input-area">
        <label for="file-input" class="cam-btn">📷</label>
        <input type="file" id="file-input" accept="image/*">
        <input type="text" id="user-input" placeholder="এখানে লিখুন...">
        <button class="send-btn" onclick="sendMessage()">Send</button>
    </div>
</div>

<script>
    const API_KEY = "AIzaSyDRg62_K1Na7elDVFhVroay9C-Mk-I5rqs";
    let base64Img = null;

    document.getElementById('file-input').onchange = function(e) {
        const reader = new FileReader();
        reader.onload = function(ev) { 
            base64Img = ev.target.result.split(',')[1];
            alert("ছবি যুক্ত হয়েছে!");
        };
        reader.readAsDataURL(e.target.files[0]);
    };

    async function sendMessage() {
        const input = document.getElementById('user-input');
        const box = document.getElementById('chat-box');
        const val = input.value.trim();
        if (!val && !base64Img) return;

        box.innerHTML += `<div class="msg user">${val}</div>`;
        input.value = "";
        box.scrollTop = box.scrollHeight;

        const payload = {
            contents: [{
                parts: [{ text: "তুমি শাহরিয়ার ভাইয়ের বানানো AI। সব প্রশ্নের উত্তর দিবে। প্রশ্ন: " + val }]
            }]
        };

        if (base64Img) {
            payload.contents[0].parts.push({ inline_data: { mime_type: "image/jpeg", data: base64Img } });
            base64Img = null;
        }

        try {
            const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(payload)
            });
            const data = await res.json();
            box.innerHTML += `<div class="msg ai">${data.candidates[0].content.parts[0].text}</div>`;
        } catch (e) {
            // কোনো এরর টেক্সট দেখা যাবে না
        }
        box.scrollTop = box.scrollHeight;
    }
</script>
</body>
</html>
