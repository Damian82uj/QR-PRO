
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de QR Avanzado - ViralPro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --primary: #8a2be2;
            --secondary: #5d3fd3;
            --accent: #ff6b6b;
            --light: #f0f8ff;
            --dark: #1a1a2e;
            --success: #4ade80;
            --warning: #fbbf24;
            --error: #ef4444;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea, #764ba2);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: var(--dark);
        }
        
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 1200px;
            overflow: hidden;
            position: relative;
        }
        
        header {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            padding: 25px 30px;
            text-align: center;
            position: relative;
        }
        
        .pattern {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.1;
            background-image: 
                radial-gradient(circle at 10% 20%, #ff6b6b 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, #4ade80 0%, transparent 20%);
        }
        
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            position: relative;
        }
        
        header p {
            font-size: 1.1rem;
            opacity: 0.9;
            position: relative;
        }
        
        .content {
            display: flex;
            flex-wrap: wrap;
            padding: 30px;
        }
        
        .form-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
        }
        
        .preview-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .card {
            background: white;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
            padding: 25px;
            margin-bottom: 25px;
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            overflow: hidden;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.15);
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, var(--primary), var(--secondary));
        }
        
        .card-title {
            font-size: 1.4rem;
            margin-bottom: 20px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .form-group {
            margin-bottom: 20px;
            position: relative;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .input-container {
            position: relative;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 14px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(138, 43, 226, 0.2);
        }
        
        .input-icon {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--primary);
        }
        
        .color-group {
            display: flex;
            gap: 15px;
        }
        
        .color-picker {
            flex: 1;
        }
        
        .color-picker input {
            height: 50px;
            padding: 5px;
            cursor: pointer;
            border: none;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }
        
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 14px 25px;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            margin-top: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .btn::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -60px;
            width: 50px;
            height: 200%;
            background: rgba(255, 255, 255, 0.3);
            transform: rotate(30deg);
            transition: all 0.6s;
        }
        
        .btn:hover::after {
            left: 110%;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 15px rgba(138, 43, 226, 0.3);
        }
        
        .btn:active {
            transform: translateY(-1px);
        }
        
        .btn-secondary {
            background: linear-gradient(to right, #4b5563, #6b7280);
        }
        
        .btn-success {
            background: linear-gradient(to right, var(--success), #22c55e);
        }
        
        .btn-warning {
            background: linear-gradient(to right, var(--warning), #f59e0b);
        }
        
        .btn-error {
            background: linear-gradient(to right, var(--error), #dc2626);
        }
        
        .btn-group {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .btn-group .btn {
            flex: 1;
        }
        
        #qrcode {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 250px;
            height: 250px;
            background: white;
            border-radius: 15px;
            padding: 15px;
            margin: 0 auto;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }
        
        #qrcode:hover {
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.2);
        }
        
        #logo-overlay {
            position: absolute;
            width: 60px;
            height: 60px;
            border-radius: 10px;
            background-size: cover;
            background-position: center;
            display: none;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            border: 2px solid white;
        }
        
        .preview-controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-top: 25px;
            width: 100%;
        }
        
        .preview-controls .btn {
            width: auto;
            padding: 12px 25px;
            min-width: 180px;
        }
        
        .expiry-badge {
            background: var(--warning);
            color: white;
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            margin-top: 15px;
            display: inline-block;
            font-weight: 600;
            box-shadow: 0 3px 8px rgba(251, 191, 36, 0.4);
        }
        
        footer {
            text-align: center;
            padding: 20px;
            background: var(--light);
            color: var(--dark);
            font-size: 0.9rem;
            border-top: 1px solid #e2e8f0;
        }
        
        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }
            
            header h1 {
                font-size: 2rem;
            }
            
            .btn-group {
                flex-direction: column;
            }
        }
        
        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .feature-card {
            background: rgba(138, 43, 226, 0.08);
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            transition: transform 0.3s;
            position: relative;
            overflow: hidden;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
        }
        
        .feature-card i {
            font-size: 2.5rem;
            color: var(--primary);
            margin-bottom: 15px;
        }
        
        .feature-card h3 {
            font-size: 1.1rem;
            margin-bottom: 10px;
            color: var(--secondary);
        }
        
        .loading-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 255, 255, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10;
            border-radius: 15px;
            display: none;
        }
        
        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid rgba(138, 43, 226, 0.2);
            border-top: 5px solid var(--primary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .error-message {
            background: var(--error);
            color: white;
            padding: 10px 15px;
            border-radius: 8px;
            margin-top: 10px;
            display: none;
            font-weight: 500;
        }
        
        .qr-size-control {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }
        
        .qr-size-control input {
            flex: 1;
        }
        
        .logo-size-control {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }
        
        .logo-size-control input {
            flex: 1;
        }
        
        .size-label {
            font-weight: 600;
            min-width: 80px;
        }
        
        .history-container {
            margin-top: 20px;
            padding: 15px;
            background: rgba(138, 43, 226, 0.05);
            border-radius: 10px;
            display: none;
        }
        
        .history-title {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
            color: var(--primary);
            cursor: pointer;
        }
        
        .history-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
            gap: 10px;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease;
        }
        
        .history-item {
            width: 80px;
            height: 80px;
            border-radius: 8px;
            cursor: pointer;
            background-size: cover;
            background-position: center;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
            transition: all 0.3s;
        }
        
        .history-item:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .history-visible {
            max-height: 500px;
            margin-bottom: 10px;
        }
        
        .logo-preview {
            width: 100px;
            height: 100px;
            border-radius: 10px;
            border: 2px dashed var(--primary);
            margin: 10px auto;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            background-size: contain;
            background-position: center;
            background-repeat: no-repeat;
        }
        
        .logo-preview i {
            font-size: 2rem;
            color: #d1d5db;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="pattern"></div>
        <header>
            <h1><i class="fas fa-qrcode"></i> Generador Avanzado de Códigos QR - ViralPro</h1>
            <p>Crea códigos QR personalizados con funciones avanzadas</p>
        </header>
        
        <div class="content">
            <div class="form-section">
                <div class="card">
                    <h2 class="card-title"><i class="fas fa-edit"></i> Configuración Avanzada</h2>
                    
                    <div class="form-group">
                        <label for="qr-content">Contenido (URL, email, teléfono, texto, etc.)</label>
                        <textarea id="qr-content" rows="3" placeholder="https://www.ejemplo.com, mailto:contacto@viralpro.com, +5491112345678, o cualquier texto..."></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="qr-type">Tipo de contenido</label>
                        <div class="input-container">
                            <select id="qr-type">
                                <option value="url">URL / Sitio Web</option>
                                <option value="email">Email</option>
                                <option value="tel">Teléfono</option>
                                <option value="text">Texto</option>
                                <option value="video">Video</option>
                                <option value="wifi">WiFi</option>
                                <option value="vcard">Contacto (vCard)</option>
                            </select>
                            <i class="fas fa-caret-down input-icon"></i>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="qr-logo">Logo central</label>
                        <input type="file" id="qr-logo" accept="image/*">
                        <div class="logo-preview">
                            <i class="fas fa-image"></i>
                        </div>
                        
                        <div class="logo-size-control">
                            <span class="size-label">Tamaño:</span>
                            <input type="range" id="logo-size" min="10" max="40" value="20">
                            <span id="logo-size-value">20%</span>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Personalización</label>
                        <div class="color-group">
                            <div class="color-picker">
                                <label for="fg-color">Código</label>
                                <input type="color" id="fg-color" value="#000000">
                            </div>
                            <div class="color-picker">
                                <label for="bg-color">Fondo</label>
                                <input type="color" id="bg-color" value="#ffffff">
                            </div>
                        </div>
                        
                        <div class="qr-size-control">
                            <span class="size-label">Tamaño QR:</span>
                            <input type="range" id="qr-size" min="100" max="300" value="200">
                            <span id="qr-size-value">200px</span>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="expiry-date">Fecha de vencimiento (opcional)</label>
                        <div class="input-container">
                            <input type="date" id="expiry-date">
                            <i class="fas fa-calendar input-icon"></i>
                        </div>
                    </div>
                    
                    <div class="btn-group">
                        <button id="generate-btn" class="btn">
                            <i class="fas fa-bolt"></i> Generar QR
                        </button>
                        <button id="reset-btn" class="btn btn-secondary">
                            <i class="fas fa-redo"></i> Reiniciar
                        </button>
                    </div>
                    
                    <div id="error-message" class="error-message">
                        <i class="fas fa-exclamation-circle"></i> <span id="error-text"></span>
                    </div>
                </div>
                
                <div class="card">
                    <h2 class="card-title"><i class="fas fa-star"></i> Características Premium</h2>
                    <div class="feature-grid">
                        <div class="feature-card">
                            <i class="fas fa-sliders-h"></i>
                            <h3>Control de Tamaño</h3>
                            <p>Ajusta tamaño de QR y logo</p>
                        </div>
                        <div class="feature-card">
                            <i class="fas fa-history"></i>
                            <h3>Historial</h3>
                            <p>Accede a códigos recientes</p>
                        </div>
                        <div class="feature-card">
                            <i class="fas fa-wifi"></i>
                            <h3>WiFi y vCard</h3>
                            <p>Nuevos tipos de contenido</p>
                        </div>
                        <div class="feature-card">
                            <i class="fas fa-save"></i>
                            <h3>Exportación Avanzada</h3>
                            <p>Guarda en múltiples formatos</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="preview-section">
                <div class="card">
                    <h2 class="card-title"><i class="fas fa-eye"></i> Vista Previa</h2>
                    
                    <div id="qrcode">
                        <div class="loading-overlay">
                            <div class="spinner"></div>
                        </div>
                        <div id="qrcode-canvas"></div>
                        <div id="logo-overlay"></div>
                    </div>
                    
                    <div id="expiry-display" class="expiry-badge" style="display: none;">
                        <i class="fas fa-clock"></i> Válido hasta: <span id="expiry-date-display"></span>
                    </div>
                    
                    <div class="preview-controls">
                        <button id="download-png" class="btn btn-success">
                            <i class="fas fa-download"></i> Descargar PNG
                        </button>
                        <button id="download-svg" class="btn btn-warning">
                            <i class="fas fa-file-image"></i> Descargar SVG
                        </button>
                        <button id="export-html" class="btn btn-secondary">
                            <i class="fas fa-code"></i> Exportar HTML
                        </button>
                    </div>
                </div>
                
                <div class="card">
                    <h2 class="card-title"><i class="fas fa-lightbulb"></i> Consejos Profesionales</h2>
                    <ul style="padding-left: 20px; line-height: 1.8;">
                        <li><i class="fas fa-check-circle" style="color: var(--success);"></i> Usa colores con contraste suficiente para mejor legibilidad</li>
                        <li><i class="fas fa-check-circle" style="color: var(--success);"></i> El tamaño ideal del logo es 20-25% del código QR</li>
                        <li><i class="fas fa-check-circle" style="color: var(--success);"></i> Siempre prueba tu QR con varios dispositivos</li>
                        <li><i class="fas fa-check-circle" style="color: var(--success);"></i> Para promociones, usa fechas de vencimiento</li>
                        <li><i class="fas fa-check-circle" style="color: var(--success);"></i> El formato SVG es ideal para impresión</li>
                    </ul>
                    
                    <div class="history-container">
                        <div class="history-title" id="history-toggle">
                            <i class="fas fa-history"></i>
                            <h3>Historial de Códigos</h3>
                        </div>
                        <div class="history-grid" id="history-grid"></div>
                    </div>
                </div>
            </div>
        </div>
        
        <footer>
            <p>Generador Avanzado de Códigos QR - ViralPro &copy; 2023 | Todos los derechos reservados</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Elementos del DOM
            const qrContent = document.getElementById('qr-content');
            const qrType = document.getElementById('qr-type');
            const qrLogo = document.getElementById('qr-logo');
            const logoPreview = document.querySelector('.logo-preview');
            const logoSize = document.getElementById('logo-size');
            const logoSizeValue = document.getElementById('logo-size-value');
            const qrSize = document.getElementById('qr-size');
            const qrSizeValue = document.getElementById('qr-size-value');
            const fgColor = document.getElementById('fg-color');
            const bgColor = document.getElementById('bg-color');
            const expiryDate = document.getElementById('expiry-date');
            const generateBtn = document.getElementById('generate-btn');
            const resetBtn = document.getElementById('reset-btn');
            const downloadPng = document.getElementById('download-png');
            const downloadSvg = document.getElementById('download-svg');
            const exportHtml = document.getElementById('export-html');
            const qrcodeCanvas = document.getElementById('qrcode-canvas');
            const logoOverlay = document.getElementById('logo-overlay');
            const expiryDisplay = document.getElementById('expiry-display');
            const expiryDateDisplay = document.getElementById('expiry-date-display');
            const errorMessage = document.getElementById('error-message');
            const errorText = document.getElementById('error-text');
            const loadingOverlay = document.querySelector('.loading-overlay');
            const historyToggle = document.getElementById('history-toggle');
            const historyGrid = document.getElementById('history-grid');
            const historyContainer = document.querySelector('.history-container');
            
            let qrCode = null;
            let logoDataUrl = null;
            let qrHistory = [];
            const MAX_HISTORY = 12;
            
            // Inicializar generador
            function initQR() {
                if (qrCode) {
                    qrCode.clear();
                }
                
                qrcodeCanvas.innerHTML = '';
                logoOverlay.style.display = 'none';
                expiryDisplay.style.display = 'none';
                downloadPng.disabled = true;
                downloadSvg.disabled = true;
                exportHtml.disabled = true;
            }
            
            initQR();
            
            // Manejar cambio de tamaño del logo
            logoSize.addEventListener('input', function() {
                logoSizeValue.textContent = `${this.value}%`;
                if (logoDataUrl) {
                    updateLogoSize();
                }
            });
            
            // Manejar cambio de tamaño del QR
            qrSize.addEventListener('input', function() {
                qrSizeValue.textContent = `${this.value}px`;
                if (qrCode) {
                    generateQRCode();
                }
            });
            
            // Actualizar tamaño del logo
            function updateLogoSize() {
                const size = parseInt(logoSize.value);
                const qrContainer = document.getElementById('qrcode');
                const qrWidth = qrContainer.offsetWidth;
                const logoSizePx = (size / 100) * qrWidth;
                
                logoOverlay.style.width = `${logoSizePx}px`;
                logoOverlay.style.height = `${logoSizePx}px`;
            }
            
            // Generar código QR
            function generateQRCode() {
                const content = qrContent.value.trim();
                const qrWidth = parseInt(qrSize.value);
                const qrHeight = parseInt(qrSize.value);
                
                if (!content) {
                    showError('Por favor ingresa contenido para el código QR');
                    return;
                }
                
                // Formatear contenido según el tipo seleccionado
                let formattedContent = content;
                switch(qrType.value) {
                    case 'email':
                        if (!content.startsWith('mailto:')) {
                            formattedContent = 'mailto:' + content;
                        }
                        break;
                    case 'tel':
                        if (!content.startsWith('tel:')) {
                            formattedContent = 'tel:' + content;
                        }
                        break;
                    case 'video':
                        if (!content.startsWith('http')) {
                            showError('Por favor ingresa una URL válida para video');
                            return;
                        }
                        break;
                    case 'wifi':
                        formattedContent = `WIFI:S:${content};T:WPA;P:;H:;`;
                        break;
                    case 'vcard':
                        formattedContent = `BEGIN:VCARD\nVERSION:3.0\nFN:${content}\nEND:VCARD`;
                        break;
                }
                
                initQR();
                
                // Mostrar carga
                loadingOverlay.style.display = 'flex';
                
                // Pequeño retardo para permitir que se muestre la animación
                setTimeout(() => {
                    // Crear nuevo código QR
                    qrCode = new QRCode(qrcodeCanvas, {
                        text: formattedContent,
                        width: qrWidth,
                        height: qrHeight,
                        colorDark: fgColor.value,
                        colorLight: bgColor.value,
                        correctLevel: QRCode.CorrectLevel.H
                    });
                    
                    // Ocultar carga
                    loadingOverlay.style.display = 'none';
                    
                    // Mostrar logo si existe
                    if (logoDataUrl) {
                        logoOverlay.style.backgroundImage = `url(${logoDataUrl})`;
                        logoOverlay.style.display = 'block';
                        updateLogoSize();
                    }
                    
                    // Mostrar fecha de vencimiento si existe
                    if (expiryDate.value) {
                        const date = new Date(expiryDate.value);
                        expiryDateDisplay.textContent = date.toLocaleDateString('es-ES', {
                            day: '2-digit',
                            month: '2-digit',
                            year: 'numeric'
                        });
                        expiryDisplay.style.display = 'block';
                    }
                    
                    // Habilitar botones de descarga
                    downloadPng.disabled = false;
                    downloadSvg.disabled = false;
                    exportHtml.disabled = false;
                    
                    // Guardar en historial
                    saveToHistory();
                }, 300);
            }
            
            // Manejar logo
            qrLogo.addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (!file) return;
                
                if (!file.type.match('image.*')) {
                    showError('Por favor selecciona un archivo de imagen válido');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = function(event) {
                    logoDataUrl = event.target.result;
                    logoPreview.style.backgroundImage = `url(${logoDataUrl})`;
                    logoPreview.innerHTML = '';
                    
                    // Si ya hay un QR generado, actualizar el logo
                    if (qrCode) {
                        logoOverlay.style.backgroundImage = `url(${logoDataUrl})`;
                        logoOverlay.style.display = 'block';
                        updateLogoSize();
                    }
                };
                reader.readAsDataURL(file);
            });
            
            // Descargar PNG
            downloadPng.addEventListener('click', function() {
                html2canvas(document.getElementById('qrcode')).then(canvas => {
                    const link = document.createElement('a');
                    link.download = `qr-viralpro-${Date.now()}.png`;
                    link.href = canvas.toDataURL('image/png');
                    link.click();
                });
            });
            
            // Descargar SVG
            downloadSvg.addEventListener('click', function() {
                if (!qrCode) return;
                
                const svgContent = qrcodeCanvas.querySelector('svg').outerHTML;
                const blob = new Blob([svgContent], { type: 'image/svg+xml' });
                const link = document.createElement('a');
                link.download = `qr-viralpro-${Date.now()}.svg`;
                link.href = URL.createObjectURL(blob);
                link.click();
            });
            
            // Exportar HTML
            exportHtml.addEventListener('click', function() {
                html2canvas(document.getElementById('qrcode')).then(canvas => {
                    const qrDataUrl = canvas.toDataURL('image/png');
                    
                    const htmlContent = `
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Código QR - ViralPro</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea, #764ba2);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            padding: 20px;
        }
        .qr-container {
            text-align: center;
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            max-width: 90%;
        }
        h1 {
            color: #8a2be2;
            margin-bottom: 20px;
        }
        .qr-code {
            margin: 20px auto;
            max-width: 100%;
        }
        .expiry {
            background: #fbbf24;
            color: white;
            padding: 8px 20px;
            border-radius: 20px;
            font-weight: bold;
            display: inline-block;
            margin-top: 20px;
        }
        .footer {
            margin-top: 30px;
            color: #6b7280;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <div class="qr-container">
        <h1>Código QR - ViralPro</h1>
        <p>Escanea este código con tu dispositivo móvil</p>
        <div class="qr-code">
            <img src="${qrDataUrl}" alt="Código QR">
        </div>
                        ${expiryDate.value ? `
        <div class="expiry">
            <i class="fas fa-clock"></i> Válido hasta: ${expiryDateDisplay.textContent}
        </div>
                        ` : ''}
        <div class="footer">
            Generado por ViralPro QR Generator
        </div>
    </div>
    <script>
        // Añadir icono de reloj si hay fecha de expiración
        if (document.querySelector('.expiry')) {
            const clockIcon = document.createElement('i');
            clockIcon.className = 'fas fa-clock';
            document.querySelector('.expiry').prepend(clockIcon);
        }
    <\/script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/js/all.min.js"><\/script>
</body>
</html>`;
                    
                    const blob = new Blob([htmlContent], { type: 'text/html' });
                    const link = document.createElement('a');
                    link.download = `qr-viralpro-${Date.now()}.html`;
                    link.href = URL.createObjectURL(blob);
                    link.click();
                });
            });
            
            // Cambiar colores en tiempo real
            fgColor.addEventListener('input', function() {
                if (qrCode) {
                    qrCode._htOption.colorDark = this.value;
                    qrCode.makeCode(qrCode._htOption.text);
                    
                    if (logoDataUrl) {
                        logoOverlay.style.display = 'block';
                    }
                }
            });
            
            bgColor.addEventListener('input', function() {
                if (qrCode) {
                    qrCode._htOption.colorLight = this.value;
                    qrCode.makeCode(qrCode._htOption.text);
                    
                    if (logoDataUrl) {
                        logoOverlay.style.display = 'block';
                    }
                }
            });
            
            // Reiniciar formulario
            resetBtn.addEventListener('click', function() {
                qrContent.value = '';
                qrType.value = 'url';
                qrLogo.value = '';
                logoPreview.style.backgroundImage = '';
                logoPreview.innerHTML = '<i class="fas fa-image"></i>';
                logoDataUrl = null;
                fgColor.value = '#000000';
                bgColor.value = '#ffffff';
                expiryDate.value = '';
                logoSize.value = '20';
                logoSizeValue.textContent = '20%';
                qrSize.value = '200';
                qrSizeValue.textContent = '200px';
                
                initQR();
                hideError();
            });
            
            // Generar QR al hacer clic en el botón
            generateBtn.addEventListener('click', generateQRCode);
            
            // Mostrar/ocultar historial
            historyToggle.addEventListener('click', function() {
                historyGrid.classList.toggle('history-visible');
                historyContainer.style.display = 'block';
            });
            
            // Guardar QR en historial
            function saveToHistory() {
                // Obtener imagen del QR
                const qrImg = qrcodeCanvas.querySelector('canvas');
                if (!qrImg) return;
                
                const imgData = qrImg.toDataURL('image/png');
                
                // Agregar al inicio del historial
                qrHistory.unshift({
                    data: imgData,
                    timestamp: new Date()
                });
                
                // Limitar el historial
                if (qrHistory.length > MAX_HISTORY) {
                    qrHistory.pop();
                }
                
                // Actualizar la vista del historial
                updateHistoryView();
            }
            
            // Actualizar vista de historial
            function updateHistoryView() {
                historyGrid.innerHTML = '';
                
                qrHistory.forEach(item => {
                    const historyItem = document.createElement('div');
                    historyItem.className = 'history-item';
                    historyItem.style.backgroundImage = `url(${item.data})`;
                    
                    historyItem.addEventListener('click', function() {
                        // Cargar este QR como el actual
                        qrcodeCanvas.innerHTML = '';
                        const img = document.createElement('img');
                        img.src = item.data;
                        img.style.width = '100%';
                        qrcodeCanvas.appendChild(img);
                        
                        // Habilitar botones de descarga
                        downloadPng.disabled = false;
                        downloadSvg.disabled = false;
                        exportHtml.disabled = false;
                    });
                    
                    historyGrid.appendChild(historyItem);
                });
                
                if (qrHistory.length > 0) {
                    historyContainer.style.display = 'block';
                }
            }
            
            // Mostrar mensaje de error
            function showError(message) {
                errorText.textContent = message;
                errorMessage.style.display = 'block';
            }
            
            // Ocultar mensaje de error
            function hideError() {
                errorMessage.style.display = 'none';
            }
            
            // Ejemplo de contenido inicial
            qrContent.value = 'https://www.viralpro.com';
        });
    </script>
</body>
</html>
```

