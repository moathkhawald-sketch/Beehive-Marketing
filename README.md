<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بلاك دايموند | Black Diamond</title>
    <!-- خطوط جوجل (Cairo) -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <!-- أيقونات FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-color: #0a0a0a;
            --gold: #d4af37;
            --gold-light: #f3e5ab;
            --card-bg: rgba(25, 25, 25, 0.7);
            --text-light: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Cairo', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-light);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
            background-image: radial-gradient(circle at 50% 50%, #1a1a1a 0%, #000000 100%);
        }

        /* تأثيرات الخلفية المتحركة (جمرات متوهجة) */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            background: radial-gradient(circle, var(--gold) 0%, transparent 70%);
            border-radius: 50%;
            opacity: 0.3;
            animation: float 6s infinite ease-in-out alternate;
        }

        @keyframes float {
            0% { transform: translateY(0) scale(1); opacity: 0.2; }
            100% { transform: translateY(-50px) scale(1.5); opacity: 0.6; }
        }

        /* الحاوية الرئيسية */
        .container {
            position: relative;
            z-index: 1;
            width: 90%;
            max-width: 450px;
            margin: 40px auto;
            text-align: center;
        }

        /* رأس الصفحة */
        .header {
            margin-bottom: 30px;
            animation: fadeInDown 1s ease;
        }

        .logo-container {
            width: 120px;
            height: 120px;
            margin: 0 auto 15px;
            background: linear-gradient(135deg, #2a2a2a, #000);
            border: 3px solid var(--gold);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
            animation: pulseGlow 2s infinite alternate;
        }

        .logo-container i {
            font-size: 3rem;
            color: var(--gold);
        }

        .title {
            font-size: 1.8rem;
            font-weight: 900;
            color: var(--gold);
            text-shadow: 0 2px 10px rgba(0,0,0,0.5);
            margin-bottom: 5px;
        }

        .subtitle {
            font-size: 1rem;
            color: #aaa;
            margin-bottom: 20px;
        }

        /* الروابط (الأزرار) */
        .links-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .link-item {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px 20px;
            background: var(--card-bg);
            border: 1px solid rgba(212, 175, 55, 0.2);
            border-radius: 12px;
            text-decoration: none;
            color: var(--text-light);
            font-size: 1.1rem;
            font-weight: 700;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            opacity: 0;
            transform: translateY(20px);
            animation: fadeInUp 0.5s forwards;
        }

        /* تأثير تأخير ظهور الأزرار تتابعياً */
        .link-item:nth-child(1) { animation-delay: 0.2s; }
        .link-item:nth-child(2) { animation-delay: 0.4s; }
        .link-item:nth-child(3) { animation-delay: 0.6s; }
        .link-item:nth-child(4) { animation-delay: 0.8s; }

        .link-item i {
            margin-left: 10px;
            font-size: 1.3rem;
            color: var(--gold);
        }

        .link-item:hover {
            transform: translateY(-3px) scale(1.02);
            background: rgba(212, 175, 55, 0.1);
            border-color: var(--gold);
            box-shadow: 0 5px 15px rgba(212, 175, 55, 0.2);
        }

        /* تذييل الصفحة (الفوتر) */
        footer {
            margin-top: 50px;
            padding-bottom: 20px;
            font-size: 0.9rem;
            color: #777;
            animation: fadeIn 2s ease;
        }

        .dev-link {
            color: var(--gold);
            text-decoration: none;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .dev-link:hover {
            color: var(--gold-light);
            text-shadow: 0 0 8px rgba(212, 175, 55, 0.6);
        }

        /* نافذة حقوق التطوير (Modal) */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 100;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .modal-content {
            background: #111;
            border: 2px solid var(--gold);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            width: 90%;
            max-width: 350px;
            transform: scale(0.8);
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            position: relative;
        }

        .modal-overlay.active .modal-content {
            transform: scale(1);
        }

        .close-btn {
            position: absolute;
            top: 10px;
            right: 15px;
            color: #aaa;
            font-size: 1.5rem;
            cursor: pointer;
            transition: 0.3s;
        }

        .close-btn:hover {
            color: var(--gold);
        }

        .modal-content h3 {
            color: var(--text-light);
            margin-bottom: 10px;
            font-size: 1.4rem;
        }

        .modal-content h3 span {
            color: var(--gold);
        }

        .modal-content p {
            color: #aaa;
            font-size: 0.9rem;
            margin-bottom: 20px;
        }

        .modal-btn {
            display: inline-block;
            background: var(--gold);
            color: #000;
            padding: 10px 20px;
            border-radius: 8px;
            text-decoration: none;
            font-weight: bold;
            transition: 0.3s;
        }

        .modal-btn:hover {
            background: var(--gold-light);
            box-shadow: 0 0 15px rgba(212, 175, 55, 0.5);
        }

        /* Animations */
        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeInUp {
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulseGlow {
            from { box-shadow: 0 0 10px rgba(212, 175, 55, 0.2); }
            to { box-shadow: 0 0 25px rgba(212, 175, 55, 0.6); }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>

    <!-- الجمرات المتحركة في الخلفية -->
    <div class="particles" id="particles"></div>

    <div class="container">
        <!-- الهيدر واللوجو -->
        <header class="header">
            <div class="logo-container">
                <i class="fa-solid fa-fire-flame-curved"></i>
            </div>
            <h1 class="title">بلاك دايموند</h1>
            <p class="subtitle">شركة أسرتي الذهبية _ فحم وحطب</p>
        </header>

        <!-- الروابط -->
        <main class="links-container">
            <a href="https://www.blackdiamondjo.com/" target="_blank" class="link-item">
                <i class="fa-solid fa-globe"></i>
                الموقع الإلكتروني
            </a>
            
            <a href="https://www.facebook.com/profile.php?id=61593015848857" target="_blank" class="link-item">
                <i class="fa-brands fa-facebook-f"></i>
                صفحتنا على فيسبوك
            </a>
            
            <a href="https://maps.app.goo.gl/hmkk3k2nSvVbcVm39" target="_blank" class="link-item">
                <i class="fa-solid fa-location-dot"></i>
                موقعنا على الخريطة
            </a>
            
            <a href="mailto:info@blackdiamondjo.com" class="link-item">
                <i class="fa-solid fa-envelope"></i>
                info@blackdiamondjo.com
            </a>
        </main>

        <!-- الفوتر وحقوق التطوير -->
        <footer>
            <p>تطوير وبرمجة <span class="dev-link" onclick="openModal()">Beehive Marketing</span> &copy; 2026</p>
        </footer>
    </div>

    <!-- نافذة شركة التطوير (Modal) -->
    <div class="modal-overlay" id="beehiveModal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            <h3><span>Beehive</span> Marketing</h3>
            <p>حلول برمجية وتسويقية متكاملة</p>
            <a href="https://keen-cascaron-437ef0.netlify.app/" target="_blank" class="modal-btn">
                <i class="fa-solid fa-headset"></i> تواصل معنا
            </a>
        </div>
    </div>

    <script>
        // دالة توليد الجمرات المتحركة في الخلفية
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 15;

            for (let i = 0; i < particleCount; i++) {
                let particle = document.createElement('div');
                particle.classList.add('particle');
                
                // أحجام وأماكن عشوائية
                let size = Math.random() * 80 + 20 + 'px';
                particle.style.width = size;
                particle.style.height = size;
                particle.style.left = Math.random() * 100 + 'vw';
                particle.style.top = Math.random() * 100 + 'vh';
                
                // تأخير وحركة عشوائية
                particle.style.animationDuration = (Math.random() * 4 + 3) + 's';
                particle.style.animationDelay = (Math.random() * 2) + 's';

                particlesContainer.appendChild(particle);
            }
        }
        createParticles();

        // دوال التحكم بالنافذة المنبثقة (Modal)
        const modal = document.getElementById('beehiveModal');

        function openModal() {
            modal.classList.add('active');
        }

        function closeModal() {
            modal.classList.remove('active');
        }

        // إغلاق النافذة عند الضغط خارجها
        window.onclick = function(event) {
            if (event.target == modal) {
                closeModal();
            }
        }
    </script>
</body>
</html>
