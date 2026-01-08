# This is the Layout of the Software 

> This should be taken as insipration of the main user interface that will be implemented  

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Windows 11 Audio Suite</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

        :root {
            --win-red: #E81123;
            --win-bg: rgba(26, 26, 26, 0.9);
            --glass-stroke: rgba(255, 255, 255, 0.08);
        }

        body {
            background-color: #050505;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            font-family: "Segoe UI Variable Text", "Segoe UI", "Inter", sans-serif;
            color: white;
            user-select: none;
        }

        /* The Main Glass Container */
        .glass-container {
            background: var(--win-bg);
            backdrop-filter: blur(25px) saturate(150%);
            border: 1px solid var(--glass-stroke);
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.15), 0 10px 30px rgba(0,0,0,0.5);
            transition: all 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
        }

        /* Windows 11 Rect-Circle Action Button */
        .action-rect {
            width: 38px;
            height: 38px;
            background: var(--win-red);
            border-radius: 10px; 
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 15px rgba(232, 17, 35, 0.4);
            cursor: pointer;
        }

        /* State: Recording */
        .is-recording .action-rect {
            border-radius: 50%;
            transform: rotate(90deg);
            background: #ff2e3d;
        }

        /* Magic Open Source Loading Spinner */
        .magic-loader {
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-left-color: white;
            border-radius: 50%;
            animation: magic-spin 0.8s cubic-bezier(0.4, 0, 0.2, 1) infinite;
        }

        @keyframes magic-spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* Tooltip Logic */
        [data-title] { position: relative; }
        [data-title]:hover::after {
            content: attr(data-title);
            position: absolute;
            bottom: -38px;
            left: 50%;
            transform: translateX(-50%);
            background: #2b2b2b;
            color: #d1d1d1;
            font-size: 11px;
            padding: 5px 10px;
            border-radius: 6px;
            border: 1px solid rgba(255,255,255,0.1);
            white-space: nowrap;
            z-index: 100;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            pointer-events: none;
        }

        /* Morphing Transitions */
        .state-layer { transition: all 0.4s ease; }
        .hidden-ui {
            opacity: 0;
            transform: scale(0.9) translateY(10px);
            pointer-events: none;
            position: absolute;
        }
        .visible-ui {
            opacity: 1;
            transform: scale(1) translateY(0);
            position: relative;
        }

        /* Small Win11 Button Style */
        .win-tool-btn {
            @apply p-2 rounded-lg transition-all duration-200;
        }
        .win-tool-btn:hover { background: rgba(255, 255, 255, 0.08); color: white; }
        .win-tool-btn:active { transform: scale(0.9); }
    </style>
