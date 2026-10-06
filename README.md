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
      --mag-soft: #fdf2f8;
      --mag-border: #fbcfe8;
      --text-main: #0f172a;
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
    }

    /* OCULTAR BARRA SUPERIOR DE GOOGLE TRANSLATE */
    body { top: 0 !important; }
    .skiptranslate iframe { display: none !important; }

    /* CABECERA GLOBAL SIEMPRE VISIBLE */
    .global-header-sticky {
      position: sticky;
      top: 0;
      z-index: 9999;
      width: 100%;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }

    /* BANNER ACADÉMICO */
    .academic-topbar {
      background: linear-gradient(90deg, #3d0213, #831034, #3d0213);
      color: #fce7f3;
      font-size: 11px;
      font-weight: 700;
      padding: 7px 12px;
      text-align: center;
      border-bottom: 1px solid var(--mag-vivid);
      letter-spacing: 0.5px;
    }

    /* BARRA ESTATAL (CRONÓMETRO E IDIOMAS) */
    .gov-top-bar {
      background-color: var(--mag-dark);
      color: #ffffff;
      padding: 10px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }

    /* CONTROLES DE IDIOMA */
    .lang-controls {
      display: flex;
      align-items: center;
      gap: 6px;
      background: var(--mag-darkest);
      padding: 4px;
      border-radius: 8px;
      border: 1px solid #831034;
    }
    .btn-lang {
      background: #831034;
      color: white;
      border: none;
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 11px;
      font-weight: 700;
      cursor: pointer;
      transition: background 0.2s;
    }
    .btn-lang:hover { background: #be185d; }
    
    /* Adaptación del Widget de Google Translate */
    #google_translate_element select {
      background: #831034;
      color: white;
      border: none;
      padding: 4px 6px;
      border-radius: 4px;
      font-size: 11px;
      font-weight: 700;
      cursor: pointer;
      outline: none;
    }

    /* MENÚ HORIZONTAL ESTÁTICO */
    .gov-nav-horizontal {
      background-color: var(--mag-darkest);
      display: flex;
      overflow-x: auto;
      padding: 6px 12px;
      gap: 6px;
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
    .nav-item-btn:hover { background: rgba(255, 255, 255, 0.12); color: #ffffff; }

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

    /* CONTENEDOR CENTRAL DE PANTALLAS */
    .center-content {
      display: flex;
      flex-grow: 1;
      align-items: center;
      justify-content: center;
      padding: 20px 16px;
    }

    .layout-wrapper {
      max-width: 1180px;
      width: 100%;
      margin: 0 auto;
      padding: 20px 16px;
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    /* TARJETAS Y PANELES */
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
      margin-bottom: 14px;
      padding-bottom: 8px;
      border-bottom: 2px solid #fce7f3;
      display: flex;
      justify-content: space-between;
    }

    /* BOTONES GLOBALES */
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
      box-shadow: 0 4px 14px rgba(190, 24, 93, 0.3);
      transition: opacity 0.2s;
    }
    .btn-main:hover { opacity: 0.9; }

    /* BOTONES INTEROPERABILIDAD */
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
      box-shadow: 0 2px 6px rgba(0,0,0,0.15);
      transition: transform 0.2s;
    }
    .btn-interop:hover { transform: translateY(-2px) scale(1.03); }
    .btn-reniec { background: linear-gradient(135deg, #0284c7, #0369a1); }
    .btn-migra { background: linear-gradient(135deg, #d97706, #b45309); }
    .btn-pnp { background: linear-gradient(135deg, #047857, #065f46); }
    .btn-inpe { background: linear-gradient(135deg, #b91c1c, #991b1b); }

    /* BARRA PROGRESO PROCESAL */
    .process-stepper { display: flex; justify-content: space-between; position: relative; margin: 18px 0 26px; }
    .process-stepper::before { content: ''; position: absolute; top: 14px; left: 10px; right: 10px; height: 4px; background: #e2e8f0; z-index: 1; }
    .process-progress-bar { position: absolute; top: 14px; left: 10px; width: 35%; height: 4px; background: linear-gradient(90deg, #831034, #be185d); z-index: 2; }
    .step-item { position: relative; z-index: 3; text-align: center; flex: 1; }
    .step-circle { width: 30px; height: 30px; border-radius: 50%; background: #ffffff; border: 3px solid #cbd5e1; margin: 0 auto 6px; display: flex; align-items: center; justify-content: center; font-size: 11px; font-weight: bold; color: #64748b; }
    .step-item.completed .step-circle { border-color: #831034; background: #831034; color: #ffffff; }
    .step-item.active .step-circle { border-color: #be185d; background: #be185d; color: #ffffff; box-shadow: 0 0 0 3px rgba(190, 24, 93, 0.25); }

    /* LÍNEA DE TIEMPO */
    .timeline-container { position: relative; padding: 12px 0 12px 24px; border-left: 3px solid var(--mag-vivid); margin-left: 10px; }
    .timeline-event { position: relative; margin-bottom: 16px; }
    .timeline-badge { position: absolute; left: -33px; top: 2px; width: 18px; height: 18px; border-radius: 50%; background: #be185d; border: 3px solid #ffffff; }
    .timeline-card-content { background: #fdf2f8; border: 1px solid var(--mag-border); border-radius: 12px; padding: 10px 14px; }

    /* MODALES FLOTANTES */
    .modal-overlay {
      position: fixed; top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(36, 3, 21, 0.8); backdrop-filter: blur(3px);
      display: none; align-items: center; justify-content: center; padding: 14px; z-index: 20000;
    }
    .modal-card {
      background: #ffffff; border-radius: 18px; max-width: 650px; width: 100%; max-height: 90vh; overflow-y: auto;
      border: 1px solid var(--mag-border); box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }

    /* TABLAS RESPONSIVAS */
    table { width: 100%; border-collapse: collapse; font-size: 12px; }
    th { background: var(--mag-dark); color: #ffffff; text-align: left; padding: 9px 8px; }
    td { padding: 9px 8px; border-bottom: 1px solid #fce7f3; }
    .view-desktop { display: block; }
    .view-mobile { display: none; }

    @media (max-width: 768px) {
      .view-desktop { display: none; }
      .view-mobile { display: block; }
      .process-stepper { flex-wrap: wrap; gap: 8px; }
      .process-stepper::before, .process-progress-bar { display: none; }
      .split-responsive { grid-template-columns: 1fr !important; }
      .gov-top-bar { flex-direction: column; align-items: stretch; }
      .lang-controls { justify-content: space-between; }
    }
    .split-responsive { display: grid; grid-template-columns: 2fr 1fr; gap: 16px; margin-bottom: 16px; }

  </style>
  
  <!-- SCRIPT API DE GOOGLE TRANSLATE -->
  <script type="text/javascript">
    function googleTranslateElementInit() {
      new google.translate.TranslateElement({
        pageLanguage: 'es', 
        includedLanguages: 'en,fr,de,it,pt,ru,zh-CN,ja,qu,ay', 
        layout: google.translate.TranslateElement.InlineLayout.SIMPLE,
        autoDisplay: false
      }, 'google_translate_element');
    }
  </script>
  <script type="text/javascript" src="https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
</head>
<body>

  <!-- ============================================================ -->
  <!-- CABECERA GLOBAL (SIEMPRE VISIBLE EN TODAS LAS PANTALLAS)     -->
  <!-- ============================================================ -->
  <header class="global-header-sticky">
    <div class="academic-topbar">
      PRODUCTO ACADÉMICO UNIVERSITARIO - FACULTAD DE DERECHO | SIMULADOR NO OFICIAL
    </div>

    <div class="gov-top-bar">
      <div style="display: flex; align-items: center; gap: 8px;">
        <svg style="width: 22px; height: 22px; color: #fbcfe8;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 21h18"/><path d="M3 10h18"/><path d="M5 10v11"/><path d="M19 10v11"/><path d="M9 10v11"/><path d="M15 10v11"/><path d="M12 2 2 7h20L12 2z"/></svg>
        <div>
          <div style="font-size: 9px; font-weight: 800; color: #fbcfe8; letter-spacing: 0.5px;">PODER JUDICIAL DEL PERÚ</div>
          <div style="font-size: 13px; font-weight: 700;">CEJ Electrónico - Distrito Judicial de Puno</div>
        </div>
      </div>

      <!-- CONTROLES DERECHOS: CRONÓMETRO + IDIOMAS -->
      <div style="display: flex; align-items: center; gap: 8px; flex-wrap: wrap;">
        <!-- Cronómetro -->
        <div class="timer-pill" id="timer-indicator">
          <span style="font-size: 11px;">Sesión:</span>
          <strong id="timer-text">07:00</strong>
        </div>
        
        <!-- Botones de Idioma -->
        <div class="lang-controls">
          <button class="btn-lang" onclick="setLanguage('es')">ES</button>
          <button class="btn-lang" onclick="setLanguage('en')">EN</button>
          <div id="google_translate_element" style="overflow: hidden; border-radius: 4px;"></div>
        </div>
      </div>
    </div>

    <!-- Menú de Navegación Horizontal -->
    <div class="gov-nav-horizontal">
      <button onclick="showGlobalInfo('inicio')" class="nav-item-btn active">Inicio</button>
      <button onclick="showGlobalInfo('mision')" class="nav-item-btn">Misión</button>
      <button onclick="showGlobalInfo('vision')" class="nav-item-btn">Visión</button>
      <button onclick="showGlobalInfo('transparencia')" class="nav-item-btn">Transparencia</button>
      <button onclick="showGlobalInfo('contactanos')" class="nav-item-btn">Contáctanos</button>
      <button onclick="forceCaptchaFromMenu()" style="margin-left:auto; background:#be185d; color:white; border:none; padding:8px 14px; border-radius:6px; font-size:12px; font-weight:bold; cursor:pointer;">🔍 Búsqueda de Expediente</button>
    </div>
  </header>

  <!-- ============================================================ -->
  <!-- ZONA DINÁMICA DE PANTALLAS (0, 1, 2, 4, 5)                   -->
  <!-- ============================================================ -->

  <!-- PANTALLA 0: BIENVENIDA -->
  <div id="pantalla-0" class="screen-stage active center-content">
    <div class="card-academic">
      <div class="academic-header-box">
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
        <p style="font-size: 13px; color: #fce7f3; margin-top: 4px;">Simulador Académico Interactivo</p>
      </div>

      <div style="padding: 24px; text-align: left;">
        <div style="background: #fdf2f8; border: 1px solid var(--mag-border); border-radius: 12px; padding: 14px; margin-bottom: 16px;">
          <div style="font-size: 13px; margin-bottom: 6px;"><span style="color: var(--text-muted);">Estudiante:</span> <strong style="color: var(--mag-primary); font-size: 14px;"> Sonia Pilar Condori Ruelas</strong></div>
          <div style="font-size: 13px; margin-bottom: 6px;"><span style="color: var(--text-muted);">Curso:</span> <strong style="color: var(--mag-dark);"> Gobierno Digital e Informático</strong></div>
          <div style="font-size: 13px;"><span style="color: var(--text-muted);">Docente:</span> <strong style="color: var(--mag-dark);"> Dr. Michael Espinoza Coila</strong></div>
        </div>
        <div style="background: #fff1f2; border-left: 4px solid #be185d; padding: 10px 12px; border-radius: 6px; margin-bottom: 18px;">
          <p style="font-size: 11px; color: #4a0418; line-height: 1.4; font-weight: 600;">AVISO: Producto netamente académico universitario. NO es un sitio oficial del Poder Judicial del Perú.</p>
        </div>
        <button onclick="triggerScreenTransition(1, 'p1-loader', 2)" class="btn-main">
          <span>Ingresar al Sistema de Consulta</span>
        </button>
      </div>
    </div>

  <!-- PANTALLA 1: CARGA INICIAL -->
  <div id="pantalla-1" class="screen-stage center-content">
    <div style="max-width: 360px; width: 100%; text-align: center;">
      <svg style="width: 48px; height: 48px; color: #831034; margin-bottom: 12px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
      </svg>
      <h3 style="font-size: 16px; font-weight: 700; color: #4a0418;">Iniciando Servidor Jurisdiccional</h3>
      <div style="background: #fce7f3; height: 8px; border-radius: 8px; overflow: hidden; margin: 16px 0;">
        <div id="p1-loader" style="height: 100%; background: linear-gradient(90deg, #831034, #be185d); width: 0%; transition: width 0.1s;"></div>
      </div>
    </div>
  </div>

  <!-- PANTALLA 2: PORTAL PRINCIPAL, TEMIS Y FORMULARIO -->
  <div id="pantalla-2" class="screen-stage">
    <div class="layout-wrapper">
      
      <!-- Panel de Temis (Estado Inicial) -->
      <div id="p2-temis-box" onclick="showCaptchaModal()" class="panel-card" style="text-align: center; padding: 40px 16px; cursor: pointer;">
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
        <h2 style="font-size: 19px; color: #4a0418; font-weight: 800;">Portal Jurisdiccional EJE</h2>
        <p style="font-size: 13px; color: #64748b; margin: 8px auto 14px;">Haga clic aquí para ingresar el <strong>CAPTCHA</strong> e iniciar la búsqueda.</p>
        <span style="font-size: 11px; background: #be185d; color: white; padding: 6px 14px; border-radius: 20px; font-weight: bold;">Desbloquear búsqueda</span>
      </div>

      <!-- Formulario de Búsqueda (Se revela tras Comunicado) -->
      <div id="p2-search-form" class="panel-card" style="display: none; max-width: 650px; margin: 0 auto; width: 100%;">
        <div style="background: #4a0418; color: white; padding: 12px 16px; border-radius: 12px 12px 0 0; margin: -18px -18px 16px; display: flex; justify-content: space-between;">
          <strong style="font-size: 13px;">Búsqueda de Causas</strong>
        </div>
        
        <div style="display: flex; gap: 8px; margin-bottom: 14px; border-bottom: 1px solid #fce7f3; padding-bottom: 8px;">
          <button style="background: #831034; color: white; border: none; padding: 7px 14px; border-radius: 6px; font-size: 12px; font-weight: bold;">Por Expediente</button>
          <button style="background: #e2e8f0; color: #334155; border: none; padding: 7px 14px; border-radius: 6px; font-size: 12px; font-weight: bold;">Por Partes</button>
        </div>

        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(110px, 1fr)); gap: 8px; margin-bottom: 12px;">
          <div><label style="font-size: 11px; font-weight: bold; color: #64748b;">Correlativo</label><input type="text" value="00174" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;"></div>
          <div><label style="font-size: 11px; font-weight: bold; color: #64748b;">Año</label><input type="text" value="2019" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;"></div>
          <div><label style="font-size: 11px; font-weight: bold; color: #64748b;">Cuaderno</label><input type="text" value="0" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;"></div>
          <div><label style="font-size: 11px; font-weight: bold; color: #64748b;">Distrito</label><input type="text" value="2111" style="width: 100%; padding: 8px; border: 1px solid #cbd5e1; border-radius: 6px; text-align: center; font-weight: bold;"></div>
        </div>

        <button onclick="triggerScreenTransition(4, 'p4-loader', 5)" class="btn-main">Consultar Expediente Judicial</button>
      </div>

      <!-- Panel de Información General -->
      <div id="p2-info-panel" class="panel-card" style="display: none;">
        <h3 id="info-title" style="color: var(--mag-primary); font-size: 16px; margin-bottom: 8px;"></h3>
        <p id="info-desc" style="font-size: 13px; line-height: 1.6;"></p>
        <button onclick="closeInfoMenu()" style="margin-top: 14px; background: #e2e8f0; border: none; padding: 7px 14px; border-radius: 6px; font-weight: 600; cursor: pointer;">Cerrar</button>
      </div>

    </div>
  </div>

  <!-- PANTALLA 4: CARGA DE BASE DE DATOS -->
  <div id="pantalla-4" class="screen-stage center-content">
    <div style="max-width: 360px; width: 100%; text-align: center;">
      <svg style="width: 48px; height: 48px; color: #be185d; margin-bottom: 12px;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1-2.5-2.5Z"/><path d="M6 6h10"/><path d="M6 10h10"/>
      </svg>
      <h3 style="font-size: 16px; font-weight: 700; color: #4a0418;">Indexando Cuaderno Laboral Digital</h3>
      <div style="background: #fce7f3; height: 8px; border-radius: 8px; overflow: hidden; margin: 16px 0;">
        <div id="p4-loader" style="height: 100%; background: linear-gradient(90deg, #831034, #be185d); width: 0%; transition: width 0.1s;"></div>
      </div>
    </div>
  </div>

  <!-- PANTALLA 5: EXPEDIENTE JUDICIAL ELECTRÓNICO (EJE) -->
  <div id="pantalla-5" class="screen-stage">
    <div style="background: #4a0418; color: white; padding: 12px 16px; border-bottom: 2px solid #be185d;">
      <div class="layout-wrapper" style="padding: 0; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px;">
        <div>
          <div style="font-size: 10px; color: #fbcfe8; font-weight: 700;">MÓDULO DEL EXPEDIENTE EJE</div>
          <div style="font-size: 16px; font-weight: 800; font-family: monospace;">EXP. 00174-2019-0-2111-JR-LA-02</div>
        </div>
        <button onclick="activateScreen(2)" style="background: rgba(255,255,255,0.15); border: 1px solid rgba(255,255,255,0.3); color: white; padding: 6px 14px; border-radius: 6px; font-size: 12px; cursor: pointer;">← Volver</button>
      </div>
    </div>

    <div class="layout-wrapper">
      
      <!-- I. REPORTE DE EXPEDIENTE -->
      <div class="panel-card">
        <div class="panel-roman-title">
          <span>I. REPORTE DE EXPEDIENTE</span>
          <span style="font-size: 11px; background: #fdf2f8; border: 1px solid #fbcfe8; padding: 2px 8px; border-radius: 4px; font-family: monospace; color: #831034;">Barcode: 22019001742111334000038</span>
        </div>
        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; font-size: 12px;">
          <div><span style="color: #64748b; display: block;">Distrito / Sede:</span> <strong>Puno / San Román – Juliaca</strong></div>
          <div><span style="color: #64748b; display: block;">Juzgado:</span> <strong>Juzgado de Trabajo – Zona Norte</strong></div>
          <div><span style="color: #64748b; display: block;">Juez:</span> <strong>Huamán Romero, Gonzalo Víctor</strong></div>
          <div><span style="color: #64748b; display: block;">Secretaria:</span> <strong>Carlos Villán, Rosario</strong></div>
          <div><span style="color: #64748b; display: block;">Materia:</span> <strong style="color: #831034;">Desnaturalización / Ley 26636</strong></div>
        </div>
      </div>

      <!-- II. ESTADO Y LÍNEA DE TIEMPO -->
      <div class="panel-card">
        <div class="panel-roman-title">
          <span>II. ESTADO, PROGRESO Y LÍNEA DE TIEMPO</span>
          <span style="font-size: 11px; background: #ecfdf5; border: 1px solid #a7f3d0; padding: 2px 8px; border-radius: 4px; color: #047857;">Etapa: Postulatoria</span>
        </div>

        <div class="process-stepper">
          <div class="process-progress-bar"></div>
          <div class="step-item completed"><div class="step-circle">✓</div><div class="step-label">1. Postulatoria</div></div>
          <div class="step-item active"><div class="step-circle">2</div><div class="step-label" style="color: #831034;">2. Probatoria</div></div>
          <div class="step-item"><div class="step-circle">3</div><div class="step-label">3. Decisoria</div></div>
          <div class="step-item"><div class="step-circle">4</div><div class="step-label">4. Impugnatoria</div></div>
          <div class="step-item"><div class="step-circle">5</div><div class="step-label">5. Ejecución</div></div>
        </div>

        <div class="timeline-container" id="timeline-flow-list"></div>
      </div>

      <!-- III. PARTES PROCESALES E INTEROPERABILIDAD -->
      <div class="panel-card">
        <div class="panel-roman-title">
          <span>III. PARTES PROCESALES (INTEROPERABILIDAD INSTITUCIONAL)</span>
        </div>
        
        <div style="display: flex; flex-direction: column; gap: 12px;">
          <!-- Demandante -->
          <div style="background: #fdf2f8; border: 1px solid #fbcfe8; padding: 12px; border-radius: 10px;">
            <div style="font-size: 10px; color: #be185d; font-weight: 800; margin-bottom: 4px;">PARTE DEMANDANTE (DNI: 02167445)</div>
            <div style="font-size: 14px; font-weight: bold; margin-bottom: 8px;">Andrés Leonidas Supo Quispe</div>
            
            <div style="display: flex; flex-wrap: wrap; gap: 6px;">
              <button onclick="showReniecCard()" class="btn-interop btn-reniec">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC</span>
              </button>
              <button onclick="showInterop('MIGRACIONES', 'Sin alertas migratorias. Pasaporte ordinario vigente.')" class="btn-interop btn-migra">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="m4.93 4.93 4.24 4.24"/></svg>
                <span>MIGRACIONES</span>
              </button>
              <button onclick="showInterop('PNP', 'SISTEMA ESINPOL: NO REGISTRA ORDEN DE CAPTURA NI REQUISITORIA VIGENTE.')" class="btn-interop btn-pnp">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
                <span>PNP Requisitorias</span>
              </button>
              <button onclick="showInterop('INPE', 'REGISTRO PENITENCIARIO: NO REGISTRA ANTECEDENTES PENALES.')" class="btn-interop btn-inpe">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="18" height="11" x="3" y="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>
                <span>INPE Penales</span>
              </button>
            </div>
          </div>

          <!-- Demandada -->
          <div style="background: #fff1f2; border: 1px solid #fecdd3; padding: 12px; border-radius: 10px;">
            <div style="font-size: 10px; color: #e11d48; font-weight: 800; margin-bottom: 4px;">PARTE DEMANDADA (RUC: 20131257750)</div>
            <div style="font-size: 14px; font-weight: bold; margin-bottom: 8px;">EsSalud Red Asistencial Juliaca</div>
            <div style="display: flex; flex-wrap: wrap; gap: 6px;">
              <button onclick="showInterop('RENIEC Apoderado', 'Identidad validada. Facultades en Partida N° 11008571.')" class="btn-interop btn-reniec">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>RENIEC (Apoderado)</span>
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- IV. SEGUIMIENTO DEL EXPEDIENTE -->
      <div class="panel-card">
        <div class="panel-roman-title">
          <span>IV. SEGUIMIENTO DEL EXPEDIENTE (RESOLUCIONES PDF)</span>
        </div>
        <div class="view-desktop">
          <table>
            <thead>
              <tr><th>N°</th><th>Fojas</th><th>Fecha</th><th>Tipo Documento</th><th>Descripción</th><th style="text-align: center;">PDF</th></tr>
            </thead>
            <tbody id="acts-table-rows"></tbody>
          </table>
        </div>
        <div id="acts-cards-mobile" class="view-mobile"></div>
      </div>

    </div>
  </div>

  <!-- ============================================================ -->
  <!-- MODALES FLOTANTES GLOBALES                                   -->
  <!-- ============================================================ -->

  <!-- MODAL CAPTCHA -->
  <div id="modal-captcha" class="modal-overlay">
    <div class="modal-card" style="max-width: 420px; padding: 24px;">
      <h3 style="color: #4a0418; font-size: 16px; font-weight: bold; margin-bottom: 12px;">Validación CAPTCHA</h3>
      <div style="display: flex; gap: 8px; align-items: center; margin-bottom: 16px;">
        <div id="captcha-render" style="background: #240315; color: #fbcfe8; font-family: monospace; font-size: 24px; font-weight: 800; letter-spacing: 5px; padding: 8px 16px; border-radius: 8px; text-decoration: line-through;">8M4X1</div>
        <input type="text" id="captcha-input-txt" placeholder="Código" style="flex-grow: 1; padding: 10px; border: 1px solid #cbd5e1; border-radius: 8px; text-transform: uppercase; font-weight: bold;">
      </div>
      <button onclick="checkCaptcha()" class="btn-main">Validar</button>
      <div id="captcha-err" style="display: none; color: #e11d48; font-size: 12px; margin-top: 8px; text-align: center; font-weight: bold;">Error. Código inválido.</div>
    </div>
  </div>

  <!-- MODAL COMUNICADO MINJUSDH -->
  <div id="modal-comunicado" class="modal-overlay">
    <div class="modal-card" style="max-width: 520px; padding: 24px; border-top: 5px solid #831034;">
      <h3 style="color: #4a0418; font-size: 16px; font-weight: 800; margin-bottom: 12px;">COMUNICADO OFICIAL</h3>
      <div style="background: #fdf2f8; padding: 14px; border-radius: 10px; font-size: 12px; line-height: 1.6; text-align: justify; margin-bottom: 16px;">
        Se ha incluido un nuevo campo como medida de protección para que solo las partes accedan a sus expedientes, a requerimiento de la <strong>Autoridad Nacional de Protección de Datos Personales</strong> y el <strong>MINJUSDH</strong>, según la <strong>Ley N° 29733</strong> (Ley de Protección de Datos Personales).
      </div>
      <button onclick="acceptComunicado()" class="btn-main">He leído y Acepto el Comunicado</button>
    </div>
  </div>

  <!-- MODAL RENIEC CENSURADO (LEY 29733) -->
  <div id="modal-reniec" class="modal-overlay">
    <div class="modal-card" style="max-width: 560px; padding: 20px; border-top: 4px solid #0284c7;">
      <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #e2e8f0; padding-bottom: 10px; margin-bottom: 14px;">
        <strong style="color: #0369a1; font-size: 14px;">RENIEC - Ficha de Identificación Biométrica</strong>
        <button onclick="document.getElementById('modal-reniec').style.display='none'" style="background: none; border: none; font-size: 16px; cursor: pointer;">✕</button>
      </div>
      
      <div style="font-size: 10px; background: #e0f2fe; color: #0369a1; padding: 6px; border-radius: 4px; margin-bottom: 14px;">
        Info protegida por Ley N° 29733. Datos sensibles censurados (***).
      </div>

      <div style="display: grid; grid-template-columns: 120px 1fr; gap: 16px; background: white; border: 1px solid #cbd5e1; border-radius: 8px; padding: 12px;">
        <div style="text-align: center;">
          <div style="width: 100px; height: 130px; background: #f1f5f9; border: 1px solid #94a3b8; border-radius: 6px; margin: 0 auto; display: flex; align-items: center; justify-content: center; position: relative;">
            <svg style="width: 60px; height: 60px; color: #64748b;" viewBox="0 0 24 24" fill="currentColor"><path fill-rule="evenodd" d="M7.5 6a4.5 4.5 0 1 1 9 0 4.5 4.5 0 0 1-9 0ZM3.751 20.105a8.25 8.25 0 0 1 16.498 0 .75.75 0 0 1-.437.695A18.683 18.683 0 0 1 12 22.5c-2.786 0-5.433-.608-7.812-1.7a.75.75 0 0 1-.437-.695Z" clip-rule="evenodd"/></svg>
            <div style="position: absolute; bottom: 0; width: 100%; background: #0284c7; color: white; font-size: 8px; font-weight: bold; padding: 2px 0;">FOTO BIOMÉTRICA</div>
          </div>
        </div>
        <div style="font-size: 11px; line-height: 1.8;">
          <div><strong>Apellidos:</strong> SUPO QUISPE</div>
          <div><strong>Nombres:</strong> ANDRÉS LEONIDAS</div>
          <div><strong>DNI:</strong> 0216<span style="letter-spacing: 2px;">****</span></div>
          <div><strong>Fecha Nac.:</strong> **/**/197*</div>
          <div><strong>Estado Civil:</strong> Casado</div>
          <div><strong>Ubigeo:</strong> 21<span style="letter-spacing: 2px;">****</span> (Juliaca)</div>
          <div><strong>Dirección:</strong> Av. Manco Cápac 964, <span style="letter-spacing: 2px;">*******</span></div>
        </div>
      </div>
      <button onclick="document.getElementById('modal-reniec').style.display='none'" style="width: 100%; margin-top: 14px; background: #0284c7; color: white; border: none; padding: 8px; border-radius: 6px; font-weight: bold; cursor: pointer;">Cerrar Ficha</button>
    </div>
  </div>

  <!-- MODAL INTEROPERABILIDAD GENERAL -->
  <div id="modal-interop" class="modal-overlay">
    <div class="modal-card" style="max-width: 450px; padding: 20px;">
      <h4 id="int-title" style="color: #4a0418; font-size: 14px; font-weight: bold; margin-bottom: 12px; border-bottom: 1px solid #fce7f3; padding-bottom: 6px;">Consulta</h4>
      <div id="int-body" style="background: #f8fafc; border: 1px solid #e2e8f0; padding: 12px; border-radius: 6px; font-size: 12px; color: #1e293b; line-height: 1.6;"></div>
      <button onclick="document.getElementById('modal-interop').style.display='none'" style="width: 100%; margin-top: 14px; background: #475569; color: white; border: none; padding: 8px; border-radius: 6px; font-weight: bold; cursor: pointer;">Cerrar</button>
    </div>
  </div>

  <!-- MODAL VISOR PDF JUDICIAL -->
  <div id="modal-pdf" class="modal-overlay">
    <div class="modal-card" style="max-width: 680px; padding: 0; background: #525659; border-radius: 8px; overflow: hidden;">
      <div style="background: #1e293b; color: white; padding: 8px 12px; display: flex; justify-content: space-between; font-size: 11px;">
        <strong id="pdf-title">Documento.pdf</strong>
        <button onclick="document.getElementById('modal-pdf').style.display='none'" style="background: #ef4444; border: none; color: white; padding: 2px 8px; border-radius: 4px; cursor: pointer;">Cerrar ✕</button>
      </div>
      <div style="padding: 16px; display: flex; justify-content: center; max-height: 70vh; overflow-y: auto;">
        <div style="background: white; width: 100%; max-width: 580px; min-height: 600px; padding: 30px; font-family: 'Times New Roman', serif; font-size: 12px; line-height: 1.6; color: black; box-shadow: 0 4px 12px rgba(0,0,0,0.5); position: relative;">
          <div style="position: absolute; top: 40%; left: 15%; transform: rotate(-35deg); font-size: 40px; font-weight: bold; color: rgba(131,16,52,0.06); pointer-events: none;">PODER JUDICIAL</div>
          <div style="text-align: center; border-bottom: 2px solid black; padding-bottom: 10px; margin-bottom: 16px;">
            <div style="font-weight: bold;">CORTE SUPERIOR DE JUSTICIA DE PUNO</div>
            <div style="font-size: 10px;">JUZGADO DE TRABAJO - ZONA NORTE JULIACA</div>
          </div>
          <div id="pdf-content" style="text-align: justify; margin-bottom: 30px;"></div>
          <div style="border-top: 1px dashed gray; padding-top: 10px; font-family: monospace; font-size: 10px;">
            <strong>FIRMADO DIGITALMENTE POR: GONZALO VÍCTOR HUAMÁN ROMERO (JUEZ)</strong><br>
            <span style="color: #059669;">✓ Certificado Digital RENIEC/PJ Válido. SISTEMA EJE.</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- MODAL TIMEOUT -->
  <div id="modal-timeout" class="modal-overlay">
    <div class="modal-card" style="max-width: 320px; text-align: center; padding: 24px;">
      <h3 style="color: #831034; font-size: 16px; margin-bottom: 8px;">Sesión Finalizada</h3>
      <p style="font-size: 12px; color: #64748b; margin-bottom: 16px;">El tiempo de inactividad de 7 minutos ha culminado.</p>
      <button onclick="location.reload()" class="btn-main">Volver al Inicio</button>
    </div>
  </div>

  <!-- PIE DE PÁGINA -->
  <footer style="background: #240315; color: #fbcfe8; font-size: 11px; text-align: center; padding: 12px; border-top: 1px solid #4a0418;">
    Facultad de Derecho | Gobierno Digital e Informático - Docente: Dr. Michael Espinoza Coila | Estudiante: Sonia Pilar Condori Ruelas
  </footer>

  <script>
    // DATOS ESTRUCTURADOS DEL EXPEDIENTE
    var ACTS = [
      { num: 1, fojas: "Fjs. 1-2", fecha: "26/06/2019", tipo: "Cargo de Ingreso", desc: "Carátula oficial de recepción en Mesa de Partes.", html: "MESA DE PARTES DE JULIACA. Expediente N° 00174-2019-0-2111-JR-LA-02 recepcionado conforme." },
      { num: 2, fojas: "Fjs. 2-26", fecha: "26/06/2019", tipo: "Demanda Laboral", desc: "Escrito de demanda por desnaturalización.", html: "SEÑOR JUEZ: Interpongo demanda de desnaturalización de intermediación laboral contra EsSalud." },
      { num: 3, fojas: "Fjs. 97", fecha: "11/07/2019", tipo: "Oficio Redistribución", desc: "Derivación al Juzgado Especializado de Trabajo.", html: "Por disposición de la Presidencia de la Corte, se remite causa al Juzgado Laboral competente." },
      { num: 4, fojas: "Fjs. 99", fecha: "13/08/2019", tipo: "Resolución N° 01", desc: "Auto Admisorio Provisional.", html: "AUTOS Y VISTOS: Se declara ADMISIBLE PROVISIONALMENTE. Concédase 3 días para subsanar." },
      { num: 5, fojas: "Fjs. 101-104", fecha: "21/08/2019", tipo: "Escrito Subsanación", desc: "Absolución de requerimiento del demandante.", html: "Se cumple con precisar que no se emplaza a SILSA por ser EsSalud la titular real de la relación laboral." },
      { num: 6, fojas: "Fjs. 105", fecha: "28/08/2019", tipo: "Resolución N° 02", desc: "Admisorio Definitivo.", html: "AUTOS Y VISTOS: Téngase por subsanada y ADMÍTASE A TRÁMITE la demanda en la vía ordinaria." }
    ];

    // FUNCIÓN DE IDIOMAS VÍA GOOGLE TRANSLATE COOKIE
    function setLanguage(lang) {
      var combo = document.querySelector('.goog-te-combo');
      if (combo) {
        combo.value = lang;
        combo.dispatchEvent(new Event('change'));
      }
      if (lang === 'es') {
        document.cookie = "googtrans=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
        document.cookie = "googtrans=; expires=Thu, 01 Jan 1970 00:00:00 UTC; domain=" + window.location.hostname + "; path=/;";
        window.location.reload();
      }
    }

    // CONTROL DE PANTALLAS (0, 1, 2, 4, 5)
    function activateScreen(n) {
      var scrs = document.querySelectorAll('.screen-stage');
      scrs.forEach(function(s) { s.classList.remove('active'); });
      document.getElementById('pantalla-' + n).classList.add('active');
      window.scrollTo(0, 0);
    }

    function triggerScreenTransition(target, loaderId, nextTarget) {
      activateScreen(target);
      if (target === 1 || target === 4) {
        if(target === 1) startSessionTimer();
        var p = 0;
        var bar = document.getElementById(loaderId);
        bar.style.width = '0%';
        var iv = setInterval(function() {
          p += 25; bar.style.width = p + '%';
          if (p >= 100) {
            clearInterval(iv);
            setTimeout(function() { 
              if(nextTarget === 5) renderScreen5();
              activateScreen(nextTarget); 
            }, 150);
          }
        }, 50);
      }
    }

    // PANTALLA 2 LÓGICA (INFO Y BÚSQUEDA)
    function showGlobalInfo(topic) {
      if(document.getElementById('pantalla-0').classList.contains('active')) return;
      if(!document.getElementById('pantalla-2').classList.contains('active')) activateScreen(2);
      
      document.getElementById('temis-blank-box').style.display = 'none';
      document.getElementById('p2-search-form').style.display = 'none';
      document.getElementById('p2-info-panel').style.display = 'block';
      
      var t = document.getElementById('info-title'), d = document.getElementById('info-desc');
      if (topic === 'mision') { t.innerText = "Misión"; d.innerText = "Administrar Justicia garantizando el debido proceso."; }
      else if (topic === 'vision') { t.innerText = "Visión"; d.innerText = "Ser un Poder del Estado moderno y confiable."; }
      else if (topic === 'transparencia') { t.innerText = "Transparencia"; d.innerText = "Acceso público a resoluciones y presupuestos."; }
      else if (topic === 'contactanos') { t.innerText = "Contáctanos"; d.innerText = "Sede Juliaca: Jr. Apurímac. Teléfono: (051) 507000."; }
      else closeInfoMenu();
    }

    function closeInfoMenu() {
      document.getElementById('p2-info-panel').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'block';
    }

    function showCaptchaModal() {
      document.getElementById('modal-captcha').style.display = 'flex';
      var code = Math.random().toString(36).substring(2, 7).toUpperCase();
      document.getElementById('captcha-render').innerText = code;
      document.getElementById('captcha-input-txt').value = "";
      document.getElementById('captcha-err').style.display = 'none';
    }

    function forceCaptchaFromMenu() {
      if(!document.getElementById('pantalla-2').classList.contains('active')) activateScreen(2);
      closeInfoMenu();
      showCaptchaModal();
    }

    function checkCaptcha() {
      var input = document.getElementById('captcha-input-txt').value.toUpperCase();
      var real = document.getElementById('captcha-render').innerText;
      if (input === real) {
        document.getElementById('modal-captcha').style.display = 'none';
        document.getElementById('modal-comunicado').style.display = 'flex';
      } else {
        document.getElementById('captcha-err').style.display = 'block';
      }
    }

    function acceptComunicado() {
      document.getElementById('modal-comunicado').style.display = 'none';
      document.getElementById('temis-blank-box').style.display = 'none';
      document.getElementById('p2-info-panel').style.display = 'none';
      document.getElementById('p2-search-form').style.display = 'block';
    }

    // MODALES INTEROPERABILIDAD Y PDF
    function showReniecCard() { document.getElementById('modal-reniec').style.display = 'flex'; }
    function showInterop(t, res) {
      document.getElementById('int-title').innerText = t;
      document.getElementById('int-body').innerHTML = "<strong>Resultado Oficial:</strong> " + res;
      document.getElementById('modal-interop').style.display = 'flex';
    }
    
    // RENDERIZADO PANTALLA 5
    function renderScreen5() {
      // Línea de tiempo
      var tl = document.getElementById('timeline-flow-list');
      tl.innerHTML = '';
      ACTS.forEach(function(a) {
        tl.innerHTML += '<div class="timeline-event"><div class="timeline-badge"></div><div class="timeline-card-content"><strong style="color:#831034; font-size:11px;">' + a.tipo + '</strong> <span style="float:right; font-size:10px; color:gray;">' + a.fecha + '</span><div style="font-size:11px; margin-top:4px;">' + a.desc + '</div></div></div>';
      });

      // Tabla y Móvil PDF
      var tb = document.getElementById('acts-table-rows'), mc = document.getElementById('acts-cards-mobile');
      tb.innerHTML = ''; mc.innerHTML = '';
      ACTS.forEach(function(a) {
        var btn = '<button onclick="openPdf(\'' + a.tipo + '\', \'' + a.html.replace(/'/g,"\\'") + '\')" style="background:#831034; color:white; border:none; padding:4px 8px; border-radius:4px; font-size:10px; font-weight:bold; cursor:pointer;">PDF</button>';
        tb.innerHTML += '<tr><td style="text-align:center;">'+a.num+'</td><td>'+a.fojas+'</td><td>'+a.fecha+'</td><td style="color:#831034; font-weight:bold;">'+a.tipo+'</td><td>'+a.desc+'</td><td style="text-align:center;">'+btn+'</td></tr>';
        mc.innerHTML += '<div style="border:1px solid #fbcfe8; border-radius:8px; padding:10px; margin-bottom:8px; background:white;"><div style="font-weight:bold; color:#831034; font-size:12px;">'+a.tipo+'</div><div style="font-size:11px; color:gray; margin-bottom:6px;">'+a.desc+'</div>'+btn+'</div>';
      });
    }

    function openPdf(t, h) {
      document.getElementById('pdf-title').innerText = t.replace(/\s+/g, '_') + '.pdf';
      document.getElementById('pdf-content').innerHTML = h;
      document.getElementById('modal-pdf').style.display = 'flex';
    }

    // CRONÓMETRO DE 7 MINUTOS
    var timeSecs = 420, tmr;
    function startSessionTimer() {
      if(tmr) clearInterval(tmr);
      timeSecs = 420; tickTimer();
      tmr = setInterval(function() {
        timeSecs--; tickTimer();
        if(timeSecs <= 0) { clearInterval(tmr); document.getElementById('modal-timeout').style.display='flex'; }
      }, 1000);
    }
    function resetTimer() { timeSecs = 420; tickTimer(); }
    function tickTimer() {
      var m = Math.floor(timeSecs/60), s = timeSecs%60;
      var str = (m<10?'0'+m:m)+':'+(s<10?'0'+s:s);
      var el = document.getElementById('timer-text');
      var bx = document.getElementById('timer-indicator');
      if(el) el.innerText = str;
      if(timeSecs <= 60 && bx) bx.classList.add('timer-alert');
      else if(bx) bx.classList.remove('timer-alert');
    }
  </script>
</body>
</html>
