<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim AI - Your Assistant</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #0f172a; color: white; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        #chat-container { width: 95%; max-width: 500px; background: #1e293b; border-radius: 20px; box-shadow: 0 10px 40px rgba(0,0,0,0.6); overflow: hidden; display: flex; flex-direction: column; height: 85vh; border: 1px solid rgba(56, 189, 248, 0.2); }
        .header { background: #38bdf8; color: #000; padding: 20px; text-align: center; font-weight: 800; font-size: 1.2rem; letter-spacing: 1px; }
        #chat-box { flex: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 12px; scroll-behavior: smooth; }
        .message { padding: 12px 18px; border-radius: 15px; max-width: 85%; font-size: 0.95rem; line-height: 1.5; }
        .user-msg { background: #38bdf8; color: #000; align-self: flex-end; border-bottom-right-radius: 2px; }
        .ai-msg { background: #334155; color: #fff; align-self: flex-start; border-bottom-left-radius: 2px; }
        .input-area { display: flex; padding: 15px; background: #0f172a; gap: 10px; border-top: 1px solid #334155; }
        input { flex: 1; padding: 14px; border: none; border-radius: 12px; background: #1e293b; color: white; outline: none; font-size: 1rem; }
        button { padding: 0 25px; background: #38bdf8; border: none; border-radius: 12px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        button:hover { background: #0ea5e9; }
        /* Scrollbar styling */
        #chat-box::-webkit-scrollbar { width: 5px; }
        #chat-box::-webkit-scrollbar-thumb { background: #334155; border-radius: 10px; }
    </style>
</head>
<body>

<div id="chat-container">
    <div class="header">Your AI Assistant</div>
    <div id="chat-box">
        <div class="message ai-msg">আসসালামু আলাইকুম! আমি শাহরিয়ার ভাইয়ের বানানো AI। আপনাকে কীভাবে সাহায্য করতে পারি?</div>
    </div>
    <div class="input-area">
        <input type="text" id="user-input" placeholder="এখানে কিছু লিখুন..." onkeypress="if(event.key === 'Enter') sendMessage()">
        <button onclick="sendMessage()">Send</button>
    </div>
</div>

<script>
    // আপনার API Key
    const API_KEY = "AIzaSyDRg62_K1Na7elDVFhVroay9C-Mk-I5rqs"; 

    async function sendMessage() {
        const input = document.getElementById('user-input');
        const chatBox = document.getElementById('chat-box');
        const userText = input.value.trim();
        
        if (!userText) return;

        // User Message Display
        chatBox.innerHTML += `<div class="message user-msg">${userText}</div>`;
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
            
            if (data.error) {
                chatBox.innerHTML += `<div class="message ai-msg" style="color: #ff4444;">দুঃখিত, এখন উত্তর দিতে পারছি না। আবার চেষ্টা করুন।</div>`;
            } else {
                const aiText = data.candidates[0].content.parts[0].text;
                chatBox.innerHTML += `<div class="message ai-msg">${aiText}</div>`;
            }
            
            chatBox.scrollTop = chatBox.scrollHeight;
        } catch (error) {
            chatBox.innerHTML += `<div class="message ai-msg">সার্ভারে সমস্যা হচ্ছে। দয়া করে ইন্টারনেট কানেকশন চেক করুন।</div>`;
            chatBox.scrollTop = chatBox.scrollHeight;
        }
    }
</script>

</body>
</html>
