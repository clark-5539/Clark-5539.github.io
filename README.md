# Clark-5539.github.io
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diseñador de Armamento RPG</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=MedievalSharp&family=Poppins:wght@400;600&display=swap');
        
        :root {
            --primary: #6d28d9;
            --secondary: #f59e0b;
            --dark: #1e293b;
            --light: #f8fafc;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #0f172a;
            color: var(--light);
            min-height: 100vh;
        }
        
        .medieval {
            font-family: 'MedievalSharp', cursive;
        }
        
        .weapon-card {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #1e293b, #334155);
            border: 1px solid #475569;
        }
        
        .weapon-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
        }
        
        .stat-bar {
            height: 8px;
            border-radius: 4px;
            background: #334155;
        }
        
        .stat-progress {
            height: 100%;
            border-radius: 4px;
            background: linear-gradient(90deg, var(--primary), #8b5cf6);
        }
        
        .tab-active {
            border-bottom: 3px solid var(--secondary);
            color: var(--secondary);
        }
        
        .texture-preview {
            width: 100%;
            aspect-ratio: 1;
            background-size: cover;
            background-position: center;
            border: 2px solid #475569;
            transition: all 0.2s ease;
        }
        
        .texture-preview:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(245, 158, 11, 0.5);
        }
        
        #model-viewer {
            background: radial-gradient(circle, #1e293b 0%, #0f172a 100%);
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid var(--secondary);
            position: relative;
            overflow: hidden;
        }
        
        .upgrade-btn {
            background: linear-gradient(135deg, var(--primary), #7c3aed);
            transition: all 0.2s ease;
        }
        
        .upgrade-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(109, 40, 217, 0.4);
        }
        
        .section-title {
            position: relative;
            display: inline-block;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -8px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), transparent);
        }
        
        .floating-btn {
            animation: float 3s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
    </style>
</head>
<body class="pb-20">
    <!-- Header -->
    <header class="bg-slate-900 py-4 px-6 shadow-lg sticky top-0 z-10">
        <div class="flex justify-between items-center">
            <h1 class="text-2xl medieval font-bold text-purple-400">Arsenal Mágico</h1>
            <button id="save-btn" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg transition">
                Guardar
            </button>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4">
        <!-- Navigation Tabs -->
        <div class="flex border-b border-slate-700 mt-6 mb-8">
            <button class="tab-btn px-6 py-3 font-medium tab-active" data-tab="weapons">Armas</button>
            <button class="tab-btn px-6 py-3 font-medium" data-tab="armors">Armaduras</button>
            <button class="tab-btn px-6 py-3 font-medium" data-tab="textures">Texturas</button>
            <button class="tab-btn px-6 py-3 font-medium" data-tab="my-creations">Mis Creaciones</button>
        </div>

        <!-- Weapons Section -->
        <section id="weapons" class="tab-content py-4 active">
            <h2 class="text-xl medieval font-bold mb-6 section-title">Diseña tu Arma</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Weapon Type Selection -->
                <div class="weapon-card p-6 rounded-xl">
                    <h3 class="text-lg font-semibold mb-4">Tipo de Arma</h3>
                    <div class="grid grid-cols-2 gap-3">
                        <button class="weapon-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="magic">
                            Magia
                        </button>
                        <button class="weapon-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="range">
                            Distancia
                        </button>
                        <button class="weapon-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="melee">
                            Cuerpo a Cuerpo
                        </button>
                        <button class="weapon-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="mid-range">
                            Media Distancia
                        </button>
                    </div>
                    
                    <!-- Model Preview -->
                    <div id="model-viewer" class="mt-6 rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/221e27cb-713b-4b8c-ac0f-93f03ab94193.png" alt="Vista previa 3D de un arma de rol genérica - funda de espada flotando con efectos de partículas mágicas" class="w-full h-full object-contain" />
                    </div>
                </div>
                
                <!-- Weapon Stats -->
                <div class="weapon-card p-6 rounded-xl">
                    <h3 class="text-lg font-semibold mb-4">Estadísticas</h3>
                    
                    <div class="mb-4">
                        <label class="block mb-2">Nombre del Arma</label>
                        <input type="text" id="weapon-name" class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                    </div>
                    
                    <div class="space-y-4">
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Daño</span>
                                <span id="damage-value" class="font-medium">25</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 50%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Velocidad</span>
                                <span id="speed-value" class="font-medium">60</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 60%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Alcance</span>
                                <span id="range-value" class="font-medium">30</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 30%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Crítico</span>
                                <span id="crit-value" class="font-medium">15%</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 15%"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-8">
                        <h4 class="font-medium mb-2">Habilidades Especiales</h4>
                        <select id="special-ability" class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option value="">Seleccionar habilidad</option>
                            <option value="fire">Llamas Ardientes</option>
                            <option value="ice">Congelación</option>
                            <option value="lightning">Impacto Eléctrico</option>
                            <option value="poison">Veneno Corrosivo</option>
                        </select>
                    </div>
                    
                    <button id="create-weapon-btn" class="mt-6 w-full py-3 rounded-lg upgrade-btn text-white font-medium">
                        Crear Arma
                    </button>
                </div>
            </div>
            
            <!-- Weapon Customization -->
            <div class="weapon-card p-6 rounded-xl mt-6">
                <h3 class="text-lg font-semibold mb-4">Personalización</h3>
                
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div>
                        <h4 class="text-sm font-medium mb-2">Material</h4>
                        <select class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option>Hierro</option>
                            <option>Acero</option>
                            <option>Mithril</option>
                            <option>Ébano</option>
                        </select>
                    </div>
                    
                    <div>
                        <h4 class="text-sm font-medium mb-2">Tamaño</h4>
                        <select class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option>Pequeño</option>
                            <option>Mediano</option>
                            <option>Grande</option>
                        </select>
                    </div>
                    
                    <div>
                        <h4 class="text-sm font-medium mb-2">Estilo</h4>
                        <select class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option>Clásico</option>
                            <option>Gótico</option>
                            <option>Élfico</option>
                            <option>Demoníaco</option>
                        </select>
                    </div>
                    
                    <div>
                        <h4 class="text-sm font-medium mb-2">Efectos</h4>
                        <select class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option>Ninguno</option>
                            <option>Resplandor</option>
                            <option>Humo</option>
                            <option>Chispas</option>
                        </select>
                    </div>
                </div>
            </div>
        </section>

        <!-- Armors Section -->
        <section id="armors" class="tab-content py-4 hidden">
            <h2 class="text-xl medieval font-bold mb-6 section-title">Diseña tu Armadura</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Armor Type Selection -->
                <div class="weapon-card p-6 rounded-xl">
                    <h3 class="text-lg font-semibold mb-4">Tipo de Armadura</h3>
                    <div class="grid grid-cols-2 gap-3">
                        <button class="armor-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="light">
                            Ligera
                        </button>
                        <button class="armor-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="medium">
                            Media
                        </button>
                        <button class="armor-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="heavy">
                            Pesada
                        </button>
                        <button class="armor-type-btn py-2 px-4 rounded-lg bg-slate-700 hover:bg-purple-800 transition" data-type="magic">
                            Mágica
                        </button>
                    </div>
                    
                    <!-- Model Preview -->
                    <div id="armor-model-viewer" class="mt-6 rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/711e8ef8-57e4-46d3-b936-d5a68cb3ccf7.png" alt="Vista previa 3D de una armadura de pecho medieval con diseños ornamentales y superficies pulidas" class="w-full h-full object-contain" />
                    </div>
                </div>
                
                <!-- Armor Stats -->
                <div class="weapon-card p-6 rounded-xl">
                    <h3 class="text-lg font-semibold mb-4">Estadísticas</h3>
                    
                    <div class="mb-4">
                        <label class="block mb-2">Nombre de la Armadura</label>
                        <input type="text" id="armor-name" class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                    </div>
                    
                    <div class="space-y-4">
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Defensa</span>
                                <span id="defense-value" class="font-medium">45</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 45%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Resistencia Mágica</span>
                                <span id="magic-resist-value" class="font-medium">30</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 30%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Movilidad</span>
                                <span id="mobility-value" class="font-medium">65</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 65%"></div>
                            </div>
                        </div>
                        
                        <div>
                            <div class="flex justify-between mb-1">
                                <span>Durabilidad</span>
                                <span id="durability-value" class="font-medium">80</span>
                            </div>
                            <div class="stat-bar">
                                <div class="stat-progress" style="width: 80%"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-8">
                        <h4 class="font-medium mb-2">Bonus de Conjunto</h4>
                        <select id="set-bonus" class="w-full p-2 rounded bg-slate-700 border border-slate-600">
                            <option value="">Seleccionar bonus</option>
                            <option value="health">+20% Salud</option>
                            <option value="stamina">+15% Energía</option>
                            <option value="crit">+5% Crítico</option>
                            <option value="speed">+10% Velocidad</option>
                        </select>
                    </div>
                    
                    <button id="create-armor-btn" class="mt-6 w-full py-3 rounded-lg upgrade-btn text-white font-medium">
                        Crear Armadura
                    </button>
                </div>
            </div>
        </section>

        <!-- Textures Section -->
        <section id="textures" class="tab-content py-4 hidden">
            <h2 class="text-xl medieval font-bold mb-6 section-title">Biblioteca de Texturas</h2>
            
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="texture-item">
                    <div class="texture-preview rounded-lg" 
                         onclick="applyTexture('metallic_gold')" 
                         style="background-image: url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/74e7af20-189d-485f-b2f8-3d72c0dd47b7.png')"
                         title="Oro Metálico">
                    </div>
                    <p class="text-center mt-2 text-sm">Oro Metálico</p>
                </div>
                
                <div class="texture-item">
                    <div class="texture-preview rounded-lg" 
                         onclick="applyTexture('obsidian')" 
                         style="background-image: url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/cf248712-d994-4f8d-a726-78ff76f8e430.png')"
                         title="Obsidiana">
                    </div>
                    <p class="text-center mt-2 text-sm">Obsidiana</p>
                </div>
                
                <div class="texture-item">
                    <div class="texture-preview rounded-lg" 
                         onclick="applyTexture('dragon_scale')" 
                         style="background-image: url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ad5954b4-d96f-47ed-834c-181c7cef5b4c.png')"
                         title="Escama de Dragón">
                    </div>
                    <p class="text-center mt-2 text-sm">Escama de Dragón</p>
                </div>
                
                <div class="texture-item">
                    <div class="texture-preview rounded-lg" 
                         onclick="applyTexture('crystal')" 
                         style="background-image: url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/6f9a7e75-26f6-4ffc-a6ca-2016435e6896.png')"
                         title="Cristal">
                    </div>
                    <p class="text-center mt-2 text-sm">Cristal</p>
                </div>
                
                <div class="texture-item">
                    <div class="texture-preview rounded-lg" 
                         onclick="applyTexture('runes')" 
                         style="background-image: url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/7ba4
