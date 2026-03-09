<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Antim Smart Hub 2026</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --primary: #00f2ff; --bg: #05070a; --card: #111827; }
        body { font-family: 'Inter', sans-serif; background: var(--bg); color: white; margin: 0; padding: 15px; }
        
        .header { text-align: center; padding: 40px 0; }
        .header h1 { font-size: 2rem; color: var(--primary); text-transform: uppercase; letter-spacing: 2px; }
        .header p { color: #94a3b8; font-size: 0.9rem; }

        .container { max-width: 600px; margin: auto; display: flex; flex-direction: column; gap: 20px; }
        
        /* Modern Card Style */
        .tool-card { background: var(--card); padding: 20px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.05); box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .tool-card h3 { margin-top: 0; display: flex; align-items: center; gap: 10px; color: var(--primary); }

        /* Quick Notes App */
        #note-input { width: 100%; padding: 10px; background: #0b1120; border: 1px solid #334155; color: white; border-radius: 8px; outline: none; margin-bottom: 10px; }
        .note-item { background: #1e293b; padding: 10px; border-radius: 5px; margin-top: 5px; display: flex; justify-content: space-between; font-size: 0.9rem; }

        /* Photo Filter Tool */
        #upload-photo { display: none; }
        .upload-btn { display: block; text-align: center; padding: 15px; border: 2px dashed #334155; border-radius: 10px; cursor: pointer; transition: 0.3s; }
        .upload-btn:hover { border-color: var(--primary); }
        #preview-img { width: 100%; border-radius: 10px; margin-top: 15px; display: none; filter: contrast(1.2) brightness(1.1) saturate(1.3); }

        button { background: var(--primary); color: black; border: none; padding: 10px 20px; border-radius: 8px; font-weight: bold; cursor: pointer; transition: 0.3s; width: 100%; }
        button:hover { transform: scale(1.02); box-shadow: 0 0 15px var(--primary); }

        footer { text-align: center; padding: 40px; color: #475569; font-size: 0.8rem; }
    </style>
</head>
<body>

    <div class="header">
        <h1>Antim Smart Hub</h1>
        <p>Future Utility Tools • Generation 2026</p>
    </div>

    <div class="container">
        
        <div class="tool-card">
            <h3><i class="fas fa-wand-magic-sparkles"></i> AI Photo Enhancer</h3>
            <label for="upload-photo" class="upload-btn" id="label">
                <i class="fas fa-cloud-upload-alt"></i> ছবি সিলেক্ট করুন
            </label>
            <input type="file" id="upload-photo" accept="image/*">
            <img id="preview-img">
            <p style="font-size: 0.7rem; color: #64748b; margin-top: 10px;">*ছবিটি অটোমেটিক ২০২৬-এর সিনেম্যাটিক ফিল্টার পাবে।</p>
        </div>

        <div class="tool-card">
            <h3><i class="fas fa-list-check"></i> Quick Notes</h3>
            <input type="text" id="note-input" placeholder="জরুরি কিছু লিখে রাখুন...">
            <button onclick="addNote()">Save to Memory</button>
            <div id="note-list"></div>
        </div>

        <div class="tool-card">
            <h3><i class="fas fa-bolt"></i> Smart Unit Hub</h3>
            <div style="display: flex; gap: 10px;">
                <input type="number" id="val" placeholder="Value..." style="flex:1; padding: 10px; border-radius: 8px; background: #0b1120; border: 1px solid #334155; color: white;">
                <button onclick="convert()" style="flex:1;">Convert Now</button>
            </div>
            <p id="result" style="margin-top: 15px; font-weight: bold; text-align: center;"></p>
        </div>

    </div>

    <footer>
        &copy; 2026 Shahriar Hossain Antim. <br>
        Developed for Next-Gen Users.
    </footer>

    <script>
        // --- 1. Photo Filter logic ---
        const fileInput = document.getElementById('upload-photo');
        fileInput.onchange = (e) => {
            const file = e.target.files[0];
            const reader = new FileReader();
            reader.onload = (event) => {
                const img = document.getElementById('preview-img');
                img.src = event.target.result;
                img.style.display = 'block';
                document.getElementById('label').innerHTML = "ছবি আপলোড হয়েছে ✅";
            }
            reader.readAsDataURL(file);
        };

        // --- 2. Note logic (Save without Database) ---
        function loadNotes() {
            const notes = JSON.parse(localStorage.getItem('antim_notes') || '[]');
            const list = document.getElementById('note-list');
            list.innerHTML = "";
            notes.forEach((n, i) => {
                list.innerHTML += `<div class="note-item">${n} <i class="fas fa-trash" onclick="deleteNote(${i})" style="color:#ff4b4b; cursor:pointer;"></i></div>`;
            });
        }

        function addNote() {
            const input = document.getElementById('note-input');
            const notes = JSON.parse(localStorage.getItem('antim_notes') || '[]');
            if (input.value) {
                notes.push(input.value);
                localStorage.setItem('antim_notes', JSON.stringify(notes));
                input.value = "";
                loadNotes();
            }
        }

        function deleteNote(i) {
            const notes = JSON.parse(localStorage.getItem('antim_notes') || '[]');
            notes.splice(i, 1);
            localStorage.setItem('antim_notes', JSON.stringify(notes));
            loadNotes();
        }

        // --- 3. Simple Converter ---
        function convert() {
            const val = document.getElementById('val').value;
            if(!val) return;
            const res = (val * 10.7639).toFixed(2); // Example: Square meter to Sq Feet
            document.getElementById('result').innerText = val + " Sq Meter = " + res + " Sq Feet";
        }

        loadNotes();
    </script>
</body>
</html>
