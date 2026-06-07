<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<script async src="https://www.googletagmanager.com/gtag/js?id=G-KNTP1QVNHJ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-KNTP1QVNHJ');
</script>
    
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Google Books - Premium Portal</title>
    <style>
        :root {
            --tg-dark-bg: #17212b;
            --laser-blue: #00f0ff;
            --laser-glow: rgba(0, 240, 255, 0.45);
            --btn-blue: #2481cc;
            --btn-shadow: rgba(11, 44, 71, 0.95);
            --card-radius: 35px;
            --transition-smooth: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; }
        body { background-color: var(--tg-dark-bg); color: #ffffff; display: flex; flex-direction: column; align-items: center; justify-content: flex-start; min-height: 100vh; padding: 160px 24px 110px 24px; position: relative; overflow-x: hidden; -webkit-font-smoothing: antialiased; }
        
        /* افزایش فونت دکمه تلگرام به 16px */
        .telegram-btn { position: fixed; top: 30px; left: 50%; transform: translateX(-50%); z-index: 10000; background: linear-gradient(135deg, #00f0ff, #0066ff); color: #ffffff; text-decoration: none; padding: 13px 38px; border-radius: 20px; font-size: 16px; font-weight: 700; display: flex; align-items: center; justify-content: center; gap: 12px; border: 1px solid rgba(255, 255, 255, 0.25); box-shadow: 0 8px 25px var(--laser-glow), inset 0 1px 2px rgba(255, 255, 255, 0.4); transition: var(--transition-smooth); white-space: nowrap; }
        .telegram-btn:hover { transform: translateX(-50%) translateY(-3px); box-shadow: 0 12px 35px rgba(0, 240, 255, 0.7); filter: brightness(1.1); }
        .telegram-icon { width: 22px; height: 22px; fill: #ffffff; transition: var(--transition-smooth); }
        .telegram-btn:hover .telegram-icon { transform: scale(1.1); }
        
        .main-title { font-size: 3rem; font-weight: 900; text-align: center; margin-bottom: 40px; line-height: 1.2; letter-spacing: -1px; background: linear-gradient(180deg, #ffffff 0%, #b0c4de 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-shadow: 0 4px 20px rgba(0, 0, 0, 0.5); }
        
        /* استایل‌های بخش چوکات لیزری مایع */
        .premium-request-container {
            width: 100%;
            max-width: 1200px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 24px;
            margin-bottom: 60px;
            perspective: 1000px;
        }
        .laser-chokat {
            width: 100%;
            min-height: 140px;
            background: linear-gradient(270deg, #111c24, #192d3d, #111c24);
            background-size: 400% 400%;
            animation: gradientFluid 12s ease infinite;
            border: 2px solid rgba(0, 240, 255, 0.3);
            border-radius: 24px;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 30px 24px;
            text-align: center;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4), 0 0 25px rgba(0, 240, 255, 0.15);
            transform: rotateX(6deg);
            transition: var(--transition-smooth);
        }
        .laser-chokat:hover {
            transform: rotateX(2deg) translateY(-2px);
            border-color: rgba(0, 240, 255, 0.5);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5), 0 0 35px rgba(0, 240, 255, 0.3);
        }
        @keyframes gradientFluid {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .laser-shapes-layer {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 1;
        }
        .laser-svg {
            position: absolute;
            stroke: var(--laser-blue);
            stroke-width: 1.2;
            fill: none;
            opacity: 0.18;
            filter: drop-shadow(0 0 5px var(--laser-blue));
            animation: shapeLiquidMove 16s ease-in-out infinite alternate;
        }
        @keyframes shapeLiquidMove {
            0% { transform: translate(0, 0) rotate(0deg) scale(1); }
            50% { transform: translate(30px, -20px) rotate(15deg) scale(1.1); }
            100% { transform: translate(-20px, 25px) rotate(-15deg) scale(0.95); }
        }
        .laser-bubble {
            position: absolute;
            background: rgba(0, 240, 255, 0.05);
            border: 1px solid rgba(0, 240, 255, 0.3);
            border-radius: 50%;
            bottom: -30px;
            filter: drop-shadow(0 0 4px var(--laser-blue));
            animation: bubbleRise 9s infinite linear;
            z-index: 1;
        }
        @keyframes bubbleRise {
            0% { transform: translateY(0) translateX(0); opacity: 0; }
            15% { opacity: 0.5; }
            85% { opacity: 0.5; }
            100% { transform: translateY(-200px) translateX(25px); opacity: 0; }
        }
        .chokat-text {
            position: relative;
            z-index: 2;
            font-size: 1.15rem;
            font-weight: 600;
            color: #ffffff;
            line-height: 1.6;
            letter-spacing: 0.3px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.8), 0 0 10px rgba(0, 240, 255, 0.3);
            max-width: 850px;
        }
        .chokat-btn {
            max-width: 320px;
            z-index: 2;
        }

        .cards-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 40px; width: 100%; max-width: 1200px; justify-content: center; }
        .card-wrapper { display: flex; flex-direction: column; align-items: center; width: 100%; background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.06); padding: 22px; border-radius: calc(var(--card-radius) + 10px); box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3); transition: var(--transition-smooth); }
        .card-wrapper:hover { transform: translateY(-8px); background: rgba(255, 255, 255, 0.05); border-color: rgba(255, 255, 255, 0.12); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5); }
        .card-img-box { width: 100%; aspect-ratio: 1 / 1; background-color: #ffffff; border-radius: var(--card-radius); padding: 20px; display: flex; align-items: center; justify-content: center; margin-bottom: 22px; box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3); transition: var(--transition-smooth); }
        .card-img { max-width: 100%; max-height: 100%; object-fit: contain; transition: var(--transition-smooth); }
        .card-wrapper:hover .card-img { transform: scale(1.05); }
        
        /* افزایش فونت دکمه‌های اصلی کارت‌ها به 16px */
        .card-btn { width: 100%; background-color: var(--btn-blue); color: #ffffff; text-decoration: none; text-align: center; padding: 14px 20px; border-radius: 16px; font-size: 16px; font-weight: 600; box-shadow: 0 10px 22px var(--btn-shadow); border: 1px solid rgba(255, 255, 255, 0.08); transition: var(--transition-smooth); cursor: pointer;}
        .card-btn:hover { background-color: #2b96eb; box-shadow: 0 12px 28px rgba(36, 129, 204, 0.5); transform: translateY(-1px); }
        .attribution { display: none; }
        
        /* استایل بنر شناور تبلیغاتی در پایین صفحه */
        #floating-ad {
            position: fixed;
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;
            z-index: 999999999;
            width: auto;
            height: auto;
            display: flex;
            justify-content: center;
            align-items: center;
            pointer-events: auto;
        }

        /* اضافه شده برای پنجره اسکرولی Modal */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.85);
            z-index: 1000000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
            padding: 20px;
            direction: ltr; /* برای چپ چین بودن متن انگلیسی */
        }
        .modal-content {
            background: #1e2a36;
            border: 1px solid rgba(0, 240, 255, 0.3);
            border-radius: 20px;
            padding: 30px;
            max-width: 600px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto; /* ایجاد اسکرول داخلی در صورت نیاز */
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6), 0 0 25px rgba(0, 240, 255, 0.15);
            display: flex;
            flex-direction: column;
            gap: 24px;
        }
        .modal-text {
            color: #ffffff;
            line-height: 1.7;
            font-size: 15px;
            white-space: pre-line;
            text-align: left;
        }
        .modal-got-it-btn {
            background-color: var(--btn-blue);
            color: #ffffff;
            text-decoration: none;
            text-align: center;
            padding: 14px 20px;
            border-radius: 16px;
            font-size: 16px;
            font-weight: 600;
            box-shadow: 0 10px 22px var(--btn-shadow);
            border: 1px solid rgba(255, 255, 255, 0.08);
            transition: var(--transition-smooth);
            width: 100%;
        }
        .modal-got-it-btn:hover {
            background-color: #2b96eb;
            transform: translateY(-2px);
            box-shadow: 0 12px 28px rgba(36, 129, 204, 0.5);
        }
        
        @media (max-width: 950px) { .cards-container { grid-template-columns: repeat(2, 1fr); gap: 30px; } .main-title { font-size: 2.5rem; } }
        @media (max-width: 600px) {
            body { padding-top: 130px; padding-left: 12px; padding-right: 12px; }
            .main-title { font-size: 1.8rem; margin-bottom: 35px; }
            .premium-request-container { margin-bottom: 40px; gap: 16px; }
            .laser-chokat { padding: 20px 15px; min-height: 110px; border-radius: 18px; }
            .chokat-text { font-size: 0.95rem; line-height: 1.5; }
            .cards-container { grid-template-columns: repeat(2, 1fr); gap: 12px; }
            .card-wrapper { padding: 10px; border-radius: 25px; }
            .card-img-box { border-radius: 20px; padding: 10px; margin-bottom: 12px; }
            /* افزایش سایز فونت دکمه‌ها در موبایل به اندازه ۱ عدد */
            .card-btn { font-size: 12px; padding: 11px 4px; border-radius: 12px; box-shadow: 0 6px 14px var(--btn-shadow); }
            .telegram-btn { padding: 11px 24px; font-size: 14px; top: 20px; border-radius: 14px; box-shadow: 0 6px 18px var(--laser-glow); }
        }
    </style>
