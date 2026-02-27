<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مغامرة الرياضيات الشاملة - الصف الخامس 🏆</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        /* جميع الأنماط السابقة مع إضافة شاشة السجلات وتحسينات */
        :root {
            --sky: #1a1a4e;
            --ocean: #0d3b6e;
            --island: #2d6a4f;
            --sand: #f9c74f;
            --coral: #f94144;
            --mint: #90e0ef;
            --cloud: #caf0f8;
            --gold: #ffd60a;
            --purple: #7b2d8b;
            --green: #52b788;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Tajawal', sans-serif;
            background: linear-gradient(180deg, #0a0a2e 0%, #1a1a6e 40%, #0d3b6e 100%);
            min-height: 100vh;
            color: white;
            overflow-x: hidden;
        }

        /* Stars background */
        .stars {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            animation: twinkle var(--d, 3s) ease-in-out infinite alternate;
        }
        @keyframes twinkle {
            from { opacity: 0.2; transform: scale(1); }
            to { opacity: 1; transform: scale(1.5); }
        }

        /* Screen system */
        .screen { display: none; position: relative; z-index: 1; min-height: 100vh; }
        .screen.active { display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 20px; }

        /* Home Screen */
        #home { background: radial-gradient(ellipse at 50% 0%, #3a0ca3 0%, transparent 70%); }
        .game-title {
            font-size: clamp(2.5rem, 8vw, 5rem);
            font-weight: 900;
            text-align: center;
            background: linear-gradient(135deg, #ffd60a, #f9c74f, #ffd60a);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 30px rgba(255,214,10,0.5));
            animation: glow-title 2s ease-in-out infinite alternate;
        }
        @keyframes glow-title {
            from { filter: drop-shadow(0 0 20px rgba(255,214,10,0.4)); }
            to { filter: drop-shadow(0 0 50px rgba(255,214,10,0.9)); }
        }

        .subtitle { font-size: 1.3rem; color: #caf0f8; margin-bottom: 40px; }
        .hero-character { font-size: 8rem; animation: float 3s ease-in-out infinite; }
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(-5deg); }
            50% { transform: translateY(-20px) rotate(5deg); }
        }

        .start-btn {
            background: linear-gradient(135deg, #ffd60a, #f9a825);
            color: #1a1a4e;
            border: none;
            padding: 18px 60px;
            font-size: 1.5rem;
            font-weight: 900;
            border-radius: 50px;
            cursor: pointer;
            margin-top: 30px;
            box-shadow: 0 10px 40px rgba(255,214,10,0.5);
            animation: pulse-btn 2s infinite;
            transition: transform 0.2s;
        }
        .start-btn:hover { transform: scale(1.05); }
        @keyframes pulse-btn {
            0%, 100% { box-shadow: 0 10px 40px rgba(255,214,10,0.5); }
            50% { box-shadow: 0 10px 40px rgba(255,214,10,0.5), 0 0 0 20px rgba(255,214,10,0); }
        }

        /* Map Screen */
        #map { padding: 30px 20px; }
        .map-title {
            font-size: 2rem;
            font-weight: 900;
            color: var(--gold);
            text-align: center;
            margin-bottom: 40px;
            text-shadow: 0 0 20px rgba(255,214,10,0.5);
        }
        .islands-container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            justify-content: center;
            max-width: 1200px;
            width: 100%;
        }
        .island-card {
            background: linear-gradient(135deg, var(--c1, #2d6a4f), var(--c2, #1b4332));
            border-radius: 24px;
            padding: 30px;
            width: 260px;
            text-align: center;
            cursor: pointer;
            border: 3px solid rgba(255,255,255,0.1);
            transition: all 0.3s ease;
            position: relative;
        }
        .island-card:hover { transform: translateY(-8px) scale(1.03); border-color: rgba(255,255,255,0.4); }
        .island-card.locked { opacity: 0.5; cursor: not-allowed; filter: grayscale(0.5); }
        .island-emoji { font-size: 4rem; margin-bottom: 15px; display: block; }
        .island-name { font-size: 1.3rem; font-weight: 900; color: white; margin-bottom: 8px; }
        .island-desc { font-size: 0.9rem; color: rgba(255,255,255,0.8); }
        .island-progress { margin-top: 15px; background: rgba(0,0,0,0.3); border-radius: 20px; height: 8px; overflow: hidden; }
        .island-progress-fill { height: 100%; background: var(--gold); border-radius: 20px; transition: width 1s; }
        .island-stars { color: var(--gold); font-size: 1.2rem; margin-top: 10px; }
        .lock-badge { position: absolute; top: 15px; left: 15px; font-size: 1.5rem; }

        /* Lessons Screen */
        #lessons { padding: 30px 20px; }
        .back-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255,255,255,0.15);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            padding: 10px 20px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 700;
            transition: all 0.2s;
            z-index: 100;
        }
        .back-btn:hover { background: rgba(255,255,255,0.25); transform: scale(1.05); }
        .lessons-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            max-width: 800px;
            width: 100%;
            margin-top: 30px;
        }
        .lesson-card {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 20px;
            padding: 25px;
            width: 220px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }
        .lesson-card:hover { background: rgba(255,255,255,0.2); transform: translateY(-5px); border-color: var(--gold); }
        .lesson-card.done { border-color: var(--green); background: rgba(82,183,136,0.2); }
        .lesson-emoji { font-size: 3rem; margin-bottom: 10px; }
        .lesson-title { font-size: 1.1rem; font-weight: 700; color: white; }

        /* Activity Screen */
        #activity { padding: 30px 20px; justify-content: flex-start; padding-top: 80px; }
        .activity-box {
            background: rgba(255,255,255,0.08);
            backdrop-filter: blur(20px);
            border: 2px solid rgba(255,255,255,0.15);
            border-radius: 28px;
            padding: 40px;
            max-width: 700px;
            width: 100%;
            text-align: center;
        }
        .activity-type-badge {
            display: inline-block;
            background: var(--gold);
            color: #1a1a4e;
            padding: 6px 20px;
            border-radius: 20px;
            font-weight: 900;
            font-size: 0.9rem;
            margin-bottom: 20px;
        }
        .activity-title { font-size: 1.8rem; font-weight: 900; color: white; margin-bottom: 10px; }
        .quiz-options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }
        .quiz-option {
            background: rgba(255,255,255,0.1);
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 16px;
            padding: 18px;
            font-size: 1.2rem;
            color: white;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 700;
        }
        .quiz-option:hover { background: rgba(255,255,255,0.2); border-color: var(--gold); }
        .quiz-option.correct { background: rgba(82,183,136,0.4); border-color: #52b788; animation: correct-bounce 0.5s; }
        .quiz-option.wrong { background: rgba(249,65,68,0.3); border-color: #f94144; animation: shake 0.4s; }
        @keyframes correct-bounce { 0%,100%{transform:scale(1)} 50%{transform:scale(1.1)} }
        @keyframes shake { 0%,100%{transform:translateX(0)} 25%{transform:translateX(-10px)} 75%{transform:translateX(10px)} }

        /* Buttons */
        .action-btn {
            background: linear-gradient(135deg, #3a0ca3, #7b2d8b);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1rem;
            font-weight: 700;
            border-radius: 30px;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.2s;
            box-shadow: 0 5px 20px rgba(58,12,163,0.4);
        }
        .action-btn:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(58,12,163,0.5); }
        .action-btn.gold { background: linear-gradient(135deg, #ffd60a, #f9a825); color: #1a1a4e; }

        /* Success Screen */
        #success { text-align: center; }
        .success-emoji { font-size: 8rem; animation: float 2s ease-in-out infinite; }
        .success-title { font-size: 3rem; font-weight: 900; color: var(--gold); margin: 20px 0; }
        .success-stars { font-size: 3rem; margin: 10px; animation: stars-pop 0.5s 0.3s both; }
        @keyframes stars-pop {
            from { transform: scale(0) rotate(-20deg); opacity: 0; }
            to { transform: scale(1) rotate(0); opacity: 1; }
        }

        /* Assessment Screen */
        #assessment { text-align: center; }
        .assessment-icon { font-size: 6rem; margin-bottom: 20px; }
        .assessment-title { font-size: 2.5rem; font-weight: 900; color: var(--gold); margin: 10px 0; }
        .assessment-detail { font-size: 1.5rem; margin: 20px 0; color: var(--mint); }
        .assessment-stars { font-size: 3rem; margin: 20px; color: var(--gold); }

        /* Records Screen */
        #records { text-align: center; padding: 30px 20px; }
        .records-table {
            width: 100%;
            max-width: 800px;
            margin: 20px auto;
            border-collapse: collapse;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            overflow: hidden;
        }
        .records-table th, .records-table td {
            padding: 12px;
            border-bottom: 1px solid rgba(255,255,255,0.2);
            color: white;
        }
        .records-table th {
            background: var(--gold);
            color: #1a1a4e;
            font-weight: 900;
        }

        /* Fireworks */
        .firework {
            position: fixed;
            width: 10px; height: 10px;
            border-radius: 50%;
            animation: firework-anim 1s ease-out forwards;
            pointer-events: none;
        }
        @keyframes firework-anim {
            0% { transform: translate(0,0) scale(1); opacity: 1; }
            100% { transform: translate(var(--tx), var(--ty)) scale(0); opacity: 0; }
        }

        /* Progress bar */
        .xp-bar-container {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 90%;
            max-width: 500px;
            background: rgba(0,0,0,0.4);
            border-radius: 20px;
            padding: 8px 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 50;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.15);
        }
        .xp-label { font-size: 0.85rem; color: var(--gold); font-weight: 700; white-space: nowrap; }
        .xp-track { flex: 1; background: rgba(255,255,255,0.1); border-radius: 10px; height: 10px; overflow: hidden; }
        .xp-fill { height: 100%; background: linear-gradient(90deg, #ffd60a, #f9a825); border-radius: 10px; transition: width 1s; }

        /* Notification */
        .notification {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(-100px);
            background: linear-gradient(135deg, #52b788, #2d6a4f);
            color: white;
            padding: 15px 30px;
            border-radius: 30px;
            font-weight: 700;
            font-size: 1.1rem;
            z-index: 200;
            transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        .notification.show { transform: translateX(-50%) translateY(0); }

        /* Wave */
        .wave-container {
            position: fixed;
            bottom: 0; left: 0;
            width: 100%;
            height: 120px;
            pointer-events: none;
            z-index: 0;
            opacity: 0.3;
        }
        .wave {
            position: absolute;
            bottom: 0;
            width: 200%;
            height: 100px;
            background: #0d3b6e;
            border-radius: 50% 50% 0 0 / 30px 30px 0 0;
            animation: wave-anim 4s ease-in-out infinite;
        }
        .wave:nth-child(2) {
            background: #1a5276;
            animation-delay: -2s;
            opacity: 0.5;
        }
        @keyframes wave-anim {
            0%, 100% { transform: translateX(0); }
            50% { transform: translateX(-25%); }
        }

        /* Records button */
        .records-btn {
            position: fixed;
            top: 20px;
            left: 20px;
            background: rgba(255,255,255,0.15);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            padding: 10px 20px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 700;
            transition: all 0.2s;
            z-index: 100;
        }
        .records-btn:hover { background: rgba(255,255,255,0.25); transform: scale(1.05); }

        @media (max-width: 600px) {
            .quiz-options { grid-template-columns: 1fr; }
            .island-card { width: 100%; max-width: 320px; }
            .lesson-card { width: 160px; }
            .activity-box { padding: 25px; }
        }
    </style>
</head>
<body>

<!-- Stars -->
<div class="stars" id="starsContainer"></div>

<!-- Wave -->
<div class="wave-container">
    <div class="wave"></div>
    <div class="wave"></div>
</div>

<!-- Notification -->
<div class="notification" id="notification">✅ أحسنت!</div>

<!-- XP Bar -->
<div class="xp-bar-container" id="xpBar" style="display:none">
    <span class="xp-label">⭐ نقاط البطل</span>
    <div class="xp-track"><div class="xp-fill" id="xpFill" style="width:0%"></div></div>
    <span class="xp-label" id="xpNum">0 / 100</span>
</div>

<!-- Records Button -->
<button class="records-btn" onclick="showRecords()">📜 سجل الأبطال</button>

<!-- ========== HOME SCREEN ========== -->
<div class="screen active" id="home">
    <div class="game-title">مغامرة الرياضيات ✨</div>
    <p class="subtitle">الصف الخامس الابتدائي - الفصل الدراسي الأول 📚</p>
    <div class="hero-character">🧑‍🎓</div>
    <p style="color:rgba(255,255,255,0.7); margin-top:10px">اكتشف 8 جزر و 48 درساً واجمع النجوم!</p>

    <div id="registerForm" style="width:100%;max-width:380px;margin-top:20px">
        <input id="usernameInput" type="text" placeholder="✏️ اكتب اسمك هنا..." maxlength="20"
               style="width:100%;padding:15px 20px;border-radius:30px;border:2px solid rgba(255,255,255,0.3);
               background:rgba(255,255,255,0.1);color:white;font-size:1.1rem;text-align:center;margin-bottom:15px;"
               onkeydown="if(event.key==='Enter')registerAndStart()">
        <div id="inputError" style="color:#f94144;font-size:0.9rem;margin-bottom:10px;display:none">⚠️ من فضلك اكتب اسمك أولاً</div>
        <button class="start-btn" onclick="registerAndStart()">🗺️ ابدأ الرحلة!</button>
    </div>

    <div id="welcomeBack" style="display:none;margin-top:20px;text-align:center">
        <div id="welcomeName" style="font-size:1.5rem;font-weight:900;color:var(--gold);margin-bottom:15px"></div>
        <button class="start-btn" onclick="showMap()">🗺️ استمر في الرحلة!</button>
        <br>
        <button onclick="resetUser()" style="margin-top:12px;background:transparent;border:1px solid rgba(255,255,255,0.3);color:rgba(255,255,255,0.6);padding:8px 20px;border-radius:20px;cursor:pointer;">
            🔄 لاعب جديد
        </button>
    </div>
</div>

<!-- ========== MAP SCREEN ========== -->
<div class="screen" id="map">
    <h2 class="map-title">🗺️ جزر الرياضيات</h2>
    <div class="islands-container" id="islandsContainer"></div>
</div>

<!-- ========== LESSONS SCREEN ========== -->
<div class="screen" id="lessons">
    <button class="back-btn" onclick="showMap()">🗺️ الخريطة</button>
    <h2 class="map-title" id="lessonIslandTitle">مهام الجزيرة</h2>
    <div class="lessons-grid" id="lessonsGrid"></div>
</div>

<!-- ========== ACTIVITY SCREEN ========== -->
<div class="screen" id="activity">
    <button class="back-btn" onclick="safeBackToLessons()">◀ رجوع</button>
    <div class="activity-box" id="activityContent"></div>
</div>

<!-- ========== SUCCESS SCREEN ========== -->
<div class="screen" id="success">
    <div class="success-emoji" id="successEmoji">🏆</div>
    <div class="success-title" id="successTitle">أحسنت يا بطل!</div>
    <div class="success-stars" id="earnedStars">⭐⭐⭐</div>
    <p id="successMsg" style="color:rgba(255,255,255,0.8); font-size:1.2rem; margin:15px 0">لقد أتممت المهمة وكسبت نقاط!</p>
    <div style="display:flex;gap:15px;justify-content:center;flex-wrap:wrap;margin-top:10px">
        <button class="action-btn" onclick="retryCurrentLesson()">🔄 أعد التحدي</button>
        <button class="action-btn gold" onclick="goToNextLesson()">التالي ◀</button>
    </div>
    <p style="color:var(--mint); margin-top:20px; font-size:0.9rem;" id="autoMsg">سيتم الانتقال تلقائياً بعد 3 ثوانٍ...</p>
</div>

<!-- ========== ASSESSMENT SCREEN ========== -->
<div class="screen" id="assessment">
    <div class="assessment-icon" id="assessmentIcon">🏝️</div>
    <div class="assessment-title" id="assessmentTitle">تقييم الجزيرة</div>
    <div class="assessment-detail" id="assessmentDetail">لقد أكملت 5 من 5 دروس</div>
    <div class="assessment-stars" id="assessmentStars">⭐⭐⭐</div>
    <p id="assessmentScore" style="color:white; font-size:1.3rem;">إجمالي النقاط: 150</p>
    <p id="assessmentTime" style="color:var(--mint); font-size:1.1rem;"></p>
    <button class="action-btn gold assessment-next-btn" id="assessmentNextBtn">التالي</button>
    <p style="color:var(--mint); margin-top:20px; font-size:0.9rem;" id="assessmentAutoMsg">سيتم الانتقال تلقائياً بعد 4 ثوانٍ...</p>
</div>

<!-- ========== RECORDS SCREEN ========== -->
<div class="screen" id="records">
    <button class="back-btn" onclick="showScreen('home')">🏠 الرئيسية</button>
    <h2 class="map-title">📜 سجل الأبطال</h2>
    <table class="records-table" id="recordsTable">
        <thead>
            <tr><th>الاسم</th><th>التاريخ</th><th>الوقت</th><th>النقاط</th><th>المستوى</th></tr>
        </thead>
        <tbody id="recordsBody"></tbody>
    </table>
    <button class="action-btn" onclick="clearRecords()" style="margin-top:20px;background:#f94144;">🗑️ مسح السجل</button>
</div>

<script>
    // ===== 1. الخلفية النجمية =====
    (function createStars() {
        const container = document.getElementById('starsContainer');
        for (let i = 0; i < 100; i++) {
            const star = document.createElement('div');
            star.className = 'star';
            const size = Math.random() * 3 + 1;
            star.style.cssText = `
                left:${Math.random()*100}%;
                top:${Math.random()*100}%;
                width:${size}px; height:${size}px;
                --d:${Math.random()*3+2}s;
                animation-delay:${Math.random()*3}s;
            `;
            container.appendChild(star);
        }
    })();

    // ===== 2. حالة اللعبة (مع مؤقت) =====
    let gameState = {
        xp: 0,
        completedLessons: [],
        currentIsland: 0,
        currentLesson: null,
        currentUser: null,
        level: 1,
        totalLessonsCount: 0,
        startTime: null,      // وقت بدء الجلسة (timestamp)
        elapsedTime: 0,        // الوقت الإجمالي بالثواني (بدون الجلسة الحالية)
        sessionStart: null     // وقت بدء الجلسة الحالية (لحساب الوقت المستمر)
    };

    // ===== 3. سجل المحاولات =====
    let records = [];

    // ===== 4. تحميل الحالة والسجلات =====
    try {
        const saved = localStorage.getItem('math_hero_state_v5');
        if (saved) gameState = { ...gameState, ...JSON.parse(saved) };
        const savedRecords = localStorage.getItem('math_hero_records_v5');
        if (savedRecords) records = JSON.parse(savedRecords);
    } catch (e) {}

    // حساب إجمالي الدروس (يتم تعيينه بعد تعريف الجزر)
    // سيتم حسابه لاحقاً

    // ===== 5. دوال إدارة الوقت =====
    function startTimer() {
        if (!gameState.startTime) {
            gameState.startTime = Date.now();
            gameState.sessionStart = Date.now();
        } else {
            gameState.sessionStart = Date.now();
        }
        saveState();
    }

    function pauseTimer() {
        if (gameState.sessionStart) {
            const now = Date.now();
            const diff = Math.floor((now - gameState.sessionStart) / 1000);
            gameState.elapsedTime += diff;
            gameState.sessionStart = null;
            saveState();
        }
    }

    function getTotalTime() {
        let total = gameState.elapsedTime;
        if (gameState.sessionStart) {
            total += Math.floor((Date.now() - gameState.sessionStart) / 1000);
        }
        return total;
    }

    function formatTime(seconds) {
        const mins = Math.floor(seconds / 60);
        const secs = seconds % 60;
        return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
    }

    // ===== 6. حفظ الحالة والسجلات =====
    function saveState() {
        try { localStorage.setItem('math_hero_state_v5', JSON.stringify(gameState)); } catch (e) {}
    }
    function saveRecords() {
        try { localStorage.setItem('math_hero_records_v5', JSON.stringify(records)); } catch (e) {}
    }

    // ===== 7. بيانات الجزر (8 وحدات، ~48 درساً) =====
    const islands = [
        { // الوحدة 1: القيمة المكانية
            title: "🏝️ جزيرة القيمة المكانية", c1: "#f39c12", c2: "#e67e22", emoji: "🔢",
            lessons: [
                { emoji:"1️⃣", title:"الأعداد الكبيرة", type:"مكانية", activity:"u1l1" },
                { emoji:"2️⃣", title:"تغيير القيم المكانية", type:"مكانية", activity:"u1l2" },
                { emoji:"3️⃣", title:"صيغ متنوعة لكتابة الأعداد", type:"مكانية", activity:"u1l3" },
                { emoji:"4️⃣", title:"تكوين الأعداد وتحليلها", type:"مكانية", activity:"u1l4" },
                { emoji:"5️⃣", title:"مقارنة الأعداد الكبيرة", type:"مكانية", activity:"u1l5" },
                { emoji:"6️⃣", title:"مقارنة الأعداد في صيغ مختلفة", type:"مكانية", activity:"u1l6" },
                { emoji:"7️⃣", title:"ترتيب الأعداد تنازليًا وتصاعديًا", type:"مكانية", activity:"u1l7" },
                { emoji:"8️⃣", title:"قواعد التقريب", type:"مكانية", activity:"u1l8" }
            ]
        },
        { // الوحدة 2: استراتيجيات الجمع والطرح
            title: "🏝️ جزيرة الجمع والطرح", c1: "#3498db", c2: "#2980b9", emoji: "➕➖",
            lessons: [
                { emoji:"🧮", title:"خواص عملية الجمع", type:"جمع", activity:"u2l1" },
                { emoji:"🔁", title:"الجمع مع إعادة التسمية", type:"جمع", activity:"u2l2" },
                { emoji:"↩️", title:"الطرح مع إعادة التسمية", type:"طرح", activity:"u2l3" },
                { emoji:"📊", title:"النماذج الشريطية والمتغيرات", type:"جمع/طرح", activity:"u2l4" },
                { emoji:"📝", title:"مسائل كلامية متعددة الخطوات", type:"مسائل", activity:"u2l5" }
            ]
        },
        { // الوحدة 3: مفاهيم القياس
            title: "🏝️ جزيرة القياس", c1: "#2ecc71", c2: "#27ae60", emoji: "📏⏱️",
            lessons: [
                { emoji:"📏", title:"قياس الطول", type:"طول", activity:"u3l1" },
                { emoji:"⚖️", title:"قياس الكتلة", type:"كتلة", activity:"u3l2" },
                { emoji:"🧪", title:"وحدات قياس السعة", type:"سعة", activity:"u3l3" },
                { emoji:"⏰", title:"وحدات قياس الوقت", type:"وقت", activity:"u3l4" },
                { emoji:"⌛", title:"الوقت المنقضي", type:"وقت", activity:"u3l5" },
                { emoji:"📐", title:"تطبيقات القياس 1", type:"قياس", activity:"u3l6" },
                { emoji:"📏✏️", title:"تطبيقات القياس 2", type:"قياس", activity:"u3l7" }
            ]
        },
        { // الوحدة 4: المساحة والمحيط
            title: "🏝️ جزيرة المساحة والمحيط", c1: "#e74c3c", c2: "#c0392b", emoji: "📐🔲",
            lessons: [
                { emoji:"🔄", title:"إيجاد المحيط", type:"محيط", activity:"u4l1" },
                { emoji:"🔲", title:"إيجاد المساحة", type:"مساحة", activity:"u4l2" },
                { emoji:"❓", title:"أبعاد مجهولة", type:"هندسة", activity:"u4l3" },
                { emoji:"🏛️", title:"الأشكال الهندسية المركبة", type:"هندسة", activity:"u4l4" }
            ]
        },
        { // الوحدة 5: الضرب كعلاقة
            title: "🏝️ جزيرة الضرب كعلاقة", c1: "#9b59b6", c2: "#8e44ad", emoji: "✖️🔗",
            lessons: [
                { emoji:"🔢", title:"مقارنة الأعداد باستخدام الضرب", type:"ضرب", activity:"u5l1" },
                { emoji:"⚖️", title:"تكوين معادلات للمقارنة", type:"ضرب", activity:"u5l2" },
                { emoji:"🧮", title:"حل معادلات للمقارنة", type:"ضرب", activity:"u5l3" },
                { emoji:"🔄", title:"خاصية الإبدال", type:"خواص", activity:"u5l4" },
                { emoji:"1️⃣", title:"العنصر المحايد والضرب في صفر", type:"خواص", activity:"u5l5" },
                { emoji:"🤝", title:"خاصية الدمج", type:"خواص", activity:"u5l6" },
                { emoji:"📈", title:"تطبيق الأنماط في الضرب", type:"أنماط", activity:"u5l7" }
            ]
        },
        { // الوحدة 6: العوامل والمضاعفات
            title: "🏝️ جزيرة العوامل والمضاعفات", c1: "#1abc9c", c2: "#16a085", emoji: "🔢✖️",
            lessons: [
                { emoji:"🔍", title:"تحديد عوامل الأعداد الصحيحة", type:"عوامل", activity:"u6l1" },
                { emoji:"🥇", title:"الأعداد الأولية ومتعددة العوامل", type:"عوامل", activity:"u6l2" },
                { emoji:"📏", title:"العامل المشترك الأكبر (ع.م.أ)", type:"عوامل", activity:"u6l3" },
                { emoji:"🔁", title:"تحديد مضاعفات الأعداد الصحيحة", type:"مضاعفات", activity:"u6l4" },
                { emoji:"🤝", title:"المضاعفات المشتركة", type:"مضاعفات", activity:"u6l5" },
                { emoji:"🔄", title:"العلاقات بين العوامل والمضاعفات", type:"علاقات", activity:"u6l6" }
            ]
        },
        { // الوحدة 7: عمليتا الضرب والقسمة
            title: "🏝️ جزيرة الضرب والقسمة", c1: "#e67e22", c2: "#d35400", emoji: "➗✖️",
            lessons: [
                { emoji:"📐", title:"نموذج مساحة المستطيل (الضرب)", type:"ضرب", activity:"u7l1" },
                { emoji:"📦", title:"خاصية التوزيع", type:"ضرب", activity:"u7l2" },
                { emoji:"🔨", title:"خوارزمية الضرب بالتجزئة", type:"ضرب", activity:"u7l3" },
                { emoji:"1️⃣", title:"الضرب في عدد مكون من رقم واحد", type:"ضرب", activity:"u7l4" },
                { emoji:"🔟", title:"ضرب عدد مكون من رقمين في مضاعفات 10", type:"ضرب", activity:"u7l5" },
                { emoji:"🔄", title:"استكشاف باقي القسمة", type:"قسمة", activity:"u7l6" },
                { emoji:"📊", title:"الأنماط في القسمة", type:"قسمة", activity:"u7l7" },
                { emoji:"📐", title:"القسمة باستخدام نموذج مساحة المستطيل", type:"قسمة", activity:"u7l8" },
                { emoji:"🧩", title:"خوارزمية خارج القسمة بالتجزئة", type:"قسمة", activity:"u7l9" },
                { emoji:"📏", title:"خوارزمية القسمة المعيارية", type:"قسمة", activity:"u7l10" },
                { emoji:"🔄", title:"القسمة والضرب", type:"علاقة", activity:"u7l11" }
            ]
        },
        { // الوحدة 8: ترتيب العمليات
            title: "🏝️ جزيرة ترتيب العمليات", c1: "#f1c40f", c2: "#f39c12", emoji: "⚖️🔢",
            lessons: [
                { emoji:"🧮", title:"ترتيب إجراء العمليات الحسابية", type:"ترتيب", activity:"u8l1" },
                { emoji:"📝", title:"ترتيب العمليات والمسائل الكلامية", type:"مسائل", activity:"u8l2" }
            ]
        }
    ];

    // تعيين totalLessonsCount
    gameState.totalLessonsCount = islands.reduce((acc, island) => acc + island.lessons.length, 0);

    // ===== 8. بنوك الأسئلة لكل درس (مصغرة هنا - في النسخة الكاملة ستكون أكبر) =====
    const activities = {
        // الوحدة 1 - نموذج
        u1l1: [
            { q: "ما قيمة الرقم ٥ في العدد ٥٦٧٨٢؟", opts: ["٥٠٠٠٠", "٥٠٠٠", "٥٠٠", "٥"], ans: 0 },
            { q: "ما قيمة الرقم ٣ في العدد ٣٤٥٦٧؟", opts: ["٣٠٠٠٠", "٣٠٠٠", "٣٠٠", "٣"], ans: 0 },
            { q: "في العدد ٨٢٣٤٥، ما قيمة الرقم ٢؟", opts: ["٢٠٠٠", "٢٠٠", "٢٠٠٠٠", "٢"], ans: 0 },
            { q: "في العدد ٩٠٧٠٦، ما قيمة الرقم ٧؟", opts: ["٧٠٠", "٧٠٠٠", "٧٠", "٧"], ans: 0 },
            { q: "الرقم ٤ في العدد ٤٥٠٠٠٠ يمثل:", opts: ["٤٠٠٠٠٠", "٤٠٠٠٠", "٤٠٠٠", "٤٠٠"], ans: 0 }
        ],
        u1l2: [
            { q: "إذا غيرنا الرقم ٣ في العدد ٣٢٤ إلى ٨، فكم يصبح العدد الجديد؟", opts: ["٨٢٤", "٣٨٤", "٣٢٨", "٨٤٢"], ans: 0 },
            { q: "إذا غيرنا الرقم ٥ في العدد ٥٧٩ إلى ٢، فما العدد الجديد؟", opts: ["٢٧٩", "٥٢٩", "٥٧٢", "٢٩٧"], ans: 0 }
        ],
        // باقي الدروس ستضاف بنفس الطريقة
    };

    // ===== 9. دوال خلط واختيار عشوائي =====
    function shuffleArray(arr) {
        for (let i = arr.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        return arr;
    }

    function selectRandomQuestions(questionBank, count = 5) {
        if (!questionBank || questionBank.length === 0) return [];
        const shuffled = shuffleArray([...questionBank]);
        return shuffled.slice(0, Math.min(count, shuffled.length));
    }

    function shuffleOptions(question) {
        const options = [...question.opts];
        const correctIndex = question.ans;
        const correctText = options[correctIndex];
        const shuffled = shuffleArray(options);
        const newCorrectIndex = shuffled.indexOf(correctText);
        return { q: question.q, opts: shuffled, ans: newCorrectIndex };
    }

    // ===== 10. دوال العرض الأساسية =====
    function showScreen(id) {
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        document.getElementById('xpBar').style.display = id === 'home' ? 'none' : 'flex';
        if (id !== 'home' && gameState.currentUser) {
            document.querySelector('.xp-label').textContent = '⭐ ' + gameState.currentUser;
        }
        window.scrollTo(0, 0);
    }
    window.showScreen = showScreen;

    // ===== 11. دوال التسجيل وإدارة المستخدم =====
    window.registerAndStart = function() {
        const input = document.getElementById('usernameInput');
        const errEl = document.getElementById('inputError');
        const username = input ? input.value.trim() : '';
        if (!username) {
            if (errEl) errEl.style.display = 'block';
            if (input) input.focus();
            return;
        }
        if (errEl) errEl.style.display = 'none';
        gameState.currentUser = username;
        startTimer(); // بدء المؤقت
        try { localStorage.setItem('mathGameUser_v5', username); } catch (e) {}
        saveState();
        showMap();
    };

    window.resetUser = function() {
        pauseTimer();
        try { localStorage.removeItem('mathGameUser_v5'); } catch (e) {}
        gameState = {
            xp: 0, completedLessons: [], currentIsland: 0, currentLesson: null,
            currentUser: null, level: 1, totalLessonsCount: gameState.totalLessonsCount,
            startTime: null, elapsedTime: 0, sessionStart: null
        };
        document.getElementById('welcomeBack').style.display = 'none';
        document.getElementById('registerForm').style.display = 'block';
        document.getElementById('usernameInput').value = '';
        updateXPBar();
        renderIslands();
        showScreen('home');
        saveState();
    };

    // ===== 12. دوال الخريطة والدروس =====
    function showMap() {
        if (!gameState.currentUser) {
            showNotif('✏️ سجل اسمك أولاً!', false);
            showScreen('home');
            return;
        }
        renderIslands();
        showScreen('map');
    }
    window.showMap = showMap;

    function renderIslands() {
        const container = document.getElementById('islandsContainer');
        container.innerHTML = islands.map((island, idx) => {
            const locked = idx > 0 && !isIslandUnlocked(idx - 1);
            const completedCount = island.lessons.filter((_, i) => gameState.completedLessons.includes(idx + '-' + i)).length;
            const pct = (completedCount / island.lessons.length) * 100;
            const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';
            return `
                <div class="island-card ${locked ? 'locked' : ''}" style="--c1:${island.c1};--c2:${island.c2}" onclick="${!locked ? `showLessons(${idx})` : ''}">
                    ${locked ? '<span class="lock-badge">🔒</span>' : ''}
                    <span class="island-emoji">${island.emoji}</span>
                    <div class="island-name">${island.title}</div>
                    <div class="island-desc">${island.lessons.length} دروس</div>
                    <div class="island-stars">${stars}</div>
                    <div class="island-progress"><div class="island-progress-fill" style="width:${pct}%"></div></div>
                </div>
            `;
        }).join('');
    }

    function showLessons(islandIdx) {
        const island = islands[islandIdx];
        if (islandIdx >= 1 && !isIslandUnlocked(islandIdx - 1)) {
            showNotif('🔒 أكمل الجزيرة السابقة أولاً!', false);
            return;
        }
        gameState.currentIsland = islandIdx;
        document.getElementById('lessonIslandTitle').textContent = island.title;
        const grid = document.getElementById('lessonsGrid');
        grid.innerHTML = island.lessons.map((lesson, i) => {
            const lessonId = islandIdx + '-' + i;
            const done = gameState.completedLessons.includes(lessonId);
            return '<div class="lesson-card ' + (done ? 'done' : '') + '" onclick="startLesson(' + islandIdx + ', ' + i + ')">'
                + '<div class="lesson-emoji">' + lesson.emoji + '</div>'
                + '<div class="lesson-title">' + lesson.title + '</div>'
                + '<div class="lesson-type">' + lesson.type + '</div>'
                + (done ? '<div style="color:#52b788;font-size:0.9rem;margin-top:8px">✅ مكتمل</div>' : '')
                + '</div>';
        }).join('');
        showScreen('lessons');
    }
    window.showLessons = showLessons;

    // ===== 13. دوال الأنشطة والأسئلة =====
    function startLesson(islandIdx, lessonIdx) {
        const lesson = islands[islandIdx].lessons[lessonIdx];
        gameState.currentLesson = islandIdx + '-' + lessonIdx;
        window._activityStarted = true;
        window._activityDone = false;
        document.getElementById('activityContent').innerHTML = renderQuiz(lesson.activity);
        showScreen('activity');
    }
    window.startLesson = startLesson;

    function renderQuiz(lessonId) {
        const questionBank = activities[lessonId];
        if (!questionBank || questionBank.length === 0) {
            return `
                <div class="activity-type-badge">🧮 نشاط</div>
                <div class="activity-title">نشاط تفاعلي</div>
                <div class="activity-instruction">هذا النشاط قيد التطوير، اضغط "أكملت" للمتابعة.</div>
                <button class="action-btn gold" onclick="completeActivity(50)">✅ أكملت</button>
            `;
        }
        const selected = selectRandomQuestions(questionBank, 5);
        const shuffledQuestions = selected.map(q => shuffleOptions(q));
        let current = 0;
        let score = 0;
        const questions = shuffledQuestions;

        function renderQ() {
            const q = questions[current];
            return `
                <div class="activity-type-badge">🧮 اختبار سريع</div>
                <div style="text-align:center;margin-bottom:10px;color:rgba(255,255,255,0.6)">${current + 1} / ${questions.length}</div>
                <div class="activity-title" style="font-size:1.5rem;">${q.q}</div>
                <div class="quiz-options" id="opts">
                    ${q.opts.map((o, i) => `<button class="quiz-option" onclick="window.handleAnswer(${i}, '${lessonId}')">${o}</button>`).join('')}
                </div>
            `;
        }

        window.handleAnswer = function(idx, lid) {
            if (lid !== lessonId) return;
            const q = questions[current];
            const btns = document.querySelectorAll('.quiz-option');
            btns.forEach(b => b.disabled = true);
            if (idx === q.ans) {
                btns[idx].classList.add('correct');
                score++;
                showNotif('✅ إجابة صحيحة!');
            } else {
                btns[idx].classList.add('wrong');
                btns[q.ans].classList.add('correct');
                showNotif('❌ خطأ، حاول مرة أخرى', false);
            }
            current++;
            setTimeout(() => {
                if (current < questions.length) {
                    document.getElementById('activityContent').innerHTML = renderQ();
                } else {
                    completeActivity(score * 15);
                }
            }, 1200);
        };
        return renderQ();
    }

    function completeActivity(xpGain) {
        window._activityDone = true;
        const lessonId = gameState.currentLesson;
        const isFirstTime = !gameState.completedLessons.includes(lessonId);
        if (isFirstTime) {
            gameState.completedLessons.push(lessonId);
            gameState.xp = parseInt(gameState.xp || 0) + parseInt(xpGain || 0);
            const newLevel = Math.floor(gameState.xp / 100) + 1;
            if (newLevel > (gameState.level || 1)) {
                gameState.level = newLevel;
                setTimeout(() => showNotif('🎉 وصلت المستوى ' + newLevel + '!'), 2000);
            }
        }
        saveState();
        updateXPBar();
        renderIslands();
        showSuccess(xpGain, isFirstTime);
    }
    window.completeActivity = completeActivity;

    function showSuccess(xp, isFirstTime = true) {
        const stars = xp >= 60 ? '⭐⭐⭐' : xp >= 30 ? '⭐⭐' : '⭐';
        document.getElementById('earnedStars').textContent = isFirstTime ? stars : '✅';
        document.getElementById('successTitle').textContent = isFirstTime ? 'أحسنت يا بطل! 🎉' : 'درس مكتمل!';
        document.getElementById('successMsg').textContent = isFirstTime
            ? 'كسبت ' + xp + ' نقطة! استمر!'
            : 'سبق إكمال هذا الدرس. لا تُضاف نقاط عند المراجعة.';
        document.getElementById('successEmoji').textContent = isFirstTime ? '🏆' : '📚';
        document.getElementById('autoMsg').style.display = 'block';
        showScreen('success');
        if (isFirstTime) launchFireworks();
        clearTimeout(window.successTimeout);
        window.successTimeout = setTimeout(goToNextLesson, 3000);
    }

    window.goToNextLesson = function() {
        if (!gameState.currentLesson) return;
        const [islandIdx, lessonIdx] = gameState.currentLesson.split('-').map(Number);
        const island = islands[islandIdx];
        if (lessonIdx + 1 < island.lessons.length) {
            startLesson(islandIdx, lessonIdx + 1);
        } else {
            showIslandAssessment(islandIdx);
        }
    };
    window.retryCurrentLesson = function() {
        if (!gameState.currentLesson) { showScreen('lessons'); return; }
        const parts = gameState.currentLesson.split('-').map(Number);
        startLesson(parts[0], parts[1]);
    };
    window.safeBackToLessons = function() {
        if (window._activityStarted && !window._activityDone) {
            if (!confirm('لم تكمل النشاط بعد. هل تريد الخروج؟')) return;
        }
        window._activityStarted = false;
        window._activityDone = false;
        showScreen('lessons');
    };

    // ===== 14. دوال التقييم =====
    function showIslandAssessment(islandIdx) {
        const island = islands[islandIdx];
        const completedCount = island.lessons.filter((_, i) => gameState.completedLessons.includes(islandIdx + '-' + i)).length;
        const total = island.lessons.length;
        const earnedPoints = Math.min(completedCount * 75, gameState.xp);
        const pct = (completedCount / total) * 100;
        const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';

        document.getElementById('assessmentIcon').textContent = island.emoji;
        document.getElementById('assessmentTitle').textContent = `تقييم ${island.title}`;
        document.getElementById('assessmentDetail').textContent = `لقد أكملت ${completedCount} من ${total} دروس`;
        document.getElementById('assessmentStars').textContent = stars;
        document.getElementById('assessmentScore').textContent = `إجمالي النقاط في هذه الجزيرة: ~${earnedPoints}`;
        document.getElementById('assessmentTime').textContent = `الوقت حتى الآن: ${formatTime(getTotalTime())}`;

        const nextBtn = document.getElementById('assessmentNextBtn');
        const autoMsg = document.getElementById('assessmentAutoMsg');

        if (islandIdx === islands.length - 1) {
            nextBtn.onclick = showFinalAssessment;
            autoMsg.textContent = 'سيتم الانتقال إلى التقييم النهائي بعد 4 ثوانٍ...';
        } else {
            nextBtn.onclick = function() {
                gameState.currentIsland = islandIdx + 1;
                showLessons(islandIdx + 1);
            };
            autoMsg.textContent = 'سيتم الانتقال إلى الجزيرة التالية بعد 4 ثوانٍ...';
        }
        showScreen('assessment');

        clearTimeout(window.assessmentTimeout);
        window.assessmentTimeout = setTimeout(() => {
            if (islandIdx === islands.length - 1) {
                showFinalAssessment();
            } else {
                gameState.currentIsland = islandIdx + 1;
                showLessons(islandIdx + 1);
            }
        }, 4000);
    }

    function showFinalAssessment() {
        pauseTimer(); // إيقاف المؤقت
        const totalTime = getTotalTime();
        const totalCompleted = gameState.completedLessons.length;
        const total = gameState.totalLessonsCount;
        const totalXP = gameState.xp;
        const level = gameState.level;
        const pct = (totalCompleted / total) * 100;
        const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';

        // مكافأة زمنية
        let timeBonus = 0;
        if (totalTime < 1800) timeBonus = 100;
        else if (totalTime < 3600) timeBonus = 50;
        else timeBonus = 10;

        const finalXP = totalXP + timeBonus;

        // تسجيل المحاولة
        const record = {
            name: gameState.currentUser,
            date: new Date().toLocaleString('ar-EG'),
            time: formatTime(totalTime),
            points: finalXP,
            level: level
        };
        records.push(record);
        saveRecords();

        document.getElementById('assessmentIcon').textContent = '🏆';
        document.getElementById('assessmentTitle').textContent = 'تهانينا! لقد أكملت المغامرة';
        document.getElementById('assessmentDetail').textContent = `لقد أكملت ${totalCompleted} من ${total} درس`;
        document.getElementById('assessmentStars').textContent = stars;
        document.getElementById('assessmentScore').textContent = `إجمالي نقاطك: ${finalXP} (مع مكافأة السرعة: +${timeBonus}) - المستوى: ${level}`;
        document.getElementById('assessmentTime').textContent = `الزمن المستغرق: ${formatTime(totalTime)}`;
        document.getElementById('assessmentNextBtn').textContent = '🎮 العب مجدداً';
        document.getElementById('assessmentNextBtn').onclick = resetUser;
        document.getElementById('assessmentAutoMsg').textContent = 'شكراً لك على اللعب!';
        showScreen('assessment');
        launchFireworks();
    }

    // ===== 15. دوال السجلات =====
    window.showRecords = function() {
        const tbody = document.getElementById('recordsBody');
        tbody.innerHTML = '';
        if (records.length === 0) {
            tbody.innerHTML = '<tr><td colspan="5" style="text-align:center;">لا توجد محاولات بعد</td></tr>';
        } else {
            [...records].reverse().slice(0, 10).forEach(rec => {
                tbody.innerHTML += `<tr><td>${rec.name}</td><td>${rec.date}</td><td>${rec.time}</td><td>${rec.points}</td><td>${rec.level}</td></tr>`;
            });
        }
        showScreen('records');
    };

    window.clearRecords = function() {
        if (confirm('هل أنت متأكد من مسح جميع السجلات؟')) {
            records = [];
            saveRecords();
            showRecords();
        }
    };

    // ===== 16. دوال مساعدة =====
    function isIslandUnlocked(islandIdx) {
        const island = islands[islandIdx];
        const completed = island.lessons.filter((_, i) => gameState.completedLessons.includes(islandIdx + '-' + i)).length;
        return completed >= Math.ceil(island.lessons.length * 0.6);
    }

    function updateXPBar() {
        const xp = parseInt(gameState.xp || 0);
        const level = Math.floor(xp / 100) + 1;
        gameState.level = level;
        const xpInLevel = xp % 100;
        document.getElementById('xpFill').style.width = xpInLevel + '%';
        document.getElementById('xpNum').textContent = 'مستوى ' + level + ' (' + xpInLevel + '/100)';
    }

    let notifTimeout;
    function showNotif(msg, good = true) {
        const el = document.getElementById('notification');
        el.textContent = msg;
        el.style.background = good
            ? 'linear-gradient(135deg, #52b788, #2d6a4f)'
            : 'linear-gradient(135deg, #f94144, #9d0208)';
        el.classList.add('show');
        clearTimeout(notifTimeout);
        notifTimeout = setTimeout(() => el.classList.remove('show'), 1800);
    }

    function launchFireworks() {
        const colors = ['#ffd60a', '#f9c74f', '#90e0ef', '#f94144', '#52b788'];
        for (let i = 0; i < 30; i++) {
            setTimeout(() => {
                const fw = document.createElement('div');
                fw.className = 'firework';
                fw.style.cssText = `
                    left:${Math.random() * 100}vw;
                    top:${Math.random() * 60 + 10}vh;
                    background:${colors[Math.floor(Math.random() * colors.length)]};
                    --tx:${(Math.random() - 0.5) * 200}px;
                    --ty:${(Math.random() - 0.5) * 200}px;
                    animation-delay:${Math.random() * 0.5}s;
                `;
                document.body.appendChild(fw);
                setTimeout(() => fw.remove(), 1200);
            }, i * 60);
        }
    }

    // ===== 17. تحميل البيانات عند بدء التشغيل =====
    window.onload = function() {
        updateXPBar();
        renderIslands();
        try {
            const savedUser = localStorage.getItem('mathGameUser_v5');
            if (savedUser && savedUser.trim()) {
                gameState.currentUser = savedUser;
                document.getElementById('registerForm').style.display = 'none';
                document.getElementById('welcomeBack').style.display = 'block';
                document.getElementById('welcomeName').textContent = '👋 أهلاً يا ' + savedUser + '!';
                if (gameState.startTime) {
                    gameState.sessionStart = Date.now(); // استئناف المؤقت
                }
            }
        } catch (e) {}
    };

    // حفظ الوقت عند إغلاق الصفحة
    window.addEventListener('beforeunload', function() {
        pauseTimer();
    });
</script>

</body>
</html>
