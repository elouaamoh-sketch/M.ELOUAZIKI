<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.ELOUAZIKI - التطبيق الشامل</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #121212;
            color: #ffffff;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }

        /* شاشة الترحيب والتسجيل عبر جوجل */
        #authScreen {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #181818;
            border: 1px solid #333;
            border-radius: 20px;
            padding: 30px;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.7);
            text-align: center;
        }

        #authScreen h1 {
            color: #f1c40f;
            font-size: 1.8rem;
            margin-bottom: 8px;
        }

        #authScreen p {
            color: #aaa;
            font-size: 1rem;
            margin-bottom: 25px;
        }

        .google-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            width: 100%;
            padding: 12px;
            background: #ffffff;
            color: #121212;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.3s;
            margin-bottom: 15px;
        }

        .google-btn:hover {
            background: #e0e0e0;
        }

        /* إدخال كود التحقق من 3 أرقام */
        #codeBox {
            display: none;
            flex-direction: column;
            width: 100%;
            animation: fadeIn 0.4s ease;
        }

        .form-group {
            margin-bottom: 15px;
            text-align: right;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.85rem;
            color: #ccc;
        }

        .form-group input {
            width: 100%;
            padding: 11px;
            background: #222;
            border: 1px solid #444;
            border-radius: 6px;
            color: #fff;
            outline: none;
            text-align: center;
            font-size: 1.1rem;
            letter-spacing: 3px;
        }

        .form-group input:focus {
            border-color: #f1c40f;
        }

        .action-btn {
            width: 100%;
            padding: 11px;
            background: #f1c40f;
            color: #121212;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }

        .action-btn:hover {
            background: #d4ac0d;
        }

        /* الشاشة الرئيسية الشاملة (تشبه Chrome وتضم كافة المواقع) */
        #homeScreen {
            display: none;
            flex-direction: column;
            align-items: center;
            width: 100%;
            max-width: 800px;
            animation: fadeIn 0.5s ease;
        }

        .home-header {
            color: #f1c40f;
            font-size: 2.2rem;
            margin-bottom: 5px;
            letter-spacing: 2px;
            text-align: center;
        }

        .home-sub {
            color: #888;
            margin-bottom: 25px;
            font-size: 0.95rem;
        }

        .section-title {
            width: 100%;
            color: #f1c40f;
            font-size: 1.1rem;
            margin: 20px 0 12px 0;
            border-bottom: 1px solid #333;
            padding-bottom: 5px;
            text-align: right;
        }

        .shortcuts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: 15px;
            width: 100%;
        }

        .shortcut-card {
            background: #1a1a1a;
            border: 1px solid #333;
            border-radius: 12px;
            padding: 18px 10px;
            text-align: center;
            text-decoration: none;
            color: #fff;
            transition: 0.3s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.4);
        }

        .shortcut-card:hover {
            border-color: #f1c40f;
            transform: translateY(-3px);
        }

        .shortcut-card .icon {
            font-size: 2rem;
            margin-bottom: 8px;
        }

        .shortcut-card span {
            font-size: 0.9rem;
            font-weight: 500;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <!-- 1. شاشة تسجيل الدخول والترحيب -->
    <div id="authScreen">
        <h1>M.ELOUAZIKI</h1>
        <p>مرحباً بك يا سيدي</p>

        <!-- زر التسجيل بـ Google -->
        <div id="googleLoginArea" style="width: 100%;">
            <button class="google-btn" onclick="showCodePrompt()">
                <svg width="20" height="20" viewBox="0 0 24 24"><path fill="#4285F4" d="M23.745 12.27c0-.7-.06-1.4-.19-2.07H12v4.51h6.6c-.29 1.52-1.14 2.82-2.4 3.68v3.05h3.88c2.27-2.09 3.66-5.17 3.66-9.17z"/><path fill="#34A853" d="M12 24c3.24 0 5.95-1.08 7.93-2.91l-3.88-3.05c-1.08.72-2.45 1.16-4.05 1.16-3.13 0-5.78-2.11-6.73-4.96H1.19v3.15C3.17 21.36 7.24 24 12 24z"/><path fill="#FBBC05" d="M5.27 14.24c-.25-.72-.38-1.49-.38-2.24s.13-1.52.38-2.24V6.61H1.19C.43 8.13 0 9.87 0 11.7s.43 3.57 1.19 5.09l4.08-2.55z"/><path fill="#EA4335" d="M12 4.75c1.77 0 3.35.61 4.6 1.8l3.42-3.42C17.95 1.19 15.24 0 12 0 7.24 0 3.17 2.64 1.19 6.61l4.08 3.15c.95-2.85 3.6-4.96 6.73-4.96z"/></svg>
                التسجيل باستخدام Google
            </button>
        </div>

        <!-- خانة إدخال الكود السري (من 3 أرقام) -->
        <div id="codeBox">
            <div class="form-group">
                <label>اختر حساب Gmail الخاص بك</label>
                <input type="email" id="emailInput" value="mohamed.elouaziki@gmail.com">
            </div>
            <div class="form-group">
                <label>أنشئ كلمة السر الخاصة بك</label>
                <input type="password" id="passInput" placeholder="كلمة المرور">
            </div>
            <div class="form-group">
                <label>أدخل كود التحقق (أدخل 3 أرقام، مثلاً: 123)</label>
                <input type="text" id="pinInput" maxlength="3" placeholder="---">
            </div>
            <button class="action-btn" onclick="verifyPin()">تأكيد والدخول</button>
        </div>
    </div>

    <!-- 2. الشاشة الرئيسية الشاملة (تضم جميع المواقع، الفيديوهات، وصفحات الويب) -->
    <div id="homeScreen">
        <h1 class="home-header">M.ELOUAZIKI</h1>
        <p class="home-sub">متصفحك الشامل - جميع المواقع والصفحات المفضلة</p>
        
        <div class="section-title">محركات البحث والمنصات الكبرى</div>
        <div class="shortcuts-grid">
            <a href="https://www.google.com" target="_blank" class="shortcut-card">
                <div class="icon">🌐</div>
                <span>جوجل الشامل</span>
            </a>
            <a href="https://www.youtube.com" target="_blank" class="shortcut-card">
                <div class="icon">📺</div>
                <span>يوتيوب</span>
            </a>
            <a href="https://github.com" target="_blank" class="shortcut-card">
                <div class="icon">💻</div>
                <span>جيت هب</span>
            </a>
            <a href="https://stackoverflow.com" target="_blank" class="shortcut-card">
                <div class="icon">🛠️</div>
                <span>ستاك أوفرفلو</span>
            </a>
        </div>

        <div class="section-title">تطبيقات ومواقع الويب المفضلة</div>
        <div class="shortcuts-grid">
            <a href="https://codepen.io" target="_blank" class="shortcut-card">
                <div class="icon">⚡</div>
                <span>كود بين</span>
            </a>
            <a href="https://en.wikipedia.org" target="_blank" class="shortcut-card">
                <div class="icon">📚</div>
                <span>ويكيبيديا</span>
            </a>
            <a href="https://translate.google.com" target="_blank" class="shortcut-card">
                <div class="icon">🔤</div>
                <span>الترجمة</span>
            </a>
            <a href="https://maps.google.com" target="_blank" class="shortcut-card">
                <div class="icon">🗺️</div>
                <span>الخرائط</span>
            </a>
        </div>

        <div class="section-title">الفيديوهات والوسائط</div>
        <div class="shortcuts-grid">
            <a href="https://www.youtube.com" target="_blank" class="shortcut-card">
                <div class="icon">🎬</div>
                <span>مشغل الفيديوهات 1</span>
            </a>
            <a href="https://www.youtube.com" target="_blank" class="shortcut-card">
                <div class="icon">🎥</div>
                <span>مشغل الفيديوهات 2</span>
            </a>
        </div>
    </div>

    <script>
        // إظهار خانة إدخال الكود عند الضغط على زر جوجل
        function showCodePrompt() {
            document.getElementById('googleLoginArea').style.display = 'none';
            document.getElementById('codeBox').style.display = 'flex';
        }

        // التحقق من الكود المكون من 3 أرقام
        function verifyPin() {
            const pin = document.getElementById('pinInput').value;
            const pass = document.getElementById('passInput').value;

            if(pin.length === 3) {
                // الانتقال المباشر للشاشة الرئيسية الشاملة
                document.getElementById('authScreen').style.display = 'none';
                document.getElementById('homeScreen').style.display = 'flex';
            } else {
                alert('الرجاء إدخال كود صحيح مكون من 3 أرقام (مثال: 123)');
            }
        }
    </script>
</body>
</html>
