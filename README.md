<index.html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>CEJ - Expediente Judicial Electrónico | Corte Superior de Justicia de Puno</title>
  
  <style>
    /* ==========================================================
       PALETA INSTITUCIONAL: MAGENTA / VINO IMPERIAL & ORO VIEJO
       ========================================================== */
    :root {
      --mag-darkest: #18020e;
      --mag-dark: #3f0314;
      --mag-primary: #750e2e;
      --mag-vivid: #be185d;
      --mag-light: #fdf2f8;
      --mag-border: #fbcfe8;
      --gold-accent: #c5a059;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --surface-white: #ffffff;
      --radius-lg: 16px;
      --radius-md: 10px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background-color: var(--mag-light);
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow-x: hidden;
    }

    /* ==========================================================
       BARRA PERMANENTE Y NAVEGACIÓN SUPERIOR
       ========================================================== */
    .top-header-bar {
      background-color: var(--mag-dark);
      color: #ffffff;
      padding: 8px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 1000;
      box-shadow: 0 2px 10px rgba(0,0,0,0.25);
      border-bottom: 2px solid var(--mag-vivid);
    }

    .top-header-left {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .badge-gov-logo {
      background: rgba(255, 255, 255, 0.12);
      padding: 6px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .subnav-bar {
      background-color: var(--mag-darkest);
      display: flex;
      overflow-x: auto;
      padding: 6px 12px;
      gap: 6px;
      position: sticky;
      top: 50px;
      z-index: 999;
      box-shadow: 0 2px 6px rgba(0,0,0,0.15);
    }
    .subnav-bar::-webkit-scrollbar { display: none; }

    .nav-btn {
      background: transparent;
      border: none;
      color: #fbcfe8;
      padding: 7px 12px;
      font-size: 11px;
      font-weight: 700;
      cursor: pointer;
      border-radius: 6px;
      white-space: nowrap;
      transition: all 0.2s ease;
    }
    .nav-btn:hover, .nav-btn.active {
      background: rgba(255, 255, 255, 0.15);
      color: #ffffff;
    }

    .btn-search-trigger {
      margin-left: auto;
      background: linear-gradient(90deg, #be185d, #e11d48) !important;
      color: #ffffff !important;
      font-weight: 800;
      box-shadow: 0 2px 8px rgba(190, 24, 93, 0.4);
    }

    /* CONTROLES DERECHA */
    .controls-group {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .lang-box {
      display: flex;
      background: rgba(0,0,0,0.3);
      padding: 2px;
      border-radius: 6px;
    }
    .lang-btn {
      background: transparent;
      border: none;
      color: #fbcfe8;
      font-size: 10px;
      font-weight: 800;
      padding: 3px 6px;
      border-radius: 4px;
      cursor: pointer;
    }
    .lang-btn.active {
      background: var(--mag-vivid);
      color: #ffffff;
    }

    .session-clock {
      background: var(--mag-darkest);
      border: 1px solid var(--mag-primary);
      color: #fce7f3;
      padding: 4px 8px;
      border-radius: 6px;
      font-family: monospace;
      font-size: 11px;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    /* ==========================================================
       GESTIÓN DE PANTALLAS INDEPENDIENTES (DISPLAY: NONE !IMPORTANT)
       ========================================================== */
    .screen-stage {
      display: none !important;
      width: 100%;
      flex-grow: 1;
    }
    .screen-stage.active {
      display: flex !important;
      flex-direction: column;
    }

    .center-wrapper {
      display: flex;
      flex-grow: 1;
      align-items: center;
      justify-content: center;
      padding: 20px 14px;
    }

    .academic-card {
      background: var(--surface-white);
      border-radius: 20px;
      border: 1px solid var(--mag-border);
      box-shadow: 0 15px 35px rgba(117, 14, 46, 0.12);
      width: 100%;
      max-width: 620px;
      overflow: hidden;
      text-align: center;
    }

    .academic-card-header {
      background: linear-gradient(135deg, #3f0314, #750e2e, #be185d);
      color: white;
      padding: 26px 20px;
    }

    .btn-action-primary {
      background: linear-gradient(90deg, #750e2e, #be185d);
      color: #ffffff;
      border: none;
      padding: 13px 22px;
      border-radius: 12px;
      font-weight: 700;
      font-size: 13px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      width: 100%;
      transition: all 0.2s ease;
      box-shadow: 0 4px 14px rgba(190, 24, 93, 0.3);
    }
    .btn-action-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 18px rgba(190, 24, 93, 0.4);
    }

    /* ==========================================================
       LÍNEA DE TIEMPO INTERACTIVA
       ========================================================== */
    .timeline-wrapper {
      position: relative;
      padding: 16px 0 16px 26px;
      border-left: 3px solid var(--mag-vivid);
      margin-left: 12px;
    }
    .timeline-node {
      position: relative;
      margin-bottom: 18px;
      transition: transform 0.2s;
    }
    .timeline-node:hover {
      transform: translateX(4px);
    }
    .timeline-dot {
      position: absolute;
      left: -35px;
      top: 4px;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background: #be185d;
      border: 3px solid #ffffff;
      box-shadow: 0 0 0 2px #be185d;
    }
    .timeline-card {
      background: #fdf2f8;
      border: 1px solid var(--mag-border);
      border-radius: 10px;
      padding: 12px 14px;
    }

    /* ==========================================================
       BOTONES DINÁMICOS DE INTEROPERABILIDAD
       ========================================================== */
    .btn-interop {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 7px 11px;
      border-radius: 8px;
      font-size: 11px;
      font-weight: 700;
      border: none;
      cursor: pointer;
      color: #ffffff;
      transition: all 0.25s ease;
      box-shadow: 0 2px 6px rgba(0,0,0,0.12);
    }
    .btn-interop:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 12px rgba(0,0,0,0.22);
    }
    .btn-reniec { background: linear-gradient(135deg, #0284c7, #0369a1); }
    .btn-migra { background: linear-gradient(135deg, #d97706, #b45309); }
    .btn-pnp { background: linear-gradient(135deg, #059669, #047857); }
    .btn-inpe { background: linear-gradient(135deg, #dc2626, #b91c1c); }

    /* ==========================================================
       MODAL Y VISOR DE RESOLUCIONES / DOCUMENTOS TIPO PDF
       ========================================================== */
    .modal-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(24, 2, 14, 0.78);
      backdrop-filter: blur(4px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 14px;
      z-index: 2500;
    }
    .modal-sheet {
      background: #ffffff;
      border-radius: 16px;
      max-width: 680px;
      width: 100%;
      max-height: 88vh;
      overflow-y: auto;
      border: 1px solid var(--mag-border);
      box-shadow: 0 20px 40px rgba(0,0,0,0.35);
    }

    .pdf-bar {
      background: #334155;
      color: white;
      padding: 8px 14px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
    }
    .pdf-paper {
      background: #ffffff;
      box-shadow: 0 4px 16px rgba(0,0,0,0.08);
      margin: 16px auto;
      max-width: 600px;
      padding: 28px;
      font-family: Georgia, serif;
      font-size: 13px;
      line-height: 1.6;
      border: 1px solid #cbd5e1;
      transform-origin: top center;
      transition: transform 0.2s ease;
    }

    /* ==========================================================
       CHATBOT IURISNIANO FLOTANTE
       ========================================================== */
    #chatbot-bubble {
      position: fixed;
      bottom: 22px;
      right: 22px;
      background: linear-gradient(135deg, #750e2e, #be185d);
      color: white;
      width: 58px;
      height: 58px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 8px 24px rgba(190, 24, 93, 0.45);
      cursor: pointer;
      z-index: 3000;
      transition: all 0.3s;
    }
    #chatbot-bubble:hover {
      transform: scale(1.1) rotate(5deg);
    }
    #chatbot-dialog {
      position: fixed;
      bottom: 90px;
      right: 22px;
      width: 340px;
      max-width: 90vw;
      height: 470px;
      background: #ffffff;
      border-radius: 18px;
      border: 1px solid var(--mag-border);
      box-shadow: 0 12px 35px rgba(0,0,0,0.3);
      display: none;
      flex-direction: column;
      z-index: 3000;
      overflow: hidden;
    }

    /* BARRA DE PROGRESO DE ETAPA PROCESAL */
    .stepper-bar {
      display: flex;
      justify-content: space-between;
      margin: 14px 0 20px;
      font-size: 11px;
      text-align: center;
    }
    .stepper-step {
      flex: 1;
    }
    .stepper-circle {
      width: 26px;
      height: 26px;
      border-radius: 50%;
      margin: 0 auto 4px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
    }
    .stepper-active { background: #be185d; color: white; }
    .stepper-done { background: #750e2e; color: white; }
    .stepper-idle { background: #cbd5e1; color: #64748b; }
  </style>
</head>
<body>

  <!-- ==========================================================
       1. BARRA SUPERIOR PERMANENTE EN TODAS LAS PANTALLAS
       ========================================================== -->
  <header class="top-header-bar">
    <div class="top-header-left">
      <div class="badge-gov-logo">
        <svg style="width: 22px; height: 22px; color: #fbcfe8;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M3 21h18"/><path d="M3 10h18"/><path d="M5 10v11"/><path d="M19 10v11"/><path d="M9 10v11"/><path d="M15 10v11"/><path d="M12 2 2 7h20L12 2z"/>
        </svg>
      </div>
      <div>
        <div style="font-size: 8px; font-weight: 800; color: #fbcfe8; letter-spacing: 0.5px;">PODER JUDICIAL DEL PERÚ</div>
        <div id="txt-app-title" style="font-size: 12px; font-weight: 700;">CEJ Electrónico - CSJ Puno</div>
      </div>
    </div>

    <div class="controls-group">
      <!-- Selector de Idiomas -->
      <div class="lang-box">
        <button id="btn-lang-es" onclick="switchLanguage('es')" class="lang-btn active">ES</button>
        <button id="btn-lang-en" onclick="switchLanguage('en')" class="lang-btn">EN</button>
      </div>

      <!-- Temporizador de Sesión -->
      <div class="session-clock">
        <span id="txt-session-label">Sesión:</span> <strong id="clock-display">07:00</strong>
      </div>
    </div>
  </header>

  <!-- 2. SUBBARRA HORIZONTAL PERMANENTE -->
  <nav class="subnav-bar">
    <button onclick="switchScreen(0)" class="nav-btn" id="nav-item-home">Inicio</button>
    <button onclick="openInfoView('mision')" class="nav-btn" id="nav-item-mision">Misión</button>
    <button onclick="openInfoView('vision')" class="nav-btn" id="nav-item-vision">Visión</button>
    <button onclick="openInfoView('transparencia')" class="nav-btn" id="nav-item-transp">Transparencia</button>
    <button onclick="openInfoView('contactanos')" class="nav-btn" id="nav-item-contact">Contáctanos</button>
    <button onclick="startSearchFlow()" class="nav-btn btn-search-trigger" id="nav-item-search">🔍 Búsqueda de Expediente</button>
  </nav>

  <!-- ==========================================================
       CONTENEDOR DE PANTALLAS MUTUAMENTE EXCLUYENTES
       ========================================================== -->
  <div style="flex-grow: 1; display: flex; flex-direction: column;">

    <!-- ========================================== -->
    <!-- PANTALLA 0: BIENVENIDA (ESTÁTICA CON TEMIS)-->
    <!-- ========================================== -->
    <div id="screen-0" class="screen-stage active center-wrapper">
      <div class="academic-card">
        <div class="academic-card-header">
          <!-- Balanza de Temis Centrada -->
          <div style="margin: 0 auto 12px; width: 95px; height: 95px; background: rgba(255,255,255,0.14); border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid #fbcfe8;">
            <svg style="width: 65px; height: 65px;" viewBox="0 0 200 200" fill="none">
              <circle cx="100" cy="100" r="90" fill="#fdf2f8" stroke="#be185d" stroke-width="3" stroke-dasharray="4 2"/>
              <path d="M100 25 L100 160" stroke="#750e2e" stroke-width="4" stroke-linecap="round"/>
              <path d="M80 160 L120 160" stroke="#750e2e" stroke-width="6" stroke-linecap="round"/>
              <path d="M50 55 L150 55" stroke="#be185d" stroke-width="4" stroke-linecap="round"/>
              <circle cx="100" cy="55" r="6" fill="#750e2e"/>
              <path d="M50 55 L35 95" stroke="#9f1239" stroke-width="2"/><path d="M50 55 L65 95" stroke="#9f1239" stroke-width="2"/>
              <path d="M25 95 Q50 115 75 95 Z" fill="#fbcfe8"/>
              <path d="M150 55 L135 95" stroke="#9f1239" stroke-width="2"/><path d="M150 55 L165 95" stroke="#9f1239" stroke-width="2"/>
              <path d="M125 95 Q150 115 175 95 Z" fill="#fbcfe8"/>
              <path d="M85 40 Q100 35 115 40" stroke="#3f0314" stroke-width="3"/>
            </svg>
          </div>
          <h1 id="p0-heading" style="font-size: 18px; font-weight: 800;">SISTEMA DE CONSULTA DE EXPEDIENTES (CEJ / EJE)</h1>
          <p id="p0-subheading" style="font-size: 12px; color: #fce7f3; margin-top: 4px;">Simulación Jurisdiccional para Derecho e Informática</p>
        </div>

        <div style="padding: 22px; text-align: left;">
          <!-- Ficha de Autoría Académica -->
          <div style="background: #fdf2f8; border: 1px solid var(--mag-border); border-radius: 12px; padding: 14px; margin-bottom: 14px; font-size: 12px; line-height: 1.7;">
            <div><span style="color: var(--text-muted);" id="p0-lbl-author">Estudiante:</span> <strong style="color: var(--mag-primary); font-size: 13px;">Sonia Pilar Condori Ruelas</strong></div>
            <div><span style="color: var(--text-muted);" id="p0-lbl-course">Curso:</span> <strong style="color: var(--mag-dark);">Gobierno Digital e Informático</strong></div>
            <div><span style="color: var(--text-muted);" id="p0-lbl-teacher">Docente:</span> <strong style="color: var(--mag-dark);">Dr. Michael Espinoza Coila</strong></div>
          </div>

          <!-- Advertencia de Simulación -->
          <div style="background: #fff1f2; border-left: 4px solid #be185d; padding: 10px 12px; border-radius: 6px; margin-bottom: 18px;">
            <p id="p0-lbl-warning" style="font-size: 11px; color: #4a0418; line-height: 1.5; font-weight: 600;">
              COMUNICADO: El presente trabajo es un producto netamente académico y NO es un sitio oficial del Poder Judicial del Perú. Su diseño responde con exclusividad a fines pedagógicos universitarios.
            </p>
          </div>

          <button onclick="switchScreen(1)" class="btn-action-primary" id="p0-btn-submit">
            <span>Ingresar al Sistema Jurisdiccional</span> →
          </button>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 1: CARGA INICIAL DINÁMICA (0% A 100%) -->
    <!-- ========================================== -->
    <div id="screen-1" class="screen-stage center-wrapper">
      <div style="max-width: 360px; width: 100%; text-align: center; background: white; padding: 30px 20px; border-radius: 16px; border: 1px solid var(--mag-border); box-shadow: 0 4px 15px rgba(0,0,0,0.05);">
        <svg style="width: 44px; height: 44px; color: #750e2e; margin-bottom: 12px; animation: spinLoader 1.5s linear infinite;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
        </svg>
        <h3 id="p1-loader-title" style="font-size: 15px; font-weight: 700; color: #3f0314;">Estableciendo Conexión Cifrada</h3>
        <p id="p1-loader-desc" style="font-size: 12px; color: #64748b; margin-top: 4px;">Accediendo a la Sede Central Juliaca - CSJ Puno...</p>
        <div style="font-weight: 800; font-size: 14px; color: var(--mag-vivid); margin-top: 14px;" id="p1-percentage">0%</div>
        <div style="background: #fce7f3; height: 8px; border-radius: 8px; overflow: hidden; margin-top: 6px;">
          <div id="p1-progress-bar" style="height: 100%; background: linear-gradient(90deg, #750e2e, #be185d); width: 0%; transition: width 0.1s linear;"></div>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 2: PORTAL ESTATAL Y TEMIS          -->
    <!-- ========================================== -->
    <div id="screen-2" class="screen-stage">
      <div style="max-width: 1100px; width: 100%; margin: 20px auto; padding: 0 16px; flex-grow: 1; display: flex; flex-direction: column; justify-content: center;">
        
        <!-- Temis Interactiva de Pantalla 2 -->
        <div id="box-temis-blank" onclick="startSearchFlow()" style="background: white; border: 1px solid var(--mag-border); border-radius: 20px; text-align: center; padding: 42px 16px; cursor: pointer; box-shadow: 0 4px 15px rgba(0,0,0,0.02);">
          <svg style="width: 130px; height: 130px; margin: 0 auto 14px; display: block;" viewBox="0 0 200 200" fill="none">
            <circle cx="100" cy="100" r="90" fill="#fdf2f8" stroke="#be185d" stroke-width="3" stroke-dasharray="4 2"/>
            <path d="M100 25 L100 160" stroke="#750e2e" stroke-width="4" stroke-linecap="round"/>
            <path d="M80 160 L120 160" stroke="#750e2e" stroke-width="6" stroke-linecap="round"/>
            <path d="M50 55 L150 55" stroke="#be185d" stroke-width="4" stroke-linecap="round"/>
            <circle cx="100" cy="55" r="6" fill="#750e2e"/>
            <path d="M50 55 L35 95" stroke="#9f1239" stroke-width="2"/><path d="M50 55 L65 95" stroke="#9f1239" stroke-width="2"/>
            <path d="M25 95 Q50 115 75 95 Z" fill="#fbcfe8"/>
            <path d="M150 55 L135 95" stroke="#9f1239" stroke-width="2"/><path d="M150 55 L165 95" stroke="#9f1239" stroke-width="2"/>
            <path d="M125 95 Q150 115 175 95 Z" fill="#fbcfe8"/>
            <path d="M85 40 Q100 35 115 40" stroke="#3f0314" stroke-width="3"/>
          </svg>
          <h2 id="p2-temis-title" style="font-size: 19px; color: #3f0314; font-weight: 800;">Consulta de Expedientes Judiciales (CEJ)</h2>
          <p id="p2-temis-desc" style="font-size: 13px; color: #64748b; max-width: 500px; margin: 8px auto 16px;">
            Haga clic en este recuadro para validar el código CAPTCHA de seguridad e iniciar la consulta de causas del Distrito Judicial de Puno.
          </p>
          <span id="p2-temis-badge" style="font-size: 11px; background: #be185d; color: white; padding: 7px 16px; border-radius: 20px; font-weight: bold; display: inline-block;">
            Clic aquí para desbloquear búsqueda
          </span>
        </div>

        <!-- Formulario Desplegado tras CAPTCHA y Comunicado -->
        <div id="panel-search-form" style="display: none; background: white; border: 1px solid var(--mag-border); border-radius: 20px; padding: 22px; max-width: 620px; margin: 0 auto; width: 100%; box-shadow: 0 4px 15px rgba(0,0,0,0.05);">
          <div style="background: #3f0314; color: white; padding: 14px 18px; border-radius: 12px 12px 0 0; margin: -22px -22px 18px; display: flex; justify-content: space-between; align-items: center;">
            <strong id="p2-form-heading" style="font-size: 13px;">Búsqueda Jurisdiccional de Causas</strong>
            <button onclick="cancelSearchFlow()" style="background: none; border: none; color: #fbcfe8; cursor: pointer; font-size: 16px;">✕</button>
          </div>

          <!-- Selector de Modo -->
          <div style="display: flex; gap: 8px; margin-bottom: 14px; border-bottom: 1px solid #fce7f3; padding-bottom: 8px;">
            <button id="btn-tab-code" onclick="toggleSearchTab('code')" style="background: #750e2e; color: white; border: none; padding: 7px 14px; border-radius: 6px; font-size: 11px; font-weight: bold; cursor: pointer;">Por Número de Expediente</button>
            <button id="btn-tab-party" onclick="toggleSearchTab('party')" style="background: #e2e8f0; color: #334155; border: none; padding: 7px 14px; border-radius: 6px; font-size: 11px; font-weight: bold; cursor: pointer;">Por Partes Procesales</button>
          </div>

          <div id="fields-by-code">
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
                <label style="font-size: 11px; font-weight: bold; color: #64748b;">Distrito Jud.</label>
                <input type="text" value="2111" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;">
              </div>
            </div>
          </div>

          <div id="fields-by-party" style="display: none; margin-bottom: 12px;">
            <label style="font-size: 11px; font-weight: bold; color: #64748b;">Demandante o Demandado:</label>
            <input type="text" value="Andrés Leonidas Supo Quispe" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; margin-top: 4px; font-weight: bold;">
          </div>

          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 10px; border-radius: 8px; font-size: 12px; margin-bottom: 16px;">
            Expediente asignado: <strong style="color: #750e2e;">00174-2019-0-2111-JR-LA-02</strong> (EsSalud vs Supo)
          </div>

          <button onclick="switchScreen(4)" class="btn-action-primary" id="p2-btn-submit">
            <span>Consultar Expediente Judicial</span> →
          </button>
        </div>

      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 4: CARGA DE BASE DE DATOS (0% A 100%) -->
    <!-- ========================================== -->
    <div id="screen-4" class="screen-stage center-wrapper">
      <div style="max-width: 360px; width: 100%; text-align: center; background: white; padding: 30px 20px; border-radius: 16px; border: 1px solid var(--mag-border); box-shadow: 0 4px 15px rgba(0,0,0,0.05);">
        <svg style="width: 44px; height: 44px; color: #be185d; margin-bottom: 12px; animation: bounce 1s infinite;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1-2.5-2.5Z"/><path d="M6 6h10"/><path d="M6 10h10"/>
        </svg>
        <h3 id="p4-loader-title" style="font-size: 15px; font-weight: 700; color: #3f0314;">Indexando Cuaderno Laboral Digital</h3>
        <p id="p4-loader-desc" style="font-size: 12px; color: #64748b; margin-top: 4px;">Recuperando resoluciones, notificaciones y fojas...</p>
        <div style="font-weight: 800; font-size: 14px; color: var(--mag-primary); margin-top: 14px;" id="p4-percentage">0%</div>
        <div style="background: #fce7f3; height: 8px; border-radius: 8px; overflow: hidden; margin-top: 6px;">
          <div id="p4-progress-bar" style="height: 100%; background: linear-gradient(90deg, #750e2e, #be185d); width: 0%; transition: width 0.1s linear;"></div>
        </div>
      </div>
    </div>

    <!-- ========================================== -->
    <!-- PANTALLA 5: EXPEDIENTE COMPLETO ESTRUCTURADO-->
    <!-- ========================================== -->
    <div id="screen-5" class="screen-stage">
      <div style="max-width: 1100px; width: 100%; margin: 16px auto; padding: 0 16px; flex-grow: 1;">
        
        <!-- I. REPORTE DE EXPEDIENTE -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px; box-shadow: 0 2px 8px rgba(0,0,0,0.02);">
          <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-i-title" style="color: var(--mag-primary); font-size: 13px;">I. REPORTE DE EXPEDIENTE</strong>
            <span style="font-family: monospace; font-size: 11px; background: #fdf2f8; padding: 3px 8px; border-radius: 4px; color: #750e2e; font-weight: bold;">EXP: 00174-2019-0-2111-JR-LA-02</span>
          </div>
          <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; font-size: 12px;">
            <div><span style="color: #64748b; display: block;" id="lbl-dist">Distrito Judicial / Sede:</span> <strong>Puno / San Román – Juliaca</strong></div>
            <div><span style="color: #64748b; display: block;" id="lbl-court">Juzgado:</span> <strong>Juzgado de Trabajo – Zona Norte</strong></div>
            <div><span style="color: #64748b; display: block;" id="lbl-judge">Juez a Cargo:</span> <strong>Huamán Romero, Gonzalo Víctor</strong></div>
            <div><span style="color: #64748b; display: block;" id="lbl-sec">Secretaria Judicial:</span> <strong>Carlos Villán, Rosario</strong></div>
            <div><span style="color: #64748b; display: block;" id="lbl-matter">Materia Procesal:</span> <strong style="color: #750e2e;">Desnaturalización Laboral (Ley 26636)</strong></div>
          </div>
        </div>

        <!-- II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px; box-shadow: 0 2px 8px rgba(0,0,0,0.02);">
          <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-ii-title" style="color: var(--mag-primary); font-size: 13px;">II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO</strong>
            <span style="font-size: 11px; color: #047857; font-weight: bold; background: #ecfdf5; padding: 2px 8px; border-radius: 4px;">Etapa: Postulatoria</span>
          </div>

          <!-- Barra Visual de Etapa Procesal -->
          <div class="stepper-bar">
            <div class="stepper-step">
              <div class="stepper-circle stepper-done">✓</div>
              <strong>1. Postulatoria</strong>
            </div>
            <div class="stepper-step">
              <div class="stepper-circle stepper-active">2</div>
              <strong>2. Probatoria</strong>
            </div>
            <div class="stepper-step">
              <div class="stepper-circle stepper-idle">3</div>
              <span style="color:#94a3b8;">3. Decisoria</span>
            </div>
            <div class="stepper-step">
              <div class="stepper-circle stepper-idle">4</div>
              <span style="color:#94a3b8;">4. Ejecución</span>
            </div>
          </div>

          <!-- Línea de Tiempo de los Hitos del Caso -->
          <div class="timeline-wrapper" id="timeline-flow-box"></div>
        </div>

        <!-- III. PARTES PROCESALES CON CONSULTAS DE INTEROPERABILIDAD -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 16px; box-shadow: 0 2px 8px rgba(0,0,0,0.02);">
          <div style="border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-iii-title" style="color: var(--mag-primary); font-size: 13px;">III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)</strong>
          </div>

          <!-- Demandante -->
          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; border-radius: 12px; padding: 12px; margin-bottom: 12px;">
            <div style="font-weight: bold; font-size: 13px; color: #750e2e;">DEMANDANTE: Andrés Leonidas Supo Quispe (DNI 02167445)</div>
            <div style="font-size: 11px; color: #64748b; margin: 4px 0 10px;">Abog. Lino Larico Larico (Reg. CAP 47) | Casilla SINOE: 60375</div>
            
            <!-- Botones Dinámicos de Interoperabilidad -->
            <div style="display: flex; flex-wrap: wrap; gap: 8px;">
              <button onclick="openReniecProtectedModal('Andrés Leonidas Supo Quispe', '02167445')" class="btn-interop btn-reniec">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC (Identidad Protegida)</span>
              </button>
              <button onclick="openGenericInterop('MIGRACIONES', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'Sin impedimento de salida del país. Pasaporte ordinario válido.')" class="btn-interop btn-migra">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="m4.93 4.93 4.24 4.24"/><path d="m14.83 9.17 4.24-4.24"/></svg>
                <span>MIGRACIONES</span>
              </button>
              <button onclick="openGenericInterop('PNP', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'SISTEMA ESINPOL / RQ: NO REGISTRA ORDEN DE CAPTURA NI REQUISITORIA VIGENTE.')" class="btn-interop btn-pnp">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
                <span>PNP (Requisitorias)</span>
              </button>
              <button onclick="openGenericInterop('INPE', 'Andrés Leonidas Supo Quispe', 'DNI: 02167445', 'REGISTRO PENAL: NO REGISTRA ANTECEDENTES PENITENCIARIOS.')" class="btn-interop btn-inpe">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="18" height="18" x="3" y="3" rx="2"/><path d="M3 9h18"/><path d="M9 21V9"/></svg>
                <span>INPE (Penales)</span>
              </button>
            </div>
          </div>

          <!-- Demandada -->
          <div style="background: #fff1f2; border: 1px solid #fecdd3; border-radius: 12px; padding: 12px;">
            <div style="font-weight: bold; font-size: 13px; color: #be185d;">DEMANDADA: Seguro Social de Salud - EsSalud (RUC 20131257750)</div>
            <div style="font-size: 11px; color: #64748b; margin: 4px 0 10px;">Apoderado Judicial: Abog. Hernán Rolando López Alférez (DNI 01207861) | Casilla: 59629</div>
            <div style="display: flex; gap: 8px;">
              <button onclick="openReniecProtectedModal('Hernán Rolando López Alférez', '01207861')" class="btn-interop btn-reniec">
                <svg style="width:14px; height:14px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC (Apoderado)</span>
              </button>
            </div>
          </div>
        </div>

        <!-- IV. SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES EN PDF) -->
        <div style="background: white; border: 1px solid var(--mag-border); border-radius: 16px; padding: 18px; margin-bottom: 24px; box-shadow: 0 2px 8px rgba(0,0,0,0.02);">
          <div style="border-bottom: 2px solid #fce7f3; padding-bottom: 8px; margin-bottom: 12px;">
            <strong id="sec-iv-title" style="color: var(--mag-primary); font-size: 13px;">IV. SEGUIMIENTO DEL EXPEDIENTE (NOTIFICACIONES Y RESOLUCIONES)</strong>
          </div>
          <table style="width: 100%; border-collapse: collapse; font-size: 12px;">
            <thead>
              <tr style="background: #3f0314; color: white;">
                <th style="padding: 8px;">N°</th>
                <th style="padding: 8px;">Fojas</th>
                <th style="padding: 8px;">Fecha</th>
                <th style="padding: 8px;">Documento</th>
                <th style="padding: 8px; text-align: center;">Acción</th>
              </tr>
            </thead>
            <tbody id="acts-table-body"></tbody>
          </table>
        </div>

      </div>
    </div>

  </div>

  <!-- ==========================================================
       MODALES FLOTANTES
       ========================================================== -->

  <!-- MODAL: INFORMACIÓN INSTITUCIONAL DE NAVEGACIÓN -->
  <div id="modal-info-view" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 520px; padding: 22px;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid var(--mag-border); padding-bottom: 8px; margin-bottom: 12px;">
        <h3 id="info-modal-heading" style="color: var(--mag-primary); font-size: 15px; font-weight: 800;">Información Institucional</h3>
        <button onclick="closeModal('modal-info-view')" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>
      <div id="info-modal-text" style="font-size: 13px; line-height: 1.6; color: var(--text-main); margin-bottom: 16px;"></div>
      <button onclick="closeModal('modal-info-view')" class="btn-action-primary" style="padding: 8px 14px; font-size: 12px;">Cerrar</button>
    </div>
  </div>

  <!-- MODAL: RENIEC CON FOTOGRAFÍA Y DATOS CENSURADOS -->
  <div id="modal-reniec" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 520px; padding: 20px;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #0284c7; padding-bottom: 8px; margin-bottom: 14px;">
        <div style="font-weight: 800; color: #0284c7; font-size: 14px;">RENIEC - CONSULTA REGISTRAL EN LÍNEA</div>
        <button onclick="closeModal('modal-reniec')" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>

      <div style="display: flex; gap: 14px; background: #f8fafc; border: 1px solid #e2e8f0; padding: 14px; border-radius: 10px;">
        <!-- Fotografía Simulada -->
        <div style="width: 110px; height: 130px; background: #e2e8f0; border: 2px solid #94a3b8; border-radius: 6px; display: flex; flex-direction: column; align-items: center; justify-content: center; position: relative; overflow: hidden; flex-shrink: 0;">
          <svg style="width: 60px; height: 60px; color: #64748b;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/>
          </svg>
          <span style="font-size: 8px; color: #475569; font-weight: bold; margin-top: 4px;">FOTO RENIEC</span>
          <div style="position: absolute; bottom: 0; width: 100%; background: rgba(2, 132, 199, 0.85); color: white; font-size: 8px; text-align: center; padding: 1px;">VERIFICADO</div>
        </div>

        <!-- Datos con Censura de Protección -->
        <div style="flex-grow: 1; font-size: 11px; line-height: 1.6;">
          <div><span style="color: #64748b;">Nombres:</span> <strong id="reniec-txt-nom">ANDRES ********</strong></div>
          <div><span style="color: #64748b;">Apellidos:</span> <strong id="reniec-txt-ape">SUPO ********</strong></div>
          <div><span style="color: #64748b;">DNI:</span> <strong id="reniec-txt-dni">0216****</strong></div>
          <div><span style="color: #64748b;">Fecha Nacimiento:</span> <strong>14/08/19**</strong></div>
          <div><span style="color: #64748b;">Ubigeo:</span> <strong>211101 (JULIACA - PUNO)</strong></div>
          <div><span style="color: #64748b;">Dirección:</span> <strong>AV. MANCO CAPAC N° 9** (CENSURADO)</strong></div>
          <div><span style="color: #64748b;">Estado:</span> <span style="color: #059669; font-weight: bold;">ACTIVO / SIN RESTRICCIÓN</span></div>
        </div>
      </div>

      <div style="background: #eff6ff; border: 1px solid #bfdbfe; padding: 8px 10px; border-radius: 6px; font-size: 10px; color: #1e40af; margin-top: 10px;">
        * Medida técnica de seguridad: Información anonimizada con asteriscos conforme a la Ley N° 29733 (Ley de Protección de Datos Personales).
      </div>
    </div>
  </div>

  <!-- MODAL: INTEROPERABILIDAD GENÉRICA -->
  <div id="modal-generic-interop" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 480px; padding: 20px;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid var(--mag-border); padding-bottom: 8px; margin-bottom: 12px;">
        <h4 id="gen-interop-heading" style="color: var(--mag-primary); font-size: 14px; font-weight: bold;">Consulta Interoperabilidad</h4>
        <button onclick="closeModal('modal-generic-interop')" style="background: none; border: none; font-size: 18px; cursor: pointer;">✕</button>
      </div>
      <div style="font-size: 12px; margin-bottom: 6px;">Titular: <strong id="gen-interop-person"></strong></div>
      <div style="font-size: 11px; color: #64748b; margin-bottom: 12px;">Doc: <strong id="gen-interop-number"></strong></div>
      <div id="gen-interop-details" style="background: #f8fafc; border: 1px solid #e2e8f0; padding: 12px; border-radius: 8px; font-size: 12px; line-height: 1.5; margin-bottom: 14px;"></div>
      <button onclick="closeModal('modal-generic-interop')" class="btn-action-primary" style="padding: 8px 14px; font-size: 11px;">Cerrar Consulta</button>
    </div>
  </div>

  <!-- MODAL: VISOR DE RESOLUCIONES / DOCUMENTOS TIPO PDF -->
  <div id="modal-pdf-view" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 680px; background: #e2e8f0;">
      <div class="pdf-bar">
        <span id="pdf-doc-name">Resolucion_01_2019.pdf</span>
        <div style="display: flex; gap: 6px; align-items: center;">
          <button onclick="zoomPdfDoc(-0.1)" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">-</button>
          <button onclick="zoomPdfDoc(0.1)" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">+</button>
          <button onclick="downloadPdfSimulated()" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">💾 Descargar</button>
          <button onclick="window.print()" style="background: #475569; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">🖨️ Imprimir</button>
          <button onclick="closeModal('modal-pdf-view')" style="background: #ef4444; border: none; color: white; padding: 3px 8px; border-radius: 4px; cursor: pointer;">✕</button>
        </div>
      </div>
      <div class="pdf-paper" id="pdf-doc-paper"></div>
    </div>
  </div>

  <!-- MODAL: COMUNICADO MINJUSDH -->
  <div id="modal-comunicado" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 480px; padding: 22px;">
      <h3 style="color: #3f0314; font-size: 15px; font-weight: 800; margin-bottom: 10px;">COMUNICADO OFICIAL</h3>
      <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 12px; border-radius: 8px; font-size: 12px; line-height: 1.6; color: #334155; text-align: justify; margin-bottom: 14px;">
        A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la <strong>Autoridad Nacional de Protección de Datos Personales</strong> y la <strong>Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH</strong>. Al amparo de la <strong>Ley N° 29733</strong>, Ley de Protección de Datos Personales.
      </div>
      <button onclick="acceptComunicadoAndShowSearch()" class="btn-action-primary">He leído y Acepto el Comunicado</button>
    </div>
  </div>

  <!-- MODAL: CAPTCHA FLOTANTE -->
  <div id="modal-captcha" class="modal-overlay">
    <div class="modal-sheet" style="max-width: 420px; padding: 22px;">
      <h3 style="color: #3f0314; font-size: 15px; font-weight: bold; margin-bottom: 10px;">Seguridad CAPTCHA</h3>
      <div style="display: flex; gap: 8px; align-items: center; margin-bottom: 12px;">
        <div id="captcha-display-text" style="background: #18020e; color: #fbcfe8; font-family: monospace; font-size: 20px; font-weight: 800; letter-spacing: 4px; padding: 8px 14px; border-radius: 8px; text-decoration: line-through;">
          8M4X1
        </div>
        <button onclick="generateRandomCaptcha()" style="padding: 8px 12px; border: 1px solid #cbd5e1; border-radius: 6px; cursor: pointer; background: white;">↻</button>
        <input type="text" id="captcha-input-field" placeholder="Código" style="flex-grow: 1; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-transform: uppercase; font-weight: bold;">
      </div>
      <button onclick="validateCaptchaAction()" class="btn-action-primary">Validar y Continuar</button>
      <div id="captcha-error-text" style="display: none; color: #e11d48; font-size: 11px; margin-top: 6px; text-align: center;">Código incorrecto. Intente de nuevo.</div>
    </div>
  </div>

  <!-- ==========================================================
       CHATBOT IURISNIANO FLOTANTE
       ========================================================== -->
  <div id="chatbot-bubble" onclick="toggleChatbotWindow()" title="Habla con Iurisniano">
    <svg style="width:28px; height:28px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
    </svg>
  </div>

  <div id="chatbot-dialog">
    <div style="background: linear-gradient(135deg, #3f0314, #be185d); color: white; padding: 12px 14px; display: flex; justify-content: space-between; align-items: center;">
      <div style="display: flex; align-items: center; gap: 8px;">
        <div style="width: 28px; height: 28px; background: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; color: #750e2e; font-weight: bold; font-size: 13px;">⚖️</div>
        <div>
          <strong style="font-size: 13px;">IURISNIANO</strong>
          <div style="font-size: 9px; color: #fce7f3;">Asistente Judicial Virtual</div>
        </div>
      </div>
      <button onclick="toggleChatbotWindow()" style="background: none; border: none; color: white; font-size: 16px; cursor: pointer;">✕</button>
    </div>

    <!-- Preguntas rápidas -->
    <div style="display: flex; gap: 4px; padding: 6px 10px; background: #fdf2f8; border-bottom: 1px solid var(--mag-border); overflow-x: auto;">
      <button onclick="quickAskBot('¿Dónde está la demanda?')" style="background: white; border: 1px solid var(--mag-border); border-radius: 12px; padding: 2px 8px; font-size: 9px; cursor: pointer; white-space: nowrap; color: #750e2e;">📄 Demanda</button>
      <button onclick="quickAskBot('¿Quién es el juez?')" style="background: white; border: 1px solid var(--mag-border); border-radius: 12px; padding: 2px 8px; font-size: 9px; cursor: pointer; white-space: nowrap; color: #750e2e;">⚖️ Juez</button>
      <button onclick="quickAskBot('¿Dónde están las resoluciones?')" style="background: white; border: 1px solid var(--mag-border); border-radius: 12px; padding: 2px 8px; font-size: 9px; cursor: pointer; white-space: nowrap; color: #750e2e;">🏛️ Resoluciones</button>
    </div>

    <!-- Mensajes -->
    <div id="chatbot-log" style="flex-grow: 1; padding: 12px; overflow-y: auto; font-size: 12px; display: flex; flex-direction: column; gap: 8px; background: #fffafc;">
      <div style="background: #ffffff; padding: 8px 12px; border-radius: 12px; border: 1px solid var(--mag-border); max-width: 85%; align-self: flex-start;">
        ¡Hola! 👋 Soy <strong>Iurisniano</strong>, tu asistente legal del expediente. Puedes preguntarme sobre fojas, resoluciones, el juez del caso o dónde está la demanda. ¿En qué te ayudo hoy?
      </div>
    </div>

    <!-- Input -->
    <div style="padding: 8px; border-top: 1px solid #e2e8f0; display: flex; gap: 6px; background: white;">
      <input type="text" id="chatbot-text-input" placeholder="Pregúntale a Iurisniano..." style="flex-grow: 1; padding: 7px 10px; border: 1px solid #cbd5e1; border-radius: 8px; font-size: 11px;" onkeypress="if(event.key==='Enter') sendChatMessage()">
      <button onclick="sendChatMessage()" style="background: #750e2e; color: white; border: none; padding: 6px 12px; border-radius: 8px; font-size: 11px; cursor: pointer; font-weight: bold;">Enviar</button>
    </div>
  </div>

  <style>
    @keyframes spinLoader { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    @keyframes bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-5px); } }
  </style>

  <!-- ==========================================================
       LÓGICA JAVASCRIPT COMPLETA Y FUNCIONAL
       ========================================================== -->
  <script>
    // BASE DE DATOS DE ACTUADOS JUDICIALES
    var ACTUADOS = [
      { n: 1, f: "Fjs. 1-2", d: "26/06/2019", t: "Cargo / Carátula", des: "Ingreso en Mesa de Partes Única de Juliaca.", title: "Carátula de Ingreso CDG N° 00174-2019", content: "<p><strong>PODER JUDICIAL DEL PERÚ - CORTE SUPERIOR DE PUNO</strong></p><p>Expediente: 00174-2019-0-2111-JR-LA-02</p><p>Materia: Desnaturalización de Contrato</p><p>Ingreso: 26/06/2019 11:31:38 - Fojas: 26</p>" },
      { n: 2, f: "Fjs. 2-26", d: "26/06/2019", t: "Escrito N° 01 (Demanda)", des: "Demanda laboral ordinaria de desnaturalización.", title: "Escrito 01 - Demanda Laboral", content: "<p><strong>SEÑOR JUEZ DE TRABAJO DE SAN ROMÁN - JULIACA:</strong></p><p>Andrés Leonidas Supo Quispe solicita se declare la desnaturalización de la intermediación laboral prestada a EsSalud mediante SILSA y se ordene la inclusión en planillas a plazo indeterminado (D. Leg. 728).</p>" },
      { n: 3, f: "Fjs. 26-96", d: "26/06/2019", t: "Recepción de Recaudos", des: "Ingreso formal de medios probatorios adjuntos.", title: "Recepción de Instrumental Probatoria", content: "<p>Recepción de medios probatorios adjuntos en Mesa de Partes para calificación de admisibilidad.</p>" },
      { n: 4, f: "Fjs. 97", d: "11/07/2019", t: "Redistribución", des: "Pasa al Juzgado de Trabajo Zona Norte.", title: "Oficio de Redistribución Jurisdiccional", content: "<p>Cúmplase con la Res. Adm. N° 232-2019-CE-PJ derivando la causa laboral al Juzgado Especializado de Trabajo - Sede Juliaca.</p>" },
      { n: 5, f: "Fjs. 98", d: "12/07/2019", t: "Razón de Secretaría", des: "Secretaria Rosario Carlos Villán asume causa.", title: "Razón de Secretaría", content: "<p>Doy cuenta a fojas 98 que asumo funciones de especialista legal de causa. Rosario Carlos Villán.</p>" },
      { n: 6, f: "Fjs. 99", d: "13/08/2019", t: "Resolución N° 01", des: "Admisorio provisional: concede 3 días.", title: "Resolución N° 01 - Admisorio Provisional", content: "<p><strong>JUZGADO DE TRABAJO ZONA NORTE - JULIACA</strong></p><p>RESOLUCIÓN NRO. 01 (13/08/2019)</p><p>SE RESUELVE: Declarar ADMISIBLE PROVISIONALMENTE la demanda y conceder tres días al actor para pronunciarse sobre SILSA. Juez: Huamán Romero.</p>" },
      { n: 7, f: "Fjs. 100", d: "15/08/2019", t: "Cédula Electrónica", des: "Notificación SINOE N° 6475-2019.", title: "Cédula SINOE N° 6475-2019", content: "<p>Notificado válidamente a la casilla electrónica 60375 del demandante.</p>" },
      { n: 8, f: "Fjs. 101-104", d: "21/08/2019", t: "Escrito N° 02", des: "Subsanación: mando ejercido por EsSalud.", title: "Escrito 02 - Absuelve Traslado", content: "<p>El accionante absuelve traslado señalando que el provecho directo del servicio y el poder de dirección lo ejerció la empresa usuaria EsSalud.</p>" },
      { n: 9, f: "Fjs. 105", d: "28/08/2019", t: "Resolución N° 02", des: "Admite formalmente la demanda a trámite.", title: "Resolución N° 02 - Auto Admisorio", content: "<p><strong>RESOLUCIÓN NRO. 02 (28/08/2019)</strong></p><p>SE RESUELVE: Tener por subsanada la demanda y ADMITIR A TRÁMITE en la vía ordinaria laboral. Córrase traslado a EsSalud por diez días bajo apercibimiento de rebeldía.</p>" },
      { n: 10, f: "Fjs. 106", d: "05/09/2019", t: "Cédula Electrónica", des: "Notificación SINOE N° 63800-2019.", title: "Cédula SINOE N° 63800-2019", content: "<p>Notificación electrónica formal del admisorio de la demanda al actor.</p>" },
      { n: 11, f: "Fjs. 107", d: "10/09/2019", t: "Cédula Física", des: "Emplazamiento formal a EsSalud Juliaca.", title: "Cédula de Emplazamiento N° 7304-2019", content: "<p>Emplazamiento presencial a EsSalud en Av. Santos Chocano S/N, La Capilla, Juliaca.</p>" },
      { n: 12, f: "Fjs. 108-124+", d: "25/09/2019", t: "Contestación", des: "EsSalud contesta mediante apoderado.", title: "Contestación de Demanda - EsSalud", content: "<p>EsSalud se apersona mediante Hernán López Alférez, señala casilla 59629 y solicita declarar infundada la demanda alegando falta de vacante en el CAP.</p>" }
    ];

    // CONTROL CENTRALIZADO DE PANTALLAS (P0, P1, P2, P4, P5)
    function switchScreen(screenNum) {
      document.querySelectorAll('.screen-stage').forEach(el => el.classList.remove('active'));
      const target = document.getElementById('screen-' + screenNum);
      if (target) target.classList.add('active');
      window.scrollTo(0, 0);

      if (screenNum === 1) startDynamicLoader('p1-progress-bar', 'p1-percentage', 2);
      if (screenNum === 4) startDynamicLoader('p4-progress-bar', 'p4-percentage', 5);
      if (screenNum === 5) renderScreen5Content();
    }

    // CARGADOR DINÁMICO 0% A 100%
    function startDynamicLoader(barId, pctId, nextScreen) {
      let pct = 0;
      const bar = document.getElementById(barId);
      const text = document.getElementById(pctId);
      bar.style.width = '0%';
      text.innerText = '0%';

      const interval = setInterval(() => {
        pct += 20;
        bar.style.width = pct + '%';
        text.innerText = pct + '%';
        if (pct >= 100) {
          clearInterval(interval);
          setTimeout(() => switchScreen(nextScreen), 150);
        }
      }, 50);
    }

    // WORKFLOW DE BÚSQUEDA
    function startSearchFlow() {
      openModal('modal-captcha');
      generateRandomCaptcha();
    }

    function cancelSearchFlow() {
      document.getElementById('panel-search-form').style.display = 'none';
      document.getElementById('box-temis-blank').style.display = 'block';
    }

    function toggleSearchTab(mode) {
      const btnC = document.getElementById('btn-tab-code');
      const btnP = document.getElementById('btn-tab-party');
      const boxC = document.getElementById('fields-by-code');
      const boxP = document.getElementById('fields-by-party');

      if (mode === 'code') {
        btnC.style.background = '#750e2e';
        btnC.style.color = 'white';
        btnP.style.background = '#e2e8f0';
        btnP.style.color = '#334155';
        boxC.style.display = 'block';
        boxP.style.display = 'none';
      } else {
        btnP.style.background = '#750e2e';
        btnP.style.color = 'white';
        btnC.style.background = '#e2e8f0';
        btnC.style.color = '#334155';
        boxP.style.display = 'block';
        boxC.style.display = 'none';
      }
    }

    // CAPTCHA
    let currentCaptchaCode = "";
    function generateRandomCaptcha() {
      const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      let res = "";
      for (let i = 0; i < 5; i++) res += chars.charAt(Math.floor(Math.random() * chars.length));
      currentCaptchaCode = res;
      document.getElementById('captcha-display-text').innerText = res;
      document.getElementById('captcha-input-field').value = "";
      document.getElementById('captcha-error-text').style.display = 'none';
    }

    function validateCaptchaAction() {
      const input = document.getElementById('captcha-input-field').value.trim().toUpperCase();
      if (input === currentCaptchaCode) {
        closeModal('modal-captcha');
        openModal('modal-comunicado');
      } else {
        document.getElementById('captcha-error-text').style.display = 'block';
        generateRandomCaptcha();
      }
    }

    function acceptComunicadoAndShowSearch() {
      closeModal('modal-comunicado');
      switchScreen(2);
      document.getElementById('box-temis-blank').style.display = 'none';
      document.getElementById('panel-search-form').style.display = 'block';
    }

    // MODALES
    function openModal(id) { document.getElementById(id).style.display = 'flex'; }
    function closeModal(id) { document.getElementById(id).style.display = 'none'; }

    // BOTONES DE NAVEGACIÓN TOTALMENTE FUNCIONALES
    function openInfoView(topic) {
      const title = document.getElementById('info-modal-heading');
      const body = document.getElementById('info-modal-text');

      if (topic === 'mision') {
        title.innerText = "Misión Institucional del Poder Judicial";
        body.innerHTML = "<p>Administrar Justicia a través de sus órganos jurisdiccionales, con arreglo a la Constitución y a las leyes, garantizando la seguridad jurídica, la tutela jurisdiccional efectiva y el Estado de Derecho en todo el territorio de la República del Perú.</p>";
      } else if (topic === 'vision') {
        title.innerText = "Visión del Poder Judicial";
        body.innerHTML = "<p>Ser un Poder del Estado moderno, autónomo, eficiente y transparente, reconocido por brindar una justicia célere, confiable e inclusiva con estándares de calidad y ética.</p>";
      } else if (topic === 'transparencia') {
        title.innerText = "Portal de Transparencia Estándar";
        body.innerHTML = "<p>En cumplimiento de la Ley de Transparencia y Acceso a la Información Pública, la Corte Superior de Justicia de Puno pone a disposición ciudadana el acceso a contrataciones, presupuestos anuales, directorio judicial y resoluciones administrativas.</p>";
      } else if (topic === 'contactanos') {
        title.innerText = "Sedes y Canales de Atención";
        body.innerHTML = "<p><strong>Sede Central Juliaca:</strong> Jr. Apurímac / Pumacahua, San Román, Puno.<br><strong>Módulo Laboral Zona Norte:</strong> Jr. Mariano Núñez N° 139, Juliaca.<br><strong>Central Telefónica:</strong> (051) 507000.</p>";
      }
      openModal('modal-info-view');
    }

    // INTEROPERABILIDAD RENIEC (CENSURADA)
    function openReniecProtectedModal(nom, dni) {
      document.getElementById('reniec-txt-nom').innerText = nom.split(' ')[0] + " ********";
      document.getElementById('reniec-txt-ape').innerText = (nom.split(' ')[1] || 'QUISPE') + " ********";
      document.getElementById('reniec-txt-dni').innerText = dni.substring(0, 4) + "****";
      openModal('modal-reniec');
    }

    function openGenericInterop(org, nom, doc, desc) {
      document.getElementById('gen-interop-heading').innerText = "Interoperabilidad: " + org;
      document.getElementById('gen-interop-person').innerText = nom;
      document.getElementById('gen-interop-number').innerText = doc;
      document.getElementById('gen-interop-details').innerText = desc;
      openModal('modal-generic-interop');
    }

    // VISOR DE RESOLUCIONES / DOCUMENTOS TIPO PDF
    let pdfScaleLevel = 1;
    function openPdfDocument(num) {
      const act = ACTUADOS.find(a => a.n === num);
      if (!act) return;
      pdfScaleLevel = 1;
      document.getElementById('pdf-doc-name').innerText = `${act.t.replace(/[^a-zA-Z0-9]/g, '_')}.pdf`;
      const paper = document.getElementById('pdf-doc-paper');
      paper.style.transform = `scale(${pdfScaleLevel})`;
      paper.innerHTML = `
        <div style="border-bottom: 2px solid #334155; padding-bottom: 8px; margin-bottom: 14px; display: flex; justify-content: space-between;">
          <strong>PODER JUDICIAL DEL PERÚ</strong>
          <span style="font-size: 11px;">${act.f}</span>
        </div>
        <h3 style="font-size: 14px; margin-bottom: 10px;">${act.title}</h3>
        <div>${act.content}</div>
        <div style="margin-top: 35px; border-top: 1px dashed #94a3b8; padding-top: 10px; font-size: 10px; color: #64748b;">
          Documento suscrito con Firma Digital Oficial conforme a la Ley N° 27269. Código de verificación electrónica: PJ-${act.n}9827319028.
        </div>
      `;
      openModal('modal-pdf-view');
    }

    function zoomPdfDoc(delta) {
      pdfScaleLevel += delta;
      if (pdfScaleLevel < 0.7) pdfScaleLevel = 0.7;
      if (pdfScaleLevel > 1.4) pdfScaleLevel = 1.4;
      document.getElementById('pdf-doc-paper').style.transform = `scale(${pdfScaleLevel})`;
    }

    function downloadPdfSimulated() {
      const link = document.createElement('a');
      link.href = 'data:text/plain;charset=utf-8,' + encodeURIComponent('Expediente Judicial Electrónico 00174-2019-0-2111-JR-LA-02');
      link.download = document.getElementById('pdf-doc-name').innerText;
      link.click();
    }

    // RENDERIZADO PANTALLA 5
    function renderScreen5Content() {
      // 1. Línea de tiempo
      const tBox = document.getElementById('timeline-flow-box');
      tBox.innerHTML = '';
      [ACTUADOS[0], ACTUADOS[1], ACTUADOS[3], ACTUADOS[5], ACTUADOS[8], ACTUADOS[11]].forEach(item => {
        const div = document.createElement('div');
        div.className = 'timeline-node';
        div.innerHTML = `
          <div class="timeline-dot"></div>
          <div class="timeline-card">
            <div style="display:flex; justify-content:space-between; font-size:11px; margin-bottom:2px;">
              <strong style="color:#750e2e;">${item.t}</strong>
              <span style="color:#64748b; font-family:monospace;">${item.d}</span>
            </div>
            <div style="font-size:11px; color:#334155; margin-bottom:6px;">${item.des}</div>
            <button onclick="openPdfDocument(${item.n})" style="background:#750e2e; color:white; border:none; padding:3px 8px; border-radius:4px; font-size:10px; cursor:pointer;">Ver PDF</button>
          </div>
        `;
        tBox.appendChild(div);
      });

      // 2. Tabla de actuados
      const tbody = document.getElementById('acts-table-body');
      tbody.innerHTML = '';
      ACTUADOS.forEach(a => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td style="padding:7px; text-align:center; font-weight:bold;">${a.n < 10 ? '0' + a.n : a.n}</td>
          <td style="padding:7px; font-family:monospace;">${a.f}</td>
          <td style="padding:7px;">${a.d}</td>
          <td style="padding:7px; font-weight:bold; color:#750e2e;">${a.t}</td>
          <td style="padding:7px; text-align:center;">
            <button onclick="openPdfDocument(${a.n})" style="background:#be185d; color:white; border:none; padding:4px 8px; border-radius:4px; font-size:11px; cursor:pointer;">📄 Ver PDF</button>
          </td>
        `;
        tbody.appendChild(tr);
      });
    }

    // CHATBOT IURISNIANO (CONTEXTUAL DEL EXPEDIENTE)
    function toggleChatbotWindow() {
      const w = document.getElementById('chatbot-dialog');
      w.style.display = w.style.display === 'flex' ? 'none' : 'flex';
    }

    function quickAskBot(text) {
      document.getElementById('chatbot-text-input').value = text;
      sendChatMessage();
    }

    function sendChatMessage() {
      const input = document.getElementById('chatbot-text-input');
      const val = input.value.trim();
      if (!val) return;

      const log = document.getElementById('chatbot-log');
      const uMsg = document.createElement('div');
      uMsg.style = "background:#750e2e; color:white; padding:8px 12px; border-radius:12px; max-width:85%; align-self:flex-end;";
      uMsg.innerText = val;
      log.appendChild(uMsg);
      input.value = "";

      const q = val.toLowerCase();
      let resp = "¡Con gusto te oriento! 😊 Puedes revisar la sección IV de Seguimiento o preguntarme por alguna foja o resolución específica.";

      if (q.includes("demanda") || q.includes("escrito 01") || q.includes("donde esta la demanda")) {
        resp = "¡Por supuesto! La demanda laboral se encuentra en el **Actuado N° 02, a Fojas 2 al 26**. Fue presentada el 26/06/2019 solicitando la desnaturalización con EsSalud. 📄";
      } else if (q.includes("juez") || q.includes("quien es el juez")) {
        resp = "El juez titular del despacho es el magistrado **Gonzalo Víctor Huamán Romero**, del Juzgado de Trabajo Zona Norte de Juliaca. ⚖️";
      } else if (q.includes("secretaria") || q.includes("especialista")) {
        resp = "La especialista legal a cargo de la causa es la Dra. **Rosario Carlos Villán**. ✍️";
      } else if (q.includes("resolucion 1") || q.includes("resolucion 01")) {
        resp = "La **Resolución N° 01** fue dictada el 13/08/2019 (Actuado N° 06, Fojas 99), requiriendo al demandante pronunciarse sobre SILSA en un plazo de 3 días.";
      } else if (q.includes("resolucion 2") || q.includes("resolucion 02") || q.includes("admisorio")) {
        resp = "El auto admisorio definitivo es la **Resolución N° 02** (Actuado N° 09, Fojas 105), emitida el 28/08/2019 corriendo traslado a EsSalud. 🏛️";
      } else if (q.includes("partes") || q.includes("demandante")) {
        resp = "El demandante es **Andrés Leonidas Supo Quispe** y la entidad demandada es **EsSalud Red Juliaca**. Toda su interoperabilidad con RENIEC y PNP está disponible en la Sección III. 🔍";
      }

      setTimeout(() => {
        const bMsg = document.createElement('div');
        bMsg.style = "background:#ffffff; padding:8px 12px; border-radius:12px; border:1px solid var(--mag-border); max-width:85%; align-self:flex-start;";
        bMsg.innerHTML = resp;
        log.appendChild(bMsg);
        log.scrollTop = log.scrollHeight;
      }, 350);
    }

    // MULTI-IDIOMA DINÁMICO (ES / EN)
    var DICTIONARY = {
      es: {
        appTitle: "CEJ Electrónico - CSJ Puno",
        home: "Inicio", mision: "Misión", vision: "Visión", transp: "Transparencia", contact: "Contáctanos", searchBtn: "🔍 Búsqueda de Expediente",
        sessionLbl: "Sesión:",
        p0Head: "SISTEMA DE CONSULTA DE EXPEDIENTES (CEJ / EJE)",
        p0Sub: "Simulación Jurisdiccional para Derecho e Informática",
        p0Btn: "Ingresar al Sistema Jurisdiccional",
        p1Title: "Estableciendo Conexión Cifrada", p1Desc: "Accediendo a la Sede Central Juliaca - CSJ Puno...",
        p4Title: "Indexando Cuaderno Laboral Digital", p4Desc: "Recuperando resoluciones, notificaciones y fojas...",
        secI: "I. REPORTE DE EXPEDIENTE", secII: "II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO", secIII: "III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)", secIV: "IV. SEGUIMIENTO DEL EXPEDIENTE (NOTIFICACIONES Y RESOLUCIONES)"
      },
      en: {
        appTitle: "Electronic Case Tracking - Puno",
        home: "Home", mision: "Mission", vision: "Vision", transp: "Transparency", contact: "Contact", searchBtn: "🔍 Case Search",
        sessionLbl: "Session:",
        p0Head: "ELECTRONIC COURT RECORD INQUIRY (CEJ / EJE)",
        p0Sub: "Academic Simulation for Digital Government and IT Law",
        p0Btn: "Access Jurisdictional System",
        p1Title: "Establishing Encrypted Connection", p1Desc: "Connecting to Juliaca Headquarters - CSJ Puno...",
        p4Title: "Indexing Digital Case File", p4Desc: "Retrieving case orders, service notices and filings...",
        secI: "I. CASE REPORT", secII: "II. STATUS, PROGRESS AND TIMELINE", secIII: "III. PROCEDURAL PARTIES (INTEROPERABILITY)", secIV: "IV. CASE TRACKING (NOTIFICATIONS AND RESOLUTIONS)"
      }
    };

    function switchLanguage(lang) {
      document.getElementById('btn-lang-es').className = lang === 'es' ? 'lang-btn active' : 'lang-btn';
      document.getElementById('btn-lang-en').className = lang === 'en' ? 'lang-btn active' : 'lang-btn';

      const d = DICTIONARY[lang];
      document.getElementById('txt-app-title').innerText = d.appTitle;
      document.getElementById('nav-item-home').innerText = d.home;
      document.getElementById('nav-item-mision').innerText = d.mision;
      document.getElementById('nav-item-vision').innerText = d.vision;
      document.getElementById('nav-item-transp').innerText = d.transp;
      document.getElementById('nav-item-contact').innerText = d.contact;
      document.getElementById('nav-item-search').innerText = d.searchBtn;
      document.getElementById('txt-session-label').innerText = d.sessionLbl;

      document.getElementById('p0-heading').innerText = d.p0Head;
      document.getElementById('p0-subheading').innerText = d.p0Sub;
      document.getElementById('p0-btn-submit').innerHTML = `<span>${d.p0Btn}</span> →`;

      document.getElementById('p1-loader-title').innerText = d.p1Title;
      document.getElementById('p1-loader-desc').innerText = d.p1Desc;

      document.getElementById('p4-loader-title').innerText = d.p4Title;
      document.getElementById('p4-loader-desc').innerText = d.p4Desc;

      document.getElementById('sec-i-title').innerText = d.secI;
      document.getElementById('sec-ii-title').innerText = d.secII;
      document.getElementById('sec-iii-title').innerText = d.secIII;
      document.getElementById('sec-iv-title').innerText = d.secIV;
    }

    // TEMPORIZADOR DE SESIÓN DE 7 MINUTOS (420 SEGUNDOS)
    var sessionTimeLeft = 420;
    setInterval(() => {
      sessionTimeLeft--;
      if (sessionTimeLeft <= 0) {
        alert("Su sesión de 7 minutos ha finalizado por seguridad. Redirigiendo al inicio.");
        location.reload();
      }
      const m = Math.floor(sessionTimeLeft / 60);
      const s = sessionTimeLeft % 60;
      document.getElementById('clock-display').innerText = (m < 10 ? '0' + m : m) + ':' + (s < 10 ? '0' + s : s);
    }, 1000);
  </script>
</body>
</html>