</head>
<body>

    <a href="https://books-photoes.webflow.io/old-home" class="telegram-btn">
        <span>Our Telegram channels</span>
        <svg class="telegram-icon" viewBox="0 0 24 24">
            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-1-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69.01-.03.01-.14-.07-.2-.08-.06-.19-.04-.27-.02-.11.02-1.93 1.23-5.46 3.62-.51.35-.98.52-1.4.51-.46-.01-1.35-.26-2.01-.48-.81-.27-1.46-.42-1.4-.88.03-.24.38-.49 1.04-.74 4.07-1.77 6.79-2.94 8.15-3.5 3.89-1.61 4.7-1.89 5.23-1.9.11 0 .37.03.54.17.14.12.18.28.2.45-.02.07-.02.13-.03.2z"/>
        </svg>
    </a>

    <h1 class="main-title">Welcome To<br>!Google Books</h1>

    <div class="premium-request-container">
        <div class="laser-chokat">
            <div class="laser-shapes-layer">
                <svg class="laser-svg" style="top: 15%; left: 8%; animation-delay: 0s; width: 35px; height: 35px;" viewBox="0 0 24 24"><path d="M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.39-.39-1.02-.39-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"/></svg>
                <svg class="laser-svg" style="top: 55%; left: 15%; animation-delay: -3s; width: 40px; height: 40px;" viewBox="0 0 24 24"><path d="M18 2H6c-1.1 0-2 .9-2 2v16c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm0 18H6V4h12v16z"/></svg>
                <svg class="laser-svg" style="top: 20%; right: 12%; animation-delay: -6s; width: 38px; height: 38px;" viewBox="0 0 24 24"><path d="M21 3c-1.66 0-3 1.34-3 3 0 .7.24 1.33.64 1.85L11.5 15.0L9 12.5l-1.5 1.5 4 4 8-8.5c.53.37 1.17.5 1.85.5 1.66 0 3-1.34 3-3s-1.34-3-3-3z"/></svg>
                <svg class="laser-svg" style="top: 50%; right: 7%; animation-delay: -9s; width: 45px; height: 45px;" viewBox="0 0 24 24"><path d="M12 6c-1.5-2-5-2.5-7-2.5v14c2 0 5.5.5 7 2.5 1.5-2 5-2.5 7-2.5V3.5c-2 0-5.5.5-7 2.5z"/></svg>
                <div class="laser-bubble" style="left: 20%; width: 12px; height: 12px; animation-duration: 7s; animation-delay: 1s;"></div>
                <div class="laser-bubble" style="left: 45%; width: 8px; height: 8px; animation-duration: 10s; animation-delay: 3s;"></div>
                <div class="laser-bubble" style="left: 70%; width: 14px; height: 14px; animation-duration: 8s; animation-delay: 0s;"></div>
                <div class="laser-bubble" style="right: 25%; width: 10px; height: 10px; animation-duration: 11s; animation-delay: 5s;"></div>
            </div>
            <div class="chokat-text">
            Couldn't find your book? Click the button below and request it from support
            </div>
        </div>
        <a href="https://google-books.github.io/Request/" class="card-btn chokat-btn">Request Book</a>
    </div>

    <div class="cards-container">
        <div class="card-wrapper">
            <div class="card-img-box">
                <img src="https://trilliardaire.sirv.com/FreeBooks.png" alt="Free Books" class="card-img" crossorigin="anonymous">
            </div>
            <a href="https://google-books.github.io/Archives/" class="card-btn">Free Books</a>
        </div>

        <div class="card-wrapper">
            <div class="card-img-box">
                <img src="https://trilliardaire.sirv.com/%DA%A9%D8%AA%D8%A7%D8%A8%20%D9%87%D8%A7%DB%8C%20%DA%AF%D9%88%DA%AF%D9%84/audio.avif" alt="Free Audio Books" class="card-img" crossorigin="anonymous">
            </div>
            <a href="#" id="open-audio-modal" class="card-btn">Free Audio Books</a>
        </div>

        <div class="card-wrapper">
            <div class="card-img-box">
                <img src="https://trilliardaire.sirv.com/pngtree-google-play-download-icon-vector-png-image_12256662.png" alt="Our Apps" class="card-img" crossorigin="anonymous">
            </div>
            <a href="https://play.google.com/store/apps/developer?id=AbdulrahmanANDROID" class="card-btn">Our Apps</a>
        </div>

        <div class="card-wrapper">
            <div class="card-img-box">
                <img src="https://trilliardaire.sirv.com/%DA%A9%D8%AA%D8%A7%D8%A8%20%D9%87%D8%A7%DB%8C%20%DA%AF%D9%88%DA%AF%D9%84/lopk.jpg" alt="Requested Books" class="card-img" crossorigin="anonymous">
            </div>
            <a href="https://google-books.github.io/Requested-Books/" class="card-btn">Requested Books</a>
        </div>
    </div>

    <div id="audio-modal" class="modal-overlay">
        <div class="modal-content">
            <div class="modal-text">📚 All audiobooks are free. Download Guide:

