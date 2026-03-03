<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gemini Vision AI Assistant</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #0e1117; color: white; margin: 0; display: flex; flex-direction: column; height: 100vh; }
        .header { background: #262730; padding: 20px; text-align: center; border-bottom: 1px solid #444; }
        #chat-box { flex: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 15px; }
        .message { padding: 12px 18px; border-radius: 10px; max-width: 85%; line-height: 1.5; font-size: 15px; }
        .user { background: #2b313e; align-self: flex-end; border: 1px solid #444; }
        .assistant { background: #1c1e26; align-self: flex-start; color: #00f2ff; border: 1px solid #333; }
        .input-container { background: #262730; padding: 20px; display: flex; flex-direction: column; gap: 10px; }
        .controls { display: flex; gap: 10px; align-items: center; }
        input[type="text"] { flex: 1; padding: 12px; border-radius: 5px; border: 1px solid #444; background: #0e1117; color: white; outline: none; }
        .file-label { cursor: pointer; background: #444; padding: 10px; border-radius: 5px; font-size: 20px; }
        button { background: #ff4b4b; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer; font-weight: bold; }
        #img-preview { max-width: 100px; border-radius: 5px; display: none; margin-bottom: 10px; }
        #api-setup { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #0e1117; display: flex; flex-direction: column; align-items: center; justify-content: center; z-index: 1000; }
    </style>
</head>
<body>

<div id="api-setup">
    <h2>Enter Your New API Key</h2>
    <input type="password" id="api-key-input" placeholder="Paste Gemini API Key..." style="width: 300px; margin-bottom: 20px; padding: 10px;">
    <button onclick="saveKey()">Start AI Assistant</button>
</div>

<div class="header">
    <h1>📸 Gemini Vision AI</h1>
    <p>শাহরিয়ার ভাইয়ের স্পেশাল অ্যাসিস্ট্যান্ট</p>
</div>

<div id="chat-box">
    <div class="message assistant">আসসালামু আলাইকুম! আমি শাহরিয়ার ভাইয়ের বানানো AI। আপনি ছবি আপলোড করেও আমার সাথে কথা বলতে পারেন।</div>
</div>

<div class="input-container">
    <img id="img-preview">
    <div class="controls">
        <label for="file-input" class="file-label">📸</label>
        <input type="file" id="file-input" accept="image/*" style="display: none;">
        <input type="text" id="user-input" placeholder="ছবির বিষয়ে কিছু লিখুন...">
        <button onclick="sendMessage()">Send</button>
    </div>
</div>

<script>
    let API_KEY = "";
    let base64Image = "";

    function saveKey() {
        const key = document.getElementById('api-key-input').value;
        if (key) {
            API_KEY = key;
            document.getElementById('api-setup').style.display = 'none';
        }
    }

    document.getElementById('file-input').onchange = function(e) {
        const file = e.target.files[0];
        const reader = new FileReader();
        reader.onload = function(event) {
            base64Image = event.target.result.split(',')[1];
            const preview = document.getElementById('img-preview');
            preview.src = event.target.result;
            preview.style.display = 'block';
        };
        reader.readAsDataURL(file);
    };

    async function sendMessage() {
        const input = document.getElementById('user-input');
        const box = document.getElementById('chat-box');
        const text = input.value.trim();
        
        if (!text && !base64Image) return;

        // User display
        box.innerHTML += `<div class="message user">${text}</div>`;
        input.value = "";
        document.getElementById('img-preview').style.display = 'none';
        box.scrollTop = box.scrollHeight;

        const parts = [{ text: "তুমি শাহরিয়ার ভাইয়ের বানানো AI। উত্তর দাও: " + text }];
        if (base64Image) {
            parts.push({ inline_data: { mime_type: "image/jpeg", data: base64Image } });
        }

        try {
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ contents: [{ parts: parts }] })
            });

            const data = await response.json();
            const aiReply = data.candidates[0].content.parts[0].text;
            box.innerHTML += `<div class="message assistant">${aiReply}</div>`;
            base64Image = ""; // Reset image
        } catch (error) {
            box.innerHTML += `<div class="message assistant" style="color:red">দুঃখিত, কোনো সমস্যা হয়েছে। দয়া করে সঠিক API Key ব্যবহার করুন।</div>`;
        }
        box.scrollTop = box.scrollHeight;
    }
</script>

</body>
</html>
