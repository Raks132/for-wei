# for-wei
confessiin
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Wei ♡</title>
    <style>
        :root {
            --soft-pink: #ffe4e1;
            --accent-pink: #ffb6c1;
            --text-color: #5d4037;
        }
        body, html {
            margin: 0; padding: 0;
            width: 100%; height: 100%;
            overflow: hidden;
            background-color: var(--soft-pink);
            font-family: 'Georgia', serif;
            color: var(--text-color);
            transition: background 2s ease;
        }

        /* RAINBOW BACKGROUND */
        .rainbow-bg {
            background: linear-gradient(124deg, #ff2400, #e81d1d, #e8b71d, #1de840, #1ddde8, #2b1de8, #dd00f3, #dd00f3);
            background-size: 1600% 1600%;
            animation: rainbowMove 10s ease infinite;
        }
        @keyframes rainbowMove {
            0% {background-position: 0% 82%}
            50% {background-position: 100% 19%}
            100% {background-position: 0% 82%}
        }

        .heart {
            position: absolute;
            font-size: 20px;
            user-select: none;
            pointer-events: none;
            animation: fall linear forwards;
            z-index: 1;
        }
        @keyframes fall { to { transform: translateY(110vh); } }

        .side-emoji {
            position: fixed;
            font-size: 35px;
            pointer-events: none;
            z-index: 99;
            animation: fly-up 1.5s ease-out forwards;
        }
        @keyframes fly-up {
            0% { transform: translateY(0) scale(0.5); opacity: 1; }
            100% { transform: translateY(-300px) scale(2); opacity: 0; }
        }

        .slide {
            position: absolute;
            width: 100%; height: 100%;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            text-align: center;
            padding: 20px; box-sizing: border-box;
            transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.5s ease;
            z-index: 2;
        }
        .hidden { transform: translateX(100%); }
        .past { transform: translateX(-100%); }
        .fade-out { opacity: 0; pointer-events: none; }

        .content-box {
            background: rgba(255, 255, 255, 0.6);
            backdrop-filter: blur(10px);
            padding: 40px;
            border-radius: 30px;
            max-width: 500px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            border: 1px solid rgba(255,255,255,0.8);
        }

        h1 { font-size: 2.5rem; margin-bottom: 20px; color: #db7093; }
        p { font-size: 1.2rem; line-height: 1.6; margin-bottom: 30px; }

        .btn {
            background: white;
            color: #db7093;
            border: 2px solid #db7093;
            padding: 12px 30px;
            border-radius: 50px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.3s;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        .btn:hover { background: #db7093; color: white; transform: scale(1.05); }

        #surprise-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            display: none;
            flex-direction: column;
            align-items: center; justify-content: center;
            z-index: 100;
        }
        #surprise-text { 
            font-size: 3.5rem; 
            color: white; 
            font-weight: bold; 
            text-align: center;
            text-shadow: 2px 2px 15px rgba(0,0,0,0.5);
        }

        .surprise-btn {
            background: #ff1493 !important;
            color: white !important;
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.1); } }

        /* The "NO" button trickery */
        #noBtn {
            position: relative;
            transition: all 0.2s ease;
        }
    </style>
</head>
<body>

    <audio id="bgMusic" loop preload="auto">
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg">
    </audio>

    <div class="slide" id="slide1">
        <div class="content-box">
            <h1>Hi Wei... ♡</h1>
            <p>I have something I've wanted to tell you for a long time. Will you listen?</p>
            <button class="btn" onclick="startExperience()">Continue to Read</button>
        </div>
    </div>

    <div class="slide hidden" id="slide2">
        <div class="content-box">
            <p>I still remember the Intramurals. Seeing you play so well... I searched your name on Facebook just to add you.</p>
            <button class="btn" onclick="triggerNext(2)">Continue</button>
        </div>
    </div>

    <div class="slide hidden" id="slide3">
        <div class="content-box">
            <p>You're smart, athletic, and 10/10 beautiful. I love our CODM games, kahit hindi ka nag mmic -,- .</p>
            <button class="btn" onclick="triggerNext(3)">Keep Reading</button>
        </div>
    </div>

    <div class="slide hidden" id="slide4">
        <div class="content-box">
            <p>I've been waiting for a chance for us to know each other better. I accept everything about you, because to me, you're perfect.</p>
            <button class="btn" onclick="triggerNext(4)">Almost there...</button>
        </div>
    </div>

    <div class="slide hidden" id="slide5">
        <div class="content-box">
            <h1>Before I go...</h1>
            <p>I have one last thing to show you. It's a bit of a surprise.</p>
            <button class="btn surprise-btn" onclick="showSurprise()">Click for a Surprise ✨</button>
        </div>
    </div>

    <div id="surprise-overlay">
        <div id="surprise-text">I REALLY LIKE YOU, WEI! ❤️</div>
        <p style="color: white; font-size: 1.5rem; margin-top: 20px;">Give me a chance to prove it?</p>
        <div style="margin-top: 30px;">
            <button class="btn" onclick="alert('You made me the happiest person! ❤️')">YES</button>
            <button class="btn" id="noBtn" onmouseover="moveNo()" onclick="moveNo()">NO</button>
        </div>
    </div>

    <script>
        const audio = document.getElementById('bgMusic');
        let isRainbow = false;

        function startExperience() {
            audio.volume = 0.5;
            audio.play().catch(e => console.log("Audio play blocked"));
            triggerNext(1);
        }

        function triggerNext(num) {
            popEmojis();
            nextSlide(num);
        }

        function nextSlide(num) {
            document.getElementById('slide' + num).classList.add('past');
            const next = document.getElementById('slide' + (num + 1));
            if(next) next.classList.remove('hidden');
        }

        function popEmojis() {
            const emojis = ['💕', '💘', '🩷'];
            for(let i=0; i<8; i++) {
                const e = document.createElement('div');
                e.className = 'side-emoji';
                e.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                const side = Math.random() > 0.5 ? 'left' : 'right';
                e.style[side] = (Math.random() * 60 + 20) + 'px';
                e.style.bottom = '100px';
                document.body.appendChild(e);
                setTimeout(() => e.remove(), 1500);
            }
        }

        setInterval(() => {
            const h = document.createElement('div');
            h.className = 'heart';
            h.innerHTML = '❤';
            h.style.left = Math.random() * 100 + 'vw';
            h.style.animationDuration = Math.random() * 3 + 2 + 's';
            h.style.color = isRainbow ? `hsl(${Math.random() * 360}, 100%, 70%)` : '#ffb6c1';
            document.body.appendChild(h);
            setTimeout(() => h.remove(), 5000);
        }, 200);

        function showSurprise() {
            // Fade out Music
            let fadeOut = setInterval(() => {
                if (audio.volume > 0.05) audio.volume -= 0.05;
                else { audio.pause(); clearInterval(fadeOut); }
            }, 100);

            document.getElementById('slide5').classList.add('fade-out');
            isRainbow = true;
            document.body.classList.add('rainbow-bg');
            setTimeout(() => {
                document.getElementById('surprise-overlay').style.display = 'flex';
            }, 500);
        }

        // Unlimited "NO" Button escapes
        function moveNo() {
            const btn = document.getElementById('noBtn');
            const x = Math.random() * (window.innerWidth - btn.offsetWidth - 20);
            const y = Math.random() * (window.innerHeight - btn.offsetHeight - 20);
            
            btn.style.position = 'fixed';
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';
        }
    </script>
</body>
</html>
