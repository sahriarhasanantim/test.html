<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim AI - Ultra Pro</title>
    <style>
        * { box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background: #0b0f1a; color: white; margin: 0; display: flex; justify-content: center; height: 100vh; }
        #chat-container { width: 100%; max-width: 600px; display: flex; flex-direction: column; background: #161b22; position: relative; }
        .header { background: #38bdf8; color: #000; padding: 15px; text-align: center; font-weight: bold; font-size: 1.2rem; box-shadow: 0 2px 10px rgba(0,0,0,0.3); }
        #chat-box { flex: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 15px; }
        .msg { padding: 12px 16px; border-radius: 18px; max-width: 85%; line-height: 1.5; font-size: 15px; word-wrap: break-word; }
        .user { background: #38bdf8; color: #000; align-self: flex-end; border-bottom-right-radius: 2px; }
        .ai { background: #2d333b; color: #f0f6fc; align-self: flex-start; border-bottom-left-radius: 2px; white-space: pre-wrap; }
        
        /* Image Preview Style */
        .img-preview { max-width: 200px; border-radius: 10px; margin-top: 5px; display: block; }

        .input-area { padding: 15px; background: #0b0f1a; display: flex; flex-direction: column; gap: 10px; }
        .controls { display: flex; gap: 10px; align-items: center; }
        input[type="text"] { flex: 1; padding: 12px; border-radius: 25px; border: none; background: #2d333b; color: white; outline: none; font-size: 15px; }
        
        .icon-btn { background: #38bdf8; border: none; width: 45px; height: 45px; border-radius: 50%; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 20px; transition: 0.3s; }
        .icon-btn:hover { background: #0ea5e9; }
        #file-input { display: none; }
        .file-label { background: #2d333b; color: #38bdf8; padding: 10px; border-radius: 50%; cursor: pointer; border: 1px solid #38bdf8; }
    </style>
</head>
<body>

<div id="chat-container">
    <div class="header">Your AI Assistant</div>
    <div id="chat-box">
        <div class="msg ai">আসসালামু আলাইকুম! আমি শাহরিয়ার ভাইয়ের বানানো AI। আপনি আমাকে লিখে বা ছবি দিয়ে যেকোনো প্রশ্ন করতে পারেন।</div>
    </div>

    <div class="input-area">
        <div id="preview-container"></div>
        <div class="controls">
            <label for="file-input" class="file-label">📷</label>
            <input type="file" id="file-input" accept="image/*">
            <input type="text" id="user-input" placeholder="এখানে লিখুন...">
            <button class="icon-btn" onclick="sendMessage()">➤</button>
        </div>
    </div>
</div>

<script>
    const API_KEY = "AIzaSyDRg62_K1Na7elDVFhVroay9C-Mk-I5rqs";
    let selectedImageBase64 = null;

    // Handle Image Selection
    document.getElementById('file-input').onchange = function(e) {
        const file = e.target.files[0];
        if (!file) return;

        const reader = new FileReader();
        reader.onload = function(event) {
            selectedImageBase64 = event.target.result.split(',')[1];
            document.getElementById('preview-container').innerHTML = 
                `<img src="${event.target.result}" style="width:50px; height:50px; border-radius:5px; border:1px solid #38bdf8;">`;
        };
        reader.readAsDataURL(file);
    };

    async function sendMessage() {
        const input = document.getElementById('user-input');
        const box = document.getElementById('chat-box');
        const text = input.value.trim();
        
        if (!text && !selectedImageBase64) return;

        // Display User Message
        let userContent = text;
        if(selectedImageBase64) {
            box.innerHTML += `<div class="msg user"><img src="data:image/jpeg;base64,${selectedImageBase64}" class="img-preview"><br>${text}</div>`;
        } else {
            box.innerHTML += `<div class="msg user">${text}</div>`;
        }

        input.value = "";
        document.getElementById('preview-container').innerHTML = "";
        box.scrollTop = box.scrollHeight;

        const payload = {
            contents: [{
                parts: [
                    { text: "তুমি শাহরিয়ার ভাইয়ের বানানো AI। সব প্রশ্নের উত্তর বন্ধুসুলভভাবে দিবে। প্রশ্ন: " + text }
                ]
            }]
        };

        if (selectedImageBase64) {
            payload.contents[0].parts.push({
                inline_data: { mime_type: "image/jpeg", data: selectedImageBase64 }
            });
        }

        selectedImageBase64 = null; // Clear image for next msg

        try {
            const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(payload)
            });

            const data = await res.json();
            const reply = data.candidates[0].content.parts[0].text;
            box.innerHTML += `<div class="msg ai">${reply}</div>`;
        } catch (e) {
            box.innerHTML += `<div class="msg ai" style="color:#ff4444;">দুঃখিত ভাই, সার্ভারে সমস্যা হচ্ছে। API Key চেক করুন।</div>`;
        }
        box.scrollTop = box.scrollHeight;
    }
</script>

</body>
</html>
