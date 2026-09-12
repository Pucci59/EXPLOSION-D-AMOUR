# EXPLOSION-D-AMOUR
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pour Toi ❤️</title>
    
    <!-- Polices Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Montserrat:wght@400;600&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #2b080e 0%, #4a0e17 40%, #1a0508 100%);
            --gold: #f7d070;
            --soft-white: #fff5f5;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            background: var(--bg-gradient);
            font-family: 'Montserrat', sans-serif;
            color: var(--soft-white);
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* Canvas pour fond étoilé */
        #bg-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }

        .main-container {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 90%;
            max-width: 700px;
            text-align: center;
        }

        /* Cœur Central */
        .heart-wrapper {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
        }

        .heart-svg {
            width: 220px;
            height: 220px;
            fill: #d62828;
            filter: drop-shadow(0 0 25px rgba(255, 117, 140, 0.8));
            animation: heartbeat 1.2s infinite ease-in-out;
        }

        .countdown-text {
            position: absolute;
            font-size: 4rem;
            font-weight: 700;
            color: #ffffff;
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
            user-select: none;
        }

        .click-hint {
            position: absolute;
            bottom: -40px;
            font-size: 0.9rem;
            color: var(--gold);
            letter-spacing: 1px;
            white-space: nowrap;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            14% { transform: scale(1.1); }
            28% { transform: scale(1); }
            42% { transform: scale(1.1); }
            70% { transform: scale(1); }
        }

        /* Animation d'explosion */
        .explode {
            animation: explodeAnim 0.6s forwards ease-out !important;
        }

        @keyframes explodeAnim {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.8); opacity: 0.8; }
            100% { transform: scale(0); opacity: 0; }
        }

        /* Message Carte */
        .message-card {
            background: rgba(88, 24, 37, 0.85);
            border: 2px solid rgba(247, 208, 112, 0.5);
            border-radius: 20px;
            padding: 35px 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6);
            width: 100%;
            max-width: 650px;
            
            /* Masqué par défaut */
            display: none;
            opacity: 0;
            transform: scale(0.8);
            transition: all 0.8s ease-out;
        }

        .message-card.show {
            display: block !important;
            opacity: 1 !important;
            transform: scale(1) !important;
        }

        .romantic-text {
            font-family: 'Dancing Script', cursive;
            font-size: 2rem;
            line-height: 1.6;
            color: #fff;
        }

        .highlight {
            color: var(--gold);
            font-weight: bold;
        }

        .emoji {
            font-size: 2.2rem;
            display: inline-block;
            animation: floatEmoji 2s infinite ease-in-out;
        }

        @keyframes floatEmoji {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-6px); }
        }

        @media (max-width: 600px) {
            .romantic-text {
                font-size: 1.55rem;
                line-height: 1.5;
            }
            .heart-svg {
                width: 170px;
                height: 170px;
            }
            .countdown-text {
                font-size: 3rem;
            }
        }
    </style>
</head>
<body>

    <canvas id="bg-canvas"></canvas>

    <div class="main-container">
        
        <!-- Étape 1 : Cœur & Compte à rebours -->
        <div class="heart-wrapper" id="heart-btn" onclick="startCountdown()">
            <svg class="heart-svg" viewBox="0 0 32 32">
                <path d="M16 28.5C15.4 28.5 14.8 28.2 14.4 27.8C8.3 21.9 4 17.8 2.2 14.3C0.2 10.5 0.9 6.1 3.9 3.3C6.3 1 9.9 0.6 13 2.3C14.2 3 15.2 4 16 5.2C16.8 4 17.8 3 19 2.3C22.1 0.6 25.7 1 28.1 3.3C31.1 6.1 31.8 10.5 29.8 14.3C28 17.8 23.7 21.9 17.6 27.8C17.2 28.2 16.6 28.5 16 28.5Z"/>
            </svg>
            <span class="countdown-text" id="countdown">3</span>
            <span class="click-hint" id="hint">Clique sur le cœur pour démarrer ❤️</span>
        </div>

        <!-- Étape 2 : Le Message -->
        <div class="message-card" id="message-card">
            <p class="romantic-text">
                Oups mon cœur il a explosé tellement tu est trop ravissante, tellement t’est magnifique tu me fait perdre tout mes moyens. Carrément je deviens incontrôlable à 2 doigt de faire une crise d’excès de beauté.<br><br>
                Je suis trop accroc à ta beauté magnifique comme de l’intérieur que l’extérieur que j’en perds tous mes moyens et que je suis à deux doigt d’exploser.<br><br>
                Je t’aime et je t’adore, je suis fan de toi <br>
                <span class="highlight">(est ce que je peux avoir un autographe de toi ? <span class="emoji">🥺</span>)</span>
            </p>
        </div>

    </div>

    <!-- Script Purement JS (Sans librairie externe) -->
    <script>
        // 1. Fond étoilé animé
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let width = canvas.width = window.innerWidth;
        let height = canvas.height = window.innerHeight;

        window.addEventListener('resize', () => {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        });

        const stars = Array.from({ length: 50 }, () => ({
            x: Math.random() * width,
            y: Math.random() * height,
            size: Math.random() * 3 + 1,
            alpha: Math.random(),
            speed: Math.random() * 0.02 + 0.005
        }));

        function drawStars() {
            ctx.clearRect(0, 0, width, height);
            stars.forEach(s => {
                s.alpha += s.speed;
                if (s.alpha > 1 || s.alpha < 0) s.speed = -s.speed;
                ctx.fillStyle = `rgba(255, 245, 245, ${Math.abs(s.alpha)})`;
                ctx.beginPath();
                ctx.arc(s.x, s.y, s.size, 0, Math.PI * 2);
                ctx.fill();
            });
            requestAnimationFrame(drawStars);
        }
        drawStars();

        // 2. Gestion de l'interaction et du compte à rebours
        let started = false;

        function startCountdown() {
            if (started) return;
            started = true;

            document.getElementById('hint').style.display = 'none';

            let count = 3;
            const countdownEl = document.getElementById('countdown');
            const heartBtn = document.getElementById('heart-btn');
            const messageCard = document.getElementById('message-card');

            const interval = setInterval(() => {
                count--;
                if (count > 0) {
                    countdownEl.textContent = count;
                } else {
                    clearInterval(interval);
                    countdownEl.textContent = "0";

                    // Animation d'explosion
                    heartBtn.classList.add('explode');

                    // Affichage direct du message après l'explosion
                    setTimeout(() => {
                        heartBtn.style.display = 'none';
                        messageCard.classList.add('show');
                    }, 500);
                }
            }, 1000);
        }
    </script>
</body>
</html>
