<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SOS Miquéias Braga</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background-color: #0f172a; /* Fundo mais escuro/azulado */
            color: #f8fafc;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        /* Oculta views inativas */
        .view { display: none; }
        .view.active { display: block; }

        /* Estilização de inputs para mobile */
        input:not([type="checkbox"]), textarea, select {
            background-color: #1e293b;
            color: white;
            border: 1px solid #334155;
            border-radius: 0.5rem;
            padding: 0.875rem;
            width: 100%;
            font-size: 1rem;
        }
        
        input[type="date"]::-webkit-calendar-picker-indicator,
        input[type="time"]::-webkit-calendar-picker-indicator {
            filter: invert(1);
        }

        .pulse-btn {
            animation: pulse-red 2s infinite;
        }

        @keyframes pulse-red {
            0% { box-shadow: 0 0 0 0 rgba(220, 38, 38, 0.7); }
            70% { box-shadow: 0 0 0 20px rgba(220, 38, 38, 0); }
            100% { box-shadow: 0 0 0 0 rgba(220, 38, 38, 0); }
        }

        /* ESTILOS DE IMPRESSÃO */
        @media print {
            body { background-color: white !important; color: black !important; }
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            
            #print-container {
                padding: 20px;
                font-family: Arial, sans-serif;
            }
            .print-record {
                border-bottom: 1px solid #ccc;
                padding-bottom: 15px;
                margin-bottom: 15px;
                page-break-inside: avoid;
            }
            .print-record h3 { margin: 0 0 10px 0; font-size: 16px; border-bottom: 1px solid #eee; padding-bottom: 5px; }
            .print-record p { margin: 4px 0; font-size: 14px; }
            .print-record strong { font-weight: bold; }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col pb-24">

    <!-- ÁREA DE IMPRESSÃO (Fica oculta na tela, aparece só no papel) -->
    <div id="print-container" class="hidden print-only">
        <h1 style="text-align: center; margin-bottom: 20px; border-bottom: 2px solid #000; padding-bottom: 10px; font-size: 20px;">
            Histórico de Crises - Miquéias Braga Domingos
        </h1>
        <div id="print-content"></div>
    </div>

    <!-- CABEÇALHO -->
    <header class="bg-slate-900 border-b border-slate-800 p-4 sticky top-0 z-50 shadow-md flex justify-between items-center no-print">
        <div>
            <h1 class="text-xl font-black text-red-500 tracking-tight">🚨 SOS MIQUÉIAS</h1>
        </div>
        <button id="btn-sound" onclick="toggleSound()" class="px-4 py-2 bg-slate-800 border border-slate-700 rounded-lg text-sm font-bold text-gray-300">
            🔊 Som: ON
        </button>
    </header>

    <main class="flex-grow max-w-md mx-auto w-full p-4 no-print">

        <!-- ========================================== -->
        <!-- VIEW 1: HOME (INFORMAÇÕES E BOTÃO)         -->
        <!-- ========================================== -->
        <div id="view-home" class="view active space-y-6">
            
            <!-- IDENTIFICAÇÃO -->
            <div class="bg-slate-800 rounded-2xl p-5 border-l-4 border-blue-500 shadow-lg">
                <h2 class="text-xl font-black text-white mb-3">MIQUÉIAS BRAGA DOMINGOS</h2>
                <div class="space-y-2 text-sm font-medium text-slate-300">
                    <p class="flex items-center gap-2"><span>🧩</span> TEA Grau Leve</p>
                    <p class="flex items-center gap-2"><span>⚡</span> Epilepsia</p>
                    <p class="flex items-center gap-2"><span>🔄</span> Crises de ausência e convulsivas</p>
                </div>
            </div>

            <!-- INFORMAÇÕES FIXAS -->
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 shadow-lg">
                <h3 class="font-bold text-yellow-500 mb-3 flex items-center gap-2"><span>💊</span> Medicação e Suplementos</h3>
                <div class="space-y-3 text-sm text-slate-300">
                    <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                        <p class="text-white font-bold">Levetiracetam 500mg</p>
                        <p class="text-xs text-yellow-400">Uso: 21:00</p>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                            <p class="text-xs text-slate-400 mb-1">Manhã</p>
                            <p class="text-white font-semibold text-sm">PEA</p>
                            <p class="text-white font-semibold text-sm">L-Teanina 200mg</p>
                        </div>
                        <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                            <p class="text-xs text-slate-400 mb-1">Noite</p>
                            <p class="text-white font-semibold text-sm">Melatonina 41mg</p>
                        </div>
                    </div>
                </div>

                <!-- ALERTAS FIXOS -->
                <div class="mt-4 bg-red-900/30 border border-red-800 rounded-xl p-4">
                    <h4 class="text-red-400 font-bold mb-2 flex items-center gap-2"><span>⚠️</span> AVISOS IMPORTANTES</h4>
                    <ul class="text-xs text-slate-300 space-y-2 font-medium">
                        <li>🚫 Nunca medicar ou suplementar durante ou após a crise sem autorização do responsável.</li>
                        <li>🚫 Não oferecer líquidos ou alimentos.</li>
                        <li>⏳ Aguardar responsável.</li>
                    </ul>
                </div>
            </div>

            <!-- BOTÃO PRINCIPAL -->
            <button onclick="startPanicMode()" class="w-full bg-red-600 hover:bg-red-700 text-white font-black text-2xl py-10 rounded-2xl shadow-2xl pulse-btn transition-colors flex flex-col items-center justify-center gap-3">
                <span class="text-5xl">👉</span>
                <span class="tracking-wide text-center">INICIAR PROTOCOLO<br>DE CRISE</span>
            </button>

            <!-- BOTÃO DIRETO PARA REGISTRO -->
            <button onclick="openRegistrationForm()" class="w-full bg-slate-700 hover:bg-slate-600 border border-slate-600 text-white font-bold text-lg py-4 rounded-2xl shadow-lg transition-colors flex items-center justify-center gap-2">
                <span>📝</span> Registrar Crise Manualmente
            </button>

            <!-- ESTATÍSTICAS E HISTÓRICO -->
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 mt-6 shadow-lg">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-slate-400 text-sm uppercase tracking-wider">
                        <span>📊 Resumo do Mês</span>
                    </h3>
                    <button onclick="openPrintView()" class="bg-blue-600 hover:bg-blue-700 text-white text-xs font-bold py-2 px-3 rounded flex items-center gap-1 transition-colors">
                        <span>🖨️</span> Imprimir
                    </button>
                </div>

                <div class="grid grid-cols-2 gap-4 mb-5">
                    <div class="bg-slate-900 p-3 rounded-xl border border-slate-700 text-center">
                        <p class="text-xs text-slate-400">Total de Crises</p>
                        <p id="stat-total" class="text-2xl font-black text-yellow-500">0</p>
                    </div>
                    <div class="bg-slate-900 p-3 rounded-xl border border-slate-700 text-center">
                        <p class="text-xs text-slate-400">Última Crise</p>
                        <p id="stat-last" class="text-sm font-bold text-white mt-1">Nenhuma</p>
                    </div>
                </div>
                
                <h3 class="font-bold text-slate-400 mb-3 text-sm uppercase tracking-wider">Últimos Registros</h3>
                <div id="history-list" class="space-y-3">
                    <!-- Preenchido via JS -->
                </div>
            </div>
        </div>

        <!-- ========================================== -->
        <!-- VIEW: SELEÇÃO PARA IMPRESSÃO               -->
        <!-- ========================================== -->
        <div id="view-print" class="view space-y-4">
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 shadow-xl">
                <div class="flex justify-between items-center mb-4 border-b border-slate-700 pb-4">
                    <h2 class="text-xl font-black text-white flex items-center gap-2">
                        <span>🖨️</span> Imprimir Histórico
                    </h2>
                    <button onclick="switchView('view-home')" class="text-slate-400 hover:text-white font-bold">Voltar</button>
                </div>

                <div class="mb-4">
                    <label class="flex items-center gap-3 cursor-pointer bg-slate-900 p-3 rounded-xl border border-slate-600">
                        <input type="checkbox" id="cb-select-all" onchange="toggleSelectAll(this)" class="w-6 h-6 accent-blue-500">
                        <span class="font-bold text-white">Selecionar Todos os Registros</span>
                    </label>
                </div>

                <div id="print-selection-list" class="space-y-3 max-h-[50vh] overflow-y-auto pr-2">
                    <!-- Preenchido via JS com checkboxes -->
                </div>

                <div class="mt-6 pt-4 border-t border-slate-700">
                    <button onclick="executePrint()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-black text-lg py-4 rounded-2xl shadow-lg transition-colors flex justify-center gap-2">
                        👉 GERAR RELATÓRIO
                    </button>
                </div>
            </div>
        </div>

        <!-- ========================================== -->
        <!-- VIEW 2: MODO PÂNICO (SIMPLIFICADO)         -->
        <!-- ========================================== -->
        <div id="view-panic" class="view space-y-4">
            
            <div class="bg-red-600 rounded-2xl p-6 text-center shadow-2xl">
                <h2 class="text-3xl font-black text-white uppercase tracking-wider mb-2">Modo Emergência</h2>
                <div class="bg-red-800/50 p-4 rounded-xl mt-4 border border-red-400/30">
                    <p class="font-bold text-yellow-300 text-lg uppercase mb-1">Atenção ao tempo!</p>
                    <p class="text-sm text-white">⚠️ Se a crise passar de 5 minutos, acione socorro médico imediatamente.</p>
                </div>
            </div>

            <!-- INSTRUÇÕES DIRETAS -->
            <div class="bg-slate-800 rounded-2xl p-6 border-2 border-yellow-500 shadow-xl">
                <ul class="space-y-5 text-xl font-bold text-white">
                    <li class="flex items-center gap-4"><span class="text-3xl">🧘</span> Manter calma</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛑</span> Afastar pessoas</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛌</span> Deitar de lado</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛡️</span> Proteger a cabeça</li>
                </ul>
            </div>

            <!-- ALERTAS PROIBITIVOS -->
            <div class="bg-slate-900 rounded-2xl p-6 border-2 border-red-500 shadow-xl space-y-4">
                <div class="flex items-center gap-3 text-red-500 font-black text-xl">
                    <span class="text-3xl">🚫</span> NÃO colocar nada na boca
                </div>
                <div class="flex items-center gap-3 text-red-500 font-black text-xl">
                    <span class="text-3xl">🚫</span> NÃO segurar o corpo
                </div>
                <div class="flex items-center gap-3 text-red-500 font-black text-xl">
                    <span class="text-3xl">🚫</span> NÃO dar líquidos
                </div>
            </div>

            <button onclick="openRegistrationForm()" class="w-full bg-yellow-500 hover:bg-yellow-600 text-slate-900 font-black text-xl py-6 rounded-2xl shadow-xl mt-8 flex justify-center gap-2 transition-colors">
                👉 REGISTRAR CRISE
            </button>
        </div>

        <!-- ========================================== -->
        <!-- VIEW 3: FORMULÁRIO PÓS-CRISE               -->
        <!-- ========================================== -->
        <div id="view-form" class="view space-y-6">

            <!-- ORIENTAÇÕES PÓS-CRISE -->
            <div class="bg-yellow-900/40 border border-yellow-600 rounded-2xl p-5 shadow-lg">
                <h3 class="font-black text-yellow-500 text-lg mb-3 flex items-center gap-2"><span>⚠️</span> ORIENTAÇÃO PÓS-CRISE</h3>
                <ul class="text-sm text-slate-200 space-y-2 font-medium">
                    <li>• Ambiente calmo e evitar estímulos (luz/barulho).</li>
                    <li>• Não oferecer nada via oral.</li>
                    <li>• Aguardar recuperação completa.</li>
                </ul>
                <div class="mt-4 p-3 bg-slate-900 rounded-xl border border-slate-700">
                    <p class="text-sm font-bold text-blue-400">💡 OBSERVAÇÃO:</p>
                    <p class="text-xs text-slate-300 mt-1">Em caso de febre ou dor, agir apenas conforme orientação do responsável.</p>
                </div>
            </div>

            <form id="crisis-form" onsubmit="saveAndSend(event)" class="space-y-6 bg-slate-800 p-5 rounded-2xl border border-slate-700 shadow-xl">
                <h2 class="text-2xl font-black text-white mb-4 border-b border-slate-700 pb-3">📝 Registro da Crise</h2>

                <!-- DATA E HORA -->
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Data</label>
                        <input type="date" id="f-date" required>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Hora</label>
                        <input type="time" id="f-time" required>
                    </div>
                </div>

                <!-- TEMPO MANUAL -->
                <div class="bg-slate-900 p-4 rounded-xl border border-slate-700">
                    <label class="block text-xs font-bold text-yellow-500 uppercase mb-3">⏱️ Tempo da crise (Duração)</label>
                    <div class="flex gap-4 items-center">
                        <div class="flex-1 flex items-center gap-2">
                            <input type="number" id="f-min" min="0" placeholder="0" class="text-center font-bold text-xl" required>
                            <span class="text-slate-400 font-bold">min</span>
                        </div>
                        <div class="flex-1 flex items-center gap-2">
                            <input type="number" id="f-sec" min="0" max="59" placeholder="0" class="text-center font-bold text-xl" required>
                            <span class="text-slate-400 font-bold">seg</span>
                        </div>
                    </div>
                </div>

                <!-- TIPO -->
                <div>
                    <label class="block text-xs font-bold text-slate-400 uppercase mb-2">Tipo de Crise</label>
                    <div class="grid grid-cols-2 gap-3">
                        <label class="flex items-center justify-center gap-2 cursor-pointer bg-slate-700 hover:bg-slate-600 p-4 rounded-xl border border-slate-600 transition-colors">
                            <input type="radio" name="f-type" value="Ausência" class="w-5 h-5 accent-blue-500" required>
                            <span class="font-bold text-sm">Ausência</span>
                        </label>
                        <label class="flex items-center justify-center gap-2 cursor-pointer bg-slate-700 hover:bg-slate-600 p-4 rounded-xl border border-slate-600 transition-colors">
                            <input type="radio" name="f-type" value="Convulsiva" class="w-5 h-5 accent-red-500">
                            <span class="font-bold text-sm">Convulsiva</span>
                        </label>
                    </div>
                </div>

                <!-- DETALHES ANTES -->
                <div class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">O que estava fazendo antes?</label>
                        <input type="text" id="f-before" placeholder="Ex: Assistindo TV, Brincando..." required>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Febre?</label>
                            <select id="f-fever" required class="font-bold">
                                <option value="" disabled selected>Selecione</option>
                                <option value="Não">Não</option>
                                <option value="Sim">Sim</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Possível Infecção?</label>
                            <input type="text" id="f-infection" placeholder="Ex: Garganta, gripe">
                        </div>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Alimentação antes</label>
                        <input type="text" id="f-food" placeholder="O que comeu nas últimas horas?">
                    </div>
                </div>

                <!-- SINAIS VITAIS -->
                <div class="bg-slate-900 p-4 rounded-xl border border-slate-700 space-y-4">
                    <h3 class="font-black text-green-400 text-sm uppercase tracking-wider">🩺 Sinais Vitais (Pós-Crise)</h3>
                    
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1 flex justify-between">
                            <span>Pressão (PA)</span>
                            <span class="text-slate-500">Normal: 90x60 a 120x80</span>
                        </label>
                        <input type="text" id="f-pa" placeholder="Ex: 110x70">
                    </div>
                    
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-400 uppercase mb-1 flex flex-col">
                                <span>SpO2 (%)</span>
                                <span class="text-slate-500 font-normal mt-0.5">Normal: 95% a 100%</span>
                            </label>
                            <input type="number" id="f-spo2" placeholder="Ex: 98">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-slate-400 uppercase mb-1 flex flex-col">
                                <span>BPM</span>
                                <span class="text-slate-500 font-normal mt-0.5">Normal: 60 a 100</span>
                            </label>
                            <input type="number" id="f-bpm" placeholder="Ex: 80">
                        </div>
                    </div>
                </div>

                <!-- OBSERVAÇÕES -->
                <div>
                    <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Observações Gerais</label>
                    <textarea id="f-notes" rows="3" placeholder="Detalhes adicionais importantes..."></textarea>
                </div>

                <!-- BOTÕES DE AÇÃO -->
                <div class="pt-4 flex flex-col gap-3">
                    <button type="submit" class="w-full bg-green-600 hover:bg-green-700 text-white font-black text-xl py-5 rounded-2xl flex items-center justify-center gap-2 shadow-lg transition-colors">
                        👉 ENVIAR PARA RESPONSÁVEL
                    </button>
                    <button type="button" onclick="cancelRegistration()" class="w-full bg-transparent border-2 border-slate-600 text-slate-300 py-4 rounded-2xl font-bold hover:bg-slate-800 transition-colors">
                        Cancelar Registro
                    </button>
                </div>
            </form>
        </div>

    </main>

    <!-- CAIXA DE MENSAGEM (Substitui o alert padrão) -->
    <div id="custom-modal" class="hidden fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 no-print">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl p-6 w-full max-w-sm shadow-2xl text-center">
            <div class="text-4xl mb-4">⚠️</div>
            <h3 id="modal-title" class="text-xl font-bold text-white mb-2">Aviso</h3>
            <p id="modal-text" class="text-slate-300 mb-6"></p>
            <button onclick="closeModal()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition-colors">OK, entendi</button>
        </div>
    </div>
    
    <!-- MODAL DE CONFIRMAÇÃO (Para Cancelar) -->
    <div id="confirm-modal" class="hidden fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 no-print">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl p-6 w-full max-w-sm shadow-2xl text-center">
            <div class="text-4xl mb-4">❓</div>
            <h3 class="text-xl font-bold text-white mb-2">Atenção</h3>
            <p class="text-slate-300 mb-6">Deseja cancelar este registro? Nada será salvo.</p>
            <div class="flex gap-3">
                <button onclick="closeConfirmModal(false)" class="flex-1 bg-slate-600 hover:bg-slate-500 text-white font-bold py-3 rounded-xl transition-colors">Não</button>
                <button onclick="closeConfirmModal(true)" class="flex-1 bg-red-600 hover:bg-red-700 text-white font-bold py-3 rounded-xl transition-colors">Sim, cancelar</button>
            </div>
        </div>
    </div>

    <script>
        // ESTADOS GERAIS
        let isSilent = false;
        let audioCtx = null;
        const RESPONSAVEL_PHONE = "5584987813129";
        
        // INICIALIZAÇÃO
        document.addEventListener("DOMContentLoaded", () => {
            loadHistoryAndStats();
        });

        // ==========================
        // SISTEMA DE INTERFACE E MODAL
        // ==========================
        function switchView(viewId) {
            document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');
            window.scrollTo(0, 0);
        }

        function showMessage(title, text) {
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-text').innerText = text;
            document.getElementById('custom-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('custom-modal').classList.add('hidden');
        }

        function cancelRegistration() {
            document.getElementById('confirm-modal').classList.remove('hidden');
        }

        function closeConfirmModal(confirm) {
            document.getElementById('confirm-modal').classList.add('hidden');
            if (confirm) {
                switchView('view-home');
            }
        }

        // ==========================
        // SISTEMA DE ÁUDIO E VIBRAÇÃO
        // ==========================
        function toggleSound() {
            isSilent = !isSilent;
            const btn = document.getElementById('btn-sound');
            if(isSilent) {
                btn.innerText = "🔇 Som: OFF";
                btn.classList.replace('text-gray-300', 'text-red-400');
            } else {
                btn.innerText = "🔊 Som: ON";
                btn.classList.replace('text-red-400', 'text-gray-300');
            }
        }

        function playBeep() {
            if (isSilent) return;
            try {
                if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                if (audioCtx.state === 'suspended') audioCtx.resume();

                const oscillator = audioCtx.createOscillator();
                const gainNode = audioCtx.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioCtx.destination);
                
                oscillator.type = 'square';
                oscillator.frequency.setValueAtTime(800, audioCtx.currentTime);
                oscillator.frequency.exponentialRampToValueAtTime(1000, audioCtx.currentTime + 0.2);
                gainNode.gain.setValueAtTime(0.2, audioCtx.currentTime);
                
                oscillator.start();
                oscillator.stop(audioCtx.currentTime + 0.3);
            } catch (e) { console.log("Áudio bloqueado"); }
        }

        function triggerVibration(pattern) {
            if ("vibrate" in navigator && !isSilent) {
                navigator.vibrate(pattern);
            }
        }

        // ==========================
        // MODO PÂNICO E FORMULÁRIO
        // ==========================
        function startPanicMode() {
            if (!audioCtx && !isSilent) {
                try { audioCtx = new (window.AudioContext || window.webkitAudioContext)(); } catch(e){}
            }

            switchView('view-panic');
            triggerVibration([300, 100, 300, 100, 600]); 
            playBeep();
        }

        function openRegistrationForm() {
            triggerVibration(100);
            
            const now = new Date();
            const localDate = now.getFullYear() + '-' + String(now.getMonth() + 1).padStart(2, '0') + '-' + String(now.getDate()).padStart(2, '0');
            const localTime = String(now.getHours()).padStart(2, '0') + ':' + String(now.getMinutes()).padStart(2, '0');
            
            document.getElementById('f-date').value = localDate;
            document.getElementById('f-time').value = localTime;
            
            document.getElementById('f-min').value = '';
            document.getElementById('f-sec').value = '';
            document.getElementById('f-before').value = '';
            document.getElementById('f-fever').value = '';
            document.getElementById('f-infection').value = '';
            document.getElementById('f-food').value = '';
            document.getElementById('f-pa').value = '';
            document.getElementById('f-spo2').value = '';
            document.getElementById('f-bpm').value = '';
            document.getElementById('f-notes').value = '';
            document.querySelectorAll('input[name="f-type"]').forEach(r => r.checked = false);

            switchView('view-form');
        }

        function saveAndSend(e) {
            e.preventDefault();
            
            const min = document.getElementById('f-min').value || 0;
            const sec = document.getElementById('f-sec').value || 0;
            const timeStr = `${min}min ${sec}seg`;

            const data = {
                id: Date.now(),
                date: document.getElementById('f-date').value,
                time: document.getElementById('f-time').value,
                duration: timeStr,
                type: document.querySelector('input[name="f-type"]:checked').value,
                before: document.getElementById('f-before').value,
                fever: document.getElementById('f-fever').value,
                infection: document.getElementById('f-infection').value || 'Não informada',
                food: document.getElementById('f-food').value || 'Não informada',
                pa: document.getElementById('f-pa').value || 'Não aferido',
                spo2: document.getElementById('f-spo2').value || 'Não aferido',
                bpm: document.getElementById('f-bpm').value || 'Não aferido',
                notes: document.getElementById('f-notes').value || 'Nenhuma'
            };

            let history = JSON.parse(localStorage.getItem('crises_miqueias_v2')) || [];
            history.unshift(data); 
            localStorage.setItem('crises_miqueias_v2', JSON.stringify(history));

            loadHistoryAndStats();
            switchView('view-home');

            const dateBR = data.date.split('-').reverse().join('/');
            const msg = `Crise registrada — Miquéias Braga\nData: ${dateBR}\nHora: ${data.time}\nTempo: ${data.duration}\nTipo: ${data.type}\nAntes da crise: ${data.before}\nFebre: ${data.fever}\nInfecção: ${data.infection}\nAlimentação: ${data.food}\nSinais vitais:\nPA: ${data.pa}\nSpO2: ${data.spo2}${data.spo2 !== 'Não aferido' ? '%' : ''}\nBPM: ${data.bpm}\nObservações: ${data.notes}`;

            const url = `https://wa.me/${RESPONSAVEL_PHONE}?text=${encodeURIComponent(msg)}`;
            window.open(url, '_blank');
        }

        // ==========================
        // SISTEMA DE IMPRESSÃO
        // ==========================
        function openPrintView() {
            const history = JSON.parse(localStorage.getItem('crises_miqueias_v2')) || [];
            const listContainer = document.getElementById('print-selection-list');
            
            if (history.length === 0) {
                listContainer.innerHTML = '<p class="text-slate-500 text-center py-6">Nenhum registro disponível para impressão.</p>';
            } else {
                listContainer.innerHTML = history.map(item => {
                    const dateBR = item.date.split('-').reverse().join('/');
                    return `
                    <label class="flex items-start gap-4 cursor-pointer bg-slate-700 hover:bg-slate-600 p-4 rounded-xl border border-slate-600 transition-colors">
                        <input type="checkbox" class="print-cb w-6 h-6 mt-1 accent-blue-500" value="${item.id}">
                        <div class="flex-1">
                            <div class="flex justify-between items-start">
                                <p class="font-bold text-white">${dateBR} às ${item.time}</p>
                                <span class="text-xs font-bold text-slate-300 bg-slate-800 px-2 py-1 rounded">${item.duration}</span>
                            </div>
                            <p class="text-sm text-yellow-500 font-bold mt-1">${item.type}</p>
                        </div>
                    </label>`;
                }).join('');
            }

            document.getElementById('cb-select-all').checked = false;
            switchView('view-print');
        }

        function toggleSelectAll(masterCheckbox) {
            const checkboxes = document.querySelectorAll('.print-cb');
            checkboxes.forEach(cb => cb.checked = masterCheckbox.checked);
        }

        function executePrint() {
            const selectedCheckboxes = document.querySelectorAll('.print-cb:checked');
            if (selectedCheckboxes.length === 0) {
                showMessage("Nenhum item selecionado", "Por favor, selecione pelo menos um registro para poder gerar o relatório de impressão.");
                return;
            }

            const selectedIds = Array.from(selectedCheckboxes).map(cb => parseInt(cb.value));
            const history = JSON.parse(localStorage.getItem('crises_miqueias_v2')) || [];
            
            // Filtra os itens selecionados e os prepara em HTML limpo para o papel
            const recordsToPrint = history.filter(item => selectedIds.includes(item.id));
            
            const printHtml = recordsToPrint.map(data => {
                const dateBR = data.date.split('-').reverse().join('/');
                return `
                <div class="print-record">
                    <h3>Registro: ${dateBR} às ${data.time}</h3>
                    <p><strong>Tipo de Crise:</strong> ${data.type}</p>
                    <p><strong>Duração:</strong> ${data.duration}</p>
                    <p><strong>O que estava fazendo:</strong> ${data.before}</p>
                    <p><strong>Apresentou Febre?</strong> ${data.fever}</p>
                    <p><strong>Possível Infecção:</strong> ${data.infection}</p>
                    <p><strong>Alimentação Recente:</strong> ${data.food}</p>
                    <p><strong>Sinais Vitais Pós-Crise:</strong> PA: ${data.pa} | SpO2: ${data.spo2}${data.spo2 !== 'Não aferido' ? '%' : ''} | BPM: ${data.bpm}</p>
                    <p><strong>Observações Extras:</strong> ${data.notes}</p>
                </div>`;
            }).join('');

            // Injeta o conteúdo na div de impressão
            document.getElementById('print-content').innerHTML = printHtml;

            // Chama a caixa de impressão do navegador
            window.print();
        }

        // ==========================
        // HISTÓRICO HOME PAGE
        // ==========================
        function loadHistoryAndStats() {
            const history = JSON.parse(localStorage.getItem('crises_miqueias_v2')) || [];
            
            const now = new Date();
            const currentMonth = String(now.getMonth() + 1).padStart(2, '0');
            const currentYear = String(now.getFullYear());
            
            const monthCrises = history.filter(item => {
                if(!item.date) return false;
                const [y, m, d] = item.date.split('-');
                return m === currentMonth && y === currentYear;
            });

            document.getElementById('stat-total').innerText = monthCrises.length;

            if (history.length > 0) {
                const lastDate = history[0].date.split('-').reverse().join('/');
                document.getElementById('stat-last').innerText = lastDate;
            } else {
                document.getElementById('stat-last').innerText = "Nenhuma";
            }

            const listContainer = document.getElementById('history-list');
            if (history.length === 0) {
                listContainer.innerHTML = '<p class="text-slate-500 text-sm text-center py-4">Nenhum registro encontrado.</p>';
                return;
            }

            listContainer.innerHTML = history.slice(0, 5).map(item => {
                const dateBR = item.date.split('-').reverse().join('/');
                return `
                <div class="bg-slate-900 p-4 rounded-xl border-l-4 border-slate-600 shadow-sm flex flex-col gap-1">
                    <div class="flex justify-between items-start">
                        <p class="font-bold text-white text-sm">${dateBR} às ${item.time}</p>
                        <span class="text-xs font-bold text-slate-400 bg-slate-800 px-2 py-1 rounded">${item.duration}</span>
                    </div>
                    <p class="text-sm text-slate-300">Tipo: <span class="font-bold text-yellow-500">${item.type}</span></p>
                    <p class="text-xs text-slate-500 truncate">Obs: ${item.notes}</p>
                </div>`;
            }).join('');
        }
    </script>
</body>
</html>
