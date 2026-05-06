<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>For My Pari ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #ff4d6d;
            --soft-pink: #fff0f3;
            --dark-pink: #c9184a;
            --bg-gradient: linear-gradient(180deg, #fff0f3 0%, #ffccd5 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: var(--bg-gradient);
            height: 100dvh; /* Dynamic height for mobile browsers */
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Floating Hearts Background */
        .hearts-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .heart {
            position: absolute;
            color: var(--primary-pink);
            opacity: 0.6;
            animation: float 4s linear infinite;
            font-size: 20px;
        }

        @keyframes float {
            0% { transform: translateY(105vh) scale(0); opacity: 1; }
            100% { transform: translateY(-10vh) scale(1.5); opacity: 0; }
        }

        /* Main Card */
        .scene {
            display: none;
            width: 85%;
            max-width: 350px;
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 25px;
            box-shadow: 0 10px 25px rgba(255, 77, 109, 0.2);
            text-align: center;
            z-index: 10;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            max-height: 80dvh;
            overflow-y: auto;
        }

        @keyframes popIn {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .active { display: block; }

        h1 {
            font-family: 'Dancing Script', cursive;
            color: var(--dark-pink);
            font-size: 2.2rem;
            margin-bottom: 15px;
        }

        p {
            font-size: 1rem;
            color: #444;
            line-height: 1.5;
            margin-bottom: 20px;
        }

        /* Mobile Buttons */
        .btn-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
            align-items: center;
        }

        .btn {
            background-color: var(--primary-pink);
            color: white;
            border: none;
            width: 100%;
            padding: 15px;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 15px;
            cursor: pointer;
            transition: transform 0.2s;
            box-shadow: 0 5px 15px rgba(255, 77, 109, 0.3);
        }

        .btn:active {
            transform: scale(0.95);
        }

        #no-btn {
            background-color: #adb5bd;
            position: relative;
        }

        /* Letter Box */
        .letter-content {
            font-family: 'Dancing Script', cursive;
            font-size: 1.3rem;
            text-align: left;
            color: #333;
            white-space: pre-wrap;
            line-height: 1.4;
            margin-bottom: 10px;
        }

        .flower {
            font-size: 1.5rem;
            display: block;
            margin: 10px 0;
        }

        /* Custom Scrollbar for the Letter */
        .scene::-webkit-scrollbar {
            width: 4px;
        }
        .scene::-webkit-scrollbar-thumb {
            background: var(--primary-pink);
            border-radius: 10px;
        }

    </style>
</head>
<body>

    <div class="hearts-container" id="hearts"></div>

    <!-- Scene 1: Welcome -->
    <div id="scene1" class="scene active">
        <div style="font-size: 4rem; margin-bottom: 10px;">💌</div>
        <h1>Hi Beautiful</h1>
        <p>I have a little something for you. Will you open it?</p>
        <button class="btn" onclick="nextScene(2)">Click to begin</button>
    </div>

    <!-- Scene 2: The Question -->
    <div id="scene2" class="scene">
        <h1>Hey Pari... ❤️</h1>
        <p>Do you want to see what I made for you?</p>
        <div class="btn-container">
            <button class="btn" onclick="nextScene(3)">Yes, I do! 😍</button>
            <button class="btn" id="no-btn" ontouchstart="moveNoButton()" onclick="moveNoButton()">No 😢</button>
        </div>
    </div>

    <!-- Scene 3: The Love Letter -->
    <div id="scene3" class="scene">
        <h1>My Everything ❤️</h1>
        <div id="letter-text" class="letter-content"></div>
        <button class="btn" style="margin-top: 20px; display: none;" id="restart-btn" onclick="location.reload()">Read again? ✨</button>
    </div>

    <script>
        // 1. Mobile Heart Generator
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = ['❤️', '💖', '🌸', '✨'][Math.floor(Math.random() * 4)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 2 + 3) + 's';
            document.getElementById('hearts').appendChild(heart);
            setTimeout(() => heart.remove(), 4000);
        }
        setInterval(createHeart, 400);

        // 2. Scene Navigation
        function nextScene(sceneNumber) {
            document.querySelectorAll('.scene').forEach(s => s.classList.remove('active'));
            document.getElementById('scene' + sceneNumber).classList.add('active');
            
            if(sceneNumber === 3) {
                setTimeout(startTyping, 500);
            }
        }

        // 3. Dodge Button Logic (Mobile Friendly)
        function moveNoButton() {
            const btn = document.getElementById('no-btn');
            // Keep button within screen bounds
            const maxX = window.innerWidth - btn.offsetWidth - 40;
            const maxY = window.innerHeight - btn.offsetHeight - 40;
            
            const randomX = Math.max(20, Math.floor(Math.random() * maxX));
            const randomY = Math.max(20, Math.floor(Math.random() * maxY));
            
            btn.style.position = 'fixed';
            btn.style.left = randomX + 'px';
            btn.style.top = randomY + 'px';
            btn.style.width = 'auto';
            btn.style.padding = '10px 25px';
        }

        // 4. Typing Animation
        const message = `Dearest Pari ❤️

Maybe I can’t always express my feelings the way I truly want to… but one thing will always remain true—

You became one of the most beautiful parts of my life. 🌸

Your smile makes even my hardest days feel lighter, and your presence brings a kind of peace my heart never knew before.

I made this little website just to remind you how deeply loved you are… more than words could ever fully explain. 💞

No matter how busy life gets, how difficult days become, or how many challenges come our way… I will always care for you, support you, and stand beside you.

You are my happiness, my comfort, my favorite notification, and the safest feeling I’ve ever known. ❤️✨

forever yours,
Piyush`;

        let i = 0;
        function startTyping() {
            const letterDiv = document.getElementById("letter-text");
            const sceneDiv = document.getElementById("scene3");
            
            if (i < message.length) {
                letterDiv.innerHTML += message.charAt(i);
                i++;
                // Scroll down automatically as text types
                sceneDiv.scrollTop = sceneDiv.scrollHeight;
                setTimeout(startTyping, 40);
            } else {
                document.getElementById('restart-btn').style.display = 'block';
            }
        }
    </script>
</body>
</html>
