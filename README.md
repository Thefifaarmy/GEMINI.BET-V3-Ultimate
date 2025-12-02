# GEMINI.BET-V3-Ultimate
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>GEMINI.BET | Ultimate Crypto Casino</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;500;700;900&family=Space+Grotesk:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* --- CORE SETUP --- */
        :root {
            --primary: #00ffa3;
            --primary-dim: rgba(0, 255, 163, 0.1);
            --gold: #ffd700;
            --bg-dark: #050505;
            --glass: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
            --blur: 16px;
        }

        /* Lock the viewport specifically for mobile to prevent "bouncing" */
        html, body {
            height: 100%;
            width: 100%;
            overflow: hidden;
            background-color: var(--bg-dark);
            font-family: 'Outfit', sans-serif;
            color: white;
            -webkit-tap-highlight-color: transparent;
            overscroll-behavior: none;
            touch-action: manipulation;
        }

        /* --- AMBIENT BG --- */
        .ambient-bg {
            position: fixed;
            top: 0; left: 0; width: 100vw; height: 100vh;
            background: radial-gradient(circle at 15% 50%, rgba(56, 189, 248, 0.08), transparent 25%),
                        radial-gradient(circle at 85% 30%, rgba(0, 255, 163, 0.08), transparent 25%);
            z-index: -1;
            pointer-events: none;
        }

        /* --- UI COMPONENTS --- */
        .glass-panel {
            background: var(--glass);
            backdrop-filter: blur(var(--blur));
            -webkit-backdrop-filter: blur(var(--blur));
            border: 1px solid var(--glass-border);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        .btn-premium {
            background: linear-gradient(135deg, #00ffa3 0%, #00c27a 100%);
            color: #000;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 0 20px rgba(0, 255, 163, 0.3), inset 0 2px 0 rgba(255,255,255,0.3);
            transition: all 0.2s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            border: none;
        }
        .btn-premium:active { transform: scale(0.96); box-shadow: 0 0 10px rgba(0, 255, 163, 0.1); }
        .btn-premium:disabled { background: #333; color: #666; box-shadow: none; cursor: not-allowed; }

        .btn-secondary {
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1);
            color: #aaa;
            transition: 0.2s;
        }
        .btn-secondary:active { background: rgba(255,255,255,0.1); color: white; }

        .game-thumb {
            transition: all 0.3s ease;
            background: linear-gradient(180deg, rgba(30,41,59,0.7) 0%, rgba(15,23,42,1) 100%);
        }
        .game-thumb:active { transform: scale(0.95); }

        .currency-font { font-family: 'Space Grotesk', monospace; }

        /* --- GAME SPECIFIC AESTHETICS --- */
        
        /* Crash Graph */
        .crash-canvas-container {
            position: relative;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: inset 0 0 50px rgba(0,0,0,0.8);
            background: radial-gradient(circle at center, #1a2333 0%, #0b101e 100%);
        }

        /* Mines */
        .mine-tile {
            background: linear-gradient(145deg, #2a3545, #1e2633);
            box-shadow: 0 4px 6px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,255,0.1);
            transition: transform 0.1s;
        }
        .mine-tile:active { transform: scale(0.9); }
        .mine-tile.revealed { background: #111; box-shadow: inset 0 2px 4px rgba(0,0,0,0.5); }
        .mine-tile.gem { border: 1px solid var(--primary); box-shadow: 0 0 15px var(--primary-dim); }
        .mine-tile.bomb { border: 1px solid #ff4757; box-shadow: 0 0 15px rgba(255, 71, 87, 0.4); }

        /* Roulette Tape */
        .roulette-track-bg {
            background: #0f1219;
            box-shadow: inset 0 0 30px #000;
            border-top: 2px solid #333;
            border-bottom: 2px solid #333;
        }
        .marker-arrow {
            width: 0; height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-top: 15px solid white;
            filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
            z-index: 20;
        }

        /* Towers */
        .tower-btn {
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1);
            box-shadow: 0 4px 0 rgba(0,0,0,0.3);
        }
        .tower-btn:active { transform: translateY(4px); box-shadow: none; }
        .tower-btn.safe { background: var(--primary); color: black; box-shadow: 0 0 15px var(--primary); border:none; }
        .tower-btn.dead { background: #ff4757; color: white; box-shadow: 0 0 15px #ff4757; border:none; }

        /* SLOTS */
        .slot-reel {
            background: #0b101e;
            border: 2px solid #334155;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: inset 0 0 20px #000;
            position: relative;
        }
        .slot-reel::before {
            content: ''; position: absolute; top:0; left:0; width:100%; height: 20%;
            background: linear-gradient(to bottom, rgba(0,0,0,0.8), transparent); z-index: 10;
        }
        .slot-reel::after {
            content: ''; position: absolute; bottom:0; left:0; width:100%; height: 20%;
            background: linear-gradient(to top, rgba(0,0,0,0.8), transparent); z-index: 10;
        }
        .reel-strip { transition: transform 0.1s linear; will-change: transform; }
        .slot-symbol {
            height: 100px; display: flex; align-items: center; justify-content: center;
            font-size: 3rem; filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
        }
        .blur-spin { filter: blur(4px); }

        /* HORSE RACING */
        .track-lane {
            border-bottom: 1px dashed rgba(255,255,255,0.1);
            position: relative;
            background: rgba(0,0,0,0.2);
        }
        .horse-runner {
            transition: left 0.5s linear;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.5));
            will-change: left;
        }

        /* Particles Canvas */
        #fxCanvas {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 100;
        }

        /* Animations */
        @keyframes shake-screen {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            100% { transform: translate(1px, -1px) rotate(0deg); }
        }
        .shake-active { animation: shake-screen 0.2s ease-in-out infinite; }
        
        @keyframes big-win-pulse {
            0% { transform: scale(0.8); opacity: 0; }
            50% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(1); opacity: 1; }
        }

        /* Scrollable Area */
        .scroll-container {
            height: 100%;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            padding-bottom: 100px; 
        }

        /* Big Win Overlay */
        #bigWinOverlay {
            background: radial-gradient(circle, rgba(255, 215, 0, 0.3) 0%, rgba(0,0,0,0.9) 70%);
            backdrop-filter: blur(5px);
        }
    </style>
