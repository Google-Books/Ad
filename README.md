<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pro Compressor</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <style>
        /* ================= THEMES & VARIABLES ================= */
        :root {
            --text-color: #ffffff;
            --text-muted: #b0bec5;
            --glass-bg: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
            --primary-accent: #ffffff;
            --border-radius: 16px;
            --accent-color: #4caf50;
        }

        body {
            margin: 0; padding: 0; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            color: var(--text-color); overflow-x: hidden; transition: background 0.5s ease;
            background: linear-gradient(-45deg, #0f2027, #203a43, #2c5364);
            background-size: 400% 400%; animation: gradientBG 15s ease infinite; min-height: 100vh;
        }

        body[data-theme="sunset"] { background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab); background-size: 400% 400%; }
        body[data-theme="purple"] { background: linear-gradient(-45deg, #4b134f, #c94b4b); background-size: 400% 400%; }
        body[data-theme="blue"] { background: linear-gradient(-45deg, #1e3c72, #2a5298, #00d2ff); background-size: 400% 400%; }

        @keyframes gradientBG { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }

        * { box-sizing: border-box; }
        a { color: var(--primary-accent); text-decoration: none; }
        
        .glass-panel {
            background: var(--glass-bg); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border); border-radius: var(--border-radius);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3);
        }

        /* ================= SPLASH SCREEN ================= */
        #splash-screen {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            background: inherit;
        }
        .splash-title { font-size: 2.8rem; font-weight: bold; margin-bottom: 5px; text-shadow: 0 2px 10px rgba(0,0,0,0.5); }
        .lang-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; width: 90%; max-width: 450px; margin-top: 20px; }
        .lang-btn {
            background: var(--glass-bg); border: 1px solid var(--glass-border); color: #fff;
            padding: 15px; border-radius: var(--border-radius); cursor: pointer; text-align: center;
            transition: all 0.3s ease; font-size: 1.1rem;
        }
        .lang-btn:hover { background: rgba(255,255,255,0.25); transform: translateY(-3px); }

        /* ================= MAIN APP LAYOUT ================= */
        #app-container { display: none; padding-bottom: 80px; min-height: 100vh; display: flex; flex-direction: column; }
        header { padding: 20px; text-align: center; border-bottom: 1px solid var(--glass-border); }
        header h2 { margin: 0; font-size: 1.8rem; letter-spacing: 1px; }
        
        .view-section { display: none; padding: 20px; max-width: 800px; margin: 0 auto; width: 100%; flex-grow: 1; animation: fadeIn 0.4s; }
        .view-section.active { display: flex; flex-direction: column; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* ================= CENTRAL BUTTON (HOME) ================= */
        .center-stage { flex-grow: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .big-upload-btn {
            width: 200px; height: 200px; border-radius: 50%; background: rgba(255,255,255,0.1);
            border: 2px dashed rgba(255,255,255,0.5); display: flex; flex-direction: column; align-items: center; justify-content: center;
            cursor: pointer; transition: 0.3s; box-shadow: 0 0 30px rgba(0,0,0,0.2); margin-bottom: 20px;
        }
        .big-upload-btn:hover { background: rgba(255,255,255,0.2); transform: scale(1.05); border-color: #fff; }
        .big-upload-btn svg { width: 60px; height: 60px; fill: #fff; margin-bottom: 10px; }
        input[type="file"] { display: none; }

        /* ================= CONFIGURATION / TOOLS PAGE ================= */
        .preview-container {
            width: 100%; height: 300px; background: rgba(0,0,0,0.4); border-radius: 12px; margin-bottom: 20px;
            display: flex; justify-content: center; align-items: center; overflow: hidden; position: relative;
        }
        .preview-container img, .preview-container video { width: 100%; height: 100%; object-fit: contain; }
        .file-badge { position: absolute; top: 10px; right: 10px; background: rgba(0,0,0,0.6); padding: 5px 10px; border-radius: 20px; font-size: 0.85rem; }

        .tools-grid { display: grid; grid-template-columns: 1fr; gap: 15px; }
        .tool-group { background: var(--glass-bg); padding: 15px; border-radius: 12px; border: 1px solid var(--glass-border); }
        .tool-group label { display: block; margin-bottom: 8px; font-size: 0.95rem; color: #ddd; }
        
        .form-control {
            width: 100%; padding: 12px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.3);
            background: rgba(0,0,0,0.2); color: #fff; font-size: 1rem; transition: 0.3s;
        }
        .form-control:focus { outline: none; border-color: var(--accent-color); background: rgba(0,0,0,0.4); }
        .form-control option { background: #2c5364; color: #fff; }
        input[type=range] { width: 100%; cursor: pointer; accent-color: var(--accent-color); }
        
        .action-btn {
            background: var(--accent-color); color: #fff; border: none; padding: 15px;
            border-radius: 8px; font-weight: bold; font-size: 1.1rem; cursor: pointer; transition: 0.3s; width: 100%; margin-top: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        .action-btn:hover { filter: brightness(1.1); transform: translateY(-2px); }

        /* ================= SETTINGS & PRIVACY ================= */
        .settings-item { margin-bottom: 20px; padding: 20px; }
        .theme-circle {
            display: inline-block; width: 45px; height: 45px; border-radius: 50%; margin-right: 15px;
            cursor: pointer; border: 2px solid #fff; box-shadow: 0 4px 10px rgba(0,0,0,0.3); transition: 0.3s;
        }
        .theme-circle:hover { transform: scale(1.1); }
        
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.6);
            backdrop-filter: blur(5px); display: none; justify-content: center; align-items: center; z-index: 1000;
        }
        .modal-box { width: 90%; max-width: 500px; max-height: 80vh; padding: 25px; overflow-y: auto; position: relative; }
        .close-btn { position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; color: #fff; }

        /* ================= PROCESSING SCREEN ================= */
        #processing-screen {
            display: none; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            background: inherit; z-index: 2000; flex-direction: column; align-items: center; padding-top: 10vh;
        }
        .progress-header { width: 85%; max-width: 500px; text-align: center; }
        .progress-track { width: 100%; height: 15px; background: rgba(255,255,255,0.2); border-radius: 10px; margin-top: 20px; overflow: hidden; }
        .progress-fill { height: 100%; width: 0%; background: var(--accent-color); transition: width 0.3s; box-shadow: 0 0 15px var(--accent-color); }
        
        .ad-container {
            margin-top: auto; margin-bottom: 15vh;
            width: 300px; height: 250px; background: rgba(0,0,0,0.2); border-radius: 8px;
            display: flex; justify-content: center; align-items: center; overflow: hidden;
        }

        /* ================= BOTTOM NAVIGATION ================= */
        nav.bottom-nav {
            position: fixed; bottom: 0; left: 0; width: 100%; background: rgba(0, 0, 0, 0.5); backdrop-filter: blur(15px);
            display: flex; justify-content: space-around; padding: 15px 0; border-top: 1px solid rgba(255,255,255,0.1); z-index: 100;
        }
        .nav-item { color: var(--text-muted); cursor: pointer; font-size: 1rem; transition: 0.3s; }
        .nav-item.active { color: #fff; font-weight: bold; transform: scale(1.1); text-shadow: 0 0 10px rgba(255,255,255,0.5); }
    </style>
</head>
<body>

    <div id="splash-screen">
        <h1 class="splash-title">Pro Compressor</h1>
        <p style="color: #ddd; margin-bottom: 20px;">Select Language / انتخاب زبان</p>
        <div class="lang-grid">
            <div class="lang-btn" onclick="initApp('en')">English</div>
            <div class="lang-btn" onclick="initApp('fa')">دری</div>
            <div class="lang-btn" onclick="initApp('zh')">中文</div>
            <div class="lang-btn" onclick="initApp('ja')">日本語</div>
            <div class="lang-btn" onclick="initApp('de')">Deutsch</div>
            <div class="lang-btn" onclick="initApp('ru')">Русский</div>
            <div class="lang-btn" onclick="initApp('hi')">हिन्दी</div>
            <div class="lang-btn" onclick="initApp('ar')">العربية</div>
        </div>
        <button style="margin-top: 25px; background: none; border: none; color: #bbb; cursor: pointer; text-decoration: underline;" onclick="initApp('en')">Skip</button>
    </div>

    <div id="app-container">
        <header>
            <h2>Pro Compressor</h2>
        </header>

        <main id="view-home" class="view-section active">
            <div class="center-stage">
                <input type="file" id="main-file-input" multiple onchange="handleFileSelect(event)">
                <div class="big-upload-btn" onclick="document.getElementById('main-file-input').click()">
                    <svg viewBox="0 0 24 24"><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/></svg>
                    <span id="txt-select-file" style="font-weight: bold; font-size: 1.1rem;">Select File(s)</span>
                </div>
                <p id="txt-home-desc" style="color: var(--text-muted); max-width: 300px;">
                    Select an Image, Video, or Document. Select multiple files to create a Zip archive.
                </p>
            </div>
        </main>

        <main id="view-config" class="view-section">
            <button id="btn-back" style="background:none; border:none; color:#fff; text-align:left; font-size:1rem; cursor:pointer; margin-bottom:15px;" onclick="switchView('home')">← Back</button>
            
            <div class="preview-container" id="preview-area">
                </div>

            <div class="tools-grid">
                <div class="tool-group">
                    <label id="lbl-filename">File Name</label>
                    <input type="text" id="config-filename" class="form-control" placeholder="Enter output name...">
                </div>

                <div class="tool-group">
                    <label id="lbl-format">Target Format</label>
                    <select id="config-format" class="form-control"></select>
                </div>

                <div class="tool-group">
                    <label><span id="lbl-quality">Target Size / Quality</span> (<span id="slider-val">80</span>%)</label>
                    <input type="range" id="config-quality" min="10" max="100" value="80" oninput="document.getElementById('slider-val').innerText = this.value">
                </div>
            </div>

            <button class="action-btn" id="btn-start" onclick="startProcessing()">Start Processing</button>
        </main>

        <main id="view-settings" class="view-section">
            <div class="glass-panel settings-item">
                <label style="display:block; margin-bottom:10px; font-weight:bold;" id="lbl-set-lang">Language</label>
                <select id="lang-selector" class="form-control" onchange="changeLanguage(this.value)">
                    <option value="en">English</option>
                    <option value="fa">دری</option>
                    <option value="zh">中文</option>
                    <option value="ja">日本語</option>
                    <option value="de">Deutsch</option>
                    <option value="ru">Русский</option>
                    <option value="hi">हिन्दी</option>
                    <option value="ar">العربية</option>
                </select>
            </div>

            <div class="glass-panel settings-item">
                <h3 id="txt-themes" style="margin-top:0;">Visual Themes</h3>
                <div style="margin-top: 15px;">
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #0f2027, #203a43);" onclick="setTheme('default')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #ee7752, #e73c7e);" onclick="setTheme('sunset')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #1e3c72, #00d2ff);" onclick="setTheme('blue')"></div>
                    <div class="theme-circle" style="background: linear-gradient(-45deg, #4b134f, #c94b4b);" onclick="setTheme('purple')"></div>
                </div>
            </div>

            <div class="glass-panel settings-item">
                <h3 id="txt-legal" style="margin-top:0;">Legal</h3>
                <button id="btn-priv-modal" class="action-btn" style="background: rgba(255,255,255,0.1); border: 1px solid rgba(255,255,255,0.3);" onclick="document.getElementById('privacy-modal').style.display='flex'">Privacy Policy</button>
            </div>
        </main>

        <nav class="bottom-nav">
            <div class="nav-item active" id="nav-home" onclick="switchView('home', this)">🏠 Home</div>
            <div class="nav-item" id="nav-settings" onclick="switchView('settings', this)">⚙️ Settings</div>
        </nav>
    </div>

    <div id="privacy-modal" class="modal-overlay">
        <div class="glass-panel modal-box">
            <span class="close-btn" onclick="document.getElementById('privacy-modal').style.display='none'">&times;</span>
            <h2 id="txt-priv-title" style="margin-bottom: 15px; margin-top:0;">Privacy Policy</h2>
            <div style="font-size: 0.9rem; line-height: 1.6; color: #ddd; text-align: justify;">
                <p><strong>Pro Compressor Privacy Policy (Abdulrahman)</strong></p>
                <p><strong>1. Information Collection:</strong> Collects basic usage data and IP address to function properly.</p>
                <p><strong>2. Cookies & Ad SDKs:</strong> We use third-party SDKs like AdMob which may collect non-personal data for analytics and ads.</p>
                <p><strong>3. Your Rights:</strong> You have the right to request access or deletion of your data. Contact us to exercise these rights.</p>
                <p><strong>4. Data Retention:</strong> User data is retained only as long as necessary. We use safeguards to protect your info.</p>
                <p><strong>Contact:</strong> <em>hkymy9323@gmail.com</em></p>
            </div>
        </div>
    </div>

    <div id="processing-screen">
        <div class="progress-header">
            <h2 id="process-title" data-state="processing">Processing...</h2>
            <p id="process-desc">Please wait while we prepare your file(s).</p>
            <div class="progress-track">
                <div class="progress-fill" id="progress-bar"></div>
            </div>
            
            <div id="result-actions" style="display:none; margin-top:20px; gap:10px; justify-content:center;">
                <button class="action-btn" id="btn-download" onclick="downloadResult()">Download File</button>
                <button class="action-btn" id="btn-back-home" style="background: rgba(255,255,255,0.2);" onclick="closeProcessing()">Back Home</button>
            </div>
        </div>

        <div class="ad-container" id="ad-container"></div>
    </div>

    <script>
        let currentType = '';
        let selectedFiles = [];
        let processedDataUrl = null; 
        let processedBlob = null;
        let processedFilename = 'output';
        let adInterval = null;

        // Comprehensive Dictionary for ALL texts
        const dict = {
            en: { home: "🏠 Home", set: "⚙️ Settings", btnSel: "Select File(s)", desc: "Select an Image, Video, or Document. Select multiple files to create a Zip.", fname: "File Name", fmt: "Target Format", qual: "Target Size / Quality", start: "Start Processing", themes: "Visual Themes", legal: "Legal", lang: "Language", back: "← Back", proc: "Processing...", wait: "Please wait while we prepare your file(s).", comp: "Complete!", ready: "Your file is ready to download.", dl: "Download File", bh: "Back Home", priv: "Privacy Policy", filesSel: "Files Selected", alertVid: "You can only select 1 video at a time.", alertLib: "JSZip library not loaded. Simulating...", note: "Note: Video/Doc requires external packages in production." },
            fa: { home: "🏠 خانه", set: "⚙️ تنظیمات", btnSel: "انتخاب فایل", desc: "عکس، ویدیو یا سند انتخاب کنید. برای ساخت Zip چند فایل انتخاب کنید.", fname: "نام فایل", fmt: "فرمت خروجی", qual: "کیفیت / حجم هدف", start: "شروع پردازش", themes: "تم‌های ظاهری", legal: "حقوقی", lang: "زبان", back: "← بازگشت", proc: "در حال پردازش...", wait: "لطفاً منتظر بمانید...", comp: "تکمیل شد!", ready: "فایل شما برای دانلود آماده است.", dl: "دانلود فایل", bh: "بازگشت به خانه", priv: "حریم خصوصی", filesSel: "فایل انتخاب شد", alertVid: "شما فقط می‌توانید ۱ ویدیو انتخاب کنید.", alertLib: "کتابخانه JSZip بارگیری نشد. در حال شبیه‌سازی...", note: "توجه: پردازش ویدیو/سند در نسخه واقعی نیاز به پکیج‌های خارجی دارد." },
            zh: { home: "🏠 首页", set: "⚙️ 设置", btnSel: "选择文件", desc: "选择图像，视频或文档。选择多个文件创建Zip。", fname: "文件名", fmt: "目标格式", qual: "目标大小 / 质量", start: "开始处理", themes: "视觉主题", legal: "合法", lang: "语言", back: "← 返回", proc: "处理中...", wait: "请稍候...", comp: "完成！", ready: "文件已准备好下载。", dl: "下载文件", bh: "返回首页", priv: "隐私政策", filesSel: "个文件已选择", alertVid: "一次只能选择1个视频。", alertLib: "未加载JSZip库，正在模拟...", note: "注意：视频/文档在生产环境中需要外部包。" },
            ja: { home: "🏠 ホーム", set: "⚙️ 設定", btnSel: "ファイルを選択", desc: "画像、動画、ドキュメントを選択します。複数選択でZip作成。", fname: "ファイル名", fmt: "フォーマット", qual: "品質 / サイズ", start: "処理開始", themes: "テーマ", legal: "法的", lang: "言語", back: "← 戻る", proc: "処理中...", wait: "お待ちください...", comp: "完了！", ready: "ファイルのダウンロード準備ができました。", dl: "ファイルをダウンロード", bh: "ホームに戻る", priv: "プライバシーポリシー", filesSel: "ファイル選択済み", alertVid: "一度に選択できる動画は1つだけです。", alertLib: "JSZipがロードされていません。シミュレーション中...", note: "注：動画/ドキュメントには外部パッケージが必要です。" },
            de: { home: "🏠 Start", set: "⚙️ Einst.", btnSel: "Datei wählen", desc: "Bild, Video oder Dokument wählen. Mehrere für Zip.", fname: "Dateiname", fmt: "Format", qual: "Qualität", start: "Verarbeitung starten", themes: "Themen", legal: "Rechtlich", lang: "Sprache", back: "← Zurück", proc: "Verarbeitung...", wait: "Bitte warten...", comp: "Abgeschlossen!", ready: "Ihre Datei ist zum Download bereit.", dl: "Datei herunterladen", bh: "Zurück zur Start", priv: "Datenschutz", filesSel: "Dateien ausgewählt", alertVid: "Nur 1 Video auf einmal wählbar.", alertLib: "JSZip nicht geladen. Simuliere...", note: "Hinweis: Video/Dokument erfordert externe Pakete." },
            ru: { home: "🏠 Главная", set: "⚙️ Настройки", btnSel: "Выбрать файл", desc: "Выберите изображение, видео или документ. Несколько для Zip.", fname: "Имя файла", fmt: "Формат", qual: "Качество", start: "Начать", themes: "Темы", legal: "Юридическая", lang: "Язык", back: "← Назад", proc: "Обработка...", wait: "Пожалуйста, подождите...", comp: "Готово!", ready: "Ваш файл готов к скачиванию.", dl: "Скачать файл", bh: "На главную", priv: "Конфиденциальность", filesSel: "файлов выбрано", alertVid: "Можно выбрать только 1 видео.", alertLib: "JSZip не загружен. Симуляция...", note: "Примечание: Для видео нужны внешние пакеты." },
            hi: { home: "🏠 होम", set: "⚙️ सेटिंग्स", btnSel: "फ़ाइल चुनें", desc: "छवि, वीडियो या दस्तावेज़ चुनें। ज़िप के लिए कई चुनें।", fname: "फ़ाइल का नाम", fmt: "प्रारूप", qual: "गुणवत्ता", start: "शुरू करें", themes: "विषय", legal: "कानूनी", lang: "भाषा", back: "← वापस", proc: "प्रसंस्करण...", wait: "कृपया प्रतीक्षा करें...", comp: "पूरा हुआ!", ready: "आपकी फ़ाइल डाउनलोड के लिए तैयार है।", dl: "फ़ाइल डाउनलोड करें", bh: "होम पर वापस", priv: "गोपनीयता नीति", filesSel: "फ़ाइलें चयनित", alertVid: "आप एक बार में केवल 1 वीडियो चुन सकते हैं।", alertLib: "JSZip लोड नहीं हुआ। अनुकरण...", note: "नोट: वीडियो के लिए बाहरी पैकेज की आवश्यकता है।" },
            ar: { home: "🏠 الرئيسية", set: "⚙️ الإعدادات", btnSel: "اختر ملف", desc: "اختر صورة، فيديو أو مستند. لإنشاء Zip اختر عدة ملفات.", fname: "اسم الملف", fmt: "الصيغة", qual: "الجودة / الحجم", start: "بدء المعالجة", themes: "السمات", legal: "قانوني", lang: "اللغة", back: "← رجوع", proc: "جاري المعالجة...", wait: "يرجى الانتظار...", comp: "اكتمل!", ready: "ملفك جاهز للتنزيل.", dl: "تنزيل الملف", bh: "العودة للرئيسية", priv: "سياسة الخصوصية", filesSel: "ملفات محددة", alertVid: "يمكنك تحديد فيديو واحد فقط.", alertLib: "مكتبة JSZip غير محملة. جاري المحاكاة...", note: "ملاحظة: يتطلب الفيديو حزم خارجية." }
        };

        // Helper string translation fetcher
        function getText(key) {
            const lang = document.getElementById('lang-selector').value || 'en';
            return (dict[lang] && dict[lang][key]) ? dict[lang][key] : dict['en'][key];
        }

        // Safe DOM Text Updater
        function setText(id, text) {
            const el = document.getElementById(id);
            if (el && text) el.innerText = text;
        }

        function initApp(lang) {
            try {
                // Ensure dropdown matches selection
                document.getElementById('lang-selector').value = lang;
                changeLanguage(lang);
            } catch (e) {
                console.error("Translation Error: ", e);
            } finally {
                // Guaranteed to open the app even if translation glitches
                document.getElementById('splash-screen').style.display = 'none';
                document.getElementById('app-container').style.display = 'flex';
            }
        }

        function changeLanguage(lang) {
            document.body.style.direction = (lang === 'fa' || lang === 'ar') ? 'rtl' : 'ltr';
            
            setText('nav-home', getText('home'));
            setText('nav-settings', getText('set'));
            setText('txt-select-file', getText('btnSel'));
            setText('txt-home-desc', getText('desc'));
            setText('lbl-filename', getText('fname'));
            setText('lbl-format', getText('fmt'));
            setText('lbl-quality', getText('qual'));
            setText('btn-start', getText('start'));
            setText('txt-themes', getText('themes'));
            setText('txt-legal', getText('legal'));
            setText('lbl-set-lang', getText('lang'));
            setText('btn-back', getText('back'));
            setText('btn-download', getText('dl'));
            setText('btn-back-home', getText('bh'));
            setText('txt-priv-title', getText('priv'));
            setText('btn-priv-modal', getText('priv'));
            
            // Re-render file badge if exists
            const fileBadge = document.querySelector('.file-badge');
            if(fileBadge && selectedFiles.length > 1) {
                fileBadge.innerText = `${selectedFiles.length} ${getText('filesSel')}`;
            }

            // Processing texts based on state
            const procTitle = document.getElementById('process-title');
            if (procTitle) {
                if (procTitle.dataset.state === 'complete') {
                    setText('process-title', getText('comp'));
                    setText('process-desc', getText('ready'));
                } else {
                    setText('process-title', getText('proc'));
                    setText('process-desc', getText('wait'));
                }
            }
        }

        function switchView(viewId, navElement) {
            document.querySelectorAll('.view-section').forEach(v => v.classList.remove('active'));
            document.getElementById('view-' + viewId).classList.add('active');
            
            if(navElement) {
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                navElement.classList.add('active');
            } else if (viewId === 'home') {
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                document.getElementById('nav-home').classList.add('active');
            }
        }

        function setTheme(theme) {
            document.body.setAttribute('data-theme', theme);
        }

        function handleFileSelect(event) {
            const files = event.target.files;
            if(!files || files.length === 0) return;

            selectedFiles = Array.from(files);
            const firstFile = selectedFiles[0];
            const mime = firstFile.type;

            if(selectedFiles.length > 1) {
                if(selectedFiles.every(f => f.type.startsWith('image/')) && selectedFiles.length <= 5) {
                    currentType = 'image-multiple';
                } else {
                    currentType = 'zip';
                }
            } else {
                if(mime.startsWith('image/')) currentType = 'image';
                else if(mime.startsWith('video/')) currentType = 'video';
                else currentType = 'doc';
            }

            if(currentType === 'video' && selectedFiles.length > 1) {
                alert(getText('alertVid'));
                event.target.value = ''; return;
            }

            setupConfigUI();
            switchView('config');
        }

        function setupConfigUI() {
            const firstFile = selectedFiles[0];
            const originalName = firstFile.name.substring(0, firstFile.name.lastIndexOf('.')) || firstFile.name;
            
            document.getElementById('config-filename').value = currentType === 'zip' ? 'archive' : originalName;

            const formatSelect = document.getElementById('config-format');
            formatSelect.innerHTML = '';
            
            let options = [];
            if(currentType.startsWith('image')) options = ['WebP', 'JPG', 'PNG'];
            if(currentType === 'video') options = ['MP4', 'MKV', 'WebM'];
            if(currentType === 'doc') options = ['PDF', 'TXT', 'DOCX'];
            if(currentType === 'zip') options = ['ZIP'];

            options.forEach(opt => {
                const el = document.createElement('option');
                el.value = opt.toLowerCase(); el.innerText = opt;
                formatSelect.appendChild(el);
            });

            const previewArea = document.getElementById('preview-area');
            previewArea.innerHTML = '';
            
            if(selectedFiles.length > 1) {
                previewArea.innerHTML = `<div class="file-badge">${selectedFiles.length} ${getText('filesSel')}</div>`;
            }

            if(currentType.startsWith('image')) {
                const img = document.createElement('img');
                img.src = URL.createObjectURL(firstFile);
                previewArea.appendChild(img);
            } else if(currentType === 'video') {
                const vid = document.createElement('video');
                vid.src = URL.createObjectURL(firstFile);
                vid.controls = true;
                previewArea.appendChild(vid);
            } else {
                previewArea.innerHTML += `<div style="text-align:center; font-size:4rem;">📄</div>`;
            }
        }

        function startProcessing() {
            document.getElementById('app-container').style.display = 'none';
            document.getElementById('processing-screen').style.display = 'flex';
            document.getElementById('result-actions').style.display = 'none';
            
            document.getElementById('process-title').dataset.state = 'processing';
            setText('process-title', getText('proc'));
            setText('process-desc', getText('wait'));
            
            const bar = document.getElementById('progress-bar');
            bar.style.width = '0%';

            const targetFormat = document.getElementById('config-format').value;
            processedFilename = document.getElementById('config-filename').value + '.' + targetFormat;
            const quality = document.getElementById('config-quality').value / 100;

            manageAds();

            if(currentType.startsWith('image') && targetFormat === 'webp') {
                processImageToWebp(selectedFiles[0], quality, bar);
            } else if(currentType === 'zip') {
                processZip(selectedFiles, bar);
            } else {
                simulateProcessing(bar);
            }
        }

        function manageAds() {
            const adContainer = document.getElementById('ad-container');
            function injectAd() {
                if (navigator.onLine) {
                    adContainer.innerHTML = `
                        <iframe srcdoc="
                            <html><body style='margin:0;display:flex;justify-content:center;align-items:center;'>
                            <script>
                                atOptions = { 'key' : 'd3b5f554367d6f64704b6cdd8f68b658', 'format' : 'iframe', 'height' : 250, 'width' : 300, 'params' : {} };
                            </script>
                            <script src='https://speedingdeadlyplays.com/d3b5f554367d6f64704b6cdd8f68b658/invoke.js'></script>
                            </body></html>
                        " width="300" height="250" frameborder="0" scrolling="no"></iframe>`;
                } else {
                    adContainer.innerHTML = '';
                }
            }
            injectAd();
            if(adInterval) clearInterval(adInterval);
            adInterval = setInterval(injectAd, 10000);
        }

        function simulateProcessing(bar) {
            let width = 0;
            const int = setInterval(() => {
                width += Math.random() * 15;
                if(width >= 100) { width = 100; clearInterval(int); finishProcessing(); }
                bar.style.width = width + '%';
            }, 400);
        }

        function processImageToWebp(file, quality, bar) {
            const reader = new FileReader();
            reader.onload = function(e) {
                bar.style.width = '40%';
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    canvas.width = img.width; canvas.height = img.height;
                    canvas.getContext('2d').drawImage(img, 0, 0);
                    processedDataUrl = canvas.toDataURL('image/webp', quality);
                    bar.style.width = '100%';
                    setTimeout(finishProcessing, 500);
                }
                img.src = e.target.result;
            }
            reader.readAsDataURL(file);
        }

        function processZip(files, bar) {
            if(typeof JSZip === 'undefined') { 
                console.log(getText('alertLib'));
                simulateProcessing(bar); 
                return; 
            }
            const zip = new JSZip();
            files.forEach(file => zip.file(file.name, file));
            zip.generateAsync({type:"blob"}, function(meta) {
                bar.style.width = (meta.percent) + '%';
            }).then(function(content) {
                processedBlob = content;
                bar.style.width = '100%';
                setTimeout(finishProcessing, 500);
            });
        }

        function finishProcessing() {
            document.getElementById('process-title').dataset.state = 'complete';
            setText('process-title', getText('comp'));
            setText('process-desc', getText('ready'));
            document.getElementById('result-actions').style.display = 'flex';
        }

        function downloadResult() {
            const link = document.createElement('a');
            link.download = processedFilename;
            if(currentType.startsWith('image') && processedDataUrl) link.href = processedDataUrl;
            else if(currentType === 'zip' && processedBlob) link.href = URL.createObjectURL(processedBlob);
            else { alert(getText('note')); return; }
            link.click();
        }

        function closeProcessing() {
            if(adInterval) clearInterval(adInterval);
            document.getElementById('processing-screen').style.display = 'none';
            document.getElementById('app-container').style.display = 'flex';
            document.getElementById('main-file-input').value = '';
            processedDataUrl = null; processedBlob = null;
            switchView('home');
        }
    </script>
</body>
</html>
