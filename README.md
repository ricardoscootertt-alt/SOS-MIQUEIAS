<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SOS Miquéias Braga</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background-color: #0f172a; 
            color: #f8fafc;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        .view { display: none; }
        .view.active { display: block; }

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

    <!-- ÁREA DE IMPRESSÃO -->
    <div id="print-container" class="hidden print-only">
        <h1 style="text-align: center; margin-bottom: 20px; border-bottom: 2px solid #000; padding-bottom: 10px; font-size: 20px;">
            Histórico de Crises - Miquéias Braga Domingos
        </h1>
        <div id="print-content"></div>
    </div>

    <!-- CABEÇALHO -->
    <header class="bg-slate-900 border-b border-slate-800 p-4 sticky top-0 z-50 shadow-md flex justify-between items-center no-print">
        <div class="flex items-center gap-3">
            <div>
                <h1 class="text-xl font-black text-red-500 tracking-tight">🚨 SOS MIQUÉIAS</h1>
                <p id="cloud-status" class="text-[10px] font-bold text-blue-400">📊 Banco de Dados Local Ativo</p>
            </div>
        </div>
        <div class="flex gap-2">
            <button onclick="window.openSettings()" class="p-2 bg-slate-800 border border-slate-700 rounded-lg text-lg">
                ⚙️
            </button>
            <button id="btn-sound" onclick="window.toggleSound()" class="px-3 py-2 bg-slate-800 border border-slate-700 rounded-lg text-sm font-bold text-gray-300">
                🔊
            </button>
        </div>
    </header>

    <main class="flex-grow max-w-md mx-auto w-full p-4 no-print">

        <!-- ========================================== -->
        <!-- VIEW 1: HOME (INFORMAÇÕES E BOTÃO)         -->
        <!-- ========================================== -->
        <div id="view-home" class="view active space-y-6">
            
            <div class="bg-slate-800 rounded-2xl p-5 border-l-4 border-blue-500 shadow-lg relative">
                <h2 class="text-xl font-black text-white mb-3">MIQUÉIAS BRAGA DOMINGOS</h2>
                <div class="space-y-2 text-sm font-medium text-slate-300">
                    <p class="flex items-center gap-2"><span>🧩</span> TEA Grau Leve</p>
                    <p class="flex items-center gap-2"><span>⚡</span> Epilepsia</p>
                    <p class="flex items-center gap-2"><span>🔄</span> Crises de ausência e convulsivas</p>
                </div>
            </div>

            <!-- PAINEL DE MEDICAÇÃO (Dinâmico) -->
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 shadow-lg">
                <div class="flex justify-between items-center mb-3">
                    <h3 class="font-bold text-yellow-500 flex items-center gap-2"><span>💊</span> Medicação Atual</h3>
                </div>
                
                <div class="space-y-3 text-sm text-slate-300">
                    <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                        <p id="ui-med-principal" class="text-white font-bold whitespace-pre-line">Levetiracetam 500mg (21:00)</p>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                            <p class="text-xs text-slate-400 mb-1">Manhã</p>
                            <p id="ui-med-manha" class="text-white font-semibold text-sm whitespace-pre-line">PEA\nL-Teanina 200mg</p>
                        </div>
                        <div class="bg-slate-900 p-3 rounded-lg border border-slate-700">
                            <p class="text-xs text-slate-400 mb-1">Noite</p>
                            <p id="ui-med-noite" class="text-white font-semibold text-sm whitespace-pre-line">Melatonina 41mg</p>
                        </div>
                    </div>
                </div>

                <div class="mt-4 bg-red-900/30 border border-red-800 rounded-xl p-4">
                    <h4 class="text-red-400 font-bold mb-2 flex items-center gap-2"><span>⚠️</span> AVISOS IMPORTANTES</h4>
                    <ul class="text-xs text-slate-300 space-y-2 font-medium">
                        <li>🚫 Nunca medicar ou suplementar durante ou após a crise sem autorização do responsável.</li>
                        <li>🚫 Não oferecer líquidos ou alimentos.</li>
                        <li>⏳ Aguardar responsável.</li>
                    </ul>
                </div>
            </div>

            <button onclick="window.startPanicMode()" class="w-full bg-red-600 hover:bg-red-700 text-white font-black text-2xl py-10 rounded-2xl shadow-2xl pulse-btn transition-colors flex flex-col items-center justify-center gap-3">
                <span class="text-5xl">👉</span>
                <span class="tracking-wide text-center">INICIAR PROTOCOLO<br>DE CRISE</span>
            </button>

            <button onclick="window.openRegistrationForm()" class="w-full bg-slate-700 hover:bg-slate-600 border border-slate-600 text-white font-bold text-lg py-4 rounded-2xl shadow-lg transition-colors flex items-center justify-center gap-2">
                <span>📝</span> Registar Crise Manualmente
            </button>

            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 mt-6 shadow-lg">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-slate-400 text-sm uppercase tracking-wider">
                        <span>📊 Resumo do Mês</span>
                    </h3>
                    <div class="flex gap-2">
                        <button onclick="window.syncGoogleSheets()" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold py-2 px-3 rounded flex items-center gap-1">
                            <span>🔄</span> Sync
                        </button>
                        <button onclick="window.openPrintView()" class="bg-blue-600 hover:bg-blue-700 text-white text-xs font-bold py-2 px-3 rounded flex items-center gap-1">
                            <span>🖨️</span> Imprimir
                        </button>
                    </div>
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
                
                <h3 class="font-bold text-slate-400 mb-3 text-sm uppercase tracking-wider">Últimos Registos</h3>
                <div id="history-list" class="space-y-3">
                    <p class="text-slate-500 text-sm text-center py-4">A carregar...</p>
                </div>
            </div>
        </div>

        <!-- ========================================== -->
        <!-- VIEW: CONFIGURAÇÕES E MEDICAÇÃO            -->
        <!-- ========================================== -->
        <div id="view-settings" class="view space-y-4">
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 shadow-xl">
                <div class="flex justify-between items-center mb-6 border-b border-slate-700 pb-4">
                    <h2 class="text-xl font-black text-white flex items-center gap-2">
                        <span>⚙️</span> Configurações
                    </h2>
                    <button onclick="window.switchView('view-home')" class="text-slate-400 hover:text-white font-bold">Voltar</button>
                </div>

                <div class="space-y-6">
                    <!-- Config de Medicações -->
                    <div>
                        <h3 class="text-yellow-500 font-bold mb-3">💊 Editar Medicações e Suplementos</h3>
                        <div class="space-y-3">
                            <div>
                                <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Medicação Principal (Geral)</label>
                                <textarea id="cfg-med-principal" rows="2" class="text-sm"></textarea>
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Suplementação da Manhã</label>
                                <textarea id="cfg-med-manha" rows="2" class="text-sm"></textarea>
                            </div>
                            <div>
                                <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Suplementação da Noite</label>
                                <textarea id="cfg-med-noite" rows="2" class="text-sm"></textarea>
                            </div>
                            <button onclick="window.saveMedications()" class="w-full bg-yellow-600 hover:bg-yellow-700 text-white font-bold py-3 rounded-xl transition-colors">
                                Guardar Alterações Médicas
                            </button>
                        </div>
                    </div>

                    <hr class="border-slate-700">

                    <!-- Config de Banco de Dados Google Sheets -->
                    <div>
                        <h3 class="text-green-500 font-bold mb-3">📊 Banco de Dados (Google Planilhas)</h3>
                        <p class="text-xs text-slate-400 mb-3">Insira o link (URL) do Google Apps Script para sincronizar na sua Planilha automaticamente.</p>
                        <input type="text" id="cfg-gs-url" placeholder="https://script.google.com/macros/s/.../exec" class="text-sm mb-3">
                        <button onclick="window.saveDatabaseConfig()" class="w-full bg-green-700 hover:bg-green-600 text-white font-bold py-3 rounded-xl transition-colors">
                            Conectar Planilha
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- ========================================== -->
        <!-- VIEW: LOGIN ADMINISTRADOR                  -->
        <!-- ========================================== -->
        <div id="view-login" class="view space-y-4">
            <div class="bg-slate-800 rounded-2xl p-6 border border-slate-700 shadow-xl mt-10">
                <h2 class="text-2xl font-black text-white text-center mb-2">🔐 Acesso Restrito</h2>
                <p class="text-slate-400 text-sm text-center mb-6">Esta área requer credenciais maternas para alterar configurações ou excluir dados.</p>
                
                <form onsubmit="window.handleLogin(event)" class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Email Mãe</label>
                        <input type="email" id="login-email" required placeholder="sosmiqueias@gmail.com">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Senha</label>
                        <input type="password" id="login-pass" required placeholder="••••••••">
                    </div>
                    <div class="pt-2 flex gap-3">
                        <button type="button" onclick="window.switchView('view-home')" class="flex-1 bg-slate-700 hover:bg-slate-600 text-white font-bold py-3 rounded-xl transition-colors">Cancelar</button>
                        <button type="submit" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition-colors">Entrar</button>
                    </div>
                </form>
            </div>
        </div>

        <!-- AS OUTRAS VIEWS (Imprimir, Pânico, Formulário) CONTINUAM IGUAIS -->
        <!-- VIEW: SELEÇÃO PARA IMPRESSÃO -->
        <div id="view-print" class="view space-y-4">
            <div class="bg-slate-800 rounded-2xl p-5 border border-slate-700 shadow-xl">
                <div class="flex justify-between items-center mb-4 border-b border-slate-700 pb-4">
                    <h2 class="text-xl font-black text-white flex items-center gap-2">
                        <span>🖨️</span> Imprimir Histórico
                    </h2>
                    <button onclick="window.switchView('view-home')" class="text-slate-400 hover:text-white font-bold">Voltar</button>
                </div>
                <div class="mb-4">
                    <label class="flex items-center gap-3 cursor-pointer bg-slate-900 p-3 rounded-xl border border-slate-600">
                        <input type="checkbox" id="cb-select-all" onchange="window.toggleSelectAll(this)" class="w-6 h-6 accent-blue-500">
                        <span class="font-bold text-white">Selecionar Todos os Registos</span>
                    </label>
                </div>
                <div id="print-selection-list" class="space-y-3 max-h-[50vh] overflow-y-auto pr-2"></div>
                <div class="mt-6 pt-4 border-t border-slate-700">
                    <button onclick="window.executePrint()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-black text-lg py-4 rounded-2xl shadow-lg transition-colors flex justify-center gap-2">
                        👉 GERAR RELATÓRIO
                    </button>
                </div>
            </div>
        </div>

        <!-- VIEW 2: MODO PÂNICO -->
        <div id="view-panic" class="view space-y-4">
            <div class="bg-red-600 rounded-2xl p-6 text-center shadow-2xl">
                <h2 class="text-3xl font-black text-white uppercase tracking-wider mb-2">Modo Emergência</h2>
                <div class="bg-red-800/50 p-4 rounded-xl mt-4 border border-red-400/30">
                    <p class="font-bold text-yellow-300 text-lg uppercase mb-1">Atenção ao tempo!</p>
                    <p class="text-sm text-white">⚠️ Se a crise passar de 5 minutos, acione socorro médico imediatamente.</p>
                </div>
            </div>
            <div class="bg-slate-800 rounded-2xl p-6 border-2 border-yellow-500 shadow-xl">
                <ul class="space-y-5 text-xl font-bold text-white">
                    <li class="flex items-center gap-4"><span class="text-3xl">🧘</span> Manter a calma</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛑</span> Afastar pessoas</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛌</span> Deitar de lado</li>
                    <li class="flex items-center gap-4"><span class="text-3xl">🛡️</span> Proteger a cabeça</li>
                </ul>
            </div>
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
            <button onclick="window.openRegistrationForm()" class="w-full bg-yellow-500 hover:bg-yellow-600 text-slate-900 font-black text-xl py-6 rounded-2xl shadow-xl mt-8 flex justify-center gap-2 transition-colors">
                👉 REGISTAR CRISE
            </button>
        </div>

        <!-- VIEW 3: FORMULÁRIO PÓS-CRISE -->
        <div id="view-form" class="view space-y-6">
            <div class="bg-yellow-900/40 border border-yellow-600 rounded-2xl p-5 shadow-lg">
                <h3 class="font-black text-yellow-500 text-lg mb-3 flex items-center gap-2"><span>⚠️</span> ORIENTAÇÃO PÓS-CRISE</h3>
                <ul class="text-sm text-slate-200 space-y-2 font-medium">
                    <li>• Ambiente calmo e evitar estímulos (luz/barulho).</li>
                    <li>• Não oferecer nada via oral.</li>
                    <li>• Aguardar recuperação completa.</li>
                </ul>
            </div>

            <form id="crisis-form" onsubmit="window.saveAndSend(event)" class="space-y-6 bg-slate-800 p-5 rounded-2xl border border-slate-700 shadow-xl">
                <h2 class="text-2xl font-black text-white mb-4 border-b border-slate-700 pb-3">📝 Registo da Crise</h2>

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

                <div class="space-y-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">O que estava a fazer antes?</label>
                        <input type="text" id="f-before" placeholder="Ex: A ver TV, A brincar..." required>
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
                            <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Possível Infeção?</label>
                            <input type="text" id="f-infection" placeholder="Ex: Garganta, gripe">
                        </div>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Alimentação antes</label>
                        <input type="text" id="f-food" placeholder="O que comeu nas últimas horas?">
                    </div>
                </div>

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

                <div>
                    <label class="block text-xs font-bold text-slate-400 uppercase mb-1">Observações Gerais</label>
                    <textarea id="f-notes" rows="3" placeholder="Detalhes adicionais importantes..."></textarea>
                </div>

                <div class="pt-4 flex flex-col gap-3">
                    <button type="submit" id="btn-submit-form" class="w-full bg-green-600 hover:bg-green-700 text-white font-black text-xl py-5 rounded-2xl flex items-center justify-center gap-2 shadow-lg transition-colors">
                        👉 GUARDAR REGISTO E ENVIAR
                    </button>
                    <button type="button" onclick="window.cancelRegistration()" class="w-full bg-transparent border-2 border-slate-600 text-slate-300 py-4 rounded-2xl font-bold hover:bg-slate-800 transition-colors">
                        Cancelar Registo
                    </button>
                </div>
            </form>
        </div>

    </main>

    <!-- MODAL DE MENSAGENS E ALERTAS -->
    <div id="custom-modal" class="hidden fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 no-print">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl p-6 w-full max-w-sm shadow-2xl text-center">
            <div class="text-4xl mb-4" id="modal-icon">⚠️</div>
            <h3 id="modal-title" class="text-xl font-bold text-white mb-2">Aviso</h3>
            <p id="modal-text" class="text-slate-300 mb-6"></p>
            <button onclick="window.closeModal()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition-colors">OK, entendi</button>
        </div>
    </div>
    
    <!-- MODAL DE CONFIRMAÇÃO (CANCELAR/APAGAR) -->
    <div id="confirm-modal" class="hidden fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 no-print">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl p-6 w-full max-w-sm shadow-2xl text-center">
            <div class="text-4xl mb-4" id="confirm-icon">❓</div>
            <h3 class="text-xl font-bold text-white mb-2" id="confirm-title">Atenção</h3>
            <p class="text-slate-300 mb-6" id="confirm-text">Deseja cancelar este registo? Nada será guardado.</p>
            <div class="flex gap-3">
                <button onclick="window.closeConfirmModal(false)" class="flex-1 bg-slate-600 hover:bg-slate-500 text-white font-bold py-3 rounded-xl transition-colors">Não</button>
                <button id="btn-confirm-yes" onclick="window.closeConfirmModal(true)" class="flex-1 bg-red-600 hover:bg-red-700 text-white font-bold py-3 rounded-xl transition-colors">Sim</button>
            </div>
        </div>
    </div>

    <!-- SCRIPT (100% INDEPENDENTE E LOCAL + INTEGRAÇÃO PLANILHA) -->
    <script>
        // ESTADO GLOBAL
        const RESPONSAVEL_PHONE = "5584987813129";
        const ADMIN_EMAIL = "sosmiqueias@gmail.com";
        const ADMIN_PASS = "sosmiqueiastt1";
        
        let isSilent = false;
        let audioCtx = null;
        let isAuthenticated = false;
        let actionAfterLogin = null;
        let itemToDelete = null;

        // BANCO DE DADOS LOCAL E CONFIGURAÇÕES
        window.globalCrises = JSON.parse(localStorage.getItem('miqueias_crises_db')) || [];
        
        const defaultMeds = {
            principal: "Levetiracetam 500mg\nUso: 21:00",
            manha: "PEA\nL-Teanina 200mg",
            noite: "Melatonina 41mg"
        };

        // INICIALIZAÇÃO
        document.addEventListener("DOMContentLoaded", () => {
            loadMedications();
            renderHistoryAndStats();
            
            // Pré-preencher config Google Sheets se existir
            const gsUrl = localStorage.getItem('miqueias_gs_url') || '';
            document.getElementById('cfg-gs-url').value = gsUrl;
            
            if(gsUrl) {
                document.getElementById('cloud-status').innerText = "✅ Google Planilhas Conectado";
                document.getElementById('cloud-status').classList.replace('text-blue-400', 'text-green-400');
            }
        });

        // -----------------------------------------
        // GERENCIAMENTO DE MEDICAÇÕES E CONFIG
        // -----------------------------------------
        function loadMedications() {
            const savedMeds = JSON.parse(localStorage.getItem('miqueias_meds_config')) || defaultMeds;
            
            // Atualizar UI da Home
            document.getElementById('ui-med-principal').innerText = savedMeds.principal;
            document.getElementById('ui-med-manha').innerText = savedMeds.manha;
            document.getElementById('ui-med-noite').innerText = savedMeds.noite;

            // Preencher campos de edição nas configurações
            document.getElementById('cfg-med-principal').value = savedMeds.principal;
            document.getElementById('cfg-med-manha').value = savedMeds.manha;
            document.getElementById('cfg-med-noite').value = savedMeds.noite;
        }

        window.saveMedications = function() {
            const newMeds = {
                principal: document.getElementById('cfg-med-principal').value,
                manha: document.getElementById('cfg-med-manha').value,
                noite: document.getElementById('cfg-med-noite').value
            };
            localStorage.setItem('miqueias_meds_config', JSON.stringify(newMeds));
            loadMedications();
            window.showMessage("Sucesso", "As medicações foram atualizadas na memória da plataforma.");
            document.getElementById('modal-icon').innerText = "✅";
        }

        window.saveDatabaseConfig = function() {
            const url = document.getElementById('cfg-gs-url').value.trim();
            if(url && !url.startsWith("https://script.google.com/")) {
                window.showMessage("Erro", "A URL inserida não parece ser um link válido do Google Apps Script.");
                return;
            }
            localStorage.setItem('miqueias_gs_url', url);
            window.showMessage("Sucesso", "Configuração de Banco de Dados guardada com sucesso.");
            document.getElementById('modal-icon').innerText = "✅";
            if(url) {
                document.getElementById('cloud-status').innerText = "✅ Google Planilhas Conectado";
                document.getElementById('cloud-status').classList.replace('text-blue-400', 'text-green-400');
            } else {
                document.getElementById('cloud-status').innerText = "📊 Banco de Dados Local Ativo";
                document.getElementById('cloud-status').className = "text-[10px] font-bold text-blue-400";
            }
        }

        // -----------------------------------------
        // INTEGRAÇÃO COM GOOGLE PLANILHAS (API)
        // -----------------------------------------
        async function sendToGoogleSheets(action, payload) {
            const gsUrl = localStorage.getItem('miqueias_gs_url');
            if (!gsUrl) return; // Trabalha apenas offline se não configurado

            try {
                // Fetch sem CORS stricto para Apps Script
                await fetch(gsUrl, {
                    method: 'POST',
                    mode: 'no-cors', 
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ action: action, data: payload })
                });
                console.log("Planilha atualizada via background.");
            } catch (error) {
                console.error("Erro ao sincronizar com Google Sheets", error);
            }
        }

        window.syncGoogleSheets = function() {
            const gsUrl = localStorage.getItem('miqueias_gs_url');
            if (!gsUrl) {
                window.showMessage("Banco de Dados", "Para fazer backup online e sincronizar, adicione a URL da sua Planilha do Google na área de Configurações (⚙️).");
                return;
            }
            window.showMessage("Sincronização", "O sistema web envia os dados automaticamente em segundo plano para sua planilha.");
            document.getElementById('modal-icon').innerText = "🔄";
        }

        // -----------------------------------------
        // SISTEMA DE AUTENTICAÇÃO
        // -----------------------------------------
        window.openSettings = function() {
            if(isAuthenticated) {
                window.switchView('view-settings');
            } else {
                actionAfterLogin = 'view-settings';
                window.switchView('view-login');
            }
        }

        window.handleLogin = function(e) {
            e.preventDefault();
            const email = document.getElementById('login-email').value;
            const pass = document.getElementById('login-pass').value;

            if(email === ADMIN_EMAIL && pass === ADMIN_PASS) {
                isAuthenticated = true;
                document.getElementById('login-email').value = "";
                document.getElementById('login-pass').value = "";
                
                if(actionAfterLogin === 'delete_item' && itemToDelete) {
                    executeDelete(itemToDelete);
                    window.switchView('view-home');
                } else if(actionAfterLogin) {
                    window.switchView(actionAfterLogin);
                }
            } else {
                window.showMessage("Acesso Negado", "E-mail ou senha incorretos.");
                document.getElementById('modal-icon').innerText = "❌";
            }
        }

        // -----------------------------------------
        // FUNÇÕES DE UI / CORE
        // -----------------------------------------
        window.switchView = function(viewId) {
            document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');
            window.scrollTo(0, 0);
        }

        window.showMessage = function(title, text) {
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-text').innerText = text;
            document.getElementById('custom-modal').classList.remove('hidden');
        }

        window.closeModal = function() {
            document.getElementById('custom-modal').classList.add('hidden');
            document.getElementById('modal-icon').innerText = "⚠️";
        }

        window.cancelRegistration = function() {
            document.getElementById('confirm-icon').innerText = "❓";
            document.getElementById('confirm-title').innerText = "Cancelar Registo";
            document.getElementById('confirm-text').innerText = "Deseja cancelar este registo? Nada será guardado.";
            document.getElementById('btn-confirm-yes').onclick = () => window.closeConfirmModal(true);
            document.getElementById('confirm-modal').classList.remove('hidden');
        }

        window.closeConfirmModal = function(confirm) {
            document.getElementById('confirm-modal').classList.add('hidden');
            if (confirm) window.switchView('view-home');
        }

        window.toggleSound = function() {
            isSilent = !isSilent;
            const btn = document.getElementById('btn-sound');
            if(isSilent) {
                btn.innerText = "🔇";
                btn.classList.replace('text-gray-300', 'text-red-400');
            } else {
                btn.innerText = "🔊";
                btn.classList.replace('text-red-400', 'text-gray-300');
            }
        }

        window.playBeep = function() {
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
            } catch (e) {}
        }

        window.triggerVibration = function(pattern) {
            if ("vibrate" in navigator && !isSilent) navigator.vibrate(pattern);
        }

        window.startPanicMode = function() {
            if (!audioCtx && !isSilent) {
                try { audioCtx = new (window.AudioContext || window.webkitAudioContext)(); } catch(e){}
            }
            window.switchView('view-panic');
            window.triggerVibration([300, 100, 300, 100, 600]); 
            window.playBeep();
        }

        window.openRegistrationForm = function() {
            window.triggerVibration(100);
            const now = new Date();
            document.getElementById('f-date').value = now.getFullYear() + '-' + String(now.getMonth() + 1).padStart(2, '0') + '-' + String(now.getDate()).padStart(2, '0');
            document.getElementById('f-time').value = String(now.getHours()).padStart(2, '0') + ':' + String(now.getMinutes()).padStart(2, '0');
            
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

            window.switchView('view-form');
        }

        // GUARDAR DADOS 
        window.saveAndSend = function(e) {
            e.preventDefault();
            const btnSubmit = document.getElementById('btn-submit-form');
            btnSubmit.innerText = "⏳ A Guardar...";
            btnSubmit.disabled = true;
            
            const min = document.getElementById('f-min').value || 0;
            const sec = document.getElementById('f-sec').value || 0;
            const timeStr = `${min}min ${sec}seg`;

            const dataToSave = {
                id: "id_" + Date.now().toString(),
                timestamp: Date.now(),
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

            // Salva na memória do Dispositivo (Funciona Offline e Online)
            window.globalCrises.unshift(dataToSave);
            localStorage.setItem('miqueias_crises_db', JSON.stringify(window.globalCrises));
            
            // Envia para o Google Planilhas no fundo
            sendToGoogleSheets("add", dataToSave);

            renderHistoryAndStats();

            btnSubmit.innerText = "👉 GUARDAR REGISTO E ENVIAR";
            btnSubmit.disabled = false;
            window.switchView('view-home');

            const dateBR = dataToSave.date.split('-').reverse().join('/');
            const msg = `Crise registada — Miquéias Braga\nData: ${dateBR}\nHora: ${dataToSave.time}\nTempo: ${dataToSave.duration}\nTipo: ${dataToSave.type}\nAntes da crise: ${dataToSave.before}\nFebre: ${dataToSave.fever}\nInfeção: ${dataToSave.infection}\nAlimentação: ${dataToSave.food}\nSinais vitais:\nPA: ${dataToSave.pa}\nSpO2: ${dataToSave.spo2}${dataToSave.spo2 !== 'Não aferido' ? '%' : ''}\nBPM: ${dataToSave.bpm}\nObservações: ${dataToSave.notes}`;

            const url = `https://wa.me/${RESPONSAVEL_PHONE}?text=${encodeURIComponent(msg)}`;
            window.open(url, '_blank');
        }

        // RENDERIZAR ESTATÍSTICAS E LISTA
        function renderHistoryAndStats() {
            const history = window.globalCrises;
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
                listContainer.innerHTML = '<p class="text-slate-500 text-sm text-center py-4">Nenhum registo encontrado.</p>';
                return;
            }

            listContainer.innerHTML = history.slice(0, 20).map(item => {
                const dateBR = item.date.split('-').reverse().join('/');
                return `
                <div class="bg-slate-900 p-4 rounded-xl border-l-4 border-slate-600 shadow-sm flex flex-col gap-1 relative">
                    <button onclick="window.requestDelete('${item.id}')" class="absolute top-2 right-2 text-slate-500 hover:text-red-500 bg-slate-800 rounded px-2 py-1 text-xs">🗑️ Excluir</button>
                    <div class="flex justify-between items-start pr-16">
                        <p class="font-bold text-white text-sm">${dateBR} às ${item.time}</p>
                    </div>
                    <span class="text-xs font-bold text-slate-400 bg-slate-800 px-2 py-1 rounded w-max mt-1">${item.duration}</span>
                    <p class="text-sm text-slate-300 mt-1">Tipo: <span class="font-bold text-yellow-500">${item.type}</span></p>
                    <p class="text-xs text-slate-500 truncate">Obs: ${item.notes}</p>
                </div>`;
            }).join('');
        }

        // SISTEMA DE EXCLUSÃO DE REGISTOS
        window.requestDelete = function(id) {
            itemToDelete = id;
            if(isAuthenticated) {
                // Já autenticado na sessão, mostrar confirmação direta
                document.getElementById('confirm-icon').innerText = "🗑️";
                document.getElementById('confirm-title').innerText = "Excluir Registo";
                document.getElementById('confirm-text').innerText = "Tem certeza que deseja apagar permanentemente este registo?";
                document.getElementById('btn-confirm-yes').onclick = () => {
                    executeDelete(itemToDelete);
                    document.getElementById('confirm-modal').classList.add('hidden');
                };
                document.getElementById('confirm-modal').classList.remove('hidden');
            } else {
                // Pedir credenciais
                actionAfterLogin = 'delete_item';
                window.switchView('view-login');
            }
        }

        function executeDelete(id) {
            // Remove do array local
            window.globalCrises = window.globalCrises.filter(item => item.id !== id);
            localStorage.setItem('miqueias_crises_db', JSON.stringify(window.globalCrises));
            
            // Renderiza
            renderHistoryAndStats();
            
            // Envia comando de delete para a Planilha do Google
            sendToGoogleSheets("delete", { id: id });
            
            window.showMessage("Excluído", "O registo foi apagado do banco de dados com sucesso.");
            document.getElementById('modal-icon').innerText = "🗑️";
            itemToDelete = null;
        }

        // SISTEMA DE IMPRESSÃO
        window.openPrintView = function() {
            const history = window.globalCrises;
            const listContainer = document.getElementById('print-selection-list');
            
            if (history.length === 0) {
                listContainer.innerHTML = '<p class="text-slate-500 text-center py-6">Nenhum registo disponível para impressão.</p>';
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
            window.switchView('view-print');
        }

        window.toggleSelectAll = function(masterCheckbox) {
            const checkboxes = document.querySelectorAll('.print-cb');
            checkboxes.forEach(cb => cb.checked = masterCheckbox.checked);
        }

        window.executePrint = function() {
            const selectedCheckboxes = document.querySelectorAll('.print-cb:checked');
            if (selectedCheckboxes.length === 0) {
                window.showMessage("Nenhum item selecionado", "Por favor, selecione pelo menos um registo para poder gerar o relatório de impressão.");
                return;
            }

            const selectedIds = Array.from(selectedCheckboxes).map(cb => String(cb.value));
            const history = window.globalCrises;
            
            const recordsToPrint = history.filter(item => selectedIds.includes(String(item.id)));
            
            const printHtml = recordsToPrint.map(data => {
                const dateBR = data.date.split('-').reverse().join('/');
                return `
                <div class="print-record">
                    <h3>Registo: ${dateBR} às ${data.time}</h3>
                    <p><strong>Tipo de Crise:</strong> ${data.type}</p>
                    <p><strong>Duração:</strong> ${data.duration}</p>
                    <p><strong>O que estava a fazer:</strong> ${data.before}</p>
                    <p><strong>Apresentou Febre?</strong> ${data.fever}</p>
                    <p><strong>Possível Infeção:</strong> ${data.infection}</p>
                    <p><strong>Alimentação Recente:</strong> ${data.food}</p>
                    <p><strong>Sinais Vitais Pós-Crise:</strong> PA: ${data.pa} | SpO2: ${data.spo2}${data.spo2 !== 'Não aferido' ? '%' : ''} | BPM: ${data.bpm}</p>
                    <p><strong>Observações Extras:</strong> ${data.notes}</p>
                </div>`;
            }).join('');

            document.getElementById('print-content').innerHTML = printHtml;
            window.print();
        }
    </script>
    
    <!-- 
    ========================================================
    INSTRUÇÕES PARA ATIVAR O BANCO DE DADOS GOOGLE PLANILHAS
    ========================================================
    Como o Javascript não pode fazer "Login" no Google de forma invisível, siga este passo a passo para criar sua "API" na Planilha:

    1. Crie uma nova Planilha no seu Google Drive da conta sosmiqueias@gmail.com
    2. Na Planilha, clique em "Extensões" -> "Apps Script"
    3. Apague tudo o que estiver escrito lá e cole o seguinte código:

    function doPost(e) {
      var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
      var req = JSON.parse(e.postData.contents);
      var data = req.data;

      if(req.action === 'add') {
         sheet.appendRow([data.id, data.date, data.time, data.duration, data.type, data.before, data.fever, data.infection, data.food, data.pa, data.spo2, data.bpm, data.notes]);
         return ContentService.createTextOutput(JSON.stringify({"status": "success"})).setMimeType(ContentService.MimeType.JSON);
      } else if(req.action === 'delete') {
         var dataRange = sheet.getDataRange();
         var values = dataRange.getValues();
         for (var i = 0; i < values.length; i++) {
            if (values[i][0] == data.id) {
               sheet.deleteRow(i + 1);
               break;
            }
         }
         return ContentService.createTextOutput(JSON.stringify({"status": "success"})).setMimeType(ContentService.MimeType.JSON);
      }
    }

    4. Clique em "Implantar" (botão azul no canto superior direito) -> "Nova implantação".
    5. Escolha o tipo "App da Web" (engrenagem no lado esquerdo).
    6. Em "Quem pode acessar", coloque "Qualquer pessoa".
    7. Clique em "Implantar", autorize o acesso (em Advanced / Ir para o projeto) e copie a URL do Web App gerada.
    8. Abra o seu aplicativo web (este HTML), clique na engrenagem (⚙️ Configurações) com a senha.
    9. Cole a URL copiada na área de Banco de Dados e pronto! Todos os seus dados estarão seguros na sua planilha.
    -->
</body>
</html>
