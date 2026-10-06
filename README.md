<index.html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>CEJ - Expediente Judicial Electrónico | Gobierno Digital e Informático</title>
  
  <style>
    :root {
      --mag-darkest: #1f0212;
      --mag-dark: #4a0418;
      --mag-primary: #831034;
      --mag-vivid: #be185d;
      --mag-rose: #f43f5e;
      --mag-soft: #fdf2f8;
      --mag-border: #fbcfe8;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --bg-white: #ffffff;
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

    /* BARRA SUPERIOR PERMANENTE */
    .permanent-top-header {
      background-color: var(--mag-dark);
      color: #ffffff;
      padding: 8px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 1000;
      box-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }

    .gov-nav-horizontal {
      background-color: var(--mag-darkest);
      display: flex;
      overflow-x: auto;
      padding: 6px 12px;
      gap: 6px;
      position: sticky;
      top: 48px;
      z-index: 999;
    }
    .gov-nav-horizontal::-webkit-scrollbar { display: none; }

    .nav-item-btn {
      background: transparent;
      border: none;
      color: #fbcfe8;
      padding: 6px 12px;
      font-size: 12px;
      font-weight: 600;
      cursor: pointer;
      border-radius: 6px;
      white-space: nowrap;
      transition: all 0.2s;
    }
    .nav-item-btn:hover, .nav-item-btn.active {
      background: rgba(255, 255, 255, 0.15);
      color: #ffffff;
    }

    .lang-switcher {
      display: flex;
      gap: 4px;
      background: rgba(0,0,0,0.25);
      padding: 2px 4px;
      border-radius: 6px;
    }
    .btn-lang {
      background: transparent;
      border: none;
      color: #fbcfe8;
      font-size: 10px;
      font-weight: 800;
      padding: 2px 6px;
      border-radius: 4px;
      cursor: pointer;
    }
    .btn-lang.active {
      background: var(--mag-vivid);
      color: white;
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

    .btn-main {
      background: linear-gradient(90deg, #831034, #be185d);
      color: #ffffff;
      border: none;
      padding: 12px 20px;
      border-radius: 12px;
      font-weight: 700;
      font-size: 13px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      width: 100%;
      transition: all 0.25s ease;
      box-shadow: 0 4px 12px rgba(190, 24, 93, 0.3);
    }
    .btn-main:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(190, 24, 93, 0.4);
    }

    /* BOTONES DE INTEROPERABILIDAD DINÁMICOS CON MOVIMIENTO */
    .btn-interop {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 7px 12px;
      border-radius: 8px;
      font-size: 11px;
      font-weight: 700;
      border: none;
      cursor: pointer;
      color: #ffffff;
      transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: 0 2px 6px rgba(0,0,0,0.15);
      position: relative;
      overflow: hidden;
    }
    .btn-interop:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 6px 14px rgba(0,0,0,0.25);
    }
    .btn-interop:active { transform: translateY(0) scale(0.98); }
    
    .btn-reniec { background: linear-gradient(135deg, #0284c7, #0369a1); }
    .btn-migra { background: linear-gradient(135deg, #d97706, #b45309); }
    .btn-pnp { background: linear-gradient(135deg, #059669, #047857); }
    .btn-inpe { background: linear-gradient(135deg, #dc2626, #b91c1c); }

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
      transition: transform 0.2s;
    }
    .timeline-event:hover { transform: translateX(4px); }
    .timeline-badge {
      position: absolute;
      left: -33px;
      top: 4px;
      width: 18px;
      height: 18px;
      border-radius: 50%;
      background: #be185d;
      border: 3px solid #ffffff;
      box-shadow: 0 0 0 2px #be185d;
      animation: pulseNode 2s infinite;
    }
    @keyframes pulseNode {
      0%, 100% { box-shadow: 0 0 0 2px #be185d; }
      50% { box-shadow: 0 0 0 5px rgba(190, 24, 93, 0.35); }
    }

    .timeline-card-content {
      background: #fdf2f8;
      border: 1px solid var(--mag-border);
      border-radius: 12px;
      padding: 10px 14px;
    }

    /* VISOR PDF SIMULADO */
    .pdf-viewer-bar {
      background: #334155;
      color: white;
      padding: 8px 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
    }
    .pdf-body-paper {
      background: #ffffff;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      margin: 16px auto;
      max-width: 580px;
      padding: 30px;
      font-family: Georgia, serif;
      font-size: 13px;
      line-height: 1.6;
      border: 1px solid #cbd5e1;
    }

    /* CHATBOT IURISNIANO FLOTANTE */
    #chatbot-bubble-btn {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: linear-gradient(135deg, #831034, #be185d);
      color: white;
      width: 56px;
      height: 56px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 6px 20px rgba(190, 24, 93, 0.4);
      cursor: pointer;
      z-index: 3000;
      transition: all 0.3s;
    }
    #chatbot-bubble-btn:hover {
      transform: scale(1.08) rotate(5deg);
    }
    #chatbot-window {
      position: fixed;
      bottom: 85px;
      right: 20px;
      width: 330px;
      max-width: 90vw;
      height: 420px;
      background: #ffffff;
      border-radius: 16px;
      border: 1px solid var(--mag-border);
      box-shadow: 0 10px 30px rgba(0,0,0,0.25);
      display: none;
      flex-direction: column;
      z-index: 3000;
      overflow: hidden;
    }

    /* MODAL */
    .modal-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(36, 3, 21, 0.78);
      backdrop-filter: blur(3px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 14px;
      z-index: 2500;
    }
    .modal-card {
      background: #ffffff;
      border-radius: 18px;
      max-width: 650px;
      width: 100%;
      max-height: 85vh;
      overflow-y: auto;
      border: 1px solid var(--mag-border);
    }
    
    .timer-pill {
      background: var(--mag-darkest);
      border: 1px solid #831034;
      color: #fce7f3;
      padding: 4px 8px;
      border-radius: 6px;
      font-family: monospace;
      font-size: 11px;
    }
  </style>
</head>
<body>

  <!-- BARRA DE MENÚ PERMANENTE SUPERIOR -->
  <header class="permanent-top-header">
    <div style="display: flex; align-items: center; gap: 8px;">
      <svg style="width: 22px; height: 22px; color: #fbcfe8;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M3 21h18"/><path d="M3 10h18"/><path d="M5 10v11"/><path d="M19 10v11"/><path d="M9 10v11"/><path d="M15 10v11"/><path d="M12 2 2 7h20L12 2z"/>
      </svg>
      <div>
        <div style="font-size: 8px; font-weight: 800; color: #fbcfe8; letter-spacing: 0.5px;">PODER JUDICIAL DEL PERÚ</div>
        <div id="ui-system-title" style="font-size: 12px; font-weight: 700;">CEJ Electrónico - Puno</div>
      </div>
    </div>

    <div style="display: flex; align-items: center; gap: 8px;">
      <!-- Selector de Idiomas -->
      <div class="lang-switcher">
        <button id="btn-es" onclick="setLanguage('es')" class="btn-lang active">ES</button>
        <button id="btn-en" onclick="setLanguage('en')" class="btn-lang">EN</button>
      </div>

      <!-- Temporizador de 7 min -->
      <div class="timer-pill">
        <span id="ui-timer-lbl">Sesión:</span> <strong id="timer-text">07:00</strong>
      </div>
    </div>
  </header>

  <!-- NAVEGACIÓN HORIZONTAL PERMANENTE -->
  <nav class="gov-nav-horizontal">
    <button onclick="switchScreen(0)" class="nav-item-btn" id="nav-btn-home">Inicio</button>
    <button onclick="showInfoMenu('mision')" class="nav-item-btn" id="nav-btn-mision">Misión</button>
    <button onclick="showInfoMenu('vision')" class="nav-item-btn" id="nav-btn-vision">Visión</button>
    <button onclick="showInfoMenu('transparencia')" class="nav-item-btn" id="nav-btn-transp">Transparencia</button>
    <button onclick="showInfoMenu('contactanos')" class="nav-item-btn" id="nav-btn-contact">Contáctanos</button>
    <button onclick="triggerCaptchaWorkflow()" class="nav-item-btn" style="margin-left:auto; background:#be185d; color:white; font-weight:bold;" id="nav-btn-search">🔍 Búsqueda de Expediente</button>
  </nav>

  <!-- CONTENEDOR PRINCIPAL DE PANTALLAS -->
  <div style="flex-grow: 1; display: flex; flex-direction: column;">

    <!-- ========================================== -->
    <!-- PANTALLA 0: BIENVENIDA (ESTÁTICA CON TEMIS)-->
    <!-- ========================================== -->
    <div id="pantalla-0" class="screen-stage active center-content">
      <div class="card-academic">
        <div style="background: linear-gradient(135deg, #4a0418, #be185d); color: white; padding: 24px;">
          <!-- Temis en el centro -->
          <div style="margin: 0 auto 10px; width: 100px; height: 100px; background: rgba(255,255,255,0.12); border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid #fbcfe8;">
            <svg style="width: 70px; height: 70px;" viewBox="0 0 200 200" fill="none">
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
          <h1 id="p0-title" style="font-size: 18px; font-weight: 800;">SISTEMA DE CONSULTA DE EXPEDIENTES (CEJ / EJE)</h1>
          <p id="p0-sub" style="font-size: 12px; color: #fce7f3; margin-top: 4px;">Simulación Jurisdiccional para Derecho e Informática</p>
        </div>

        <div style="padding: 20px; text-align: left;">
          <div style="background: #fdf2f8; border: 1px solid var(--mag-border); border-radius: 12px; padding: 12px; margin-bottom: 14px; font-size: 12px;">
            <div><span style="color: var(--text-muted);" id="lbl-student">Estudiante:</span> <strong style="color: var(--mag-primary);">Sonia Pilar Condori Ruelas</strong></div>
            <div style="margin: 4px 0;"><span style="color: var(--text-muted);" id="lbl-course">Curso:</span> <strong style="color: var(--mag-dark);">Gobierno Digital e Informático</strong></div>
            <div><span style="color: var(--text-muted);" id="lbl-teacher">Docente:</span> <strong style="color: var(--mag-dark);">Dr. Michael Espinoza Coila</strong></div>
          </div>

          <div style="background: #fff1f2; border-left: 4px solid #be185d; padding: 8px 12px; border-radius: 6px; margin-bottom: 16px;">
            <p id="p0-warning" style="font-size: 11px; color: #4a0418; line-height: 1.4; font-weight: 600;">
              AVISO: El presente trabajo es un producto netamente académico y NO es un sitio oficial del Poder Judicial del Perú.
            </p>
          </div>

          <button onclick="switchScreen(1)" class="btn-main" id="btn-enter-system">
            <span>Ingresar al Sistema</span> →
          </button>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 1: PANTALLA DE CARGA 1            -->
    <!-- ========================================== -->
    <div id="pantalla-1" class="screen-stage center-content">
      <div style="max-width: 340px; width: 100%; text-align: center;">
        <svg style="width: 44px; height: 44px; color: #831034; margin-bottom: 12px; animation: spin 2s linear infinite;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
        </svg>
        <h3 id="p1-title" style="font-size: 15px; font-weight: 700; color: #4a0418;">Iniciando Portal Institucional</h3>
        <p id="p1-desc" style="font-size: 12px; color: #64748b; margin-top: 4px;">Cargando módulos de Gobierno Digital...</p>
        <div style="background: #fce7f3; height: 7px; border-radius: 8px; overflow: hidden; margin-top: 14px;">
          <div id="p1-loader-fill" style="height: 100%; background: linear-gradient(90deg, #831034, #be185d); width: 0%; transition: width 0.1s linear;"></div>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 2: PRINCIPAL Y BÚSQUEDA           -->
    <!-- ========================================== -->
    <div id="pantalla-2" class="screen-stage">
      <div style="max-width: 1100px; width: 100%; margin: 20px auto; padding: 0 16px; flex-grow: 1; display: flex; flex-direction: column; justify-content: center;">
        
        <!-- Temis interactiva -->
        <div id="temis-blank-box" onclick="triggerCaptchaWorkflow()" style="background: white; border: 1px solid var(--mag-border); border-radius: 18px; text-align: center; padding: 36px 16px; cursor: pointer;">
          <svg style="width: 120px; height: 120px; margin: 0 auto 12px; display: block;" viewBox="0 0 200 200" fill="none">
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
          <h2 id="p2-temis-title" style="font-size: 18px; color: #4a0418; font-weight: 800;">Consulta de Expedientes Judiciales (CEJ)</h2>
          <p id="p2-temis-desc" style="font-size: 13px; color: #64748b; max-width: 480px; margin: 8px auto 14px;">
            Haga clic en este recuadro o en el menú para validar el CAPTCHA y buscar su expediente.
          </p>
          <span id="p2-temis-btn" style="font-size: 11px; background: #be185d; color: white; padding: 6px 14px; border-radius: 20px; font-weight: bold; display: inline-block;">
            Clic aquí para desbloquear búsqueda
          </span>
        </div>

        <!-- Formulario de Búsqueda tras CAPTCHA y Comunicado -->
        <div id="search-inline-panel" style="display: none; background: white; border: 1px solid var(--mag-border); border-radius: 18px; padding: 20px; max-width: 600px; margin: 0 auto; width: 100%;">
          <div style="background: #4a0418; color: white; padding: 12px 16px; border-radius: 12px 12px 0 0; margin: -20px -20px 16px; display: flex; justify-content: space-between; align-items: center;">
            <strong id="search-form-title" style="font-size: 13px;">Búsqueda Jurisdiccional de Causas</strong>
            <button onclick="cancelSearchWorkflow()" style="background: none; border: none; color: #fbcfe8; cursor: pointer; font-size: 16px;">✕</button>
          </div>

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

          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 10px; border-radius: 8px; font-size: 12px; margin-bottom: 16px;">
            Expediente asignado: <strong style="color: #831034;">00174-2019-0-2111-JR-LA-02</strong> (EsSalud vs Supo)
          </div>

          <button onclick="switchScreen(4)" class="btn-main" id="btn-submit-search">
            <span>Consultar Expediente Judicial</span> →
          </button>
        </div>

      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 4: PANTALLA DE CARGA 2            -->
    <!-- ========================================== -->
    <div id="pantalla-4" class="screen-stage center-content">
      <div style="max-width: 340px; width: 100%; text-align: center;">
        <svg style="width: 44px; height: 44px; color: #be185d; margin-bottom: 12px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1-2.5-2.5Z"/><path d="M6 6h10"/><path d="M6 10h10"/>
        </svg>
        <h3 id="p4-title" style="font-size: 15px; font-weight: 700; color: #4a0418;">Indexando Cuaderno Laboral Digital</h3>
        <p id="p4-desc" style="font-size: 12px; color: #64748b; margin-top: 4px;">Recuperando resoluciones y línea de tiempo...</p>
        <div style="background: #fce7f3; height: 7px; border-radius: 8px; overflow: hidden; margin-top: 14px;">
          <div id="p4-loader-fill" style="height: 100%; background: linear-gradient(90deg, #831034, #be185d); width: 0%; transition: width 0.1s linear;"></div>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 5: EXPEDIENTE COMPLETO ESTRUCTURADO-->
    <!-- ========================================== -->
    <div id="pantalla-5" class="screen-stage">
      <div style="max-width: 1100px; width: 100%; margin: 16px auto; padding: 0 16px; flex-grow: 1;">
        
        <!-- I. REPORTE DE EXPEDIENTE -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px;">
          <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-i-title" style="color: var(--mag-primary); font-size: 13px;">I. REPORTE DE EXPEDIENTE</strong>
            <span style="font-family: monospace; font-size: 11px; background: #fdf2f8; padding: 2px 6px; border-radius: 4px; color: #831034;">EXP: 00174-2019-0-2111-JR-LA-02</span>
          </div>
          <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; font-size: 12px;">
            <div><span style="color: #64748b; display: block;" id="f-dist">Distrito Judicial / Sede:</span> <strong>Puno / San Román – Juliaca</strong></div>
            <div><span style="color: #64748b; display: block;" id="f-court">Juzgado:</span> <strong>Juzgado de Trabajo – Zona Norte</strong></div>
            <div><span style="color: #64748b; display: block;" id="f-judge">Juez a Cargo:</span> <strong>Huamán Romero, Gonzalo Víctor</strong></div>
            <div><span style="color: #64748b; display: block;" id="f-sec">Secretaria Judicial:</span> <strong>Carlos Villán, Rosario</strong></div>
            <div><span style="color: #64748b; display: block;" id="f-mat">Materia Procesal:</span> <strong style="color: #831034;">Desnaturalización Laboral (Ley 26636)</strong></div>
          </div>
        </div>

        <!-- II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px;">
          <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-ii-title" style="color: var(--mag-primary); font-size: 13px;">II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO</strong>
            <span style="font-size: 11px; color: #047857; font-weight: bold; background: #ecfdf5; padding: 2px 8px; border-radius: 4px;">Etapa: Postulatoria</span>
          </div>

          <!-- Barra de Proceso -->
          <div style="display: flex; justify-content: space-between; margin: 10px 0 16px; font-size: 11px; text-align: center;">
            <div style="flex:1;"><div style="width:24px; height:24px; border-radius:50%; background:#831034; color:white; margin:0 auto 4px; display:flex; align-items:center; justify-content:center;">✓</div><strong>Postulatoria</strong></div>
            <div style="flex:1;"><div style="width:24px; height:24px; border-radius:50%; background:#be185d; color:white; margin:0 auto 4px; display:flex; align-items:center; justify-content:center;">2</div><strong>Probatoria</strong></div>
            <div style="flex:1;"><div style="width:24px; height:24px; border-radius:50%; background:#cbd5e1; color:#64748b; margin:0 auto 4px; display:flex; align-items:center; justify-content:center;">3</div><span style="color:#94a3b8;">Decisoria</span></div>
            <div style="flex:1;"><div style="width:24px; height:24px; border-radius:50%; background:#cbd5e1; color:#64748b; margin:0 auto 4px; display:flex; align-items:center; justify-content:center;">4</div><span style="color:#94a3b8;">Ejecución</span></div>
          </div>

          <!-- Línea de tiempo -->
          <div class="timeline-container" id="timeline-flow-list"></div>
        </div>

        <!-- III. PARTES PROCESALES CON BOTONES DINÁMICOS -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px;">
          <div style="border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-iii-title" style="color: var(--mag-primary); font-size: 13px;">III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)</strong>
          </div>

          <!-- Demandante -->
          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; border-radius: 12px; padding: 12px; margin-bottom: 12px;">
            <div style="font-weight: bold; font-size: 13px; color: #831034;">DEMANDANTE: Andrés Leonidas Supo Quispe (DNI 02167445)</div>
            <div style="font-size: 11px; color: #64748b; margin: 4px 0 10px;">Abog. Lino Larico Larico (Reg. CAP 47) | Casilla SINOE: 60375</div>
            
            <!-- Botones dinámicos con iconos -->
            <div style="display: flex; flex-wrap: wrap; gap: 8px;">
              <button onclick="openReniecModal('Andrés Leonidas Supo Quispe', '02167445')" class="btn-interop btn-reniec">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC (Identidad Protegida)</span>
              </button>
              <button onclick="openStandardInterop('MIGRACIONES', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'Sin impedimento de salida del país. Pasaporte ordinario válido.')" class="btn-interop btn-migra">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="m4.93 4.93 4.24 4.24"/><path d="m14.83 9.17 4.24-4.24"/></svg>
                <span>MIGRACIONES</span>
              </button>
              <button onclick="openStandardInterop('PNP', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'ESINPOL: NO REGISTRA ORDEN DE CAPTURA NI REQUISITORIA VIGENTE.')" class="btn-interop btn-pnp">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
                <span>PNP (Requisitorias)</span>
              </button>
              <button onclick="openStandardInterop('INPE', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'REGISTRO PENAL: NO REGISTRA ANTECEDENTES PENITENCIARIOS.')" class="btn-interop btn-inpe">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="18" height="18" x="3" y="3" rx="2"/><path d="M3 9h18"/><path d="M9 21V9"/></svg>
                <span>INPE (Penales)</span>
              </button>
            </div>
          </div>

          <!-- Demandada -->
          <div style="background: #fff1f2; border: 1px solid #fecdd3; border-radius: 12px; padding: 12px;">
            <div style="font-weight: bold; font-size: 13px; color: #e11d48;">DEMANDADA: Seguro Social de Salud - EsSalud (RUC 20131257750)</div>
            <div style="font-size: 11px; color: #64748b; margin: 4px 0 10px;">Apoderado: Abog. Hernán Rolando López Alférez (DNI 01207861) | Casilla: 59629</div>
            <div style="display: flex; gap: 8px;">
              <button onclick="openReniecModal('Hernán Rolando López Alférez', '01207861')" class="btn-interop btn-reniec">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC (Apoderado)</span>
              </button>
            </div>
          </div>
        </div>

        <!-- IV. SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES EN PDF) -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 20px;">
          <div style="border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-iv-title" style="color: var(--mag-primary); font-size: 13px;">IV. SEGUIMIENTO DEL EXPEDIENTE (NOTIFICACIONES Y RESOLUCIONES)</strong>
          </div>
          <table style="width: 100%; border-collapse: collapse; font-size: 12px;">
            <thead>
              <tr style="background: #4a0418; color: white;">
                <th style="padding: 8px;">N°</th>
                <th style="padding: 8px;">Fojas</th>
                <th style="padding: 8px;">Fecha</th>
                <th style="padding: 8px;">Documento</th>
                <th style="padding: 8px;">Acción</th>
              </tr>
            </thead>
            <tbody id="acts-table-body"></tbody>
          </table>
        </div>

      </div>
    </div>

  </div>

  <!-- ========================================== -->
  <!-- MODAL: RENIEC CON FOTO Y DATOS CENSURADOS  -->
  <!-- ========================================== -->
  <div id="reniec-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 520px; padding: 20px;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #0284c7; padding-bottom: 8px; margin-bottom: 14px;">
        <div style="font-weight: 800; color: #0284c7; font-size: 14px;">RENIEC - CONSULTA REGISTRAL EN LÍNEA</div>
        <button onclick="closeModal('reniec-modal')" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>

      <!-- Ficha de Identidad -->
      <div style="display: flex; gap: 14px; background: #f8fafc; border: 1px solid #e2e8f0; padding: 14px; border-radius: 10px;">
        <!-- Fotografía Simulada -->
        <div style="width: 110px; height: 130px; background: #e2e8f0; border: 2px solid #94a3b8; border-radius: 6px; display: flex; flex-direction: column; align-items: center; justify-content: center; position: relative; overflow: hidden;">
          <svg style="width: 60px; height: 60px; color: #64748b;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/>
          </svg>
          <span style="font-size: 9px; color: #475569; font-weight: bold; margin-top: 4px;">FOTO RENIEC</span>
          <!-- Franja de seguridad -->
          <div style="position: absolute; bottom: 0; width: 100%; background: rgba(2, 132, 199, 0.85); color: white; font-size: 8px; text-align: center; padding: 1px;">VERIFICADO</div>
        </div>

        <!-- Datos con censura para protección de datos personales -->
        <div style="flex-grow: 1; font-size: 11px; line-height: 1.6;">
          <div><span style="color: #64748b;">Nombres:</span> <strong id="reniec-nom">ANDRES ********</strong></div>
          <div><span style="color: #64748b;">Apellidos:</span> <strong id="reniec-ape">SUPO ********</strong></div>
          <div><span style="color: #64748b;">DNI:</span> <strong id="reniec-dni">0216****</strong></div>
          <div><span style="color: #64748b;">Fecha Nacimiento:</span> <strong>14/08/19**</strong></div>
          <div><span style="color: #64748b;">Ubigeo:</span> <strong>211101 (JULIACA - PUNO)</strong></div>
          <div><span style="color: #64748b;">Dirección Domiciliaria:</span> <strong>AV. MANCO CAPAC N° 9** (CENSURADO)</strong></div>
          <div><span style="color: #64748b;">Restricción Legal:</span> <span style="color: #059669; font-weight: bold;">NINGUNA</span></div>
        </div>
      </div>

      <div style="background: #eff6ff; border: 1px solid #bfdbfe; padding: 8px 10px; border-radius: 6px; font-size: 10px; color: #1e40af; margin-top: 10px;">
        * Medida técnica de protección: Datos anonimizados con asteriscos conforme a la Ley N° 29733 (Ley de Protección de Datos Personales).
      </div>
    </div>
  </div>

  <!-- ========================================== -->
  <!-- MODAL: VISOR DE RESOLUCIONES TIPO PDF      -->
  <!-- ========================================== -->
  <div id="pdf-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 680px; background: #e2e8f0;">
      <!-- Barra superior PDF -->
      <div class="pdf-viewer-bar">
        <span id="pdf-filename">Resolucion_01_2019.pdf</span>
        <div style="display: flex; gap: 8px;">
          <button onclick="alert('Descarga simulada del documento judicial')" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">💾 Descargar</button>
          <button onclick="window.print()" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">🖨️ Imprimir</button>
          <button onclick="closeModal('pdf-modal')" style="background: #ef4444; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">✕</button>
        </div>
      </div>

      <!-- Hoja PDF -->
      <div class="pdf-body-paper" id="pdf-paper-content">
        <!-- Contenido inyectado -->
      </div>
    </div>
  </div>

  <!-- ========================================== -->
  <!-- MODAL: COMUNICADO MINJUSDH                 -->
  <!-- ========================================== -->
  <div id="comunicado-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 480px; padding: 22px;">
      <h3 style="color: #4a0418; font-size: 15px; font-weight: 800; margin-bottom: 10px;">COMUNICADO OFICIAL</h3>
      <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 12px; border-radius: 8px; font-size: 12px; line-height: 1.6; color: #334155; text-align: justify; margin-bottom: 14px;">
        A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la <strong>Autoridad Nacional de Protección de Datos Personales</strong> y la <strong>Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH</strong>. Al amparo de la <strong>Ley N° 29733</strong>, Ley de Protección de Datos Personales.
      </div>
      <button onclick="acceptComunicado()" class="btn-main">He leído y Acepto el Comunicado</button>
    </div>
  </div>

  <!-- ========================================== -->
  <!-- MODAL: CAPTCHA FLOTANTE                    -->
  <!-- ========================================== -->
  <div id="captcha-modal" class="modal-overlay">
    <div class="modal-card" style="max-width: 420px; padding: 22px;">
      <h3 style="color: #4a0418; font-size: 15px; font-weight: bold; margin-bottom: 10px;">Seguridad CAPTCHA</h3>
      <div style="display: flex; gap: 8px; align-items: center; margin-bottom: 12px;">
        <div id="captcha-code" style="background: #240315; color: #fbcfe8; font-family: monospace; font-size: 20px; font-weight: 800; letter-spacing: 4px; padding: 8px 14px; border-radius: 8px; text-decoration: line-through;">
          8M4X1
        </div>
        <button onclick="generateCaptcha()" style="padding: 8px 12px; border: 1px solid #cbd5e1; border-radius: 6px; cursor: pointer; background: white;">↻</button>
        <input type="text" id="captcha-input" placeholder="Código" style="flex-grow: 1; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-transform: uppercase; font-weight: bold;">
      </div>
      <button onclick="validateCaptcha()" class="btn-main">Validar y Continuar</button>
      <div id="captcha-err" style="display: none; color: #e11d48; font-size: 11px; margin-top: 6px; text-align: center;">Código incorrecto. Intente de nuevo.</div>
    </div>
  </div>

  <!-- ========================================== -->
  <!-- CHATBOT FLOTANTE: IURISNIANO               -->
  <!-- ========================================== -->
  <div id="chatbot-bubble-btn" onclick="toggleChatbot()" title="Habla con Iurisniano">
    <svg style="width:28px; height:28px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
    </svg>
  </div>

  <div id="chatbot-window">
    <div style="background: linear-gradient(135deg, #4a0418, #be185d); color: white; padding: 12px 14px; display: flex; justify-content: space-between; align-items: center;">
      <div style="display: flex; align-items: center; gap: 8px;">
        <div style="width: 28px; height: 28px; background: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; color: #831034; font-weight: bold; font-size: 12px;">⚖️</div>
        <div>
          <strong style="font-size: 13px;">IURISNIANO</strong>
          <div style="font-size: 9px; color: #fce7f3;">Tu asistente judicial amigable</div>
        </div>
      </div>
      <button onclick="toggleChatbot()" style="background: none; border: none; color: white; font-size: 16px; cursor: pointer;">✕</button>
    </div>

    <div id="chatbot-messages" style="flex-grow: 1; padding: 12px; overflow-y: auto; font-size: 12px; display: flex; flex-direction: column; gap: 8px; background: #fdf2f8;">
      <div style="background: #ffffff; padding: 8px 12px; border-radius: 12px; border: 1px solid var(--mag-border); max-width: 85%; align-self: flex-start;">
        ¡Hola! 👋 Soy <strong>Iurisniano</strong>, tu asistente legal del expediente. Puedes preguntarme sobre fojas, resoluciones, el juez del caso o dónde está la demanda. ¿En qué te ayudo hoy?
      </div>
    </div>

    <div style="padding: 8px; border-top: 1px solid #e2e8f0; display: flex; gap: 6px; background: white;">
      <input type="text" id="chatbot-input" placeholder="Pregúntale a Iurisniano..." style="flex-grow: 1; padding: 7px 10px; border: 1px solid #cbd5e1; border-radius: 8px; font-size: 11px;" onkeypress="if(event.key==='Enter') sendChatMsg()">
      <button onclick="sendChatMsg()" style="background: #831034; color: white; border: none; padding: 6px 12px; border-radius: 8px; font-size: 11px; cursor: pointer; font-weight: bold;">Enviar</button>
    </div>
  </div>

  <!-- SCRIPT LOGIC -->
  <script>
    // DATOS DE SEGUIMIENTO (12 ACTUADOS)
    var ACTS = [
      { n: 1, f: "Fjs. 1-2", d: "26/06/2019", t: "Cargo / Carátula", des: "Ingreso en Mesa de Partes Única de Juliaca.", pdfTitle: "Carátula de Ingreso CDG N° 00174-2019", pdfBody: "<p><strong>PODER JUDICIAL DEL PERÚ - CORTE DE PUNO</strong></p><p>Expediente: 00174-2019-0-2111-JR-LA-02</p><p>Materia: Desnaturalización de Contrato</p><p>Ingreso: 26/06/2019 11:31:38 - Fojas: 26</p>" },
      { n: 2, f: "Fjs. 2-26", d: "26/06/2019", t: "Escrito N° 01 (Demanda)", des: "Demanda laboral ordinaria de desnaturalización.", pdfTitle: "Escrito 01 - Demanda Laboral", pdfBody: "<p><strong>SEÑOR JUEZ DE TRABAJO DE SAN ROMÁN:</strong></p><p>Andrés Leonidas Supo Quispe solicita se declare la desnaturalización de la intermediación laboral prestada a EsSalud mediante SILSA y se ordene la inclusión en planillas a plazo indeterminado (D. Leg. 728).</p>" },
      { n: 3, f: "Fjs. 26-96", d: "26/06/2019", t: "Recepción de Recaudos", des: "Ingreso formal de medios adjuntos a la demanda.", pdfTitle: "Recepción de Instrumental", pdfBody: "<p>Recepción de medios probatorios adjuntos en Mesa de Partes para calificación de admisibilidad.</p>" },
      { n: 4, f: "Fjs. 97", d: "11/07/2019", t: "Redistribución", des: "Pasa al Juzgado de Trabajo Zona Norte.", pdfTitle: "Oficio de Redistribución", pdfBody: "<p>Cúmplase con la Res. Adm. N° 232-2019-CE-PJ derivando la causa laboral al Juzgado Especializado de Trabajo - Sede Juliaca.</p>" },
      { n: 5, f: "Fjs. 98", d: "12/07/2019", t: "Razón de Secretaría", des: "Secretaria Rosario Carlos Villán asume causa.", pdfTitle: "Razón de Secretaría", pdfBody: "<p>Doy cuenta a fojas 98 que asumo funciones de especialista legal de causa. Rosario Carlos Villán.</p>" },
      { n: 6, f: "Fjs. 99", d: "13/08/2019", t: "Resolución N° 01", des: "Admisorio provisional: concede 3 días.", pdfTitle: "Resolución N° 01 - Admisorio Provisional", pdfBody: "<p><strong>JUZGADO DE TRABAJO ZONA NORTE - JULIACA</strong></p><p>RESOLUCIÓN NRO. 01 (13/08/2019)</p><p>SE RESUELVE: Declarar ADMISIBLE PROVISIONALMENTE la demanda y conceder tres días al actor para pronunciarse sobre SILSA. Juez: Huamán Romero.</p>" },
      { n: 7, f: "Fjs. 100", d: "15/08/2019", t: "Cédula Electrónica", des: "Notificación SINOE N° 6475-2019.", pdfTitle: "Cédula SINOE N° 6475-2019", pdfBody: "<p>Notificado válidamente a la casilla electrónica 60375 del demandante.</p>" },
      { n: 8, f: "Fjs. 101-104", d: "21/08/2019", t: "Escrito N° 02", des: "Subsanación: mando ejercido por EsSalud.", pdfTitle: "Escrito 02 - Absuelve Traslado", pdfBody: "<p>El accionante absuelve traslado señalando que el provecho directo del servicio y el poder de dirección lo ejerció la empresa usuaria EsSalud.</p>" },
      { n: 9, f: "Fjs. 105", d: "28/08/2019", t: "Resolución N° 02", des: "Admite formalmente la demanda a trámite.", pdfTitle: "Resolución N° 02 - Auto Admisorio", pdfBody: "<p><strong>RESOLUCIÓN NRO. 02 (28/08/2019)</strong></p><p>SE RESUELVE: Tener por subsanada la demanda y ADMITIR A TRÁMITE en la vía ordinaria laboral. Córrase traslado a EsSalud por diez días bajo apercibimiento de rebeldía.</p>" },
      { n: 10, f: "Fjs. 106", d: "05/09/2019", t: "Cédula Electrónica", des: "Notificación SINOE N° 63800-2019.", pdfTitle: "Cédula SINOE N° 63800-2019", pdfBody: "<p>Notificación electrónica formal del admisorio de la demanda al actor.</p>" },
      { n: 11, f: "Fjs. 107", d: "10/09/2019", t: "Cédula Física", des: "Emplazamiento formal a EsSalud Juliaca.", pdfTitle: "Cédula de Emplazamiento N° 7304-2019", pdfBody: "<p>Emplazamiento presencial a EsSalud en Av. Santos Chocano S/N, La Capilla, Juliaca.</p>" },
      { n: 12, f: "Fjs. 108-124+", d: "25/09/2019", t: "Contestación", des: "EsSalud contesta mediante apoderado.", pdfTitle: "Contestación de Demanda - EsSalud", pdfBody: "<p>EsSalud se apersona mediante Hernán López Alférez, señala casilla 59629 y solicita declarar infundada la demanda alegando falta de vacante en el CAP.</p>" }
    ];

    // CONTROL DE PANTALLAS
    function switchScreen(screenNum) {
      document.querySelectorAll('.screen-stage').forEach(el => el.classList.remove('active'));
      const target = document.getElementById('pantalla-' + screenNum);
      if (target) target.classList.add('active');
      window.scrollTo(0, 0);

      if (screenNum === 1) runLoader('p1-loader-fill', 2);
      if (screenNum === 4) runLoader('p4-loader-fill', 5);
      if (screenNum === 5) renderScreen5();
    }

    function runLoader(barId, nextScreen) {
      let p = 0;
      const el = document.getElementById(barId);
      el.style.width = '0%';
      const iv = setInterval(() => {
        p += 20;
        el.style.width = p + '%';
        if (p >= 100) {
          clearInterval(iv);
          setTimeout(() => switchScreen(nextScreen), 150);
        }
      }, 50);
    }

    // WORKFLOW DE BÚSQUEDA
    function triggerCaptchaWorkflow() {
      openModal('captcha-modal');
      generateCaptcha();
    }

    function validateCaptcha() {
      const val = document.getElementById('captcha-input').value.trim().toUpperCase();
      if (val === currentCaptcha) {
        closeModal('captcha-modal');
        openModal('comunicado-modal');
      } else {
        document.getElementById('captcha-err').style.display = 'block';
        generateCaptcha();
      }
    }

    function acceptComunicado() {
      closeModal('comunicado-modal');
      switchScreen(2);
      document.getElementById('temis-blank-box').style.display = 'none';
      document.getElementById('search-inline-panel').style.display = 'block';
    }

    function cancelSearchWorkflow() {
      document.getElementById('search-inline-panel').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'block';
    }

    // CAPTCHA
    let currentCaptcha = "";
    function generateCaptcha() {
      const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      let code = "";
      for (let i = 0; i < 5; i++) code += chars.charAt(Math.floor(Math.random() * chars.length));
      currentCaptcha = code;
      document.getElementById('captcha-code').innerText = code;
      document.getElementById('captcha-input').value = "";
      document.getElementById('captcha-err').style.display = 'none';
    }

    // MODALES
    function openModal(id) { document.getElementById(id).style.display = 'flex'; }
    function closeModal(id) { document.getElementById(id).style.display = 'none'; }

    // INTEROPERABILIDAD RENIEC (CENSURADA)
    function openReniecModal(nom, dni) {
      document.getElementById('reniec-nom').innerText = nom.split(' ')[0] + " ********";
      document.getElementById('reniec-ape').innerText = (nom.split(' ')[1] || 'QUISPE') + " ********";
      document.getElementById('reniec-dni').innerText = dni.substring(0, 4) + "****";
      openModal('reniec-modal');
    }

    function openStandardInterop(tipo, nom, doc, desc) {
      alert(`[INTEROPERABILIDAD - ${tipo}]\n\nSujeto: ${nom}\nDocumento: ${doc}\n\nResultado Oficial:\n${desc}`);
    }

    // VISOR PDF
    function openPdfDoc(num) {
      const act = ACTS.find(a => a.n === num);
      if (!act) return;
      document.getElementById('pdf-filename').innerText = `${act.t.replace(/[^a-zA-Z0-9]/g, '_')}.pdf`;
      document.getElementById('pdf-paper-content').innerHTML = `
        <div style="border-bottom: 2px solid #334155; padding-bottom: 8px; margin-bottom: 14px; display: flex; justify-content: space-between;">
          <strong>PODER JUDICIAL DEL PERÚ</strong>
          <span style="font-size: 11px;">${act.f}</span>
        </div>
        <h3 style="font-size: 14px; margin-bottom: 10px;">${act.pdfTitle}</h3>
        <div>${act.pdfBody}</div>
        <div style="margin-top: 30px; border-top: 1px dashed #94a3b8; padding-top: 10px; font-size: 10px; color: #64748b;">
          Firmado digitalmente conforme a la Ley N° 27269. Código de verificación electrónica: PJ-${act.n}0981729381.
        </div>
      `;
      openModal('pdf-modal');
    }

    // RENDERIZADO PANTALLA 5
    function renderScreen5() {
      // Línea de tiempo
      const tBox = document.getElementById('timeline-flow-list');
      tBox.innerHTML = '';
      [ACTS[0], ACTS[1], ACTS[3], ACTS[5], ACTS[8], ACTS[11]].forEach(item => {
        const div = document.createElement('div');
        div.className = 'timeline-event';
        div.innerHTML = `
          <div class="timeline-badge"></div>
          <div class="timeline-card-content">
            <div style="display:flex; justify-content:space-between; font-size:11px; margin-bottom:2px;">
              <strong style="color:#831034;">${item.t}</strong>
              <span style="color:#64748b; font-family:monospace;">${item.d}</span>
            </div>
            <div style="font-size:11px; color:#334155; margin-bottom:6px;">${item.des}</div>
            <button onclick="openPdfDoc(${item.n})" style="background:#831034; color:white; border:none; padding:3px 8px; border-radius:4px; font-size:10px; cursor:pointer;">Ver PDF</button>
          </div>
        `;
        tBox.appendChild(div);
      });

      // Tabla de actuados
      const tbody = document.getElementById('acts-table-body');
      tbody.innerHTML = '';
      ACTS.forEach(a => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td style="padding:6px; text-align:center; font-weight:bold;">${a.n < 10 ? '0' + a.n : a.n}</td>
          <td style="padding:6px; font-family:monospace;">${a.f}</td>
          <td style="padding:6px;">${a.d}</td>
          <td style="padding:6px; font-weight:bold; color:#831034;">${a.t}</td>
          <td style="padding:6px; text-align:center;">
            <button onclick="openPdfDoc(${a.n})" style="background:#be185d; color:white; border:none; padding:4px 8px; border-radius:4px; font-size:11px; cursor:pointer;">📄 Ver PDF</button>
          </td>
        `;
        tbody.appendChild(tr);
      });
    }

    // CHATBOT IURISNIANO
    function toggleChatbot() {
      const w = document.getElementById('chatbot-window');
      w.style.display = w.style.display === 'flex' ? 'none' : 'flex';
    }

    function sendChatMsg() {
      const inp = document.getElementById('chatbot-input');
      const txt = inp.value.trim();
      if (!txt) return;

      const c = document.getElementById('chatbot-messages');
      
      // Mensaje de usuario
      const uDiv = document.createElement('div');
      uDiv.style = "background:#831034; color:white; padding:8px 12px; border-radius:12px; max-width:85%; align-self:flex-end;";
      uDiv.innerText = txt;
      c.appendChild(uDiv);
      inp.value = "";

      // Respuesta empática de Iurisniano
      const q = txt.toLowerCase();
      let r = "¡Con gusto te oriento! 😊 Puedes encontrar esa información revisando la sección IV de Seguimiento o dime si buscas un actuado específico.";

      if (q.includes("demanda") || q.includes("escrito 01") || q.includes("donde esta la demanda")) {
        r = "¡Claro que sí! La demanda laboral se encuentra en el **Actuado N° 02, a Fojas 2 al 26**. Fue presentada el 26/06/2019. 📄";
      } else if (q.includes("juez") || q.includes("quien es el juez")) {
        r = "El juez a cargo del despacho es el magistrado **Gonzalo Víctor Huamán Romero**, del Juzgado de Trabajo Zona Norte de Juliaca. ⚖️";
      } else if (q.includes("secretaria") || q.includes("especialista")) {
        r = "La especialista legal responsable de la causa es la Dra. **Rosario Carlos Villán**. ✍️";
      } else if (q.includes("resolucion 1") || q.includes("resolucion 01")) {
        r = "La **Resolución N° 01** está en el Actuado N° 06 (Fojas 99), emitida el 13/08/2019, donde se concedió 3 días de plazo al demandante. Puedes abrir su PDF directamente.";
      } else if (q.includes("resolucion 2") || q.includes("resolucion 02") || q.includes("admisorio")) {
        r = "El auto admisorio definitivo es la **Resolución N° 02** (Actuado N° 09, Fojas 105), expedida el 28/08/2019 corriendo traslado a EsSalud. 🏛️";
      } else if (q.includes("partes") || q.includes("demandante") || q.includes("demandado")) {
        r = "La parte demandante es don **Andrés Leonidas Supo Quispe** y la demandada es **EsSalud Red Asistencial Juliaca**. Toda su interoperabilidad con RENIEC y PNP está en la Sección III. 🔍";
      }

      setTimeout(() => {
        const bDiv = document.createElement('div');
        bDiv.style = "background:#ffffff; padding:8px 12px; border-radius:12px; border:1px solid var(--mag-border); max-width:85%; align-self:flex-start;";
        bDiv.innerHTML = r;
        c.appendChild(bDiv);
        c.scrollTop = c.scrollHeight;
      }, 400);
    }

    // MULTI-IDIOMA (ES / EN)
    var currentLang = 'es';
    var DICT = {
      es: {
        sysTitle: "CEJ Electrónico - Puno",
        home: "Inicio", mision: "Misión", vision: "Visión", transp: "Transparencia", contact: "Contáctanos", searchBtn: "🔍 Búsqueda de Expediente",
        p0Title: "SISTEMA DE CONSULTA DE EXPEDIENTES (CEJ / EJE)",
        p0Sub: "Simulación Jurisdiccional para Derecho e Informática",
        btnEnter: "Ingresar al Sistema",
        p1Title: "Iniciando Portal Institucional", p1Desc: "Cargando módulos de Gobierno Digital...",
        p4Title: "Indexando Cuaderno Laboral Digital", p4Desc: "Recuperando resoluciones y línea de tiempo...",
        secI: "I. REPORTE DE EXPEDIENTE", secII: "II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO", secIII: "III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)", secIV: "IV. SEGUIMIENTO DEL EXPEDIENTE (NOTIFICACIONES Y RESOLUCIONES)"
      },
      en: {
        sysTitle: "Electronic Court Records - Puno",
        home: "Home", mision: "Mission", vision: "Vision", transp: "Transparency", contact: "Contact Us", searchBtn: "🔍 Case Search",
        p0Title: "JUDICIAL CASE CONSULTATION SYSTEM (CEJ / EJE)",
        p0Sub: "Academic Simulation for Digital Government and IT Law",
        btnEnter: "Enter System",
        p1Title: "Launching Institutional Portal", p1Desc: "Loading Digital Government modules...",
        p4Title: "Indexing Digital Case File", p4Desc: "Fetching resolutions and timeline...",
        secI: "I. CASE REPORT", secII: "II. STATUS, PROGRESS AND TIMELINE", secIII: "III. PROCEDURAL PARTIES (INTEROPERABILITY)", secIV: "IV. CASE TRACKING (NOTIFICATIONS AND RESOLUTIONS)"
      }
    };

    function setLanguage(lang) {
      currentLang = lang;
      document.getElementById('btn-es').className = lang === 'es' ? 'btn-lang active' : 'btn-lang';
      document.getElementById('btn-en').className = lang === 'en' ? 'btn-lang active' : 'btn-lang';

      const d = DICT[lang];
      document.getElementById('ui-system-title').innerText = d.sysTitle;
      document.getElementById('nav-btn-home').innerText = d.home;
      document.getElementById('nav-btn-mision').innerText = d.mision;
      document.getElementById('nav-btn-vision').innerText = d.vision;
      document.getElementById('nav-btn-transp').innerText = d.transp;
      document.getElementById('nav-btn-contact').innerText = d.contact;
      document.getElementById('nav-btn-search').innerText = d.searchBtn;
      document.getElementById('p0-title').innerText = d.p0Title;
      document.getElementById('p0-sub').innerText = d.p0Sub;
      document.getElementById('btn-enter-system').innerText = d.btnEnter + " →";
      document.getElementById('p1-title').innerText = d.p1Title;
      document.getElementById('p1-desc').innerText = d.p1Desc;
      document.getElementById('p4-title').innerText = d.p4Title;
      document.getElementById('p4-desc').innerText = d.p4Desc;
      document.getElementById('sec-i-title').innerText = d.secI;
      document.getElementById('sec-ii-title').innerText = d.secII;
      document.getElementById('sec-iii-title').innerText = d.secIII;
      document.getElementById('sec-iv-title').innerText = d.secIV;
    }

    // MENÚ INSTITUCIONAL
    function showInfoMenu(topic) {
      alert(`[INFORMACIÓN INSTITUCIONAL - ${topic.toUpperCase()}]\n\nPoder Judicial del Perú - Corte Superior de Justicia de Puno.\nComprometidos con la justicia célere, digital y transparente.`);
    }

    // TEMPORIZADOR DE 7 MINUTOS
    var secondsRemaining = 420;
    setInterval(() => {
      secondsRemaining--;
      if (secondsRemaining <= 0) {
        alert("Su sesión de 7 minutos ha finalizado por seguridad. Redirigiendo a pantalla de inicio.");
        location.reload();
      }
      const m = Math.floor(secondsRemaining / 60);
      const s = secondsRemaining % 60;
      document.getElementById('timer-text').innerText = (m < 10 ? '0' + m : m) + ':' + (s < 10 ? '0' + s : s);
    }, 1000);
  </script>
</body>
</html>
