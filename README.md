<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim AI - My Own Brain</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #0f172a; color: white; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        #chat-container { width: 90%; max-width: 500px; background: #1e293b; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.5); overflow: hidden; display: flex; flex-direction: column; }
        #chat-box { height: 400px; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 10px; }
        .message { padding: 10px 15px; border-radius: 15px; max-width: 80%; line-height: 1.4; }
        .user-msg { background: #38bdf8; color: #000; align-self: flex-end; }
        .ai-msg { background: #334155; color: #fff; align-self: flex-start; }
        .input-area { display: flex; padding: 15px; background: #0f172a; gap: 10px; }
        input { flex: 1; padding: 12px; border: none; border-radius: 10px; background: #1e293b; color: white; outline: none; }
        button { padding: 10px 20px; background: #38bdf8; border: none; border-radius: 10px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>

<div id="chat-container">
    <h3 style="text-align: center; padding: 10px; background: #38bdf8; color: black; margin: 0;">Antim AI Assistant</h3>
    <div id="chat-box">
        <div class="message ai-msg">আসসালামু আলাইকুম শাহরিয়ার ভাই! আমি আপনার নিজের বানানো AI। কিছু জানতে চান?</div>
    </div>
    <div class="input-area">
        <input type="text" id="user-input" placeholder="Type something...">
        <button onclick="sendMessage()">Send</button>
    </div>
</div>

<script>
    // AIzaSyDRg62_K1Na7elDVFhVroay9C-Mk-I5rqs
    const API_KEY = "YOUR_API_KEY_HERE"; 

    async function sendMessage() {
        const input = document.getElementById('user-input');
        const chatBox = document.getElementById('chat-box');
        if (!input.value) return;

        // User Message
        chatBox.innerHTML += `<div class="message user-msg">${input.value}</div>`;
        const userText = input.value;
        input.value = "";
        chatBox.scrollTop = chatBox.scrollHeight;

        try {
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    contents: [{ parts: [{ text: userText }] }]
                })
            });

            const data = await response.json();
            const aiText = data.candidates[0].content.parts[0].text;

            // AI Message
            chatBox.innerHTML += `<div class="message ai-msg">${aiText}</div>`;
            chatBox.scrollTop = chatBox.scrollHeight;
        } catch (error) {
            chatBox.innerHTML += `<div class="message ai-msg">উফ! কোথাও একটা ঝামেলা হয়েছে। API Key চেক করেছেন?</div>`;
        }
    }
</script>

</body>
</html>