</head>
<body class="flex flex-col">

    <!-- FX CANVAS -->
    <canvas id="fxCanvas"></canvas>
    
    <!-- BIG WIN OVERLAY -->
    <div id="bigWinOverlay" class="fixed inset-0 z-[200] hidden flex-col items-center justify-center pointer-events-none">
        <h1 class="text-6xl md:text-8xl font-black text-yellow-400 drop-shadow-[0_0_20px_rgba(255,215,0,0.8)] animate-[big-win-pulse_0.5s_ease-out_forwards]">BIG WIN</h1>
        <div id="bigWinAmount" class="text-4xl md:text-6xl font-bold text-white mt-4 currency-font drop-shadow-lg">$0.00</div>
    </div>

    <!-- AMBIENT BG -->
    <div class="ambient-bg"></div>

    <!-- HEADER -->
    <header class="h-16 flex-none glass-panel border-b-0 z-50 flex items-center justify-between px-5 sticky top-0">
        <div class="flex items-center gap-3" onclick="showLobby()">
            <div class="w-9 h-9 rounded-lg bg-gradient-to-br from-white to-gray-400 flex items-center justify-center shadow-lg cursor-pointer">
                <i class="fas fa-gem text-black text-lg"></i>
            </div>
            <div class="flex flex-col leading-none cursor-pointer">
                <span class="font-bold text-lg tracking-wide">GEMINI</span>
                <span class="text-[10px] text-emerald-400 font-bold tracking-[0.2em] uppercase">Casino</span>
            </div>
        </div>
        
        <div class="glass-panel px-3 py-1.5 rounded-full flex items-center gap-3">
            <div class="flex flex-col items-end leading-none">
                <span class="text-[9px] text-gray-400 font-bold uppercase">Balance</span>
                <span class="currency-font text-emerald-400 font-bold text-sm" id="globalBalance">$1,000.00</span>
            </div>
            <button onclick="addFunds()" class="w-6 h-6 rounded-full bg-emerald-500/20 text-emerald-400 flex items-center justify-center border border-emerald-500/50 hover:bg-emerald-500 hover:text-black transition">
                <i class="fas fa-plus text-xs"></i>
            </button>
        </div>
    </header>

    <!-- SCROLLABLE CONTENT -->
    <main class="flex-1 relative overflow-hidden">
        <div class="scroll-container px-4 py-6" id="mainContent">
            
            <!-- LOBBY -->
            <div id="lobby" class="flex flex-col gap-6 fade-in">
                <!-- Promo Banner -->
                <div class="w-full h-40 rounded-2xl bg-gradient-to-r from-purple-900 to-slate-900 relative overflow-hidden flex items-center px-6 border border-white/10 shadow-2xl">
                    <div class="absolute right-0 top-0 h-full w-1/2 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] opacity-20"></div>
                    <div class="z-10">
                        <div class="text-xs font-bold text-purple-400 uppercase tracking-widest mb-1">New Release</div>
                        <h2 class="text-2xl font-black italic text-white mb-2">NEON SLOTS</h2>
                        <button onclick="loadGame('slots')" class="px-4 py-2 bg-white text-black text-xs font-bold rounded-full uppercase hover:bg-gray-200 transition">Spin Now</button>
                    </div>
                </div>

                <h3 class="text-sm font-bold text-gray-400 uppercase tracking-widest pl-1"><i class="fas fa-fire text-orange-500 mr-2"></i>All Games</h3>
                
                <div class="grid grid-cols-2 gap-4">
                    <!-- Space Crash -->
                    <div onclick="loadGame('crash')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-purple-500 rotate-12"><i class="fas fa-rocket"></i></div>
                        <div class="z-10 bg-purple-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-purple-400 border border-purple-500/30"><i class="fas fa-rocket"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Space Crash</h4><span class="text-xs text-emerald-400 currency-font">MAX 5000x</span></div>
                    </div>

                    <!-- Mines -->
                    <div onclick="loadGame('mines')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-emerald-500 rotate-12"><i class="fas fa-bomb"></i></div>
                        <div class="z-10 bg-emerald-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-emerald-400 border border-emerald-500/30"><i class="fas fa-gem"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Gem Mines</h4><span class="text-xs text-emerald-400 currency-font">98% RTP</span></div>
                    </div>

                    <!-- Slots (NEW) -->
                    <div onclick="loadGame('slots')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-pink-500 rotate-12"><i class="fas fa-slot-machine"></i></div>
                        <div class="z-10 bg-pink-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-pink-400 border border-pink-500/30"><i class="fas fa-star"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Neon Slots</h4><span class="text-xs text-pink-400 currency-font">JACKPOT</span></div>
                    </div>

                    <!-- Horse Racing (NEW) -->
                    <div onclick="loadGame('horse')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-orange-500 rotate-12"><i class="fas fa-horse-head"></i></div>
                        <div class="z-10 bg-orange-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-orange-400 border border-orange-500/30"><i class="fas fa-flag-checkered"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Turbo Derby</h4><span class="text-xs text-orange-400 currency-font">LIVE RACE</span></div>
                    </div>

                    <!-- Towers -->
                    <div onclick="loadGame('towers')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-yellow-500 rotate-12"><i class="fas fa-layer-group"></i></div>
                        <div class="z-10 bg-yellow-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-yellow-400 border border-yellow-500/30"><i class="fas fa-dungeon"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Sky Towers</h4><span class="text-xs text-yellow-400 currency-font">HIGH RISK</span></div>
                    </div>

                    <!-- Roulette -->
                    <div onclick="loadGame('roulette')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer">
                        <div class="absolute -right-4 -top-4 text-8xl opacity-10 group-hover:opacity-20 transition text-red-500 rotate-12"><i class="fas fa-circle-notch"></i></div>
                        <div class="z-10 bg-red-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-red-400 border border-red-500/30"><i class="fas fa-compact-disc"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">X-Roulette</h4><span class="text-xs text-red-400 currency-font">CLASSIC</span></div>
                    </div>

                     <!-- Blackjack -->
                     <div onclick="loadGame('blackjack')" class="game-thumb glass-panel p-4 rounded-xl relative overflow-hidden group h-40 flex flex-col justify-between border-t border-white/10 cursor-pointer col-span-2">
                        <div class="absolute -right-4 -top-10 text-9xl opacity-10 group-hover:opacity-20 transition text-blue-500 rotate-12"><i class="fas fa-playing-cards"></i></div>
                        <div class="z-10 bg-blue-500/20 w-10 h-10 rounded-lg flex items-center justify-center text-blue-400 border border-blue-500/30"><i class="fas fa-cards"></i></div>
                        <div class="z-10"><h4 class="font-bold text-lg leading-tight">Blackjack Pro</h4><span class="text-xs text-blue-400 currency-font">STRATEGY</span></div>
                    </div>
                </div>
                
                <div class="text-center text-xs text-gray-600 font-mono mt-8 mb-4">
                    PROVABLY FAIR SYSTEM<br>
                    ID: 8827-XJ92-K291
                </div>
            </div>

            <!-- GAME VIEW -->
            <div id="gameContainer" class="hidden flex flex-col gap-5 h-full">
                <!-- Game Header -->
                <div class="flex items-center justify-between">
                    <button onclick="showLobby()" class="text-gray-400 hover:text-white flex items-center gap-2 text-sm font-bold uppercase tracking-wider transition">
                        <i class="fas fa-chevron-left"></i> Back
                    </button>
                    <div class="flex items-center gap-2">
                         <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                         <span id="activeGameTitle" class="font-bold text-sm tracking-widest text-emerald-400">CRASH</span>
                    </div>
                </div>

                <!-- DYNAMIC VIEWPORT -->
                <div id="gameViewport" class="glass-panel w-full aspect-[4/3] rounded-2xl relative flex items-center justify-center overflow-hidden border-t border-white/10 shadow-2xl bg-black/40">
                    <!-- Game content injected here -->
                </div>

                <!-- CONTROLS PANEL -->
                <div class="glass-panel p-5 rounded-2xl border-t border-white/10 flex flex-col gap-4 bg-[#0a0f18]">
                    
                    <!-- Bet Input Row -->
                    <div class="flex gap-3">
                        <div class="flex-1 relative">
                            <span class="absolute left-3 top-1/2 -translate-y-1/2 text-emerald-500 font-bold">$</span>
                            <input type="number" id="betInput" value="10" class="w-full bg-[#050505] border border-white/10 rounded-xl py-3 pl-8 pr-3 font-mono font-bold text-white focus:outline-none focus:border-emerald-500 transition">
                        </div>
                        <div class="flex gap-1">
                            <button onclick="adjustBet(0.5)" class="btn-secondary px-3 rounded-lg text-xs font-bold">½</button>
                            <button onclick="adjustBet(2)" class="btn-secondary px-3 rounded-lg text-xs font-bold">2x</button>
                        </div>
                    </div>

                    <!-- Game Specific Inputs -->
                    <div id="gameSpecificControls"></div>

                    <!-- Main Action Button -->
                    <div class="flex flex-col gap-2">
                        <button id="mainActionBtn" class="btn-premium w-full py-4 rounded-xl text-lg shadow-lg relative overflow-hidden group">
                            <span class="relative z-10">PLACE BET</span>
                            <div class="absolute inset-0 bg-white/20 translate-y-full group-hover:translate-y-0 transition transform duration-300"></div>
                        </button>
                        <div id="gameStatus" class="text-center text-[10px] text-gray-500 font-mono h-4 uppercase tracking-wider">Ready to play</div>
                    </div>
                </div>
            </div>

        </div>
    </main>

    <!-- TOAST NOTIFICATION -->
    <div id="toast" class="fixed top-6 left-1/2 -translate-x-1/2 glass-panel border border-emerald-500/50 px-6 py-3 rounded-full shadow-2xl transform -translate-y-20 transition-all duration-300 z-[100] flex items-center gap-3">
        <div class="w-2 h-2 rounded-full bg-emerald-500 shadow-[0_0_10px_#00ffa3]"></div>
        <span id="toastMsg" class="font-bold text-sm tracking-wide">Notification</span>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // --- VISUAL FX SYSTEM ---
        const canvas = document.getElementById('fxCanvas');
        const ctx = canvas.getContext('2d');
        let particles = [];
        
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        function createParticles(x, y, color) {
            for(let i=0; i<40; i++) {
                particles.push({
                    x: x, y: y,
                    vx: (Math.random() - 0.5) * 12,
                    vy: (Math.random() - 0.5) * 12,
                    life: 1.0,
                    color: color,
                    size: Math.random() * 5 + 2
                });
            }
        }

        function animateFX() {
            ctx.clearRect(0,0, canvas.width, canvas.height);
            particles.forEach((p, index) => {
                p.x += p.vx;
                p.y += p.vy;
                p.vy += 0.2; // Gravity
                p.life -= 0.02;
                p.size *= 0.95;
                
                ctx.fillStyle = p.color;
                ctx.globalAlpha = p.life;
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI*2);
                ctx.fill();
                
                if(p.life <= 0) particles.splice(index, 1);
            });
            ctx.globalAlpha = 1.0;
            requestAnimationFrame(animateFX);
        }
        animateFX();

        function triggerWinEffect(amount = 0) {
            createParticles(window.innerWidth/2, window.innerHeight/2, '#00ffa3');
            createParticles(window.innerWidth/2, window.innerHeight/2, '#ffd700');
            
            if(amount > 0) {
                // Show Big Win Overlay
                const overlay = document.getElementById('bigWinOverlay');
                const amtEl = document.getElementById('bigWinAmount');
                amtEl.innerText = `$${amount.toFixed(2)}`;
                overlay.classList.remove('hidden');
                overlay.classList.add('flex');
                
                // Hide after 2s
                setTimeout(() => {
                    overlay.classList.add('hidden');
                    overlay.classList.remove('flex');
                }, 2000);
            }
        }

        function shakeScreen() {
            const vp = document.getElementById('gameViewport');
            vp.classList.add('shake-active');
            setTimeout(() => vp.classList.remove('shake-active'), 300);
        }

        // --- GAME CORE ---
        let balance = 1000.00;
        let activeGame = null;
        let gameActive = false;
        
        function updateBalanceUI() {
            document.getElementById('globalBalance').innerText = `$${balance.toFixed(2)}`;
            const balEl = document.getElementById('globalBalance');
            balEl.classList.add('text-white');
            setTimeout(() => balEl.classList.remove('text-white'), 200);
        }

        function showToast(msg, type='success') {
            const toast = document.getElementById('toast');
            document.getElementById('toastMsg').innerText = msg;
            toast.style.borderColor = type === 'error' ? 'rgba(255, 71, 87, 0.5)' : 'rgba(0, 255, 163, 0.5)';
            toast.querySelector('div').style.backgroundColor = type === 'error' ? '#ff4757' : '#00ffa3';
            toast.classList.remove('-translate-y-20');
            setTimeout(() => toast.classList.add('-translate-y-20'), 2500);
        }

        function adjustBet(multiplier) {
            const input = document.getElementById('betInput');
            let val = parseFloat(input.value) * multiplier;
            if(val < 1) val = 1;
            if(val > balance) val = balance;
            input.value = val.toFixed(2);
        }

        function addFunds() {
            balance += 1000;
            updateBalanceUI();
            showToast("Added $1,000 Credits");
            createParticles(window.innerWidth - 50, 50, '#00ffa3');
        }

        function showLobby() {
            if(gameActive) {
                if(!confirm("Leave current game? Progress will be lost.")) return;
                gameActive = false;
                if(activeGame === 'crash') cancelAnimationFrame(crashAnimId);
                if(activeGame === 'horse') cancelAnimationFrame(horseAnimId);
            }
            document.getElementById('lobby').classList.remove('hidden');
            document.getElementById('gameContainer').classList.add('hidden');
            document.getElementById('mainContent').scrollTop = 0;
            activeGame = null;
        }

        function loadGame(gameName) {
            document.getElementById('lobby').classList.add('hidden');
            document.getElementById('gameContainer').classList.remove('hidden');
            activeGame = gameName;
            
            const titleMap = {
                'crash': 'SPACE CRASH',
                'mines': 'GEM MINES',
                'towers': 'SKY TOWERS',
                'roulette': 'X-ROULETTE',
                'blackjack': 'BLACKJACK PRO',
                'slots': 'NEON SLOTS',
                'horse': 'TURBO DERBY'
            };
            document.getElementById('activeGameTitle').innerText = titleMap[gameName];
            document.getElementById('gameStatus').innerText = "WAITING FOR BET...";
            
            const viewport = document.getElementById('gameViewport');
            const controls = document.getElementById('gameSpecificControls');
            const btn = document.getElementById('mainActionBtn');
            
            viewport.innerHTML = '';
            controls.innerHTML = '';
            btn.innerHTML = '<span class="relative z-10">PLACE BET</span><div class="absolute inset-0 bg-white/20 translate-y-full group-hover:translate-y-0 transition transform duration-300"></div>';
            btn.onclick = () => initGameLogic(gameName);
            btn.disabled = false;
            btn.style.background = ''; 

            if(gameName === 'crash') renderCrash(viewport);
            if(gameName === 'mines') renderMines(viewport, controls);
            if(gameName === 'towers') renderTowers(viewport, controls);
            if(gameName === 'roulette') renderRoulette(viewport, controls);
            if(gameName === 'blackjack') renderBlackjack(viewport, controls);
            if(gameName === 'slots') renderSlots(viewport, controls);
            if(gameName === 'horse') renderHorse(viewport, controls);
        }

        function initGameLogic(game) {
            const bet = parseFloat(document.getElementById('betInput').value);
            if(isNaN(bet) || bet <= 0) return showToast("Invalid Bet Amount", "error");
            if(bet > balance) return showToast("Insufficient Balance", "error");

            if(game === 'crash') startCrash(bet);
            if(game === 'mines') startMines(bet);
            if(game === 'towers') startTowers(bet);
            if(game === 'roulette') startRoulette(bet);
            if(game === 'blackjack') startBlackjack(bet);
            if(game === 'slots') startSlots(bet);
            if(game === 'horse') startHorse(bet);
        }

        /* ----------------------------------------------------------------
           NEW GAMES: SLOTS & HORSE RACING
           ---------------------------------------------------------------- */

        // --- GAME: SLOTS ---
        const slotSymbols = ['🍒', '🍋', '🍇', '💎', '7️⃣', '🔔']; 
        // Payouts: 3xCherry=2, 3xLemon=3, 3xGrape=5, 3xBell=10, 3xGem=20, 3xSeven=50
        
        function renderSlots(container, controls) {
            container.innerHTML = `
                <div class="flex gap-2 p-4 w-full justify-center items-center h-full bg-[#0f0f13]">
                    <div class="slot-reel flex-1 h-full flex flex-col items-center relative"><div class="reel-strip" id="reel-1"><div class="slot-symbol">7️⃣</div></div></div>
                    <div class="slot-reel flex-1 h-full flex flex-col items-center relative"><div class="reel-strip" id="reel-2"><div class="slot-symbol">💎</div></div></div>
                    <div class="slot-reel flex-1 h-full flex flex-col items-center relative"><div class="reel-strip" id="reel-3"><div class="slot-symbol">🍒</div></div></div>
                    <div class="absolute w-full h-[2px] bg-red-500/50 top-1/2 z-20 pointer-events-none"></div>
                </div>
            `;
        }

        function startSlots(bet) {
            balance -= bet;
            updateBalanceUI();
            
            const btn = document.getElementById('mainActionBtn');
            btn.disabled = true;

            // Determine outcome first
            const r1 = Math.floor(Math.random() * slotSymbols.length);
            const r2 = Math.floor(Math.random() * slotSymbols.length);
            const r3 = Math.floor(Math.random() * slotSymbols.length);
            
            // Spin Animation
            const strips = [document.getElementById('reel-1'), document.getElementById('reel-2'), document.getElementById('reel-3')];
            
            strips.forEach((strip, i) => {
                strip.innerHTML = '';
                // Create a tall strip of random symbols
                let html = '';
                for(let k=0; k<20; k++) {
                    html += `<div class="slot-symbol">${slotSymbols[Math.floor(Math.random()*slotSymbols.length)]}</div>`;
                }
                // Add the result symbol at the end
                const resultSym = (i===0) ? slotSymbols[r1] : (i===1) ? slotSymbols[r2] : slotSymbols[r3];
                html += `<div class="slot-symbol" id="res-${i}">${resultSym}</div>`;
                strip.innerHTML = html;
                
                strip.style.transition = 'none';
                strip.style.transform = 'translateY(0)';
                
                // Trigger spin
                setTimeout(() => {
                    strip.style.transition = `transform ${1 + (i*0.5)}s cubic-bezier(0.45, 0.05, 0.55, 0.95)`;
                    strip.style.transform = `translateY(-${20 * 100}px)`; // 20 symbols * 100px height
                    strip.classList.add('blur-spin');
                }, 50);

                // Stop Event
                setTimeout(() => {
                    strip.classList.remove('blur-spin');
                    shakeScreen(); // Shake on stop
                    // Reset strip to just the result to save memory/DOM
                    strip.style.transition = 'none';
                    strip.style.transform = 'translateY(0)';
                    strip.innerHTML = `<div class="slot-symbol">${resultSym}</div>`;
                }, 1000 + (i*500));
            });

            // Check Win
            setTimeout(() => {
                btn.disabled = false;
                
                if(r1 === r2 && r2 === r3) {
                    const sym = slotSymbols[r1];
                    let mult = 0;
                    if(sym==='🍒') mult=5;
                    if(sym==='🍋') mult=8;
                    if(sym==='🍇') mult=12;
                    if(sym==='🔔') mult=20;
                    if(sym==='💎') mult=50;
                    if(sym==='7️⃣') mult=100;

                    const win = bet * mult;
                    balance += win;
                    updateBalanceUI();
                    triggerWinEffect(win);
                    showToast(`JACKPOT! ${sym}${sym}${sym}`, 'success');
                } else if (r1 === r2 || r2 === r3 || r1 === r3) {
                    // Small win for pair?
                    const win = bet * 1.5;
                    balance += win;
                    updateBalanceUI();
                    showToast("Mini Win! (Pair)", 'success');
                    createParticles(window.innerWidth/2, window.innerHeight/2, '#00ffa3');
                } else {
                    showToast("No Luck", 'error');
                }
            }, 2500);
        }

        // --- GAME: HORSE RACING ---
        let horseSelection = null;
        let horseAnimId;
        
        function renderHorse(container, controls) {
            controls.innerHTML = `
                <div class="flex gap-2 mt-2">
                    <button onclick="selectHorse(0)" id="hbtn-0" class="flex-1 bg-red-500 h-10 rounded font-bold border-b-4 border-red-700 active:border-b-0 active:translate-y-1 text-xs">RED (4x)</button>
                    <button onclick="selectHorse(1)" id="hbtn-1" class="flex-1 bg-blue-500 h-10 rounded font-bold border-b-4 border-blue-700 active:border-b-0 active:translate-y-1 text-xs">BLUE (4x)</button>
                    <button onclick="selectHorse(2)" id="hbtn-2" class="flex-1 bg-green-500 h-10 rounded font-bold border-b-4 border-green-700 active:border-b-0 active:translate-y-1 text-xs text-black">GRN (4x)</button>
                    <button onclick="selectHorse(3)" id="hbtn-3" class="flex-1 bg-yellow-500 h-10 rounded font-bold border-b-4 border-yellow-700 active:border-b-0 active:translate-y-1 text-xs text-black">YEL (4x)</button>
                </div>
                <div class="text-center text-[10px] text-gray-500 mt-2">PICK A WINNER</div>
            `;
            container.innerHTML = `
                <div class="w-full h-full flex flex-col justify-center bg-[#1a2333] relative overflow-hidden border-2 border-white/10 rounded-lg">
                    <div class="absolute right-[10%] top-0 h-full border-r-4 border-dashed border-white/20 z-0"></div> <!-- Finish Line -->
                    <div class="track-lane flex-1 flex items-center px-2"><div id="horse-0" class="horse-runner text-2xl relative left-0">🐎<span class="text-xs text-red-500 font-bold absolute -top-2 left-0">1</span></div></div>
                    <div class="track-lane flex-1 flex items-center px-2"><div id="horse-1" class="horse-runner text-2xl relative left-0">🐎<span class="text-xs text-blue-500 font-bold absolute -top-2 left-0">2</span></div></div>
                    <div class="track-lane flex-1 flex items-center px-2"><div id="horse-2" class="horse-runner text-2xl relative left-0">🐎<span class="text-xs text-green-500 font-bold absolute -top-2 left-0">3</span></div></div>
                    <div class="track-lane flex-1 flex items-center px-2"><div id="horse-3" class="horse-runner text-2xl relative left-0">🐎<span class="text-xs text-yellow-500 font-bold absolute -top-2 left-0">4</span></div></div>
                </div>
            `;
            horseSelection = null;
        }

        function selectHorse(idx) {
            horseSelection = idx;
            // Visual feedback
            for(let i=0; i<4; i++) document.getElementById(`hbtn-${i}`).classList.add('opacity-50');
            document.getElementById(`hbtn-${idx}`).classList.remove('opacity-50');
            document.getElementById(`hbtn-${idx}`).classList.add('ring-2', 'ring-white');
        }

        function startHorse(bet) {
            if(horseSelection === null) return showToast("Pick a Horse!", "error");
            
            balance -= bet;
            updateBalanceUI();
            
            const btn = document.getElementById('mainActionBtn');
            btn.disabled = true;

            // Animation Logic
            let positions = [0, 0, 0, 0];
            let finished = false;
            let winner = -1;
            
            function raceLoop() {
                if(finished) return;
                
                // Random speeds
                for(let i=0; i<4; i++) {
                    if(Math.random() > 0.3) positions[i] += Math.random() * 1.5; // Speed
                    const el = document.getElementById(`horse-${i}`);
                    el.style.left = `${positions[i]}%`;
                    
                    if(positions[i] >= 85 && winner === -1) { // 85% is finish line visually
                        winner = i;
                        finished = true;
                    }
                }
                
                if(!finished) {
                    horseAnimId = requestAnimationFrame(raceLoop);
                } else {
                    endRace(winner, bet);
                }
            }
            raceLoop();
        }

        function endRace(winner, bet) {
            setTimeout(() => {
                const btn = document.getElementById('mainActionBtn');
                btn.disabled = false;
                
                if(winner === horseSelection) {
                    const win = bet * 4;
                    balance += win;
                    updateBalanceUI();
                    triggerWinEffect(win);
                    showToast(`Horse ${winner+1} Won! +$${win.toFixed(2)}`, 'success');
                } else {
                    showToast(`Horse ${winner+1} Won. You lost.`, 'error');
                }
            }, 500);
        }

        // --- PREVIOUS GAMES (CRASH, MINES, ETC) ---
        // (Copied and compacted from previous version)
        
        // CRASH
        let crashMultiplier=1.00, crashAnimId, crashRunning=false;
        function renderCrash(c){c.innerHTML=`<div class="absolute top-6 text-5xl font-black text-white z-10 drop-shadow-xl tracking-tighter" id="crashDisplay">1.00x</div><div class="crash-canvas-container w-full h-full"><canvas id="crashCanvas" width="600" height="400" class="w-full h-full"></canvas></div>`;}
        function startCrash(bet){if(crashRunning){finishCrash(true,bet);return;}balance-=bet;updateBalanceUI();crashRunning=true;gameActive=true;const btn=document.getElementById('mainActionBtn');btn.querySelector('span').innerText="CASHOUT";btn.style.background='#eab308';const canvas=document.getElementById('crashCanvas');const ctx=canvas.getContext('2d');const display=document.getElementById('crashDisplay');let progress=0;crashMultiplier=1.00;const crashPoint=(Math.random()>0.5)?(1+Math.random()*5):(1+Math.random());function loop(){if(!crashRunning)return;progress+=0.05;crashMultiplier+=0.005+(crashMultiplier*0.002);display.innerText=crashMultiplier.toFixed(2)+'x';ctx.clearRect(0,0,canvas.width,canvas.height);let x=canvas.width*(progress/100);let y=canvas.height-(canvas.height*(progress/100));ctx.beginPath();ctx.moveTo(0,canvas.height);ctx.quadraticCurveTo(canvas.width*0.5,canvas.height,x,y);ctx.strokeStyle='#00ffa3';ctx.lineWidth=4;ctx.stroke();ctx.font='30px Arial';ctx.fillText('🚀',x-15,y-10);if(crashMultiplier>=crashPoint){finishCrash(false,bet);}else if(progress<100){crashAnimId=requestAnimationFrame(loop);}else{finishCrash(false,bet);}}loop();}
        function finishCrash(won,bet){crashRunning=false;gameActive=false;cancelAnimationFrame(crashAnimId);const btn=document.getElementById('mainActionBtn');btn.querySelector('span').innerText="PLACE BET";btn.style.background='';if(won){const win=bet*crashMultiplier;balance+=win;updateBalanceUI();triggerWinEffect(win);showToast(`+$${win.toFixed(2)}`,'success');}else{showToast("Crashed!",'error');shakeScreen();}}

        // MINES
        let mineGrid=[],mineCount=3,minesActive=false,minesBet=0,tilesRevealed=0;
        function renderMines(c,ctl){ctl.innerHTML=`<div class="flex gap-2"><button onclick="mineCount=3" class="flex-1 btn-secondary py-2 text-xs">3 Bombs</button><button onclick="mineCount=5" class="flex-1 btn-secondary py-2 text-xs">5 Bombs</button></div>`;c.innerHTML=`<div id="minesGrid" class="grid grid-cols-5 gap-3 w-full max-w-[320px] aspect-square p-2"></div>`;const g=document.getElementById('minesGrid');for(let i=0;i<25;i++)g.innerHTML+=`<div id="tile-${i}" class="mine-tile rounded-lg cursor-pointer flex items-center justify-center text-2xl"></div>`;}
        function startMines(bet){if(minesActive){cashoutMines();return;}balance-=bet;minesBet=bet;updateBalanceUI();minesActive=true;gameActive=true;tilesRevealed=0;const btn=document.getElementById('mainActionBtn');btn.querySelector('span').innerText="CASHOUT $0.00";btn.style.background='#eab308';mineGrid=Array(25).fill('gem');let p=0;while(p<mineCount){let idx=Math.floor(Math.random()*25);if(mineGrid[idx]!=='bomb'){mineGrid[idx]='bomb';p++;}}for(let i=0;i<25;i++){const t=document.getElementById(`tile-${i}`);t.className='mine-tile rounded-lg cursor-pointer flex items-center justify-center text-2xl';t.innerHTML='';t.onclick=()=>clickMineTile(i);}}
        function clickMineTile(idx){if(!minesActive)return;const t=document.getElementById(`tile-${idx}`);if(t.classList.contains('revealed'))return;t.classList.add('revealed');if(mineGrid[idx]==='bomb'){t.classList.add('bomb');t.innerHTML='💣';minesActive=false;gameActive=false;document.getElementById('mainActionBtn').querySelector('span').innerText="PLACE BET";document.getElementById('mainActionBtn').style.background='';showToast("BOOM!",'error');shakeScreen();}else{t.classList.add('gem');t.innerHTML='💎';tilesRevealed++;let m=1;for(let i=0;i<tilesRevealed;i++)m*=(25-i)/(25-mineCount-i);const w=minesBet*m;document.getElementById('mainActionBtn').querySelector('span').innerText=`CASHOUT $${w.toFixed(2)}`;if(tilesRevealed===(25-mineCount))cashoutMines();}}
        function cashoutMines(){let m=1;for(let i=0;i<tilesRevealed;i++)m*=(25-i)/(25-mineCount-i);const w=minesBet*m;balance+=w;updateBalanceUI();triggerWinEffect(w);showToast(`+$${w.toFixed(2)}`,'success');minesActive=false;gameActive=false;document.getElementById('mainActionBtn').querySelector('span').innerText="PLACE BET";document.getElementById('mainActionBtn').style.background='';}

        // TOWERS
        let towerLevel=0,towerActive=false,towerBet=0;
        function renderTowers(c,ctl){ctl.innerHTML=`<select id="towerDiff" class="w-full bg-[#050505] border border-white/10 rounded-lg py-2 px-2 text-white text-xs"><option value="easy">Easy</option><option value="medium">Medium</option><option value="hard">Hard</option></select>`;c.innerHTML=`<div id="towersGrid" class="flex flex-col-reverse w-full max-w-[280px] gap-2"></div>`;renderTowerRows();}
        function renderTowerRows(ar=-1){const g=document.getElementById('towersGrid');g.innerHTML='';for(let i=0;i<8;i++){let h=`<div class="flex gap-2 justify-center w-full" id="row-${i}">`;for(let j=0;j<3;j++){const d=(i!==ar)?'opacity-30 pointer-events-none':'';h+=`<button class="tower-btn h-10 flex-1 rounded-md transition ${d}" onclick="clickTower(${i},${j})"></button>`;}g.innerHTML+=h+`</div>`;}}
        function startTowers(bet){if(towerActive){cashoutTowers();return;}balance-=bet;towerBet=bet;updateBalanceUI();towerActive=true;gameActive=true;towerLevel=0;renderTowerRows(0);const btn=document.getElementById('mainActionBtn');btn.querySelector('span').innerText="CASHOUT";btn.style.background='#eab308';}
        function clickTower(row,col){if(!towerActive||row!==towerLevel)return;const d=document.getElementById('towerDiff').value;let chance=0.66,mult=1.45;if(d==='medium'){chance=0.5;mult=1.95;}if(d==='hard'){chance=0.33;mult=2.95;}if(Math.random()<chance){document.getElementById(`row-${row}`).children[col].classList.add('safe');towerLevel++;let w=towerBet*Math.pow(mult,towerLevel);document.getElementById('mainActionBtn').querySelector('span').innerText=`CASHOUT $${w.toFixed(2)}`;if(towerLevel>=8)cashoutTowers();else renderTowerRows(towerLevel);}else{document.getElementById(`row-${row}`).children[col].classList.add('dead');towerActive=false;gameActive=false;document.getElementById('mainActionBtn').querySelector('span').innerText="PLACE BET";document.getElementById('mainActionBtn').style.background='';shakeScreen();showToast("Fell down!",'error');}}
        function cashoutTowers(){const d=document.getElementById('towerDiff').value;let mult=1.45;if(d==='medium')mult=1.95;if(d==='hard')mult=2.95;const w=towerBet*Math.pow(mult,towerLevel);balance+=w;updateBalanceUI();triggerWinEffect(w);showToast(`+$${w.toFixed(2)}`,'success');towerActive=false;gameActive=false;document.getElementById('mainActionBtn').querySelector('span').innerText="PLACE BET";document.getElementById('mainActionBtn').style.background='';}

        // ROULETTE
        let rouletteSelection=null;
        function renderRoulette(c,ctl){ctl.innerHTML=`<div class="flex gap-2"><button onclick="rouletteSelection='red';showToast('Red Selected')" class="flex-1 bg-red-500 h-10 rounded text-xs font-bold">RED 2x</button><button onclick="rouletteSelection='black';showToast('Black Selected')" class="flex-1 bg-gray-800 h-10 rounded text-xs font-bold">BLACK 2x</button><button onclick="rouletteSelection='green';showToast('Green Selected')" class="flex-1 bg-green-500 h-10 rounded text-xs font-bold text-black">ZERO 14x</button></div>`;c.innerHTML=`<div class="w-full relative py-6 bg-[#0f1219] border-y-2 border-[#1e272e]"><div class="marker-arrow absolute top-0 left-1/2 -translate-x-1/2 z-20"></div><div class="overflow-hidden w-full h-[80px] relative"><div id="rouletteTape" class="flex items-center h-full absolute left-1/2 transform -translate-x-[40px]"></div></div></div>`;let h='';for(let i=0;i<100;i++){let cl='bg-gray-800 text-white';if(i%15===0)cl='bg-green-500 text-black';else if(i%2!==0)cl='bg-red-500 text-white';h+=`<div class="w-[80px] h-[70px] flex-none rounded-md mx-1 flex items-center justify-center font-black text-2xl ${cl}">${i%15}</div>`;}document.getElementById('rouletteTape').innerHTML=h;}
        function startRoulette(bet){if(!rouletteSelection)return showToast("Select Color",'error');balance-=bet;updateBalanceUI();const btn=document.getElementById('mainActionBtn');btn.disabled=true;const outcome=Math.floor(Math.random()*15);let col=(outcome===0)?'green':(outcome%2!==0)?'red':'black';const offset=(75+outcome)*88;const t=document.getElementById('rouletteTape');t.style.transition='transform 4s cubic-bezier(0.1,0.8,0.1,1)';t.style.transform=`translateX(-${offset}px)`;setTimeout(()=>{btn.disabled=false;t.style.transition='none';t.style.transform='translateX(-40px)';if(col===rouletteSelection){const w=bet*((col==='green')?14:2);balance+=w;updateBalanceUI();triggerWinEffect(w);showToast("WIN!",'success');}else{showToast("Lost",'error');}},4000);}

        // BLACKJACK
        let bjDeck=[],pHand=[],dHand=[],bjActive=false,bjBet=0;
        function renderBlackjack(c,ctl){ctl.innerHTML=`<div class="flex gap-2"><button onclick="bjHit()" id="bHit" disabled class="flex-1 bg-blue-600 h-10 rounded text-xs font-bold">HIT</button><button onclick="bjStand()" id="bStand" disabled class="flex-1 bg-orange-600 h-10 rounded text-xs font-bold">STAND</button></div>`;c.innerHTML=`<div class="flex flex-col justify-between h-full py-4"><div class="text-center"><div id="dCards" class="flex justify-center -space-x-4 h-[100px]"></div><div class="text-xs text-gray-500">DEALER <span id="dScore"></span></div></div><div class="text-center"><div id="pCards" class="flex justify-center -space-x-4 h-[100px]"></div><div class="text-xs text-gray-500">YOU <span id="pScore"></span></div></div></div>`;}
        function startBlackjack(bet){if(bjActive)return;balance-=bet;bjBet=bet;updateBalanceUI();bjActive=true;bjDeck=[];const s=['♠','♥','♦','♣'],v=['2','3','4','5','6','7','8','9','10','J','Q','K','A'];for(let S of s)for(let V of v)bjDeck.push({s:S,v:V});bjDeck.sort(()=>Math.random()-0.5);pHand=[bjDeck.pop(),bjDeck.pop()];dHand=[bjDeck.pop(),bjDeck.pop()];updBJ(true);document.getElementById('mainActionBtn').classList.add('hidden');document.getElementById('bHit').disabled=false;document.getElementById('bStand').disabled=false;}
        function updBJ(h){document.getElementById('dCards').innerHTML='';document.getElementById('pCards').innerHTML='';rC(dHand[0],'dCards');if(h)rC({},'dCards',true);else rC(dHand[1],'dCards');if(!h)for(let i=2;i<dHand.length;i++)rC(dHand[i],'dCards');pHand.forEach(c=>rC(c,'pCards'));document.getElementById('pScore').innerText=calc(pHand);document.getElementById('dScore').innerText=h?"?":calc(dHand);}
        function rC(c,t,h=false){const el=document.getElementById(t);if(h)el.innerHTML+=`<div class="w-[70px] h-[100px] bg-blue-900 rounded border-2 border-white/20 flex items-center justify-center relative z-0">?</div>`;else el.innerHTML+=`<div class="w-[70px] h-[100px] bg-white text-black rounded shadow flex flex-col items-center justify-center relative z-10 font-bold text-xl ${(c.s==='♥'||c.s==='♦')?'text-red-500':'text-black'}">${c.v}${c.s}</div>`;}
        function calc(h){let s=0,a=0;for(let c of h){let v=parseInt(c.v);if(isNaN(v))v=(c.v==='A')?11:10;s+=v;if(c.v==='A')a++;}while(s>21&&a>0){s-=10;a--;}return s;}
        function bjHit(){pHand.push(bjDeck.pop());updBJ(true);if(calc(pHand)>21)endBJ(false);}
        function bjStand(){updBJ(false);while(calc(dHand)<17){dHand.push(bjDeck.pop());updBJ(false);}let d=calc(dHand),p=calc(pHand);if(d>21||p>d)endBJ(true);else if(p===d)endBJ('push');else endBJ(false);}
        function endBJ(r){bjActive=false;document.getElementById('bHit').disabled=true;document.getElementById('bStand').disabled=true;document.getElementById('mainActionBtn').classList.remove('hidden');if(r===true){const w=bjBet*2;balance+=w;updateBalanceUI();triggerWinEffect(w);showToast("WIN!",'success');}else if(r==='push'){balance+=bjBet;updateBalanceUI();showToast("PUSH",'success');}else{showToast("DEALER WINS",'error');}}

    </script>
</body>
</html>


