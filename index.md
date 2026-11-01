<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="theme-color" content="#4F46E5">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <title>Organizaê — Gestão Escolar, Notas e Foco</title>
  <!-- Ícone SVG Embutido (PWA Favicon) -->
  <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512' fill='none'%3E%3Crect width='512' height='512' rx='128' fill='%234F46E5'/%3E%3Cpath d='M368 272C368 338.274 314.274 392 248 392C181.726 392 128 338.274 128 272C128 205.726 181.726 152 248 152C273.2 152 296.6 159.8 316 173' stroke='white' stroke-width='40' stroke-linecap='round'/%3E%3Cpath d='M224 96H272' stroke='white' stroke-width='32' stroke-linecap='round'/%3E%3Cpath d='M196 268L236 308L364 164' stroke='%2310B981' stroke-width='44' stroke-linecap='round' stroke-linejoin='round'/%3E%3Ccircle cx='384' cy='212' r='20' fill='%23F59E0B'/%3E%3C/svg%3E">
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
    body {
      font-family: 'Inter', sans-serif;
      background-color: #0F172A;
      color: #0F172A;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
    }
    /* Proporção Mobile-First 9:16 (RNF13) */
    .app-shell {
      max-width: 430px;
      margin: 0 auto;
      min-height: 100dvh;
      background-color: #F8FAFC;
      position: relative;
      display: flex;
      flex-direction: column;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.6);
    }
    .hide-scroll::-webkit-scrollbar {
      display: none;
    }
    /* Área mínima de toque acessível (RNF03) */
    .touch-target {
      min-height: 44px;
    }
  </style>
</head>
<body>

