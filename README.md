<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Quantum Revolution: An Interactive Presentation</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            overscroll-behavior: none;
        }
        .slide {
            min-height: 100vh;
            scroll-snap-align: start;
            display: none; /* Hidden by default, JS will manage visibility */
        }
        .slide.active {
            display: flex;
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        #padlock-icon.shattered {
            animation: shatter 0.5s forwards;
        }
        @keyframes shatter {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(1.5) rotate(20deg); opacity: 0; }
        }
        .hndl-item {
            animation: float-up 5s linear infinite;
        }
        @keyframes float-up {
            0% { transform: translateY(100%); opacity: 0; }
            10%, 90% { opacity: 1; }
            100% { transform: translateY(-100%); opacity: 0; }
        }
        .attack-wave {
            animation: move-wave 1.5s forwards;
        }
        @keyframes move-wave {
            0% { transform: translateX(-100%) scaleX(0.5); opacity: 0.5; }
            50% { opacity: 1; }
            100% { transform: translateX(0) scaleX(1); opacity: 0; }
        }
        .shield-effect {
            animation: shield-pulse 0.5s;
        }
        @keyframes shield-pulse {
            0% { transform: scale(1); opacity: 0; }
            50% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(1); opacity: 0; }
        }
    </style>
</head>
<body class="bg-gray-900 text-white overflow-hidden">

    <div id="presentation-container" class="relative w-full h-screen">

        <!-- Slide 1: Title -->
        <section id="slide-1" class="slide active flex-col justify-center items-center text-center p-8 relative">
            <canvas id="q-canvas" class="absolute top-0 left-0 w-full h-full z-0"></canvas>
            <div class="relative z-10 glass-panel rounded-2xl p-8 md:p-12 max-w-4xl">
                <h1 class="text-4xl md:text-6xl font-bold text-cyan-300 drop-shadow-lg">The Quantum Revolution</h1>
                <h2 class="text-xl md:text-2xl mt-4 text-gray-200">Securing Our Digital Future</h2>
                <p class="mt-6 max-w-2xl mx-auto text-gray-300">An interactive guide to understanding the threat and preparing for Post-Quantum Cryptography (PQC).</p>
                <button onclick="changeSlide(1)" class="mt-8 bg-cyan-500 hover:bg-cyan-400 text-white font-bold py-3 px-8 rounded-lg transition-transform transform hover:scale-105">Start Presentation</button>
            </div>
        </section>

        <!-- Slide 2: A New Kind of Computing -->
        <section id="slide-2" class="slide flex-col justify-center items-center p-8 bg-gray-800">
            <div class="w-full max-w-5xl text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-4 text-cyan-300">A New Kind of Computing</h2>
                <p class="text-lg text-gray-300 mb-8">Quantum computers aren't just faster—they play by different rules.</p>
                <div class="flex flex-col md:flex-row justify-around items-center gap-8">
                    <!-- Classical Computer -->
                    <div class="w-full md:w-1/2 p-6 bg-gray-700 rounded-2xl">
                        <h3 class="text-2xl font-semibold mb-4">Classical Bit</h3>
                        <div class="flex justify-center items-center h-24">
                            <div id="classical-bit" class="w-16 h-16 rounded-full transition-colors duration-300 bg-blue-500 flex justify-center items-center text-3xl font-bold">0</div>
                        </div>
                        <button onclick="runClassicalComputer()" class="mt-4 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-6 rounded-lg">Flip Bit</button>
                        <p class="mt-4 text-gray-400">Always in a definite state: either 0 or 1.</p>
                    </div>
                    <!-- Quantum Computer -->
                    <div class="w-full md:w-1/2 p-6 bg-gray-700 rounded-2xl border-2 border-cyan-400">
                        <h3 class="text-2xl font-semibold mb-4">Quantum Qubit</h3>
                        <div class="flex justify-center items-center h-24">
                            <div id="qubit" class="w-16 h-16 rounded-full transition-all duration-300 flex justify-center items-center text-3xl font-bold" style="background: radial-gradient(circle, #67E8F9, #22D3EE);">?</div>
                        </div>
                        <button onclick="runQuantumComputer()" class="mt-4 bg-cyan-500 hover:bg-cyan-400 text-white font-bold py-2 px-6 rounded-lg">Measure Qubit</button>
                        <p class="mt-4 text-gray-400">Exists in a superposition of 0 and 1 until measured.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Slide 3: The Quantum Threat -->
        <section id="slide-3" class="slide flex-col justify-center items-center p-8 bg-gray-800 relative overflow-hidden">
            <div id="hndl-container" class="absolute top-0 left-0 w-full h-full z-0"></div>
            <div class="relative z-10 w-full max-w-5xl text-center">
                 <h2 class="text-3xl md:text-4xl font-bold mb-4 text-red-400">The Shattered Padlock</h2>
                 <p class="text-lg text-gray-300 mb-8">How quantum computers break today's encryption.</p>
                 <div class="flex justify-center items-center my-12">
                     <svg id="padlock-icon" class="w-32 h-32 text-green-400 transition-all" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path></svg>
                 </div>
                 <button onclick="runShor()" class="bg-red-500 hover:bg-red-400 text-white font-bold py-3 px-8 rounded-lg">Run Shor's Algorithm</button>
                 <p id="hndl-text" class="mt-8 text-gray-400 opacity-0 transition-opacity duration-500">Adversaries are now using "Harvest Now, Decrypt Later" (HNDL), storing your data to break it in the future.</p>
            </div>
        </section>
        
        <!-- Slide 4: The Solution: PQC -->
        <section id="slide-4" class="slide flex-col justify-center items-center p-8 bg-gray-800">
            <div class="w-full max-w-5xl text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-4 text-green-400">Building a Quantum-Resistant Future</h2>
                <p class="text-lg text-gray-300 mb-8">Post-Quantum Cryptography (PQC) is the new shield.</p>
                <div class="relative flex justify-center items-center my-12">
                    <div id="shield-effect-container" class="absolute inset-0 flex justify-center items-center"></div>
                    <svg class="w-32 h-32 text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"></path></svg>
                    <p class="absolute font-bold text-4xl text-white">PQC</p>
                </div>
                 <p class="text-gray-400 mb-6">Based on new math believed to be hard for ANY computer.</p>
                <div class="flex justify-center gap-4">
                    <button onclick="runAttack('classical')" class="bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-6 rounded-lg">Attack with Classical</button>
                    <button onclick="runAttack('quantum')" class="bg-cyan-500 hover:bg-cyan-400 text-white font-bold py-2 px-6 rounded-lg">Attack with Quantum</button>
                </div>
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/NIST_logo.svg/2560px-NIST_logo.svg.png" alt="NIST Logo" class="h-8 mx-auto mt-8 invert brightness-0">
                <p class="text-sm text-gray-500 mt-2">Standardized by NIST in 2024</p>
            </div>
        </section>

        <!-- Slide 5: Mosca's Theorem -->
        <section id="slide-5" class="slide flex-col justify-center items-center p-8 bg-gray-800">
            <div class="w-full max-w-5xl text-center">
                 <h2 class="text-3xl md:text-4xl font-bold mb-4 text-yellow-400">The Timeline for Action</h2>
                 <p class="text-lg text-gray-300 mb-2">When do you need to act? Mosca's Theorem helps: <span class="font-bold">X + Y > Z</span></p>
                 <p class="text-lg text-gray-300 mb-8">If the formula is true, you're already at risk.</p>
                 <div class="bg-gray-700 p-8 rounded-2xl w-full">
                    <!-- Sliders -->
                    <div class="space-y-6">
                        <div>
                           <label for="x-slider" class="flex justify-between font-semibold"><span>X: Data Secrecy Lifespan</span><span id="x-val">15 years</span></label>
                           <input id="x-slider" type="range" min="1" max="50" value="15" class="w-full h-2 bg-gray-600 rounded-lg appearance-none cursor-pointer">
                        </div>
                        <div>
                           <label for="y-slider" class="flex justify-between font-semibold"><span>Y: Migration Time</span><span id="y-val">5 years</span></label>
                           <input id="y-slider" type="range" min="1" max="20" value="5" class="w-full h-2 bg-gray-600 rounded-lg appearance-none cursor-pointer">
                        </div>
                        <div>
                           <label for="z-slider" class="flex justify-between font-semibold"><span>Z: Time Until Quantum Threat</span><span id="z-val">10 years</span></label>
                           <input id="z-slider" type="range" min="1" max="30" value="10" class="w-full h-2 bg-gray-600 rounded-lg appearance-none cursor-pointer">
                        </div>
                    </div>
                    <!-- Visualization -->
                     <div class="mt-8 pt-4 border-t border-gray-600">
                         <h3 class="font-bold text-lg mb-4">Risk Assessment</h3>
                         <div class="relative h-10 bg-gray-600 rounded-lg">
                            <div id="xy-bar" class="absolute top-0 left-0 h-10 bg-gradient-to-r from-orange-500 to-red-500 rounded-lg transition-all duration-300" style="width: 66.6%;"></div>
                            <div id="z-marker" class="absolute top-0 h-full border-l-4 border-dashed border-cyan-400 transition-all duration-300" style="left: 33.3%;">
                                <span class="absolute -top-6 -translate-x-1/2 text-cyan-300 font-bold">Z</span>
                            </div>
                         </div>
                         <div id="risk-status" class="mt-4 text-2xl font-bold p-4 rounded-lg bg-red-500/20 text-red-400">YOU ARE AT RISK</div>
                     </div>
                 </div>
            </div>
        </section>

        <!-- Slide 6: Summary -->
        <section id="slide-6" class="slide flex-col justify-center items-center p-8 bg-gray-800">
             <div class="w-full max-w-5xl text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-8 text-cyan-300">Your Quantum Readiness Checklist</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-gray-700 p-6 rounded-xl transform transition-transform hover:scale-105 hover:bg-gray-600">
                        <h3 class="text-xl font-bold text-red-400">The Threat is Real</h3>
                        <p class="mt-2 text-gray-300">Future quantum computers will break the encryption that currently protects our digital world.</p>
                    </div>
                    <div class="bg-gray-700 p-6 rounded-xl transform transition-transform hover:scale-105 hover:bg-gray-600">
                        <h3 class="text-xl font-bold text-orange-400">The Danger is Now</h3>
                        <p class="mt-2 text-gray-300">"Harvest Now, Decrypt Later" means data encrypted today is already at risk of future exposure.</p>
                    </div>
                    <div class="bg-gray-700 p-6 rounded-xl transform transition-transform hover:scale-105 hover:bg-gray-600">
                        <h3 class="text-xl font-bold text-green-400">The Solution is Here</h3>
                        <p class="mt-2 text-gray-300">Post-Quantum Cryptography (PQC) provides a path forward, with new global standards finalized.</p>
                    </div>
                    <div class="bg-gray-700 p-6 rounded-xl transform transition-transform hover:scale-105 hover:bg-gray-600">
                        <h3 class="text-xl font-bold text-yellow-400">The Action is Urgent</h3>
                        <p class="mt-2 text-gray-300">Organizations must begin the journey to become "crypto-agile" by planning their migration.</p>
                    </div>
                </div>
             </div>
        </section>

        <!-- Slide 7: Q&A -->
        <section id="slide-7" class="slide flex-col justify-center items-center p-8 text-center bg-gray-800">
            <div class="w-full max-w-5xl">
                <h2 class="text-4xl md:text-6xl font-bold mb-8 text-cyan-300">Q&A & Discussion</h2>
                <p class="text-2xl text-gray-300 mb-4">How does this apply to our organization?</p>
                <p class="text-2xl text-gray-300 mb-12">What are the first steps we can take?</p>
                 <svg class="w-24 h-24 mx-auto text-gray-500 mb-8" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                <button onclick="changeSlide(0)" class="bg-cyan-500 hover:bg-cyan-400 text-white font-bold py-3 px-8 rounded-lg">Restart</button>
            </div>
        </section>

    </div>

    <!-- Navigation -->
    <div id="navigation" class="absolute bottom-0 left-0 right-0 p-4 flex justify-between items-center z-20">
        <button id="prev-btn" onclick="changeSlide(currentSlide - 1)" class="bg-gray-700/50 hover:bg-gray-600/50 text-white font-bold py-2 px-4 rounded-lg hidden">&lt; Prev</button>
        <div id="progress-bar" class="w-1/2 h-2 bg-gray-700 rounded-full mx-4">
            <div id="progress-indicator" class="h-2 bg-cyan-400 rounded-full transition-all duration-300"></div>
        </div>
        <button id="next-btn" onclick="changeSlide(currentSlide + 1)" class="bg-gray-700/50 hover:bg-gray-600/50 text-white font-bold py-2 px-4 rounded-lg">Next &gt;</button>
    </div>

    <script>
        // --- Core Presentation Logic ---
        const slides = document.querySelectorAll('.slide');
        const totalSlides = slides.length;
        let currentSlide = 0;

        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const progressIndicator = document.getElementById('progress-indicator');
        
        function showSlide(index) {
            slides.forEach((slide, i) => {
                slide.classList.toggle('active', i === index);
            });
            updateNavigation();
        }

        function changeSlide(index) {
            currentSlide = (index + totalSlides) % totalSlides;
            showSlide(currentSlide);
        }

        function updateNavigation() {
            // Hide nav on first and last slide
            if (currentSlide === 0 || currentSlide === totalSlides -1) {
                document.getElementById('navigation').style.display = 'none';
            } else {
                 document.getElementById('navigation').style.display = 'flex';
            }
            prevBtn.style.display = currentSlide > 1 && currentSlide < totalSlides - 1 ? 'block' : 'none'; // Show prev only after slide 2
            nextBtn.style.display = currentSlide > 0 && currentSlide < totalSlides - 1 ? 'block' : 'none';
            
            // Update progress bar
            const progress = currentSlide > 0 ? ((currentSlide) / (totalSlides - 2)) * 100 : 0;
            progressIndicator.style.width = `${progress}%`;
        }

        // --- Slide 1: Quantum Canvas Animation ---
        const canvas = document.getElementById('q-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];
        
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 1;
                this.speedX = Math.random() * 2 - 1;
                this.speedY = Math.random() * 2 - 1;
                this.isQuantum = Math.random() > 0.5;
                this.color = this.isQuantum ? `hsla(${Math.random() * 60 + 180}, 100%, 70%, 0.8)`: 'rgba(255, 255, 255, 0.8)';
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.size > 0.2) this.size -= 0.01;
                if (this.x > canvas.width || this.x < 0) this.speedX *= -1;
                if (this.y > canvas.height || this.y < 0) this.speedY *= -1;
                 if (this.isQuantum) {
                    this.color = `hsla(${Math.random() * 60 + 180}, 100%, 70%, 0.8)`;
                }
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function initParticles() {
            particles = [];
            for (let i = 0; i < 100; i++) {
                particles.push(new Particle());
            }
        }
        
        function animateCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateCanvas);
        }

        // --- Slide 2: Computer Simulation ---
        const classicalBit = document.getElementById('classical-bit');
        const qubit = document.getElementById('qubit');
        let bitState = 0;

        function runClassicalComputer() {
            bitState = 1 - bitState; // flip between 0 and 1
            classicalBit.textContent = bitState;
            classicalBit.style.backgroundColor = bitState === 0 ? '#3B82F6' : '#EF4444'; // blue for 0, red for 1
        }

        function runQuantumComputer() {
            // Show superposition
            qubit.textContent = '?';
            qubit.style.transform = 'scale(1.2) rotate(360deg)';
            qubit.style.background = `radial-gradient(circle, #EF4444, #3B82F6)`;

            // Collapse to a state after a delay
            setTimeout(() => {
                const collapsedState = Math.round(Math.random());
                qubit.textContent = collapsedState;
                qubit.style.transform = 'scale(1)';
                qubit.style.background = collapsedState === 0 ? '#3B82F6' : '#EF4444';
            }, 1000);
        }

        // --- Slide 3: Shor's Algorithm ---
        const padlock = document.getElementById('padlock-icon');
        const hndlText = document.getElementById('hndl-text');
        const hndlContainer = document.getElementById('hndl-container');

        function runShor() {
            if (padlock.classList.contains('shattered')) return;
            
            // 1. Shatter the padlock
            padlock.classList.add('shattered', 'text-red-500');

            // 2. Show HNDL text and animation
            setTimeout(() => {
                hndlText.style.opacity = '1';
                for (let i=0; i<20; i++) {
                    const el = document.createElement('div');
                    el.innerHTML = '&#128190;'; // Floppy disk emoji
                    el.className = 'hndl-item absolute text-2xl';
                    el.style.left = `${Math.random() * 100}%`;
                    el.style.animationDelay = `${Math.random() * 5}s`;
                    hndlContainer.appendChild(el);
                }
            }, 500);
        }
        
        // --- Slide 4: PQC Shield ---
        const shieldContainer = document.getElementById('shield-effect-container');
        function runAttack(type) {
            // Add shield visual
            const shield = document.createElement('div');
            shield.className = 'shield-effect absolute w-48 h-48 border-4 rounded-full';
            shield.style.borderColor = type === 'quantum' ? '#22D3EE' : '#3B82F6';
            shieldContainer.innerHTML = '';
            shieldContainer.appendChild(shield);

            // Remove after animation
            setTimeout(() => shield.remove(), 500);
        }

        // --- Slide 5: Mosca's Theorem ---
        const xSlider = document.getElementById('x-slider');
        const ySlider = document.getElementById('y-slider');
        const zSlider = document.getElementById('z-slider');
        
        function updateMoscaTheorem() {
            const x = parseInt(xSlider.value);
            const y = parseInt(ySlider.value);
            const z = parseInt(zSlider.value);
            
            document.getElementById('x-val').textContent = `${x} years`;
            document.getElementById('y-val').textContent = `${y} years`;
            document.getElementById('z-val').textContent = `${z} years`;

            const totalTime = Math.max(xSlider.max, ySlider.max, zSlider.max, x+y, z);

            const xyWidth = ((x + y) / totalTime) * 100;
            const zPos = (z / totalTime) * 100;

            document.getElementById('xy-bar').style.width = `${xyWidth}%`;
            document.getElementById('z-marker').style.left = `${zPos}%`;

            const riskStatus = document.getElementById('risk-status');
            if (x + y > z) {
                riskStatus.textContent = "YOU ARE AT RISK";
                riskStatus.className = "mt-4 text-2xl font-bold p-4 rounded-lg bg-red-500/20 text-red-400";
            } else {
                riskStatus.textContent = "YOU ARE SAFE (FOR NOW)";
                riskStatus.className = "mt-4 text-2xl font-bold p-4 rounded-lg bg-green-500/20 text-green-400";
            }
        }
        
        [xSlider, ySlider, zSlider].forEach(slider => slider.addEventListener('input', updateMoscaTheorem));
        
        
        // --- Initial Setup ---
        window.onload = () => {
            resizeCanvas();
            initParticles();
            animateCanvas();
            showSlide(0);
            updateMoscaTheorem();
        };

        window.onresize = () => {
            resizeCanvas();
            initParticles();
        };
    </script>
</body>
</html>
