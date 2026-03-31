<html lang="mn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Төрсөн өдрийн мэнд хүргье, Хөөрхөнөө!</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            /* Ягаан өнгөнд суурилсан зөөлөн gradient фон */
            background: linear-gradient(135deg, #fce4ec 0%, #f8bbd0 50%, #fce4ec 100%);
            font-family: 'Segoe UI', 'Roboto', sans-serif;
            overflow: hidden;
            text-align: center;
            color: #880e4f; /* Гүн ягаан текст */
        }
        .container {
            width: 85%;
            max-width: 550px;
            z-index: 10;
            position: relative;
        }
        .hidden { display: none !important; }
        /* Илүү чамин постер загвар */
        .poster {
            background: rgba(255, 255, 255, 0.85);
            padding: 50px 40px;
            border-radius: 30px;
            border: 3px solid #f48fb1; /* Ягаан хүрээ */
            box-shadow: 0 15px 35px rgba(244, 143, 177, 0.3); /* Ягаан туяатай сүүдэр */
            animation: fadeInPost 1.2s ease-out;
            backdrop-filter: blur(5px); /* Арын фоныг бүрлүүлэх эффект */
        }
        h1 { color: #c2185b; font-size: 2.2em; margin-bottom: 20px; font-weight: 700; }
        p { color: #880e4f; line-height: 1.8; font-size: 1.2em; font-weight: 500;}
        /* Чичиргээт (Pulse) эффекттэй товчлуур */
        button {
            background-color: #ff80ab;
            color: white;
            border: none;
            padding: 15px 35px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 18px;
            margin-top: 30px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(255, 128, 171, 0.4);
            transition: all 0.3s ease;
            animation: pulse 2s infinite;
        }
        button:hover {
            background-color: #f50057;
            transform: scale(1.08) translateY(-2px);
            box-shadow: 0 8px 20px rgba(245, 0, 87, 0.5);
        }
        /* Хөдөлгөөнт эффектүүд */
        @keyframes fadeInPost {
            from { opacity: 0; transform: scale(0.9) translateY(30px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(255, 128, 171, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(255, 128, 171, 0); }
            100% { box-shadow: 0 0 0 0 rgba(255, 128, 171, 0); }
        }
        /* Нар, Цэцэгсийн хэсэг */
        #scene-animation {
            position: relative;
            height: 150px;
            margin-bottom: 20px;
            overflow: hidden;
        }
        .sun {
            font-size: 60px;
            position: absolute;
            bottom: -70px;
            left: calc(50% - 30px);
            transition: transform 6s cubic-bezier(0.22, 1, 0.36, 1);
        }
        .flower-row {
            font-size: 40px;
            position: absolute;
            bottom: 0;
            width: 100%;
            opacity: 0;
            transition: opacity 3s ease 2s; /* Нар мандсаны дараа харагдана */
        }
        /* Төгсгөл хэсгийн зураг */
        #final-image {
            width: 250px;
            height: 250px;
            border-radius: 50%;
            border: 8px solid white;
            box-shadow: 0 0 30px rgba(244, 143, 177, 0.5);
            object-fit: cover;
            margin-bottom: 20px;
            animation: fadeInPost 1.5s ease-out;
        }
        /* Цэцгэн борооны Canvas */
        #flower-canvas {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        /* CSS-ээр хийсэн Typing Effect */
        .typing {
            display: inline-block;
            overflow: hidden;
            border-right: .15em solid #c2185b; /* Cursor */
            white-space: nowrap;
            margin: 0 auto;
            letter-spacing: .15em;
            animation: typing 3.5s steps(40, end), blink-caret .75s step-end infinite;
        }
        @keyframes typing { from { width: 0 } to { width: 100% } }
        @keyframes blink-caret { from, to { border-color: transparent } 50% { border-color: #c2185b; } }

    </style>
</head>
<body>
    <audio id="bgMusic" loop>
        <source src="5.mp3" type="audio/mpeg">
    </audio>
    <canvas id="flower-canvas"></canvas>
    <div id="part1" class="container">
        <div class="poster">
            <h1>Сайн уу? 👋</h1>
            <p>Энэ өдрийн мэнд хөөрхөнөө!</p>
            <button onclick="startExperience()">Цааш ❤️</button>
        </div>
    </div>
    <div id="part2" class="container hidden">
        <div id="scene-animation">
            <div class="sun">☀️</div>
            <div class="flower-row">🌸🌻🌹🌷🌼🌷🌹🌻🌸</div>
        </div>
        <div id="poster2a" class="poster">
            <h1 class="typing">Төрсөн өдрийн мэнд!</h1>
        </div>
        <div id="poster2b" class="poster hidden">
            <p id="apology-text"></p> <button id="nextBtn" class="hidden" onclick="showFinal()">Цааш 🌸</button>
        </div>
    </div>
    <div id="part3" class="container hidden">
        <img id="final-image" src="9.jpg" alt="Зураг">
        <h1 style="color: #c2185b; font-size: 2em;">Үргэлж инээмсэглэж яваарай 🌸</h1>
        <p>Чи их хичээж байгаа шүү.</p>
    </div>
    <script>
        const bgMusic = document.getElementById('bgMusic');
        function startExperience() {
            bgMusic.play().catch(e => console.log("Audio play blocked"));
            document.getElementById('part1').classList.add('hidden');
            document.getElementById('part2').classList.remove('hidden');
            // Нар мандах эффект
            setTimeout(() => {
                document.querySelector('.sun').style.transform = 'translateY(-140px)';
                document.querySelector('.flower-row').style.opacity = '1';
            }, 100);
            // 10 секундын дараа (Нарыг харж амжсаны дараа) уучлалтын постер
            setTimeout(() => {
                document.getElementById('poster2a').classList.add('hidden');
                document.getElementById('poster2b').classList.remove('hidden');
                // Уучлалтын текстийг нэг нэгээр нь бичих
                typeWriter("apology-text", "Өнгөрсөн хугацаанд баярлалаа, бас чин сэтгэлээсээ уучлалт хүсье. Дэндүү бодлогүй зан гаргаж тавгүйтэлдэг байсанд үнэхээр уучлаарай... 😭😭😭", 60);
                // Текст бичигдэж дууссаны дараа товчлуур гаргах
                setTimeout(() => {
                    document.getElementById('nextBtn').classList.remove('hidden');
                }, 9000); // Текстийн уртаас хамаарч тааруулна
            }, 10000);
        }
        function showFinal() {
            document.getElementById('part2').classList.add('hidden');
            document.getElementById('part3').classList.remove('hidden');
            document.getElementById('scene-animation').classList.add('hidden');
            startFlowerRain(); // Цэцгэн бороо эхлүүлэх
        }
        // Текст бичих функц
        function typeWriter(elementId, text, speed) {
            let i = 0;
            const element = document.getElementById(elementId);
            element.innerHTML = "";
            function type() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(type, speed);
                }
            }
            type();
        }
        // Цэцгэн борооны эффект (Canvas)
        function startFlowerRain() {
            const canvas = document.getElementById('flower-canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            const flowers = ['🌸', '🌹', '🌺', '🌻', '🌼', '🌷', '💖'];
            const particles = [];
            function createParticle() {
                return {
                    x: Math.random() * canvas.width,
                    y: -50,
                    text: flowers[Math.floor(Math.random() * flowers.length)],
                    size: Math.random() * 25 + 15,
                    speed: Math.random() * 2 + 1,
                    angle: Math.random() * 6,
                    spin: Math.random() * 0.2 - 0.1
                };
            }
            for(let i = 0; i < 70; i++) {
                setTimeout(() => {
                    particles.push(createParticle());
                }, i * 100);
            }
            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                particles.forEach(p => {
                    p.y += p.speed;
                    p.x += Math.sin(p.angle) * 0.5;
                    p.angle += 0.02;       
                    ctx.font = `${p.size}px serif`;
                    ctx.save();
                    ctx.translate(p.x, p.y);
                    // Эргэлдэх хөдөлгөөн нэмэх (сонголт)
                    // ctx.rotate(p.angle * p.spin); 
                    ctx.fillText(p.text, -p.size/2, p.size/2);
                    ctx.restore();
                    // Дээшээ буцаах биш, дороос алга болоод дээрээс дахин гарч ирнэ
                    if(p.y > canvas.height + 50) {
                        p.y = -50;
                        p.x = Math.random() * canvas.width;
                    }
                });
                requestAnimationFrame(animate);
            }
            animate();
            // Цонхны хэмжээ өөрчлөгдөхөд canvas-ийг тааруулах
            window.addEventListener('resize', () => {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            });
        }
    </script>
</body>
</html>
