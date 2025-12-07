<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Poly Taka a Tak 💋💦 College</title>
    
    <!-- Icons & Fonts -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600&family=Nosifer&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <!-- GSAP Animation Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>

    <style>
        /* --- VARIABLES & RESET --- */
        :root {
            --primary: #ff00cc;
            --ocean-1: #006994;
            --ocean-2: #003366;
            --blood: #8a0303;
            --glass: rgba(255, 255, 255, 0.85);
            --ship-hull: #2c3e50;
            --ship-deck: #c0392b;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Poppins', sans-serif; }
        body { overflow-x: hidden; width: 100vw; height: 100vh; }

        /* --- 1. INTRO SCENE (Night Sky) --- */
        #intro-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(to bottom, #000000, #1a0b2e, #2d3436);
            z-index: 9999;
            overflow: hidden;
        }

        /* MOON */
        .moon {
            position: absolute; top: 15%; right: 20%;
            width: 120px; height: 120px;
            background: #dcdde1; border-radius: 50%;
            box-shadow: 0 0 60px rgba(255, 255, 255, 0.3); z-index: 5;
        }
        .crater { position: absolute; background: #b2bec3; border-radius: 50%; opacity: 0.6; }

        /* LAUNCH PAD */
        .launch-pad {
            position: absolute; bottom: 0; left: 10%; width: 140px; height: 250px; z-index: 10;
        }
        .pad-base {
            position: absolute; bottom: 0; left: -20px; width: 180px; height: 20px; 
            background: #333; border-top: 5px solid #ffeb3b;
        }
        .pad-tower {
            position: absolute; bottom: 20px; left: 20px; width: 30px; height: 200px; 
            background: linear-gradient(90deg, #444, #666); border-right: 3px solid #222;
        }
        .pad-arm {
            position: absolute; bottom: 150px; left: 50px; width: 40px; height: 10px; background: #555;
            transform-origin: left;
        }

        /* ROCKET */
        .rocket-container {
            position: absolute; bottom: 20px; left: 14.5%; 
            width: 60px; height: 160px; z-index: 20;
        }
        .rocket-body {
            width: 50px; height: 120px; background: linear-gradient(to right, #ecf0f1, #bdc3c7);
            border-radius: 50% 50% 5px 5px; position: relative; z-index: 2;
        }
        .rocket-window {
            position: absolute; top: 30px; left: 15px; width: 20px; height: 20px; 
            background: #3498db; border: 3px solid #2c3e50; border-radius: 50%;
        }
        .rocket-fin {
            position: absolute; bottom: 0; width: 20px; height: 40px; background: #e74c3c; z-index: 1;
        }
        .exhaust-flame {
            position: absolute; bottom: -30px; left: 10px; width: 30px; height: 40px;
            background: linear-gradient(to bottom, #f1c40f, #e74c3c);
            border-radius: 0 0 50% 50%; display: none;
            animation: thrust 0.1s infinite alternate;
        }
        @keyframes thrust { from { height: 40px; } to { height: 55px; opacity: 0.8; } }

        /* BOMB */
        .bomb {
            position: absolute; width: 30px; height: 30px; background: #000;
            border-radius: 50%; z-index: 15; opacity: 0; /* Hidden initially */
        }
        .bomb i { color: red; font-size: 10px; position: absolute; top: 8px; left: 10px; animation: blink 0.2s infinite; }
        @keyframes blink { 0% { opacity: 1; } 50% { opacity: 0; } }

        /* MAD SCIENTIST LAB (Overlay) */
        #lab-overlay {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.9); z-index: 50;
            display: none; opacity: 0; flex-direction: column;
            justify-content: center; align-items: center; border: 5px solid #0f0;
        }
        .lab-table {
            position: absolute; bottom: 0; width: 100%; height: 200px; background: #444;
            border-top: 10px solid #222; display: flex; justify-content: center; align-items: flex-end;
        }
        
        /* The Boom Button */
        .boom-button-casing {
            width: 120px; height: 60px; background: #222; border-radius: 10px 10px 0 0;
            position: relative; margin-bottom: 20px;
            box-shadow: 0 0 20px rgba(255,0,0,0.2);
        }
        .boom-button {
            width: 80px; height: 40px; background: radial-gradient(circle, #ff5252, #b71c1c);
            border-radius: 50%; position: absolute; top: -20px; left: 20px;
            cursor: pointer; box-shadow: 0 5px 0 #7f0000; transition: 0.1s;
        }
        .boom-button:active, .boom-button.pressed {
            top: -10px; box-shadow: 0 0 0 #7f0000;
        }
        .boom-text {
            color: white; position: absolute; bottom: 10px; width: 100%; text-align: center; font-weight: bold; font-family: monospace;
        }

        /* The Scientist */
        .scientist {
            position: absolute; bottom: 50px; right: -200px; /* Start off screen */
            width: 150px; height: 300px;
        }
        .sci-head {
            width: 60px; height: 70px; background: #ffccbc; border-radius: 10px;
            position: absolute; top: 0; left: 45px; z-index: 2;
        }
        .sci-hair {
            position: absolute; top: -20px; left: 35px; font-size: 80px; color: #eee; z-index: 1;
        }
        .sci-body {
            width: 100px; height: 180px; background: white; position: absolute; top: 70px; left: 25px;
            border-radius: 20px 20px 0 0; z-index: 1;
        }
        .sci-hand {
            width: 20px; height: 80px; background: #ffccbc; 
            position: absolute; top: 80px; left: 10px; transform-origin: top;
            transform: rotate(20deg);
        }

        /* EXPLOSION & TEXT */
        .explosion {
            position: absolute; top: 15%; right: 20%; transform: translate(50%, 50%);
            width: 0; height: 0; border-radius: 50%; opacity: 0; z-index: 60;
            background: radial-gradient(circle, #fff 10%, #ffeb3b 30%, #ff5722 60%, #000 90%);
        }
        .shockwave {
            position: absolute; top: 15%; right: 20%; transform: translate(50%, 50%);
            width: 10px; height: 10px; border: 5px solid white; border-radius: 50%;
            opacity: 0; z-index: 59;
        }
        .bloody-text {
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(0);
            font-family: 'Nosifer', cursive; color: var(--blood); font-size: 2.5rem;
            text-align: center; text-shadow: 2px 2px 0px #000, 0 0 20px red; z-index: 100; width: 90%;
        }

        /* --- 2. MAIN WEBSITE --- */
        #main-content {
            display: none; opacity: 0; width: 100%; min-height: 100vh;
            background: linear-gradient(to bottom, #87CEEB 0%, #E0F7FA 100%);
            position: relative; padding-bottom: 180px;
        }

        /* Ocean & Ship Wrapper */
        .ocean-container { position: fixed; bottom: 0; left: 0; width: 100%; height: 150px; overflow: hidden; z-index: 0; pointer-events: none; }
        .wave {
            position: absolute; bottom: 0; left: 0; width: 200%; height: 100%;
            background: url('data:image/svg+xml;utf8,<svg viewBox="0 0 1440 320" xmlns="http://www.w3.org/2000/svg"><path fill="%23006994" fill-opacity="0.6" d="M0,192L48,197.3C96,203,192,213,288,229.3C384,245,480,267,576,250.7C672,235,768,181,864,181.3C960,181,1056,235,1152,234.7C1248,235,1344,181,1392,154.7L1440,128L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path></svg>');
            background-size: 50% 100%; animation: wave 10s linear infinite; z-index: 2;
        }
        .wave:nth-of-type(2) {
            bottom: 10px; opacity: 0.8; animation: wave 15s linear infinite reverse; z-index: 4;
            background-image: url('data:image/svg+xml;utf8,<svg viewBox="0 0 1440 320" xmlns="http://www.w3.org/2000/svg"><path fill="%23003366" fill-opacity="0.9" d="M0,160L48,176C96,192,192,224,288,224C384,224,480,192,576,165.3C672,139,768,117,864,128C960,139,1056,181,1152,197.3C1248,213,1344,203,1392,197.3L1440,192L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path></svg>');
        }
        @keyframes wave { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

        /* Ship */
        .ship-wrapper { position: absolute; bottom: 40px; left: -200px; z-index: 3; animation: sail 35s linear infinite; }
        .ship { position: relative; width: 160px; height: 80px; animation: bob 3s ease-in-out infinite; }
        .hull { width: 160px; height: 40px; background: var(--ship-hull); border-radius: 0 0 30px 30px; position: absolute; bottom: 0; clip-path: polygon(0 0, 100% 0, 90% 100%, 10% 100%); }
        .hull::after { content: ''; position: absolute; top: 10px; left: 0; width: 100%; height: 5px; background: white; }
        .cabin { width: 80px; height: 30px; background: var(--ship-deck); position: absolute; bottom: 40px; left: 40px; border-radius: 5px 5px 0 0; }
        .cabin-window { width: 10px; height: 10px; background: #fff; border-radius: 50%; position: absolute; top: 10px; }
        .chimney { width: 20px; height: 30px; background: #333; position: absolute; bottom: 70px; left: 60px; }
        .chimney::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 5px; background: red; }
        .smoke { position: absolute; width: 10px; height: 10px; background: rgba(255,255,255,0.6); border-radius: 50%; bottom: 100px; left: 65px; opacity: 0; }
        .s1 { animation: puff 2s infinite 0s; } .s2 { animation: puff 2s infinite 0.7s; } .s3 { animation: puff 2s infinite 1.4s; }

        @keyframes sail { 0% { left: -200px; transform: scaleX(1); } 49% { transform: scaleX(1); } 50% { left: 110vw; transform: scaleX(-1); } 100% { left: 110vw; transform: scaleX(1); } }
        @keyframes bob { 0%, 100% { transform: translateY(0) rotate(0deg); } 50% { transform: translateY(8px) rotate(1deg); } }
        @keyframes puff { 0% { transform: translateY(0) scale(1); opacity: 0.8; } 100% { transform: translateY(-40px) scale(2.5) translateX(10px); opacity: 0; } }

        /* UI */
        .content-wrapper { position: relative; z-index: 10; padding: 20px; max-width: 1200px; margin: 0 auto; }
        header { text-align: center; margin: 30px 0; }
        .site-title { font-family: 'Fredoka', sans-serif; font-size: 2.5rem; color: #003366; text-shadow: 2px 2px 0px #fff; }
        .filters { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; margin-bottom: 20px; }
        .filter-btn { padding: 8px 20px; border: none; border-radius: 20px; background: rgba(255,255,255,0.6); cursor: pointer; font-weight: 600; transition: 0.3s; }
        .filter-btn.active, .filter-btn:hover { background: #006994; color: white; }
        .pdf-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; }
        .card { background: var(--glass); padding: 20px; border-radius: 15px; box-shadow: 0 10px 20px rgba(0,0,0,0.1); text-align: center; transition: 0.3s; }
        .card:hover { transform: translateY(-10px) scale(1.02); background: white; }
        .card-icon { font-size: 2.5rem; color: #ff00cc; margin-bottom: 10px; }
        .card-title { font-weight: 600; margin-bottom: 15px; color: #333; height: 50px; overflow: hidden; display: flex; align-items: center; justify-content: center; }
        .btn-group { display: flex; gap: 10px; }
        .btn { flex: 1; padding: 10px; border-radius: 8px; border: none; cursor: pointer; text-decoration: none; font-weight: 600; color: white; display: flex; align-items: center; justify-content: center; gap: 5px; }
        .btn-view { background: #006994; } .btn-dl { background: #e17055; }

        /* Viewer */
        #pdf-viewer-section { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: white; z-index: 2000; flex-direction: column; }
        .viewer-header { height: 60px; background: #003366; color: white; display: flex; align-items: center; padding: 0 20px; }
        .back-btn { background: #ff00cc; color: white; border: none; padding: 8px 20px; border-radius: 5px; cursor: pointer; font-weight: bold; margin-right: 20px; }
        .pdf-frame { width: 100%; height: calc(100% - 60px); border: none; }

        @media (max-width: 600px) { .bloody-text { font-size: 1.5rem; } .moon { width: 80px; height: 80px; right: 10%; } }
    </style>
</head>
<body>

    <!-- 1. INTRO ANIMATION -->
    <div id="intro-overlay">
        <!-- Moon -->
        <div class="moon" id="moon">
            <div class="crater" style="top:20px; left:20px; width:20px; height:20px;"></div>
            <div class="crater" style="bottom:30px; right:20px; width:30px; height:30px;"></div>
        </div>
        
        <!-- Launch Pad -->
        <div class="launch-pad">
            <div class="pad-tower"></div>
            <div class="pad-arm" id="padArm"></div>
            <div class="pad-base"></div>
        </div>

        <!-- Rocket -->
        <div class="rocket-container" id="rocket">
            <div class="rocket-fin" style="left: -15px; border-radius: 100% 0 0 0;"></div>
            <div class="rocket-fin" style="right: -15px; border-radius: 0 100% 0 0;"></div>
            <div class="rocket-body">
                <div class="rocket-window"></div>
            </div>
            <div class="exhaust-flame" id="flame"></div>
        </div>

        <!-- Bomb -->
        <div class="bomb" id="bomb"><i class="fas fa-radiation"></i></div>

        <!-- Mad Scientist Lab Overlay -->
        <div id="lab-overlay">
            <h1 style="color:#0f0; font-family:'Courier New'; margin-bottom:50px; text-shadow:0 0 10px #0f0;">LABORATORY CONTROL</h1>
            <div class="lab-table">
                <div class="boom-button-casing">
                    <div class="boom-button" id="boomBtn"></div>
                    <div class="boom-text">BOOM 💥</div>
                </div>
            </div>
            <!-- Scientist Character -->
            <div class="scientist" id="scientist">
                <i class="fas fa-bolt sci-hair"></i>
                <div class="sci-head">
                    <!-- Glasses -->
                    <div style="position:absolute; top:25px; left:10px; width:15px; height:15px; background:black; border-radius:50%;"></div>
                    <div style="position:absolute; top:25px; right:10px; width:15px; height:15px; background:black; border-radius:50%;"></div>
                    <div style="position:absolute; top:30px; left:25px; width:10px; height:2px; background:black;"></div>
                </div>
                <div class="sci-body"></div>
                <div class="sci-hand" id="sciHand"></div>
            </div>
        </div>

        <!-- Real Blast Effects -->
        <div class="explosion" id="explosion"></div>
        <div class="shockwave" id="shockwave"></div>
        
        <div class="bloody-text" id="bloodyText">Welcome to Polytechnic <br> Taka a Tak 💋💦 College</div>
    </div>

    <!-- 2. MAIN CONTENT -->
    <div id="main-content">
        <div class="content-wrapper">
            <header>
                <h1 class="site-title">Poly Taka a Tak 💋💦 College</h1>
                <p>Subject-wise First Semester PDFs</p>
            </header>

            <div class="filters">
                <button class="filter-btn active" onclick="renderPDFs('all')">All</button>
                <button class="filter-btn" onclick="renderPDFs('Communication')">Communication</button>
                <button class="filter-btn" onclick="renderPDFs('Physics')">Physics</button>
                <button class="filter-btn" onclick="renderPDFs('Chemistry')">Chemistry</button>
                <button class="filter-btn" onclick="renderPDFs('Maths')">Maths</button>
                <button class="filter-btn" onclick="renderPDFs('PYQ')">PYQs</button>
            </div>

            <div class="pdf-grid" id="pdfContainer"></div>
        </div>

        <!-- Ocean & Ship -->
        <div class="ocean-container">
            <div class="wave"></div>
            <div class="ship-wrapper">
                <div class="ship">
                    <div class="smoke s1"></div> <div class="smoke s2"></div> <div class="smoke s3"></div>
                    <div class="chimney"></div>
                    <div class="cabin"><div class="cabin-window" style="left:10px;"></div><div class="cabin-window" style="left:35px;"></div><div class="cabin-window" style="left:60px;"></div></div>
                    <div class="hull"></div>
                </div>
            </div>
            <div class="wave"></div>
        </div>
    </div>

    <!-- 3. PDF VIEWER -->
    <div id="pdf-viewer-section">
        <div class="viewer-header">
            <button class="back-btn" onclick="closePDF()"><i class="fas fa-arrow-left"></i> Back</button>
            <span>PDF Viewer</span>
        </div>
        <iframe id="pdfFrame" class="pdf-frame" src=""></iframe>
    </div>

    <script>
        // DATA
        const db = [
            { title: "All Subjects PYQ (PDF)", category: "PYQ", link: "https://drive.google.com/file/d/1_PLBO5aGkaVbGfynHmlUz--vV49AeyZP/view?usp=drivesdk" },
            { title: "PYQ Full Folder", category: "PYQ", link: "https://drive.google.com/drive/folders/1K-DjXuPN9VjnPeCf2l2SowyrOLwoPyf2" },
            { title: "Comm. Skills Paper 1", category: "Communication", link: "https://drive.google.com/file/d/1eqr-l1zxfz_NS3KQNM1mKUcl-5SQkX5z/view?usp=drivesdk" },
            { title: "Comm. Skills Paper 2", category: "Communication", link: "https://drive.google.com/file/d/15DYAyRNuTXs9w1X5KO3VD0nxiV0cezPN/view?usp=drivesdk" },
            { title: "Comm. Skills Paper 3", category: "Communication", link: "https://drive.google.com/file/d/1k4Lz_R2f31f5ACyPvZAuijHFk72IYw2Y/view?usp=drivesdk" },
            { title: "Physics Paper 1", category: "Physics", link: "https://drive.google.com/file/d/1g9p3DWpXydbZVYjTAXcllC38k8V7sVbj/view?usp=drivesdk" },
            { title: "Physics Paper 2", category: "Physics", link: "https://drive.google.com/file/d/1NYYFYf6gkvTY0JBVwQSzddwkr6kDqC74/view?usp=drivesdk" },
            { title: "Physics Paper 3", category: "Physics", link: "https://drive.google.com/file/d/1RULrMfiDZ0nLHcuar8-BSNCsC_IqMnWf/view?usp=drivesdk" },
            { title: "Physics Paper 4", category: "Physics", link: "https://drive.google.com/file/d/1AAaA7ls6zQGKh6L5hfEqpHOLtD2GqqGJ/view?usp=drivesdk" },
            { title: "Physics Paper 5", category: "Physics", link: "https://drive.google.com/file/d/1IEt7xTyljMe08W1S7n-7QRiiMTOZvI21/view?usp=drivesdk" },
            { title: "Chemistry Paper 1", category: "Chemistry", link: "https://drive.google.com/file/d/1VZrUCG4RAhSJVPfUoFiDj6wBQzvKcy6p/view?usp=drivesdk" },
            { title: "Chemistry Book", category: "Chemistry", link: "https://drive.google.com/file/d/1ilVIj41ZG_EGwqSRsxoUfOPNG93-bidb/view?usp=drivesdk" },
            { title: "Chemistry Paper 2", category: "Chemistry", link: "https://drive.google.com/file/d/1UDO6hiCK77CXEWWYw4fuI3yFkxk6WUzg/view?usp=drivesdk" },
            { title: "Chemistry Paper 3", category: "Chemistry", link: "https://drive.google.com/file/d/1WMa75kVC0dl8l3Oi4JU4ClskNwdiu13B/view?usp=drivesdk" },
            { title: "Chemistry Paper 4", category: "Chemistry", link: "https://drive.google.com/file/d/1uDw0ve8RUE5FAAt8--gocX0gwPRGOACx/view?usp=drivesdk" },
            { title: "Chemistry Paper 5", category: "Chemistry", link: "https://drive.google.com/file/d/1nowz9XV25J-ccXVFSzOyMjB8HPSCB8v0/view?usp=drivesdk" },
            { title: "Maths: Complex No 1", category: "Maths", link: "https://drive.google.com/file/d/1FzZG3hDm0y4iCK2mb4HUyt4O8TEAZYpx/view?usp=drivesdk" },
            { title: "Maths: Complex No 2", category: "Maths", link: "https://drive.google.com/file/d/1cUhklPJjhtd37IGJCYYa9uPoj2tNv98m/view?usp=drivesdk" },
            { title: "Maths: Paper 3", category: "Maths", link: "https://drive.google.com/file/d/18MEZlaYvUucMdISfSTTFMIlww8eH98Km/view?usp=drivesdk" },
            { title: "Maths: Paper 4", category: "Maths", link: "https://drive.google.com/file/d/1NvI0_-OruK8bAkYjHVEMreAVKh9cHvRo/view?usp=drivesdk" },
            { title: "Maths: Paper 5", category: "Maths", link: "https://drive.google.com/file/d/11Wosd0PybquAn_y8dEt4OEV27OjCcZrj/view?usp=drivesdk" },
            { title: "Maths: Paper 6", category: "Maths", link: "https://drive.google.com/file/d/1DGEiomYl8pwaCOVVamL0JwZixEM0Kry1/view?usp=drivesdk" },
            { title: "Maths: Paper 7", category: "Maths", link: "https://drive.google.com/file/d/1M77apPd42mfMtt1jN59WXzsAY-zACGxt/view?usp=drivesdk" },
            { title: "Maths: Paper 8", category: "Maths", link: "https://drive.google.com/file/d/1HRyx20kNsPZhxdsQPJD0xj6cx7XIu4MZ/view?usp=drivesdk" },
            { title: "Maths: Paper 9", category: "Maths", link: "https://drive.google.com/file/d/1MZYDdZjdzq7PRHou3DCY-q81O8Y9tSET/view?usp=drivesdk" }
        ];

        // --- MASTER ANIMATION SEQUENCE ---
        window.onload = () => {
            const tl = gsap.timeline({
                onComplete: () => {
                    gsap.to("#intro-overlay", { opacity: 0, duration: 1, display: "none" });
                    document.getElementById("main-content").style.display = "block";
                    gsap.to("#main-content", { opacity: 1, duration: 1 });
                    gsap.from(".card", { y: 50, opacity: 0, duration: 0.5, stagger: 0.05 });
                }
            });

            // Elements
            const rocket = document.getElementById('rocket');
            const flame = document.getElementById('flame');
            const bomb = document.getElementById('bomb');
            const moon = document.getElementById('moon');
            const lab = document.getElementById('lab-overlay');
            
            // 1. LAUNCH
            tl.to("#padArm", { rotation: -45, duration: 1 }) // Move arm away
              .add(() => flame.style.display = "block")
              .to(rocket, { y: -window.innerHeight * 0.7, duration: 2.5, ease: "power2.in" }) // Fly Up
              .to(rocket, { left: "75%", top: "10%", rotation: 45, duration: 1.5, ease: "power1.out" }) // To Moon

            // 2. DROP BOMB
              .add(() => {
                  const rRect = rocket.getBoundingClientRect();
                  bomb.style.opacity = 1;
                  bomb.style.left = (rRect.left + 15) + "px";
                  bomb.style.top = (rRect.top + 50) + "px";
              })
              .to(bomb, { top: "18%", left: "78%", duration: 0.5, ease: "power1.in" }) // Bomb lands on moon

            // 3. RETURN TO BASE
              .to(rocket, { rotation: 180, duration: 0.5 }) // Turn around
              .to(rocket, { left: "14.5%", top: "auto", bottom: "20px", rotation: 180, duration: 2, ease: "power2.out" }) // Fly back down
              .add(() => flame.style.display = "none") // Landed

            // 4. SHOW LAB
              .to(lab, { display: "flex", opacity: 1, duration: 0.5 })
              
            // 5. SCIENTIST WALKS IN
              .to("#scientist", { right: "30%", duration: 1, ease: "back.out(1.7)" })
              .to("#sciHand", { rotation: -30, duration: 0.2, yoyo: true, repeat: 2 }) // Wave hand
              
            // 6. PRESS BUTTON
              .to("#sciHand", { rotation: -60, duration: 0.5 }) // Raise hand
              .to("#sciHand", { rotation: 40, duration: 0.1 }) // Slam hand down
              .add(() => document.getElementById("boomBtn").classList.add("pressed")) // Visual Press
              
            // 7. BLAST SEQUENCE
              .to(lab, { opacity: 0, duration: 0.2, delay: 0.2 }) // Hide Lab fast
              .add(() => {
                  bomb.style.display = "none";
                  moon.style.opacity = 0; // Moon gone
              })
              // Real Blast Animation
              .to("#explosion", { opacity: 1, width: "600px", height: "600px", duration: 0.1, ease: "elastic.out" })
              .to("#shockwave", { opacity: 0.8, width: "800px", height: "800px", border: "50px solid white", duration: 0.3 }, "<")
              .to("#explosion", { opacity: 0, scale: 1.2, duration: 0.5 })
              .to("#shockwave", { opacity: 0, scale: 1.5, duration: 0.5 }, "<")

            // 8. TEXT REVEAL
              .to("#bloodyText", { scale: 1, opacity: 1, duration: 0.5, ease: "elastic.out(1, 0.3)" })
              .to("#bloodyText", { scale: 1.05, duration: 2, yoyo: true, repeat: 1 });
        };

        // VIEWER LOGIC
        function openPDF(url) {
            if(url.includes("folders")) { window.open(url, '_blank'); return; }
            let embedUrl = url;
            if(url.includes("view?usp=drivesdk")) embedUrl = url.replace("view?usp=drivesdk", "preview");
            else if (url.includes("/view")) embedUrl = url.replace("/view", "/preview");
            document.getElementById("pdfFrame").src = embedUrl;
            document.getElementById("main-content").style.display = "none";
            document.getElementById("pdf-viewer-section").style.display = "flex";
        }

        function closePDF() {
            document.getElementById("pdfFrame").src = "";
            document.getElementById("pdf-viewer-section").style.display = "none";
            document.getElementById("main-content").style.display = "block";
        }

        // RENDER LOGIC
        const container = document.getElementById('pdfContainer');
        function renderPDFs(filterCat) {
            container.innerHTML = "";
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.toggle('active', btn.textContent.includes(filterCat) || (filterCat === 'all' && btn.textContent === 'All'));
            });
            const filteredData = filterCat === 'all' ? db : db.filter(item => item.category === filterCat);
            filteredData.forEach(item => {
                let downloadLink = item.link.includes('file/d/') ? `https://drive.google.com/uc?export=download&id=${item.link.match(/file\/d\/(.*?)\//)[1]}` : item.link;
                let iconClass = "fa-file-pdf";
                if(item.category === "Maths") iconClass = "fa-calculator";
                if(item.category === "Physics") iconClass = "fa-atom";
                if(item.category === "Chemistry") iconClass = "fa-flask";
                const viewAction = item.link.includes("folders") ? `target="_blank" href="${item.link}"` : `href="#" onclick="openPDF('${item.link}')"`;
                container.innerHTML += `
                    <div class="card">
                        <div class="card-icon"><i class="fas ${iconClass}"></i></div>
                        <div class="card-title">${item.title}</div>
                        <div class="btn-group">
                            <a ${viewAction} class="btn btn-view"><i class="fas fa-eye"></i> View</a>
                            <a href="${downloadLink}" class="btn btn-dl"><i class="fas fa-download"></i> Save</a>
                        </div>
                    </div>`;
            });
        }
        renderPDFs('all');
    </script>
</body>
</html>