<div class="app-shell">

  <!-- ================= T01: TELA DE IDENTIFICAÇÃO E LOGIN (RF01, RF02, RF03) ================= -->
  <section id="login-screen" class="flex-1 flex flex-col justify-center px-6 py-8 bg-gradient-to-b from-indigo-600 via-indigo-700 to-slate-900 text-white">
    <div class="mb-6 text-center">
      <!-- Ícone Oficial Organizaê SVG -->
      <div class="w-20 h-20 mx-auto mb-3 shadow-2xl rounded-3xl overflow-hidden border-2 border-white/20">
        <svg viewBox="0 0 512 512" fill="none" xmlns="http://www.w3.org/2000/svg" class="w-full h-full">
          <rect width="512" height="512" rx="120" fill="url(#logo_grad)"/>
          <path d="M368 272C368 338.274 314.274 392 248 392C181.726 392 128 338.274 128 272C128 205.726 181.726 152 248 152C273.2 152 296.6 159.8 316 173" stroke="#FFFFFF" stroke-width="40" stroke-linecap="round"/>
          <path d="M224 96H272" stroke="#FFFFFF" stroke-width="32" stroke-linecap="round"/>
          <path d="M196 268L236 308L364 164" stroke="#10B981" stroke-width="44" stroke-linecap="round" stroke-linejoin="round"/>
          <circle cx="384" cy="212" r="22" fill="#F59E0B"/>
          <defs>
            <linearGradient id="logo_grad" x1="0" y1="0" x2="512" y2="512" gradientUnits="userSpaceOnUse">
              <stop stop-color="#4F46E5"/>
              <stop offset="1" stop-color="#312E81"/>
            </linearGradient>
          </defs>
        </svg>
      </div>
      <h1 class="text-3xl font-extrabold tracking-tight">Organizaê</h1>
      <p class="text-indigo-200 text-xs font-medium mt-1">Sua turma sincronizada. Seu foco no lugar.</p>
    </div>

    <form id="login-form" class="bg-white text-slate-900 rounded-3xl p-6 shadow-2xl space-y-3.5">
      <div>
        <label class="block text-[11px] font-extrabold uppercase tracking-wider text-slate-500 mb-1">Nome do Estudante</label>
        <input type="text" id="input-name" required placeholder="Ex.: Lucas Silva"
          class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600 text-sm font-medium touch-target">
      </div>

      <div class="grid grid-cols-2 gap-2.5">
        <div>
          <label class="block text-[11px] font-extrabold uppercase tracking-wider text-slate-500 mb-1">E-mail (RF01)</label>
          <input type="email" id="input-email" required value="aluno@cetep.edu.br" placeholder="seu@email.com"
            class="w-full px-3 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600 text-xs font-medium touch-target">
        </div>
        <div>
          <label class="block text-[11px] font-extrabold uppercase tracking-wider text-slate-500 mb-1">Turma (Código)</label>
          <input type="text" id="input-class" required value="INFO-3A" placeholder="INFO-3A"
            class="w-full px-3 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600 text-sm font-extrabold uppercase text-indigo-700 touch-target">
        </div>
      </div>

      <div>
        <div class="flex items-center justify-between mb-1">
          <label class="block text-[11px] font-extrabold uppercase tracking-wider text-slate-500">Senha de Acesso</label>
          <button type="button" onclick="recoverPassword()" class="text-[11px] font-bold text-indigo-600 hover:underline">
            Esqueceu a senha? (RF03)
          </button>
        </div>
        <input type="password" id="input-pass" required value="123456"
          class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600 text-sm touch-target">
      </div>

      <div>
        <label class="block text-[11px] font-extrabold uppercase tracking-wider text-slate-500 mb-1.5">Perfil de Atuação (RN01)</label>
        <div class="grid grid-cols-2 gap-2">
          <button type="button" id="role-aluno" onclick="selectLoginRole('Aluno')"
            class="py-2.5 px-3 rounded-xl border-2 border-indigo-600 bg-indigo-50 text-indigo-700 font-extrabold text-xs flex flex-col items-center gap-1 transition touch-target">
            <i data-lucide="graduation-cap" class="w-5 h-5"></i>
            <span>Estudante (Aluno)</span>
          </button>
          <button type="button" id="role-rep" onclick="selectLoginRole('Representante')"
            class="py-2.5 px-3 rounded-xl border-2 border-slate-200 text-slate-600 font-bold text-xs flex flex-col items-center gap-1 transition touch-target">
            <i data-lucide="shield-check" class="w-5 h-5"></i>
            <span>Representante</span>
          </button>
        </div>
      </div>

      <button type="submit" class="w-full py-3.5 bg-indigo-600 hover:bg-indigo-700 active:scale-[0.99] text-white font-extrabold rounded-xl shadow-lg shadow-indigo-600/30 transition flex items-center justify-center gap-2 touch-target">
        <span>Acessar Organizaê</span>
        <i data-lucide="arrow-right" class="w-4 h-4"></i>
      </button>
    </form>

    <p class="text-center text-[11px] text-indigo-200 mt-5">
      CETEP Araci • Curso Técnico em Informática • 2026
    </p>
  </section>

  <!-- ================= ESTRUTURA PRINCIPAL DO APLICATIVO ================= -->
  <div id="main-app" class="hidden flex-1 flex flex-col h-full pb-20">

    <!-- Cabeçalho Superior Hierarquizado (RI01, RI02, RF31) -->
    <header class="bg-indigo-600 text-white px-4 pt-5 pb-4 rounded-b-3xl shadow-md">
      <div class="flex items-center justify-between mb-3">
        <div class="flex items-center gap-2.5">
          <div class="w-9 h-9 rounded-xl bg-white/15 flex items-center justify-center border border-white/20 shrink-0">
            <i data-lucide="check-circle" class="w-5 h-5 text-amber-400"></i>
          </div>
          <div>
            <div class="flex items-center gap-1.5">
              <span id="badge-turma" class="text-[10px] font-extrabold uppercase tracking-wider bg-indigo-800/80 px-2 py-0.5 rounded-md">INFO-3A</span>
              <span id="badge-reminder-header" class="text-[10px] font-bold bg-amber-500 text-slate-950 px-2 py-0.5 rounded-md flex items-center gap-1">
                <i data-lucide="bell" class="w-3 h-3"></i>
                <span id="reminder-label-top">Alerta: 24h</span>
              </span>
            </div>
            <h2 id="greeting-name" class="text-base font-extrabold leading-tight mt-0.5">Olá, Estudante</h2>
          </div>
        </div>

        <div class="flex items-center gap-1.5">
          <button onclick="toggleRoleQuick()" title="Alternar Perfil para Demonstração"
            class="text-[11px] bg-white/15 hover:bg-white/25 px-2.5 py-2 rounded-xl font-bold flex items-center gap-1 backdrop-blur-sm transition">
            <i data-lucide="repeat" class="w-3.5 h-3.5 text-amber-300"></i>
            <span id="header-role-label">Aluno</span>
          </button>
          <button onclick="logout()" title="Sair da Conta" class="p-2 bg-white/10 hover:bg-white/20 rounded-xl">
            <i data-lucide="log-out" class="w-4 h-4"></i>
          </button>
        </div>
      </div>

      <!-- Painel Resumo da Página Inicial (RF31) -->
      <div class="grid grid-cols-4 gap-1.5 bg-indigo-700/70 p-2.5 rounded-2xl text-center border border-indigo-500/30">
        <div>
          <p class="text-[10px] text-indigo-200 font-semibold">Pendentes</p>
          <p id="stat-pending" class="text-base font-extrabold">0</p>
        </div>
        <div class="border-x border-indigo-500/40">
          <p class="text-[10px] text-indigo-200 font-semibold">Críticas</p>
          <p id="stat-critical" class="text-base font-extrabold text-rose-300">0</p>
        </div>
        <div class="border-r border-indigo-500/40">
          <p class="text-[10px] text-indigo-200 font-semibold">Ciclos Foco</p>
          <p id="stat-pomodoros" class="text-base font-extrabold text-amber-300">0</p>
        </div>
        <div>
          <p class="text-[10px] text-indigo-200 font-semibold">Média Geral</p>
          <p id="stat-avg" class="text-base font-extrabold text-emerald-300">--</p>
        </div>
      </div>
    </header>

    <!-- ================= T02: ABA 1 — ATIVIDADES E MATRIZ DE PRIORIDADES ================= -->
    <main id="tab-mural" class="flex-1 px-4 pt-3.5 overflow-y-auto space-y-3 hide-scroll">

      <!-- Banner de Lembretes Automáticos de Prazo (RF26, RF28) -->
      <div id="urgent-banner" class="hidden bg-amber-50 border border-amber-300 rounded-2xl p-3 flex items-center justify-between gap-2">
        <div class="flex items-center gap-2">
          <i data-lucide="bell-ring" class="w-4 h-4 text-amber-600 shrink-0"></i>
          <p id="urgent-banner-text" class="text-xs font-bold text-amber-900"></p>
        </div>
        <span class="text-[10px] font-extrabold uppercase bg-amber-200 text-amber-900 px-2 py-0.5 rounded-md shrink-0">RF28</span>
      </div>

      <!-- Barra de Pesquisa e Botão Nova Tarefa (RF07, RF20) -->
      <div class="flex gap-2">
        <div class="relative flex-1">
          <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3 top-1/2 -translate-y-1/2"></i>
          <input type="text" id="search-input" oninput="renderTasks()" placeholder="Pesquisar tarefa ou matéria... (RF20)"
            class="w-full pl-9 pr-3 py-2.5 bg-white rounded-xl border border-slate-200 text-xs font-medium focus:outline-none focus:ring-2 focus:ring-indigo-600 touch-target">
        </div>
        <button onclick="openTaskModal()" class="bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-extrabold px-3.5 py-2.5 rounded-xl shadow flex items-center gap-1.5 shrink-0 transition touch-target">
          <i data-lucide="plus" class="w-4 h-4"></i>
          <span id="btn-new-task-label">Nova</span>
        </button>
      </div>

      <!-- Filtros e Ordenação (RF17, RF18, RF21, RF22) -->
      <div class="flex items-center justify-between gap-2">
        <div class="flex gap-1.5 overflow-x-auto pb-1 hide-scroll">
          <button onclick="setFilter('all')" id="filter-all" class="px-2.5 py-1.5 rounded-lg text-[11px] font-extrabold bg-slate-900 text-white shrink-0">Pendentes</button>
          <button onclick="setFilter('critical')" id="filter-critical" class="px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-rose-100 text-rose-800 shrink-0">Críticas</button>
          <button onclick="setFilter('turma')" id="filter-turma" class="px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-slate-200 text-slate-700 shrink-0">Turma</button>
          <button onclick="setFilter('pessoal')" id="filter-pessoal" class="px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-slate-200 text-slate-700 shrink-0">Pessoais</button>
          <button onclick="setFilter('done')" id="filter-done" class="px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-slate-200 text-slate-700 shrink-0">Concluídas (RF18)</button>
        </div>

        <select id="sort-select" onchange="renderTasks()" title="Ordenar Atividades (RF22)"
          class="bg-white border border-slate-200 rounded-lg px-2 py-1.5 text-[11px] font-bold text-slate-700 shrink-0">
          <option value="priority">Matriz Prioridade</option>
          <option value="date">Data Entrega</option>
          <option value="score">Pontuação</option>
          <option value="subject">Disciplina</option>
        </select>
      </div>

      <!-- Lista de Cartões de Atividades -->
      <div id="tasks-container" class="space-y-3 pb-6"></div>
    </main>

    <!-- ================= T04: ABA 2 — TEMPORIZADOR DE FOCO POMODORO (RF25, RN06) ================= -->
    <main id="tab-foco" class="hidden flex-1 px-5 pt-4 overflow-y-auto flex flex-col items-center justify-between pb-6">
      <div class="w-full text-center space-y-2">
        <span id="pomo-mode-badge" class="inline-block px-3 py-1 rounded-full text-[11px] font-extrabold uppercase tracking-wider bg-indigo-100 text-indigo-700">
          Ciclo de Foco • 25 min
        </span>
        <div>
          <label class="block text-xs font-bold text-slate-500">Vinculado à Atividade (RF25):</label>
          <select id="pomo-task-select" onchange="selectPomoTask(this.value)"
            class="mt-1 w-full bg-white border border-slate-200 rounded-xl px-3 py-2.5 text-xs font-bold text-slate-800 focus:outline-none focus:ring-2 focus:ring-indigo-600 touch-target">
          </select>
        </div>
      </div>

      <!-- Mostrador Circular Pomodoro -->
      <div class="my-3 flex flex-col items-center">
        <div class="w-56 h-56 rounded-full border-[10px] border-indigo-600 bg-white shadow-xl flex flex-col items-center justify-center relative">
          <span id="pomo-timer-display" class="text-5xl font-extrabold tracking-tight text-slate-900">25:00</span>
          <span id="pomo-status-text" class="text-xs font-bold text-slate-400 mt-1.5">Pronto para iniciar</span>
        </div>
      </div>

      <!-- Botões de Ação e Simulador para Banca -->
      <div class="w-full space-y-3">
        <div class="grid grid-cols-2 gap-3">
          <button id="btn-pomo-toggle" onclick="togglePomodoro()"
            class="py-3.5 bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold rounded-2xl shadow-lg flex items-center justify-center gap-2 transition touch-target">
            <i data-lucide="play" class="w-5 h-5"></i>
            <span id="btn-pomo-label">Iniciar Foco</span>
          </button>
          <button onclick="resetPomodoro()"
            class="py-3.5 bg-slate-200 hover:bg-slate-300 text-slate-800 font-extrabold rounded-2xl flex items-center justify-center gap-2 transition touch-target">
            <i data-lucide="rotate-ccw" class="w-5 h-5"></i>
            <span>Reiniciar</span>
          </button>
        </div>

        <div class="bg-amber-50 border border-amber-300 rounded-2xl p-3 flex items-center justify-between">
          <div class="text-xs text-amber-950">
            <p class="font-extrabold">Simulador Ao Vivo (Banca TCC)</p>
            <p class="text-[11px] text-amber-800">Testa o término em 00:00 (RN06) em 5 segundos.</p>
          </div>
          <button onclick="startDemoPomodoro()" class="bg-amber-500 hover:bg-amber-600 text-slate-950 text-xs font-extrabold px-3 py-2 rounded-xl shrink-0 touch-target">
            Simular 5s
          </button>
        </div>
      </div>
    </main>

    <!-- ================= T05: ABA 3 — DISCIPLINAS, NOTAS, MÉDIAS E CALENDÁRIO ================= -->
    <main id="tab-notas" class="hidden flex-1 px-4 pt-4 overflow-y-auto space-y-4 pb-6 hide-scroll">

      <!-- Seção 1: Desempenho Escolar e Médias por Disciplina (RF04-RF06, RF29, RF30, RN04, RN07) -->
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-3">
        <div class="flex items-center justify-between">
          <div>
            <h3 class="text-xs font-extrabold uppercase tracking-wider text-slate-800">Disciplinas & Médias (RF30)</h3>
            <p class="text-[11px] text-slate-500">Cálculo automático das atividades avaliadas (RN07)</p>
          </div>
        </div>

        <!-- Formulário Rápido para Cadastrar Disciplina (RF04) -->
        <form onsubmit="addDiscipline(event)" class="flex gap-1.5">
          <input type="text" id="new-disc-name" required placeholder="Nova disciplina (Ex.: Programação Web)"
            class="flex-1 px-3 py-2 text-xs rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600">
          <input type="color" id="new-disc-color" value="#4F46E5" class="w-10 h-9 rounded-xl border border-slate-200 p-1 bg-white cursor-pointer">
          <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-extrabold px-3 py-2 rounded-xl shrink-0">
            + Matéria
          </button>
        </form>

        <div id="disciplines-container" class="space-y-2"></div>
      </div>

      <!-- Seção 2: Registro de Notas por Atividade Avaliativa (RF29, RN07) -->
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-2.5">
        <h3 class="text-xs font-extrabold uppercase tracking-wider text-slate-800">Lançar Notas Obtidas (RF29 / RN07)</h3>
        <p class="text-[11px] text-slate-500">Informe sua nota (0 até a pontuação máxima da atividade):</p>
        <div id="grades-list-container" class="space-y-2"></div>
      </div>

      <!-- Seção 3: Calendário / Agenda Cronológica de Entregas (RF23) e Lembretes (RF26) -->
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-3">
        <div class="flex items-center justify-between">
          <h3 class="text-xs font-extrabold uppercase tracking-wider text-slate-800">Calendário de Entregas (RF23)</h3>
          <select id="reminder-config" onchange="updateReminderSetting(this.value)"
            class="text-[11px] font-bold bg-indigo-50 text-indigo-700 border border-indigo-200 rounded-lg px-2 py-1">
            <option value="1">Lembrete: 24h antes (RF26)</option>
            <option value="3" selected>Lembrete: 3 dias antes</option>
            <option value="7">Lembrete: 7 dias antes</option>
          </select>
        </div>
        <div id="calendar-container" class="space-y-2"></div>
      </div>

    </main>

    <!-- Barra de Navegação Inferior Fixa (RNF01, RNF02 — Acesso em até 3 toques) -->
    <nav class="fixed bottom-0 left-1/2 -translate-x-1/2 w-full max-w-[430px] bg-white border-t border-slate-200 px-4 py-2 flex justify-around items-center z-20">
      <button onclick="switchTab('mural')" id="nav-mural" class="flex flex-col items-center gap-0.5 text-indigo-600 font-extrabold text-[11px] py-1 px-3">
        <i data-lucide="layout-list" class="w-5 h-5"></i>
        <span>Atividades</span>
      </button>
      <button onclick="switchTab('foco')" id="nav-foco" class="flex flex-col items-center gap-0.5 text-slate-400 font-bold text-[11px] py-1 px-3">
        <i data-lucide="timer" class="w-5 h-5"></i>
        <span>Modo Foco</span>
      </button>
      <button onclick="switchTab('notas')" id="nav-notas" class="flex flex-col items-center gap-0.5 text-slate-400 font-bold text-[11px] py-1 px-3">
        <i data-lucide="award" class="w-5 h-5"></i>
        <span>Notas & Agenda</span>
      </button>
    </nav>
  </div>

  <!-- ================= T03: MODAL DE CADASTRO / EDIÇÃO DE ATIVIDADE ================= -->
  <div id="task-modal" class="hidden fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white w-full max-w-[430px] rounded-t-3xl sm:rounded-3xl p-5 space-y-3 max-h-[92dvh] overflow-y-auto">
      <div class="flex items-center justify-between">
        <h3 id="modal-title-heading" class="text-base font-extrabold text-slate-900">Cadastrar Atividade</h3>
        <button onclick="closeTaskModal()" class="p-1.5 text-slate-400 hover:text-slate-600 rounded-lg">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <form id="task-form" class="space-y-3">
        <input type="hidden" id="edit-task-id" value="">

        <div>
          <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Visibilidade da Tarefa (RN01)</label>
          <select id="task-scope" class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-xs font-bold text-slate-800 touch-target">
            <option value="turma" id="opt-scope-turma">Mural Coletivo da Turma (Representante)</option>
            <option value="pessoal">Tarefa Particular (Apenas para mim)</option>
          </select>
          <p id="scope-helper" class="text-[10px] text-slate-500 mt-1"></p>
        </div>

        <div>
          <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Título da Atividade (RF07)</label>
          <input type="text" id="task-title" required placeholder="Ex.: Seminário de Redes de Computadores"
            class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 text-xs font-medium touch-target">
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Disciplina (RF10)</label>
            <select id="task-subject" required class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-xs font-bold touch-target">
            </select>
          </div>
          <div>
            <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Peso / Urgência (RF13)</label>
            <select id="task-weight" class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-xs font-bold touch-target">
              <option value="Alto">Alto (Prova / TCC)</option>
              <option value="Médio" selected>Médio (Trabalho)</option>
              <option value="Baixo">Baixo (Exercício)</option>
            </select>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-2">
          <div>
            <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Data Entrega (RN04)</label>
            <input type="date" id="task-date" required
              class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-xs font-bold touch-target">
          </div>
          <div>
            <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Nota Máxima (RF13)</label>
            <input type="number" id="task-max-score" step="0.5" min="1" max="100" value="10" required
              class="w-full px-3 py-2.5 rounded-xl border border-slate-200 text-xs font-bold touch-target">
          </div>
        </div>
        <p id="date-error" class="hidden text-[11px] text-rose-600 font-extrabold">
          Bloqueado (RN04): A data de entrega não pode ser anterior à data de hoje.
        </p>

        <div>
          <label class="block text-[11px] font-extrabold uppercase text-slate-500 mb-1">Descrição e Instruções (RF11)</label>
          <textarea id="task-desc" rows="2" placeholder="Instruções e materiais necessários..."
            class="w-full px-3.5 py-2 rounded-xl border border-slate-200 text-xs"></textarea>
        </div>

        <button type="submit" class="w-full py-3.5 bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold rounded-xl shadow-lg transition touch-target">
          Salvar Atividade
        </button>
      </form>
    </div>
  </div>

