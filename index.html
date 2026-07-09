<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modern Compressor & Converter</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <style>
        /* ================= MODERN ANIMATED GRADIENT THEMES ================= */
        :root {
            --text-color: #ffffff;
            --text-muted: #b0bec5;
            --glass-bg: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
            --primary-accent: #ffffff;
            --border-radius: 16px;
        }

        body {
            margin: 0; padding: 0; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            color: var(--text-color); overflow-x: hidden; transition: background 0.5s ease;
            /* Default Theme: Dark Ocean */
            background: linear-gradient(-45deg, #0f2027, #203a43, #2c5364);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            min-height: 100vh;
        }

        body[data-theme="sunset"] { background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab); background-size: 400% 400%; }
        body[data-theme="purple"] { background: linear-gradient(-45deg, #4b134f, #c94b4b); background-size: 400% 400%; }
        body[data-theme="blue"] { background: linear-gradient(-45deg, #1e3c72, #2a5298, #00d2ff); background-size: 400% 400%; }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* ================= GLOBAL & GLASSMORPHISM ================= */
        * { box-sizing: border-box; }
        a { color: var(--primary-accent); text-decoration: none; }
        
        .glass-panel {
            background: var(--glass-bg); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border); border-radius: var(--border-radius);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3);
        }

        /* ================= SPLASH & MAIN LAYOUT ================= */
        #splash-screen {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            background: inherit;
        }
        .lang-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; width: 90%; max-width: 400px; margin-top: 20px; }
        .lang-btn {
            background: var(--glass-bg); border: 1px solid var(--glass-border); color: #fff;
            padding: 15px; border-radius: var(--border-radius); cursor: pointer; text-align: center;
            transition: all 0.3s ease;
        }
        .lang-btn:hover { background: rgba(255,255,255,0.25); transform: translateY(-3px); }

        #app-container { display: none; padding-bottom: 80px; }
        header { padding: 20px; text-align: center; border-bottom: 1px solid var(--glass-border); }
        .tab-content { display: none; padding: 20px; max-width: 900px; margin: 0 auto; animation: fadeIn 0.4s; }
        .tab-content.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* ================= CARDS & UI ELEMENTS ================= */
        .grid-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
        .tool-card { padding: 25px 20px; text-align: center; transition: transform 0.3s ease; }
        .tool-card:hover { transform: translateY(-5px); }
        .tool-card h3 { margin-bottom: 10px; font-size: 1.5rem; }
        .tool-card p { color: var(--text-muted); font-size: 0.95rem; margin-bottom: 20px; }
        
        .action-btn {
            background: rgba(255,255,255,0.15); color: #fff; border: 1px solid rgba(255,255,255,0.3);
            padding: 12px 20px; border-radius: 30px; font-weight: bold; cursor: pointer; transition: 0.3s;
            width: 100%; font-size: 1rem; backdrop-filter: blur(5px);
        }
        .action-btn:hover { background: rgba(255,255,255,0.3); }

        input[type="file"] { display: none; }

        /* ================= SETTINGS & MODALS ================= */
        .settings-item { margin-bottom: 20px; padding: 20px; }
        .theme-circle {
            display: inline-block; width: 45px; height: 45px; border-radius: 50%; margin-right: 15px;
            cursor: pointer; border: 2px solid #fff; box-shadow: 0 4px 10px rgba(0,0,0,0.3); transition: 0.3s;
        }
        .theme-circle:hover { transform: scale(1.1); }
        
        /* Modals (Config & Privacy) */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.6);
            backdrop-filter: blur(5px); display: none; justify-content: center; align-items: center; z-index: 1000;
        }
        .modal-box {
            width: 90%; max-width: 500px; max-height: 85vh; padding: 25px;
            overflow-y: auto; position: relative;
        }
        .modal-box h2 { margin-top: 0; text-align: center; }
        .close-btn { position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; color: #fff; }

        /* Config Forms */
        .form-group { margin-bottom: 15px; text-align: left; }
        .form-group label { display: block; margin-bottom: 5px; font-size: 0.9rem; color: #ddd; }
        .form-control {
            width: 100%; padding: 10px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.3);
            background: rgba(0,0,0,0.2); color: #fff; font-size: 1rem;
        }
        .form-control option { background: #2c5364; color: #fff; }
        
        /* Slider */
        input[type=range] { width: 100%; cursor: pointer; }
        
        /* Preview Area */
        #preview-area {
            width: 100%; height: 180px; background: rgba(0,0,0,0.3); border-radius: 8px; margin-bottom: 15px;
            display: flex; justify-content: center; align-items: center; overflow: hidden;
        }
        #preview-area img, #preview-area video { max-width: 100%; max-height: 100%; object-fit: contain; }
        .file-count-badge { font-size: 0.85rem; color: #ffeb3b; text-align: center; margin-top: 5px; }

        /* ================= PROCESSING SCREEN ================= */
        #processing-screen {
            display: none; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            background: inherit; z-index: 2000; flex-direction: column; align-items: center;
        }
        .progress-header { margin-top: 10vh; width: 80%; max-width: 500px; text-align: center; }
        .progress-track { width: 100%; height: 12px; background: rgba(255,255,255,0.2); border-radius: 10px; margin-top: 15px; overflow: hidden; }
        .progress-fill { height: 100%; width: 0%; background: #4caf50; transition: width 0.3s; box-shadow: 0 0 10px #4caf50; }
        
        .ad-container {
            margin-top: auto; margin-bottom: 20vh; /* Lower-Middle positioning */
            width: 300px; height: 250px; background: rgba(255,255,255,0.05);
            display: flex; justify-content: center; align-items: center; border-radius: 8px;
        }

        #result-actions { display: none; margin-top: 20px; width: 100%; gap: 10px; justify-content: center; }

        /* ================= BOTTOM NAVIGATION ================= */
        nav.bottom-nav {
            position: fixed; bottom: 0; left: 0; width: 100%;
            background: rgba(0, 0, 0, 0.4); backdrop-filter: blur(15px);
            display: flex; justify-content: space-around; padding: 15px 0; border-top: 1px solid rgba(255,255,255,0.1); z-index: 100;
        }
        .nav-item { color: var(--text-muted); cursor: pointer; font-size: 0.95rem; transition: 0.3s; }
        .nav-item.active { color: #fff; font-weight: bold; transform: scale(1.1); }
    </style>
</head>
<body>

    <div id="splash-screen">
        <h1 style="font-size: 2.5rem; margin-bottom: 5px;">Modern Tools</h1>
        <p style="color: #ddd;">Select Language / انتخاب زبان</p>
        <div class="lang-grid">
            <div class="lang-btn" onclick="initApp('en')">🇬🇧 English</div>
            <div class="lang-btn" onclick="initApp('fa')">🇦🇫 دری (Dari)</div>
        </div>
        <button class="action-btn" style="margin-top: 30px; width: auto; border: none; background: transparent; text-decoration: underline;" onclick="initApp('en')">Skip (English)</button>
    </div>

    <div id="app-container">
        <header>
            <h2 id="header-title">Compressor & Converter</h2>
        </header>

        <main id="tab-home" class="tab-content active">
            <div class="grid-container">
                <div class="glass-panel tool-card">
                    <h3 id="txt-img-title">Image Tools</h3>
                    <p id="txt-img-desc">Convert & compress up to 5 images.</p>
                    <input type="file" id="upload-image" multiple accept="image/*" onchange="handleFileSelect(event, 'image')">
                    <button class="action-btn" onclick="document.getElementById('upload-image').click()" id="txt-img-btn">Select Images</button>
                </div>
                <div class="glass-panel tool-card">
                    <h3 id="txt-video-title">Video Tools</h3>
                    <p id="txt-video-desc">Compress & convert 1 video file.</p>
                    <input type="file" id="upload-video" accept="video/*" onchange="handleFileSelect(event, 'video')">
                    <button class="action-btn" onclick="document.getElementById('upload-video').click()" id="txt-video-btn">Select Video</button>
                </div>
                <div class="glass-panel tool-card">
                    <h3 id="txt-zip-title">Zip Archiver</h3>
                    <p id="txt-zip-desc">Compress multiple files into a Zip.</p>
                    <input type="file" id="upload-zip" multiple onchange="handleFileSelect(event, 'zip')">
                    <button class="action-btn" onclick="document.getElementById('upload-zip').click()" id="txt-zip-btn">Select Files for Zip</button>
                </div>
                <div class="glass-panel tool-card">
                    <h3 id="txt-doc-title">Document Tools</h3>
                    <p id="txt-doc-desc">Convert PDF, TXT, DOCX offline.</p>
                    <input type="file" id="upload-doc" onchange="handleFileSelect(event, 'doc')">
                    <button class="action-btn" onclick="document.getElementById('upload-doc').click()" id="txt-doc-btn">Select Document</button>
                </div>
            </div>
        </main>

        <main id="tab-settings" class="tab-content">
            <div class="glass-panel settings-item">
                <h3>Visual Themes</h3>
                <div style="margin-top: 15px;">
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #0f2027, #203a43);" onclick="setTheme('default')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #ee7752, #e73c7e);" onclick="setTheme('sunset')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #1e3c72, #00d2ff);" onclick="setTheme('blue')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #4b134f, #c94b4b);" onclick="setTheme('purple')"></div>
                </div>
            </div>

            <div class="glass-panel settings-item">
                <h3>Legal & Privacy</h3>
                <button class="action-btn" onclick="document.getElementById('privacy-modal').style.display='flex'">Read Privacy Policy</button>
            </div>
        </main>

        <nav class="bottom-nav">
            <div class="nav-item active" onclick="switchTab('home', this)">🏠 Home</div>
            <div class="nav-item" onclick="switchTab('settings', this)">⚙️ Settings</div>
        </nav>
    </div>

    <div id="config-modal" class="modal-overlay">
        <div class="glass-panel modal-box">
            <span class="close-btn" onclick="closeModal('config-modal')">&times;</span>
            <h2>Configuration</h2>
            
            <div id="preview-area">
                <span style="color: #bbb;">Preview Not Available</span>
            </div>
            <div id="file-count" class="file-count-badge"></div>

            <div class="form-group">
                <label>Output File Name</label>
                <input type="text" id="config-filename" class="form-control" placeholder="Enter file name...">
            </div>

            <div class="form-group">
                <label id="format-label">Convert Format</label>
                <select id="config-format" class="form-control">
                    </select>
            </div>

            <div class="form-group">
                <label>Target Size / Quality (<span id="slider-val">80</span>%)</label>
                <input type="range" id="config-quality" min="10" max="100" value="80" oninput="document.getElementById('slider-val').innerText = this.value">
            </div>

            <button class="action-btn" style="background: #4caf50; border: none; margin-top: 10px;" onclick="startProcessing()">Start Processing</button>
        </div>
    </div>

    <div id="privacy-modal" class="modal-overlay">
        <div class="glass-panel modal-box">
            <span class="close-btn" onclick="closeModal('privacy-modal')">&times;</span>
            <h2 style="margin-bottom: 15px;">Privacy Policy</h2>
            <div style="font-size: 0.9rem; line-height: 1.6; color: #ddd; text-align: justify;">
                <p><strong>Content Compressor Privacy Policy (Operated by Abdulrahman)</strong></p>
                <p><strong>1. Information Collection:</strong> The Application collects basic usage data, IP address, and OS type to function properly.</p>
                <p><strong>2. Cookies & Ad SDKs:</strong> To keep this app free, we use third-party SDKs like AdMob which may collect non-personal data for analytics and serving ads.</p>
                <p><strong>3. Your Rights (CCPA):</strong> You have the right to request access, correction, or deletion of your personal data. California residents can opt-out of data sharing. Contact us to exercise these rights.</p>
                <p><strong>4. Data Retention & Security:</strong> User data is retained only as long as necessary (up to 12-24 months). We use physical and electronic safeguards to protect your information.</p>
                <p><strong>5. Children:</strong> Not intended for children under 3. We do not knowingly collect data from children.</p>
                <p><strong>Contact:</strong> For questions, email Abdulrahman at <em>hkymy9323@gmail.com</em>.</p>
                <p><em>Effective: 2026-07-08</em></p>
            </div>
        </div>
    </div>

    <div id="processing-screen">
        <div class="progress-header">
            <h2 id="process-title">Processing...</h2>
            <p id="process-desc">Please wait while we prepare your file(s).</p>
            <div class="progress-track">
                <div class="progress-fill" id="progress-bar"></div>
            </div>
            
            <div id="result-actions">
                <button class="action-btn" style="background: #2196f3; width: auto;" id="btn-download" onclick="downloadResult()">Download File</button>
                <button class="action-btn" style="background: transparent; width: auto;" onclick="closeProcessing()">Back Home</button>
            </div>
        </div>

        <div class="ad-container">
            <div id="ad-wrapper">
                <script>
                  atOptions = {
                    'key' : 'd3b5f554367d6f64704b6cdd8f68b658',
                    'format' : 'iframe',
                    'height' : 250,
                    'width' : 300,
                    'params' : {}
                  };
                </script>
                <script src="https://speedingdeadlyplays.com/d3b5f554367d6f64704b6cdd8f68b658/invoke.js"></script>
            </div>
        </div>
    </div>

    <script>
        // Global State
        let currentType = '';
        let selectedFiles = [];
        let processedDataUrl = null; 
        let processedBlob = null;
        let processedFilename = 'output';

        // Initialize
        function initApp(lang) {
            document.getElementById('splash-screen').style.display = 'none';
            document.getElementById('app-container').style.display = 'block';
            if(lang === 'fa') document.body.style.direction = 'rtl';
        }

        // Tabs
        function switchTab(tabId, element) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById('tab-' + tabId).classList.add('active');
            element.classList.add('active');
        }

        // Themes
        function setTheme(theme) {
            document.body.setAttribute('data-theme', theme);
        }

        function closeModal(id) {
            document.getElementById(id).style.display = 'none';
        }

        // Handle File Selection & Open Config Modal
        function handleFileSelect(event, type) {
            const files = event.target.files;
            if(!files || files.length === 0) return;

            // Enforce Limits
            if(type === 'image' && files.length > 5) {
                alert("You can only select up to 5 images.");
                event.target.value = ''; return;
            }
            if(type === 'video' && files.length > 1) {
                alert("You can only select 1 video at a time.");
                event.target.value = ''; return;
            }

            currentType = type;
            selectedFiles = Array.from(files);
            
            // Setup Config Modal UI
            const firstFile = selectedFiles[0];
            const originalName = firstFile.name.substring(0, firstFile.name.lastIndexOf('.')) || firstFile.name;
            const originalExt = firstFile.name.split('.').pop().toUpperCase();
            
            document.getElementById('config-filename').value = originalName;
            document.getElementById('file-count').innerText = selectedFiles.length > 1 ? `${selectedFiles.length} files selected` : '';

            // Setup Format Dropdown based on type
            const formatSelect = document.getElementById('config-format');
            const formatLabel = document.getElementById('format-label');
            formatSelect.innerHTML = '';
            
            let options = [];
            if(type === 'image') options = ['WebP', 'JPG', 'PNG'];
            if(type === 'video') options = ['MP4', 'MKV', 'WebM'];
            if(type === 'doc') options = ['PDF', 'TXT', 'DOCX'];
            if(type === 'zip') options = ['ZIP'];

            formatLabel.innerText = `Convert from [${originalExt}] to:`;
            options.forEach(opt => {
                const el = document.createElement('option');
                el.value = opt.toLowerCase(); el.innerText = opt;
                formatSelect.appendChild(el);
            });

            // Handle Previews
            const previewArea = document.getElementById('preview-area');
            previewArea.innerHTML = ''; // clear

            if(type === 'image') {
                const img = document.createElement('img');
                img.src = URL.createObjectURL(firstFile);
                previewArea.appendChild(img);
            } else if(type === 'video') {
                const vid = document.createElement('video');
                vid.src = URL.createObjectURL(firstFile);
                vid.controls = true;
                previewArea.appendChild(vid);
            } else {
                previewArea.innerHTML = `<div style="text-align:center; color:#fff;">
                    <h1 style="margin:0;">📄</h1>
                    <p>${firstFile.name}</p>
                </div>`;
            }

            document.getElementById('config-modal').style.display = 'flex';
        }

        // Start Processing Flow
        function startProcessing() {
            document.getElementById('config-modal').style.display = 'none';
            document.getElementById('app-container').style.display = 'none';
            document.getElementById('processing-screen').style.display = 'flex';
            
            document.getElementById('result-actions').style.display = 'none';
            const bar = document.getElementById('progress-bar');
            bar.style.width = '0%';

            const targetFormat = document.getElementById('config-format').value;
            processedFilename = document.getElementById('config-filename').value + '.' + targetFormat;
            const quality = document.getElementById('config-quality').value / 100;

            // Simulate or Execute Real logic
            if(currentType === 'image' && targetFormat === 'webp') {
                processImageToWebp(selectedFiles[0], quality, bar);
            } else if(currentType === 'zip') {
                processZip(selectedFiles, bar);
            } else {
                // Simulate processing for Video/Doc since it requires heavy external WASM libraries
                simulateProcessing(bar);
            }
        }

        // Simulated Progress (For Video/Docs)
        function simulateProcessing(bar) {
            let width = 0;
            const int = setInterval(() => {
                width += Math.random() * 15;
                if(width >= 100) { width = 100; clearInterval(int); finishProcessing(); }
                bar.style.width = width + '%';
            }, 400);
        }

        // Real Image to WebP using Canvas
        function processImageToWebp(file, quality, bar) {
            const reader = new FileReader();
            reader.onload = function(e) {
                bar.style.width = '40%';
                const img = new Image();
                img.onload = function() {
                    bar.style.width = '70%';
                    const canvas = document.createElement('canvas');
                    canvas.width = img.width; canvas.height = img.height;
                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0);
                    processedDataUrl = canvas.toDataURL('image/webp', quality);
                    bar.style.width = '100%';
                    setTimeout(finishProcessing, 500);
                }
                img.src = e.target.result;
            }
            reader.readAsDataURL(file);
        }

        // Real Zip Archiving using JSZip
        function processZip(files, bar) {
            if(typeof JSZip === 'undefined') {
                alert("JSZip library not loaded (Internet required for demo). Simulating...");
                simulateProcessing(bar);
                return;
            }
            const zip = new JSZip();
            let count = 0;
            
            files.forEach(file => {
                zip.file(file.name, file);
                count++;
                bar.style.width = (count / files.length * 50) + '%';
            });

            zip.generateAsync({type:"blob"}, function updateCallback(metadata) {
                bar.style.width = (50 + (metadata.percent / 2)) + '%';
            }).then(function (content) {
                processedBlob = content;
                bar.style.width = '100%';
                setTimeout(finishProcessing, 500);
            });
        }

        function finishProcessing() {
            document.getElementById('process-title').innerText = "Complete!";
            document.getElementById('process-desc').innerText = "Your file is ready to download.";
            document.getElementById('result-actions').style.display = 'flex';
        }

        function downloadResult() {
            const link = document.createElement('a');
            link.download = processedFilename;
            
            if(currentType === 'image' && processedDataUrl) {
                link.href = processedDataUrl;
            } else if(currentType === 'zip' && processedBlob) {
                link.href = URL.createObjectURL(processedBlob);
            } else {
                alert("Demo Note: Real output generated for Image(WebP) and Zip. Video/Docs require backend/local libs in Flutter.");
                return;
            }
            
            link.click();
        }

        function closeProcessing() {
            document.getElementById('processing-screen').style.display = 'none';
            document.getElementById('app-container').style.display = 'block';
            
            // Reset inputs
            document.querySelectorAll('input[type="file"]').forEach(i => i.value = '');
            document.getElementById('process-title').innerText = "Processing...";
            document.getElementById('process-desc').innerText = "Please wait while we prepare your file(s).";
            processedDataUrl = null; processedBlob = null;
        }

    </script>
</body>
</html>
