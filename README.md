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
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">
    
    <!-- Librairie canvas-confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <style>
        /* --- RESET & VARIABLES CSS --- */
        :root {
            --bg-gradient: linear-gradient(135deg, #2b080e 0%, #4a0e17 40%, #1a0508 100%);
            --primary-pink: #ff758c;
            --accent-red: #d62828;
            --deep-burgundy: rgba(88, 24, 37, 0.75);
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

        /* --- ARRIÈRE-PLAN ANIMÉ --- */
        #bg-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }

        /* --- CONTENEUR PRINCIPAL --- */
        .main-container {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 90%;
            max-width: 800px;
            text-align: center;
        }

        /* --- ÉTAPE 1 : CŒUR CENTRAL & COMPTE À REBOURS --- */
        .heart-wrapper {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .heart-svg {
            width: 240px;
            height: 240px;
            fill: url(#heart-gradient);
            filter: drop-shadow(0 0 25px rgba(255, 117, 140, 0.6));
            animation: heartbeat 1.2s infinite ease-in-out;
        }

        .countdown-text {
            position: absolute;
            font-size: 4.5rem;
            font-weight: 600;
            color: var(--soft-white);
            text-shadow: 0 0 10px rgba(0, 0, 0, 0.5), 0 0 20px var(--gold);
            user-select: none;
            font-family: 'Montserrat', sans-serif;
        }

        @keyframes heartbeat {
            0% { transform: scale(1); }
            14% { transform: scale(1.12); }
            28% { transform: scale(1); }
            42% { transform: scale(1.12); }
            70% { transform: scale(1); }
        }

        .explode-animation {
            animation: explode 0.5s forwards ease-out !important;
        }

        @keyframes explode {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.6); opacity: 0.8; }
            100% { transform: scale(0); opacity: 0; }
        }

        /* --- ÉTAPE 3 : CARTE DE MESSAGE ROMANTIQUE --- */
        .message-card {
            display: none; /* Masqué au départ */
            opacity: 0;
            transform: translateY(30px) scale(0.95);
            background: var(--deep-burgundy);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(247, 208, 112, 0.4);
            border-radius: 24px;
            padding: 40px 30px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6),
                        0 0 30px rgba(255, 117, 140, 0.3);
            transition: opacity 1s ease, transform 1s ease;
            max-width: 700px;
            width: 100%;
        }

        .message-card.visible {
            display: block; /* Devient affiché */
        }

        .message-card.fade-in {
            opacity: 1;
            transform: translateY(0) scale(1);
        }

        .romantic-text {
            font-family: 'Dancing Script', cursive;
            font-size: 2.1rem;
            line-height: 1.6;
            color: var(--soft-white);
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.8);
        }

        .romantic-text .highlight {
            color: var(--gold);
            font-weight: 700;
        }

        .sub-emoji {
            font-size: 2.3rem;
            display: inline-block;
            vertical-align: middle;
            animation: floatEmoji 2s infinite ease-in-out;
        }

        @keyframes floatEmoji {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        /* --- RESPONSIVE DESIGN --- */
        @media (max-width: 600px) {
            .heart-svg {
                width: 180px;
                height: 180px;
            }

            .countdown-text {
                font-size: 3.5rem;
            }

            .message-card {
                padding: 25px 20px;
            }

            .romantic-text {
                font-size: 1.6rem;
                line-height: 1.5;
            }
        }
    </style>
</head>
<body>

    <!-- SVG Defs pour le dégradé du cœur -->
    <svg width="0" height="0" style="position:absolute;">
        <defs>
            <linearGradient id="heart-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#ff758c" />
                <stop offset="50%" stop-color="#d62828" />
                <stop offset="100%" stop-color="#800f2f" />
            </linearGradient>
        </defs>
    </svg>

    <!-- Canvas pour fond étoilé/animé -->
    <canvas id="bg-canvas"></canvas>

    <!-- Conteneur d'interaction principal -->
    <div class="main-container">
        
        <!-- Étape 1 : Le cœur central -->
        <div class="heart-wrapper" id="heart-btn">
            <svg class="heart-svg" viewBox="0 0 32 32">
                <path d="M16 28.5C15.4 28.5 14.8 28.2 14.4 27.8C8.3 21.9 4 17.8 2.2 14.3C0.2 10.5 0.9 6.1 3.9 3.3C6.3 1 9.9 0.6 13 2.3C14.2 3 15.2 4 16 5.2C16.8 4 17.8 3 19 2.3C22.1 0.6 25.7 1 28.1 3.3C31.1 6.1 31.8 10.5 29.8 14.3C28 17.8 23.7 21.9 17.6 27.8C17.2 28.2 16.6 28.5 16 28.5Z"/>
            </svg>
            <span class="countdown-text" id="countdown">3</span>
        </div>

        <!-- Étape 3 : Le Message Romantique -->
        <div class="message-card" id="message-card">
            <p class="romantic-text">
                Oups mon cœur il a explosé tellement tu est trop ravissante, tellement t’est magnifique tu me fait perdre tout mes moyens. Carrément je deviens incontrôlable à 2 doigt de faire une crise d’excès de beauté.<br><br>
                Je suis trop accroc à ta beauté magnifique comme de l’intérieur que l’extérieur que j’en perds tous mes moyens et que je suis à deux doigt d’exploser.<br><br>
                Je t’aime et je t’adore, je suis fan de toi <br>
                <span class="highlight">(est ce que je peux avoir un autographe de toi ? <span class="sub-emoji">🥺</span>)</span>
            </p>
        </div>

    </div>

    <script>
        /* --- 1. ARRIÈRE-PLAN ANIMÉ --- */
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');

        let width = canvas.width = window.innerWidth;
        let height = canvas.height = window.innerHeight;

        window.addEventListener('resize', () => {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        });

        class Particle {
            constructor() {
                this.reset();
            }

            reset() {
                this.x = Math.random() * width;
                this.y = Math.random() * height + height;
                this.size = Math.random() * 10 + 6;
                this.speedY = Math.random() * 0.8 + 0.3;
                this.speedX = Math.random() * 0.4 - 0.2;
                this.opacity = Math.random() * 0.5 + 0.2;
                this.isHeart = Math.random() > 0.4;
                this.color = `hsla(${Math.random() * 20 + 340}, 80%, 75%, ${this.opacity})`;
            }

            update() {
                this.y -= this.speedY;
                this.x += this.speedX;
                if (this.y < -20) this.reset();
            }

            draw() {
                ctx.fillStyle = this.color;
                if (this.isHeart) {
                    ctx.beginPath();
                    const topCurveHeight = this.size * 0.3;
                    ctx.moveTo(this.x, this.y + topCurveHeight);
                    ctx.bezierCurveTo(this.x, this.y, this.x - this.size / 2, this.y, this.x - this.size / 2, this.y + topCurveHeight);
                    ctx.bezierCurveTo(this.x - this.size / 2, this.y + (this.size + topCurveHeight) / 2, this.x, this.y + this.size, this.x, this.y + this.size);
                    ctx.bezierCurveTo(this.x, this.y + this.size, this.x + this.size / 2, this.y + (this.size + topCurveHeight) / 2, this.x + this.size / 2, this.y + topCurveHeight);
                    ctx.bezierCurveTo(this.x + this.size / 2, this.y, this.x, this.y, this.x, this.y + topCurveHeight);
                    ctx.closePath();
                    ctx.fill();
                } else {
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size / 4, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
        }

        const particles = Array.from({ length: 40 }, () => new Particle());

        function animateBG() {
            ctx.clearRect(0, 0, width, height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateBG);
        }
        animateBG();

        /* --- 2. COMPTE À REBOURS ET AFFICHAGE --- */
        const countdownEl = document.getElementById('countdown');
        const heartBtn = document.getElementById('heart-btn');
        const messageCard = document.getElementById('message-card');

        let count = 3;

        // Démarrage automatique
        const timer = setInterval(() => {
            count--;
            if (count > 0) {
                countdownEl.textContent = count;
            } else {
                clearInterval(timer);
                countdownEl.textContent = "0";
                triggerExplosion();
            }
        }, 1000);

        function triggerExplosion() {
            // Effet d'explosion du cœur central
            heartBtn.classList.add('explode-animation');

            // Confettis cœurs
            if (typeof confetti === 'function') {
                const heartShape = confetti.shapeFromPath({
                    path: 'M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z'
                });

                confetti({
                    particleCount: 100,
                    spread: 90,
                    origin: { y: 0.5 },
                    colors: ['#ff758c', '#d62828', '#f7d070', '#ffffff'],
                    shapes: [heartShape],
                    scalar: 2
                });
            }

            // Masquer le cœur et afficher la carte du message
            setTimeout(() => {
                heartBtn.style.display = 'none';
                
                // 1. Activer le bloc dans le DOM
                messageCard.classList.add('visible');
                
                // 2. Lancer l'animation de fondu
                setTimeout(() => {
                    messageCard.classList.add('fade-in');
                }, 50);

            }, 400);
        }
    </script>
</body>
</html>
