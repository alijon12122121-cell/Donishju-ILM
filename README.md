<!DOCTYPE html>
<html lang="tg">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Донишҷӯ-Илм | КИТК 2026</title>
    <style>
        :root {
            --glass: rgba(255, 255, 255, 0.08);
            --border: rgba(255, 255, 255, 0.2);
            --accent: #6366f1;
            --gold: #fbbf24;
        }

        body {
            margin: 0; font-family: 'Segoe UI', Roboto, sans-serif;
            background: radial-gradient(circle at top right, #1e1b4b, #020617);
            color: white; min-height: 100vh; overflow-x: hidden;
        }

        /* Экрани Логин */
        #authScreen {
            position: fixed; inset: 0; z-index: 9999;
            background: #020617; display: flex; align-items: center; justify-content: center;
        }

        .auth-card {
            background: rgba(255,255,255,0.05); backdrop-filter: blur(50px);
            padding: 50px; border-radius: 40px; border: 1px solid var(--border);
            width: 380px; text-align: center; box-shadow: 0 0 80px rgba(99, 102, 241, 0.15);
        }

        .premium-input {
            width: 100%; padding: 15px; margin: 12px 0; border-radius: 15px;
            border: 1px solid var(--border); background: rgba(255,255,255,0.05);
            color: white; outline: none; transition: 0.3s; box-sizing: border-box;
        }

        .btn {
            width: 100%; padding: 15px; border-radius: 15px; border: none;
            font-weight: 700; cursor: pointer; transition: 0.4s; text-transform: uppercase;
        }
        .btn-glow { background: linear-gradient(45deg, #4f46e5, #818cf8); color: white; box-shadow: 0 10px 20px rgba(79, 70, 229, 0.3); }

        /* Барномаи Асосӣ */
        #app { display: none; }

        nav {
            padding: 15px 6%; display: flex; justify-content: space-between; align-items: center;
            background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(25px);
            position: sticky; top: 0; z-index: 100; border-bottom: 1px solid var(--border);
        }

        .logo { font-size: 26px; font-weight: 900; background: linear-gradient(to right, #fff, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }

        .container { max-width: 1400px; margin: 40px auto; padding: 0 25px; }

        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(310px, 1fr)); gap: 30px; }

        .glass-card {
            background: var(--glass); backdrop-filter: blur(20px);
            border-radius: 30px; border: 1px solid var(--border);
            overflow: hidden; transition: 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
            height: 100%; display: flex; flex-direction: column;
        }
        .glass-card:hover { transform: translateY(-12px); border-color: var(--accent); background: rgba(255,255,255,0.15); }

        .card-img { 
            width: 100%; height: 190px; object-fit: cover; 
            background: #1e293b; /* Ранги эҳтиётӣ агар сурат бор нашавад */
        }
        
        .card-body { padding: 25px; flex-grow: 1; display: flex; flex-direction: column; }

        .price-chip {
            background: rgba(251, 191, 36, 0.15); color: var(--gold);
            padding: 6px 16px; border-radius: 12px; font-weight: 800; display: inline-block; margin-bottom: 15px; width: fit-content;
        }

        /* Системаи Тест */
        #testModal { display: none; position: fixed; inset: 0; z-index: 5000; background: rgba(0,0,0,0.95); backdrop-filter: blur(15px); }
        .test-box { max-width: 580px; margin: 4% auto; background: white; color: #0f172a; padding: 40px; border-radius: 35px; box-shadow: 0 20px 50px rgba(0,0,0,0.3); }
        .opt-btn { width: 100%; padding: 16px; margin: 10px 0; border: 2px solid #e2e8f0; border-radius: 18px; cursor: pointer; font-size: 16px; font-weight: 600; text-align: left; transition: 0.2s; }
        .opt-btn:hover { background: #f1f5f9; border-color: var(--accent); }

        /* Оинаи маълумот */
        #infoModal { display: none; position: fixed; inset: 0; z-index: 6000; background: rgba(0,0,0,0.9); overflow-y: auto; }
        .info-card { max-width: 850px; margin: 40px auto; background: white; color: #1e293b; padding: 50px; border-radius: 40px; position: relative; }
    </style>
</head>
<body>

<div id="authScreen">
    <div class="auth-card">
        <h1 style="color:white; margin:0 0 5px 0;">ДОНИШҶӮ-ИЛМ</h1>
        <p style="color:#94a3b8; margin-bottom:30px;">Портали академии КИТК</p>
        <input type="text" id="uName" class="premium-input" placeholder="Номи пурра">
        <input type="tel" id="uPhone" class="premium-input" placeholder="Рақами телефон">
        <button class="btn btn-glow" onclick="initApp()">ВОРИД ШУДАН</button>
    </div>
</div>

<div id="app">
    <nav>
        <div class="logo">ДОНИШҶӮ-ИЛМ</div>
        <input type="text" class="premium-input" style="width:300px; margin:0;" id="search" placeholder="Ҷустуҷӯ..." onkeyup="filter()">
        <div id="userDisplay" style="font-weight:bold; color:var(--accent);"></div>
    </nav>

    <div class="container">
        <div style="background: var(--glass); padding: 35px; border-radius: 35px; border: 1px solid var(--border); margin-bottom: 40px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 20px;">
            <div>
                <h2 style="margin:0">Коллеҷи информатика ва техникаи компютерӣ</h2>
                <p style="color:var(--accent); font-weight:bold; margin:5px 0;">Шаҳри Душанбе</p>
            </div>
            <div style="text-align:right">
                <div style="font-size:22px; font-weight:900; color:var(--gold);">РЕЙТИНГ: <span id="userRating">1250</span> ⭐</div>
                <button class="btn btn-glow" style="width:auto; padding:10px 25px; margin-top:10px; font-size:12px;" onclick="startQuiz()">ОҒОЗИ ТЕСТИ 20-САВОЛА</button>
            </div>
        </div>

        <div class="grid" id="mainGrid"></div>
    </div>
</div>

<div id="testModal">
    <div class="test-box">
        <h2 id="qCount" style="color:var(--accent)">Саволи 1/20</h2>
        <p id="qText" style="font-size:20px; font-weight:700; margin-bottom:25px;"></p>
        <div id="qOptions"></div>
        <p style="color:#ef4444; font-size:13px; margin-top:20px; font-weight:bold;">⚠ Хато кунед, аз саволи 1 оғоз мешавад!</p>
    </div>
</div>

<div id="infoModal">
    <div class="info-card">
        <button style="position:absolute; right:30px; top:20px; background:none; border:none; font-size:45px; cursor:pointer;" onclick="closeM()">×</button>
        <h1 id="iTitle" style="color:#1e1b4b; margin-top:0;"></h1>
        <div id="iContent" style="font-size:18px; line-height:1.8; color:#334155; text-align:justify;"></div>
    </div>
</div>

<script>
    const t_tj = ["Барномасози Веб", "Киберамният", "Зеҳни Сунъӣ", "Дизайни Графикӣ", "Программасозии Мобилӣ", "Базаи Маълумот", "Робототехника", "Шабакаҳои Cisco", "3D Моделсозӣ", "Тесткунандаи СМ"];
    const jobs = [];

    // Сохтани 50 ихтисос бо суратҳои боэътимод
    for(let i=0; i<50; i++) {
        let idx = i % 10;
        jobs.push({
            n: t_tj[idx] + (i > 9 ? ` (Курси ${Math.floor(i/10) + 1})` : ""),
            p: Math.floor(Math.random() * (500 - 100 + 1)) + 100,
            // Истифодаи Picsum барои суратҳои зуд
            img: `https://picsum.photos/seed/${i + 123}/400/250`,
            d: `Ин ихтисоси ${t_tj[idx]} дар Коллеҷи информатика ва техникаи компютерии шаҳри Душанбе яке аз самтҳои калидӣ ба ҳисоб меравад. Барномаи таълимӣ тибқи стандартҳои байналмилалӣ сохта шудааст. Донишҷӯён пас аз хатм метавонанд дар ширкатҳои калони IT кор кунанд ва маоши хуб гиранд. Маълумоти муфассал: Омӯзиш дар лабораторияҳои муосир гузаронида шуда, 70% дарсҳо амалӣ мебошанд.`
        });
    }

    const quiz = [
        {q: "HTML чӣ маъно дорад?", a: ["HyperText Markup Language", "High Tech Modern Language", "Hyperlink Toolset"], c: 0},
        {q: "CPU чист?", a: ["Хотираи компютер", "Протсессори марказӣ", "Видеокарта"], c: 1},
        {q: "RAM барои чӣ лозим аст?", a: ["Ҳифзи файлҳои доимӣ", "Хотираи фаврӣ барои иҷрои барномаҳо", "Чопи ҳуҷҷатҳо"], c: 1},
        {q: "Асосгузори Microsoft кист?", a: ["Стив Ҷобс", "Билл Гейтс", "Илон Маск"], c: 1},
        {q: "Python кадом намуди забон аст?", a: ["Забони барномасозӣ", "Системаи оператсионӣ", "Браузер"], c: 0},
        {q: "IP-суроға чист?", a: ["Номи компютер", "Суроғаи рақамии дастгоҳ дар шабака", "Парол"], c: 1},
        {q: "Google Chrome чист?", a: ["Системаи оператсионӣ", "Браузер", "Антивирус"], c: 1},
        {q: "Frontend чист?", a: ["Қисми техникии сервер", "Қисми намоёни сайт", "Базаи маълумот"], c: 1},
        {q: "Кадом дастгоҳ барои ворид кардани матн аст?", a: ["Принтер", "Клавиатура", "Монитор"], c: 1},
        {q: "Мағзи компютер кадом аст?", a: ["CPU", "HDD", "Cooler"], c: 0},
        {q: "Windows чист?", a: ["Системаи оператсионӣ", "Барномаи офисӣ", "Бозӣ"], c: 0},
        {q: "Файли .jpg кадом намуди маълумот аст?", a: ["Матн", "Расм", "Мусиқӣ"], c: 1},
        {q: "WWW чӣ маъно дорад?", a: ["World Wide Web", "Wide Web World", "World Web Wide"], c: 0},
        {q: "SQL барои чӣ истифода мешавад?", a: ["Барои базаи маълумот", "Барои расмкашӣ", "Барои видео"], c: 0},
        {q: "Суръати интернет бо чӣ чен мешавад?", a: ["Кг", "Мбит/с", "Листр"], c: 1},
        {q: "Wi-Fi чӣ тавр кор мекунад?", a: ["Бо сим", "Бо мавҷҳои радиоӣ", "Бо садо"], c: 1},
        {q: "Антивирус барои чӣ лозим аст?", a: ["Барои бозӣ", "Ҳимоя аз вирусҳо", "Дизайни сайт"], c: 1},
        {q: "Linux чист?", a: ["Системаи оператсионӣ", "Номи компютер", "Сайт"], c: 0},
        {q: "Backend чист?", a: ["Дизайни сайт", "Қисми мантиқӣ ва серверии барнома", "Расми сайт"], c: 1},
        {q: "Алгоритм чист?", a: ["Навбати иҷрои амалҳо", "Намуди монитор", "Тугма"], c: 0}
    ];

    let currentQ = 0;

    function initApp() {
        const name = document.getElementById('uName').value;
        if(name.length < 2) return alert("Номро пурра нависед!");
        document.getElementById('authScreen').style.display = 'none';
        document.getElementById('app').style.display = 'block';
        document.getElementById('userDisplay').innerText = "👤 " + name;
        renderCards();
    }

    function renderCards() {
        const grid = document.getElementById('mainGrid');
        grid.innerHTML = jobs.map((j, i) => `
            <div class="glass-card">
                <img src="${j.img}" class="card-img" alt="photo" onerror="this.src='https://via.placeholder.com/400x250/1e293b/ffffff?text=${j.n}'">
                <div class="card-body">
                    <div class="price-chip">${j.p} сомонӣ</div>
                    <h3 style="margin:0 0 12px 0; font-size:18px;">${j.n}</h3>
                    <p style="font-size:13px; opacity:0.7; margin-bottom:20px; line-height:1.5;">${j.d.substring(0, 85)}...</p>
                    <button class="btn btn-glow" style="padding:10px; font-size:11px; margin-top:auto;" onclick="openInfo(${i})">МАЪЛУМОТИ ПУРРА</button>
                </div>
            </div>
        `).join('');
    }

    function openInfo(i) {
        document.getElementById('iTitle').innerText = jobs[i].n;
        document.getElementById('iContent').innerText = jobs[i].d + " Ин касб яке аз самтҳои ояндадор дар бозори меҳнат аст. Донишҷӯёни КИТК дар ин соҳа дониши амиқ мегиранд.";
        document.getElementById('infoModal').style.display = 'block';
    }

    function closeM() { document.getElementById('infoModal').style.display = 'none'; }

    function startQuiz() {
        currentQ = 0;
        showQ();
        document.getElementById('testModal').style.display = 'block';
    }

    function showQ() {
        const q = quiz[currentQ];
        document.getElementById('qCount').innerText = `Саволи ${currentQ + 1}/20`;
        document.getElementById('qText').innerText = q.q;
        const oBox = document.getElementById('qOptions');
        oBox.innerHTML = '';
        q.a.forEach((opt, idx) => {
            const b = document.createElement('button');
            b.className = 'opt-btn';
            b.innerText = opt;
            b.onclick = () => checkQ(idx);
            oBox.appendChild(b);
        });
    }

    function checkQ(idx) {
        if(idx === quiz[currentQ].c) {
            currentQ++;
            if(currentQ < 20) showQ();
            else {
                alert("АҲСАН! Шумо ҳамаи 20 саволро дуруст ҷавоб додед!");
                document.getElementById('userRating').innerText = parseInt(document.getElementById('userRating').innerText) + 500;
                document.getElementById('testModal').style.display = 'none';
            }
        } else {
            alert("ХАТО! Шумо ба саволи 1 баргаштед.");
            currentQ = 0;
            showQ();
        }
    }

    function filter() {
        const val = document.getElementById('search').value.toLowerCase();
        document.querySelectorAll('.glass-card').forEach(card => {
            card.style.display = card.innerText.toLowerCase().includes(val) ? 'block' : 'none';
        });
    }
</script>

</body>
</html>
