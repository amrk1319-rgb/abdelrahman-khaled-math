<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مغامرة الرياضيات - الصف الأول الإعدادي (الترم الثاني) 📐</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        /* جميع الأنماط السابقة - نفس التنسيق مع تحسينات بسيطة */
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
    <p class="subtitle">الصف الأول الإعدادي - الفصل الدراسي الثاني 📚</p>
    <div class="hero-character">🧑‍🎓</div>
    <p style="color:rgba(255,255,255,0.7); margin-top:10px">اكتشف قوانين الأسس والجذور والمعادلات!</p>

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
    <h2 class="map-title">🗺️ جزر الرياضيات - الترم الثاني</h2>
    <div class="islands-container" id="islandsContainer"></div>
</div>

<!-- ========== LESSONS SCREEN ========== -->
<div class="screen" id="lessons">
    <button class="back-btn" onclick="showMap()">🗺️ الخريطة</button>
    <h2 class="map-title" id="lessonIslandTitle">دروس الجزيرة</h2>
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
        startTime: null,
        elapsedTime: 0,
        sessionStart: null
    };

    // ===== 3. سجل المحاولات =====
    let records = [];

    // ===== 4. تحميل الحالة والسجلات =====
    try {
        const saved = localStorage.getItem('math_prep1_term2_state');
        if (saved) gameState = { ...gameState, ...JSON.parse(saved) };
        const savedRecords = localStorage.getItem('math_prep1_term2_records');
        if (savedRecords) records = JSON.parse(savedRecords);
    } catch (e) {}

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
        try { localStorage.setItem('math_prep1_term2_state', JSON.stringify(gameState)); } catch (e) {}
    }
    function saveRecords() {
        try { localStorage.setItem('math_prep1_term2_records', JSON.stringify(records)); } catch (e) {}
    }

    // ===== 7. بيانات الجزر (وحدات الترم الثاني - الصف الأول الإعدادي) =====
    const islands = [
        { // الوحدة 1: الأسس والجذور التربيعية
            title: "🏝️ جزيرة الأسس والجذور", c1: "#f39c12", c2: "#e67e22", emoji: "🔢",
            lessons: [
                { emoji:"📐", title:"مفهوم الأسس", type:"أسس", activity:"u1l1" },
                { emoji:"✖️", title:"قوانين الأسس (الضرب)", type:"أسس", activity:"u1l2" },
                { emoji:"➗", title:"قوانين الأسس (القسمة)", type:"أسس", activity:"u1l3" },
                { emoji:"🔢", title:"الأسس السالبة والصفر", type:"أسس", activity:"u1l4" },
                { emoji:"√", title:"الجذر التربيعي", type:"جذور", activity:"u1l5" },
                { emoji:"∛", title:"الجذر التكعيبي", type:"جذور", activity:"u1l6" },
                { emoji:"📏", title:"تطبيقات على الأسس والجذور", type:"تطبيقات", activity:"u1l7" }
            ]
        },
        { // الوحدة 2: الصيغ والتحليل
            title: "🏝️ جزيرة الصيغ والتحليل", c1: "#3498db", c2: "#2980b9", emoji: "📝",
            lessons: [
                { emoji:"📐", title:"صيغ الضرب المختصر (مربع مجموع)", type:"صيغ", activity:"u2l1" },
                { emoji:"📏", title:"صيغ الضرب المختصر (مربع فرق)", type:"صيغ", activity:"u2l2" },
                { emoji:"➗", title:"الفرق بين مربعين", type:"صيغ", activity:"u2l3" },
                { emoji:"🔍", title:"تحليل المقدار الثلاثي (بسيط)", type:"تحليل", activity:"u2l4" },
                { emoji:"🧩", title:"تحليل المقدار الثلاثي (مع معامل)", type:"تحليل", activity:"u2l5" },
                { emoji:"🔄", title:"التحليل بإخراج العامل المشترك", type:"تحليل", activity:"u2l6" },
                { emoji:"📊", title:"تطبيقات على التحليل", type:"تطبيقات", activity:"u2l7" }
            ]
        },
        { // الوحدة 3: العمليات على الأعداد الحقيقية
            title: "🏝️ جزيرة العمليات", c1: "#2ecc71", c2: "#27ae60", emoji: "🧮",
            lessons: [
                { emoji:"➕", title:"جمع وطرح الأعداد الحقيقية", type:"عمليات", activity:"u3l1" },
                { emoji:"✖️", title:"ضرب الأعداد الحقيقية", type:"عمليات", activity:"u3l2" },
                { emoji:"➗", title:"قسمة الأعداد الحقيقية", type:"عمليات", activity:"u3l3" },
                { emoji:"🔢", title:"الترتيب والعمليات", type:"عمليات", activity:"u3l4" },
                { emoji:"📐", title:"خواص العمليات", type:"عمليات", activity:"u3l5" }
            ]
        },
        { // الوحدة 4: المعادلات والمجاهيل
            title: "🏝️ جزيرة المعادلات", c1: "#e74c3c", c2: "#c0392b", emoji: "⚖️",
            lessons: [
                { emoji:"🔍", title:"حل معادلة الدرجة الأولى (خطوة واحدة)", type:"معادلات", activity:"u4l1" },
                { emoji:"⚖️", title:"حل معادلة الدرجة الأولى (خطوتين)", type:"معادلات", activity:"u4l2" },
                { emoji:"📝", title:"معادلات تحتوي أقواس", type:"معادلات", activity:"u4l3" },
                { emoji:"📊", title:"معادلات تحتوي كسور", type:"معادلات", activity:"u4l4" },
                { emoji:"🔢", title:"تطبيقات على المعادلات (مسائل)", type:"تطبيقات", activity:"u4l5" },
                { emoji:"🔀", title:"معادلات الدرجة الثانية (بسيطة)", type:"معادلات", activity:"u4l6" },
                { emoji:"📐", title:"حل معادلات باستخدام التحليل", type:"معادلات", activity:"u4l7" }
            ]
        },
        { // الوحدة 5: العلاقات والدوال
            title: "🏝️ جزيرة العلاقات", c1: "#9b59b6", c2: "#8e44ad", emoji: "📈",
            lessons: [
                { emoji:"🔗", title:"العلاقات (المجال والمدى)", type:"علاقات", activity:"u5l1" },
                { emoji:"📊", title:"تمثيل العلاقات بيانياً", type:"علاقات", activity:"u5l2" },
                { emoji:"📐", title:"الدوال (مقدمة)", type:"دوال", activity:"u5l3" },
                { emoji:"📝", title:"تطبيقات على الدوال", type:"تطبيقات", activity:"u5l4" }
            ]
        }
    ];

    // تعيين totalLessonsCount
    gameState.totalLessonsCount = islands.reduce((acc, island) => acc + island.lessons.length, 0);    // ===== 8. بنوك الأسئلة لكل درس (كبيرة ومتنوعة) =====
    const activities = {
        // ========== الوحدة 1 ==========
        u1l1: [ // مفهوم الأسس
            { q: "ما قيمة ٣²؟", opts: ["٩", "٦", "٨", "٢٧"], ans: 0 },
            { q: "ما قيمة ٥³؟", opts: ["١٢٥", "٢٥", "١٥", "٦٢٥"], ans: 0 },
            { q: "٢⁴ =", opts: ["١٦", "٨", "٣٢", "٦٤"], ans: 0 },
            { q: "١٠⁵ =", opts: ["١٠٠٠٠٠", "١٠٠٠", "١٠٠٠٠", "١٠٠٠٠٠٠"], ans: 0 },
            { q: "٧² =", opts: ["٤٩", "١٤", "٤٩", "٥٦"], ans: 0 },
            { q: "أي مما يلي يساوي ٢⁵؟", opts: ["٣٢", "٢٥", "١٠", "٦٤"], ans: 0 },
            { q: "الأساس في ٨⁴ هو:", opts: ["٨", "٤", "٨⁴", "٤٨"], ans: 0 },
            { q: "الأس في ٦³ هو:", opts: ["٣", "٦", "٦³", "٢١٦"], ans: 0 },
            { q: "٩⁰ =", opts: ["١", "٠", "٩", "غير معرف"], ans: 0 },
            { q: "(-٣)² =", opts: ["٩", "-٩", "٦", "-٦"], ans: 0 }
        ],
        u1l2: [ // قوانين الأسس (الضرب)
            { q: "٢³ × ٢⁴ =", opts: ["٢⁷", "٢¹²", "٤⁷", "٨⁷"], ans: 0 },
            { q: "٥² × ٥³ =", opts: ["٥⁵", "٥⁶", "٢٥⁵", "١٠⁵"], ans: 0 },
            { q: "٣⁴ × ٣ =", opts: ["٣⁵", "٣⁴", "٩⁴", "٢٧"], ans: 0 },
            { q: "أ^٢ × أ^٥ =", opts: ["أ^٧", "أ^١٠", "٢أ^٧", "أ^٣"], ans: 0 },
            { q: "٢² × ٢³ × ٢⁴ =", opts: ["٢⁹", "٢²⁴", "٨⁹", "١٦⁹"], ans: 0 },
            { q: "إذا كان ٣^س × ٣^٢ = ٣^٨، فإن س =", opts: ["٦", "٤", "١٠", "١٦"], ans: 0 },
            { q: "قيمة (٤² × ٤³) ÷ ٤⁴ =", opts: ["٤", "٤⁵", "٤⁶", "٤¹"], ans: 0 },
            { q: "أي مما يلي يساوي ٦⁵؟", opts: ["٦² × ٦³", "٦⁴ × ٦", "٦¹ × ٦⁴", "جميع ما سبق"], ans: 3 },
            { q: "(-٢)³ × (-٢)² =", opts: ["(-٢)⁵", "٢⁵", "-٣٢", "٣٢"], ans: 0 },
            { q: "ص^٤ × ص^٣ × ص^٢ =", opts: ["ص^٩", "ص^٢٤", "٣ص^٩", "ص^١٢"], ans: 0 }
        ],
        u1l3: [ // قوانين الأسس (القسمة)
            { q: "٢⁵ ÷ ٢³ =", opts: ["٢²", "٢⁸", "٢¹⁵", "٢"], ans: 0 },
            { q: "٣⁷ ÷ ٣⁴ =", opts: ["٣³", "٣¹¹", "٩³", "٢٧"], ans: 0 },
            { q: "أ^٨ ÷ أ^٥ =", opts: ["أ³", "أ¹³", "أ⁴٠", "أ"], ans: 0 },
            { q: "٥⁹ ÷ ٥⁷ =", opts: ["٥²", "٥¹⁶", "٢٥", "١٠"], ans: 0 },
            { q: "(٦⁵ × ٦³) ÷ ٦⁴ =", opts: ["٦⁴", "٦¹²", "٦⁸", "٦"], ans: 0 },
            { q: "إذا كان ٧^س ÷ ٧³ = ٧⁴، فإن س =", opts: ["٧", "١", "١٢", "٤"], ans: 0 },
            { q: "١٠⁶ ÷ ١٠⁴ =", opts: ["١٠²", "١٠¹٠", "١٠٠", "١٠٠٠"], ans: 0 },
            { q: "(-٤)⁷ ÷ (-٤)⁵ =", opts: ["(-٤)²", "٤²", "-١٦", "١٦"], ans: 0 },
            { q: "ص^١٢ ÷ ص^٧ =", opts: ["ص^٥", "ص^١٩", "ص^٨٤", "ص^٤"], ans: 0 },
            { q: "٢^س ÷ ٢^ص =", opts: ["٢^(س-ص)", "٢^(س+ص)", "٢^(س×ص)", "٢^(س÷ص)"], ans: 0 }
        ],
        u1l4: [ // الأسس السالبة والصفر
            { q: "أ^٠ = (حيث أ ≠ ٠)", opts: ["١", "٠", "أ", "غير معرف"], ans: 0 },
            { q: "٥⁻² =", opts: ["١/٢٥", "-١٠", "٢٥", "-٢٥"], ans: 0 },
            { q: "٣⁻¹ =", opts: ["١/٣", "-٣", "٣", "-١/٣"], ans: 0 },
            { q: "(-٢)⁻³ =", opts: ["-١/٨", "١/٨", "-٨", "٨"], ans: 0 },
            { q: "٢⁻⁴ × ٢⁶ =", opts: ["٢²", "٢⁻²⁴", "٢¹٠", "٤"], ans: 0 },
            { q: "قيمة ٤⁰ + ٤⁻¹ =", opts: ["١ + ١/٤", "٥/٤", "١.٢٥", "جميع ما سبق"], ans: 3 },
            { q: "أي مما يلي يساوي ١؟", opts: ["٥⁰", "٧⁰", "(-٩)⁰", "جميع ما سبق"], ans: 3 },
            { q: "١٠⁻³ =", opts: ["٠.٠٠١", "٠.٠٠٠١", "٠.٠١", "١٠٠٠"], ans: 0 },
            { q: "إذا كان ٢^س = ١، فإن س =", opts: ["٠", "١", "٢", "غير معرف"], ans: 0 },
            { q: "٣⁻² + ٣⁻¹ =", opts: ["١/٩ + ١/٣", "٤/٩", "٠.٤٤٤", "جميع ما سبق"], ans: 3 }
        ],
        u1l5: [ // الجذر التربيعي
            { q: "√٢٥ =", opts: ["٥", "-٥", "٥ و -٥", "٦٢٥"], ans: 0 },
            { q: "√٣٦ =", opts: ["٦", "-٦", "٦ و -٦", "١٢"], ans: 0 },
            { q: "√٨١ =", opts: ["٩", "-٩", "٩ و -٩", "١٨"], ans: 0 },
            { q: "√١٠٠ =", opts: ["١٠", "-١٠", "١٠ و -١٠", "١٠٠٠"], ans: 0 },
            { q: "√١٢١ =", opts: ["١١", "-١١", "١١ و -١١", "١٢١"], ans: 0 },
            { q: "قيمة √(٦٤) =", opts: ["٨", "-٨", "٨ و -٨", "٤"], ans: 0 },
            { q: "√(٠.٠٤) =", opts: ["٠.٢", "٠.٠٢", "٠.٤", "٠.٠٠٤"], ans: 0 },
            { q: "أي الأعداد التالية مربع كامل؟", opts: ["١٦", "١٥", "١٧", "١٨"], ans: 0 },
            { q: "√(٩ + ١٦) =", opts: ["٥", "٧", "٢٥", "٤"], ans: 0 },
            { q: "√(٢٥) + √(١٤٤) =", opts: ["١٧", "١٦٩", "١٣", "١٥"], ans: 0 }
        ],
        u1l6: [ // الجذر التكعيبي
            { q: "∛٨ =", opts: ["٢", "٤", "٨", "١٦"], ans: 0 },
            { q: "∛٢٧ =", opts: ["٣", "٩", "٢٧", "٨١"], ans: 0 },
            { q: "∛٦٤ =", opts: ["٤", "٨", "١٦", "٣٢"], ans: 0 },
            { q: "∛١٢٥ =", opts: ["٥", "٢٥", "١٢٥", "٦٢٥"], ans: 0 },
            { q: "∛٢١٦ =", opts: ["٦", "٣٦", "٧٢", "١٠٨"], ans: 0 },
            { q: "∛(-٨) =", opts: ["-٢", "٢", "غير معرف", "-٤"], ans: 0 },
            { q: "∛(-٢٧) =", opts: ["-٣", "٣", "غير معرف", "-٩"], ans: 0 },
            { q: "أي الأعداد التالية مكعب كامل؟", opts: ["٢٧", "٢٦", "٢٨", "٢٩"], ans: 0 },
            { q: "∛(٨ × ٦٤) =", opts: ["٨", "٤", "١٢", "١٦"], ans: 0 },
            { q: "∛١٠٠٠ =", opts: ["١٠", "١٠٠", "١٠٠٠", "٣٣.٣"], ans: 0 }
        ],
        u1l7: [ // تطبيقات على الأسس والجذور
            { q: "مساحة مربع طول ضلعه ٥ سم =", opts: ["٢٥ سم²", "٢٠ سم", "٢٥ سم", "١٠ سم²"], ans: 0 },
            { q: "حجم مكعب طول حرفه ٤ سم =", opts: ["٦٤ سم³", "١٦ سم³", "٨ سم³", "٣٢ سم³"], ans: 0 },
            { q: "إذا كان طول ضلع مربع = √٢٥، فمساحته =", opts: ["٢٥", "٥", "١٠", "٢٠"], ans: 0 },
            { q: "إذا كان حجم مكعب = ٢٧ سم³، فإن طول حرفه =", opts: ["٣ سم", "٩ سم", "٢٧ سم", "٨١ سم"], ans: 0 },
            { q: "قيمة ٤√ × ٩√ =", opts: ["٦", "٣٦", "١٢", "١٣"], ans: 0 },
            { q: "قيمة (٢⁴) × (٣²) =", opts: ["١٤٤", "٢٤", "٣٦", "٧٢"], ans: 0 },
            { q: "٥√ × ٢٠√ =", opts: ["١٠", "١٠٠", "٢٥", "٢٠"], ans: 0 },
            { q: "قانون مساحة المربع هو:", opts: ["الضلع × نفسه", "الضلع × ٤", "الضلع × ٢", "الضلع + نفسه"], ans: 0 },
            { q: "حجم المكعب =", opts: ["الحرف³", "الحرف²", "الحرف × ٦", "الحرف × ١٢"], ans: 0 },
            { q: "إذا كان ٢^س = ٣٢، فإن س =", opts: ["٥", "٤", "٦", "١٦"], ans: 0 }
        ],

        // ========== الوحدة 2 ==========
        u2l1: [ // مربع مجموع
            { q: "(س + ص)² =", opts: ["س² + ٢س ص + ص²", "س² + ص²", "س² + ٢س + ص²", "س² + ٢ص + ص²"], ans: 0 },
            { q: "(٣ + ٥)² =", opts: ["٦٤", "١٦", "٣٤", "٦٨"], ans: 0 },
            { q: "(س + ٤)² =", opts: ["س² + ٨س + ١٦", "س² + ١٦", "س² + ٤س + ١٦", "س² + ٨س + ٤"], ans: 0 },
            { q: "(٢س + ٣)² =", opts: ["٤س² + ١٢س + ٩", "٢س² + ٦س + ٩", "٤س² + ٩", "٢س² + ١٢س + ٣"], ans: 0 },
            { q: "إذا كان (س + ٥)² = س² + ١٠س + ٢٥، فإن قيمة ٢٥ هي:", opts: ["مربع ٥", "ضعف ٥", "٥", "١٠"], ans: 0 },
            { q: "أكمل: (٢س + ١)² = ٤س² + ...... + ١", opts: ["٤س", "٢س", "٨س", "س"], ans: 0 },
            { q: "(أ + ب)² - (أ² + ب²) =", opts: ["٢أب", "٠", "أب", "٢أب + ب²"], ans: 0 },
            { q: "(٥ + ٣)² = ٥² + ٢×٥×٣ + ٣² =", opts: ["٢٥ + ٣٠ + ٩ = ٦٤", "٢٥ + ١٥ + ٩ = ٤٩", "٢٥ + ٦٠ + ٩ = ٩٤", "٢٥ + ٩ = ٣٤"], ans: 0 },
            { q: "(ص + ٢)² =", opts: ["ص² + ٤ص + ٤", "ص² + ٢ص + ٤", "ص² + ٤ص + ٢", "ص² + ٤"], ans: 0 },
            { q: "إذا كانت س = ٢، فاحسب (س + ٣)²", opts: ["٢٥", "١٣", "١١", "٥"], ans: 0 }
        ],
        u2l2: [ // مربع فرق
            { q: "(س - ص)² =", opts: ["س² - ٢س ص + ص²", "س² - ص²", "س² - ٢س ص - ص²", "س² + ٢س ص + ص²"], ans: 0 },
            { q: "(٧ - ٤)² =", opts: ["٩", "٢١", "٥", "٣"], ans: 0 },
            { q: "(س - ٣)² =", opts: ["س² - ٦س + ٩", "س² - ٩", "س² - ٣س + ٩", "س² - ٦س - ٩"], ans: 0 },
            { q: "(٣س - ٢)² =", opts: ["٩س² - ١٢س + ٤", "٣س² - ١٢س + ٤", "٩س² - ٤", "٩س² - ٦س + ٤"], ans: 0 },
            { q: "أكمل: (٥ - س)² = ٢٥ - ...... + س²", opts: ["١٠س", "٥س", "٢س", "٢٥س"], ans: 0 },
            { q: "(٢س - ١)² =", opts: ["٤س² - ٤س + ١", "٤س² + ٤س + ١", "٢س² - ٢س + ١", "٤س² - ١"], ans: 0 },
            { q: "(أ - ب)² + ٢أب =", opts: ["أ² + ب²", "أ² - ب²", "(أ - ب)²", "أ² - ٢أب + ب²"], ans: 0 },
            { q: "(٨ - ٣)² = ٦٤ - ٢×٨×٣ + ٩ =", opts: ["٦٤ - ٤٨ + ٩ = ٢٥", "٦٤ - ٢٤ + ٩ = ٤٩", "٦٤ - ٤٨ + ٩ = ٢٥", "٦٤ - ٤٨ - ٩ = ٧"], ans: 0 },
            { q: "(ص - ١)² =", opts: ["ص² - ٢ص + ١", "ص² - ١", "ص² + ٢ص + ١", "ص² - ٢ص - ١"], ans: 0 },
            { q: "إذا كانت س = ٤، فاحسب (س - ١)²", opts: ["٩", "١٥", "٣", "٥"], ans: 0 }
        ],
        u2l3: [ // الفرق بين مربعين
            { q: "س² - ص² =", opts: ["(س - ص)(س + ص)", "(س - ص)²", "(س + ص)²", "س² - ٢س ص + ص²"], ans: 0 },
            { q: "٩ - ٤ =", opts: ["٥", "١٣", "٣٦", "١"], ans: 0 },
            { q: "س² - ٢٥ =", opts: ["(س - ٥)(س + ٥)", "(س - ٥)²", "(س + ٥)²", "س² - ٥"], ans: 0 },
            { q: "٤س² - ٩ =", opts: ["(٢س - ٣)(٢س + ٣)", "(٢س - ٣)²", "(٢س + ٣)²", "٤(س - ٣)(س + ٣)"], ans: 0 },
            { q: "١٦ - ص² =", opts: ["(٤ - ص)(٤ + ص)", "(٤ - ص)²", "(٤ + ص)²", "١٦ - ص²"], ans: 0 },
            { q: "(س - ٢)(س + ٢) =", opts: ["س² - ٤", "س² + ٤", "(س - ٢)²", "(س + ٢)²"], ans: 0 },
            { q: "٨١ - ٤٩ =", opts: ["٣٢", "١٣٠", "٤٠", "٣٠"], ans: 0 },
            { q: "أكمل: ٣٦س² - ٢٥ = (٦س - ٥)(......)", opts: ["٦س + ٥", "٦س - ٥", "٥ - ٦س", "٣٦س + ٢٥"], ans: 0 },
            { q: "قيمة (١٠ - ٣)(١٠ + ٣) =", opts: ["٩١", "١٠٠ - ٩ = ٩١", "١٠٠ - ٦ = ٩٤", "١٠٠ - ٣ = ٩٧"], ans: 0 },
            { q: "إذا كانت س² - ٤٩ = ٠، فإن س =", opts: ["٧ أو -٧", "٧", "-٧", "٤٩"], ans: 0 }
        ],
        u2l4: [ // تحليل المقدار الثلاثي (بسيط)
            { q: "س² + ٥س + ٦ = (س + ٢)(س + ...)", opts: ["٣", "٢", "٤", "٥"], ans: 0 },
            { q: "س² + ٧س + ١٠ =", opts: ["(س + ٢)(س + ٥)", "(س + ١)(س + ١٠)", "(س + ٧)(س + ١٠)", "(س + ٥)(س + ٥)"], ans: 0 },
            { q: "س² - ٦س + ٨ =", opts: ["(س - ٢)(س - ٤)", "(س - ١)(س - ٨)", "(س + ٢)(س + ٤)", "(س - ٣)(س - ٣)"], ans: 0 },
            { q: "س² - ٤س + ٣ =", opts: ["(س - ١)(س - ٣)", "(س + ١)(س + ٣)", "(س - ١)(س + ٣)", "(س + ١)(س - ٣)"], ans: 0 },
            { q: "س² + ٩س + ٢٠ =", opts: ["(س + ٤)(س + ٥)", "(س + ٢)(س + ١٠)", "(س + ١)(س + ٢٠)", "(س + ٤)(س + ٤)"], ans: 0 },
            { q: "س² - ٧س + ١٢ =", opts: ["(س - ٣)(س - ٤)", "(س + ٣)(س + ٤)", "(س - ٢)(س - ٦)", "(س - ١)(س - ١٢)"], ans: 0 },
            { q: "س² + ٨س + ١٦ =", opts: ["(س + ٤)²", "(س + ٨)²", "(س + ٢)(س + ٨)", "(س + ١)(س + ١٦)"], ans: 0 },
            { q: "س² - ١٠س + ٢٥ =", opts: ["(س - ٥)²", "(س + ٥)²", "(س - ١٠)²", "(س - ٢٥)²"], ans: 0 },
            { q: "عامل المقدار: س² + ١١س + ٢٤", opts: ["(س + ٣)(س + ٨)", "(س + ٤)(س + ٦)", "(س + ٢)(س + ١٢)", "(س + ١)(س + ٢٤)"], ans: 0 },
            { q: "عامل المقدار: س² - ١٢س + ٣٥", opts: ["(س - ٥)(س - ٧)", "(س + ٥)(س + ٧)", "(س - ١)(س - ٣٥)", "(س - ٥)(س + ٧)"], ans: 0 }
        ],
        u2l5: [ // تحليل المقدار الثلاثي (مع معامل)
            { q: "٢س² + ٧س + ٣ =", opts: ["(٢س + ١)(س + ٣)", "(٢س + ٣)(س + ١)", "(٢س + ١)(س + ٢)", "(٢س + ٣)(س + ٢)"], ans: 0 },
            { q: "٣س² + ١٠س + ٨ =", opts: ["(٣س + ٤)(س + ٢)", "(٣س + ٢)(س + ٤)", "(٣س + ١)(س + ٨)", "(٣س + ٨)(س + ١)"], ans: 0 },
            { q: "٤س² + ١٢س + ٥ =", opts: ["(٢س + ١)(٢س + ٥)", "(٤س + ١)(س + ٥)", "(٤س + ٥)(س + ١)", "(٢س + ٥)(٢س + ١)"], ans: 0 },
            { q: "٢س² - ٩س + ٩ =", opts: ["(٢س - ٣)(س - ٣)", "(٢س + ٣)(س - ٣)", "(٢س - ٣)(س + ٣)", "(س - ٣)(٢س - ٣)"], ans: 0 },
            { q: "٦س² + ١٣س + ٦ =", opts: ["(٢س + ٣)(٣س + ٢)", "(٣س + ٢)(٢س + ٣)", "(٦س + ١)(س + ٦)", "(٣س + ١)(٢س + ٦)"], ans: 0 },
            { q: "٣س² - ١١س + ٦ =", opts: ["(٣س - ٢)(س - ٣)", "(٣س + ٢)(س - ٣)", "(س - ٣)(٣س - ٢)", "(٣س - ٣)(س - ٢)"], ans: 0 },
            { q: "٤س² + ٨س + ٣ =", opts: ["(٢س + ١)(٢س + ٣)", "(٤س + ١)(س + ٣)", "(٢س + ٣)(٢س + ١)", "(٤س + ٣)(س + ١)"], ans: 0 },
            { q: "٢س² - ٥س + ٢ =", opts: ["(٢س - ١)(س - ٢)", "(٢س + ١)(س - ٢)", "(س - ٢)(٢س - ١)", "(٢س - ٢)(س - ١)"], ans: 0 },
            { q: "٥س² + ١٧س + ٦ =", opts: ["(٥س + ٢)(س + ٣)", "(٥س + ٣)(س + ٢)", "(٥س + ١)(س + ٦)", "(٥س + ٦)(س + ١)"], ans: 0 },
            { q: "٨س² + ١٤س + ٣ =", opts: ["(٤س + ١)(٢س + ٣)", "(٨س + ١)(س + ٣)", "(٢س + ١)(٤س + ٣)", "(٨س + ٣)(س + ١)"], ans: 0 }
        ],
        u2l6: [ // التحليل بإخراج العامل المشترك
            { q: "٦س + ٩ =", opts: ["٣(٢س + ٣)", "٢(٣س + ٤)", "٣(٢س + ٢)", "٦(س + ٣)"], ans: 0 },
            { q: "٤س² - ٨س =", opts: ["٤س(س - ٢)", "٤(س² - ٢س)", "٨س(س - ١)", "٢س(٢س - ٤)"], ans: 0 },
            { q: "١٠س³ + ١٥س² =", opts: ["٥س²(٢س + ٣)", "٥س(٢س² + ٣س)", "١٠س²(س + ١.٥)", "٥س²(٢س + ٣)"], ans: 0 },
            { q: "٣أ + ٦ب - ٩جـ =", opts: ["٣(أ + ٢ب - ٣جـ)", "٣(أ + ٢ب + ٣جـ)", "٣(أ + ٢ب - ٣جـ)", "٣أ + ٦ب - ٩جـ"], ans: 0 },
            { q: "١٤س²ص - ٢١س ص² =", opts: ["٧س ص(٢س - ٣ص)", "٧س ص(٢س + ٣ص)", "٧س(٢س ص - ٣ص²)", "٧ص(٢س² - ٣س ص)"], ans: 0 },
            { q: "٨م ن³ - ١٢م² ن² =", opts: ["٤م ن²(٢ن - ٣م)", "٤م ن²(٢ن + ٣م)", "٤م ن(٢ن² - ٣م ن)", "٤ن²(٢م ن - ٣م²)"], ans: 0 },
            { q: "حلل: ٢٥س² - ٣٦ =", opts: ["(٥س - ٦)(٥س + ٦)", "٥(٥س² - ٧.٢)", "٢٥(س² - ١.٤٤)", "لا يمكن"], ans: 0 },
            { q: "العامل المشترك الأكبر للحدود ٦س³، ٩س²، ١٢س هو:", opts: ["٣س", "٣س²", "٦س", "٣"], ans: 0 },
            { q: "حلل: ٥س² + ٢٠س", opts: ["٥س(س + ٤)", "٥(س² + ٤س)", "س(٥س + ٢٠)", "٥س(س + ٤)"], ans: 0 },
            { q: "حلل: ٧أ²ب - ١٤أب²", opts: ["٧أب(أ - ٢ب)", "٧أب(أ + ٢ب)", "أب(٧أ - ١٤ب)", "٧أ(أب - ٢ب²)"], ans: 0 }
        ],
        u2l7: [ // تطبيقات على التحليل
            { q: "إذا كانت س = ٢، ص = ٣، فاحسب س² + ٢س ص + ص²", opts: ["٢٥", "١٣", "٣٦", "٥"], ans: 0 },
            { q: "حل المعادلة: س² - ٩ = ٠", opts: ["س = ٣ أو -٣", "س = ٣", "س = -٣", "س = ٩"], ans: 0 },
            { q: "مساحة مستطيل (س + ٣) (س + ٢) =", opts: ["س² + ٥س + ٦", "س² + ٦س + ٦", "س² + ٥س + ٥", "س² + ٦س + ٥"], ans: 0 },
            { q: "إذا كان (س + ١)² = ٢٥، فما قيمة س؟", opts: ["٤ أو -٦", "٤", "-٦", "٢٤"], ans: 0 },
            { q: "قيمة ٩٩² باستخدام صيغ الضرب المختصر =", opts: ["(١٠٠ - ١)² = ١٠٠٠٠ - ٢٠٠ + ١ = ٩٨٠١", "٩٩٠٠", "١٠٠٠٠ - ٩٩", "٩٨٠٠"], ans: 0 },
            { q: "حلل ثم احسب: ٤٩ - ٢٥", opts: ["(٧ - ٥)(٧ + ٥) = ٢ × ١٢ = ٢٤", "٢٤", "٤٩ - ٢٥ = ٢٤", "جميع ما سبق"], ans: 3 },
            { q: "إذا كان س² + ٦س + ٩ = ٠، فإن س =", opts: ["-٣", "٣", "٦", "-٦"], ans: 0 },
            { q: "مساحة مربع طول ضلعه (س + ٢) =", opts: ["س² + ٤س + ٤", "س² + ٤", "س² + ٢س + ٤", "س² + ٤س + ٢"], ans: 0 },
            { q: "قيمة ١٠١² - ٩٩² =", opts: ["(١٠١ - ٩٩)(١٠١ + ٩٩) = ٢ × ٢٠٠ = ٤٠٠", "٤٠٠", "٢٠٠", "٤٠٠٠"], ans: 0 },
            { q: "إذا كان (س - ٥)² = ٠، فإن س =", opts: ["٥", "-٥", "٢٥", "٠"], ans: 0 }
        ],

        // ========== الوحدة 3 ==========
        u3l1: [ // جمع وطرح الأعداد الحقيقية
            { q: "√٢ + √٢ =", opts: ["٢√٢", "٤", "٢", "√٤"], ans: 0 },
            { q: "٣√٣ - √٣ =", opts: ["٢√٣", "٣", "٤√٣", "٢"], ans: 0 },
            { q: "٥ + ٣√٢ + ٢ - √٢ =", opts: ["٧ + ٢√٢", "٧ + ٤√٢", "٧ + ٣√٢", "٧ + √٢"], ans: 0 },
            { q: "√٨ + √١٨ =", opts: ["٥√٢", "٥", "٢√٢ + ٣√٢ = ٥√٢", "٢٦"], ans: 0 },
            { q: "٤√٥ - ٢√٥ =", opts: ["٢√٥", "٢", "٦√٥", "٨√٥"], ans: 0 },
            { q: "√٢٥ + √٤ =", opts: ["٥ + ٢ = ٧", "٧", "٢٩", "٩"], ans: 0 },
            { q: "٣√٢ + ٤√٣ - ٢√٢ =", opts: ["√٢ + ٤√٣", "٥√٢ + ٤√٣", "√٢ + ٤√٣", "٧√٥"], ans: 0 },
            { q: "٢√٧ + ٣√٧ - √٧ =", opts: ["٤√٧", "٦√٧", "٥√٧", "٤"], ans: 0 },
            { q: "√٠.٠٩ + √٠.٢٥ =", opts: ["٠.٣ + ٠.٥ = ٠.٨", "٠.٨", "٠.٠٣ + ٠.٠٥ = ٠.٠٨", "٠.٣٤"], ans: 0 },
            { q: "إذا كان أ = √٣، ب = ٢√٣، فما أ + ب؟", opts: ["٣√٣", "٢√٣", "٣", "٦"], ans: 0 }
        ],
        u3l2: [ // ضرب الأعداد الحقيقية
            { q: "√٢ × √٣ =", opts: ["√٦", "٦", "√٥", "٥"], ans: 0 },
            { q: "٣√٢ × ٤√٢ =", opts: ["٣ × ٤ × ٢ = ٢٤", "٢٤", "١٢√٢", "١٢"], ans: 0 },
            { q: "√٨ × √٢ =", opts: ["√١٦ = ٤", "٤", "√٨", "٨"], ans: 0 },
            { q: "(√٥ + ٢) × (√٥ - ٢) =", opts: ["٥ - ٤ = ١", "١", "٥ + ٤ = ٩", "٥ - ٢ = ٣"], ans: 0 },
            { q: "٢√٣ × ٥√٣ =", opts: ["٢ × ٥ × ٣ = ٣٠", "٣٠", "١٠√٣", "١٠"], ans: 0 },
            { q: "√١٢ × √٧ =", opts: ["√٨٤", "٨٤", "√١٩", "١٩"], ans: 0 },
            { q: "(٢ + √٣) × (٢ + √٣) =", opts: ["٤ + ٤√٣ + ٣ = ٧ + ٤√٣", "٧ + ٤√٣", "٤ + ٣ = ٧", "٤ + ٢√٣ + ٣"], ans: 0 },
            { q: "٣√٦ × ٢√٦ =", opts: ["٦ × ٦ = ٣٦", "٣٦", "٥√٣٦", "٥√١٢"], ans: 0 },
            { q: "√٠.٠٤ × √٠.٢٥ =", opts: ["٠.٢ × ٠.٥ = ٠.١", "٠.١", "٠.٠١", "٠.٠٠٨"], ans: 0 },
            { q: "إذا كان س = √٧، ص = √٧، فما س × ص؟", opts: ["٧", "٤٩", "√١٤", "١٤"], ans: 0 }
        ]
    };        u3l3: [ // قسمة الأعداد الحقيقية
            { q: "√١٢ ÷ √٣ =", opts: ["√٤ = ٢", "٢", "٤", "√٩"], ans: 0 },
            { q: "١٠√٥ ÷ ٢√٥ =", opts: ["٥", "٥√٥", "٢٠", "١٢"], ans: 0 },
            { q: "√١٨ ÷ √٢ =", opts: ["√٩ = ٣", "٣", "٩", "٦"], ans: 0 },
            { q: "(√٥٠) ÷ (√٢) =", opts: ["√٢٥ = ٥", "٥", "٢٥", "١٠"], ans: 0 },
            { q: "٦√٣ ÷ ٢√٣ =", opts: ["٣", "٣√٣", "١٢", "٤"], ans: 0 },
            { q: "√(٢٧/٣) =", opts: ["√٩ = ٣", "٣", "٩", "٢٧"], ans: 0 },
            { q: "(٤√٦) ÷ (٢√٣) =", opts: ["٢√٢", "٢", "٨√٢", "٢√١٨"], ans: 0 },
            { q: "√٨١ ÷ √٩ =", opts: ["٩ ÷ ٣ = ٣", "٣", "٧٢", "٩"], ans: 0 },
            { q: "١٠ ÷ √٥ = (بترشيح المقام)", opts: ["١٠√٥ / ٥ = ٢√٥", "٢√٥", "√٢", "٢٠"], ans: 0 },
            { q: "إذا كان س = √٢٠، ص = √٥، فما س ÷ ص؟", opts: ["٢", "٤", "√٤ = ٢", "√١٥"], ans: 0 }
        ],
        u3l4: [ // الترتيب والعمليات
            { q: "رتب الأعداد تصاعدياً: √٤، √٩، √١٦", opts: ["٢، ٣، ٤", "٤، ٣، ٢", "٤، ٢، ٣", "٢، ٤، ٣"], ans: 0 },
            { q: "أي الأعداد أكبر: √٣٥ أم ٦؟", opts: ["√٣٥ ≈ ٥.٩، إذاً ٦ أكبر", "٦", "√٣٥", "متساويان"], ans: 0 },
            { q: "احسب: ٢ + ٣ × ٤", opts: ["٢ + ١٢ = ١٤", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "احسب: (٢ + ٣) × ٤", opts: ["٥ × ٤ = ٢٠", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "إذا كان أ = ٣، ب = ٢، فاحسب أ² + ب", opts: ["٩ + ٢ = ١١", "١١", "١٣", "٧"], ans: 0 },
            { q: "رتب الأعداد تنازلياً: ٥، √٢٧، √٨", opts: ["٥، √٢٧، √٨", "√٢٧، ٥، √٨", "٥، √٨، √٢٧", "√٢٧، √٨، ٥"], ans: 0 },
            { q: "أي الأعداد أصغر: √٨ أم ٣؟", opts: ["√٨ ≈ ٢.٨، إذاً √٨ أصغر", "٣", "√٨", "متساويان"], ans: 0 },
            { q: "احسب: ١٠ - ٤ ÷ ٢", opts: ["١٠ - ٢ = ٨", "٨", "٣", "١٢"], ans: 0 },
            { q: "احسب: ٤² - ٤", opts: ["١٦ - ٤ = ١٢", "١٢", "٤", "٠"], ans: 0 },
            { q: "قارن: √(٧+٩) و √٧ + √٩", opts: ["√١٦ = ٤، √٧ + √٩ ≈ ٢.٦ + ٣ = ٥.٦، الثاني أكبر", "الثاني أكبر", "الأول أكبر", "متساويان"], ans: 0 }
        ],
        u3l5: [ // خواص العمليات
            { q: "خاصية الإبدال في الجمع تعني:", opts: ["أ + ب = ب + أ", "أ + (ب + جـ) = (أ + ب) + جـ", "أ + ٠ = أ", "أ + (-أ) = ٠"], ans: 0 },
            { q: "خاصية التجميع في الضرب تعني:", opts: ["(أ × ب) × جـ = أ × (ب × جـ)", "أ × ب = ب × أ", "أ × ١ = أ", "أ × ٠ = ٠"], ans: 0 },
            { q: "العنصر المحايد في الجمع هو:", opts: ["٠", "١", "-١", "لا يوجد"], ans: 0 },
            { q: "العنصر المحايد في الضرب هو:", opts: ["١", "٠", "-١", "لا يوجد"], ans: 0 },
            { q: "خاصية التوزيع تعني:", opts: ["أ × (ب + جـ) = أ×ب + أ×جـ", "أ + (ب × جـ) = (أ+ب)×(أ+جـ)", "أ × (ب - جـ) = أ×ب - أ×جـ", "أ و ب صحيحتان"], ans: 0 },
            { q: "نظير ٥ الجمعي هو:", opts: ["-٥", "١/٥", "٠", "٥"], ans: 0 },
            { q: "نظير ٣ الضربي هو:", opts: ["١/٣", "-٣", "٠", "٣"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الجمع عملية إبدالية", "الطرح عملية إبدالية", "القسمة عملية إبدالية", "جميع ما سبق"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الضرب عملية تجميعية", "الضرب عملية إبدالية", "للضرب عنصر محايد", "جميع ما سبق"], ans: 3 },
            { q: "٣ × (٥ - ٢) = (٣×٥) - (٣×٢) تمثل خاصية", opts: ["التوزيع", "الإبدال", "الدمج", "المحايد"], ans: 0 }
        ],

        // ========== الوحدة 4 ==========
        u4l1: [ // حل معادلة الدرجة الأولى (خطوة واحدة)
            { q: "حل المعادلة: س + ٥ = ١٢", opts: ["س = ٧", "س = ١٧", "س = ٦٠", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: س - ٤ = ٩", opts: ["س = ١٣", "س = ٥", "س = ٣٦", "س = -٥"], ans: 0 },
            { q: "حل المعادلة: ٣س = ٢٤", opts: ["س = ٨", "س = ٢١", "س = ٢٧", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: س/٥ = ٦", opts: ["س = ٣٠", "س = ١١", "س = ١.٢", "س = ٢٥"], ans: 0 },
            { q: "إذا كانت س + ٨ = ٢٠، فإن س =", opts: ["١٢", "٢٨", "١٦٠", "٢.٥"], ans: 0 },
            { q: "إذا كانت ٧س = ٤٢، فإن س =", opts: ["٦", "٤٩", "٢٩٤", "٣٥"], ans: 0 },
            { q: "حل المعادلة: ص - ٣ = ١٠", opts: ["ص = ١٣", "ص = ٧", "ص = ٣٠", "ص = -٧"], ans: 0 },
            { q: "حل المعادلة: ٤م = ٣٦", opts: ["م = ٩", "م = ٤٠", "م = ٣٢", "م = ١٤٤"], ans: 0 },
            { q: "حل المعادلة: ن/٢ = ٨", opts: ["ن = ١٦", "ن = ٤", "ن = ١٠", "ن = ٦"], ans: 0 },
            { q: "إذا كانت س + ١٢ = ٣٠، فإن س =", opts: ["١٨", "٤٢", "٢.٥", "٣٦٠"], ans: 0 }
        ],
        u4l2: [ // حل معادلة الدرجة الأولى (خطوتين)
            { q: "حل المعادلة: ٢س + ٣ = ٩", opts: ["س = ٣", "س = ٦", "س = ١٢", "س = ٢٤"], ans: 0 },
            { q: "حل المعادلة: ٣س - ٥ = ٧", opts: ["س = ٤", "س = ٢", "س = ١٢", "س = ٣٦"], ans: 0 },
            { q: "حل المعادلة: ٤س + ٧ = ١٩", opts: ["س = ٣", "س = ١٢", "س = ٢٦", "س = ٦.٥"], ans: 0 },
            { q: "حل المعادلة: ٥س - ٢ = ١٣", opts: ["س = ٣", "س = ١١", "س = ١٥", "س = ٥٥"], ans: 0 },
            { q: "إذا كانت ٢س + ٥ = ١٥، فإن س =", opts: ["٥", "١٠", "٢٠", "٣"], ans: 0 },
            { q: "إذا كانت ٣س - ٤ = ٨، فإن س =", opts: ["٤", "١٢", "٣", "٢٤"], ans: 0 },
            { q: "حل المعادلة: ٦س + ١ = ٣١", opts: ["س = ٥", "س = ٣٠", "س = ٣٢", "س = ١.٨"], ans: 0 },
            { q: "حل المعادلة: ٧س - ٨ = ١٣", opts: ["س = ٣", "س = ٢١", "س = ٥", "س = ١٠٥"], ans: 0 },
            { q: "حل المعادلة: ٨س + ٤ = ٢٠", opts: ["س = ٢", "س = ١٦", "س = ٢٤", "س = ٣"], ans: 0 },
            { q: "إذا كانت ٤س + ٩ = ٢٥، فإن س =", opts: ["٤", "١٦", "٣٤", "٦"], ans: 0 }
        ],
        u4l3: [ // معادلات تحتوي أقواس
            { q: "حل المعادلة: ٢(س + ٣) = ١٠", opts: ["س = ٢", "س = ٧", "س = ٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: ٣(س - ٢) = ١٢", opts: ["س = ٦", "س = ١٠", "س = ٤", "س = ٣٨"], ans: 0 },
            { q: "حل المعادلة: ٤(٢س + ١) = ٢٠", opts: ["س = ٢", "س = ٤", "س = ٦", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٣) = ٢٠", opts: ["س = ٧", "س = ٤", "س = ٨", "س = ٢٣"], ans: 0 },
            { q: "إذا كانت ٢(٣س - ١) = ١٦، فإن س =", opts: ["٣", "٥", "٤", "٢"], ans: 0 },
            { q: "إذا كانت ٤(س + ٥) = ٢٨، فإن س =", opts: ["٢", "٧", "١٢", "٣"], ans: 0 },
            { q: "حل المعادلة: ٣(س + ٢) - ٤ = ١١", opts: ["س = ٣", "س = ٥", "س = ٤", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: ٢(٢س - ١) + ٣ = ١٣", opts: ["س = ٣", "س = ٤", "س = ٢", "س = ٥"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٢) = ٣س + ٤", opts: ["س = ٧", "س = ٦", "س = ٥", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: ٢(س + ٣) = ٣(س - ١)", opts: ["س = ٩", "س = ٦", "س = ٣", "س = ١٢"], ans: 0 }
        ],
        u4l4: [ // معادلات تحتوي كسور
            { q: "حل المعادلة: س/٢ + ٣ = ٥", opts: ["س = ٤", "س = ١", "س = ٢", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: (س/٣) - ٢ = ١", opts: ["س = ٩", "س = ٣", "س = ١", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: ٢س/٥ = ٤", opts: ["س = ١٠", "س = ٢.٥", "س = ٢٠", "س = ٤٠"], ans: 0 },
            { q: "حل المعادلة: (س + ١)/٢ = ٣", opts: ["س = ٥", "س = ٧", "س = ٦", "س = ٢"], ans: 0 },
            { q: "إذا كانت (س/٤) + ١ = ٣، فإن س =", opts: ["٨", "١٦", "٤", "١٢"], ans: 0 },
            { q: "إذا كانت (٢س)/٣ = ٨، فإن س =", opts: ["١٢", "٢٤", "٦", "٨"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)/٣ = ٤", opts: ["س = ١٤", "س = ١٠", "س = ١٢", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: (٣س)/٥ = ٩", opts: ["س = ١٥", "س = ٢٧", "س = ٣", "س = ٤٥"], ans: 0 },
            { q: "حل المعادلة: (س/٢) + (س/٣) = ٥", opts: ["س = ٦", "س = ١٠", "س = ١٢", "س = ٣٠"], ans: 0 },
            { q: "حل المعادلة: (٢س - ١)/٣ = ٥", opts: ["س = ٨", "س = ٧", "س = ٩", "س = ٦"], ans: 0 }
        ],
        u4l5: [ // تطبيقات على المعادلات (مسائل)
            { q: "مجموع عدد و ٥ يساوي ١٢، ما العدد؟", opts: ["٧", "١٧", "٦٠", "٢"], ans: 0 },
            { q: "ثلاثة أمثال عدد تساوي ٢٤، ما العدد؟", opts: ["٨", "٢١", "٢٧", "١٢"], ans: 0 },
            { q: "إذا كان عمر أحمد ١٢ سنة، وعمر أخيه ضعف عمره، فما مجموع عمريهما؟", opts: ["٣٦", "٢٤", "١٢", "٤٨"], ans: 0 },
            { q: "اشترى محمد ٣ كتب بـ ٢٠ جنيهاً، ودفتر بـ ٥ جنيهات. كم دفع؟", opts: ["٦٥", "٢٥", "٣٠", "٣٥"], ans: 0 },
            { q: "مستطيل طوله يزيد عن عرضه بمقدار ٣ سم، ومحيطه ٢٢ سم، فما طوله؟", opts: ["٧ سم", "٥ سم", "٤ سم", "٨ سم"], ans: 0 },
            { q: "عدد إذا أضفت إليه ٨ ثم ضاعفت الناتج تحصل على ٣٠، ما العدد؟", opts: ["٧", "٦", "٨", "٩"], ans: 0 },
            { q: "سعر قلم ٥ جنيهات، وسعر دفتر ١٠ جنيهات، كم ثمن ٣ أقلام ودفترين؟", opts: ["٣٥", "٢٥", "٤٠", "٣٠"], ans: 0 },
            { q: "إذا كان مجموع ثلاثة أعداد متتالية هو ٣٠، فما أصغرها؟", opts: ["٩", "١٠", "١١", "٨"], ans: 0 },
            { q: "عمر أميرة يساوي ضعف عمر أختها، ومجموع عمريهما ٢٧ سنة، فما عمر أختها؟", opts: ["٩", "١٨", "٢٧", "١٣.٥"], ans: 0 },
            { q: "اشترى خالد ٨ دفاتر بسعر ٦ ريالات للدفتر، ودفع ثمنها بـ ١٠٠ ريال، كم الباقي؟", opts: ["٥٢", "٤٨", "٦٨", "٧٢"], ans: 0 }
        ],
        u4l6: [ // معادلات الدرجة الثانية (بسيطة)
            { q: "حل المعادلة: س² = ٩", opts: ["س = ٣ أو -٣", "س = ٣", "س = -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² = ١٦", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² = ٢٥", opts: ["س = ٥ أو -٥", "س = ٥", "س = -٥", "س = ٢٥"], ans: 0 },
            { q: "حل المعادلة: ٢س² = ٣٢", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠", opts: ["س = ٢ أو -٢", "س = ٢", "س = -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤٩ = ٠", opts: ["س = ٧ أو -٧", "س = ٧", "س = -٧", "س = ٤٩"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)² = ٠", opts: ["س = ٢", "س = -٢", "س = ٢ أو -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² + ٦س + ٩ = ٠", opts: ["س = -٣", "س = ٣", "س = ٣ أو -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² - ١٠س + ٢٥ = ٠", opts: ["س = ٥", "س = -٥", "س = ٥ أو -٥", "س = ٢٥"], ans: 0 },
            { q: "مجموعة حل المعادلة س² = ٣٦ هي", opts: ["{٦، -٦}", "{٦}", "{-٦}", "{٣٦}"], ans: 0 }
        ],
        u4l7: [ // حل معادلات باستخدام التحليل
            { q: "حل المعادلة: س² + ٥س + ٦ = ٠", opts: ["س = -٢ أو -٣", "س = ٢ أو ٣", "س = -٥ أو -١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٥س + ٦ = ٠", opts: ["س = ٢ أو ٣", "س = -٢ أو -٣", "س = ٥ أو ١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² + ٧س + ١٠ = ٠", opts: ["س = -٢ أو -٥", "س = ٢ أو ٥", "س = -٧ أو -١٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² - ٨س + ١٥ = ٠", opts: ["س = ٣ أو ٥", "س = -٣ أو -٥", "س = ٨ أو ١٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠ باستخدام التحليل", opts: ["(س-٢)(س+٢)=٠، س=٢ أو -٢", "س=٢", "س=-٢", "س=٤"], ans: 0 },
            { q: "حل المعادلة: ٢س² + ٧س + ٣ = ٠", opts: ["س = -١/٢ أو -٣", "س = ١/٢ أو ٣", "س = -٢ أو -٣", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٣س² + ١٠س + ٨ = ٠", opts: ["س = -٤/٣ أو -٢", "س = ٤/٣ أو ٢", "س = -٢ أو -٤", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: س² - ٩س + ٢٠ = ٠", opts: ["س = ٤ أو ٥", "س = -٤ أو -٥", "س = ٩ أو ٢٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² + س - ١٢ = ٠", opts: ["س = -٤ أو ٣", "س = ٤ أو -٣", "س = ١ أو -١٢", "س = ١٢"], ans: 0 },
            { q: "مجموعة حل المعادلة س² - ٣س - ١٠ = ٠ هي", opts: ["{٥، -٢}", "{٢، -٥}", "{٥، ٢}", "{-٥، -٢}"], ans: 0 }
        ]
    };
        u3l3: [ // قسمة الأعداد الحقيقية
            { q: "√١٢ ÷ √٣ =", opts: ["√٤ = ٢", "٢", "٤", "√٩"], ans: 0 },
            { q: "١٠√٥ ÷ ٢√٥ =", opts: ["٥", "٥√٥", "٢٠", "١٢"], ans: 0 },
            { q: "√١٨ ÷ √٢ =", opts: ["√٩ = ٣", "٣", "٩", "٦"], ans: 0 },
            { q: "(√٥٠) ÷ (√٢) =", opts: ["√٢٥ = ٥", "٥", "٢٥", "١٠"], ans: 0 },
            { q: "٦√٣ ÷ ٢√٣ =", opts: ["٣", "٣√٣", "١٢", "٤"], ans: 0 },
            { q: "√(٢٧/٣) =", opts: ["√٩ = ٣", "٣", "٩", "٢٧"], ans: 0 },
            { q: "(٤√٦) ÷ (٢√٣) =", opts: ["٢√٢", "٢", "٨√٢", "٢√١٨"], ans: 0 },
            { q: "√٨١ ÷ √٩ =", opts: ["٩ ÷ ٣ = ٣", "٣", "٧٢", "٩"], ans: 0 },
            { q: "١٠ ÷ √٥ = (بترشيح المقام)", opts: ["١٠√٥ / ٥ = ٢√٥", "٢√٥", "√٢", "٢٠"], ans: 0 },
            { q: "إذا كان س = √٢٠، ص = √٥، فما س ÷ ص؟", opts: ["٢", "٤", "√٤ = ٢", "√١٥"], ans: 0 }
        ],
        u3l4: [ // الترتيب والعمليات
            { q: "رتب الأعداد تصاعدياً: √٤، √٩، √١٦", opts: ["٢، ٣، ٤", "٤، ٣، ٢", "٤، ٢، ٣", "٢، ٤، ٣"], ans: 0 },
            { q: "أي الأعداد أكبر: √٣٥ أم ٦؟", opts: ["√٣٥ ≈ ٥.٩، إذاً ٦ أكبر", "٦", "√٣٥", "متساويان"], ans: 0 },
            { q: "احسب: ٢ + ٣ × ٤", opts: ["٢ + ١٢ = ١٤", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "احسب: (٢ + ٣) × ٤", opts: ["٥ × ٤ = ٢٠", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "إذا كان أ = ٣، ب = ٢، فاحسب أ² + ب", opts: ["٩ + ٢ = ١١", "١١", "١٣", "٧"], ans: 0 },
            { q: "رتب الأعداد تنازلياً: ٥، √٢٧، √٨", opts: ["٥، √٢٧، √٨", "√٢٧، ٥، √٨", "٥، √٨، √٢٧", "√٢٧، √٨، ٥"], ans: 0 },
            { q: "أي الأعداد أصغر: √٨ أم ٣؟", opts: ["√٨ ≈ ٢.٨، إذاً √٨ أصغر", "٣", "√٨", "متساويان"], ans: 0 },
            { q: "احسب: ١٠ - ٤ ÷ ٢", opts: ["١٠ - ٢ = ٨", "٨", "٣", "١٢"], ans: 0 },
            { q: "احسب: ٤² - ٤", opts: ["١٦ - ٤ = ١٢", "١٢", "٤", "٠"], ans: 0 },
            { q: "قارن: √(٧+٩) و √٧ + √٩", opts: ["√١٦ = ٤، √٧ + √٩ ≈ ٢.٦ + ٣ = ٥.٦، الثاني أكبر", "الثاني أكبر", "الأول أكبر", "متساويان"], ans: 0 }
        ],
        u3l5: [ // خواص العمليات
            { q: "خاصية الإبدال في الجمع تعني:", opts: ["أ + ب = ب + أ", "أ + (ب + جـ) = (أ + ب) + جـ", "أ + ٠ = أ", "أ + (-أ) = ٠"], ans: 0 },
            { q: "خاصية التجميع في الضرب تعني:", opts: ["(أ × ب) × جـ = أ × (ب × جـ)", "أ × ب = ب × أ", "أ × ١ = أ", "أ × ٠ = ٠"], ans: 0 },
            { q: "العنصر المحايد في الجمع هو:", opts: ["٠", "١", "-١", "لا يوجد"], ans: 0 },
            { q: "العنصر المحايد في الضرب هو:", opts: ["١", "٠", "-١", "لا يوجد"], ans: 0 },
            { q: "خاصية التوزيع تعني:", opts: ["أ × (ب + جـ) = أ×ب + أ×جـ", "أ + (ب × جـ) = (أ+ب)×(أ+جـ)", "أ × (ب - جـ) = أ×ب - أ×جـ", "أ و ب صحيحتان"], ans: 0 },
            { q: "نظير ٥ الجمعي هو:", opts: ["-٥", "١/٥", "٠", "٥"], ans: 0 },
            { q: "نظير ٣ الضربي هو:", opts: ["١/٣", "-٣", "٠", "٣"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الجمع عملية إبدالية", "الطرح عملية إبدالية", "القسمة عملية إبدالية", "جميع ما سبق"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الضرب عملية تجميعية", "الضرب عملية إبدالية", "للضرب عنصر محايد", "جميع ما سبق"], ans: 3 },
            { q: "٣ × (٥ - ٢) = (٣×٥) - (٣×٢) تمثل خاصية", opts: ["التوزيع", "الإبدال", "الدمج", "المحايد"], ans: 0 }
        ],

        // ========== الوحدة 4 ==========
        u4l1: [ // حل معادلة الدرجة الأولى (خطوة واحدة)
            { q: "حل المعادلة: س + ٥ = ١٢", opts: ["س = ٧", "س = ١٧", "س = ٦٠", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: س - ٤ = ٩", opts: ["س = ١٣", "س = ٥", "س = ٣٦", "س = -٥"], ans: 0 },
            { q: "حل المعادلة: ٣س = ٢٤", opts: ["س = ٨", "س = ٢١", "س = ٢٧", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: س/٥ = ٦", opts: ["س = ٣٠", "س = ١١", "س = ١.٢", "س = ٢٥"], ans: 0 },
            { q: "إذا كانت س + ٨ = ٢٠، فإن س =", opts: ["١٢", "٢٨", "١٦٠", "٢.٥"], ans: 0 },
            { q: "إذا كانت ٧س = ٤٢، فإن س =", opts: ["٦", "٤٩", "٢٩٤", "٣٥"], ans: 0 },
            { q: "حل المعادلة: ص - ٣ = ١٠", opts: ["ص = ١٣", "ص = ٧", "ص = ٣٠", "ص = -٧"], ans: 0 },
            { q: "حل المعادلة: ٤م = ٣٦", opts: ["م = ٩", "م = ٤٠", "م = ٣٢", "م = ١٤٤"], ans: 0 },
            { q: "حل المعادلة: ن/٢ = ٨", opts: ["ن = ١٦", "ن = ٤", "ن = ١٠", "ن = ٦"], ans: 0 },
            { q: "إذا كانت س + ١٢ = ٣٠، فإن س =", opts: ["١٨", "٤٢", "٢.٥", "٣٦٠"], ans: 0 }
        ],
        u4l2: [ // حل معادلة الدرجة الأولى (خطوتين)
            { q: "حل المعادلة: ٢س + ٣ = ٩", opts: ["س = ٣", "س = ٦", "س = ١٢", "س = ٢٤"], ans: 0 },
            { q: "حل المعادلة: ٣س - ٥ = ٧", opts: ["س = ٤", "س = ٢", "س = ١٢", "س = ٣٦"], ans: 0 },
            { q: "حل المعادلة: ٤س + ٧ = ١٩", opts: ["س = ٣", "س = ١٢", "س = ٢٦", "س = ٦.٥"], ans: 0 },
            { q: "حل المعادلة: ٥س - ٢ = ١٣", opts: ["س = ٣", "س = ١١", "س = ١٥", "س = ٥٥"], ans: 0 },
            { q: "إذا كانت ٢س + ٥ = ١٥، فإن س =", opts: ["٥", "١٠", "٢٠", "٣"], ans: 0 },
            { q: "إذا كانت ٣س - ٤ = ٨، فإن س =", opts: ["٤", "١٢", "٣", "٢٤"], ans: 0 },
            { q: "حل المعادلة: ٦س + ١ = ٣١", opts: ["س = ٥", "س = ٣٠", "س = ٣٢", "س = ١.٨"], ans: 0 },
            { q: "حل المعادلة: ٧س - ٨ = ١٣", opts: ["س = ٣", "س = ٢١", "س = ٥", "س = ١٠٥"], ans: 0 },
            { q: "حل المعادلة: ٨س + ٤ = ٢٠", opts: ["س = ٢", "س = ١٦", "س = ٢٤", "س = ٣"], ans: 0 },
            { q: "إذا كانت ٤س + ٩ = ٢٥، فإن س =", opts: ["٤", "١٦", "٣٤", "٦"], ans: 0 }
        ],
        u4l3: [ // معادلات تحتوي أقواس
            { q: "حل المعادلة: ٢(س + ٣) = ١٠", opts: ["س = ٢", "س = ٧", "س = ٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: ٣(س - ٢) = ١٢", opts: ["س = ٦", "س = ١٠", "س = ٤", "س = ٣٨"], ans: 0 },
            { q: "حل المعادلة: ٤(٢س + ١) = ٢٠", opts: ["س = ٢", "س = ٤", "س = ٦", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٣) = ٢٠", opts: ["س = ٧", "س = ٤", "س = ٨", "س = ٢٣"], ans: 0 },
            { q: "إذا كانت ٢(٣س - ١) = ١٦، فإن س =", opts: ["٣", "٥", "٤", "٢"], ans: 0 },
            { q: "إذا كانت ٤(س + ٥) = ٢٨، فإن س =", opts: ["٢", "٧", "١٢", "٣"], ans: 0 },
            { q: "حل المعادلة: ٣(س + ٢) - ٤ = ١١", opts: ["س = ٣", "س = ٥", "س = ٤", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: ٢(٢س - ١) + ٣ = ١٣", opts: ["س = ٣", "س = ٤", "س = ٢", "س = ٥"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٢) = ٣س + ٤", opts: ["س = ٧", "س = ٦", "س = ٥", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: ٢(س + ٣) = ٣(س - ١)", opts: ["س = ٩", "س = ٦", "س = ٣", "س = ١٢"], ans: 0 }
        ],
        u4l4: [ // معادلات تحتوي كسور
            { q: "حل المعادلة: س/٢ + ٣ = ٥", opts: ["س = ٤", "س = ١", "س = ٢", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: (س/٣) - ٢ = ١", opts: ["س = ٩", "س = ٣", "س = ١", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: ٢س/٥ = ٤", opts: ["س = ١٠", "س = ٢.٥", "س = ٢٠", "س = ٤٠"], ans: 0 },
            { q: "حل المعادلة: (س + ١)/٢ = ٣", opts: ["س = ٥", "س = ٧", "س = ٦", "س = ٢"], ans: 0 },
            { q: "إذا كانت (س/٤) + ١ = ٣، فإن س =", opts: ["٨", "١٦", "٤", "١٢"], ans: 0 },
            { q: "إذا كانت (٢س)/٣ = ٨، فإن س =", opts: ["١٢", "٢٤", "٦", "٨"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)/٣ = ٤", opts: ["س = ١٤", "س = ١٠", "س = ١٢", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: (٣س)/٥ = ٩", opts: ["س = ١٥", "س = ٢٧", "س = ٣", "س = ٤٥"], ans: 0 },
            { q: "حل المعادلة: (س/٢) + (س/٣) = ٥", opts: ["س = ٦", "س = ١٠", "س = ١٢", "س = ٣٠"], ans: 0 },
            { q: "حل المعادلة: (٢س - ١)/٣ = ٥", opts: ["س = ٨", "س = ٧", "س = ٩", "س = ٦"], ans: 0 }
        ],
        u4l5: [ // تطبيقات على المعادلات (مسائل)
            { q: "مجموع عدد و ٥ يساوي ١٢، ما العدد؟", opts: ["٧", "١٧", "٦٠", "٢"], ans: 0 },
            { q: "ثلاثة أمثال عدد تساوي ٢٤، ما العدد؟", opts: ["٨", "٢١", "٢٧", "١٢"], ans: 0 },
            { q: "إذا كان عمر أحمد ١٢ سنة، وعمر أخيه ضعف عمره، فما مجموع عمريهما؟", opts: ["٣٦", "٢٤", "١٢", "٤٨"], ans: 0 },
            { q: "اشترى محمد ٣ كتب بـ ٢٠ جنيهاً، ودفتر بـ ٥ جنيهات. كم دفع؟", opts: ["٦٥", "٢٥", "٣٠", "٣٥"], ans: 0 },
            { q: "مستطيل طوله يزيد عن عرضه بمقدار ٣ سم، ومحيطه ٢٢ سم، فما طوله؟", opts: ["٧ سم", "٥ سم", "٤ سم", "٨ سم"], ans: 0 },
            { q: "عدد إذا أضفت إليه ٨ ثم ضاعفت الناتج تحصل على ٣٠، ما العدد؟", opts: ["٧", "٦", "٨", "٩"], ans: 0 },
            { q: "سعر قلم ٥ جنيهات، وسعر دفتر ١٠ جنيهات، كم ثمن ٣ أقلام ودفترين؟", opts: ["٣٥", "٢٥", "٤٠", "٣٠"], ans: 0 },
            { q: "إذا كان مجموع ثلاثة أعداد متتالية هو ٣٠، فما أصغرها؟", opts: ["٩", "١٠", "١١", "٨"], ans: 0 },
            { q: "عمر أميرة يساوي ضعف عمر أختها، ومجموع عمريهما ٢٧ سنة، فما عمر أختها؟", opts: ["٩", "١٨", "٢٧", "١٣.٥"], ans: 0 },
            { q: "اشترى خالد ٨ دفاتر بسعر ٦ ريالات للدفتر، ودفع ثمنها بـ ١٠٠ ريال، كم الباقي؟", opts: ["٥٢", "٤٨", "٦٨", "٧٢"], ans: 0 }
        ],
        u4l6: [ // معادلات الدرجة الثانية (بسيطة)
            { q: "حل المعادلة: س² = ٩", opts: ["س = ٣ أو -٣", "س = ٣", "س = -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² = ١٦", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² = ٢٥", opts: ["س = ٥ أو -٥", "س = ٥", "س = -٥", "س = ٢٥"], ans: 0 },
            { q: "حل المعادلة: ٢س² = ٣٢", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠", opts: ["س = ٢ أو -٢", "س = ٢", "س = -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤٩ = ٠", opts: ["س = ٧ أو -٧", "س = ٧", "س = -٧", "س = ٤٩"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)² = ٠", opts: ["س = ٢", "س = -٢", "س = ٢ أو -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² + ٦س + ٩ = ٠", opts: ["س = -٣", "س = ٣", "س = ٣ أو -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² - ١٠س + ٢٥ = ٠", opts: ["س = ٥", "س = -٥", "س = ٥ أو -٥", "س = ٢٥"], ans: 0 },
            { q: "مجموعة حل المعادلة س² = ٣٦ هي", opts: ["{٦، -٦}", "{٦}", "{-٦}", "{٣٦}"], ans: 0 }
        ],
        u4l7: [ // حل معادلات باستخدام التحليل
            { q: "حل المعادلة: س² + ٥س + ٦ = ٠", opts: ["س = -٢ أو -٣", "س = ٢ أو ٣", "س = -٥ أو -١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٥س + ٦ = ٠", opts: ["س = ٢ أو ٣", "س = -٢ أو -٣", "س = ٥ أو ١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² + ٧س + ١٠ = ٠", opts: ["س = -٢ أو -٥", "س = ٢ أو ٥", "س = -٧ أو -١٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² - ٨س + ١٥ = ٠", opts: ["س = ٣ أو ٥", "س = -٣ أو -٥", "س = ٨ أو ١٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠ باستخدام التحليل", opts: ["(س-٢)(س+٢)=٠، س=٢ أو -٢", "س=٢", "س=-٢", "س=٤"], ans: 0 },
            { q: "حل المعادلة: ٢س² + ٧س + ٣ = ٠", opts: ["س = -١/٢ أو -٣", "س = ١/٢ أو ٣", "س = -٢ أو -٣", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٣س² + ١٠س + ٨ = ٠", opts: ["س = -٤/٣ أو -٢", "س = ٤/٣ أو ٢", "س = -٢ أو -٤", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: س² - ٩س + ٢٠ = ٠", opts: ["س = ٤ أو ٥", "س = -٤ أو -٥", "س = ٩ أو ٢٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² + س - ١٢ = ٠", opts: ["س = -٤ أو ٣", "س = ٤ أو -٣", "س = ١ أو -١٢", "س = ١٢"], ans: 0 },
            { q: "مجموعة حل المعادلة س² - ٣س - ١٠ = ٠ هي", opts: ["{٥، -٢}", "{٢، -٥}", "{٥، ٢}", "{-٥، -٢}"], ans: 0 }
        ]
    };        u3l3: [ // قسمة الأعداد الحقيقية
            { q: "√١٢ ÷ √٣ =", opts: ["√٤ = ٢", "٢", "٤", "√٩"], ans: 0 },
            { q: "١٠√٥ ÷ ٢√٥ =", opts: ["٥", "٥√٥", "٢٠", "١٢"], ans: 0 },
            { q: "√١٨ ÷ √٢ =", opts: ["√٩ = ٣", "٣", "٩", "٦"], ans: 0 },
            { q: "(√٥٠) ÷ (√٢) =", opts: ["√٢٥ = ٥", "٥", "٢٥", "١٠"], ans: 0 },
            { q: "٦√٣ ÷ ٢√٣ =", opts: ["٣", "٣√٣", "١٢", "٤"], ans: 0 },
            { q: "√(٢٧/٣) =", opts: ["√٩ = ٣", "٣", "٩", "٢٧"], ans: 0 },
            { q: "(٤√٦) ÷ (٢√٣) =", opts: ["٢√٢", "٢", "٨√٢", "٢√١٨"], ans: 0 },
            { q: "√٨١ ÷ √٩ =", opts: ["٩ ÷ ٣ = ٣", "٣", "٧٢", "٩"], ans: 0 },
            { q: "١٠ ÷ √٥ = (بترشيح المقام)", opts: ["١٠√٥ / ٥ = ٢√٥", "٢√٥", "√٢", "٢٠"], ans: 0 },
            { q: "إذا كان س = √٢٠، ص = √٥، فما س ÷ ص؟", opts: ["٢", "٤", "√٤ = ٢", "√١٥"], ans: 0 }
        ],
        u3l4: [ // الترتيب والعمليات
            { q: "رتب الأعداد تصاعدياً: √٤، √٩، √١٦", opts: ["٢، ٣، ٤", "٤، ٣، ٢", "٤، ٢، ٣", "٢، ٤، ٣"], ans: 0 },
            { q: "أي الأعداد أكبر: √٣٥ أم ٦؟", opts: ["√٣٥ ≈ ٥.٩، إذاً ٦ أكبر", "٦", "√٣٥", "متساويان"], ans: 0 },
            { q: "احسب: ٢ + ٣ × ٤", opts: ["٢ + ١٢ = ١٤", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "احسب: (٢ + ٣) × ٤", opts: ["٥ × ٤ = ٢٠", "٢٠", "١٤", "٢٤"], ans: 0 },
            { q: "إذا كان أ = ٣، ب = ٢، فاحسب أ² + ب", opts: ["٩ + ٢ = ١١", "١١", "١٣", "٧"], ans: 0 },
            { q: "رتب الأعداد تنازلياً: ٥، √٢٧، √٨", opts: ["٥، √٢٧، √٨", "√٢٧، ٥، √٨", "٥، √٨، √٢٧", "√٢٧، √٨، ٥"], ans: 0 },
            { q: "أي الأعداد أصغر: √٨ أم ٣؟", opts: ["√٨ ≈ ٢.٨، إذاً √٨ أصغر", "٣", "√٨", "متساويان"], ans: 0 },
            { q: "احسب: ١٠ - ٤ ÷ ٢", opts: ["١٠ - ٢ = ٨", "٨", "٣", "١٢"], ans: 0 },
            { q: "احسب: ٤² - ٤", opts: ["١٦ - ٤ = ١٢", "١٢", "٤", "٠"], ans: 0 },
            { q: "قارن: √(٧+٩) و √٧ + √٩", opts: ["√١٦ = ٤، √٧ + √٩ ≈ ٢.٦ + ٣ = ٥.٦، الثاني أكبر", "الثاني أكبر", "الأول أكبر", "متساويان"], ans: 0 }
        ],
        u3l5: [ // خواص العمليات
            { q: "خاصية الإبدال في الجمع تعني:", opts: ["أ + ب = ب + أ", "أ + (ب + جـ) = (أ + ب) + جـ", "أ + ٠ = أ", "أ + (-أ) = ٠"], ans: 0 },
            { q: "خاصية التجميع في الضرب تعني:", opts: ["(أ × ب) × جـ = أ × (ب × جـ)", "أ × ب = ب × أ", "أ × ١ = أ", "أ × ٠ = ٠"], ans: 0 },
            { q: "العنصر المحايد في الجمع هو:", opts: ["٠", "١", "-١", "لا يوجد"], ans: 0 },
            { q: "العنصر المحايد في الضرب هو:", opts: ["١", "٠", "-١", "لا يوجد"], ans: 0 },
            { q: "خاصية التوزيع تعني:", opts: ["أ × (ب + جـ) = أ×ب + أ×جـ", "أ + (ب × جـ) = (أ+ب)×(أ+جـ)", "أ × (ب - جـ) = أ×ب - أ×جـ", "أ و ب صحيحتان"], ans: 0 },
            { q: "نظير ٥ الجمعي هو:", opts: ["-٥", "١/٥", "٠", "٥"], ans: 0 },
            { q: "نظير ٣ الضربي هو:", opts: ["١/٣", "-٣", "٠", "٣"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الجمع عملية إبدالية", "الطرح عملية إبدالية", "القسمة عملية إبدالية", "جميع ما سبق"], ans: 0 },
            { q: "أي العبارات التالية صحيحة؟", opts: ["الضرب عملية تجميعية", "الضرب عملية إبدالية", "للضرب عنصر محايد", "جميع ما سبق"], ans: 3 },
            { q: "٣ × (٥ - ٢) = (٣×٥) - (٣×٢) تمثل خاصية", opts: ["التوزيع", "الإبدال", "الدمج", "المحايد"], ans: 0 }
        ],

        // ========== الوحدة 4 ==========
        u4l1: [ // حل معادلة الدرجة الأولى (خطوة واحدة)
            { q: "حل المعادلة: س + ٥ = ١٢", opts: ["س = ٧", "س = ١٧", "س = ٦٠", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: س - ٤ = ٩", opts: ["س = ١٣", "س = ٥", "س = ٣٦", "س = -٥"], ans: 0 },
            { q: "حل المعادلة: ٣س = ٢٤", opts: ["س = ٨", "س = ٢١", "س = ٢٧", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: س/٥ = ٦", opts: ["س = ٣٠", "س = ١١", "س = ١.٢", "س = ٢٥"], ans: 0 },
            { q: "إذا كانت س + ٨ = ٢٠، فإن س =", opts: ["١٢", "٢٨", "١٦٠", "٢.٥"], ans: 0 },
            { q: "إذا كانت ٧س = ٤٢، فإن س =", opts: ["٦", "٤٩", "٢٩٤", "٣٥"], ans: 0 },
            { q: "حل المعادلة: ص - ٣ = ١٠", opts: ["ص = ١٣", "ص = ٧", "ص = ٣٠", "ص = -٧"], ans: 0 },
            { q: "حل المعادلة: ٤م = ٣٦", opts: ["م = ٩", "م = ٤٠", "م = ٣٢", "م = ١٤٤"], ans: 0 },
            { q: "حل المعادلة: ن/٢ = ٨", opts: ["ن = ١٦", "ن = ٤", "ن = ١٠", "ن = ٦"], ans: 0 },
            { q: "إذا كانت س + ١٢ = ٣٠، فإن س =", opts: ["١٨", "٤٢", "٢.٥", "٣٦٠"], ans: 0 }
        ],
        u4l2: [ // حل معادلة الدرجة الأولى (خطوتين)
            { q: "حل المعادلة: ٢س + ٣ = ٩", opts: ["س = ٣", "س = ٦", "س = ١٢", "س = ٢٤"], ans: 0 },
            { q: "حل المعادلة: ٣س - ٥ = ٧", opts: ["س = ٤", "س = ٢", "س = ١٢", "س = ٣٦"], ans: 0 },
            { q: "حل المعادلة: ٤س + ٧ = ١٩", opts: ["س = ٣", "س = ١٢", "س = ٢٦", "س = ٦.٥"], ans: 0 },
            { q: "حل المعادلة: ٥س - ٢ = ١٣", opts: ["س = ٣", "س = ١١", "س = ١٥", "س = ٥٥"], ans: 0 },
            { q: "إذا كانت ٢س + ٥ = ١٥، فإن س =", opts: ["٥", "١٠", "٢٠", "٣"], ans: 0 },
            { q: "إذا كانت ٣س - ٤ = ٨، فإن س =", opts: ["٤", "١٢", "٣", "٢٤"], ans: 0 },
            { q: "حل المعادلة: ٦س + ١ = ٣١", opts: ["س = ٥", "س = ٣٠", "س = ٣٢", "س = ١.٨"], ans: 0 },
            { q: "حل المعادلة: ٧س - ٨ = ١٣", opts: ["س = ٣", "س = ٢١", "س = ٥", "س = ١٠٥"], ans: 0 },
            { q: "حل المعادلة: ٨س + ٤ = ٢٠", opts: ["س = ٢", "س = ١٦", "س = ٢٤", "س = ٣"], ans: 0 },
            { q: "إذا كانت ٤س + ٩ = ٢٥، فإن س =", opts: ["٤", "١٦", "٣٤", "٦"], ans: 0 }
        ],
        u4l3: [ // معادلات تحتوي أقواس
            { q: "حل المعادلة: ٢(س + ٣) = ١٠", opts: ["س = ٢", "س = ٧", "س = ٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: ٣(س - ٢) = ١٢", opts: ["س = ٦", "س = ١٠", "س = ٤", "س = ٣٨"], ans: 0 },
            { q: "حل المعادلة: ٤(٢س + ١) = ٢٠", opts: ["س = ٢", "س = ٤", "س = ٦", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٣) = ٢٠", opts: ["س = ٧", "س = ٤", "س = ٨", "س = ٢٣"], ans: 0 },
            { q: "إذا كانت ٢(٣س - ١) = ١٦، فإن س =", opts: ["٣", "٥", "٤", "٢"], ans: 0 },
            { q: "إذا كانت ٤(س + ٥) = ٢٨، فإن س =", opts: ["٢", "٧", "١٢", "٣"], ans: 0 },
            { q: "حل المعادلة: ٣(س + ٢) - ٤ = ١١", opts: ["س = ٣", "س = ٥", "س = ٤", "س = ٢"], ans: 0 },
            { q: "حل المعادلة: ٢(٢س - ١) + ٣ = ١٣", opts: ["س = ٣", "س = ٤", "س = ٢", "س = ٥"], ans: 0 },
            { q: "حل المعادلة: ٥(س - ٢) = ٣س + ٤", opts: ["س = ٧", "س = ٦", "س = ٥", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: ٢(س + ٣) = ٣(س - ١)", opts: ["س = ٩", "س = ٦", "س = ٣", "س = ١٢"], ans: 0 }
        ],
        u4l4: [ // معادلات تحتوي كسور
            { q: "حل المعادلة: س/٢ + ٣ = ٥", opts: ["س = ٤", "س = ١", "س = ٢", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: (س/٣) - ٢ = ١", opts: ["س = ٩", "س = ٣", "س = ١", "س = ١٢"], ans: 0 },
            { q: "حل المعادلة: ٢س/٥ = ٤", opts: ["س = ١٠", "س = ٢.٥", "س = ٢٠", "س = ٤٠"], ans: 0 },
            { q: "حل المعادلة: (س + ١)/٢ = ٣", opts: ["س = ٥", "س = ٧", "س = ٦", "س = ٢"], ans: 0 },
            { q: "إذا كانت (س/٤) + ١ = ٣، فإن س =", opts: ["٨", "١٦", "٤", "١٢"], ans: 0 },
            { q: "إذا كانت (٢س)/٣ = ٨، فإن س =", opts: ["١٢", "٢٤", "٦", "٨"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)/٣ = ٤", opts: ["س = ١٤", "س = ١٠", "س = ١٢", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: (٣س)/٥ = ٩", opts: ["س = ١٥", "س = ٢٧", "س = ٣", "س = ٤٥"], ans: 0 },
            { q: "حل المعادلة: (س/٢) + (س/٣) = ٥", opts: ["س = ٦", "س = ١٠", "س = ١٢", "س = ٣٠"], ans: 0 },
            { q: "حل المعادلة: (٢س - ١)/٣ = ٥", opts: ["س = ٨", "س = ٧", "س = ٩", "س = ٦"], ans: 0 }
        ],
        u4l5: [ // تطبيقات على المعادلات (مسائل)
            { q: "مجموع عدد و ٥ يساوي ١٢، ما العدد؟", opts: ["٧", "١٧", "٦٠", "٢"], ans: 0 },
            { q: "ثلاثة أمثال عدد تساوي ٢٤، ما العدد؟", opts: ["٨", "٢١", "٢٧", "١٢"], ans: 0 },
            { q: "إذا كان عمر أحمد ١٢ سنة، وعمر أخيه ضعف عمره، فما مجموع عمريهما؟", opts: ["٣٦", "٢٤", "١٢", "٤٨"], ans: 0 },
            { q: "اشترى محمد ٣ كتب بـ ٢٠ جنيهاً، ودفتر بـ ٥ جنيهات. كم دفع؟", opts: ["٦٥", "٢٥", "٣٠", "٣٥"], ans: 0 },
            { q: "مستطيل طوله يزيد عن عرضه بمقدار ٣ سم، ومحيطه ٢٢ سم، فما طوله؟", opts: ["٧ سم", "٥ سم", "٤ سم", "٨ سم"], ans: 0 },
            { q: "عدد إذا أضفت إليه ٨ ثم ضاعفت الناتج تحصل على ٣٠، ما العدد؟", opts: ["٧", "٦", "٨", "٩"], ans: 0 },
            { q: "سعر قلم ٥ جنيهات، وسعر دفتر ١٠ جنيهات، كم ثمن ٣ أقلام ودفترين؟", opts: ["٣٥", "٢٥", "٤٠", "٣٠"], ans: 0 },
            { q: "إذا كان مجموع ثلاثة أعداد متتالية هو ٣٠، فما أصغرها؟", opts: ["٩", "١٠", "١١", "٨"], ans: 0 },
            { q: "عمر أميرة يساوي ضعف عمر أختها، ومجموع عمريهما ٢٧ سنة، فما عمر أختها؟", opts: ["٩", "١٨", "٢٧", "١٣.٥"], ans: 0 },
            { q: "اشترى خالد ٨ دفاتر بسعر ٦ ريالات للدفتر، ودفع ثمنها بـ ١٠٠ ريال، كم الباقي؟", opts: ["٥٢", "٤٨", "٦٨", "٧٢"], ans: 0 }
        ],
        u4l6: [ // معادلات الدرجة الثانية (بسيطة)
            { q: "حل المعادلة: س² = ٩", opts: ["س = ٣ أو -٣", "س = ٣", "س = -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² = ١٦", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² = ٢٥", opts: ["س = ٥ أو -٥", "س = ٥", "س = -٥", "س = ٢٥"], ans: 0 },
            { q: "حل المعادلة: ٢س² = ٣٢", opts: ["س = ٤ أو -٤", "س = ٤", "س = -٤", "س = ١٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠", opts: ["س = ٢ أو -٢", "س = ٢", "س = -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤٩ = ٠", opts: ["س = ٧ أو -٧", "س = ٧", "س = -٧", "س = ٤٩"], ans: 0 },
            { q: "حل المعادلة: (س - ٢)² = ٠", opts: ["س = ٢", "س = -٢", "س = ٢ أو -٢", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² + ٦س + ٩ = ٠", opts: ["س = -٣", "س = ٣", "س = ٣ أو -٣", "س = ٩"], ans: 0 },
            { q: "حل المعادلة: س² - ١٠س + ٢٥ = ٠", opts: ["س = ٥", "س = -٥", "س = ٥ أو -٥", "س = ٢٥"], ans: 0 },
            { q: "مجموعة حل المعادلة س² = ٣٦ هي", opts: ["{٦، -٦}", "{٦}", "{-٦}", "{٣٦}"], ans: 0 }
        ],
        u4l7: [ // حل معادلات باستخدام التحليل
            { q: "حل المعادلة: س² + ٥س + ٦ = ٠", opts: ["س = -٢ أو -٣", "س = ٢ أو ٣", "س = -٥ أو -١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² - ٥س + ٦ = ٠", opts: ["س = ٢ أو ٣", "س = -٢ أو -٣", "س = ٥ أو ١", "س = ٦"], ans: 0 },
            { q: "حل المعادلة: س² + ٧س + ١٠ = ٠", opts: ["س = -٢ أو -٥", "س = ٢ أو ٥", "س = -٧ أو -١٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² - ٨س + ١٥ = ٠", opts: ["س = ٣ أو ٥", "س = -٣ أو -٥", "س = ٨ أو ١٥", "س = ٤"], ans: 0 },
            { q: "حل المعادلة: س² - ٤ = ٠ باستخدام التحليل", opts: ["(س-٢)(س+٢)=٠، س=٢ أو -٢", "س=٢", "س=-٢", "س=٤"], ans: 0 },
            { q: "حل المعادلة: ٢س² + ٧س + ٣ = ٠", opts: ["س = -١/٢ أو -٣", "س = ١/٢ أو ٣", "س = -٢ أو -٣", "س = ٣"], ans: 0 },
            { q: "حل المعادلة: ٣س² + ١٠س + ٨ = ٠", opts: ["س = -٤/٣ أو -٢", "س = ٤/٣ أو ٢", "س = -٢ أو -٤", "س = ٨"], ans: 0 },
            { q: "حل المعادلة: س² - ٩س + ٢٠ = ٠", opts: ["س = ٤ أو ٥", "س = -٤ أو -٥", "س = ٩ أو ٢٠", "س = ١٠"], ans: 0 },
            { q: "حل المعادلة: س² + س - ١٢ = ٠", opts: ["س = -٤ أو ٣", "س = ٤ أو -٣", "س = ١ أو -١٢", "س = ١٢"], ans: 0 },
            { q: "مجموعة حل المعادلة س² - ٣س - ١٠ = ٠ هي", opts: ["{٥، -٢}", "{٢، -٥}", "{٥، ٢}", "{-٥، -٢}"], ans: 0 }
        ]
    };        // ========== الوحدة 5 ==========
        u5l1: [ // العلاقات (المجال والمدى)
            { q: "في العلاقة {(١،٢)، (٢،٣)، (٣،٤)}، المجال هو:", opts: ["{١،٢،٣}", "{٢،٣،٤}", "{(١،٢)}", "{١،٢،٣،٤}"], ans: 0 },
            { q: "في العلاقة {(١،٢)، (٢،٣)، (٣،٤)}، المدى هو:", opts: ["{٢،٣،٤}", "{١،٢،٣}", "{(٢،٣)}", "{١،٢،٣،٤}"], ans: 0 },
            { q: "إذا كانت العلاقة: س → ٢س، والمجال {١،٢،٣}، فالمدى =", opts: ["{٢،٤،٦}", "{١،٢،٣}", "{٣،٥،٧}", "{٢،٣،٤}"], ans: 0 },
            { q: "في العلاقة {(أ،٥)، (ب،٧)، (جـ،٩)}، المدى =", opts: ["{٥،٧،٩}", "{أ،ب،جـ}", "{(أ،٥)}", "{أ،ب،جـ،٥،٧،٩}"], ans: 0 },
            { q: "إذا كان المجال = {٢،٤،٦}، والقاعدة س → س + ١، فالمدى =", opts: ["{٣،٥،٧}", "{٢،٤،٦}", "{١،٢،٣}", "{٣،٤،٥}"], ans: 0 },
            { q: "عدد عناصر العلاقة {(١،١)، (٢،٤)، (٣،٩)} هو:", opts: ["٣", "٦", "٩", "٢"], ans: 0 },
            { q: "في العلاقة {(س،ص) | ص = س²، س∈{٠،١،٢}}، المدى =", opts: ["{٠،١،٤}", "{٠،١،٢}", "{٠،٢،٤}", "{١،٤}"], ans: 0 },
            { q: "أي من المجموعات التالية تمثل علاقة؟", opts: ["{(١،٢)، (٣،٤)}", "{١،٢،٣}", "{٢،٤،٦}", "جميع ما سبق"], ans: 0 },
            { q: "إذا كانت العلاقة دالة، فإن:", opts: ["لكل عنصر في المجال عنصر وحيد في المدى", "لكل عنصر في المدى عنصر وحيد في المجال", "المجال = المدى", "عدد العناصر متساو"], ans: 0 },
            { q: "أي من العلاقات التالية تمثل دالة؟", opts: ["{(١،٢)، (٢،٢)، (٣،٢)}", "{(١،٢)، (١،٣)، (٢،٤)}", "{(٢،١)، (٣،١)، (٢،٣)}", "{(١،٢)، (٢،٣)، (٢،٤)}"], ans: 0 }
        ],
        u5l2: [ // تمثيل العلاقات بيانياً
            { q: "النقطة (٢،٣) تقع في الربع:", opts: ["الأول", "الثاني", "الثالث", "الرابع"], ans: 0 },
            { q: "النقطة (-٣،٤) تقع في الربع:", opts: ["الثاني", "الأول", "الثالث", "الرابع"], ans: 0 },
            { q: "النقطة (-٢،-٥) تقع في الربع:", opts: ["الثالث", "الثاني", "الأول", "الرابع"], ans: 0 },
            { q: "النقطة (٤،-٣) تقع في الربع:", opts: ["الرابع", "الثالث", "الثاني", "الأول"], ans: 0 },
            { q: "إحداثيات نقطة الأصل هي:", opts: ["(٠،٠)", "(١،١)", "(٠،١)", "(١،٠)"], ans: 0 },
            { q: "المسافة بين النقطتين (١،٢) و (١،٥) =", opts: ["٣", "٤", "٥", "٦"], ans: 0 },
            { q: "المسافة بين النقطتين (٢،٣) و (٥،٣) =", opts: ["٣", "٤", "٥", "٦"], ans: 0 },
            { q: "تمثيل العلاقة {(١،٢)، (٢،٣)، (٣،٤)} على المستوى البياني يعطي:", opts: ["نقاطاً متفرقة", "خطاً مستقيماً", "منحنى", "دائرة"], ans: 0 },
            { q: "أي نقطة تقع على محور السينات؟", opts: ["(٣،٠)", "(٠،٣)", "(-٣،٣)", "(٣،-٣)"], ans: 0 },
            { q: "أي نقطة تقع على محور الصادات؟", opts: ["(٠،٤)", "(٤،٠)", "(-٤،٤)", "(٤،-٤)"], ans: 0 }
        ],
        u5l3: [ // الدوال (مقدمة)
            { q: "إذا كانت د(س) = ٢س + ١، فإن د(٣) =", opts: ["٧", "٥", "٦", "٨"], ans: 0 },
            { q: "إذا كانت د(س) = س²، فإن د(٤) =", opts: ["١٦", "٨", "٢", "٤"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س - ٢، فإن د(٠) =", opts: ["-٢", "٢", "٠", "٣"], ans: 0 },
            { q: "إذا كانت د(س) = ٥، فإن د(١٠) =", opts: ["٥", "١٠", "١٥", "٥٠"], ans: 0 },
            { q: "إذا كانت د(س) = س + ٣، فإن د(٢) + د(١) =", opts: ["(٥) + (٤) = ٩", "٩", "١٠", "١١"], ans: 0 },
            { q: "إذا كانت د(س) = ٢س²، فإن د(٣) =", opts: ["١٨", "١٢", "٦", "٣٦"], ans: 0 },
            { q: "إذا كانت د(س) = ٤س - ١، جد د(٢) - د(١)", opts: ["(٧) - (٣) = ٤", "٤", "٥", "٦"], ans: 0 },
            { q: "إذا كانت د(س) = ٩ - س، فإن د(٥) =", opts: ["٤", "١٤", "-٤", "٩"], ans: 0 },
            { q: "الدالة الخطية تكون على الصورة:", opts: ["د(س) = أ س + ب", "د(س) = س²", "د(س) = |س|", "د(س) = ١/س"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س، فإن د(س + ١) =", opts: ["٣س + ٣", "٣س + ١", "٣س + ٣", "٣س + ٣"], ans: 0 }
        ],
        u5l4: [ // تطبيقات على الدوال
            { q: "إذا كانت د(س) = ٢س + ٣، فأوجد د(٤) - د(٢)", opts: ["١١ - ٧ = ٤", "٤", "٥", "٦"], ans: 0 },
            { q: "دالة تعبر عن مساحة مربع طول ضلعه س هي:", opts: ["د(س) = س²", "د(س) = ٤س", "د(س) = س + س", "د(س) = ٢س"], ans: 0 },
            { q: "دالة تعبر عن محيط مربع طول ضلعه س هي:", opts: ["د(س) = ٤س", "د(س) = س²", "د(س) = ٢س", "د(س) = س + ٤"], ans: 0 },
            { q: "إذا كانت د(س) = ١٠ - ٢س، فإن د(٣) =", opts: ["٤", "١٦", "-٤", "١٠"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س - ٥، فأوجد قيمة س عندما د(س) = ١", opts: ["س = ٢", "س = ٤", "س = ٦", "س = -٢"], ans: 0 },
            { q: "إذا كانت د(س) = ٨ - س، جد د(٢) × د(١)", opts: ["٦ × ٧ = ٤٢", "٤٢", "٤٠", "٤٨"], ans: 0 },
            { q: "دالة تعبر عن مساحة مستطيل طوله ضعف عرضه (س) هي:", opts: ["د(س) = ٢س²", "د(س) = ٢س", "د(س) = س²", "د(س) = ٤س"], ans: 0 },
            { q: "إذا كانت د(س) = س + ٢، فإن مدى الدالة عندما المجال {٠،١،٢} هو:", opts: ["{٢،٣،٤}", "{٠،١،٢}", "{٢،٣،٤}", "{٢،٤،٦}"], ans: 0 },
            { q: "إذا كانت د(س) = ٤س - ١، ود(س) = ١١، فإن س =", opts: ["٣", "٤", "٥", "٢"], ans: 0 },
            { q: "أي من التالي يمثل دالة خطية؟", opts: ["د(س) = ٥س + ٣", "د(س) = س²", "د(س) = |س|", "د(س) = ٦"], ans: 0 }
        ]
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
        startTimer();
        try { localStorage.setItem('mathPrep1User', username); } catch (e) {}
        saveState();
        showMap();
    };

    window.resetUser = function() {
        pauseTimer();
        try { localStorage.removeItem('mathPrep1User'); } catch (e) {}
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

    // ===== 12. دوال الخريطة والدروس (بدون قفل) =====
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
            // جميع الجزر مفتوحة (لا يوجد قفل)
            const completedCount = island.lessons.filter((_, i) => gameState.completedLessons.includes(idx + '-' + i)).length;
            const pct = (completedCount / island.lessons.length) * 100;
            const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';
            return `
                <div class="island-card" style="--c1:${island.c1};--c2:${island.c2}" onclick="showLessons(${idx})">
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
    window.completeActivity = completeActivity;        // ========== الوحدة 5 ==========
        u5l1: [ // العلاقات (المجال والمدى)
            { q: "في العلاقة {(١،٢)، (٢،٣)، (٣،٤)}، المجال هو:", opts: ["{١،٢،٣}", "{٢،٣،٤}", "{(١،٢)}", "{١،٢،٣،٤}"], ans: 0 },
            { q: "في العلاقة {(١،٢)، (٢،٣)، (٣،٤)}، المدى هو:", opts: ["{٢،٣،٤}", "{١،٢،٣}", "{(٢،٣)}", "{١،٢،٣،٤}"], ans: 0 },
            { q: "إذا كانت العلاقة: س → ٢س، والمجال {١،٢،٣}، فالمدى =", opts: ["{٢،٤،٦}", "{١،٢،٣}", "{٣،٥،٧}", "{٢،٣،٤}"], ans: 0 },
            { q: "في العلاقة {(أ،٥)، (ب،٧)، (جـ،٩)}، المدى =", opts: ["{٥،٧،٩}", "{أ،ب،جـ}", "{(أ،٥)}", "{أ،ب،جـ،٥،٧،٩}"], ans: 0 },
            { q: "إذا كان المجال = {٢،٤،٦}، والقاعدة س → س + ١، فالمدى =", opts: ["{٣،٥،٧}", "{٢،٤،٦}", "{١،٢،٣}", "{٣،٤،٥}"], ans: 0 },
            { q: "عدد عناصر العلاقة {(١،١)، (٢،٤)، (٣،٩)} هو:", opts: ["٣", "٦", "٩", "٢"], ans: 0 },
            { q: "في العلاقة {(س،ص) | ص = س²، س∈{٠،١،٢}}، المدى =", opts: ["{٠،١،٤}", "{٠،١،٢}", "{٠،٢،٤}", "{١،٤}"], ans: 0 },
            { q: "أي من المجموعات التالية تمثل علاقة؟", opts: ["{(١،٢)، (٣،٤)}", "{١،٢،٣}", "{٢،٤،٦}", "جميع ما سبق"], ans: 0 },
            { q: "إذا كانت العلاقة دالة، فإن:", opts: ["لكل عنصر في المجال عنصر وحيد في المدى", "لكل عنصر في المدى عنصر وحيد في المجال", "المجال = المدى", "عدد العناصر متساو"], ans: 0 },
            { q: "أي من العلاقات التالية تمثل دالة؟", opts: ["{(١،٢)، (٢،٢)، (٣،٢)}", "{(١،٢)، (١،٣)، (٢،٤)}", "{(٢،١)، (٣،١)، (٢،٣)}", "{(١،٢)، (٢،٣)، (٢،٤)}"], ans: 0 }
        ],
        u5l2: [ // تمثيل العلاقات بيانياً
            { q: "النقطة (٢،٣) تقع في الربع:", opts: ["الأول", "الثاني", "الثالث", "الرابع"], ans: 0 },
            { q: "النقطة (-٣،٤) تقع في الربع:", opts: ["الثاني", "الأول", "الثالث", "الرابع"], ans: 0 },
            { q: "النقطة (-٢،-٥) تقع في الربع:", opts: ["الثالث", "الثاني", "الأول", "الرابع"], ans: 0 },
            { q: "النقطة (٤،-٣) تقع في الربع:", opts: ["الرابع", "الثالث", "الثاني", "الأول"], ans: 0 },
            { q: "إحداثيات نقطة الأصل هي:", opts: ["(٠،٠)", "(١،١)", "(٠،١)", "(١،٠)"], ans: 0 },
            { q: "المسافة بين النقطتين (١،٢) و (١،٥) =", opts: ["٣", "٤", "٥", "٦"], ans: 0 },
            { q: "المسافة بين النقطتين (٢،٣) و (٥،٣) =", opts: ["٣", "٤", "٥", "٦"], ans: 0 },
            { q: "تمثيل العلاقة {(١،٢)، (٢،٣)، (٣،٤)} على المستوى البياني يعطي:", opts: ["نقاطاً متفرقة", "خطاً مستقيماً", "منحنى", "دائرة"], ans: 0 },
            { q: "أي نقطة تقع على محور السينات؟", opts: ["(٣،٠)", "(٠،٣)", "(-٣،٣)", "(٣،-٣)"], ans: 0 },
            { q: "أي نقطة تقع على محور الصادات؟", opts: ["(٠،٤)", "(٤،٠)", "(-٤،٤)", "(٤،-٤)"], ans: 0 }
        ],
        u5l3: [ // الدوال (مقدمة)
            { q: "إذا كانت د(س) = ٢س + ١، فإن د(٣) =", opts: ["٧", "٥", "٦", "٨"], ans: 0 },
            { q: "إذا كانت د(س) = س²، فإن د(٤) =", opts: ["١٦", "٨", "٢", "٤"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س - ٢، فإن د(٠) =", opts: ["-٢", "٢", "٠", "٣"], ans: 0 },
            { q: "إذا كانت د(س) = ٥، فإن د(١٠) =", opts: ["٥", "١٠", "١٥", "٥٠"], ans: 0 },
            { q: "إذا كانت د(س) = س + ٣، فإن د(٢) + د(١) =", opts: ["(٥) + (٤) = ٩", "٩", "١٠", "١١"], ans: 0 },
            { q: "إذا كانت د(س) = ٢س²، فإن د(٣) =", opts: ["١٨", "١٢", "٦", "٣٦"], ans: 0 },
            { q: "إذا كانت د(س) = ٤س - ١، جد د(٢) - د(١)", opts: ["(٧) - (٣) = ٤", "٤", "٥", "٦"], ans: 0 },
            { q: "إذا كانت د(س) = ٩ - س، فإن د(٥) =", opts: ["٤", "١٤", "-٤", "٩"], ans: 0 },
            { q: "الدالة الخطية تكون على الصورة:", opts: ["د(س) = أ س + ب", "د(س) = س²", "د(س) = |س|", "د(س) = ١/س"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س، فإن د(س + ١) =", opts: ["٣س + ٣", "٣س + ١", "٣س + ٣", "٣س + ٣"], ans: 0 }
        ],
        u5l4: [ // تطبيقات على الدوال
            { q: "إذا كانت د(س) = ٢س + ٣، فأوجد د(٤) - د(٢)", opts: ["١١ - ٧ = ٤", "٤", "٥", "٦"], ans: 0 },
            { q: "دالة تعبر عن مساحة مربع طول ضلعه س هي:", opts: ["د(س) = س²", "د(س) = ٤س", "د(س) = س + س", "د(س) = ٢س"], ans: 0 },
            { q: "دالة تعبر عن محيط مربع طول ضلعه س هي:", opts: ["د(س) = ٤س", "د(س) = س²", "د(س) = ٢س", "د(س) = س + ٤"], ans: 0 },
            { q: "إذا كانت د(س) = ١٠ - ٢س، فإن د(٣) =", opts: ["٤", "١٦", "-٤", "١٠"], ans: 0 },
            { q: "إذا كانت د(س) = ٣س - ٥، فأوجد قيمة س عندما د(س) = ١", opts: ["س = ٢", "س = ٤", "س = ٦", "س = -٢"], ans: 0 },
            { q: "إذا كانت د(س) = ٨ - س، جد د(٢) × د(١)", opts: ["٦ × ٧ = ٤٢", "٤٢", "٤٠", "٤٨"], ans: 0 },
            { q: "دالة تعبر عن مساحة مستطيل طوله ضعف عرضه (س) هي:", opts: ["د(س) = ٢س²", "د(س) = ٢س", "د(س) = س²", "د(س) = ٤س"], ans: 0 },
            { q: "إذا كانت د(س) = س + ٢، فإن مدى الدالة عندما المجال {٠،١،٢} هو:", opts: ["{٢،٣،٤}", "{٠،١،٢}", "{٢،٣،٤}", "{٢،٤،٦}"], ans: 0 },
            { q: "إذا كانت د(س) = ٤س - ١، ود(س) = ١١، فإن س =", opts: ["٣", "٤", "٥", "٢"], ans: 0 },
            { q: "أي من التالي يمثل دالة خطية؟", opts: ["د(س) = ٥س + ٣", "د(س) = س²", "د(س) = |س|", "د(س) = ٦"], ans: 0 }
        ]
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
        startTimer();
        try { localStorage.setItem('mathPrep1User', username); } catch (e) {}
        saveState();
        showMap();
    };

    window.resetUser = function() {
        pauseTimer();
        try { localStorage.removeItem('mathPrep1User'); } catch (e) {}
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

    // ===== 12. دوال الخريطة والدروس (بدون قفل) =====
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
            // جميع الجزر مفتوحة (لا يوجد قفل)
            const completedCount = island.lessons.filter((_, i) => gameState.completedLessons.includes(idx + '-' + i)).length;
            const pct = (completedCount / island.lessons.length) * 100;
            const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';
            return `
                <div class="island-card" style="--c1:${island.c1};--c2:${island.c2}" onclick="showLessons(${idx})">
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
    window.completeActivity = completeActivity;    function showSuccess(xp, isFirstTime = true) {
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
        pauseTimer();
        const totalTime = getTotalTime();
        const totalCompleted = gameState.completedLessons.length;
        const total = gameState.totalLessonsCount;
        const totalXP = gameState.xp;
        const level = gameState.level;
        const pct = (totalCompleted / total) * 100;
        const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';

        let timeBonus = 0;
        if (totalTime < 1800) timeBonus = 100;
        else if (totalTime < 3600) timeBonus = 50;
        else timeBonus = 10;

        const finalXP = totalXP + timeBonus;

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
            const savedUser = localStorage.getItem('mathPrep1User');
            if (savedUser && savedUser.trim()) {
                gameState.currentUser = savedUser;
                document.getElementById('registerForm').style.display = 'none';
                document.getElementById('welcomeBack').style.display = 'block';
                document.getElementById('welcomeName').textContent = '👋 أهلاً يا ' + savedUser + '!';
                if (gameState.startTime) {
                    gameState.sessionStart = Date.now();
                }
            }
        } catch (e) {}
    };

    window.addEventListener('beforeunload', function() {
        pauseTimer();
    });
</script>

</body>
</html>    function showSuccess(xp, isFirstTime = true) {
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
        pauseTimer();
        const totalTime = getTotalTime();
        const totalCompleted = gameState.completedLessons.length;
        const total = gameState.totalLessonsCount;
        const totalXP = gameState.xp;
        const level = gameState.level;
        const pct = (totalCompleted / total) * 100;
        const stars = pct >= 100 ? '⭐⭐⭐' : pct >= 60 ? '⭐⭐' : pct > 0 ? '⭐' : '☆☆☆';

        let timeBonus = 0;
        if (totalTime < 1800) timeBonus = 100;
        else if (totalTime < 3600) timeBonus = 50;
        else timeBonus = 10;

        const finalXP = totalXP + timeBonus;

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
            const savedUser = localStorage.getItem('mathPrep1User');
            if (savedUser && savedUser.trim()) {
                gameState.currentUser = savedUser;
                document.getElementById('registerForm').style.display = 'none';
                document.getElementById('welcomeBack').style.display = 'block';
                document.getElementById('welcomeName').textContent = '👋 أهلاً يا ' + savedUser + '!';
                if (gameState.startTime) {
                    gameState.sessionStart = Date.now();
                }
            }
        } catch (e) {}
    };

    window.addEventListener('beforeunload', function() {
        pauseTimer();
    });
</script>

</body>
</html>
