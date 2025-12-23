


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎄 Real-Time Christmas Public Wall 🎅</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Mountains+of+Christmas:wght@700&display=swap" rel="stylesheet">
    
    <style>
        /* --- CSS STYLING --- */
        :root {
            /* Warna khas Natal */
            --bg-christmas: #0a2e1c; /* Hijau Pinus Gelap */
            --primary-red: #c41e3a;
            --snow-white: #ffffff;
            --gold: #ffd700;
        }

        body {
            font-family: 'Poppins', sans-serif;
            /* Latar belakang Gradasi & Gambar (Snowy Night) */
            background: linear-gradient(rgba(10, 46, 28, 0.8), rgba(10, 46, 28, 0.9)), 
                        url('https://images.unsplash.com/photo-1482517967863-00e15c9b44be?auto=format&fit=crop&q=80&w=2070');
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            color: white;
            overflow-x: hidden;
        }

        h1 {
            font-family: 'Mountains of Christmas', cursive;
            font-size: 3rem;
            color: var(--snow-white);
            text-shadow: 2px 2px 10px rgba(0,0,0,0.5);
            margin-bottom: 20px;
            text-align: center;
        }

        /* Form Styling */
        .input-container {
            background: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            width: 100%;
            max-width: 500px;
            margin-bottom: 30px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            border: 3px solid var(--primary-red);
        }

        input, textarea {
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-family: 'Poppins', sans-serif;
            font-size: 14px;
        }

        button {
            background-color: var(--primary-red);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 1.1em;
            transition: all 0.3s;
            box-shadow: 0 4px 0 #801026;
        }

        button:hover {
            background-color: #a01830;
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(2px);
            box-shadow: 0 0px 0 #801026;
        }

        /* Notes Grid Styling */
        .notes-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            width: 100%;
            max-width: 1200px;
            z-index: 2;
        }

        .note-card {
            width: 250px;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 5px 5px 15px rgba(0,0,0,0.3);
            position: relative;
            animation: fadeIn 0.5s ease-in;
            transform: rotate(-1deg);
            transition: transform 0.2s;
            word-wrap: break-word;
            color: #333;
        }

        /* Variasi Warna Card Natal */
        .note-card:nth-child(4n+1) { background-color: #fff740; transform: rotate(-1deg); } /* Kuning */
        .note-card:nth-child(4n+2) { background-color: #ff4d4d; color: white; transform: rotate(2deg); } /* Merah */
        .note-card:nth-child(4n+3) { background-color: #2e7d32; color: white; transform: rotate(-2deg); } /* Hijau */
        .note-card:nth-child(4n+4) { background-color: #ffffff; transform: rotate(1deg); } /* Putih Salju */

        .note-card:hover {
            transform: scale(1.1) rotate(0deg);
            z-index: 10;
        }

        .note-header {
            font-weight: 600;
            font-size: 0.95em;
            margin-bottom: 8px;
            border-bottom: 1px solid rgba(0,0,0,0.1);
            padding-bottom: 5px;
        }

        .timestamp {
            font-size: 0.7em;
            margin-top: 15px;
            text-align: right;
            opacity: 0.7;
        }

        /* Efek Salju Sederhana */
        .snowflakes {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="snowflakes" aria-hidden="true">
        <div style="position: absolute; top: -10%; left: 10%; color: white; font-size: 20px; animation: fall 10s linear infinite;">❄</div>
        <div style="position: absolute; top: -10%; left: 30%; color: white; font-size: 25px; animation: fall 12s linear infinite 2s;">❅</div>
        <div style="position: absolute; top: -10%; left: 50%; color: white; font-size: 18px; animation: fall 15s linear infinite 1s;">❆</div>
        <div style="position: absolute; top: -10%; left: 70%; color: white; font-size: 22px; animation: fall 11s linear infinite 3s;">❄</div>
        <div style="position: absolute; top: -10%; left: 90%; color: white; font-size: 24px; animation: fall 14s linear infinite 0.5s;">❅</div>
    </div>

    <style>
        @keyframes fall {
            to { transform: translateY(110vh) rotate(360deg); }
        }
    </style>

    <h1>🎄 Public Wall Notes 🎅</h1>

    <div class="input-container">
        <input type="text" id="username" placeholder="Nama Anda (Contoh: Santa)">
        <textarea id="noteText" placeholder="Tulis ucapan Natal atau pesan anda di sini..."></textarea>
        <button onclick="postNote()">🎁 Tempel Catatan</button>
    </div>

    <div class="notes-grid" id="notesBoard">
        <p style="color: white; width: 100%; text-align: center;" id="loadingText">Menyiapkan kado... (Menunggu koneksi)</p>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // CONFIG FIREBASE (Tetap menggunakan config milikmu)
        const firebaseConfig = {
            apiKey: "AIzaSyDplfPgqi9MMIlWp5f7OEtoGQoPHbf8kF0",
            authDomain: "database-notes-98ce3.firebaseapp.com",
            databaseURL: "https://database-notes-98ce3-default-rtdb.firebaseio.com",
            projectId: "database-notes-98ce3",
            storageBucket: "database-notes-98ce3.firebasestorage.app",
            messagingSenderId: "421315329256",
            appId: "1:421315329256:web:6ac6ca6e92437350b59d5d",
            measurementId: "G-YH0GLXZMM7"
        };

        let app, db;
        try {
            app = initializeApp(firebaseConfig);
            db = getDatabase(app);
            document.getElementById('loadingText').innerText = "Siap merayakan Natal!";
        } catch (e) {
            console.error(e);
            document.getElementById('loadingText').innerText = "Gagal memuat suasana Natal.";
        }

        window.postNote = function() {
            const usernameInput = document.getElementById('username');
            const noteInput = document.getElementById('noteText');
            const user = usernameInput.value.trim() || "Secret Santa";
            const text = noteInput.value.trim();

            if (text === "") {
                alert("Isi pesan tidak boleh kosong!");
                return;
            }

            push(ref(db, 'notes'), {
                user: user,
                message: text,
                timestamp: Date.now()
            }).then(() => {
                noteInput.value = "";
            }).catch((error) => {
                alert("Gagal mengirim: " + error.message);
            });
        }

        if(db) {
            const notesRef = ref(db, 'notes');
            const board = document.getElementById('notesBoard');

            onValue(notesRef, (snapshot) => {
                board.innerHTML = "";
                const data = snapshot.val();

                if (!data) {
                    board.innerHTML = "<p>Belum ada ucapan. Ayo mulai berbagi kebahagiaan!</p>";
                    return;
                }

                const notesArray = Object.values(data).sort((a, b) => b.timestamp - a.timestamp);

                notesArray.forEach(note => {
                    const date = new Date(note.timestamp).toLocaleString('id-ID');
                    const noteElement = document.createElement('div');
                    noteElement.className = 'note-card';
                    noteElement.innerHTML = `
                        <div class="note-header">
                            <span>👤 ${escapeHtml(note.user)}</span>
                        </div>
                        <div class="note-content">
                            ${escapeHtml(note.message)}
                        </div>
                        <div class="timestamp">📅 ${date}</div>
                    `;
                    board.appendChild(noteElement);
                });
            });
        }

        function escapeHtml(text) {
            return text
                .replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        document.getElementById('noteText').addEventListener('keypress', function (e) {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                window.postNote();
            }
        });
    </script>
</body>
