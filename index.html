<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AVA Movies & Animes - Secure Portal</title>
    <style>
        /* پلت رنگی تاریک با گرادینت انیمه‌ای و نئونی جدید */
        :root {
            --bg-color: #060810;
            --neon-blue: #00f0ff;
            --neon-glow-blue: rgba(0, 240, 255, 0.35);
            --neon-green: #00ffaa;
            --neon-glow-green: rgba(0, 255, 170, 0.4);
            
            /* گرادینت جدید و اختصاصی سبک انیمه/فیلم (ترکیب نارنجی اتمی، ارغوانی و قرمز آتشین) */
            --anime-gradient: linear-gradient(135deg, #ff6b00, #ff0055, #7000ff);
            --anime-glow: rgba(255, 107, 0, 0.5);
            
            --btn-dark-init: #0f121d;
            --text-dim: #435169;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, Helvetica, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
            position: relative;
            padding: 10px;
        }

        /* پس‌زمینه متحرک مینیاتوری سینما و انیمه */
        body::before {
            content: "";
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 200%;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="140" height="140" viewBox="0 0 140 140"><text x="15" y="30" fill="rgba(0, 240, 255, 0.04)" font-size="18">🎥</text><text x="85" y="25" fill="rgba(0, 255, 170, 0.03)" font-size="16">🎬</text><text x="50" y="65" fill="rgba(0, 240, 255, 0.03)" font-size="15">📺</text><text x="110" y="70" fill="rgba(0, 255, 170, 0.04)" font-size="17">🎞️</text><text x="20" y="105" fill="rgba(0, 240, 255, 0.03)" font-size="16">🎙️</text><text x="75" y="115" fill="rgba(0, 255, 170, 0.05)" font-size="18">🍿</text><text x="115" y="120" fill="rgba(0, 240, 255, 0.03)" font-size="15">🕶️</text><text x="10" y="70" fill="rgba(0, 255, 170, 0.02)" font-size="14">🦊</text><text x="80" y="75" fill="rgba(255, 255, 255, 0.03)" font-size="10">✨</text></svg>');
            background-repeat: repeat;
            z-index: -1;
            animation: cinemaSpaceScroll 30s linear infinite;
        }

        @keyframes cinemaSpaceScroll {
            0% { transform: translateY(0); }
            100% { transform: translateY(-50%); }
        }

        /* تصویر بنر بالای صفحه */
        .premium-top-banner {
            width: 92%;
            max-width: 460px;
            height: auto;
            margin-top: 25px;
            border-radius: 14px;
            box-shadow: 0 15px 45px rgba(0, 0, 0, 0.7);
            z-index: 10;
        }

        /* بخش مرکزی محتوا */
        .content-theater {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-top: 4vh;
            width: 100%;
            max-width: 500px;
            z-index: 10;
        }

        /* متن وضعیت نئونی */
        .neon-status-text {
            font-size: clamp(1.3rem, 4vw, 1.65rem);
            font-weight: 900;
            letter-spacing: 3px;
            color: var(--neon-blue);
            text-shadow: 0 0 10px var(--neon-glow-blue), 0 0 25px var(--neon-glow-blue);
            margin-bottom: 30px;
            text-transform: uppercase;
            text-align: center;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .neon-status-text.secured {
            color: var(--neon-green);
            text-shadow: 0 0 10px var(--neon-glow-green), 0 0 25px var(--neon-glow-green);
        }

        /* لودینگ آپارات سینمایی */
        .loader-theater-zone {
            width: 110px;
            height: 110px;
            margin-bottom: 35px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .cinema-reel-loader {
            width: 80px;
            height: 80px;
            border: 6px solid var(--neon-blue);
            border-radius: 50%;
            position: relative;
            box-shadow: 0 0 20px var(--neon-glow-blue);
            animation: fastReelSpin 1.3s linear infinite;
        }

        .cinema-reel-loader::before {
            content: '';
            position: absolute;
            top: 6px; left: 6px; right: 6px; bottom: 6px;
            border: 5px dashed var(--neon-blue);
            border-radius: 50%;
        }

        @keyframes fastReelSpin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .wipe-out {
            opacity: 0;
            transform: scale(0.4) rotate(-90deg);
            pointer-events: none;
            height: 0;
            margin: 0;
            overflow: hidden;
        }

        /* دکمه با طراحی تمام نئونی و گرادینت لاکچری */
        .ultra-neon-btn {
            background: var(--btn-dark-init);
            color: var(--text-dim);
            border: 1px solid rgba(255, 255, 255, 0.01);
            padding: 18px 0;
            width: 90%;
            max-width: 420px;
            text-align: center;
            font-size: clamp(1.05rem, 3.5vw, 1.25rem);
            font-weight: 800;
            border-radius: 50px;
            cursor: not-allowed;
            text-decoration: none;
            pointer-events: none;
            position: relative;
            transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            letter-spacing: 0.5px;
            box-shadow: inset 0 4px 8px rgba(0,0,0,0.9);
            display: inline-block;
        }

        /* فعال شدن دکمه با گرادینت زنده و پالس نوری خیره‌کننده انیمه */
        .ultra-neon-btn.unlocked {
            background: var(--anime-gradient);
            background-size: 200% auto;
            color: #ffffff;
            cursor: pointer;
            pointer-events: auto;
            border: 1px solid rgba(255, 255, 255, 0.25);
            box-shadow: 0 15px 40px rgba(255, 107, 0, 0.3), 0 0 25px rgba(255, 0, 85, 0.3);
            animation: moveGradient 3s linear infinite, glowPulse 1.8s infinite alternate;
        }

        @keyframes moveGradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes glowPulse {
            0% { box-shadow: 0 12px 35px rgba(255, 107, 0, 0.3), 0 0 20px rgba(255, 0, 85, 0.2); }
            100% { box-shadow: 0 22px 50px rgba(255, 107, 0, 0.6), 0 0 40px rgba(112, 0, 255, 0.5); filter: brightness(1.1); }
        }

        .ultra-neon-btn.unlocked:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 25px 55px rgba(255, 107, 0, 0.7), 0 0 45px rgba(255, 0, 85, 0.6);
        }

        .ultra-neon-btn.unlocked:active {
            transform: translateY(-2px) scale(1);
        }

        /* کانتینر اشتراکی و بهینه‌سازی شده برای فضاهای تبلیغاتی نیتیو */
        .native-ad-space {
            width: 100%;
            max-width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10;
            overflow: hidden;
        }

        .native-ad-space > div {
            max-width: 100% !important;
        }

        /* اعمال فاصله اختصاصی برای تبلیغ بالایی */
        .ad-top {
            margin-top: 15px;
            margin-bottom: 35px;
        }

        /* اعمال فاصله اختصاصی برای تبلیغ پایینی */
        .ad-bottom {
            margin-top: 45px;
            margin-bottom: 25px;
        }
    </style>
</head>
<body>

    <img src="https://trilliardaire.sirv.com/6156717967236862865_120.jpg" alt="AVA Streaming Content" class="premium-top-banner">

    <div class="content-theater">
        
        <div class="neon-status-text" id="statusPanel">DDos Gard</div>

        <div class="loader-theater-zone" id="theaterLoader">
            <div class="cinema-reel-loader"></div>
        </div>

        <div class="native-ad-space ad-top">
            <script async="async" data-cfasync="false" src="https://pl29662365.effectivecpmnetwork.com/75c6ed2bbbd3be8170e54a925c105abb/invoke.js"></script>
            <div id="container-75c6ed2bbbd3be8170e54a925c105abb"></div>
        </div>

        <a href="https://www.effectivecpmnetwork.com/t6555sr5ph?key=bf1001c9598de0606ec941ab9e3698d4" class="ultra-neon-btn" id="actionTrigger">
            AVA Free Movies & Animes
        </a>
        
    </div>

    <div class="native-ad-space ad-bottom">
        <script async="async" data-cfasync="false" src="https://pl29741961.effectivecpmnetwork.com/46fa53bab184d6979bf4dbeee413d25f/invoke.js"></script>
        <div id="container-46fa53bab184d6979bf4dbeee413d25f"></div>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            // غیب شدن لودینگ و تغییر ظاهر دکمه پس از ۲ ثانیه کامل
            setTimeout(function() {
                
                // ۱. پنهان کردن لودینگ آپارات
                const loader = document.getElementById('theaterLoader');
                loader.classList.add('wipe-out');

                // ۲. تغییر متن به وضعیت امن
                const status = document.getElementById('statusPanel');
                status.classList.add('secured');
                status.innerText = 'Site is protected';

                // ۳. روشن شدن موتور گرادینت دکمه و فعال شدن قابلیت کلیک
                const btn = document.getElementById('actionTrigger');
                btn.classList.add('unlocked');

            }, 2000);
        });
    </script>
</body>
</html>
