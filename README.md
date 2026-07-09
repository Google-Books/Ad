<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neon Compressor / Multi-Converter</title>
    <style>
        /* ================= VARIABLES & THEMES ================= */
        :root {
            --bg-color: #0d1117;
            --surface-color: #161b22;
            --text-color: #c9d1d9;
            --text-muted: #8b949e;
            --primary-color: #58a6ff;
            --neon-glow: 0 0 10px rgba(88, 166, 255, 0.5), 0 0 20px rgba(88, 166, 255, 0.3);
            --border-radius: 12px;
        }

        [data-theme="blue"] {
            --primary-color: #00ffff;
            --neon-glow: 0 0 10px #00ffff, 0 0 20px rgba(0, 255, 255, 0.5);
        }

        [data-theme="green"] {
            --primary-color: #00ff00;
            --neon-glow: 0 0 10px #00ff00, 0 0 20px rgba(0, 255, 0, 0.5);
        }

        [data-theme="purple"] {
            --primary-color: #ff00ff;
            --neon-glow: 0 0 10px #ff00ff, 0 0 20px rgba(255, 0, 255, 0.5);
        }

        /* ================= GLOBAL STYLES ================= */
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-color); overflow-x: hidden; transition: all 0.3s ease; }
        a { color: var(--primary-color); text-decoration: none; }
        
        /* ================= SPLASH SCREEN ================= */
        #splash-screen {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            background-color: rgba(13, 17, 23, 0.95);
            z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center;
            backdrop-filter: blur(10px);
        }
        .splash-header { margin-bottom: 30px; text-align: center; }
        .splash-header h1 { color: var(--primary-color); text-shadow: var(--neon-glow); font-size: 2rem; margin-bottom: 10px; }
        .lang-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; width: 90%; max-width: 400px; }
        .lang-btn {
            background: var(--surface-color); color: var(--text-color); border: 1px solid var(--primary-color);
            padding: 15px; border-radius: var(--border-radius); cursor: pointer; text-align: center;
            font-size: 1rem; transition: 0.3s; box-shadow: var(--neon-glow);
        }
        .lang-btn:hover { background: var(--primary-color); color: #000; }
        .skip-btn { margin-top: 30px; background: transparent; color: var(--text-muted); border: none; cursor: pointer; font-size: 1rem; text-decoration: underline; }

        /* ================= MAIN APP LAYOUT ================= */
        #app-container { display: none; min-height: 100vh; padding-bottom: 70px; }
        header { padding: 20px; text-align: center; border-bottom: 1px solid var(--surface-color); }
        header h1 { color: var(--primary-color); text-shadow: var(--neon-glow); font-size: 1.8rem; }
        
        .tab-content { display: none; padding: 20px; max-width: 800px; margin: 0 auto; animation: fadeIn 0.4s; }
        .tab-content.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* ================= CARDS & NEON UI ================= */
        .grid-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
        .neon-card {
            background: var(--surface-color); border: 1px solid var(--primary-color); border-radius: var(--border-radius);
            padding: 20px; box-shadow: var(--neon-glow); text-align: center; transition: 0.3s; position: relative; overflow: hidden;
        }
        .neon-card:hover { transform: translateY(-5px); box-shadow: 0 0 20px var(--primary-color); }
        .neon-card h3 { color: var(--primary-color); margin-bottom: 10px; font-size: 1.4rem; }
        .neon-card p { color: var(--text-muted); font-size: 0.9rem; margin-bottom: 15px; }
        
        .action-btn {
            background: var(--primary-color); color: var(--bg-color); border: none; padding: 10px 20px;
            border-radius: 8px; font-weight: bold; cursor: pointer; transition: 0.3s; width: 100%; margin-top: 10px;
        }
        .action-btn:hover { opacity: 0.8; box-shadow: var(--neon-glow); }
        
        /* Progress Bar */
        .progress-container { width: 100%; background: #333; border-radius: 10px; margin-top: 15px; display: none; }
        .progress-bar { height: 10px; background: var(--primary-color); border-radius: 10px; width: 0%; box-shadow: var(--neon-glow); transition: width 0.4s; }

        /* Settings UI */
        .settings-group { margin-bottom: 25px; background: var(--surface-color); padding: 15px; border-radius: var(--border-radius); }
        .settings-group h3 { margin-bottom: 15px; color: var(--primary-color); }
        .theme-btn { display: inline-block; width: 40px; height: 40px; border-radius: 50%; margin-right: 10px; cursor: pointer; border: 2px solid transparent; }
        .theme-btn[data-color="github"] { background: #58a6ff; }
        .theme-btn[data-color="blue"] { background: #00ffff; }
        .theme-btn[data-color="green"] { background: #00ff00; }
        .theme-btn[data-color="purple"] { background: #ff00ff; }

        /* Bottom Navigation */
        nav.bottom-nav {
            position: fixed; bottom: 0; left: 0; width: 100%; background: var(--surface-color);
            display: flex; justify-content: space-around; padding: 15px 0; border-top: 1px solid #333; z-index: 100;
        }
        .nav-item { color: var(--text-muted); text-align: center; cursor: pointer; font-size: 0.9rem; flex: 1; transition: 0.3s; }
        .nav-item.active { color: var(--primary-color); text-shadow: var(--neon-glow); font-weight: bold; }
        
        /* Real Image Converter Styles */
        input[type="file"] { display: none; }
        #download-link { display: none; text-align: center; margin-top: 10px; color: var(--primary-color); font-weight: bold; }

    </style>
</head>
<body>

    <div id="splash-screen">
        <div class="splash-header">
            <h1>Neon Converter</h1>
            <p>Select your language</p>
        </div>
        <div class="lang-grid">
            <div class="lang-btn" onclick="initApp('en')">🇬🇧 English</div>
            <div class="lang-btn" onclick="initApp('fa')">🇦🇫 دری (Dari)</div>
            <div class="lang-btn" onclick="initApp('zh')">🇨🇳 简体中文</div>
            <div class="lang-btn" onclick="initApp('ja')">🇯🇵 日本語</div>
            <div class="lang-btn" onclick="initApp('de')">🇩🇪 Deutsch</div>
            <div class="lang-btn" onclick="initApp('ru')">🇷🇺 Русский</div>
            <div class="lang-btn" onclick="initApp('hi')">🇮🇳 हिन्दी</div>
            <div class="lang-btn" onclick="initApp('ar')">🇸🇦 العربية</div>
        </div>
        <button class="skip-btn" onclick="initApp('en')">Skip (Default English)</button>
    </div>

    <div id="app-container">
        <header>
            <h1 id="header-title">Neon Converter</h1>
        </header>

        <main id="tab-home" class="tab-content active">
            <div class="grid-container">
                <div class="neon-card">
                    <h3 id="txt-video-title">Video Tools</h3>
                    <p id="txt-video-desc">Compress & Convert MP4, MKV, WebM offline.</p>
                    <button class="action-btn" onclick="simulateProgress('video-progress')" id="txt-video-btn">Select Video</button>
                    <div class="progress-container" id="video-progress"><div class="progress-bar"></div></div>
                </div>

                <div class="neon-card">
                    <h3 id="txt-img-title">Image Tools</h3>
                    <p id="txt-img-desc">Compress & Convert JPG/PNG to WebP (-90% Size).</p>
                    <input type="file" id="image-upload" accept="image/png, image/jpeg, image/jpg">
                    <button class="action-btn" onclick="document.getElementById('image-upload').click()" id="txt-img-btn">Select Image</button>
                    <div class="progress-container" id="img-progress"><div class="progress-bar"></div></div>
                    <a id="download-link" download="compressed_image.webp">⬇️ Download WebP</a>
                    <canvas id="canvas" style="display:none;"></canvas>
                </div>

                <div class="neon-card">
                    <h3 id="txt-doc-title">Document Tools</h3>
                    <p id="txt-doc-desc">Convert TXT, Word and PDFs on your device.</p>
                    <button class="action-btn" onclick="simulateProgress('doc-progress')" id="txt-doc-btn">Select Document</button>
                    <div class="progress-container" id="doc-progress"><div class="progress-bar"></div></div>
                </div>

                <div class="neon-card" style="border-style: dashed;">
                    <h3 id="txt-status-title">System Status</h3>
                    <p id="txt-status-desc">All conversions are 100% Free & Offline.</p>
                    <p style="color: var(--primary-color); font-weight: bold;">CPU Ready | RAM Ready</p>
                </div>
            </div>
        </main>

        <main id="tab-settings" class="tab-content">
            <div class="settings-group">
                <h3 id="txt-set-lang">Change Language</h3>
                <select class="action-btn" id="lang-selector" onchange="changeLanguage(this.value)" style="background: var(--surface-color); color: var(--text-color); border: 1px solid var(--primary-color);">
                    <option value="en">English</option>
                    <option value="fa">دری (Dari)</option>
                    <option value="zh">简体中文 (Chinese)</option>
                    <option value="ja">日本語 (Japanese)</option>
                    <option value="de">Deutsch (German)</option>
                    <option value="ru">Русский (Russian)</option>
                    <option value="hi">हिन्दी (Hindi)</option>
                    <option value="ar">العربية (Arabic)</option>
                </select>
            </div>

            <div class="settings-group">
                <h3 id="txt-set-theme">Neon Themes</h3>
                <div>
                    <div class="theme-btn" data-color="github" onclick="setTheme('github')"></div>
                    <div class="theme-btn" data-color="blue" onclick="setTheme('blue')"></div>
                    <div class="theme-btn" data-color="green" onclick="setTheme('green')"></div>
                    <div class="theme-btn" data-color="purple" onclick="setTheme('purple')"></div>
                </div>
            </div>

            <div class="settings-group">
                <h3 id="txt-set-dev">Developer</h3>
                <p>GitHub: <a href="#">@Abdulrahman</a></p>
                <p>Support: <a href="mailto:hkymy9323@gmail.com">hkymy9323@gmail.com</a></p>
            </div>
        </main>

        <main id="tab-privacy" class="tab-content">
            <div class="settings-group">
                <h3 id="txt-priv-title">Privacy Policy</h3>
                <p style="line-height: 1.6; color: var(--text-muted);" id="txt-priv-text">
                    Welcome to Neon Compressor / Multi-Converter. Your privacy is critically important to us.<br><br>
                    <strong>1. Offline Processing:</strong> All file compressions and conversions (Video, Image, Document) are processed locally on your device's CPU/RAM. We do not upload your personal files to any server.<br><br>
                    <strong>2. Advertising (AdMob):</strong> To keep this application 100% free, we use third-party advertising SDKs like Google AdMob. These services may collect non-personal data (such as device ID and IP address) to serve relevant ads.<br><br>
                    <strong>3. Contact:</strong> Developer: Abdulrahman. Email: hkymy9323@gmail.com.
                </p>
            </div>
        </main>

        <nav class="bottom-nav">
            <div class="nav-item active" onclick="switchTab('home', this)" id="nav-home">🏠 Home</div>
            <div class="nav-item" onclick="switchTab('settings', this)" id="nav-settings">⚙️ Settings</div>
            <div class="nav-item" onclick="switchTab('privacy', this)" id="nav-privacy">🛡️ Privacy</div>
        </nav>
    </div>

    <script>
        // Translations Dictionary
        const translations = {
            en: {
                navHome: "🏠 Home", navSet: "⚙️ Settings", navPriv: "🛡️ Privacy",
                vTitle: "Video Tools", vDesc: "Compress & Convert MP4, MKV, WebM offline.", vBtn: "Select Video",
                iTitle: "Image Tools", iDesc: "Compress & Convert JPG/PNG to WebP (-90% Size).", iBtn: "Select Image",
                dTitle: "Document Tools", dDesc: "Convert TXT, Word and PDFs on your device.", dBtn: "Select Document",
                sTitle: "System Status", sDesc: "All conversions are 100% Free & Offline.",
                setLang: "Change Language", setTheme: "Neon Themes", setDev: "Developer",
                pTitle: "Privacy Policy",
                pText: "Welcome to Neon Compressor. Your privacy is important.<br><br><strong>1. Offline Processing:</strong> All files are processed locally on your device. We do not upload files to servers.<br><br><strong>2. Ads (AdMob):</strong> To keep the app free, we use Google AdMob which may collect non-personal data.<br><br><strong>3. Contact:</strong> Abdulrahman (hkymy9323@gmail.com)."
            },
            fa: { /* Dari / Persian */
                navHome: "🏠 خانه", navSet: "⚙️ تنظیمات", navPriv: "🛡️ حریم خصوصی",
                vTitle: "ابزار ویدیو", vDesc: "فشرده‌سازی و تبدیل آفلاین ویدیوها.", vBtn: "انتخاب ویدیو",
                iTitle: "ابزار عکس", iDesc: "تبدیل و کاهش ۹۰ درصدی حجم عکس به WebP.", iBtn: "انتخاب عکس",
                dTitle: "ابزار اسناد", dDesc: "تبدیل فایل‌های متنی در داخل گوشی.", dBtn: "انتخاب سند",
                sTitle: "وضعیت سیستم", sDesc: "تمامی پردازش‌ها ۱۰۰٪ رایگان و آفلاین است.",
                setLang: "تغییر زبان", setTheme: "تم‌های نئونی", setDev: "توسعه‌دهنده",
                pTitle: "حریم خصوصی",
                pText: "به نئون کامپرسور خوش آمدید.<br><br><strong>۱. پردازش آفلاین:</strong> تمام فایل‌ها روی گوشی شما پردازش می‌شوند و به سروری ارسال نمی‌گردند.<br><br><strong>۲. تبلیغات:</strong> برای رایگان ماندن برنامه از AdMob استفاده می‌شود.<br><br><strong>۳. ارتباط:</strong> عبدالرحمن (hkymy9323@gmail.com)."
            },
            zh: { /* Chinese */
                navHome: "🏠 首页", navSet: "⚙️ 设置", navPriv: "🛡️ 隐私",
                vTitle: "视频工具", vDesc: "离线压缩和转换视频格式。", vBtn: "选择视频",
                iTitle: "图像工具", iDesc: "将图像压缩并转换为 WebP。", iBtn: "选择图像",
                dTitle: "文档工具", dDesc: "在设备上转换文档。", dBtn: "选择文档",
                sTitle: "系统状态", sDesc: "所有转换都是 100% 免费且离线的。",
                setLang: "更改语言", setTheme: "霓虹灯主题", setDev: "开发者",
                pTitle: "隐私政策", pText: "您的隐私很重要。文件在本地处理。我们使用 AdMob 显示广告。联系方式：Abdulrahman (hkymy9323@gmail.com)."
            },
            ja: { /* Japanese */
                navHome: "🏠 ホーム", navSet: "⚙️ 設定", navPriv: "🛡️ プライバシー",
                vTitle: "ビデオツール", vDesc: "オフラインでビデオを圧縮・変換。", vBtn: "ビデオを選択",
                iTitle: "画像ツール", iDesc: "画像をWebPに圧縮・変換。", iBtn: "画像を選択",
                dTitle: "ドキュメントツール", dDesc: "デバイス上でドキュメントを変換。", dBtn: "ドキュメントを選択",
                sTitle: "システムステータス", sDesc: "すべて100%無料・オフライン。",
                setLang: "言語の変更", setTheme: "ネオンテーマ", setDev: "開発者",
                pTitle: "プライバシーポリシー", pText: "プライバシーは重要です。ファイルはローカルで処理されます。広告にはAdMobを使用しています。連絡先：Abdulrahman (hkymy9323@gmail.com)."
            },
            de: { /* German */
                navHome: "🏠 Start", navSet: "⚙️ Einst.", navPriv: "🛡️ Datenschutz",
                vTitle: "Video-Tools", vDesc: "Videos offline komprimieren & konvertieren.", vBtn: "Video auswählen",
                iTitle: "Bild-Tools", iDesc: "Bilder in WebP komprimieren (-90%).", iBtn: "Bild auswählen",
                dTitle: "Dokument-Tools", dDesc: "Dokumente auf dem Gerät konvertieren.", dBtn: "Dokument auswählen",
                sTitle: "Systemstatus", sDesc: "Alles 100% kostenlos & offline.",
                setLang: "Sprache ändern", setTheme: "Neon-Themes", setDev: "Entwickler",
                pTitle: "Datenschutzrichtlinie", pText: "Ihre Privatsphäre ist wichtig. Dateien werden lokal verarbeitet. Wir verwenden AdMob für Anzeigen. Kontakt: Abdulrahman (hkymy9323@gmail.com)."
            },
            ru: { /* Russian */
                navHome: "🏠 Главная", navSet: "⚙️ Настройки", navPriv: "🛡️ Конфиденциальность",
                vTitle: "Видео инструменты", vDesc: "Сжатие и конвертация видео офлайн.", vBtn: "Выбрать видео",
                iTitle: "Инструменты изображений", iDesc: "Сжатие изображений в WebP.", iBtn: "Выбрать изображение",
                dTitle: "Документы", dDesc: "Конвертация документов на устройстве.", dBtn: "Выбрать документ",
                sTitle: "Статус системы", sDesc: "Всё 100% бесплатно и офлайн.",
                setLang: "Изменить язык", setTheme: "Неоновые темы", setDev: "Разработчик",
                pTitle: "Политика конфиденциальности", pText: "Конфиденциальность важна. Файлы обрабатываются локально. Мы используем AdMob. Контакты: Abdulrahman (hkymy9323@gmail.com)."
            },
            hi: { /* Hindi */
                navHome: "🏠 होम", navSet: "⚙️ सेटिंग्स", navPriv: "🛡️ प्राइवेसी",
                vTitle: "वीडियो टूल्स", vDesc: "ऑफ़लाइन वीडियो कंप्रेस और कन्वर्ट करें।", vBtn: "वीडियो चुनें",
                iTitle: "इमेज टूल्स", iDesc: "इमेज को WebP में कंप्रेस करें।", iBtn: "इमेज चुनें",
                dTitle: "डॉक्यूमेंट टूल्स", dDesc: "अपने डिवाइस पर डॉक्यूमेंट कन्वर्ट करें।", dBtn: "डॉक्यूमेंट चुनें",
                sTitle: "सिस्टम स्टेटस", sDesc: "सभी 100% मुफ़्त और ऑफ़लाइन।",
                setLang: "भाषा बदलें", setTheme: "नियॉन थीम्स", setDev: "डेवलपर",
                pTitle: "गोपनीयता नीति", pText: "आपकी गोपनीयता महत्वपूर्ण है। फ़ाइलें स्थानीय रूप से संसाधित की जाती हैं। हम AdMob का उपयोग करते हैं। संपर्क: Abdulrahman (hkymy9323@gmail.com)."
            },
            ar: { /* Arabic */
                navHome: "🏠 الرئيسية", navSet: "⚙️ الإعدادات", navPriv: "🛡️ الخصوصية",
                vTitle: "أدوات الفيديو", vDesc: "ضغط وتحويل الفيديو بدون إنترنت.", vBtn: "اختر فيديو",
                iTitle: "أدوات الصور", iDesc: "ضغط الصور وتحويلها إلى WebP.", iBtn: "اختر صورة",
                dTitle: "أدوات المستندات", dDesc: "تحويل المستندات على هاتفك.", dBtn: "اختر مستند",
                sTitle: "حالة النظام", sDesc: "جميع العمليات 100% مجانية وبدون إنترنت.",
                setLang: "تغيير اللغة", setTheme: "سمات النيون", setDev: "المطور",
                pTitle: "سياسة الخصوصية", pText: "خصوصيتك مهمة. تتم معالجة الملفات محليًا. نحن نستخدم AdMob. للتواصل: Abdulrahman (hkymy9323@gmail.com)."
            }
        };

        // Initialize App (Hide Splash, Show App, Set Lang)
        function initApp(lang) {
            document.getElementById('splash-screen').style.display = 'none';
            document.getElementById('app-container').style.display = 'block';
            document.getElementById('lang-selector').value = lang;
            changeLanguage(lang);
        }

        // Tab Switching Logic
        function switchTab(tabId, element) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(nav => nav.classList.remove('active'));
            document.getElementById('tab-' + tabId).classList.add('active');
            element.classList.add('active');
        }

        // Theme Switching Logic
        function setTheme(theme) {
            if(theme === 'github') {
                document.documentElement.removeAttribute('data-theme');
            } else {
                document.documentElement.setAttribute('data-theme', theme);
            }
        }

        // Language Switching Logic
        function changeLanguage(lang) {
            const t = translations[lang];
            if(!t) return;
            
            // Handle RTL for Arabic and Dari
            if(lang === 'fa' || lang === 'ar') {
                document.body.style.direction = "rtl";
            } else {
                document.body.style.direction = "ltr";
            }

            // Update DOM Elements
            document.getElementById('nav-home').innerText = t.navHome;
            document.getElementById('nav-settings').innerText = t.navSet;
            document.getElementById('nav-privacy').innerText = t.navPriv;

            document.getElementById('txt-video-title').innerText = t.vTitle;
            document.getElementById('txt-video-desc').innerText = t.vDesc;
            document.getElementById('txt-video-btn').innerText = t.vBtn;

            document.getElementById('txt-img-title').innerText = t.iTitle;
            document.getElementById('txt-img-desc').innerText = t.iDesc;
            document.getElementById('txt-img-btn').innerText = t.iBtn;

            document.getElementById('txt-doc-title').innerText = t.dTitle;
            document.getElementById('txt-doc-desc').innerText = t.dDesc;
            document.getElementById('txt-doc-btn').innerText = t.dBtn;

            document.getElementById('txt-status-title').innerText = t.sTitle;
            document.getElementById('txt-status-desc').innerText = t.sDesc;

            document.getElementById('txt-set-lang').innerText = t.setLang;
            document.getElementById('txt-set-theme').innerText = t.setTheme;
            document.getElementById('txt-set-dev').innerText = t.setDev;

            document.getElementById('txt-priv-title').innerText = t.pTitle;
            document.getElementById('txt-priv-text').innerHTML = t.pText;
        }

        // UI Simulation for Video/Doc (Since real offline conversion needs heavy WebAssembly)
        function simulateProgress(containerId) {
            const container = document.getElementById(containerId);
            const bar = container.querySelector('.progress-bar');
            container.style.display = 'block';
            bar.style.width = '0%';
            
            let width = 0;
            const interval = setInterval(() => {
                width += Math.random() * 20;
                if(width >= 100) {
                    width = 100;
                    clearInterval(interval);
                    setTimeout(() => {
                        container.style.display = 'none';
                        alert('Demo: Processing completed! (In the real Flutter app, local libraries will handle this).');
                    }, 500);
                }
                bar.style.width = width + '%';
            }, 500);
        }

        // ================= REAL OFFLINE IMAGE COMPRESSOR/CONVERTER TO WebP =================
        const imageUpload = document.getElementById('image-upload');
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const downloadLink = document.getElementById('download-link');
        const imgProgress = document.getElementById('img-progress');
        const imgBar = imgProgress.querySelector('.progress-bar');

        imageUpload.addEventListener('change', function(event) {
            const file = event.target.files[0];
            if(!file) return;

            imgProgress.style.display = 'block';
            imgBar.style.width = '30%';
            downloadLink.style.display = 'none';

            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    imgBar.style.width = '60%';
                    // Set canvas dimensions to image dimensions
                    canvas.width = img.width;
                    canvas.height = img.height;
                    
                    // Draw image to canvas
                    ctx.drawImage(img, 0, 0);

                    // Convert to WebP with 0.6 quality (Compresses size significantly without much visual loss)
                    const webpDataUrl = canvas.toDataURL('image/webp', 0.6);
                    
                    imgBar.style.width = '100%';
                    
                    setTimeout(() => {
                        imgProgress.style.display = 'none';
                        downloadLink.href = webpDataUrl;
                        downloadLink.style.display = 'block';
                        imageUpload.value = ''; // Reset input
                    }, 500);
                }
                img.src = e.target.result;
            }
            reader.readAsDataURL(file);
        });

    </script>
</body>
</html>
