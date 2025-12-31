<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>رسالة حب لجنة 💖</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
            background: linear-gradient(to bottom, #ffdde1, #ee9ca7);
            color: #fff;
            text-align: center;
            overflow: hidden;
        }

        h1 {
            font-size: 3em;
            margin-top: 50px;
            animation: fadeIn 2s ease-in-out;
        }

        h2 {
            font-size: 2em;
            margin: 20px 0;
            animation: fadeIn 3s ease-in-out;
        }

        p {
            font-size: 1.2em;
            margin: 10px 20px;
            animation: fadeIn 4s ease-in-out;
        }

        .heart {
            font-size: 5em;
            color: #ff4d6d;
            animation: beat 1s infinite;
        }

        audio {
            margin-top: 30px;
        }

        @keyframes beat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.3); }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px);}
            to { opacity: 1; transform: translateY(0);}
        }

        .fireworks {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
    </style>
</head>
<body>
    <h1>سنة جديدة سعيدة يا <span>جنة 💖</span></h1>
    <h2>من محمد لك بكل الحب 😘</h2>
    <p>كل عام وأنتِ بخير، يا أجمل حاجة في حياتي</p>
    <div class="heart">❤️</div>

    <audio controls autoplay loop>
        <source src="https://www.example.com/alhob_jani_tulip.mp3" type="audio/mpeg">
        متصفحك لا يدعم تشغيل الموسيقى.
    </audio>

    <canvas class="fireworks"></canvas>

    <script>
        // Simple fireworks effect
        const canvas = document.querySelector('.fireworks');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let fireworks = [];
        function random(min, max) { return Math.random() * (max - min) + min; }

        class Firework {
            constructor() {
                this.x = random(0, canvas.width);
                this.y = canvas.height;
                this.targetY = random(50, canvas.height/2);
                this.color = `hsl(${random(0, 360)}, 100%, 50%)`;
                this.particles = [];
            }
            update() {
                this.y -= 4;
                if(this.y <= this.targetY) {
                    for(let i=0;i<50;i++){
                        this.particles.push(new Particle(this.x, this.y, this.color));
                    }
                    return true;
                }
                return false;
            }
        }

        class Particle {
            constructor(x, y, color) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.vx = random(-5,5);
                this.vy = random(-5,5);
                this.alpha = 1;
            }
            update() {
                this.x += this.vx;
                this.y += this.vy;
                this.alpha -= 0.02;
            }
        }

        let particles = [];
        function animate(){
            ctx.fillStyle = 'rgba(0,0,0,0.1)';
            ctx.fillRect(0,0,canvas.width,canvas.height);

            if(Math.random() < 0.05){
                fireworks.push(new Firework());
            }

            fireworks.forEach((fw, i)=>{
                if(fw.update()) fireworks.splice(i,1);
                fw.particles.forEach((p, j)=>{
                    p.update();
                    ctx.fillStyle = `hsla(${random(0,360)},100%,50%,${p.alpha})`;
                    ctx.beginPath();
                    ctx.arc(p.x,p.y,2,0,Math.PI*2);
                    ctx.fill();
                    if(p.alpha <= 0) fw.particles.splice(j,1);
                });
            });

            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>
