<index.html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>CEJ - Expediente Judicial Electrónico | Gobierno Digital e Informático</title>
  
  <style>
    /* PALETA CROMÁTICA INSTITUCIONAL MAGENTA / VINO IMPERIAL */
    :root {
      --mag-darkest: #240315;
      --mag-dark: #4a0418;
      --mag-primary: #831034;
      --mag-vivid: #be185d;
      --mag-rose: #f43f5e;
      --mag-soft: #fdf2f8;
      --mag-border: #fbcfe8;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --bg-white: #ffffff;
      --state-green: #059669;
      --state-blue: #2563eb;
      --state-amber: #d97706;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
    }

    body {
      background-color: var(--mag-soft);
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    /* PANTALLAS MUTUAMENTE EXCLUYENTES */
    .screen-stage {
      display: none !important;
      width: 100%;
      flex-grow: 1;
    }
    .screen-stage.active {
      display: flex !important;
      flex-direction: column;
    }

    /* BANNER SUPERIOR ACADÉMICO */
    .academic-topbar {
      background: linear-gradient(90deg, #3d0213, #831034, #3d0213);
      color: #fce7f3;
      font-size: 11px;
      font-weight: 700;
      padding: 7px 12px;
      text-align: center;
      position: sticky;
      top: 0;
      z-index: 1000;
      border-bottom: 1px solid var(--mag-vivid);
      letter-spacing: 0.5px;
    }

    .center-content {
      display: flex;
      flex-grow: 1;
      align-items: center;
      justify-content: center;
      padding: 16px;
    }

    .card-academic {
      background: var(--bg-white);
      border-radius: 24px;
      border: 1px solid var(--mag-border);
      box-shadow: 0 15px 35px rgba(131, 16, 52, 0.15);
      width: 100%;
      max-width: 620px;
      overflow: hidden;
      text-align: center;
    }

    .academic-header-box {
      background: linear-gradient(135deg, #4a0418 0%, #831034 50%, #be185d 100%);
      color: #ffffff;
      padding: 28px 20px 20px;
    }

    .btn-main {
      background: linear-gradient(90deg, #831034, #be185d);
      color: #ffffff;
      border: none;
      padding: 13px 24px;
      border-radius: 12px;
      font-weight: 700;
      font-size: 14px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      width: 100%;
      transition: all 0.2s ease;
      box-shadow: 0 4px 14px rgba(190, 24, 93, 0.3);
    }
    .btn-main:hover {
      opacity: 0.95;
      transform: translateY(-1px);
    }

    /* PANTALLA 2: BARRA ESTATAL */
    .gov-top-bar {
      background-color: var(--mag-dark);
      color: #ffffff;
      padding: 10px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .gov-nav-horizontal {
      background-color: var(--mag-darkest);
      display: flex;
      overflow-x: auto;
      padding: 6px 12px;
      gap: 6px;
      -webkit-overflow-scrolling: touch;
    }
    .gov-nav-horizontal::-webkit-scrollbar { display: none; }

    .nav-item-btn {
      background: transparent;
      border: none;
      color: #fbcfe8;
      padding: 8px 14px;
      font-size: 12px;
      font-weight: 600;
      cursor: pointer;
      border-radius: 6px;
      white-space: nowrap;
    }
    .nav-item-btn.active, .nav-item-btn:hover {
      background: rgba(255, 255, 255, 0.12);
      color: #ffffff;
    }
    .nav-item-search {
      margin-left: auto;
      background: #be185d !important;
      color: #ffffff !important;
      font-weight: 700;
    }

    /* CRONÓMETRO */
    .timer-pill {
      background: var(--mag-darkest);
      border: 1px solid #831034;
      color: #fce7f3;
      padding: 4px 10px;
      border-radius: 8px;
      font-family: monospace;
      font-size: 13px;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .timer-alert {
      background: #e11d48 !important;
      animation: pulseAlert 1s infinite;
    }
    @keyframes pulseAlert {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.4; }
    }

    /* CONTENEDORES Y PANELES */
    .layout-wrapper {
      max-width: 1180px;
      width: 100%;
      margin: 0 auto;
      padding: 16px;
    }

    .panel-card {
      background: #ffffff;
      border-radius: 18px;
      border: 1px solid var(--mag-border);
      padding: 18px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.02);
      margin-bottom: 18px;
    }

    .panel-roman-title {
      font-size: 14px;
      font-weight: 800;
      color: var(--mag-primary);
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 14px;
      padding-bottom: 8px;
      border-bottom: 2px solid #fce7f3;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    /* BARRA VISUAL DE PROGRESO DEL PROCESO */
    .process-stepper {
      display: flex;
      justify-content: space-between;
      position: relative;
      margin: 18px 0 26px;
    }
    .process-stepper::before {
      content: '';
      position: absolute;
      top: 14px;
      left: 10px;
      right: 10px;
      height: 4px;
      background: #e2e8f0;
      z-index: 1;
    }
    .process-progress-bar {
      position: absolute;
      top: 14px;
      left: 10px;
      width: 35%;
      height: 4px;
      background: linear-gradient(90deg, #831034, #be185d);
      z-index: 2;
    }
    .step-item {
      position: relative;
      z-index: 3;
      text-align: center;
      flex: 1;
    }
    .step-circle {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      background: #ffffff;
      border: 3px solid #cbd5e1;
      margin: 0 auto 6px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
      font-weight: bold;
      color: #64748b;
    }
    .step-item.completed .step-circle {
      border-color: #831034;
      background: #831034;
      color: #ffffff;
    }
    .step-item.active .step-circle {
      border-color: #be185d;
      background: #be185d;
      color: #ffffff;
      box-shadow: 0 0 0 3px rgba(190, 24, 93, 0.25);
    }
    .step-label {
      font-size: 11px;
      font-weight: 600;
      color: #64748b;
    }
    .step-item.active .step-label {
      color: #831034;
      font-weight: 800;
    }

    /* BOTONES DE INTEROPERABILIDAD DINÁMICOS Y ANIMADOS */
    .btn-interop {
      position: relative;
      display: inline-flex;
      align-items: center;
      gap: 7px;
      padding: 7px 13px;
      border-radius: 9px;
      font-size: 11px;
      font-weight: 700;
      border: none;
      cursor: pointer;
      color: #ffffff;
      transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: 0 2px 6px rgba(0,0,0,0.15);
      overflow: hidden;
    }
    .btn-interop::after {
      content: '';
      position: absolute;
      top: -50%;
      left: -60%;
      width: 40%;
      height: 200%;
      background: rgba(255, 255, 255, 0.25);
      transform: rotate(30deg);
      transition: all 0.6s ease;
    }
    .btn-interop:hover::after {
      left: 140%;
    }
    .btn-interop:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 6px 14px rgba(0,0,0,0.22);
    }
    .btn-interop:active {
      transform: translateY(0) scale(0.98);
    }
    .btn-interop svg {
      width: 15px;
      height: 15px;
      flex-shrink: 0;
      transition: transform 0.25s ease;
    }
    .btn-interop:hover svg {
      transform: scale(1.15) rotate(4deg);
    }

    .btn-reniec { background: linear-gradient(135deg, #0284c7, #0369a1); }
    .btn-migra { background: linear-gradient(135deg, #d97706, #b45309); }
    .btn-pnp { background: linear-gradient(135deg, #047857, #065f46); }
    .btn-inpe { background: linear-gradient(135deg, #b91c1c, #991b1b); }

    /* LÍNEA DE TIEMPO INTERACTIVA */
    .timeline-container {
      position: relative;
      padding: 12px 0 12px 24px;
      border-left: 3px solid var(--mag-vivid);
      margin-left: 10px;
    }
    .timeline-event {
      position: relative;
      margin-bottom: 16px;
    }
    .timeline-event:last-child { margin-bottom: 0; }
    .timeline-badge {
      position: absolute;
      left: -33px;
      top: 2px;
      width: 18px;
      height: 18px;
      border-radius: 50%;
      background: #be185d;
      border: 3px solid #ffffff;
      box-shadow: 0 0 0 2px #be185d;
    }
    .timeline-card-content {
      background: #fdf2f8;
      border: 1px solid var(--mag-border);
      border-radius: 12px;
      padding: 10px 14px;
      transition: all 0.2s ease;
    }
    .timeline-card-content:hover {
      background: #ffffff;
      border-color: #be185d;
      box-shadow: 0 4px 12px rgba(190, 24, 93, 0.1);
    }

    /* VISOR PDF EN MODAL */
    .pdf-viewer-bar {
      background: #1e293b;
      color: #f1f5f9;
      padding: 8px 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid #334155;
      font-size: 11px;
    }
    .pdf-page-container {
      background: #525659;
      padding: 16px;
      display: flex;
      justify-content: center;
      overflow-y: auto;
      max-height: 60vh;
    }
    .pdf-sheet {
      background: #ffffff;
      width: 100%;
      max-width: 580px;
      min-height: 650px;
      padding: 36px 32px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.3);
      font-family: "Georgia", "Times New Roman", serif;
      font-size: 12px;
      line-height: 1.65;
      color: #111827;
      position: relative;
    }
    .pdf-watermark {
      position: absolute;
      top: 40%;
      left: 15%;
      transform: rotate(-35deg);
      font-size: 42px;
      font-weight: 800;
      color: rgba(131, 16, 52, 0.05);
      user-select: none;
      pointer-events: none;
      letter-spacing: 4px;
    }

    /* ESTILO FICHA RENIEC CON FOTOGRAFÍA */
    .reniec-card-frame {
      display: grid;
      grid-template-columns: 140px 1fr;
      gap: 16px;
      background: #ffffff;
      border: 2px solid #0284c7;
      border-radius: 12px;
      padding: 14px;
    }
    @media (max-width: 550px) {
      .reniec-card-frame { grid-template-columns: 1fr; }
    }
    .reniec-photo-box {
      background: #f1f5f9;
      border: 1px solid #cbd5e1;
      border-radius: 8px;
      padding: 6px;
      text-align: center;
    }
    .censored-pill {
      font-family: monospace;
      letter-spacing: 2px;
      background: #e2e8f0;
      padding: 1px 4px;
      border-radius: 3px;
      color: #475569;
      font-weight: bold;
    }

    /* TABLA RESPONSIVA */
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 12px;
    }
    th {
      background: var(--mag-dark);
      color: #ffffff;
      text-align: left;
      padding: 9px 8px;
      font-weight: 600;
    }
    td {
      padding: 9px 8px;
      border-bottom: 1px solid #fce7f3;
    }
    .view-desktop { display: block; }
    .view-mobile { display: none; }
    @media (max-width: 768px) {
      .view-desktop { display: none; }
      .view-mobile { display: block; }
      .split-responsive { grid-template-columns: 1fr !important; }
      .process-stepper { flex-wrap: wrap; gap: 8px; }
      .process-stepper::before, .process-progress-bar { display: none; }
    }

    .split-responsive {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 16px;
      margin-bottom: 16px;
    }

    /* MODALES FLOTANTES */
    .modal-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(36, 3, 21, 0.78);
      backdrop-filter: blur(3px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 14px;
      z-index: 2000;
    }
    .modal-card {
      background: #ffffff;
      border-radius: 18px;
      max-width: 680px;
      width: 100%;
      max-height: 90vh;
      overflow-y: auto;
      border: 1px solid var(--mag-border);
      box-shadow: 0 20px 40px rgba(0,0,0,0.35);
    }

    /* BARRAS DE PROGRESO DE PANTALLAS DE CARGA */
    .progress-bar-wrap {
      background: #fce7f3;
      height: 8px;
      border-radius: 8px;
      overflow: hidden;
      width: 100%;
      margin: 16px 0;
    }
    .progress-bar-inner {
      height: 100%;
      background: linear-gradient(90deg, #831034, #be185d);
      width: 0%;
      transition: width 0.1s linear;
    }
  </style>
</head>
<body>

  <!-- BANNER SUPERIOR INFORMATIVO -->
  <div class="academic-topbar">
    PRODUCTO ACADÉMICO UNIVERSITARIO - FACULTAD DE DERECHO | SIMULADOR NO OFICIAL
  </div>

  <div style="flex-grow: 1; display: flex; flex-direction: column;">

    <!-- ============================================================ -->
    <!-- PANTALLA 0: BIENVENIDA (ESTÁTICA CON TEMIS Y DATOS)          -->
    <!-- ============================================================ -->
    <div id="pantalla-0" class="screen-stage active center-content">
      <div class="card-academic">
        <div class="academic-header-box">
          
          <!-- TEMIS EN EL CENTRO DE LA PANTALLA 0 -->
          <div style="margin: 0 auto 12px; width: 110px; height: 110px; background: rgba(255,255,255,0.12); border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid #fbcfe8;">
            <svg style="width: 80px; height: 80px;" viewBox="0 0 200 200" fill="none">
              <circle cx="100" cy="100" r="90" fill="#fdf2f8" stroke="#be185d" stroke-width="3" stroke-dasharray="4 2"/>
              <path d="M100 25 L100 160" stroke="#831034" stroke-width="4" stroke-linecap="round"/>
              <path d="M80 160 L120 160" stroke="#831034" stroke-width="6" stroke-linecap="round"/>
              <path d="M50 55 L150 55" stroke="#be185d" stroke-width="4" stroke-linecap="round"/>
              <circle cx="100" cy="55" r="6" fill="#831034"/>
              <path d="M50 55 L35 95" stroke="#9f1239" stroke-width="2"/><path d="M50 55 L65 95" stroke="#9f1239" stroke-width="2"/>
              <path d="M25 95 Q50 115 75 95 Z" fill="#fbcfe8"/>
              <path d="M150 55 L135 95" stroke="#9f1239" stroke-width="2"/><path d="M150 55 L165 95" stroke="#9f1239" stroke-width="2"/>
              <path d="M125 95 Q150 115 175 95 Z" fill="#fbcfe8"/>
              <path d="M85 40 Q100 35 115 40" stroke="#4a0418" stroke-width="3"/>
            </svg>
          </div>

          <h1 style="font-size: 20px; font-weight: 800; letter-spacing: 0.5px;">SISTEMA DE CONSULTA DE EXPEDIENTES (CEJ / EJE)</h1>
          <p style="font-size: 13px; color: #fce7f3; margin-top: 4px;">Simulación Jurisdiccional para Derecho e Informática</p>
        </div>

        <div style="padding: 24px; text-align: left;">
          
          <!-- DATOS ACADÉMICOS -->
          <div style="background: #fdf2f8; border: 1px solid var(--mag-border); border-radius: 12px; padding: 14px; margin-bottom: 16px;">
            <div style="font-size: 13px; margin-bottom: 6px;">
              <span style="color: var(--text-muted);">Estudiante:</span>
              <strong style="color: var(--mag-primary); font-size: 14px;"> Sonia Pilar Condori Ruelas</strong>
            </div>
            <div style="font-size: 13px; margin-bottom: 6px;">
              <span style="color: var(--text-muted);">Curso:</span>
              <strong style="color: var(--mag-dark);"> Gobierno Digital e Informático</strong>
            </div>
            <div style="font-size: 13px;">
              <span style="color: var(--text-muted);">Docente:</span>
              <strong style="color: var(--mag-dark);"> Dr. Michael Espinoza Coila</strong>
            </div>
          </div>

          <!-- AVISO ACADÉMICO -->
          <div style="background: #fff1f2; border-left: 4px solid #be185d; padding: 10px 12px; border-radius: 6px; margin-bottom: 18px;">
            <p style="font-size: 11px; color: #4a0418; line-height: 1.4; font-weight: 600;">
              AVISO: El presente trabajo es un producto netamente académico y NO es un sitio oficial del Poder Judicial del Perú. Su diseño responde exclusivamente a fines didácticos universitarios.
            </p>
          </div>

          <!-- BOTÓN PASAR A PANTALLA 1 -->
          <button onclick="switchScreen(1)" class="btn-main">
            <span>Ingresar al Sistema</span>
            <svg style="width: 16px; height: 16px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          </button>
        </div>
      </div>
    </div>

    <!-- ============================================================ -->
    <!-- PANTALLA 1: CARGA DE PANTALLA (SIN BARRA, AUTOMÁTICA A LA 2) -->
    <!-- ============================================================ -->
    <div id="pantalla-1" class="screen-stage center-content">
      <div style="max-width: 360px; width: 100%; text-align: center;">
        <svg style="width: 48px; height: 48px; color: #831034; margin-bottom: 12px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
        </svg>
        <h3 style="font-size: 16px; font-weight: 700; color: #4a0418;">Iniciando Portal Institucional</h3>
        <p style="font-size: 12px; color: #64748b; margin-top: 4px;">Cargando módulos de Gobierno Digital...</p>
        <div class="progress-bar-wrap">
          <div id="p1-loader-fill" class="progress-bar-inner"></div>
        </div>
      </div>
    </div>

    <!-- ============================================================ -->
    <!-- PANTALLA 2: PÁGINA PRINCIPAL (BARRA, TEMIS, MODALES)         -->
    <!-- ============================================================ -->
    <div id="pantalla-2" class="screen-stage">
      <!-- Barra Superior -->
      <div class="gov-top-bar">
        <div style="display: flex; align-items: center; gap: 8px;">
          <svg style="width: 22px; height: 22px; color: #fbcfe8;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 21h18"/><path d="M3 10h18"/><path d="M5 10v11"/><path d="M19 10v11"/><path d="M9 10v11"/><path d="M15 10v11"/><path d="M12 2 2 7h20L12 2z"/></svg>
          <div>
            <div style="font-size: 9px; font-weight: 800; color: #fbcfe8; letter-spacing: 0.5px;">PODER JUDICIAL DEL PERÚ</div>
            <div style="font-size: 13px; font-weight: 700;">CEJ Electrónico - Distrito Judicial de Puno</div>
          </div>
        </div>

        <div style="display: flex; align-items: center; gap: 8px;">
          <div id="timer-indicator" class="timer-pill">
            <span style="font-size: 11px;">Sesión:</span>
            <strong id="timer-text">07:00</strong>
          </div>
          <button onclick="resetTimer()" title="Reiniciar sesión" style="background: none; border: 1px solid #831034; color: white; padding: 4px 8px; border-radius: 6px; cursor: pointer;">↻</button>
        </div>
      </div>

      <!-- Barra Horizontal Estatal -->
      <div class="gov-nav-horizontal">
        <button onclick="showInfoMenu('inicio')" class="nav-item-btn active">Inicio</button>
        <button onclick="showInfoMenu('mision')" class="nav-item-btn">Misión</button>
        <button onclick="showInfoMenu('vision')" class="nav-item-btn">Visión</button>
        <button onclick="showInfoMenu('transparencia')" class="nav-item-btn">Transparencia</button>
        <button onclick="showInfoMenu('contactanos')" class="nav-item-btn">Contáctanos</button>
        <button onclick="triggerCaptchaWorkflow()" class="nav-item-btn nav-item-search">🔍 Búsqueda de Expediente</button>
      </div>

      <!-- Área Central de Pantalla 2 -->
      <div class="layout-wrapper" style="flex-grow: 1; display: flex; flex-direction: column; justify-content: center;">
        
        <!-- PARTE VACÍA CON TEMIS: AL CLIC LLEVA AL CAPTCHA -->
        <div id="temis-blank-box" onclick="triggerCaptchaWorkflow()" class="panel-card" style="text-align: center; padding: 40px 16px; cursor: pointer;">
          <svg style="width: 140px; height: 140px; margin: 0 auto 14px; display: block;" viewBox="0 0 200 200" fill="none">
            <circle cx="100" cy="100" r="90" fill="#fdf2f8" stroke="#be185d" stroke-width="3" stroke-dasharray="4 2"/>
            <path d="M100 25 L100 160" stroke="#831034" stroke-width="4" stroke-linecap="round"/>
            <path d="M80 160 L120 160" stroke="#831034" stroke-width="6" stroke-linecap="round"/>
            <path d="M50 55 L150 55" stroke="#be185d" stroke-width="4" stroke-linecap="round"/>
            <circle cx="100" cy="55" r="6" fill="#831034"/>
            <path d="M50 55 L35 95" stroke="#9f1239" stroke-width="2"/><path d="M50 55 L65 95" stroke="#9f1239" stroke-width="2"/>
            <path d="M25 95 Q50 115 75 95 Z" fill="#fbcfe8"/>
            <path d="M150 55 L135 95" stroke="#9f1239" stroke-width="2"/><path d="M150 55 L165 95" stroke="#9f1239" stroke-width="2"/>
            <path d="M125 95 Q150 115 175 95 Z" fill="#fbcfe8"/>
            <path d="M85 40 Q100 35 115 40" stroke="#4a0418" stroke-width="3"/>
          </svg>
          <h2 style="font-size: 19px; color: #4a0418; font-weight: 800;">Consulta de Expedientes Judiciales (CEJ)</h2>
          <p style="font-size: 13px; color: #64748b; max-width: 480px; margin: 8px auto 14px;">
            Haga clic en cualquier parte de este espacio o en el botón superior para ingresar el <strong>CAPTCHA de seguridad</strong>.
          </p>
          <span style="font-size: 11px; background: #be185d; color: white; padding: 6px 14px; border-radius: 20px; font-weight: bold; display: inline-block;">
            Clic aquí para desbloquear búsqueda
          </span>
        </div>

        <!-- Panel de Filtro de Búsqueda Desplegado tras CAPTCHA y Comunicado -->
        <div id="search-inline-panel" class="panel-card" style="display: none; max-width: 650px; margin: 0 auto; width: 100%;">
          <div style="background: #4a0418; color: white; padding: 12px 16px; border-radius: 12px 12px 0 0; margin: -18px -18px 16px; display: flex; justify-content: space-between; align-items: center;">
            <strong style="font-size: 13px;">Búsqueda Jurisdiccional de Causas</strong>
            <button onclick="cancelSearchWorkflow()" style="background: none; border: none; color: #fbcfe8; cursor: pointer; font-size: 16px;">✕</button>
          </div>

          <!-- Pestañas Número / Partes -->
          <div style="display: flex; gap: 8px; margin-bottom: 14px; border-bottom: 1px solid #fce7f3; padding-bottom: 8px;">
            <button id="tab-code-btn" onclick="toggleSearchMode('code')" style="background: #831034; color: white; border: none; padding: 7px 14px; border-radius: 6px; font-size: 12px; font-weight: bold; cursor: pointer;">Por Número de Expediente</button>
            <button id="tab-party-btn" onclick="toggleSearchMode('party')" style="background: #e2e8f0; color: #334155; border: none; padding: 7px 14px; border-radius: 6px; font-size: 12px; font-weight: bold; cursor: pointer;">Por Partes Procesales</button>
          </div>

          <!-- Búsqueda por Número -->
          <div id="tab-code-content">
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(110px, 1fr)); gap: 8px; margin-bottom: 12px;">
              <div>
                <label style="font-size: 11px; font-weight: bold; color: #64748b;">Correlativo</label>
                <input type="text" value="00174" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;">
              </div>
              <div>
                <label style="font-size: 11px; font-weight: bold; color: #64748b;">Año</label>
                <input type="text" value="2019" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;">
              </div>
              <div>
                <label style="font-size: 11px; font-weight: bold; color: #64748b;">Cuaderno</label>
                <input type="text" value="0" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;">
              </div>
              <div>
                <label style="font-size: 11px; font-weight: bold; color: #64748b;">Distrito</label>
                <input type="text" value="2111" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;">
              </div>
            </div>
          </div>

          <!-- Búsqueda por Partes -->
          <div id="tab-party-content" style="display: none; margin-bottom: 12px;">
            <label style="font-size: 11px; font-weight: bold; color: #64748b;">Demandante o Demandado:</label>
            <input type="text" value="Andrés Leonidas Supo Quispe" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; margin-top: 4px; font-weight: bold;">
          </div>

          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 10px; border-radius: 8px; font-size: 12px; margin-bottom: 16px;">
            Expediente asignado: <strong style="color: #831034;">00174-2019-0-2111-JR-LA-02</strong> (EsSalud vs Supo)
          </div>

          <!-- BOTÓN CONSULTAR: PASA A LA PANTALLA 4 -->
          <button onclick="switchScreen(4)" class="btn-main">
            <span>Consultar Expediente Judicial</span>
            <svg style="width: 16px; height: 16px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          </button>
        </div>

        <!-- Información Menú -->
        <div id="info-display-panel" class="panel-card" style="display: none;">
          <h3 id="info-header" style="color: var(--mag-primary); margin-bottom: 8px; font-size: 16px;"></h3>
          <p id="info-paragraph" style="font-size: 13px; color: #475569; line-height: 1.6;"></p>
          <button onclick="closeInfoMenu()" style="margin-top: 14px; background: #e2e8f0; border: none; padding: 7px 14px; border-radius: 6px; cursor: pointer; font-size: 12px; font-weight: 600;">Cerrar</button>
        </div>

      </div>
    </div>

    <!-- ============================================================ -->
    <!-- PANTALLA 4: CARGA DE PANTALLA (SIN BARRA, AUTOMÁTICA A LA 5) -->
    <!-- ============================================================ -->
    <div id="pantalla-4" class="screen-stage center-content">
      <div style="max-width: 360px; width: 100%; text-align: center;">
        <svg style="width: 48px; height: 48px; color: #be185d; margin-bottom: 12px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1-2.5-2.5Z"/><path d="M6 6h10"/><path d="M6 10h10"/>
        </svg>
        <h3 style="font-size: 16px; font-weight: 700; color: #4a0418;">Indexando Cuaderno Laboral Digital</h3>
        <p style="font-size: 12px; color: #64748b; margin-top: 4px;">Recuperando resoluciones, progreso y datos procesales...</p>
        <div class="progress-bar-wrap">
          <div id="p4-loader-fill" class="progress-bar-inner"></div>
        </div>
      </div>
    </div>

    <!-- ============================================================ -->
    <!-- PANTALLA 5: EXPEDIENTE COMPLETO ESTRUCTURADO (I A IV)        -->
    <!-- ============================================================ -->
    <div id="pantalla-5" class="screen-stage">
      <!-- Encabezado del Expediente -->
      <div style="background: #4a0418; color: white; padding: 12px 16px; border-bottom: 2px solid #be185d;">
        <div class="layout-wrapper" style="padding: 0; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px;">
          <div>
            <div style="font-size: 10px; color: #fbcfe8; font-weight: 700;">MÓDULO DEL EXPEDIENTE JUDICIAL ELECTRÓNICO (EJE)</div>
            <div style="font-size: 16px; font-weight: 800; font-family: monospace;">EXP. 00174-2019-0-2111-JR-LA-02</div>
          </div>
          <button onclick="switchScreen(2)" style="background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.3); color: white; padding: 6px 14px; border-radius: 6px; cursor: pointer; font-size: 12px; font-weight: 600;">
            ← Volver a la Búsqueda
          </button>
        </div>
      </div>

      <div class="layout-wrapper" style="padding-top: 16px; padding-bottom: 30px;">
        
        <!-- I. REPORTE DE EXPEDIENTE -->
        <div class="panel-card">
          <div class="panel-roman-title">
            <span>I. REPORTE DE EXPEDIENTE</span>
            <span style="font-size: 11px; background: #fdf2f8; border: 1px solid #fbcfe8; padding: 2px 8px; border-radius: 4px; font-family: monospace; color: #831034;">Barcode: 22019001742111334000038</span>
          </div>
          <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; font-size: 12px;">
            <div><span style="color: #64748b; display: block;">Distrito Judicial / Sede:</span> <strong>Puno / San Román – Juliaca</strong></div>
            <div><span style="color: #64748b; display: block;">Órgano Jurisdiccional:</span> <strong>Juzgado de Trabajo – Zona Norte</strong></div>
            <div><span style="color: #64748b; display: block;">Juez a Cargo:</span> <strong>Huamán Romero, Gonzalo Víctor</strong></div>
            <div><span style="color: #64748b; display: block;">Secretaria Judicial:</span> <strong>Carlos Villán, Rosario</strong></div>
            <div><span style="color: #64748b; display: block;">Fecha de Ingreso:</span> <strong>26/06/2019 – 11:31:38</strong></div>
            <div><span style="color: #64748b; display: block;">Materia / Vía Procedimental:</span> <strong style="color: #831034;">Desnaturalización / Proceso Ordinario (Ley 26636)</strong></div>
          </div>
        </div>

        <!-- II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO -->
        <div class="panel-card">
          <div class="panel-roman-title">
            <span>II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO</span>
            <span style="font-size: 11px; background: #ecfdf5; border: 1px solid #a7f3d0; padding: 2px 8px; border-radius: 4px; color: #047857; font-weight: bold;">Etapa: Postulatoria (En Trámite)</span>
          </div>

          <!-- Barra Visual de Progreso del Proceso Judicial -->
          <div class="process-stepper">
            <div class="process-progress-bar"></div>
            
            <div class="step-item completed">
              <div class="step-circle">✓</div>
              <div class="step-label">1. Postulatoria<br><span style="font-size: 10px; color: #059669;">(Demanda y Traslado)</span></div>
            </div>
            <div class="step-item active">
              <div class="step-circle">2</div>
              <div class="step-label">2. Probatoria<br><span style="font-size: 10px; color: #be185d;">(En Calificación)</span></div>
            </div>
            <div class="step-item">
              <div class="step-circle">3</div>
              <div class="step-label">3. Decisoria<br><span style="font-size: 10px; color: #94a3b8;">(Sentencia)</span></div>
            </div>
            <div class="step-item">
              <div class="step-circle">4</div>
              <div class="step-label">4. Impugnatoria<br><span style="font-size: 10px; color: #94a3b8;">(Apelación)</span></div>
            </div>
            <div class="step-item">
              <div class="step-circle">5</div>
              <div class="step-label">5. Ejecución<br><span style="font-size: 10px; color: #94a3b8;">(Cumplimiento)</span></div>
            </div>
          </div>

          <!-- Línea de Tiempo de los Hitos Principales -->
          <div style="font-size: 12px; font-weight: bold; color: #4a0418; margin: 16px 0 8px;">Hitos Cronológicos del Proceso:</div>
          <div class="timeline-container" id="timeline-flow-list"></div>
        </div>

        <!-- III. PARTES PROCESALES CON CONSULTAS DE INTEROPERABILIDAD -->
        <div class="panel-card">
          <div class="panel-roman-title">
            <span>III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)</span>
            <span style="font-size: 10px; color: #64748b;">Consultas en línea certificadas</span>
          </div>
          
          <div style="display: flex; flex-direction: column; gap: 12px; font-size: 12px;">
            <!-- Demandante -->
            <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 12px; border-radius: 10px;">
              <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 6px; margin-bottom: 6px;">
                <span style="color: #be185d; font-weight: 800; font-size: 10px;">PARTE DEMANDANTE</span>
                <span style="font-family: monospace; font-size: 11px; background: white; padding: 1px 6px; border-radius: 4px; border: 1px solid #fbcfe8;">DNI: 02167445</span>
              </div>
              <div style="font-weight: bold; font-size: 14px; color: #0f172a;">Andrés Leonidas Supo Quispe</div>
              <div style="font-size: 11px; color: #64748b; margin: 2px 0 10px;">Abogado Patrocinante: Dr. Lino Larico Larico (Reg. CAP N° 47) | SINOE: <strong>60375</strong></div>
              
              <!-- Botones de Interoperabilidad con Iconos y Animaciones Dinámicas -->
              <div style="display: flex; flex-wrap: wrap; gap: 8px;">
                <!-- RENIEC -->
                <button onclick="openReniecModal()" class="btn-interop btn-reniec">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/>
                  </svg>
                  <span>RENIEC (Identidad Biométrica)</span>
                </button>

                <!-- MIGRACIONES -->
                <button onclick="openInteropModal('MIGRACIONES', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'Control Migratorio Central: Sin alertas ni impedimentos judiciales de salida del país. Pasaporte ordinario habilitado. Sin movimientos migratorios irregulares.')" class="btn-interop btn-migra">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"/><path d="m4.93 4.93 4.24 4.24"/><path d="m14.83 9.17 4.24-4.24"/><path d="m14.83 14.83 4.24 4.24"/><path d="m9.17 14.83-4.24 4.24"/>
                  </svg>
                  <span>MIGRACIONES (Alerta)</span>
                </button>

                <!-- PNP -->
                <button onclick="openInteropModal('PNP', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'SISTEMA ESINPOL / REQUISITORIAS: NO REGISTRA ORDEN DE CAPTURA NI REQUISITORIA VIGENTE a nivel nacional. Sin antecedentes policiales pendientes en la macro región policial Puno.')" class="btn-interop btn-pnp">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
                  </svg>
                  <span>PNP (Requisitorias)</span>
                </button>

                <!-- INPE -->
                <button onclick="openInteropModal('INPE', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'REGISTRO PENITENCIARIO NACIONAL: NO REGISTRA ANTECEDENTES PENALES ni sentencias condenatorias con pena privativa de libertad efectiva o suspendida en centros penitenciarios.')" class="btn-interop btn-inpe">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <rect width="18" height="11" x="3" y="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/>
                  </svg>
                  <span>INPE (Antecedentes)</span>
                </button>
              </div>
            </div>

            <!-- Demandada -->
            <div style="background: #fff1f2; border: 1px solid #fecdd3; padding: 12px; border-radius: 10px;">
              <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px;">
                <span style="color: #e11d48; font-weight: 800; font-size: 10px;">PARTE DEMANDADA (ENTIDAD PÚBLICA)</span>
                <span style="font-family: monospace; font-size: 11px; background: white; padding: 1px 6px; border-radius: 4px; border: 1px solid #fecdd3;">RUC: 20131257750</span>
              </div>
              <div style="font-weight: bold; font-size: 14px; color: #0f172a;">Seguro Social de Salud - EsSalud (Red Asistencial Juliaca)</div>
              <div style="font-size: 11px; color: #64748b; margin: 2px 0 10px;">Apoderado Judicial: Abog. Hernán Rolando López Alférez (DNI 01207861) | Casilla SINOE: <strong>59629</strong></div>

              <!-- Botones de Interoperabilidad Apoderado EsSalud -->
              <div style="display: flex; flex-wrap: wrap; gap: 8px;">
                <button onclick="openInteropModal('RENIEC', 'Hernán Rolando López Alférez (Apoderado EsSalud)', 'DNI: 01207861', 'Identidad confirmada en el registro civil. Facultades judiciales inscritas en Partida Registral N° 11008571 de la Zona Registral N° IX - Sede Lima.')" class="btn-interop btn-reniec">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                  <span>RENIEC (Apoderado)</span>
                </button>
                <button onclick="openInteropModal('PNP', 'Hernán Rolando López Alférez (Apoderado EsSalud)', 'DNI: 01207861', 'SISTEMA ESINPOL: SIN REQUISITORIAS VIGENTES NI ÓRDENES JUDICIALES DE CAPTURA REGISTRADAS.')" class="btn-interop btn-pnp">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
                  <span>PNP (Requisitorias)</span>
                </button>
              </div>
            </div>

            <!-- Tercero Vinculado -->
            <div style="background: #f8fafc; border: 1px solid #e2e8f0; padding: 10px 12px; border-radius: 10px; font-size: 11px;">
              <strong>Tercero Vinculado en la Relación de Intermediación:</strong> Servicios Integrados de Limpieza S.A. – SILSA (RUC 20100362598).
            </div>
          </div>
        </div>

        <!-- IV. SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES Y NOTIFICACIONES) -->
        <div class="panel-card">
          <div class="panel-roman-title">
            <span>IV. SEGUIMIENTO DEL EXPEDIENTE (NOTIFICACIONES Y RESOLUCIONES EN PDF)</span>
            <span style="font-size: 11px; color: #831034; font-weight: bold;">12 Actuados Registrados</span>
          </div>

          <div class="view-desktop">
            <table>
              <thead>
                <tr>
                  <th style="width: 35px; text-align: center;">N°</th>
                  <th style="width: 85px;">Fojas</th>
                  <th style="width: 85px;">Fecha</th>
                  <th style="width: 170px;">Tipo de Documento</th>
                  <th>Descripción del Actuado / Notificación</th>
                  <th style="width: 110px; text-align: center;">Visualización</th>
                </tr>
              </thead>
              <tbody id="acts-table-rows"></tbody>
            </table>
          </div>

          <div id="acts-cards-mobile" class="view-mobile"></div>
        </div>

      </div>
    </div>

  </div>

  <!-- ============================================================ -->
  <!-- MODAL COMUNICADO OFICIAL: ADVERTENCIA TÉCNICA MINJUSDH       -->
  <!-- ============================================================ -->
  <div id="comunicado-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 520px; padding: 24px; border-top: 5px solid #831034;">
      <div style="display: flex; align-items: center; gap: 8px; margin-bottom: 12px;">
        <svg style="width: 24px; height: 24px; color: #831034;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M12 9v4"/><path d="M12 17h.01"/><path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/>
        </svg>
        <h3 style="color: #4a0418; font-size: 16px; font-weight: 800; text-transform: uppercase;">COMUNICADO OFICIAL</h3>
      </div>

      <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 14px; border-radius: 10px; font-size: 12px; color: #334155; line-height: 1.6; margin-bottom: 16px; text-align: justify;">
        A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la <strong>Autoridad Nacional de Protección de Datos Personales</strong> y la <strong>Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH</strong>. Al amparo de la <strong>Ley N° 29733</strong>, Ley de Protección de Datos Personales.
      </div>

      <button onclick="acceptComunicadoAndShowSearch()" class="btn-main">
        <span>He leído y Acepto el Comunicado</span>
      </button>
    </div>
  </div>

  <!-- MODAL DE CAPTCHA FLOTANTE (PANTALLA 2) -->
  <div id="captcha-modal-overlay" class="modal-overlay">
    <div class="modal-card" style="max-width: 480px; padding: 24px;">
      <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px;">
        <h3 style="color: #4a0418; font-size: 16px; font-weight: bold;">Validación de Seguridad CAPTCHA</h3>
        <button onclick="closeCaptchaModal()" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>

      <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 10px; border-radius: 8px; font-size: 12px; color: #831034; margin-bottom: 14px;">
        Ingrese el código alfanumérico para continuar al módulo de consulta:
      </div>

      <div style="display: flex; gap: 8px; align-items: center; margin-bottom: 14px;">
        <div id="captcha-render" style="background: #240315; color: #fbcfe8; font-family: monospace; font-size: 22px; font-weight: 800; letter-spacing: 5px; padding: 8px 16px; border-radius: 8px; text-decoration: line-through;">
          8M4X1
        </div>
        <button onclick="refreshCaptcha()" style="padding: 9px 12px; border: 1px solid #cbd5e1; border-radius: 8px; cursor: pointer; background: white;" title="Nuevo código">↻</button>
        <input type="text" id="captcha-input-txt" placeholder="Código" style="flex-grow: 1; padding: 10px; border: 1px solid #cbd5e1; border-radius: 8px; text-transform: uppercase; font-weight: bold; font-size: 14px;">
      </div>

      <button onclick="validateCaptchaAndUnlock()" class="btn-main">Validar CAPTCHA</button>
      <div id="captcha-fail-msg" style="display: none; color: #e11d48; font-size: 12px; margin-top: 8px; text-align: center; font-weight: 600;">Código erróneo. Intente nuevamente.</div>
    </div>
  </div>

  <!-- MODAL ESPECIAL RENIEC CON FOTOGRAFÍA Y DATOS CENSURADOS (LEY 29733) -->
  <div id="reniec-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 580px; padding: 22px; border-top: 5px solid #0284c7;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #e0f2fe; padding-bottom: 10px; margin-bottom: 14px;">
        <div style="display: flex; align-items: center; gap: 8px;">
          <span style="background: #0284c7; color: white; font-weight: bold; font-size: 11px; padding: 3px 8px; border-radius: 4px;">RENIEC</span>
          <h4 style="font-size: 14px; font-weight: bold; color: #0369a1;">Ficha Registral de Identificación Biométrica</h4>
        </div>
        <button onclick="closeReniecModal()" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>

      <div style="font-size: 11px; background: #e0f2fe; color: #0369a1; padding: 8px 10px; border-radius: 6px; margin-bottom: 14px; font-weight: 600;">
        Información protegida por la Ley N° 29733. Los datos de filiación y ubicación se exhiben censurados mediante asteriscos.
      </div>

      <!-- Cuadro Ficha Reniec -->
      <div class="reniec-card-frame">
        <!-- Fotografía Simulada -->
        <div class="reniec-photo-box">
          <div style="width: 100%; height: 140px; background: #cbd5e1; border-radius: 6px; display: flex; flex-direction: column; align-items: center; justify-content: center; position: relative; overflow: hidden; border: 1px solid #94a3b8;">
            <svg style="width: 70px; height: 70px; color: #64748b; margin-top: 15px;" viewBox="0 0 24 24" fill="currentColor">
              <path fill-rule="evenodd" d="M7.5 6a4.5 4.5 0 1 1 9 0 4.5 4.5 0 0 1-9 0ZM3.751 20.105a8.25 8.25 0 0 1 16.498 0 .75.75 0 0 1-.437.695A18.683 18.683 0 0 1 12 22.5c-2.786 0-5.433-.608-7.812-1.7a.75.75 0 0 1-.437-.695Z" clip-rule="evenodd"/>
            </svg>
            <div style="position: absolute; bottom: 0; left: 0; right: 0; background: rgba(2, 132, 199, 0.85); color: white; font-size: 9px; padding: 2px 0; font-weight: bold; letter-spacing: 0.5px;">
              FOTO BIOMÉTRICA
            </div>
          </div>
          <div style="font-size: 10px; color: #64748b; margin-top: 6px; font-family: monospace;">DIG-VERIF: <span class="censored-pill">***</span></div>
        </div>

        <!-- Datos Parciales y Censurados -->
        <div style="font-size: 12px; line-height: 1.8; color: #1e293b;">
          <div><strong>Primer Apellido:</strong> SUPO</div>
          <div><strong>Segundo Apellido:</strong> QUISPE</div>
          <div><strong>Prenombres:</strong> ANDRÉS LEONIDAS</div>
          <div><strong>N° DNI:</strong> 0216<span class="censored-pill">****</span></div>
          <div><strong>Fecha de Nacimiento:</strong> **/**/197*</div>
          <div><strong>Sexo:</strong> Masculino</div>
          <div><strong>Estado Civil:</strong> Casado</div>
          <div><strong>Ubigeo Domicilio:</strong> 21<span class="censored-pill">****</span> (Juliaca - San Román)</div>
          <div><strong>Dirección Real:</strong> Av. Manco Cápac N° 964, <span class="censored-pill">*******</span></div>
          <div><strong>Caducidad DNI:</strong> **/**/202*</div>
        </div>
      </div>

      <button onclick="closeReniecModal()" style="width: 100%; margin-top: 16px; background: #0284c7; color: white; border: none; padding: 9px; border-radius: 8px; font-size: 12px; font-weight: bold; cursor: pointer;">Cerrar Ficha RENIEC</button>
    </div>
  </div>

  <!-- MODAL DE INTEROPERABILIDAD GENERAL (MIGRACIONES, PNP, INPE) -->
  <div id="interop-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 500px; padding: 22px;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #fce7f3; padding-bottom: 10px; margin-bottom: 14px;">
        <div style="display: flex; align-items: center; gap: 8px;">
          <span id="interop-tag" style="background: #831034; color: white; font-weight: bold; font-size: 11px; padding: 3px 8px; border-radius: 4px;">SISTEMA</span>
          <h4 id="interop-title" style="font-size: 14px; font-weight: bold; color: #4a0418;">Consulta de Interoperabilidad</h4>
        </div>
        <button onclick="closeInteropModal()" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>
      <div style="font-size: 12px; color: #64748b; margin-bottom: 6px;">Sujeto consultado: <strong id="interop-subject" style="color: #0f172a;"></strong></div>
      <div style="font-size: 11px; color: #64748b; margin-bottom: 12px;">Documento: <strong id="interop-doc" style="color: #0f172a; font-family: monospace;"></strong></div>
      
      <div id="interop-result-box" style="background: #f8fafc; border: 1px solid #e2e8f0; border-radius: 8px; padding: 12px; font-size: 12px; line-height: 1.6; color: #1e293b; margin-bottom: 16px;"></div>
      
      <button onclick="closeInteropModal()" style="width: 100%; background: #475569; color: white; border: none; padding: 8px; border-radius: 8px; font-size: 12px; font-weight: bold; cursor: pointer;">Cerrar Ficha de Consulta</button>
    </div>
  </div>

  <!-- ============================================================ -->
  <!-- MODAL VISOR DE DOCUMENTO EN FORMATO PDF JUDICIAL             -->
  <!-- ============================================================ -->
  <div id="pdf-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 680px; padding: 0; overflow: hidden; border-radius: 12px;">
      <!-- Barra superior del visor PDF -->
      <div class="pdf-viewer-bar">
        <div style="display: flex; align-items: center; gap: 8px;">
          <svg style="width: 16px; height: 16px; color: #ef4444;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"/><polyline points="14 2 14 8 20 8"/>
          </svg>
          <span id="pdf-bar-title" style="font-weight: bold;">Documento_Judicial.pdf</span>
        </div>
        <div style="display: flex; align-items: center; gap: 12px;">
          <span>Pág. 1 de 1</span>
          <button onclick="closePdfModal()" style="background: #475569; border: none; color: white; padding: 2px 8px; border-radius: 4px; cursor: pointer;">Cerrar ✕</button>
        </div>
      </div>

      <!-- Hoja digitalizada de estilo PDF -->
      <div class="pdf-page-container">
        <div class="pdf-sheet">
          <div class="pdf-watermark">PODER JUDICIAL</div>
          
          <!-- Encabezado de la Foja Judicial -->
          <div style="text-align: center; border-bottom: 2px solid #1e293b; padding-bottom: 12px; margin-bottom: 16px;">
            <div style="font-size: 11px; font-weight: bold; letter-spacing: 1px;">CORTE SUPERIOR DE JUSTICIA DE PUNO</div>
            <div style="font-size: 10px; color: #475569;">JUZGADO ESPECIALIZADO DE TRABAJO - ZONA NORTE DE JULIACA</div>
            <div style="font-size: 9px; font-family: monospace; color: #64748b; margin-top: 4px;">EXPEDIENTE: 00174-2019-0-2111-JR-LA-02 | ESPECIALISTA: CARLOS VILLÁN, ROSARIO</div>
          </div>

          <!-- Contenido Jurídico -->
          <div id="pdf-sheet-content" style="text-align: justify; margin-bottom: 24px;"></div>

          <!-- Sello de Firma Electrónica Certificada -->
          <div style="margin-top: 30px; border-top: 1px dashed #94a3b8; padding-top: 12px; display: flex; justify-content: space-between; align-items: flex-end; font-size: 10px; font-family: monospace;">
            <div style="color: #475569;">
              <div>FIRMADO DIGITALMENTE POR:</div>
              <strong style="color: #0f172a;">GONZALO VÍCTOR HUAMÁN ROMERO</strong>
              <div>Juez Titular - Juzgado de Trabajo Sede Juliaca</div>
              <div style="color: #059669; margin-top: 2px;">✓ Certificado Digital RENIEC / PJ Válido</div>
            </div>
            <div style="text-align: right; color: #64748b;">
              <div>Código Verif.: 2201900174</div>
              <div>Fecha Firma: Sistema EJE</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Pie del Visor -->
      <div style="background: #f8fafc; border-top: 1px solid #e2e8f0; padding: 8px 16px; display: flex; justify-content: space-between; align-items: center; font-size: 11px;">
        <span style="color: #059669; font-weight: bold;">Documento Incorporado al Expediente Judicial Electrónico</span>
        <button onclick="closePdfModal()" style="background: #831034; color: white; border: none; padding: 6px 14px; border-radius: 6px; cursor: pointer; font-weight: bold;">Finalizar Lectura</button>
      </div>
    </div>
  </div>

  <!-- MODAL DE SESIÓN EXPIRADA (7 MINUTOS) -->
  <div id="session-timeout-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 360px; text-align: center; padding: 24px;">
      <h3 style="color: #831034; font-size: 18px; margin-bottom: 8px;">Sesión Finalizada</h3>
      <p style="font-size: 12px; color: #64748b; margin-bottom: 16px;">Por seguridad institucional, su sesión inactiva de 7 minutos ha culminado.</p>
      <button onclick="forceRestartToScreen0()" class="btn-main">Aceptar e Ir al Inicio</button>
    </div>
  </div>

  <!-- PIE DE PÁGINA -->
  <footer style="background: #240315; color: #fbcfe8; font-size: 11px; text-align: center; padding: 12px; border-top: 1px solid #4a0418;">
    Facultad de Derecho | Gobierno Digital e Informático - Docente: Dr. Michael Espinoza Coila | Estudiante: Sonia Pilar Condori Ruelas
  </footer>

  <!-- SCRIPT LOGIC JAVASCRIPT -->
  <script>
    // BASE DE DATOS DE ACTUADOS Y NOTIFICACIONES
    var DATA_ACTUADOS = [
      { num: 1, fojas: "Fjs. 1-2", fecha: "26/06/2019", tipo: "Cargo / Carátula", desc: "Carátula oficial de ingreso CDG 00174-2019-0-2111-JR-LA-02 en Mesa de Partes Única.", html: "<p><strong>CARÁTULA OFICIAL DE INGRESO - MESA DE PARTES DE JULIACA</strong></p><p>Se deja constancia del ingreso del expediente N° 00174-2019-0-2111-JR-LA-02 por mesa de partes corporativa. Asignado inicialmente al 2° Juzgado Civil por turno. Especialista de recepción: Iván Palomino Jara. Sujetos: Supo Quispe Andrés Leonidas contra Seguro Social de Salud - EsSalud.</p>" },
      { num: 2, fojas: "Fjs. 2-26", fecha: "26/06/2019", tipo: "Escrito N° 01 (Demanda)", desc: "Demanda laboral ordinaria de desnaturalización de contrato e inclusión en planillas 728.", html: "<p><strong>SEÑOR JUEZ DEL JUZGADO DE TRABAJO DE SAN ROMÁN - JULIACA:</strong></p><p>ANDRÉS LEONIDAS SUPO QUISPE interpone demanda ordinaria laboral solicitando como pretensión principal la <strong>DESNATURALIZACIÓN DE LA INTERMEDIACIÓN LABORAL</strong> fraudulenta mantenida a través de SILSA desde el 01/12/1996; y accesoriamente su inclusión en planillas a plazo indeterminado de EsSalud bajo el D. Leg. N° 728 como Almacenero de la Unidad de Almacenes.</p>" },
      { num: 3, fojas: "Fjs. 26-96", fecha: "26/06/2019", tipo: "Recepción de Demanda", desc: "Ingreso formal de recaudos adjuntos y fijación de casilla electrónica SINOE 60375.", html: "<p>Se tienen por recepcionados los recaudos adjuntos de la demanda laboral, señalando como casilla electrónica SINOE N° 60375 y domicilio procesal en Jr. Pumacahua N° 150, Oficina 205, Juliaca.</p>" },
      { num: 4, fojas: "Fjs. 97", fecha: "11/07/2019", tipo: "Redistribución", desc: "Pasa al Juzgado de Trabajo Zona Norte de Juliaca en mérito a la Res. Adm. N° 232-2019-CE-PJ.", html: "<p><strong>DECRETO DE REDISTRIBUCIÓN:</strong></p><p>En mérito a lo resuelto en la Resolución Administrativa N° 232-2019-CE-PJ del Consejo Ejecutivo del Poder Judicial, cúmplase con remitir los actuados al Juzgado de Trabajo - Zona Norte para conocimiento de causas de la Ley 26636.</p>" },
      { num: 5, fojas: "Fjs. 98", fecha: "12/07/2019", tipo: "Razón de Secretaría", desc: "La Secretaria Judicial Rosario Carlos Villán asume formalmente la causa.", html: "<p><strong>RAZÓN DE SECRETARÍA:</strong></p><p>Doy cuenta al Despacho de asumir formalmente las funciones de especialista legal de causa por redistribución corporativa. Rosario Carlos Villán - Secretaria Judicial.</p>" },
      { num: 6, fojas: "Fjs. 99", fecha: "13/08/2019", tipo: "Resolución N° 01", desc: "Admisorio provisional: concede 3 días para pronunciarse sobre participación de SILSA.", html: "<p><strong>RESOLUCIÓN NRO. 01:</strong></p><p>Juliaca, 13 de agosto del año dos mil diecinueve.-</p><p><strong>AUTOS Y VISTOS:</strong> Con la demanda que antecede; y <strong>CONSIDERANDO:</strong> Que el demandante no ha precisado de forma expresa si corresponde emplazar en calidad de demandada a Servicios Integrados de Limpieza S.A. (SILSA); <strong>SE RESUELVE:</strong> Declarar <strong>ADMISIBLE PROVISIONALMENTE</strong> la demanda y <strong>CONCEDER TRES (03) DÍAS</strong> al demandante para que subsane dicha omisión bajo apercibimiento de rechazo.</p>" },
      { num: 7, fojas: "Fjs. 100", fecha: "15/08/2019", tipo: "Cédula Electrónica", desc: "Notificación SINOE N° 6475-2019 al demandante con la Resolución N° 01.", html: "<p><strong>CÉDULA DE NOTIFICACIÓN ELECTRÓNICA N° 6475-2019:</strong></p><p>Destinatario: Andrés Leonidas Supo Quispe / Abog. Lino Larico. Casilla SINOE: 60375. Acto procesal: Notificación de la Resolución N° 01 con fecha de depósito 15/08/2019 a las 14:22 hrs.</p>" },
      { num: 8, fojas: "Fjs. 101-104", fecha: "21/08/2019", tipo: "Escrito N° 02", desc: "Subsanación: se fundamenta que el desvío funcional y mando lo ejerció EsSalud.", html: "<p><strong>ESCRITO DE SUBSANACIÓN (REGISTRO N° 2849-2019):</strong></p><p>El actor absuelve traslado señalando que no acciona contra SILSA porque el encubrimiento laboral, mando jerárquico y provecho de labores fue asumido exclusivamente por EsSalud, por lo que opera la desnaturalización patronal directa.</p>" },
      { num: 9, fojas: "Fjs. 105", fecha: "28/08/2019", tipo: "Resolución N° 02", desc: "Admite formalmente la demanda ordinaria laboral y traslada por 10 días a EsSalud.", html: "<p><strong>RESOLUCIÓN NRO. 02:</strong></p><p>Juliaca, 28 de agosto del dos mil diecinueve.-</p><p><strong>AUTOS Y VISTOS:</strong> Con el escrito que antecede; <strong>SE RESUELVE:</strong> Tener por subsanada la demanda; <strong>ADMITIR A TRÁMITE</strong> la demanda en la vía del <strong>PROCESO ORDINARIO LABORAL</strong> conforme a la Ley N° 26636; y <strong>CORRER TRASLADO</strong> a EsSalud Red Juliaca por el término de <strong>DIEZ (10) DÍAS HÁBILES</strong> bajo apercibimiento de rebeldía.</p>" },
      { num: 10, fojas: "Fjs. 106", fecha: "05/09/2019", tipo: "Cédula Electrónica", desc: "Notificación N° 63800-2019 al demandante con la Resolución N° 02.", html: "<p><strong>CÉDULA SINOE N° 63800-2019:</strong> Notificación del admisorio de demanda (Resolución N° 02) en la casilla electrónica N° 60375.</p>" },
      { num: 11, fojas: "Fjs. 107", fecha: "10/09/2019", tipo: "Cédula Física", desc: "Emplazamiento a EsSalud en Av. Santos Chocano S/N, La Capilla, Juliaca.", html: "<p><strong>CÉDULA FÍSICA N° 7304-2019:</strong> Notificación y emplazamiento a EsSalud en su sede de Av. Santos Chocano S/N, Urb. La Capilla, Juliaca, con entrega de copias de demanda y recaudos.</p>" },
      { num: 12, fojas: "Fjs. 108-124+", fecha: "25/09/2019", tipo: "Contestación", desc: "EsSalud contesta la demanda mediante Hernán López Alférez pidiendo infundada.", html: "<p><strong>ESCRITO DE CONTESTACIÓN DE DEMANDA (REGISTRO N° 3461-2019):</strong></p><p>Hernán Rolando López Alférez, apoderado de EsSalud, contesta la demanda solicitando se declare infundada alegando que el actor fue contratado por SILSA y que no existe vacante de Almacenero en el CAP institucional.</p>" }
    ];

    // CONTROL DE PANTALLAS MUTUAMENTE EXCLUYENTES
    function switchScreen(screenNum) {
      var allStages = document.querySelectorAll('.screen-stage');
      for (var i = 0; i < allStages.length; i++) {
        allStages[i].classList.remove('active');
      }

      var target = document.getElementById('pantalla-' + screenNum);
      if (target) {
        target.classList.add('active');
      }
      window.scrollTo(0, 0);

      // Efectos automáticos
      if (screenNum === 1) {
        startSessionTimer();
        runProgressBar('p1-loader-fill', 2);
      } else if (screenNum === 4) {
        runProgressBar('p4-loader-fill', 5);
      } else if (screenNum === 5) {
        renderScreen5Data();
      }
    }

    function runProgressBar(barId, nextScreenNum) {
      var pct = 0;
      var el = document.getElementById(barId);
      el.style.width = '0%';
      var iv = setInterval(function() {
        pct += 20;
        el.style.width = pct + '%';
        if (pct >= 100) {
          clearInterval(iv);
          setTimeout(function() {
            switchScreen(nextScreenNum);
          }, 150);
        }
      }, 50);
    }

    // PANTALLA 2: WORKFLOW DE CAPTCHA Y COMUNICADO
    function triggerCaptchaWorkflow() {
      document.getElementById('captcha-modal-overlay').style.display = 'flex';
      refreshCaptcha();
    }

    function closeCaptchaModal() {
      document.getElementById('captcha-modal-overlay').style.display = 'none';
    }

    function cancelSearchWorkflow() {
      document.getElementById('search-inline-panel').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'block';
    }

    var currentCaptchaValue = "";
    function refreshCaptcha() {
      var chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      var code = "";
      for (var i = 0; i < 5; i++) {
        code += chars.charAt(Math.floor(Math.random() * chars.length));
      }
      currentCaptchaValue = code;
      document.getElementById('captcha-render').innerText = code;
      document.getElementById('captcha-input-txt').value = "";
      document.getElementById('captcha-fail-msg').style.display = 'none';
    }

    function validateCaptchaAndUnlock() {
      var userText = document.getElementById('captcha-input-txt').value.trim().toUpperCase();
      if (userText === currentCaptchaValue) {
        closeCaptchaModal();
        document.getElementById('comunicado-modal').style.display = 'flex';
      } else {
        document.getElementById('captcha-fail-msg').style.display = 'block';
        refreshCaptcha();
      }
    }

    function acceptComunicadoAndShowSearch() {
      document.getElementById('comunicado-modal').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'none';
      document.getElementById('search-inline-panel').style.display = 'block';
    }

    function toggleSearchMode(mode) {
      var btnC = document.getElementById('tab-code-btn');
      var btnP = document.getElementById('tab-party-btn');
      var tabC = document.getElementById('tab-code-content');
      var tabP = document.getElementById('tab-party-content');

      if (mode === 'code') {
        btnC.style.background = '#831034';
        btnC.style.color = 'white';
        btnP.style.background = '#e2e8f0';
        btnP.style.color = '#334155';
        tabC.style.display = 'block';
        tabP.style.display = 'none';
      } else {
        btnP.style.background = '#831034';
        btnP.style.color = 'white';
        btnC.style.background = '#e2e8f0';
        btnC.style.color = '#334155';
        tabP.style.display = 'block';
        tabC.style.display = 'none';
      }
    }

    function showInfoMenu(topic) {
      document.getElementById('temis-blank-box').style.display = 'none';
      document.getElementById('search-inline-panel').style.display = 'none';
      var panel = document.getElementById('info-display-panel');
      panel.style.display = 'block';

      var h = document.getElementById('info-header');
      var p = document.getElementById('info-paragraph');

      if (topic === 'inicio') {
        closeInfoMenu();
      } else if (topic === 'mision') {
        h.innerText = "Misión del Poder Judicial";
        p.innerText = "Administrar Justicia a través de sus órganos jurisdiccionales, garantizando la seguridad jurídica, la tutela jurisdiccional efectiva y el debido proceso.";
      } else if (topic === 'vision') {
        h.innerText = "Visión Institucional";
        p.innerText = "Ser un Poder del Estado moderno, transparente y eficiente, reconocido por brindar una justicia célere, confiable e inclusiva.";
      } else if (topic === 'transparencia') {
        h.innerText = "Transparencia Judicial";
        p.innerText = "Acceso a la información judicial pública, presupuestos, convocatorias y compras de la Corte Superior de Justicia de Puno.";
      } else {
        h.innerText = "Contáctanos";
        p.innerText = "Sede Central Juliaca: Jr. Apurímac / Pumacahua. Módulo Laboral: Jr. Mariano Núñez N° 139. Teléfono: (051) 507000.";
      }
    }

    function closeInfoMenu() {
      document.getElementById('info-display-panel').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'block';
    }

    // MODAL RENIEC
    function openReniecModal() {
      document.getElementById('reniec-modal').style.display = 'flex';
    }
    function closeReniecModal() {
      document.getElementById('reniec-modal').style.display = 'none';
    }

    // MODAL INTEROPERABILIDAD
    function openInteropModal(tipo, nombre, doc, resultado) {
      document.getElementById('interop-tag').innerText = tipo;
      document.getElementById('interop-title').innerText = "Interoperabilidad: " + tipo;
      document.getElementById('interop-subject').innerText = nombre;
      document.getElementById('interop-doc').innerText = doc;
      document.getElementById('interop-result-box').innerHTML = resultado;
      document.getElementById('interop-modal').style.display = 'flex';
    }

    function closeInteropModal() {
      document.getElementById('interop-modal').style.display = 'none';
    }

    // PANTALLA 5: RENDERIZADO DE ESTRUCTURA Y LÍNEA DE TIEMPO
    function renderScreen5Data() {
      // 1. Línea de Tiempo (Hitos Principales)
      var timelineBox = document.getElementById('timeline-flow-list');
      timelineBox.innerHTML = '';
      
      var hitos = [
        DATA_ACTUADOS[0], // Cargo de ingreso
        DATA_ACTUADOS[1], // Demanda
        DATA_ACTUADOS[3], // Redistribución
        DATA_ACTUADOS[5], // Res. 01
        DATA_ACTUADOS[8], // Res. 02
        DATA_ACTUADOS[11] // Contestación
      ];

      for (var t = 0; t < hitos.length; t++) {
        var item = hitos[t];
        var eventDiv = document.createElement('div');
        eventDiv.className = 'timeline-event';
        eventDiv.innerHTML = '<div class="timeline-badge"></div>' +
                             '<div class="timeline-card-content">' +
                             '<div style="display:flex; justify-content:space-between; font-size:11px; margin-bottom:2px;">' +
                             '<strong style="color:#831034;">' + item.tipo + '</strong>' +
                             '<span style="color:#64748b; font-family:monospace;">' + item.fecha + '</span>' +
                             '</div>' +
                             '<div style="font-size:11px; color:#334155; margin-bottom:6px;">' + item.desc + '</div>' +
                             '<div style="display:flex; justify-content:space-between; align-items:center;">' +
                             '<span style="font-size:10px; background:#fce7f3; color:#831034; padding:1px 6px; border-radius:4px; font-family:monospace;">' + item.fojas + '</span>' +
                             '<button onclick="openPdfViewerModal(' + item.num + ')" style="background:#831034; color:white; border:none; padding:3px 8px; border-radius:4px; font-size:10px; cursor:pointer; font-weight:bold;">Ver PDF</button>' +
                             '</div>' +
                             '</div>';
        timelineBox.appendChild(eventDiv);
      }

      // 2. Tabla Desktop de Seguimiento con botón PDF
      var dRows = document.getElementById('acts-table-rows');
      dRows.innerHTML = '';
      for (var i = 0; i < DATA_ACTUADOS.length; i++) {
        var a = DATA_ACTUADOS[i];
        var tr = document.createElement('tr');
        tr.innerHTML = '<td style="text-align:center; font-weight:bold;">' + (a.num < 10 ? '0' + a.num : a.num) + '</td>' +
                       '<td style="font-family:monospace;">' + a.fojas + '</td>' +
                       '<td>' + a.fecha + '</td>' +
                       '<td style="font-weight:bold; color:#831034;">' + a.tipo + '</td>' +
                       '<td style="font-size:11px; color:#475569;">' + a.desc + '</td>' +
                       '<td style="text-align:center;"><button onclick="openPdfViewerModal(' + a.num + ')" style="background:#831034; color:white; border:none; padding:4px 9px; border-radius:4px; font-size:11px; cursor:pointer; display:inline-flex; align-items:center; gap:4px; font-weight:bold;"><svg style=\"width:12px; height:12px;\" viewBox=\"0 0 24 24\" fill=\"none\" stroke=\"currentColor\" stroke-width=\"2\"><path d=\"M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z\"/><polyline points=\"14 2 14 8 20 8\"/></svg> Ver PDF</button></td>';
        dRows.appendChild(tr);
      }

      // 3. Tarjetas Móviles de Seguimiento
      var mCards = document.getElementById('acts-cards-mobile');
      mCards.innerHTML = '';
      for (var j = 0; j < DATA_ACTUADOS.length; j++) {
        var m = DATA_ACTUADOS[j];
        var div = document.createElement('div');
        div.style = "background:#ffffff; border:1px solid var(--mag-border); border-radius:12px; padding:12px; margin-bottom:8px;";
        div.innerHTML = '<div style="display:flex; justify-content:space-between; font-size:10px; margin-bottom:4px;">' +
                        '<span style="background:#fce7f3; color:#831034; font-weight:bold; padding:2px 6px; border-radius:4px;">#' + m.num + '</span>' +
                        '<span>' + m.fojas + '</span>' +
                        '<span style="color:#64748b;">' + m.fecha + '</span>' +
                        '</div>' +
                        '<div style="font-weight:bold; font-size:12px; color:#831034;">' + m.tipo + '</div>' +
                        '<div style="font-size:11px; color:#475569; margin:4px 0 8px;">' + m.desc + '</div>' +
                        '<button onclick="openPdfViewerModal(' + m.num + ')" class="btn-main" style="padding:7px; font-size:11px;"><svg style=\"width:13px; height:13px;\" viewBox=\"0 0 24 24\" fill=\"none\" stroke=\"currentColor\" stroke-width=\"2\"><path d=\"M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z\"/><polyline points=\"14 2 14 8 20 8\"/></svg> Visualizar en PDF</button>';
        mCards.appendChild(div);
      }
    }

    // MODAL VISOR EN FORMATO PDF
    function openPdfViewerModal(num) {
      var act = null;
      for (var i = 0; i < DATA_ACTUADOS.length; i++) {
        if (DATA_ACTUADOS[i].num === num) {
          act = DATA_ACTUADOS[i];
          break;
        }
      }
      if (!act) return;

      document.getElementById('pdf-bar-title').innerText = act.tipo.replace(/\s+/g, '_') + "_" + act.fojas.replace(/\s+/g, '') + ".pdf";
      document.getElementById('pdf-sheet-content').innerHTML = act.html;
      document.getElementById('pdf-modal').style.display = 'flex';
    }

    function closePdfModal() {
      document.getElementById('pdf-modal').style.display = 'none';
    }

    // TEMPORIZADOR DE 7 MINUTOS (420 SEGUNDOS)
    var remainingSeconds = 420;
    var timerTimerId = null;

    function startSessionTimer() {
      if (timerTimerId) clearInterval(timerTimerId);
      remainingSeconds = 420;
      updateTimerUI();
      timerTimerId = setInterval(function() {
        remainingSeconds--;
        updateTimerUI();
        if (remainingSeconds <= 0) {
          clearInterval(timerTimerId);
          document.getElementById('session-timeout-modal').style.display = 'flex';
        }
      }, 1000);
    }

    function resetTimer() {
      remainingSeconds = 420;
      updateTimerUI();
    }

    function updateTimerUI() {
      var m = Math.floor(remainingSeconds / 60);
      var s = remainingSeconds % 60;
      var txt = (m < 10 ? '0' + m : m) + ':' + (s < 10 ? '0' + s : s);
      var span = document.getElementById('timer-text');
      var box = document.getElementById('timer-indicator');
      if (span) span.innerText = txt;
      if (remainingSeconds <= 60 && box) {
        box.classList.add('timer-alert');
      } else if (box) {
        box.classList.remove('timer-alert');
      }
    }

    function forceRestartToScreen0() {
      document.getElementById('session-timeout-modal').style.display = 'none';
      closeCaptchaModal();
      document.getElementById('comunicado-modal').style.display = 'none';
      document.getElementById('reniec-modal').style.display = 'none';
      document.getElementById('interop-modal').style.display = 'none';
      document.getElementById('pdf-modal').style.display = 'none';
      cancelSearchWorkflow();
      switchScreen(0);
    }
  </script>
</body>
</html>