</head>
<body>

    <div class="relative">
        
        <div id="recorder-ui" class="glass-container visible-ui flex items-center h-[56px] px-3 rounded-[16px] gap-3 min-w-[340px]">
            
            <div class="flex items-center gap-3 pr-2">
                <div id="main-action-trigger" class="action-rect" data-title="Start Recording">
                    <i id="main-icon" data-lucide="mic" class="w-4 h-4 text-white"></i>
                </div>
                
                <div class="flex flex-col justify-center">
                    <div class="flex items-center gap-2 leading-none">
                        <span id="timer-display" class="text-lg font-semibold tabular-nums">00:00</span>
                        <div id="live-dot" class="w-1.5 h-1.5 bg-red-500 rounded-full hidden animate-pulse"></div>
                    </div>
                </div>
            </div>

            <div class="flex items-center gap-1 ml-auto">
                
                <button id="pause-btn" class="win-tool-btn text-white/40 opacity-30 cursor-not-allowed" data-title="Pause">
                    <i id="pause-icon" data-lucide="pause" class="w-4 h-4"></i>
                </button>

                <div class="w-[1px] h-5 bg-white/10 mx-1"></div>

                <button id="copy-btn" class="win-tool-btn text-white/60" data-title="Copy Transcript">
                    <i id="copy-icon" data-lucide="copy" class="w-4 h-4"></i>
                </button>

                <div class="w-[1px] h-5 bg-white/10 mx-1"></div>

                <button id="api-btn" class="win-tool-btn text-white/40" data-title="API Settings">
                    <i data-lucide="key" class="w-4 h-4"></i>
                </button>

                <button id="delete-btn" class="win-tool-btn text-white/30 hover:text-red-400" data-title="Delete">
                    <i data-lucide="trash-2" class="w-4 h-4"></i>
                </button>
            </div>
        </div>

        <div id="api-ui" class="glass-container hidden-ui flex items-center h-[56px] px-3 rounded-[16px] gap-3 min-w-[340px]">
            <div class="p-2 text-white/20">
                <i data-lucide="fingerprint" class="w-5 h-5"></i>
            </div>
            
            <input type="password" id="api-input" placeholder="Paste API Key..." 
                   class="bg-transparent flex-1 text-sm text-white border-none outline-none placeholder:text-white/10">
            
            <div class="flex items-center gap-1">
                <button id="save-api" class="win-tool-btn text-white/60 hover:text-green-400" data-title="Save Key">
                    <i data-lucide="arrow-right" class="w-4 h-4"></i>
                </button>
                <button id="close-api" class="win-tool-btn text-white/20 hover:text-white">
                    <i data-lucide="x" class="w-4 h-4"></i>
                </button>
            </div>
        </div>

    </div>

    <script>
        // State management
        let mode = 'idle'; 
        let timerSeconds = 0;
        let timerInterval = null;
        let lastTranscript = "Sample transcribed text from Windows 11 Audio Suite."; // Placeholder for real output

        // Elements
        const recorderUI = document.getElementById('recorder-ui');
        const apiUI = document.getElementById('api-ui');
        const mainAction = document.getElementById('main-action-trigger');
        const mainIcon = document.getElementById('main-icon');
        const timerDisplay = document.getElementById('timer-display');
        const liveDot = document.getElementById('live-dot');
        const pauseBtn = document.getElementById('pause-btn');
        const copyBtn = document.getElementById('copy-btn');
        const copyIcon = document.getElementById('copy-icon');

        // Initialize Icons
        lucide.createIcons();

        // Start/Stop Logic
        mainAction.onclick = () => {
            if (mode === 'idle') {
                startRecording();
            } else if (mode === 'recording') {
                startTranscribing();
            }
        };

        function startRecording() {
            mode = 'recording';
            recorderUI.classList.add('is-recording');
            liveDot.classList.remove('hidden');
            pauseBtn.classList.remove('opacity-30', 'cursor-not-allowed');
            pauseBtn.classList.add('text-white/70');
            mainAction.setAttribute('data-title', 'Transcribe');
            
            timerInterval = setInterval(() => {
                timerSeconds++;
                let m = Math.floor(timerSeconds / 60).toString().padStart(2, '0');
                let s = (timerSeconds % 60).toString().padStart(2, '0');
                timerDisplay.textContent = `${m}:${s}`;
            }, 1000);
        }

        function startTranscribing() {
            mode = 'transcribing';
            clearInterval(timerInterval);
            
            // UI Morph to "Magic Loader"
            mainAction.innerHTML = '<div class="magic-loader"></div>';
            mainAction.style.background = 'transparent';
            mainAction.style.boxShadow = 'none';
            mainAction.setAttribute('data-title', 'Magic is happening...');
            
            // Simulate API logic
            setTimeout(() => {
                resetUI();
            }, 3000);
        }

        function resetUI() {
            mode = 'idle';
            timerSeconds = 0;
            clearInterval(timerInterval);
            timerDisplay.textContent = '00:00';
            recorderUI.classList.remove('is-recording');
            liveDot.classList.add('hidden');
            pauseBtn.classList.add('opacity-30', 'cursor-not-allowed');
            
            mainAction.innerHTML = '<i id="main-icon" data-lucide="mic" class="w-4 h-4 text-white"></i>';
            mainAction.style.background = 'var(--win-red)';
            mainAction.style.boxShadow = '0 0 15px rgba(232, 17, 35, 0.4)';
            mainAction.setAttribute('data-title', 'Start Recording');
            lucide.createIcons();
        }

        // Copy to Clipboard Logic
        copyBtn.onclick = async () => {
            try {
                await navigator.clipboard.writeText(lastTranscript);
                
                // Visual Feedback: Success
                copyBtn.classList.add('text-green-400');
                copyBtn.innerHTML = '<i data-lucide="check" class="w-4 h-4"></i>';
                lucide.createIcons();

                setTimeout(() => {
                    copyBtn.classList.remove('text-green-400');
                    copyBtn.innerHTML = '<i data-lucide="copy" class="w-4 h-4"></i>';
                    lucide.createIcons();
                }, 2000);
            } catch (err) {
                console.error('Failed to copy text: ', err);
            }
        };

        // Toggle API Key View
        document.getElementById('api-btn').onclick = () => {
            recorderUI.classList.replace('visible-ui', 'hidden-ui');
            apiUI.classList.replace('hidden-ui', 'visible-ui');
            setTimeout(() => document.getElementById('api-input').focus(), 300);
        };

        document.getElementById('close-api').onclick = () => {
            apiUI.classList.replace('visible-ui', 'hidden-ui');
            recorderUI.classList.replace('hidden-ui', 'visible-ui');
        };

        document.getElementById('save-api').onclick = function() {
            this.innerHTML = '<i data-lucide="check" class="w-4 h-4 text-green-500"></i>';
            lucide.createIcons();
            setTimeout(() => {
                document.getElementById('close-api').click();
                this.innerHTML = '<i data-lucide="arrow-right" class="w-4 h-4"></i>';
                lucide.createIcons();
            }, 800);
        };

        document.getElementById('delete-btn').onclick = resetUI;
    </script>
</body>
</html>

```

