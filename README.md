# iyiki-do-udun-babam-icin
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>İYİ Kİ DOĞDUN KRAL!</title>
    <style>
        /* Arka planı tamamen karanlık ve gizemli yapıyoruz ki efektler patlasın */
        body {
            background-color: #050510;
            color: white;
            font-family: 'Arial Black', Gadget, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        /* Tüm içeriği tutan ana kutu */
        .card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 2px solid #ffd700;
            padding: 40px 20px;
            border-radius: 25px;
            box-shadow: 0 0 30px #ffd700, inset 0 0 20px rgba(255,215,0,0.2);
            max-width: 90%;
            width: 450px;
            z-index: 10;
            animation: nefes 3s ease-in-out infinite alternate;
        }

        /* Kartın hafifçe parlayıp sönme efekti */
        @keyframes nefes {
            0% { box-shadow: 0 0 20px #ff007f; border-color: #ff007f; }
            100% { box-shadow: 0 0 40px #ffd700; border-color: #ffd700; }
        }

        /* Abartılı Neon Başlık */
        h1 {
            font-size: 2.5rem;
            text-transform: uppercase;
            color: #fff;
            text-shadow: 0 0 10px #fff, 0 0 20px #ffd700, 0 0 40px #ffd700, 0 0 80px #ffd700;
            margin-bottom: 10px;
            animation: titreme 1.5s infinite alternate;
        }

        @keyframes titreme {
            0% { transform: scale(0.98); }
            100% { transform: scale(1.02); }
        }

        .sub-title {
            color: #00ffff;
            font-size: 1.5rem;
            text-shadow: 0 0 10px #00ffff;
            margin-bottom: 30px;
        }

        p {
            font-size: 1.1rem;
            line-height: 1.8;
            font-family: 'Segoe UI', sans-serif;
            font-weight: bold;
            color: #e0e0e0;
        }

        /* Altın Sarısı Devasa Buton */
        .btn {
            background: linear-gradient(45deg, #ffd700, #ff8c00);
            color: black;
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-size: 1.3rem;
            font-weight: bold;
            text-decoration: none;
            display: inline-block;
            margin-top: 25px;
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.4);
            transition: 0.3s;
            cursor: pointer;
        }

        .btn:active {
            transform: scale(0.95);
        }

        /* Arka plandaki havai fişek canvası */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }
    </style>
</head>
<body>

    <canvas id="canvas"></canvas>

    <div class="card">
        <h1>🎂 İYİ Kİ DOĞDUN 🎂</h1>
        <div class="sub-title">DÜNYANIN EN KRAL BABASI! 👑</div>
        
        <p>Gölgen yeter reis! Hayatımızın neşesi, ailemizin yıkılmaz direği, canım babam... Yeni yaşın senin gibi muhteşem, enerjik ve sağlık dolu geçsin!</p>
        <p>İyi ki varsın, iyi ki bizim babamızsın. Seni çok ama çok seviyoruz! ❤️</p>
        
        <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" class="btn">TIKLA VE SÜRPRİZİ GÖR! 🔥</a>
    </div>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor(x, y, color) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.radius = Math.random() * 3 + 1;
                this.upVelocity = Math.random() * 5 + 2;
                this.velocity = {
                    x: Math.random() * 6 - 3,
                    y: Math.random() * 6 - 3
                };
                this.alpha = 1;
                this.friction = 0.98;
                this.gravity = 0.2;
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.alpha;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
                ctx.fillStyle = this.color;
                ctx.fill();
                ctx.restore();
            }

            update() {
                this.velocity.x *= this.friction;
                this.velocity.y *= this.friction;
                this.velocity.y += this.gravity;
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                this.alpha -= 0.01;
            }
        }

        let particles = [];
        const colors = ['#ff007f', '#00ffff', '#ffd700', '#00ff00', '#ff8c00', '#ff00ff'];

        function spawnFirework() {
            const x = Math.random() * canvas.width;
            const y = Math.random() * (canvas.height / 2);
            const color = colors[Math.floor(Math.random() * colors.length)];
            
            for (let i = 0; i < 40; i++) {
                particles.push(new Particle(x, y, color));
            }
        }

        // Sürekli havai fişek patlat
        setInterval(spawnFirework, 800);

        function animate() {
            ctx.fillStyle = 'rgba(5, 5, 16, 0.2)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            particles.forEach((particle, index) => {
                if (particle.alpha <= 0) {
                    particles.splice(index, 1);
                } else {
                    particle.update();
                    particle.draw();
                }
            });

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
