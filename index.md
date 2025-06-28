<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cracklab Tuner - Diseño Premium</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/pitchy@4.1.0/dist/pitchy.min.js"></script>
    <style>
        :root {
            --primary: #3b82f6;
            --secondary: #10b981;
            --accent: #f59e0b;
            --dark: #1e293b;
            --darker: #0f172a;
            --light: #f1f5f9;
            
            --guitar-e2: linear-gradient(145deg, #ef4444, #dc2626);
            --guitar-a2: linear-gradient(145deg, #f97316, #ea580c);
            --guitar-d3: linear-gradient(145deg, #eab308, #ca8a04);
            --guitar-g3: linear-gradient(145deg, #22c55e, #16a34a);
            --guitar-b3: linear-gradient(145deg, #3b82f6, #2563eb);
            --guitar-e4: linear-gradient(145deg, #8b5cf6, #7c3aed);
            
            --bass-e1: linear-gradient(145deg, #ef4444, #b91c1c);
            --bass-a1: linear-gradient(145deg, #f97316, #c2410c);
            --bass-d2: linear-gradient(145deg, #eab308, #a16207);
            --bass-g2: linear-gradient(145deg, #22c55e, #15803d);
        }
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #0b1120, #0f172a);
            color: var(--light);
            overflow-x: hidden;
            min-height: 100vh;
        }
        .tuner-container {
            background: rgba(21, 30, 46, 0.9);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(71, 85, 105, 0.3);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
            max-width: 1200px;
            margin: 0 auto;
            border-radius: 24px;
            overflow: hidden;
        }
        
        /* --- Botones Mejorados --- */
        .instrument-btn {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #1e293b, #0f172a);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 14px;
            padding: 14px;
            text-align: center;
            font-weight: 600;
            position: relative;
            overflow: hidden;
            border: none;
            color: #e2e8f0;
            font-size: 15px;
        }
        .instrument-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(145deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
            border-radius: 14px;
            pointer-events: none;
        }
        .instrument-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25);
        }
        .instrument-btn.active {
            background: linear-gradient(145deg, var(--primary), #2563eb);
            transform: scale(1.05);
            box-shadow: 0 0 25px rgba(59, 130, 246, 0.7);
            color: white;
            z-index: 2;
        }
        
        .wave-btn {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #1e293b, #0f172a);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.15);
            border-radius: 10px;
            padding: 10px;
            text-align: center;
            font-weight: 500;
            position: relative;
            overflow: hidden;
            border: none;
            color: #e2e8f0;
            font-size: 14px;
        }
        .wave-btn.active {
            background: linear-gradient(145deg, var(--primary), #2563eb);
            box-shadow: 0 0 15px rgba(59, 130, 246, 0.6);
            color: white;
        }
        
        .control-btn {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #2563eb, #1d4ed8);
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.2);
            border-radius: 18px;
            padding: 18px;
            text-align: center;
            font-weight: 600;
            position: relative;
            overflow: hidden;
            border: none;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            font-size: 18px;
        }
        .control-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 18px rgba(0, 0, 0, 0.25);
        }
        .control-btn.stop {
            background: linear-gradient(145deg, #ef4444, #dc2626);
        }
        .control-btn.mic {
            background: linear-gradient(145deg, #8b5cf6, #7c3aed);
        }
        .control-btn.mic.active {
            background: linear-gradient(145deg, #ec4899, #db2777);
            box-shadow: 0 0 20px rgba(236, 72, 153, 0.5);
        }
        
        .string-btn {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #1e293b, #0f172a);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            border-radius: 14px;
            padding: 18px 10px;
            text-align: center;
            font-weight: 600;
            position: relative;
            overflow: hidden;
            border: none;
            color: white;
            font-size: 18px;
            font-weight: bold;
        }
        .string-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25);
        }
        .string-btn.active {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(245, 158, 11, 0.6);
        }
        
        /* Colores específicos para cuerdas */
        .string-btn[data-note="E"][data-octave="2"] { background: var(--guitar-e2); }
        .string-btn[data-note="A"][data-octave="2"] { background: var(--guitar-a2); }
        .string-btn[data-note="D"][data-octave="3"] { background: var(--guitar-d3); }
        .string-btn[data-note="G"][data-octave="3"] { background: var(--guitar-g3); }
        .string-btn[data-note="B"][data-octave="3"] { background: var(--guitar-b3); }
        .string-btn[data-note="E"][data-octave="4"] { background: var(--guitar-e4); }
        
        .string-btn[data-note="E"][data-octave="1"] { background: var(--bass-e1); }
        .string-btn[data-note="A"][data-octave="1"] { background: var(--bass-a1); }
        .string-btn[data-note="D"][data-octave="2"] { background: var(--bass-d2); }
        .string-btn[data-note="G"][data-octave="2"] { background: var(--bass-g2); }
        
        /* --- Indicadores visuales --- */
        .needle {
            height: 80%; width: 5px; background: linear-gradient(to top, #f59e0b, white);
            transform-origin: bottom center; transition: transform 0.2s ease;
        }
        .tuner-zone {
            background: linear-gradient(90deg, #ef4444 0%, #f59e0b 40%, #22c55e 48%, #22c55e 52%, #f59e0b 60%, #ef4444 100%);
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
        }
        .meter-point {
            transition: left 0.2s ease;
            box-shadow: 0 0 8px white;
        }
        
        /* --- Piano Styles --- */
        .piano-keyboard {
            display: flex;
            position: relative;
            height: 200px;
            background: linear-gradient(to bottom, #1e293b, #0f172a);
            border-radius: 10px;
            padding: 12px;
            box-shadow: inset 0 6px 12px rgba(0, 0, 0, 0.5);
            overflow-x: auto;
        }
        .key {
            border: 1px solid #334155;
            border-radius: 0 0 6px 6px;
            cursor: pointer;
            transition: all 0.1s ease;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            padding-bottom: 10px;
            font-weight: 600;
            font-size: 14px;
            color: #64748b;
            position: relative;
        }
        .key.white {
            width: calc(100% / 14);
            height: 180px;
            background: linear-gradient(to bottom, #f8fafc, #e2e8f0);
            z-index: 1;
            box-shadow: inset 0 -3px 6px rgba(0, 0, 0, 0.15);
        }
        .key.black {
            width: calc(100% / 14 * 0.65);
            height: 110px;
            background: linear-gradient(to bottom, #1e293b, #0f172a);
            position: absolute;
            z-index: 2;
            color: #94a3b8;
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.5);
        }
        .key.white:active, .key.white.pressed {
            background: linear-gradient(to bottom, #fcd34d, #f59e0b);
            color: #1e293b;
        }
        .key.black:active, .key.black.pressed {
            background: linear-gradient(to bottom, #f59e0b, #d97706);
            color: white;
        }
        
        /* Key labels for mobile */
        .key-label {
            position: absolute;
            bottom: 8px;
            font-size: 11px;
            color: #64748b;
            font-weight: bold;
        }
        
        /* Positioning black keys */
        .key.black[data-note="C#"] { left: calc(100% / 14 * 0.7); }
        .key.black[data-note="D#"] { left: calc(100% / 14 * 1.7); }
        .key.black[data-note="F#"] { left: calc(100% / 14 * 3.7); }
        .key.black[data-note="G#"] { left: calc(100% / 14 * 4.7); }
        .key.black[data-note="A#"] { left: calc(100% / 14 * 5.7); }
        /* Positioning black keys for second octave */
        .key.black[data-note="C#"][data-octave="4"] { left: calc(100% / 14 * 7.7); }
        .key.black[data-note="D#"][data-octave="4"] { left: calc(100% / 14 * 8.7); }
        .key.black[data-note="F#"][data-octave="4"] { left: calc(100% / 14 * 10.7); }
        .key.black[data-note="G#"][data-octave="4"] { left: calc(100% / 14 * 11.7); }
        .key.black[data-note="A#"][data-octave="4"] { left: calc(100% / 14 * 12.7); }
        
        /* --- Slider Styles --- */
        input[type="range"] {
            -webkit-appearance: none;
            height: 10px;
            border-radius: 5px;
            background: linear-gradient(90deg, var(--primary) 0%, var(--primary) var(--progress, 75%), #334155 var(--progress, 75%), #334155 100%);
            outline: none;
        }
        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 22px;
            height: 22px;
            border-radius: 50%;
            background: white;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.4);
            cursor: pointer;
            transition: all 0.2s ease;
            border: 2px solid #1e293b;
        }
        input[type="range"]::-webkit-slider-thumb:hover {
            transform: scale(1.25);
            box-shadow: 0 0 0 6px rgba(59, 130, 246, 0.3);
        }
        
        /* --- Tunning Indicator --- */
        .tuner-indicator {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 90px;
            height: 90px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            font-weight: bold;
            transition: all 0.3s ease;
            background: rgba(30, 41, 59, 0.8);
            box-shadow: 0 0 0 5px rgba(255, 255, 255, 0.15);
        }
        .tuner-indicator.in-tune {
            background: rgba(34, 197, 94, 0.3);
            box-shadow: 0 0 0 10px rgba(34, 197, 94, 0.4);
            color: white;
        }
        .tuner-indicator.sharp {
            background: rgba(239, 68, 68, 0.3);
            box-shadow: 0 0 0 10px rgba(239, 68, 68, 0.4);
            color: white;
        }
        
        /* --- Section Styles --- */
        .section-box {
            background: linear-gradient(145deg, #1e293b, #0f172a);
            border-radius: 20px;
            padding: 28px;
            box-shadow: 0 12px 20px -5px rgba(0, 0, 0, 0.3), 0 6px 8px -6px rgba(0, 0, 0, 0.15);
            border: 1px solid rgba(71, 85, 105, 0.2);
        }
        
        .freq-display {
            background: linear-gradient(145deg, #0f172a, #1e293b);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            box-shadow: inset 0 5px 10px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(71, 85, 105, 0.2);
        }
        
        /* --- Custom glow effects --- */
        .glow {
            animation: glowPulse 2s infinite ease-in-out;
        }
        @keyframes glowPulse {
            0% { box-shadow: 0 0 6px rgba(59, 130, 246, 0.7); }
            50% { box-shadow: 0 0 25px rgba(59, 130, 246, 0.9); }
            100% { box-shadow: 0 0 6px rgba(59, 130, 246, 0.7); }
        }
        
        .header-gradient {
            background: linear-gradient(90deg, #3b82f6, #10b981);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        /* Oscilloscope styles */
        .oscilloscope-container {
            background: #0f172a;
            border-radius: 14px;
            height: 140px;
            margin: 25px 0;
            position: relative;
            overflow: hidden;
            box-shadow: inset 0 5px 10px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(71, 85, 105, 0.2);
        }
        .oscilloscope {
            width: 100%;
            height: 100%;
        }
        .oscilloscope-label {
            position: absolute;
            bottom: 12px;
            right: 12px;
            color: #94a3b8;
            font-size: 14px;
            font-weight: 500;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
        }
        
        /* String button active state */
        .string-btn.active-playing {
            animation: stringGlow 1.2s infinite alternate;
        }
        @keyframes stringGlow {
            from { box-shadow: 0 0 6px rgba(245, 158, 11, 0.6); }
            to { box-shadow: 0 0 25px rgba(245, 158, 11, 0.9); }
        }
        
        /* Key active state */
        .key.pressed {
            animation: keyGlow 0.6s;
        }
        @keyframes keyGlow {
            0% { box-shadow: 0 0 6px rgba(245, 158, 11, 0.6); }
            50% { box-shadow: 0 0 20px rgba(245, 158, 11, 0.9); }
            100% { box-shadow: 0 0 6px rgba(245, 158, 11, 0.6); }
        }
        
        /* Keyboard mapping guide */
        .keyboard-guide {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
            margin-top: 20px;
            padding: 15px;
            background: rgba(30, 41, 59, 0.6);
            border-radius: 12px;
            border: 1px solid rgba(71, 85, 105, 0.2);
        }
        .key-guide-item {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 13px;
            color: #94a3b8;
        }
        .key-guide-key {
            background: #334155;
            padding: 4px 10px;
            border-radius: 5px;
            font-weight: bold;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        /* Responsive adjustments */
        @media (max-width: 768px) {
            .tuner-container {
                padding: 15px;
            }
            .section-box {
                padding: 20px;
            }
            .instrument-btn, .string-btn {
                padding: 12px;
                font-size: 14px;
            }
            .control-btn {
                padding: 14px;
                font-size: 16px;
            }
            .piano-keyboard {
                height: 160px;
            }
            .key.white {
                height: 140px;
            }
            .key.black {
                height: 90px;
            }
            .tuner-indicator {
                width: 70px;
                height: 70px;
                font-size: 22px;
            }
            .freq-display {
                padding: 16px;
            }
            #detectedNote {
                font-size: 42px;
            }
            .key-label {
                font-size: 9px;
            }
            .keyboard-guide {
                display: none;
            }
        }
        
        @media (max-width: 480px) {
            .piano-keyboard {
                height: 140px;
            }
            .key.white {
                height: 110px;
            }
            .key.black {
                height: 75px;
            }
            .instrument-btn, .wave-btn {
                font-size: 13px;
                padding: 10px;
            }
            .control-btn {
                padding: 12px;
                font-size: 15px;
            }
            #detectedNote {
                font-size: 36px;
            }
        }
        
        /* Mobile keyboard helper */
        .mobile-key-helper {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(15, 23, 42, 0.95);
            padding: 12px;
            display: flex;
            justify-content: space-around;
            z-index: 100;
            border-top: 1px solid #334155;
            box-shadow: 0 -4px 10px rgba(0, 0, 0, 0.3);
        }
        .mobile-key-helper button {
            background: #334155;
            border: none;
            border-radius: 10px;
            padding: 10px 14px;
            color: white;
            font-size: 14px;
            font-weight: bold;
            box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
            min-width: 50px;
        }
        
        /* Decoración premium */
        .accent-border {
            position: relative;
        }
        .accent-border::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 0 0 10px 10px;
        }
        
        .neon-text {
            text-shadow: 0 0 10px rgba(59, 130, 246, 0.7), 0 0 20px rgba(59, 130, 246, 0.4);
        }
    </style>
</head>
<body class="min-h-screen p-4">
    <div class="tuner-container p-8">
        <div class="text-center mb-10">
            <h1 class="text-5xl md:text-6xl font-bold header-gradient mb-3">
                <i class="fas fa-rocket mr-3"></i>Cracklab Tuner
            </h1>
            <p class="text-gray-400 text-xl">Herramienta de precisión para músicos profesionales</p>
        </div>
        
        <div class="flex flex-col lg:flex-row gap-10">
            <!-- Sección izquierda: Generador de tono -->
            <div class="lg:w-1/2">
                <div class="section-box accent-border">
                    <h2 class="text-2xl md:text-3xl font-bold text-blue-400 mb-8"><i class="fas fa-wave-square mr-3"></i>Generador de Tono</h2>
                    
                    <div class="mb-8">
                        <label class="block text-sm font-medium text-gray-300 mb-4">Modo:</label>
                        <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
                            <button id="guitarBtn" class="instrument-btn">Guitarra</button>
                            <button id="bassBtn" class="instrument-btn">Bajo</button>
                            <button id="pianoBtn" class="instrument-btn">Piano</button>
                            <button id="customBtn" class="instrument-btn">Manual</button>
                        </div>
                    </div>
                    
                    <div class="mb-8">
                        <label class="block text-sm font-medium text-gray-300 mb-4">Referencia A4:</label>
                        <select id="referenceSelect" class="w-full p-3 md:p-4 rounded-xl bg-gray-800 text-white border border-gray-700 focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="440">440 Hz (Estándar)</option>
                            <option value="432">432 Hz (Verdi)</option>
                            <option value="442">442 Hz (Orquestal)</option>
                            <option value="430.54">430.54 Hz (Barroco)</option>
                        </select>
                    </div>
                    
                    <div id="generatorModeContainer" class="mb-8">
                        <div id="stringsContainer" class="hidden grid grid-cols-3 gap-4"></div>
                        <div id="pianoContainer" class="hidden">
                            <div class="keyboard-guide mb-6">
                                <div class="key-guide-item">
                                    <span class="key-guide-key">Z</span> 
                                    <span>C3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">S</span> 
                                    <span>C#3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">X</span> 
                                    <span>D3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">D</span> 
                                    <span>D#3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">C</span> 
                                    <span>E3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">V</span> 
                                    <span>F3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">G</span> 
                                    <span>F#3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">B</span> 
                                    <span>G3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">H</span> 
                                    <span>G#3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">N</span> 
                                    <span>A3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">J</span> 
                                    <span>A#3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">M</span> 
                                    <span>B3</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">Q</span> 
                                    <span>C4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">2</span> 
                                    <span>C#4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">W</span> 
                                    <span>D4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">3</span> 
                                    <span>D#4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">E</span> 
                                    <span>E4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">R</span> 
                                    <span>F4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">5</span> 
                                    <span>F#4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">T</span> 
                                    <span>G4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">6</span> 
                                    <span>G#4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">Y</span> 
                                    <span>A4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">7</span> 
                                    <span>A#4</span>
                                </div>
                                <div class="key-guide-item">
                                    <span class="key-guide-key">U</span> 
                                    <span>B4</span>
                                </div>
                            </div>
                        </div>
                        <div id="customContainer" class="hidden col-span-3 text-center py-10 text-gray-400">
                             <i class="fas fa-sliders-h text-4xl mb-4"></i>
                             <p class="text-lg">Usa los controles para ajustar la frecuencia</p>
                        </div>
                    </div>
                    
                    <div class="oscilloscope-container">
                        <canvas id="oscilloscope" class="oscilloscope"></canvas>
                        <div class="oscilloscope-label">OSCILOSCOPIO</div>
                    </div>
                    
                    <div class="mb-8">
                        <div class="flex items-center justify-between mb-3">
                            <label class="text-sm font-medium text-gray-300">Frecuencia:</label>
                            <input type="number" id="freqInput" min="20" max="2000" step="0.001" class="w-28 bg-gray-900 text-blue-400 font-mono text-right p-3 rounded-xl border border-gray-700">
                        </div>
                        <input id="freqSlider" type="range" min="20" max="2000" value="440" step="0.001" class="w-full">
                    </div>

                    <div class="mb-8">
                        <label class="block text-sm font-medium text-gray-300 mb-3">Tipo de Onda:</label>
                        <div class="grid grid-cols-4 gap-3">
                            <button data-wave="sine" class="wave-btn active">Seno</button>
                            <button data-wave="square" class="wave-btn">Cuadrada</button>
                            <button data-wave="triangle" class="wave-btn">Triangular</button>
                            <button data-wave="sawtooth" class="wave-btn">Sierra</button>
                        </div>
                    </div>
                    
                    <div class="mb-8">
                        <label class="text-sm font-medium text-gray-300 mb-3">Volumen: <span id="volDisplay" class="text-blue-400">75%</span></label>
                        <input id="volSlider" type="range" min="0" max="1" value="0.75" step="0.01" class="w-full">
                    </div>
                    
                    <div class="flex gap-5">
                        <button id="playBtn" class="control-btn flex-1">
                            <i class="fas fa-play"></i> Reproducir
                        </button>
                        <button id="stopBtn" class="control-btn stop flex-1">
                            <i class="fas fa-stop"></i> Detener
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- Sección derecha: Afinador cromático -->
            <div class="lg:w-1/2">
                 <div class="section-box h-full accent-border">
                    <h2 class="text-2xl md:text-3xl font-bold text-yellow-400 mb-8"><i class="fas fa-microphone-alt mr-3"></i>Afinador Cromático</h2>
                    
                    <div class="mb-8 flex flex-col items-center gap-5">
                        <button id="micBtn" class="control-btn mic w-full">
                            <i class="fas fa-microphone mr-3"></i> Activar Micrófono
                        </button>
                    </div>
                    
                    <div class="relative mb-10 h-60 md:h-72 bg-gray-900 rounded-3xl overflow-hidden flex items-center justify-center">
                        <div class="tuner-zone absolute h-5 w-full top-1/2 -translate-y-1/2 opacity-30"></div>
                        <div class="needle absolute top-[10%] left-1/2 -translate-x-1/2" id="needle"><div class="absolute top-0 left-1/2 w-5 h-5 bg-accent rounded-full -translate-x-1/2 -translate-y-1/2"></div></div>
                        <div class="tuner-indicator" id="tunerIndicator"><i class="fas fa-power-off"></i></div>
                    </div>
                    
                    <div class="text-center mb-8">
                        <div class="freq-display inline-block mb-5">
                            <p class="text-sm text-gray-400 mb-2">Nota detectada</p>
                            <p id="detectedNote" class="text-5xl md:text-6xl font-extrabold text-white neon-text">--</p>
                            <p id="detectedFreq" class="text-xl md:text-2xl font-medium text-blue-400">0.00 Hz</p>
                        </div>
                        <p id="centsDisplay" class="text-2xl font-bold text-gray-400">0 Cents</p>
                    </div>
                    
                    <div class="mb-8">
                        <div class="flex items-center justify-between mb-3 text-sm text-gray-300">
                            <span>Grave</span><span id="tuneStatus" class="font-bold">APAGADO</span><span>Agudo</span>
                        </div>
                        <div class="relative h-3 mb-2">
                            <div class="h-2 rounded-full bg-gradient-to-r from-red-500 via-green-500 to-red-500"></div>
                            <div class="meter-point absolute top-[-5px] w-4 h-4 rounded-full bg-white -translate-x-1/2" id="meterPoint" style="left: 50%"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Mobile keyboard helper -->
    <div class="mobile-key-helper md:hidden">
        <button class="mobile-key" data-note="C" data-octave="3">C3</button>
        <button class="mobile-key" data-note="C#" data-octave="3">C#3</button>
        <button class="mobile-key" data-note="D" data-octave="3">D3</button>
        <button class="mobile-key" data-note="D#" data-octave="3">D#3</button>
        <button class="mobile-key" data-note="E" data-octave="3">E3</button>
        <button class="mobile-key" data-note="F" data-octave="3">F3</button>
        <button class="mobile-key" data-note="F#" data-octave="3">F#3</button>
        <button class="mobile-key" data-note="G" data-octave="3">G3</button>
        <button class="mobile-key" data-note="G#" data-octave="3">G#3</button>
        <button class="mobile-key" data-note="A" data-octave="3">A3</button>
        <button class="mobile-key" data-note="A#" data-octave="3">A#3</button>
        <button class="mobile-key" data-note="B" data-octave="3">B3</button>
    </div>

    <script>
    document.addEventListener('DOMContentLoaded', () => {
        // --- GLOBAL VARS & DOM REFS ---
        let audioContext, generatorOscillator, generatorGainNode, isGeneratorPlaying = false, currentWaveform = 'sine';
        let isMicActive = false, micStream, micAnalyser, pitch, pitchUpdateId;
        let analyser, dataArray, canvasCtx, canvas, animationId;
        let activeStringBtn = null, activeKey = null;

        const DOM = {
            guitarBtn: document.getElementById('guitarBtn'), bassBtn: document.getElementById('bassBtn'),
            pianoBtn: document.getElementById('pianoBtn'), customBtn: document.getElementById('customBtn'),
            stringsContainer: document.getElementById('stringsContainer'), pianoContainer: document.getElementById('pianoContainer'),
            customContainer: document.getElementById('customContainer'),
            playBtn: document.getElementById('playBtn'), stopBtn: document.getElementById('stopBtn'),
            freqSlider: document.getElementById('freqSlider'), freqInput: document.getElementById('freqInput'),
            volSlider: document.getElementById('volSlider'), volDisplay: document.getElementById('volDisplay'),
            waveBtns: document.querySelectorAll('.wave-btn'),
            micBtn: document.getElementById('micBtn'), needle: document.getElementById('needle'),
            tunerIndicator: document.getElementById('tunerIndicator'), meterPoint: document.getElementById('meterPoint'),
            detectedNote: document.getElementById('detectedNote'), detectedFreq: document.getElementById('detectedFreq'),
            centsDisplay: document.getElementById('centsDisplay'), tuneStatus: document.getElementById('tuneStatus'),
            referenceSelect: document.getElementById('referenceSelect'),
            oscilloscope: document.getElementById('oscilloscope')
        };

        const instrumentTunings = {
            guitar: [
                { name: 'E2', note: 'E', octave: 2 },
                { name: 'A2', note: 'A', octave: 2 },
                { name: 'D3', note: 'D', octave: 3 },
                { name: 'G3', note: 'G', octave: 3 },
                { name: 'B3', note: 'B', octave: 3 },
                { name: 'E4', note: 'E', octave: 4 }
            ],
            bass: [
                { name: 'E1', note: 'E', octave: 1 },
                { name: 'A1', note: 'A', octave: 1 },
                { name: 'D2', note: 'D', octave: 2 },
                { name: 'G2', note: 'G', octave: 2 }
            ]
        };
        const noteNames = ['C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#', 'A', 'A#', 'B'];
        
        // Keyboard mapping for piano keys - FL Studio style
        const keyMap = {
            // Primera octava (teclas blancas y negras)
            'KeyZ': { note: 'C', octave: 3 },
            'KeyS': { note: 'C#', octave: 3 },
            'KeyX': { note: 'D', octave: 3 },
            'KeyD': { note: 'D#', octave: 3 },
            'KeyC': { note: 'E', octave: 3 },
            'KeyV': { note: 'F', octave: 3 },
            'KeyG': { note: 'F#', octave: 3 },
            'KeyB': { note: 'G', octave: 3 },
            'KeyH': { note: 'G#', octave: 3 },
            'KeyN': { note: 'A', octave: 3 },
            'KeyJ': { note: 'A#', octave: 3 },
            'KeyM': { note: 'B', octave: 3 },
            
            // Segunda octava
            'KeyQ': { note: 'C', octave: 4 },
            'Digit2': { note: 'C#', octave: 4 },
            'KeyW': { note: 'D', octave: 4 },
            'Digit3': { note: 'D#', octave: 4 },
            'KeyE': { note: 'E', octave: 4 },
            'KeyR': { note: 'F', octave: 4 },
            'Digit5': { note: 'F#', octave: 4 },
            'KeyT': { note: 'G', octave: 4 },
            'Digit6': { note: 'G#', octave: 4 },
            'KeyY': { note: 'A', octave: 4 },
            'Digit7': { note: 'A#', octave: 4 },
            'KeyU': { note: 'B', octave: 4 }
        };

        // --- OSCILLOSCOPE FUNCTIONS ---
        function initOscilloscope() {
            canvas = DOM.oscilloscope;
            canvasCtx = canvas.getContext("2d");
            canvas.width = canvas.offsetWidth;
            canvas.height = canvas.offsetHeight;
            
            analyser = audioContext.createAnalyser();
            analyser.fftSize = 2048;
            generatorGainNode.connect(analyser);
            analyser.connect(audioContext.destination);
            
            dataArray = new Uint8Array(analyser.fftSize);
            drawOscilloscope();
        }
        
        function drawOscilloscope() {
            animationId = requestAnimationFrame(drawOscilloscope);
            
            analyser.getByteTimeDomainData(dataArray);
            
            canvasCtx.fillStyle = 'rgb(15, 23, 42)';
            canvasCtx.fillRect(0, 0, canvas.width, canvas.height);
            
            canvasCtx.lineWidth = 3;
            canvasCtx.strokeStyle = 'rgb(59, 130, 246)';
            canvasCtx.beginPath();
            
            const sliceWidth = canvas.width * 1.0 / analyser.fftSize;
            let x = 0;
            
            for(let i = 0; i < analyser.fftSize; i++) {
                const v = dataArray[i] / 128.0;
                const y = v * canvas.height / 2;
                
                if(i === 0) {
                    canvasCtx.moveTo(x, y);
                } else {
                    canvasCtx.lineTo(x, y);
                }
                
                x += sliceWidth;
            }
            
            canvasCtx.lineTo(canvas.width, canvas.height/2);
            canvasCtx.stroke();
            
            // Add glow effect
            canvasCtx.shadowBlur = 15;
            canvasCtx.shadowColor = 'rgba(59, 130, 246, 0.8)';
        }
        
        function stopOscilloscope() {
            if (animationId) {
                cancelAnimationFrame(animationId);
                canvasCtx.clearRect(0, 0, canvas.width, canvas.height);
            }
        }

        // --- TONE GENERATOR LOGIC ---
        function initAudioContext() {
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
                generatorGainNode = audioContext.createGain();
                generatorGainNode.gain.value = DOM.volSlider.value;
                generatorGainNode.connect(audioContext.destination);
            }
            if (audioContext.state === 'suspended') audioContext.resume();
        }
        
        function startGenerator(freq = null) {
            initAudioContext();
            if (isGeneratorPlaying) stopGenerator();
            
            const currentFrequency = freq || parseFloat(DOM.freqInput.value);
            setFrequency(currentFrequency);
            
            generatorOscillator = audioContext.createOscillator();
            generatorOscillator.type = currentWaveform;
            generatorOscillator.frequency.setValueAtTime(currentFrequency, audioContext.currentTime);
            generatorOscillator.connect(generatorGainNode);
            generatorOscillator.start();
            isGeneratorPlaying = true;
            
            initOscilloscope();
            updateGeneratorUI(true);
        }
        
        function stopGenerator() {
            if (isGeneratorPlaying && generatorOscillator) {
                generatorOscillator.stop();
                generatorOscillator.disconnect();
                isGeneratorPlaying = false;
                updateGeneratorUI(false);
                stopOscilloscope();
                
                // Reset active elements
                if (activeStringBtn) {
                    activeStringBtn.classList.remove('active-playing');
                    activeStringBtn = null;
                }
                if (activeKey) {
                    activeKey.classList.remove('pressed');
                    activeKey = null;
                }
            }
        }
        
        function setFrequency(freq) {
            const clampedFreq = Math.max(20, Math.min(2000, freq));
            DOM.freqSlider.value = clampedFreq;
            DOM.freqInput.value = clampedFreq.toFixed(3);
            
            // Actualizar progreso visual del slider
            const progress = (clampedFreq - 20) / (2000 - 20) * 100;
            DOM.freqSlider.style.setProperty('--progress', `${progress}%`);
            
            if (isGeneratorPlaying) {
                generatorOscillator.frequency.setValueAtTime(clampedFreq, audioContext.currentTime);
            }
        }
        
        function setWaveform(wave) {
            currentWaveform = wave;
            DOM.waveBtns.forEach(btn => {
                btn.classList.toggle('active', btn.dataset.wave === wave);
            });
            if (isGeneratorPlaying) generatorOscillator.type = wave;
        }

        function updateGeneratorUI(isPlaying) {
            DOM.playBtn.classList.toggle('glow', isPlaying);
            DOM.playBtn.innerHTML = isPlaying 
                ? '<i class="fas fa-pause mr-2"></i> Pausa' 
                : '<i class="fas fa-play mr-2"></i> Reproducir';
                
            DOM.playBtn.classList.toggle('from-green-500', !isPlaying);
            DOM.playBtn.classList.toggle('to-green-600', !isPlaying);
            DOM.playBtn.classList.toggle('from-yellow-500', isPlaying);
            DOM.playBtn.classList.toggle('to-yellow-600', isPlaying);
        }

        function switchGeneratorMode(mode) {
            [DOM.guitarBtn, DOM.bassBtn, DOM.pianoBtn, DOM.customBtn].forEach(btn => btn.classList.remove('active'));
            document.getElementById(`${mode}Btn`).classList.add('active');
            
            [DOM.stringsContainer, DOM.pianoContainer, DOM.customContainer].forEach(c => c.classList.add('hidden'));
            
            if (mode === 'guitar' || mode === 'bass') {
                DOM.stringsContainer.innerHTML = '';
                instrumentTunings[mode].forEach((string, index) => {
                    const btn = document.createElement('button');
                    const freq = calculateNoteFreq(string.note, string.octave);
                    btn.className = `string-btn`;
                    btn.dataset.note = string.note;
                    btn.dataset.octave = string.octave;
                    btn.innerHTML = `${string.name}<br><span class="text-sm font-normal">${freq.toFixed(2)} Hz</span>`;
                    DOM.stringsContainer.appendChild(btn);
                });
                DOM.stringsContainer.classList.remove('hidden');
            } else if (mode === 'piano') {
                DOM.pianoContainer.classList.remove('hidden');
                createPianoKeyboard();
            } else { // custom
                DOM.customContainer.classList.remove('hidden');
            }
        }
        
        function createPianoKeyboard() {
            DOM.pianoContainer.innerHTML = '<div class="piano-keyboard"></div>';
            const keyboard = DOM.pianoContainer.querySelector('.piano-keyboard');
            const notes = ['C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#', 'A', 'A#', 'B'];
            for (let octave = 3; octave <= 4; octave++) {
                notes.forEach(note => {
                    const key = document.createElement('button');
                    key.dataset.note = note;
                    key.dataset.octave = octave;
                    key.className = `key ${note.includes('#') ? 'black' : 'white'}`;
                    
                    // Add note label for mobile
                    const label = document.createElement('div');
                    label.className = 'key-label';
                    label.textContent = note.includes('#') ? note : `${note}${octave}`;
                    key.appendChild(label);
                    
                    keyboard.appendChild(key);
                });
            }
        }
        
        function calculateNoteFreq(noteName, octave) {
            const referenceA4 = parseFloat(DOM.referenceSelect.value);
            const noteIndex = noteNames.indexOf(noteName);
            const a4Index = noteNames.indexOf('A');
            const semitonesFromA4 = (noteIndex - a4Index) + (octave - 4) * 12;
            return referenceA4 * Math.pow(2, semitonesFromA4 / 12);
        }
        
        function updateStringFrequencies() {
            const strings = DOM.stringsContainer.querySelectorAll('.string-btn');
            strings.forEach(btn => {
                const note = btn.dataset.note;
                const octave = parseInt(btn.dataset.octave);
                const freq = calculateNoteFreq(note, octave);
                btn.innerHTML = `${note}${octave}<br><span class="text-sm font-normal">${freq.toFixed(2)} Hz</span>`;
            });
        }

        // --- CHROMATIC TUNER LOGIC ---
        async function startMic() {
            try {
                initAudioContext();
                micStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
                const source = audioContext.createMediaStreamSource(micStream);
                micAnalyser = audioContext.createAnalyser();
                micAnalyser.fftSize = 4096; // Increased for better low-frequency resolution
                source.connect(micAnalyser);
                pitch = new Pitchy.PitchDetector({ context: audioContext, input: source });
                isMicActive = true;
                DOM.micBtn.innerHTML = '<i class="fas fa-microphone-slash mr-3"></i> Desactivar Micrófono';
                DOM.micBtn.classList.add('active');
                DOM.tuneStatus.textContent = 'Escuchando...';
                DOM.tuneStatus.className = 'font-bold text-yellow-400';
                updatePitch();
            } catch (err) {
                alert('No se pudo acceder al micrófono. Revisa los permisos en tu navegador.');
                resetTunerUI();
            }
        }
        
        function stopMic() {
            if(pitch) pitch.close();
            if (micStream) micStream.getTracks().forEach(track => track.stop());
            isMicActive = false;
            DOM.micBtn.innerHTML = '<i class="fas fa-microphone mr-3"></i> Activar Micrófono';
            DOM.micBtn.classList.remove('active');
            cancelAnimationFrame(pitchUpdateId);
            resetTunerUI();
        }

        function updatePitch() {
            const float32Array = new Float32Array(micAnalyser.fftSize);
            micAnalyser.getFloatTimeDomainData(float32Array);
            const [frequency, clarity] = pitch.findPitch(float32Array, audioContext.sampleRate);
            
            if (clarity > 0.95 && frequency > 30) {
                const noteDetails = getNoteDetails(frequency);
                updateTunerUI(noteDetails);
            }
            pitchUpdateId = requestAnimationFrame(updatePitch);
        }

        function getNoteDetails(frequency) {
            const referenceA4 = parseFloat(DOM.referenceSelect.value);
            const halfStepsFromA4 = 12 * (Math.log(frequency / referenceA4) / Math.log(2));
            const closestNoteIndex = Math.round(halfStepsFromA4);
            const noteIndex = (9 + closestNoteIndex % 12 + 12) % 12;
            const octave = Math.floor(4 + closestNoteIndex / 12);
            
            const targetFreq = referenceA4 * Math.pow(2, closestNoteIndex / 12);
            const cents = 1200 * (Math.log(frequency / targetFreq) / Math.log(2));

            return { name: noteNames[noteIndex], octave, frequency, cents };
        }

        function updateTunerUI(note) {
            const cents = note.cents;
            DOM.detectedNote.textContent = note.name + note.octave;
            DOM.detectedFreq.textContent = `${note.frequency.toFixed(2)} Hz`;
            DOM.centsDisplay.textContent = `${cents.toFixed(1)} Cents`;
            
            const cappedCents = Math.max(-50, Math.min(50, cents));
            DOM.needle.style.transform = `translateX(-50%) rotate(${cappedCents * 0.9}deg)`;
            DOM.meterPoint.style.left = `${50 + cappedCents}%`;

            if (Math.abs(cents) < 2.5) {
                DOM.tunerIndicator.className = 'tuner-indicator in-tune';
                DOM.tunerIndicator.innerHTML = '<i class="fas fa-check"></i>';
                DOM.tuneStatus.textContent = 'AFINADO';
                DOM.tuneStatus.className = 'font-bold text-green-400';
            } else {
                DOM.tunerIndicator.className = 'tuner-indicator sharp';
                DOM.tunerIndicator.innerHTML = cents > 0 ? '<i class="fas fa-arrow-up"></i>' : '<i class="fas fa-arrow-down"></i>';
                DOM.tuneStatus.textContent = cents > 0 ? 'AGUDO' : 'GRAVE';
                DOM.tuneStatus.className = 'font-bold text-yellow-400';
            }
        }
        
        function resetTunerUI() {
            DOM.detectedNote.textContent = '--';
            DOM.detectedFreq.textContent = '0.00 Hz';
            DOM.centsDisplay.textContent = '0 Cents';
            DOM.needle.style.transform = 'translateX(-50%) rotate(0deg)';
            DOM.meterPoint.style.left = '50%';
            DOM.tuneStatus.textContent = 'APAGADO';
            DOM.tuneStatus.className = 'font-bold text-gray-400';
            DOM.tunerIndicator.className = 'tuner-indicator';
            DOM.tunerIndicator.innerHTML = '<i class="fas fa-power-off"></i>';
        }
        
        // --- KEYBOARD SUPPORT ---
        function handleKeyDown(e) {
            // Ignore if not in piano mode
            if (!DOM.pianoBtn.classList.contains('active')) return;
            
            const mapping = keyMap[e.code];
            if (!mapping) return;
            
            e.preventDefault();
            
            // Find corresponding key element
            const key = document.querySelector(`.key[data-note="${mapping.note}"][data-octave="${mapping.octave}"]`);
            if (!key) return;
            
            // If this key is already active, do nothing
            if (key === activeKey) return;
            
            // Stop any currently playing note
            if (activeKey) {
                activeKey.classList.remove('pressed');
            }
            
            // Play the new note
            const freq = calculateNoteFreq(mapping.note, mapping.octave);
            startGenerator(freq);
            key.classList.add('pressed');
            activeKey = key;
        }
        
        function handleKeyUp(e) {
            const mapping = keyMap[e.code];
            if (!mapping) return;
            
            e.preventDefault();
            
            // Find corresponding key element
            const key = document.querySelector(`.key[data-note="${mapping.note}"][data-octave="${mapping.octave}"]`);
            if (!key) return;
            
            // Only stop if this key is currently active
            if (key === activeKey) {
                stopGenerator();
            }
        }
        
        // --- EVENT LISTENERS ---
        DOM.playBtn.addEventListener('click', () => {
            if (isGeneratorPlaying) stopGenerator();
            else startGenerator();
        });
        
        DOM.stopBtn.addEventListener('click', () => stopGenerator());
        
        DOM.freqSlider.addEventListener('input', () => setFrequency(parseFloat(DOM.freqSlider.value)));
        DOM.freqInput.addEventListener('input', () => setFrequency(parseFloat(DOM.freqInput.value)));
        
        DOM.volSlider.addEventListener('input', () => {
            const vol = DOM.volSlider.value;
            const progress = vol * 100;
            DOM.volSlider.style.setProperty('--progress', `${progress}%`);
            if (generatorGainNode) generatorGainNode.gain.setValueAtTime(vol, audioContext.currentTime);
            DOM.volDisplay.textContent = `${Math.round(vol * 100)}%`;
        });
        
        DOM.waveBtns.forEach(btn => btn.addEventListener('click', () => setWaveform(btn.dataset.wave)));
        
        [DOM.guitarBtn, DOM.bassBtn, DOM.pianoBtn, DOM.customBtn].forEach(btn => {
            btn.addEventListener('click', () => switchGeneratorMode(btn.id.replace('Btn', '')));
        });
        
        DOM.stringsContainer.addEventListener('click', e => {
            const btn = e.target.closest('.string-btn');
            if (!btn) return;
            
            // Toggle functionality
            if (activeStringBtn === btn) {
                stopGenerator();
                return;
            }
            
            // Remove active state from previous button
            if (activeStringBtn) {
                activeStringBtn.classList.remove('active-playing');
            }
            
            const note = btn.dataset.note;
            const octave = parseInt(btn.dataset.octave);
            const freq = calculateNoteFreq(note, octave);
            
            startGenerator(freq);
            btn.classList.add('active-playing');
            activeStringBtn = btn;
        });
        
        DOM.pianoContainer.addEventListener('click', e => {
            const key = e.target.closest('.key');
            if (!key) return;
            
            // Toggle functionality
            if (activeKey === key) {
                stopGenerator();
                return;
            }
            
            // Remove active state from previous key
            if (activeKey) {
                activeKey.classList.remove('pressed');
            }
            
            const freq = calculateNoteFreq(key.dataset.note, parseInt(key.dataset.octave));
            startGenerator(freq);
            key.classList.add('pressed');
            activeKey = key;
        });
        
        DOM.micBtn.addEventListener('click', () => isMicActive ? stopMic() : startMic());
        
        DOM.referenceSelect.addEventListener('change', () => {
            updateStringFrequencies();
            if (isGeneratorPlaying) {
                // Recalculate frequency if we're playing a note
                if (activeStringBtn) {
                    const note = activeStringBtn.dataset.note;
                    const octave = parseInt(activeStringBtn.dataset.octave);
                    const freq = calculateNoteFreq(note, octave);
                    setFrequency(freq);
                }
                else if (activeKey) {
                    const freq = calculateNoteFreq(activeKey.dataset.note, parseInt(activeKey.dataset.octave));
                    setFrequency(freq);
                }
            }
        });
        
        // Keyboard event listeners
        document.addEventListener('keydown', handleKeyDown);
        document.addEventListener('keyup', handleKeyUp);
        
        // Mobile keyboard helper
        document.querySelectorAll('.mobile-key').forEach(button => {
            button.addEventListener('touchstart', (e) => {
                e.preventDefault();
                const note = button.dataset.note;
                const octave = parseInt(button.dataset.octave);
                const freq = calculateNoteFreq(note, octave);
                startGenerator(freq);
            });
            
            button.addEventListener('touchend', (e) => {
                e.preventDefault();
                stopGenerator();
            });
        });
        
        // --- INITIALIZATION ---
        function initApp() {
            createPianoKeyboard();
            DOM.guitarBtn.click();
            setFrequency(440);
            resetTunerUI();
            
            // Set initial slider progress
            const freqProgress = (440 - 20) / (2000 - 20) * 100;
            DOM.freqSlider.style.setProperty('--progress', `${freqProgress}%`);
            
            const volProgress = DOM.volSlider.value * 100;
            DOM.volSlider.style.setProperty('--progress', `${volProgress}%`);
        }
        
        initApp();
        
        // Handle window resize for oscilloscope
        window.addEventListener('resize', () => {
            if (canvas) {
                canvas.width = canvas.offsetWidth;
                canvas.height = canvas.offsetHeight;
            }
        });
    });
    </script>
</body>
</html>