</div>

<script>
  // ================= CHAVES DE ARMAZENAMENTO PERSISTENTE (RNF10, RNF12) =================
  const STORAGE_KEY_USER = 'organizae_user_v2';
  const STORAGE_KEY_DISCIPLINES = 'organizae_disciplines_v2';
  const STORAGE_KEY_TASKS = 'organizae_tasks_v2';
  const STORAGE_KEY_PROGRESS = 'organizae_progress_v2';
  const STORAGE_KEY_REMINDER = 'organizae_reminder_days_v2';

  let currentUser = {
    name: '',
    email: '',
    classCode: 'INFO-3A',
    role: 'Aluno'
  };

  let currentFilter = 'all';
  let reminderDaysThreshold = 3;
  let disciplines = [];
  let tasks = [];
  let userProgress = {}; // Isolamento por estudante + tarefa (RN02)

  // Temporizador Pomodoro (RF25, RN06)
  let pomoInterval = null;
  let pomoSecondsLeft = 25 * 60;
  let pomoIsRunning = false;
  let pomoIsBreak = false;
  let selectedTaskIdForPomo = null;

  function getFutureDateStr(daysAhead) {
    const d = new Date();
    d.setDate(d.getDate() + daysAhead);
    return d.toISOString().split('T')[0];
  }

  function getDefaultDisciplines() {
    return [
      { id: 'd1', name: 'Eng. de Software', color: '#4F46E5' },
      { id: 'd2', name: 'Banco de Dados', color: '#10B981' },
      { id: 'd3', name: 'Redes de Computadores', color: '#F59E0B' }
    ];
  }

  function getInitialSampleTasks(classCode) {
    return [
      {
        id: 't1',
        classCode: classCode,
        scope: 'turma',
        title: 'Defesa e Documentação ABNT — Organizaê',
        subject: 'Eng. de Software',
        dueDate: getFutureDateStr(1),
        weight: 'Alto',
        maxScore: 10.0,
        description: 'Revisar Capítulos 1 a 9 da documentação e apresentar o protótipo PWA.'
      },
      {
        id: 't2',
        classCode: classCode,
        scope: 'turma',
        title: 'Script Físico SQL (DDL) e Dicionário de Dados',
        subject: 'Banco de Dados',
        dueDate: getFutureDateStr(4),
        weight: 'Médio',
        maxScore: 10.0,
        description: 'Criar tabelas normalizadas na 3FN para Turmas, Usuários e Atividades.'
      },
      {
        id: 't3',
        classCode: classCode,
        scope: 'turma',
        title: 'Resumo Camadas OSI e Protocolo HTTPS',
        subject: 'Redes de Computadores',
        dueDate: getFutureDateStr(9),
        weight: 'Baixo',
        maxScore: 10.0,
        description: 'Fichamento técnico sobre hospedagem em nuvem e segurança web.'
      }
    ];
  }

  // ================= INICIALIZAÇÃO =================
  window.addEventListener('DOMContentLoaded', () => {
    lucide.createIcons();
    loadDataFromStorage();

    const todayStr = getFutureDateStr(0);
    document.getElementById('task-date').setAttribute('min', todayStr);
    document.getElementById('task-date').value = getFutureDateStr(2);

    if (currentUser.name) {
      showMainApp();
    }
  });

  function loadDataFromStorage() {
    const savedUser = localStorage.getItem(STORAGE_KEY_USER);
    if (savedUser) currentUser = JSON.parse(savedUser);

    const savedDisc = localStorage.getItem(STORAGE_KEY_DISCIPLINES);
    if (savedDisc) {
      disciplines = JSON.parse(savedDisc);
    } else {
      disciplines = getDefaultDisciplines();
      saveDisciplines();
    }

    const savedTasks = localStorage.getItem(STORAGE_KEY_TASKS);
    if (savedTasks) {
      tasks = JSON.parse(savedTasks);
    } else {
      tasks = getInitialSampleTasks(currentUser.classCode || 'INFO-3A');
      saveTasks();
    }

    const savedProgress = localStorage.getItem(STORAGE_KEY_PROGRESS);
    if (savedProgress) userProgress = JSON.parse(savedProgress);

    const savedRem = localStorage.getItem(STORAGE_KEY_REMINDER);
    if (savedRem) reminderDaysThreshold = parseInt(savedRem, 10);
  }

  function saveDisciplines() {
    localStorage.setItem(STORAGE_KEY_DISCIPLINES, JSON.stringify(disciplines));
  }

  function saveTasks() {
    localStorage.setItem(STORAGE_KEY_TASKS, JSON.stringify(tasks));
  }

  function saveProgress() {
    localStorage.setItem(STORAGE_KEY_PROGRESS, JSON.stringify(userProgress));
  }

  // Isolamento Individual do Progresso e Notas (RN02)
  function getMyTaskData(taskId) {
    const userKey = `${currentUser.name.trim().toLowerCase()}_${taskId}`;
    if (!userProgress[userKey]) {
      userProgress[userKey] = {
        completed: false,
        grade: null,
        subtasks: [],
        pomodoros: 0
      };
    }
    return userProgress[userKey];
  }

  // ================= CONTA, LOGIN E RECUPERAÇÃO DE SENHA (RF01-RF03, RN01) =================
  function selectLoginRole(role) {
    currentUser.role = role;
    const btnAluno = document.getElementById('role-aluno');
    const btnRep = document.getElementById('role-rep');

    if (role === 'Aluno') {
      btnAluno.className = 'py-2.5 px-3 rounded-xl border-2 border-indigo-600 bg-indigo-50 text-indigo-700 font-extrabold text-xs flex flex-col items-center gap-1 transition touch-target';
      btnRep.className = 'py-2.5 px-3 rounded-xl border-2 border-slate-200 text-slate-600 font-bold text-xs flex flex-col items-center gap-1 transition touch-target';
    } else {
      btnRep.className = 'py-2.5 px-3 rounded-xl border-2 border-indigo-600 bg-indigo-50 text-indigo-700 font-extrabold text-xs flex flex-col items-center gap-1 transition touch-target';
      btnAluno.className = 'py-2.5 px-3 rounded-xl border-2 border-slate-200 text-slate-600 font-bold text-xs flex flex-col items-center gap-1 transition touch-target';
    }
  }

  function recoverPassword() {
    const email = document.getElementById('input-email').value || 'seu e-mail cadastrado';
    alert(`Recuperação de Credenciais (RF03):\nUm link de redefinição de senha foi enviado para ${email}.`);
  }

  document.getElementById('login-form').addEventListener('submit', (e) => {
    e.preventDefault();
    currentUser.name = document.getElementById('input-name').value.trim();
    currentUser.email = document.getElementById('input-email').value.trim();
    currentUser.classCode = document.getElementById('input-class').value.trim().toUpperCase();
    localStorage.setItem(STORAGE_KEY_USER, JSON.stringify(currentUser));
    showMainApp();
  });

  function toggleRoleQuick() {
    currentUser.role = currentUser.role === 'Aluno' ? 'Representante' : 'Aluno';
    localStorage.setItem(STORAGE_KEY_USER, JSON.stringify(currentUser));
    updateHeaderUI();
    renderTasks();
  }

  function logout() {
    localStorage.removeItem(STORAGE_KEY_USER);
    document.getElementById('main-app').classList.add('hidden');
    document.getElementById('login-screen').classList.remove('hidden');
  }

  function showMainApp() {
    document.getElementById('login-screen').classList.add('hidden');
    document.getElementById('main-app').classList.remove('hidden');
    document.getElementById('reminder-config').value = String(reminderDaysThreshold);
    updateHeaderUI();
    populateSubjectSelect();
    renderTasks();
    renderDisciplinesAndGrades();
    populatePomoSelect();
  }

  function updateHeaderUI() {
    document.getElementById('badge-turma').textContent = `TURMA ${currentUser.classCode}`;
    document.getElementById('greeting-name').textContent = `Olá, ${currentUser.name}`;
    document.getElementById('header-role-label').textContent = currentUser.role;
    document.getElementById('btn-new-task-label').textContent =
      currentUser.role === 'Representante' ? 'Publicar' : 'Nova';
    document.getElementById('reminder-label-top').textContent =
      reminderDaysThreshold === 1 ? 'Alerta: 24h' : `Alerta: ${reminderDaysThreshold}d`;
  }

  // ================= MATRIZ DE PRIORIDADES E FÓRMULA MATEMÁTICA (RN03, RF19, RF22) =================
  function calculatePriority(dueDateStr, weight, maxScore = 10) {
    const today = new Date();
    today.setHours(0, 0, 0, 0);
    const due = new Date(dueDateStr + 'T00:00:00');
    const diffTime = due - today;
    const daysLeft = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

    // Fórmula documentada na Seção 1.2.2 do TCC: Prioridade = Pontuação / ((DataEntrega - DataAtual) + 1)
    const weightMultiplier = weight === 'Alto' ? 1.5 : (weight === 'Médio' ? 1.0 : 0.7);
    const denominator = Math.max(1, daysLeft + 1);
    const mathIndex = ((maxScore * weightMultiplier) / denominator).toFixed(1);

    let deadlineLabel = `Em ${daysLeft} dias`;
    if (daysLeft < 0) deadlineLabel = `Atrasada (${Math.abs(daysLeft)}d)`;
    else if (daysLeft === 0) deadlineLabel = 'Vence Hoje!';
    else if (daysLeft === 1) deadlineLabel = 'Vence Amanhã';
    else if (daysLeft <= 3) deadlineLabel = `Em até 3 dias (${daysLeft}d)`;

    // Faixas Semafóricas RN03
    if (daysLeft <= 2 || (daysLeft <= 5 && weight === 'Alto')) {
      return {
        level: 'Crítica',
        rank: 1,
        daysLeft,
        mathIndex,
        deadlineLabel,
        badgeClass: 'bg-rose-100 text-rose-800 border-rose-300',
        borderClass: 'border-l-4 border-l-rose-500'
      };
    }
    if (daysLeft <= 7) {
      return {
        level: 'Moderada',
        rank: 2,
        daysLeft,
        mathIndex,
        deadlineLabel,
        badgeClass: 'bg-amber-100 text-amber-800 border-amber-300',
        borderClass: 'border-l-4 border-l-amber-500'
      };
    }
    return {
      level: 'Planejada',
      rank: 3,
      daysLeft,
      mathIndex,
      deadlineLabel,
      badgeClass: 'bg-emerald-100 text-emerald-800 border-emerald-300',
      borderClass: 'border-l-4 border-l-emerald-500'
    };
  }

  // ================= LISTAGEM, PESQUISA, FILTROS E MICROTAREFAS =================
  function setFilter(filter) {
    currentFilter = filter;
    ['all', 'critical', 'turma', 'pessoal', 'done'].forEach(f => {
      const btn = document.getElementById(`filter-${f}`);
      if (!btn) return;
      if (f === filter) {
        btn.className = 'px-2.5 py-1.5 rounded-lg text-[11px] font-extrabold bg-slate-900 text-white shrink-0';
      } else {
        btn.className = f === 'critical'
          ? 'px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-rose-100 text-rose-800 shrink-0'
          : 'px-2.5 py-1.5 rounded-lg text-[11px] font-bold bg-slate-200 text-slate-700 shrink-0';
      }
    });
    renderTasks();
  }

  function getVisibleTasks() {
    return tasks.filter(t => {
      if (t.scope === 'turma') return t.classCode === currentUser.classCode;
      return t.owner === currentUser.name;
    }).map(t => ({
      ...t,
      priority: calculatePriority(t.dueDate, t.weight, t.maxScore || 10)
    }));
  }

  function renderTasks() {
    const container = document.getElementById('tasks-container');
    container.innerHTML = '';

    const searchQuery = (document.getElementById('search-input')?.value || '').trim().toLowerCase();
    const sortBy = document.getElementById('sort-select')?.value || 'priority';

    let visibleTasks = getVisibleTasks();

    // Atualiza contadores do Painel Inicial (RF31)
    let pendingCount = 0;
    let criticalCount = 0;
    let totalPomos = 0;
    let reminderCount = 0;

    visibleTasks.forEach(t => {
      const myData = getMyTaskData(t.id);
      totalPomos += myData.pomodoros || 0;
      if (!myData.completed) {
        pendingCount++;
        if (t.priority.level === 'Crítica') criticalCount++;
        if (t.priority.daysLeft >= 0 && t.priority.daysLeft <= reminderDaysThreshold) {
          reminderCount++;
        }
      }
    });

    document.getElementById('stat-pending').textContent = pendingCount;
    document.getElementById('stat-critical').textContent = criticalCount;
    document.getElementById('stat-pomodoros').textContent = totalPomos;
    updateOverallAverageDisplay();

    // Banner de Notificação / Lembrete Ativo (RF26, RF28)
    const banner = document.getElementById('urgent-banner');
    if (reminderCount > 0) {
      banner.classList.remove('hidden');
      document.getElementById('urgent-banner-text').textContent =
        `Você tem ${reminderCount} atividade(s) vencendo nos próximos ${reminderDaysThreshold} dia(s)!`;
    } else {
      banner.classList.add('hidden');
    }

    // Ordenação selecionada (RF22)
    visibleTasks.sort((a, b) => {
      if (sortBy === 'date') return a.priority.daysLeft - b.priority.daysLeft;
      if (sortBy === 'score') return (b.maxScore || 10) - (a.maxScore || 10);
      if (sortBy === 'subject') return a.subject.localeCompare(b.subject);
      // Padrão: Matriz de Prioridade (RN03)
      if (a.priority.rank !== b.priority.rank) return a.priority.rank - b.priority.rank;
      return b.priority.mathIndex - a.priority.mathIndex;
    });

    // Aplicação de Filtros e Busca por Palavra-Chave (RF17, RF18, RF20, RF21)
    const filtered = visibleTasks.filter(t => {
      const myData = getMyTaskData(t.id);
      if (searchQuery && !t.title.toLowerCase().includes(searchQuery) && !t.subject.toLowerCase().includes(searchQuery)) {
        return false;
      }
      if (currentFilter === 'done') return myData.completed;
      if (myData.completed) return false; // Nas demais abas exibe as pendentes (RF17)
      if (currentFilter === 'critical') return t.priority.level === 'Crítica';
      if (currentFilter === 'turma') return t.scope === 'turma';
      if (currentFilter === 'pessoal') return t.scope === 'pessoal';
      return true;
    });

    if (filtered.length === 0) {
      container.innerHTML = `
        <div class="bg-white rounded-2xl p-7 text-center border border-slate-200">
          <p class="text-xs font-extrabold text-slate-700">Nenhuma atividade encontrada neste filtro.</p>
          <p class="text-[11px] text-slate-400 mt-1">Use o botão "+ Nova" para cadastrar ou altere o filtro acima.</p>
        </div>`;
      return;
    }

    filtered.forEach(task => {
      const myData = getMyTaskData(task.id);
      const totalSub = myData.subtasks.length;
      const doneSub = myData.subtasks.filter(s => s.done).length;
      const progressPct = myData.completed ? 100 : (totalSub === 0 ? 0 : Math.round((doneSub / totalSub) * 100));

      const canModify = (task.scope === 'turma' && currentUser.role === 'Representante') || task.scope === 'pessoal';

      const subtasksHTML = myData.subtasks.map((sub, idx) => `
        <label class="flex items-center justify-between gap-2 p-2 rounded-xl bg-slate-50 hover:bg-slate-100 cursor-pointer transition">
          <div class="flex items-center gap-2 flex-1">
            <input type="checkbox" ${sub.done ? 'checked' : ''} onchange="toggleSubtask('${task.id}', ${idx})"
              class="w-4 h-4 rounded text-indigo-600 focus:ring-indigo-500">
            <span class="text-xs font-medium ${sub.done ? 'line-through text-slate-400' : 'text-slate-700'}">${sub.text}</span>
          </div>
          <button onclick="removeSubtask('${task.id}', ${idx})" class="text-slate-300 hover:text-rose-500 p-1">
            <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
          </button>
        </label>
      `).join('');

      // Botão de Desbloqueio Mental (RN05 / RF24)
      const rn05ButtonHTML = (totalSub === 0 && !myData.completed) ? `
        <button onclick="suggestInitialSteps('${task.id}')"
          class="w-full mt-1.5 py-2.5 px-3 rounded-xl bg-indigo-50 hover:bg-indigo-100 text-indigo-700 border border-indigo-200 text-xs font-extrabold flex items-center justify-center gap-1.5 transition touch-target">
          <i data-lucide="sparkles" class="w-4 h-4 text-amber-500"></i>
          <span>Não sabe por onde começar? Sugerir passos iniciais</span>
        </button>
      ` : '';

      const card = document.createElement('div');
      card.className = `bg-white rounded-2xl p-4 shadow-sm border border-slate-200 ${task.priority.borderClass} space-y-2.5`;
      card.innerHTML = `
        <div class="flex items-start justify-between gap-2">
          <div class="flex flex-wrap items-center gap-1">
            <span class="px-2 py-0.5 text-[10px] font-extrabold uppercase rounded-md border ${task.priority.badgeClass}">
              ${task.priority.level} • Índice ${task.priority.mathIndex}
            </span>
            <span class="px-2 py-0.5 text-[10px] font-bold rounded-md bg-slate-100 text-slate-700">
              ${task.subject} (${task.maxScore || 10} pts)
            </span>
            <span class="px-2 py-0.5 text-[10px] font-bold rounded-md ${task.scope === 'turma' ? 'bg-indigo-50 text-indigo-700' : 'bg-purple-50 text-purple-700'}">
              ${task.scope === 'turma' ? 'Turma' : 'Particular'}
            </span>
          </div>

          <div class="flex items-center gap-1">
            <!-- Concluir ou Reabrir Atividade (RF14, RF15) -->
            <button onclick="toggleTaskCompletion('${task.id}')" title="${myData.completed ? 'Reabrir Atividade (RF15)' : 'Concluir Atividade (RF14)'}"
              class="text-[11px] font-extrabold px-2 py-1 rounded-lg ${myData.completed ? 'bg-amber-100 text-amber-800' : 'bg-emerald-100 text-emerald-800'}">
              ${myData.completed ? 'Reabrir' : '✔ Concluir'}
            </button>
            ${canModify ? `
              <button onclick="openEditTaskModal('${task.id}')" title="Editar (RF08)" class="p-1 text-slate-400 hover:text-indigo-600">
                <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
              </button>
              <button onclick="deleteTask('${task.id}')" title="Excluir (RF09)" class="p-1 text-slate-400 hover:text-rose-600">
                <i data-lucide="trash" class="w-3.5 h-3.5"></i>
              </button>
            ` : ''}
          </div>
        </div>

        <div>
          <h4 class="text-sm font-extrabold ${myData.completed ? 'line-through text-slate-400' : 'text-slate-900'}">${task.title}</h4>
          <p class="text-xs text-slate-500 mt-0.5">${task.description || 'Sem instruções adicionais.'}</p>
        </div>

        <div class="flex items-center justify-between text-xs text-slate-700 bg-slate-50 px-3 py-2 rounded-xl">
          <span class="font-bold flex items-center gap-1.5">
            <i data-lucide="calendar" class="w-3.5 h-3.5 text-indigo-600"></i>
            ${task.priority.deadlineLabel} • Peso ${task.weight}
          </span>
          <button onclick="startFocusOnTask('${task.id}')" class="text-indigo-600 hover:text-indigo-800 font-extrabold flex items-center gap-1">
            <i data-lucide="play-circle" class="w-4 h-4"></i>
            Focar (${myData.pomodoros || 0})
          </button>
        </div>

        <!-- Barra de Progresso Individual (RF16 e RN02) -->
        <div>
          <div class="flex justify-between text-[11px] font-bold text-slate-500 mb-1">
            <span>Progresso Individual (Checklist)</span>
            <span>${progressPct}%</span>
          </div>
          <div class="w-full h-2 bg-slate-100 rounded-full overflow-hidden">
            <div class="h-full bg-indigo-600 transition-all duration-300" style="width: ${progressPct}%"></div>
          </div>
        </div>

        <!-- Microtarefas (RF16 e RN05) -->
        <div class="space-y-1.5 pt-1">
          ${subtasksHTML}
          ${rn05ButtonHTML}
          <form onsubmit="addSubtask(event, '${task.id}')" class="flex gap-1.5 pt-1">
            <input type="text" id="sub-input-${task.id}" required placeholder="Dividir em microtarefa (RF16)..."
              class="flex-1 px-3 py-1.5 text-xs rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-600">
            <button type="submit" class="bg-slate-900 hover:bg-slate-800 text-white text-xs font-extrabold px-3 py-1.5 rounded-xl">
              + Etapa
            </button>
          </form>
        </div>
      `;
      container.appendChild(card);
    });

    lucide.createIcons();
  }

  // ================= CONCLUSÃO, REABERTURA E MICROTAREFAS (RF14-RF16, RN05) =================
  function toggleTaskCompletion(taskId) {
    const myData = getMyTaskData(taskId);
    myData.completed = !myData.completed;
    saveProgress();
    renderTasks();
  }

  function suggestInitialSteps(taskId) {
    const myData = getMyTaskData(taskId);
    myData.subtasks = [
      { text: '1. Ler instruções da atividade e separar materiais de apoio', done: false },
      { text: '2. Desenvolver o rascunho ou resolução principal', done: false },
      { text: '3. Revisar o conteúdo final e realizar a entrega', done: false }
    ];
    saveProgress();
    renderTasks();
  }

  function addSubtask(event, taskId) {
    event.preventDefault();
    const input = document.getElementById(`sub-input-${taskId}`);
    const text = input.value.trim();
    if (!text) return;

    const myData = getMyTaskData(taskId);
    myData.subtasks.push({ text, done: false });
    input.value = '';
    saveProgress();
    renderTasks();
  }

  function toggleSubtask(taskId, index) {
    const myData = getMyTaskData(taskId);
    myData.subtasks[index].done = !myData.subtasks[index].done;
    saveProgress();
    renderTasks();
  }

  function removeSubtask(taskId, index) {
    const myData = getMyTaskData(taskId);
    myData.subtasks.splice(index, 1);
    saveProgress();
    renderTasks();
  }

  // ================= CADASTRO, EDIÇÃO E EXCLUSÃO DE ATIVIDADES (RF07-RF13, RN01, RN04) =================
  function populateSubjectSelect() {
    const select = document.getElementById('task-subject');
    if (!select) return;
    select.innerHTML = disciplines.map(d => `<option value="${d.name}">${d.name}</option>`).join('');
  }

  function openTaskModal() {
    document.getElementById('edit-task-id').value = '';
    document.getElementById('modal-title-heading').textContent = 'Cadastrar Atividade';
    document.getElementById('task-form').reset();
    document.getElementById('task-date').value = getFutureDateStr(2);
    document.getElementById('task-max-score').value = 10;
    populateSubjectSelect();

    const scopeSelect = document.getElementById('task-scope');
    const optTurma = document.getElementById('opt-scope-turma');
    const helper = document.getElementById('scope-helper');

    if (currentUser.role === 'Representante') {
      optTurma.disabled = false;
      scopeSelect.value = 'turma';
      helper.textContent = 'Perfil Representante: publicação habilitada para toda a turma (RN01).';
    } else {
      optTurma.disabled = true;
      scopeSelect.value = 'pessoal';
      helper.textContent = 'Perfil Aluno: criando tarefa particular (RN01).';
    }

    document.getElementById('date-error').classList.add('hidden');
    document.getElementById('task-modal').classList.remove('hidden');
  }

  function openEditTaskModal(taskId) {
    const task = tasks.find(t => t.id === taskId);
    if (!task) return;
    populateSubjectSelect();

    document.getElementById('edit-task-id').value = task.id;
    document.getElementById('modal-title-heading').textContent = 'Editar Atividade (RF08)';
    document.getElementById('task-scope').value = task.scope;
    document.getElementById('task-title').value = task.title;
    document.getElementById('task-subject').value = task.subject;
    document.getElementById('task-weight').value = task.weight;
    document.getElementById('task-date').value = task.dueDate;
    document.getElementById('task-max-score').value = task.maxScore || 10;
    document.getElementById('task-desc').value = task.description || '';
    document.getElementById('date-error').classList.add('hidden');
    document.getElementById('task-modal').classList.remove('hidden');
  }

  function closeTaskModal() {
    document.getElementById('task-modal').classList.add('hidden');
  }

  document.getElementById('task-form').addEventListener('submit', (e) => {
    e.preventDefault();
    const dueDate = document.getElementById('task-date').value;
    const todayStr = getFutureDateStr(0);

    if (dueDate < todayStr) {
      document.getElementById('date-error').classList.remove('hidden');
      return;
    }

    const scope = document.getElementById('task-scope').value;
    if (scope === 'turma' && currentUser.role !== 'Representante') {
      alert('Bloqueado (RN01): Apenas Representantes podem publicar no mural da turma.');
      return;
    }

    const editId = document.getElementById('edit-task-id').value;
    const payload = {
      classCode: currentUser.classCode,
      scope: scope,
      owner: currentUser.name,
      title: document.getElementById('task-title').value.trim(),
      subject: document.getElementById('task-subject').value,
      weight: document.getElementById('task-weight').value,
      dueDate: dueDate,
      maxScore: parseFloat(document.getElementById('task-max-score').value) || 10.0,
      description: document.getElementById('task-desc').value.trim()
    };

    if (editId) {
      const idx = tasks.findIndex(t => t.id === editId);
      if (idx > -1) tasks[idx] = { ...tasks[idx], ...payload };
    } else {
      tasks.push({ id: 'task_' + Date.now(), ...payload });
    }

    saveTasks();
    closeTaskModal();
    renderTasks();
    renderDisciplinesAndGrades();
    populatePomoSelect();
  });

  function deleteTask(taskId) {
    if (!confirm('Confirma a exclusão desta atividade? (RF09)')) return;
    tasks = tasks.filter(t => t.id !== taskId);
    saveTasks();
    renderTasks();
    renderDisciplinesAndGrades();
    populatePomoSelect();
  }

  // ================= DISCIPLINAS, NOTAS, MÉDIAS E CALENDÁRIO (T05) =================
  function addDiscipline(event) {
    event.preventDefault();
    const nameInput = document.getElementById('new-disc-name');
    const colorInput = document.getElementById('new-disc-color');
    const name = nameInput.value.trim();
    if (!name) return;

    disciplines.push({
      id: 'disc_' + Date.now(),
      name: name,
      color: colorInput.value
    });
    nameInput.value = '';
    saveDisciplines();
    populateSubjectSelect();
    renderDisciplinesAndGrades();
  }

  // Regra RN04: Impede excluir disciplina que possua tarefas ativas
  function deleteDiscipline(discId) {
    const disc = disciplines.find(d => d.id === discId);
    if (!disc) return;
    const hasActiveTasks = tasks.some(t => t.subject === disc.name);
    if (hasActiveTasks) {
      alert(`Bloqueado (RN04): A disciplina "${disc.name}" possui atividades vinculadas. Remova ou transfira as atividades antes de excluir a disciplina.`);
      return;
    }
    disciplines = disciplines.filter(d => d.id !== discId);
    saveDisciplines();
    populateSubjectSelect();
    renderDisciplinesAndGrades();
  }

  // Regra RN07: Valida limite de nota (0 <= nota <= maxScore) e calcula média
  function saveGrade(taskId, maxScore) {
    const input = document.getElementById(`grade-input-${taskId}`);
    const valStr = input.value.trim();
    const myData = getMyTaskData(taskId);

    if (valStr === '') {
      myData.grade = null;
      saveProgress();
      renderDisciplinesAndGrades();
      updateOverallAverageDisplay();
      return;
    }

    const val = parseFloat(valStr);
    if (isNaN(val) || val < 0 || val > maxScore) {
      alert(`Nota Inválida (RN07): Informe um valor entre 0 e a nota máxima da atividade (${maxScore} pts).`);
      input.value = myData.grade !== null ? myData.grade : '';
      return;
    }

    myData.grade = val;
    saveProgress();
    renderDisciplinesAndGrades();
    updateOverallAverageDisplay();
  }

  function updateOverallAverageDisplay() {
    const visible = getVisibleTasks();
    const graded = visible.map(t => getMyTaskData(t.id).grade).filter(g => g !== null && g !== undefined);
    const avgEl = document.getElementById('stat-avg');
    if (graded.length === 0) {
      avgEl.textContent = '--';
    } else {
      const avg = graded.reduce((acc, v) => acc + v, 0) / graded.length;
      avgEl.textContent = avg.toFixed(1);
    }
  }

  function updateReminderSetting(val) {
    reminderDaysThreshold = parseInt(val, 10) || 3;
    localStorage.setItem(STORAGE_KEY_REMINDER, String(reminderDaysThreshold));
    updateHeaderUI();
    renderTasks();
  }

  function renderDisciplinesAndGrades() {
    const discContainer = document.getElementById('disciplines-container');
    const gradesContainer = document.getElementById('grades-list-container');
    const calContainer = document.getElementById('calendar-container');
    if (!discContainer) return;

    const visible = getVisibleTasks();

    // 1. Renderiza Disciplinas e Médias (RF04-RF06, RF30)
    discContainer.innerHTML = disciplines.map(d => {
      const discTasks = visible.filter(t => t.subject === d.name);
      const grades = discTasks.map(t => getMyTaskData(t.id).grade).filter(g => g !== null && g !== undefined);
      const avgText = grades.length > 0
        ? (grades.reduce((a, b) => a + b, 0) / grades.length).toFixed(1)
        : 'Sem notas';

      return `
        <div class="flex items-center justify-between p-2.5 rounded-xl bg-slate-50 border border-slate-200">
          <div class="flex items-center gap-2">
            <span class="w-3 h-3 rounded-full shrink-0" style="background-color: ${d.color}"></span>
            <div>
              <p class="text-xs font-extrabold text-slate-800">${d.name}</p>
              <p class="text-[10px] text-slate-500">${discTasks.length} atividade(s) vinculada(s)</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <span class="px-2 py-1 rounded-lg bg-indigo-50 text-indigo-700 text-xs font-extrabold">
              Média: ${avgText}
            </span>
            <button onclick="deleteDiscipline('${d.id}')" title="Excluir Disciplina (RF06)" class="text-slate-300 hover:text-rose-600 p-1">
              <i data-lucide="trash-2" class="w-4 h-4"></i>
            </button>
          </div>
        </div>
      `;
    }).join('');

    // 2. Renderiza Lançamento de Notas (RF29, RN07)
    gradesContainer.innerHTML = visible.map(t => {
      const myData = getMyTaskData(t.id);
      const maxScore = t.maxScore || 10;
      return `
        <div class="flex items-center justify-between gap-2 p-2.5 rounded-xl bg-slate-50 border border-slate-200">
          <div class="flex-1">
            <p class="text-xs font-bold text-slate-800">${t.title}</p>
            <p class="text-[10px] text-slate-500">${t.subject} • Nota Máx: ${maxScore} pts</p>
          </div>
          <div class="flex items-center gap-1.5">
            <input type="number" id="grade-input-${t.id}" step="0.1" min="0" max="${maxScore}"
              value="${myData.grade !== null && myData.grade !== undefined ? myData.grade : ''}"
              placeholder="Nota"
              class="w-16 px-2 py-1.5 text-xs font-extrabold text-center rounded-lg border border-slate-300">
            <button onclick="saveGrade('${t.id}', ${maxScore})"
              class="bg-emerald-600 hover:bg-emerald-700 text-white text-[11px] font-extrabold px-2.5 py-1.5 rounded-lg">
              Salvar
            </button>
          </div>
        </div>
      `;
    }).join('');

    // 3. Renderiza Calendário Cronológico de Entregas (RF23)
    const sortedByDate = [...visible].sort((a, b) => a.priority.daysLeft - b.priority.daysLeft);
    calContainer.innerHTML = sortedByDate.map(t => `
      <div class="flex items-center justify-between p-2.5 rounded-xl bg-slate-50 border border-slate-200">
        <div class="flex items-center gap-2.5">
          <div class="bg-indigo-600 text-white rounded-xl px-2.5 py-1 text-center shrink-0">
            <p class="text-[10px] font-bold uppercase">${t.dueDate.split('-').reverse().slice(0, 2).join('/')}</p>
          </div>
          <div>
            <p class="text-xs font-bold text-slate-800">${t.title}</p>
            <p class="text-[10px] text-slate-500">${t.subject} • ${t.priority.deadlineLabel}</p>
          </div>
        </div>
        <span class="px-2 py-0.5 text-[10px] font-extrabold rounded-md border ${t.priority.badgeClass}">
          ${t.priority.level}
        </span>
      </div>
    `).join('');

    lucide.createIcons();
  }

  // ================= NAVEGAÇÃO ENTRE ABAS E POMODORO (RNF02, RF25, RN06) =================
  function switchTab(tab) {
    ['mural', 'foco', 'notas'].forEach(t => {
      const mainEl = document.getElementById(`tab-${t}`);
      const navEl = document.getElementById(`nav-${t}`);
      if (t === tab) {
        mainEl.classList.remove('hidden');
        navEl.className = 'flex flex-col items-center gap-0.5 text-indigo-600 font-extrabold text-[11px] py-1 px-3';
      } else {
        mainEl.classList.add('hidden');
        navEl.className = 'flex flex-col items-center gap-0.5 text-slate-400 font-bold text-[11px] py-1 px-3';
      }
    });

    if (tab === 'mural') renderTasks();
    if (tab === 'foco') populatePomoSelect();
    if (tab === 'notas') renderDisciplinesAndGrades();
  }

  function populatePomoSelect() {
    const select = document.getElementById('pomo-task-select');
    const myTasks = getVisibleTasks();
    select.innerHTML = myTasks.map(t => `<option value="${t.id}">${t.title} (${t.subject})</option>`).join('');
    if (selectedTaskIdForPomo && myTasks.some(t => t.id === selectedTaskIdForPomo)) {
      select.value = selectedTaskIdForPomo;
    } else if (myTasks.length > 0) {
      selectedTaskIdForPomo = myTasks[0].id;
    }
  }

  function selectPomoTask(taskId) {
    selectedTaskIdForPomo = taskId;
  }

  function startFocusOnTask(taskId) {
    selectedTaskIdForPomo = taskId;
    switchTab('foco');
  }

  function updatePomoDisplay() {
    const mins = String(Math.floor(pomoSecondsLeft / 60)).padStart(2, '0');
    const secs = String(pomoSecondsLeft % 60).padStart(2, '0');
    document.getElementById('pomo-timer-display').textContent = `${mins}:${secs}`;
  }

  function togglePomodoro() {
    if (pomoIsRunning) {
      clearInterval(pomoInterval);
      pomoIsRunning = false;
      document.getElementById('btn-pomo-label').textContent = 'Retomar';
      document.getElementById('pomo-status-text').textContent = 'Pausado';
    } else {
      pomoIsRunning = true;
      document.getElementById('btn-pomo-label').textContent = 'Pausar';
      document.getElementById('pomo-status-text').textContent = pomoIsBreak ? 'Em pausa restauradora...' : 'Foco ativo na tarefa!';
      pomoInterval = setInterval(() => {
        if (pomoSecondsLeft > 0) {
          pomoSecondsLeft--;
          updatePomoDisplay();
        } else {
          completePomodoroCycle();
        }
      }, 1000);
    }
  }

  function completePomodoroCycle() {
    clearInterval(pomoInterval);
    pomoIsRunning = false;

    if (!pomoIsBreak && selectedTaskIdForPomo) {
      const myData = getMyTaskData(selectedTaskIdForPomo);
      myData.pomodoros = (myData.pomodoros || 0) + 1;
      saveProgress();
      alert('Ciclo Pomodoro concluído em 00:00! +1 bloco contabilizado na atividade (RN06). Iniciando pausa de 5 minutos.');
      pomoIsBreak = true;
      pomoSecondsLeft = 5 * 60;
      document.getElementById('pomo-mode-badge').textContent = 'Pausa Curta • 5 min';
      document.getElementById('pomo-mode-badge').className = 'inline-block px-3 py-1 rounded-full text-[11px] font-extrabold uppercase tracking-wider bg-emerald-100 text-emerald-700';
    } else {
      alert('Pausa concluída! Pronto para um novo bloco de 25 minutos.');
      pomoIsBreak = false;
      pomoSecondsLeft = 25 * 60;
      document.getElementById('pomo-mode-badge').textContent = 'Ciclo de Foco • 25 min';
      document.getElementById('pomo-mode-badge').className = 'inline-block px-3 py-1 rounded-full text-[11px] font-extrabold uppercase tracking-wider bg-indigo-100 text-indigo-700';
    }

    document.getElementById('btn-pomo-label').textContent = 'Iniciar';
    document.getElementById('pomo-status-text').textContent = 'Ciclo finalizado';
    updatePomoDisplay();
    renderTasks();
  }

  function resetPomodoro() {
    clearInterval(pomoInterval);
    pomoIsRunning = false;
    pomoIsBreak = false;
    pomoSecondsLeft = 25 * 60;
    document.getElementById('btn-pomo-label').textContent = 'Iniciar Foco';
    document.getElementById('pomo-status-text').textContent = 'Reiniciado (sem contabilizar - RN06)';
    document.getElementById('pomo-mode-badge').textContent = 'Ciclo de Foco • 25 min';
    updatePomoDisplay();
  }

  function startDemoPomodoro() {
    clearInterval(pomoInterval);
    pomoIsRunning = false;
    pomoIsBreak = false;
    pomoSecondsLeft = 5;
    updatePomoDisplay();
    togglePomodoro();
  }
</script>
</body>
</html>