1. Click the three-line menu in the top-right corner and search for your book.

2. Click on the book cover or image.

3. On the new page, scroll all the way down and click "Torrent Free Downloads."

4. If you already have an account, enter your username and password and sign in. If you don't have an account, click "Register", create a new username, enter your email address and password, and complete the registration.

5. After registering, click "Login" and enter your username and password.

6. Now you can search for your book again and click "Torrent Free Downloads" at the bottom of the page.

7. A very small file will be downloaded first. Open the downloaded file and use a compatible torrent client to start downloading the audiobook automatically.</div>
            <a href="https://audiobookbay.lu/" target="_blank" id="modal-got-it" class="modal-got-it-btn">Got it</a>
        </div>
    </div>

    <div class="attribution">
        <a href="https://www.flaticon.com/free-icons/telegram" title="telegram icons">Telegram icons created by See Icons - Flaticon</a>
    </div>

    <div id="floating-ad"></div>
    
<script src="https://pl29659533.effectivecpmnetwork.com/66/5a/20/665a203e5d7e2ff6ed7a6d50be88fe86.js"></script>




    <script>
    (function(){
        let key="";
        let width=0;
        let height=0;
        const w=window.innerWidth;

        /* موبایل کوچک */
        if(w<=360){
            key="178c2c0d4b1d26d354d5e45deb460267";
            width=320;
            height=50;
        }
        /* موبایل بزرگ و تبلت */
        else if(w<=768){
            key="96015f0ace861be411b4df77f4509684";
            width=468;
            height=60;
        }
        /* دسکتاپ */
        else {
            key="0060a66942efa379761d703d1b4b8a14";
            width=728;
            height=90;
        }

        window.atOptions={
            key:key,
            format:'iframe',
            height:height,
            width:width,
            params:{}
        };

        const s=document.createElement("script");
        s.src="https://speedingdeadlyplays.com/"+key+"/invoke.js";
        s.async=true;
        document.getElementById("floating-ad").appendChild(s);
    })();
    </script>

    <script>
        const openBtn = document.getElementById('open-audio-modal');
        const modal = document.getElementById('audio-modal');
        const gotItBtn = document.getElementById('modal-got-it');

        // باز کردن پنجره با کلیک روی دکمه
        openBtn.addEventListener('click', function(e) {
            e.preventDefault(); // جلوگیری از رفتن به بالای صفحه
            modal.style.display = 'flex';
        });

        // بستن پنجره بعد از کلیک روی دکمه Got it
        gotItBtn.addEventListener('click', function() {
            modal.style.display = 'none';
        });

        // بستن پنجره در صورت کلیک کردن روی فضای خالی مشکی رنگ
        modal.addEventListener('click', function(e) {
            if (e.target === modal) {
                modal.style.display = 'none';
            }
        });
    </script>

    <div class="attribution">
        <a href="https://www.flaticon.com/free-icons/telegram" title="telegram icons">Telegram icons created by See Icons - Flaticon</a>
    </div>

<script src="https://pl29669973.effectivecpmnetwork.com/9c/e9/83/9ce9830bc1357a8a72e0682e4af62ce3.js"></script>

  
</body>
</html>

