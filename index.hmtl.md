<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Avaliação de Desempenho de Equipe</title>
    <!-- Carregando o Tailwind CSS para estilização fácil e responsiva -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Define a fonte Inter como padrão para uma aparência moderna */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f9fb;
        }
        /* Estilização básica para o indicador de classificação */
        .classification-indicator {
            padding: 0.5rem 1rem;
            border-radius: 0.5rem;
            font-weight: 600;
            text-align: center;
            transition: background-color 0.3s, color 0.3s;
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'excelente': '#10b981', /* Green */
                        'bom': '#f97316',      /* Orange */
                        'regular': '#f59e0b',  /* Amber */
                        'insatisfatorio': '#ef4444', /* Red */
                    }
                }
            }
        }
    </script>
</head>
<body class="p-4 sm:p-8 min-h-screen flex items-center justify-center">

    <div class="w-full max-w-2xl bg-white shadow-xl rounded-2xl p-6 sm:p-8 border border-gray-100">
        
        <header class="mb-6 text-center">
            <h1 class="text-3xl font-bold text-gray-800">Avaliação de Desempenho</h1>
        </header>

        <!-- Navegação entre Views -->
        <nav class="flex space-x-2 mb-6 border-b pb-2">
            <button id="btn-evaluation" onclick="toggleView('evaluation')" class="flex-1 py-2 px-4 text-sm font-semibold rounded-lg bg-indigo-600 text-white shadow-md hover:bg-indigo-700 transition duration-150">
                Nova Avaliação
            </button>
            <button id="btn-consultation" onclick="toggleView('consultation')" class="flex-1 py-2 px-4 text-sm font-semibold rounded-lg bg-gray-200 text-gray-700 hover:bg-gray-300 transition duration-150">
                Consultar Histórico
            </button>
        </nav>

        <!-- 1. VIEW DE AVALIAÇÃO (PADRÃO) -->
        <div id="evaluation-view">
            <p class="text-gray-500 mt-2 mb-6 text-center">Insira as informações e pontuações para salvar o registro.</p>

            <!-- Seção de Identificação -->
            <div class="space-y-4 mb-8 p-4 bg-gray-50 rounded-xl border border-gray-200">
                <h2 class="text-xl font-bold text-gray-700">Dados do Registro</h2>
                <div>
                    <label for="colaborador" class="block text-sm font-medium text-gray-700 mb-1">Nome do Colaborador (Obrigatório)</label>
                    <input type="text" id="colaborador" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500" placeholder="Ex: João da Silva">
                </div>
                <div>
                    <label for="avaliador" class="block text-sm font-medium text-gray-700 mb-1">Nome do Avaliador (Obrigatório)</label>
                    <input type="text" id="avaliador" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500" placeholder="Ex: Maria Souza (Gerente)">
                </div>
            </div>

            <!-- Seção de Entradas (Critérios de Avaliação) -->
            <div id="input-section" class="space-y-6 mb-8">

                <!-- Critério: Desempenho (Peso 50%) -->
                <div class="p-4 bg-indigo-50 rounded-xl shadow-sm border border-indigo-200">
                    <label for="desempenho" class="block text-lg font-medium text-indigo-800 mb-2">
                        1. Desempenho <span class="text-sm font-normal text-indigo-600">(Peso 50%)</span>
                    </label>
                    <select id="desempenho" class="w-full p-3 border border-indigo-300 rounded-lg focus:ring-indigo-500 focus:border-indigo-500 bg-white shadow-inner appearance-none transition duration-150 ease-in-out cursor-pointer">
                        <option value="5">5 - Excelente (Qualidade, metas, proatividade e rigor)</option>
                        <option value="4">4 - Acima da Média</option>
                        <option value="3" selected>3 - Regular (Cumprimento parcial ou inconsistente)</option>
                        <option value="2">2 - Abaixo da Média</option>
                        <option value="1">1 - Insatisfatório (Problemas de qualidade e não cumprimento de metas)</option>
                    </select>
                </div>

                <!-- Critério: Assiduidade (Peso 30%) -->
                <div class="p-4 bg-green-50 rounded-xl shadow-sm border border-green-200">
                    <label for="assiduidade" class="block text-lg font-medium text-green-800 mb-2">
                        2. Assiduidade <span class="text-sm font-normal text-green-600">(Peso 30%)</span>
                    </label>
                    <select id="assiduidade" class="w-full p-3 border border-green-300 rounded-lg focus:ring-green-500 focus:border-green-500 bg-white shadow-inner appearance-none transition duration-150 ease-in-out cursor-pointer">
                        <option value="5" selected>5 - Sempre pontual (Comprometimento total com horários)</option>
                        <option value="4">4 - Raros atrasos/faltas leves</option>
                        <option value="3">3 - Cumpre parcialmente (Atrasos e faltas regulares, mas controlados)</option>
                        <option value="2">2 - Muitos atrasos/faltas, impactando o trabalho</option>
                        <option value="1">1 - Muitas faltas e atrasos (Presença e pontualidade problemáticas)</option>
                    </select>
                </div>

                <!-- Critério: Tempo de Empresa (Peso 20%) -->
                <div class="p-4 bg-red-50 rounded-xl shadow-sm border border-red-200">
                    <label for="tempo" class="block text-lg font-medium text-red-800 mb-2">
                        3. Tempo de Empresa <span class="text-sm font-normal text-red-600">(Peso 20%)</span>
                    </label>
                    <select id="tempo" class="w-full p-3 border border-red-300 rounded-lg focus:ring-red-500 focus:border-red-500 bg-white shadow-inner appearance-none transition duration-150 ease-in-out cursor-pointer">
                        <option value="5" selected>5 - Acima de 24 meses (Experiência Consolidada)</option>
                        <option value="4">4 - 18 a 24 meses (Experiência Sênior)</option>
                        <option value="3">3 - 12 a 18 meses (Experiência Plena)</option>
                        <option value="2">2 - 7 a 11 meses (Experiência Júnior)</option>
                        <option value="1">1 - Até 6 meses (Novo na empresa)</option>
                    </select>
                </div>
            </div>

            <!-- Seção de Resultados e Salvar -->
            <div class="bg-gray-100 p-6 rounded-xl border border-gray-300">
                <h2 class="text-xl font-bold text-gray-700 mb-4 border-b pb-2">Resultado da Avaliação</h2>
                
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-4 space-y-3 sm:space-y-0">
                    <p class="text-2xl font-semibold text-gray-700">Nota Final:</p>
                    <span id="nota-final" class="text-4xl font-extrabold text-indigo-600 bg-indigo-200 px-4 py-2 rounded-lg shadow-md">
                        4.1
                    </span>
                </div>

                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-4 space-y-3 sm:space-y-0">
                    <p class="text-2xl font-semibold text-gray-700">Classificação:</p>
                    <span id="classificacao" class="classification-indicator bg-bom text-white">
                        BOM
                    </span>
                </div>
                
                <div>
                    <p class="text-lg font-semibold text-gray-700 mt-4 mb-2">Ação Sugerida:</p>
                    <p id="acao-sugerida" class="text-gray-600 p-3 bg-white border border-gray-200 rounded-lg italic">
                        Buscar pontos de melhoria e acompanhar o desenvolvimento em áreas específicas.
                    </p>
                </div>

                <button id="salvar-btn" onclick="salvarAvaliacao()" class="mt-6 w-full py-3 bg-indigo-600 text-white font-bold rounded-xl shadow-lg hover:bg-indigo-700 transition duration-300 disabled:bg-indigo-400 flex items-center justify-center">
                    <span id="btn-text">Salvar Avaliação</span>
                    <svg id="spinner" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white hidden" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                    </svg>
                </button>
                <p id="status-message" class="mt-3 text-center text-sm font-medium h-4"></p>
            </div>
        </div>

        <!-- 2. VIEW DE CONSULTA (OCULTA POR PADRÃO) -->
        <div id="consultation-view" class="hidden">
            <h2 class="text-2xl font-bold text-gray-800 mb-4">Histórico de Avaliações</h2>
            
            <p id="list-status" class="text-gray-500 mb-4 text-center">Carregando dados...</p>

            <div id="avaliacoes-list" class="space-y-3">
                <!-- A lista de avaliações será renderizada aqui -->
            </div>
        </div>
        
        <footer class="mt-6 text-xs text-gray-400 text-center">
            <p id="user-info">Aguardando inicialização...</p>
        </footer>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global Firebase Instances
        let app = null;
        let db = null;
        let auth = null;
        let userId = null;
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

        // Constantes e Pesos
        const PESOS = {
            desempenho: 0.5,
            assiduidade: 0.3,
            tempo: 0.2
        };

        const CLASSIFICACOES = [
            { min: 4.5, max: 5.0, label: 'EXCELENTE', colorClass: 'bg-excelente text-white', colorKey: 'excelente', action: 'Manter o reconhecimento e buscar novas oportunidades de desenvolvimento.' },
            { min: 3.5, max: 4.4, label: 'BOM', colorClass: 'bg-bom text-white', colorKey: 'bom', action: 'Buscar pontos de melhoria e acompanhar o desenvolvimento em áreas específicas.' },
            { min: 2.5, max: 3.4, label: 'REGULAR', colorClass: 'bg-regular text-gray-800', colorKey: 'regular', action: 'Criar um Plano de Desenvolvimento Individual (PDI) com metas claras e acompanhamento semanal.' },
            { min: 0.0, max: 2.4, label: 'INSATISFATÓRIO', colorClass: 'bg-insatisfatorio text-white', colorKey: 'insatisfatorio', action: 'Revisão urgente de performance e análise de adequação ao cargo. Pode ser necessário um acompanhamento intensivo ou desligamento.' }
        ];

        // Elementos de UI - Avaliação
        const colaboradorEl = document.getElementById('colaborador');
        const avaliadorEl = document.getElementById('avaliador');
        const desempenhoEl = document.getElementById('desempenho');
        const assiduidadeEl = document.getElementById('assiduidade');
        const tempoEl = document.getElementById('tempo');
        const notaFinalEl = document.getElementById('nota-final');
        const classificacaoEl = document.getElementById('classificacao');
        const acaoSugeridaEl = document.getElementById('acao-sugerida');
        const salvarBtn = document.getElementById('salvar-btn');
        const btnText = document.getElementById('btn-text');
        const spinner = document.getElementById('spinner');
        const statusMessageEl = document.getElementById('status-message');
        const userInfoEl = document.getElementById('user-info');
        
        // Elementos de UI - Consulta
        const evaluationView = document.getElementById('evaluation-view');
        const consultationView = document.getElementById('consultation-view');
        const btnEvaluation = document.getElementById('btn-evaluation');
        const btnConsultation = document.getElementById('btn-consultation');
        const listContainerEl = document.getElementById('avaliacoes-list');
        const listStatusEl = document.getElementById('list-status');


        /**
         * Inicializa o Firebase e realiza a autenticação do usuário.
         */
        async function setupFirebaseAndAuth() {
            try {
                // Ativar logs de debug para o Firestore
                setLogLevel('debug');
                
                const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
                
                app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);

                // Espera o estado de autenticação mudar
                await new Promise((resolve) => {
                    const unsubscribe = onAuthStateChanged(auth, async (user) => {
                        if (!user) {
                            const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
                            
                            if (initialAuthToken) {
                                await signInWithCustomToken(auth, initialAuthToken);
                            } else {
                                await signInAnonymously(auth);
                            }
                        }
                        userId = auth.currentUser?.uid || crypto.randomUUID();
                        userInfoEl.textContent = `App ID: ${appId}`; // Removido User ID para o app público
                        unsubscribe(); 
                        resolve();
                    });
                });
                
                // Inicia a escuta em tempo real dos dados (mesmo que a tela de consulta esteja oculta)
                fetchEvaluations(true); 

            } catch (error) {
                console.error("Erro ao inicializar Firebase ou autenticar:", error);
                userInfoEl.textContent = `Erro de Inicialização! Verifique o console.`;
            }
        }

        /**
         * Calcula a Nota Final com base nas pontuações e pesos.
         */
        function calcularNotaFinal() {
            const d = parseFloat(desempenhoEl.value) || 0;
            const a = parseFloat(assiduidadeEl.value) || 0;
            const t = parseFloat(tempoEl.value) || 0;

            const nota = (d * PESOS.desempenho) + (a * PESOS.assiduidade) + (t * PESOS.tempo);
            
            return Math.round(nota * 10) / 10;
        }

        /**
         * Determina a classificação e a ação sugerida com base na nota.
         * @param {number} nota - A nota final calculada.
         */
        function determinarClassificacao(nota) {
            for (const c of CLASSIFICACOES) {
                if (nota >= c.min && nota <= c.max) {
                    return c;
                }
            }
            return CLASSIFICACOES[3]; // Padrão (Insatisfatório)
        }

        /**
         * Atualiza a interface do usuário com os novos resultados.
         */
        function atualizarResultado() {
            const nota = calcularNotaFinal();
            const resultado = determinarClassificacao(nota);

            // 1. Atualiza a Nota Final
            notaFinalEl.textContent = nota.toFixed(1);

            // 2. Atualiza a Classificação (rótulo e cor)
            classificacaoEl.className = 'classification-indicator'; 
            classificacaoEl.classList.add(...resultado.colorClass.split(' '));
            classificacaoEl.textContent = resultado.label;

            // 3. Atualiza a Ação Sugerida
            acaoSugeridaEl.textContent = resultado.action;
        }

        /**
         * Salva a avaliação no Firestore no caminho PÚBLICO.
         */
        window.salvarAvaliacao = async function() {
            if (!db || !userId) {
                statusMessageEl.className = 'mt-3 text-center text-sm font-medium text-red-500';
                statusMessageEl.textContent = "Erro: Firebase não inicializado. Tente recarregar a página.";
                console.error("Firebase não inicializado.");
                return;
            }

            // 1. Coleta de Dados
            const colaboradorNome = colaboradorEl.value.trim();
            const avaliadorNome = avaliadorEl.value.trim();
            
            if (!colaboradorNome || !avaliadorNome) {
                statusMessageEl.className = 'mt-3 text-center text-sm font-medium text-red-500';
                statusMessageEl.textContent = "Por favor, preencha o Nome do Colaborador e do Avaliador.";
                return;
            }

            const nota = calcularNotaFinal();
            const resultado = determinarClassificacao(nota);

            const avaliacaoData = {
                colaborador: colaboradorNome,
                avaliador: avaliadorNome,
                desempenho: parseFloat(desempenhoEl.value),
                assiduidade: parseFloat(assiduidadeEl.value),
                tempo_empresa: parseFloat(tempoEl.value),
                nota_final: nota,
                classificacao: resultado.label,
                acao_sugerida: resultado.action,
                data_avaliacao: new Date().toISOString(),
                avaliador_id: userId // Mantém o ID do avaliador para rastreamento interno
            };
            
            // 2. Estado de Carregamento
            salvarBtn.disabled = true;
            btnText.textContent = "Salvando...";
            spinner.classList.remove('hidden');
            statusMessageEl.textContent = "";

            // 3. Salvamento no Firestore (Caminho PÚBLICO: /artifacts/{appId}/public/data/avaliacoes)
            try {
                const path = `artifacts/${appId}/public/data/avaliacoes`;
                await addDoc(collection(db, path), avaliacaoData);
                
                statusMessageEl.className = 'mt-3 text-center text-sm font-medium text-excelente';
                statusMessageEl.textContent = `Avaliação de ${colaboradorNome} salva com sucesso!`;
                
                // Limpa campos de identificação após salvar para o próximo usuário
                colaboradorEl.value = '';
                avaliadorEl.value = ''; 

            } catch (error) {
                console.error("Erro ao salvar avaliação:", error);
                statusMessageEl.className = 'mt-3 text-center text-sm font-medium text-red-500';
                statusMessageEl.textContent = "Erro ao salvar! Verifique o console.";
            } finally {
                // 4. Finaliza o Estado de Carregamento
                salvarBtn.disabled = false;
                btnText.textContent = "Salvar Avaliação";
                spinner.classList.add('hidden');
            }
        }

        /**
         * Alterna entre as telas de Avaliação e Consulta.
         * @param {string} viewId - 'evaluation' ou 'consultation'
         */
        window.toggleView = function(viewId) {
            if (viewId === 'evaluation') {
                evaluationView.classList.remove('hidden');
                consultationView.classList.add('hidden');
                btnEvaluation.classList.add('bg-indigo-600', 'text-white');
                btnEvaluation.classList.remove('bg-gray-200', 'text-gray-700');
                btnConsultation.classList.remove('bg-indigo-600', 'text-white');
                btnConsultation.classList.add('bg-gray-200', 'text-gray-700');

            } else if (viewId === 'consultation') {
                evaluationView.classList.add('hidden');
                consultationView.classList.remove('hidden');
                btnConsultation.classList.add('bg-indigo-600', 'text-white');
                btnConsultation.classList.remove('bg-gray-200', 'text-gray-700');
                btnEvaluation.classList.remove('bg-indigo-600', 'text-white');
                btnEvaluation.classList.add('bg-gray-200', 'text-gray-700');
                // A busca é feita em tempo real e já está ativa
            }
        }

        /**
         * Renderiza a lista de avaliações na tela de consulta.
         * @param {Array<Object>} evaluations - Lista de avaliações.
         */
        function renderEvaluations(evaluations) {
            listContainerEl.innerHTML = ''; // Limpa

            if (evaluations.length === 0) {
                listStatusEl.textContent = "Nenhuma avaliação encontrada. Comece a salvar novos registros!";
                return;
            }

            listStatusEl.textContent = `Total de Avaliações: ${evaluations.length}`;

            // Cria o cabeçalho da tabela (para visualização no desktop)
            const header = `
                <div class="hidden sm:grid grid-cols-12 gap-4 text-sm font-semibold text-gray-600 border-b pb-2 mb-3">
                    <div class="col-span-4">Colaborador</div>
                    <div class="col-span-2 text-center">Nota</div>
                    <div class="col-span-3 text-center">Classificação</div>
                    <div class="col-span-3 text-right">Data</div>
                </div>
            `;
            listContainerEl.innerHTML += header;

            evaluations.forEach(evalData => {
                const date = new Date(evalData.data_avaliacao);
                const formattedDate = date.toLocaleDateString('pt-BR');
                const formattedTime = date.toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' });
                
                // Busca a cor correspondente baseada na classificação
                const result = CLASSIFICACOES.find(c => c.label === evalData.classificacao);
                const color = result ? result.colorKey : 'gray-500';
                
                // Se o tailwind.config ainda não estiver completamente processado, usa a cor base.
                const colorHex = tailwind.config.theme.extend.colors[color] || '#6b7280'; 
                const textColor = color === 'regular' ? '#4b5563' : 'white';

                // Item da Lista/Tabela
                const item = `
                    <div class="bg-white p-4 rounded-xl shadow-sm mb-3 border border-gray-200 hover:shadow-md transition duration-200">
                        <div class="grid grid-cols-12 gap-4 items-center">
                            <!-- Colaborador / Nome -->
                            <div class="col-span-12 sm:col-span-4 font-bold text-gray-800 truncate" title="Avaliador: ${evalData.avaliador}">
                                ${evalData.colaborador}
                            </div>
                            
                            <!-- Nota -->
                            <div class="col-span-4 sm:col-span-2 text-center">
                                <span class="text-sm font-semibold text-gray-500 block sm:hidden">Nota:</span>
                                <span class="text-lg font-extrabold text-indigo-600">${evalData.nota_final.toFixed(1)}</span>
                            </div>
                            
                            <!-- Classificação -->
                            <div class="col-span-4 sm:col-span-3 text-center">
                                <span class="text-sm font-semibold text-gray-500 block sm:hidden">Status:</span>
                                <span class="classification-indicator" style="background-color: ${colorHex}; color: ${textColor}; padding: 4px 8px; font-size: 0.75rem;">
                                    ${evalData.classificacao}
                                </span>
                            </div>

                            <!-- Data -->
                            <div class="col-span-4 sm:col-span-3 text-right text-sm text-gray-500">
                                <span class="font-semibold block sm:hidden">Data:</span>
                                ${formattedDate} ${formattedTime}
                            </div>
                        </div>
                        <div class="mt-2 pt-2 border-t border-gray-100 sm:hidden">
                             <p class="text-xs text-gray-600 italic">Avaliador: ${evalData.avaliador}</p>
                        </div>
                    </div>
                `;
                listContainerEl.innerHTML += item;
            });
        }


        /**
         * Busca e monitora em tempo real as avaliações no Firestore no caminho PÚBLICO.
         * @param {boolean} silent - Se for true, não atualiza o status de carregamento.
         */
        function fetchEvaluations(silent = false) {
            if (!db || !userId) {
                if (!silent) listStatusEl.textContent = "Erro: Firebase não inicializado.";
                return;
            }

            if (!silent) listStatusEl.textContent = "Carregando avaliações...";

            try {
                const path = `artifacts/${appId}/public/data/avaliacoes`;
                const q = collection(db, path);
                
                // onSnapshot monitora em tempo real
                onSnapshot(q, (snapshot) => {
                    const evaluations = [];
                    snapshot.forEach((doc) => {
                        evaluations.push({ id: doc.id, ...doc.data() });
                    });

                    // Ordena localmente pela data_avaliacao, do mais recente para o mais antigo (necessário pois não usamos orderBy)
                    evaluations.sort((a, b) => {
                        const dateA = a.data_avaliacao instanceof Date ? a.data_avaliacao : new Date(a.data_avaliacao);
                        const dateB = b.data_avaliacao instanceof Date ? b.data_avaliacao : new Date(b.data_avaliacao);
                        return dateB - dateA;
                    });

                    renderEvaluations(evaluations);
                }, (error) => {
                    console.error("Erro ao buscar avaliações (onSnapshot):", error);
                    listStatusEl.textContent = "Erro ao carregar dados. Verifique o console.";
                });

            } catch (error) {
                console.error("Erro ao configurar listener do Firestore:", error);
                listStatusEl.textContent = "Erro ao buscar avaliações. Tente novamente.";
            }
        }


        // --- Inicialização ---

        // Adiciona event listeners para recalcular quando qualquer input mudar
        [desempenhoEl, assiduidadeEl, tempoEl].forEach(el => {
            el.addEventListener('change', atualizarResultado);
        });

        // Inicializa Firebase e executa o cálculo inicial
        window.onload = async function() {
            await setupFirebaseAndAuth();
            atualizarResultado();
        };

    </script>
</body>
</html>
