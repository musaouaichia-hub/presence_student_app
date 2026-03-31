[index.html](https://github.com/user-attachments/files/26359579/index.html)
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>تسجيل الحضور — QR</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&display=swap');

:root {
  --bg: #f5f0e8;
  --surface: #ffffff;
  --border: #e2ddd4;
  --accent: #1a1a2e;
  --green: #2d6a4f;
  --green-light: #d8f3dc;
  --red: #c1121f;
  --red-light: #ffe5e5;
  --text: #1a1a2e;
  --text-muted: #7a7a8c;
}

* { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Cairo', sans-serif; }

body { background: var(--bg); color: var(--text); max-width: 430px; margin: 0 auto; }

.page { display: none; min-height: 100vh; flex-direction: column; padding: 20px; }
.page.active { display: flex; }

/* Header */
.header { background: var(--accent); color: white; padding: 30px 20px; border-radius: 0 0 20px 20px; margin: -20px -20px 20px -20px; text-align: center; }
.header h1 { font-size: 24px; }

/* Form Card */
.card { background: var(--surface); padding: 20px; border-radius: 15px; border: 1px solid var(--border); box-shadow: 0 2px 10px rgba(0,0,0,0.05); margin-bottom: 20px; }
label { display: block; font-size: 14px; font-weight: 700; margin-bottom: 8px; color: var(--text-muted); }
input { width: 100%; padding: 12px; border: 1.5px solid var(--border); border-radius: 10px; margin-bottom: 15px; text-align: right; font-size: 16px; }

/* Slots */
.day-label { background: var(--accent); color: white; padding: 8px; border-radius: 8px; margin-bottom: 10px; font-weight: bold; }
.slots { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.slot-btn { padding: 15px; border: 1px solid var(--border); border-radius: 10px; background: #f9f9f9; cursor: pointer; transition: 0.2s; }
.slot-btn.active { background: var(--green-light); border-color: var(--green); color: var(--green); font-weight: bold; }
.slot-btn:disabled { opacity: 0.5; cursor: not-allowed; background: #eee; }

.btn-submit { width: 100%; padding: 15px; background: var(--accent); color: white; border: none; border-radius: 12px; font-size: 18px; font-weight: bold; cursor: pointer; }

/* Admin Stats */
.stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px; }
.stat-item { background: white; padding: 15px; border-radius: 10px; text-align: center; border: 1px solid var(--border); }
.stat-num { font-size: 24px; font-weight: 800; color: var(--accent); }

.locked-msg { font-size: 12px; color: var(--red); margin-top: 5px; }
</style>
</head>
<body>

<div class="page active" id="page-landing">
  <div class="header">
    <h1>نظام تسجيل الحضور</h1>
    <p>مرحباً بكم</p>
  </div>
  <button class="btn-submit" style="margin-bottom:15px" onclick="showPage('page-student')">📱 أنا طالب - تسجيل</button>
  <button class="btn-submit" style="background:#444" onclick="showPage('page-login')">🔐 فضاء الأستاذ</button>
</div>

<div class="page" id="page-student">
  <div class="header">
    <h1>تسجيل حضوري</h1>
  </div>
  <div class="card">
    <label>اللقب (Nom)</label>
    <input type="text" id="nom" placeholder="أدخل لقبك">
    <label>الاسم (Prénom)</label>
    <input type="text" id="prenom" placeholder="أدخل اسمك">
  </div>

  <div class="card">
    <div class="day-label" id="current-day-label">جاري التحميل...</div>
    <p style="font-size: 12px; margin-bottom: 10px;">انقر لتحديد الفترات التي حضرتها اليوم:</p>
    <div class="slots">
      <button class="slot-btn" id="btn-m" onclick="toggleSlot('m')">☀️ قبل 20:00</button>
      <button class="slot-btn" id="btn-e" onclick="toggleSlot('e')">🌙 بعد 20:00</button>
    </div>
    <p class="locked-msg" id="lock-notice">⚠️ لا يمكن تسجيل الحضور إلا لليوم الحالي.</p>
  </div>
  <button class="btn-submit" onclick="submitPresence()">✅ تأكيد الحضور</button>
</div>

<div class="page" id="page-success">
    <div style="text-align:center; margin-top: 50px;">
        <h1 style="font-size:60px">🎉</h1>
        <h2>تم التسجيل بنجاح!</h2>
        <p id="success-msg"></p>
        <br>
        <button class="btn-submit" onclick="location.reload()">العودة للرئيسية</button>
    </div>
</div>

<div class="page" id="page-login">
    <div class="header"><h1>دخول الأستاذ</h1></div>
    <div class="card">
        <label>كلمة السر</label>
        <input type="password" id="pwd">
        <button class="btn-submit" onclick="login()">دخول</button>
    </div>
</div>

<div class="page" id="page-admin">
    <div class="header"><h1>لوحة التحكم</h1></div>
    <div class="stat-grid">
        <div class="stat-item"><div class="stat-num" id="count">0</div><div>الطلاب</div></div>
        <div class="stat-item"><div class="stat-num">📅</div><div id="admin-date"></div></div>
    </div>
    <div id="student-list"></div>
    <br>
    <button class="btn-submit" style="background:var(--green)" onclick="exportCSV()">⬇️ تحميل Excel</button>
    <button class="btn-submit" style="background:var(--red); margin-top:10px" onclick="clearData()">🗑️ مسح كل البيانات</button>
</div>

<script>
const PASS = "prof2024";
let selectedM = false;
let selectedE = false;

// Système de détection de date
const today = new Date();
const dateString = today.toLocaleDateString('fr-FR'); // Ex: 31/03/2026

function showPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(id === 'page-student') {
        document.getElementById('current-day-label').innerText = "📅 تاريخ اليوم: " + dateString;
    }
}

function toggleSlot(type) {
    if(type === 'm') {
        selectedM = !selectedM;
        document.getElementById('btn-m').classList.toggle('active', selectedM);
    } else {
        selectedE = !selectedE;
        document.getElementById('btn-e').classList.toggle('active', selectedE);
    }
}

function submitPresence() {
    const n = document.getElementById('nom').value.trim();
    const p = document.getElementById('prenom').value.trim();
    if(!n || !p) return alert("يرجى إدخال الاسم واللقب");
    if(!selectedM && !selectedE) return alert("يرجى اختيار فترة واحدة على الأقل");

    const entry = {
        nom: n,
        prenom: p,
        date: dateString,
        m: selectedM ? "حاضر" : "غائب",
        e: selectedE ? "حاضر" : "غائب",
        time: today.toLocaleTimeString()
    };

    let data = JSON.parse(localStorage.getItem('presence_db') || '[]');
    data.push(entry);
    localStorage.setItem('presence_db', JSON.stringify(data));
    
    document.getElementById('success-msg').innerText = p + " " + n + "\n" + dateString;
    showPage('page-success');
}

function login() {
    if(document.getElementById('pwd').value === PASS) {
        loadAdmin();
        showPage('page-admin');
    } else {
        alert("كلمة سر خاطئة");
    }
}

function loadAdmin() {
    const data = JSON.parse(localStorage.getItem('presence_db') || '[]');
    document.getElementById('count').innerText = data.length;
    document.getElementById('admin-date').innerText = dateString;
    
    let html = "";
    data.reverse().forEach(s => {
        html += `<div class="card">
            <b>${s.nom} ${s.prenom}</b><br>
            <small>${s.date} - ${s.time}</small><br>
            <span style="color:${s.m==='حاضر'?'green':'red'}">☀️ ${s.m}</span> | 
            <span style="color:${s.e==='حاضر'?'green':'red'}">🌙 ${s.e}</span>
        </div>`;
    });
    document.getElementById('student-list').innerHTML = html || "لا يوجد مسجلين بعد";
}

function exportCSV() {
    const data = JSON.parse(localStorage.getItem('presence_db') || '[]');
    let csv = "\ufeffاللقب,الاسم,التاريخ,قبل 20h,بعد 20h,الوقت\n";
    data.forEach(s => {
        csv += `${s.nom},${s.prenom},${s.date},${s.m},${s.e},${s.time}\n`;
    });
    const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "presence_" + dateString + ".csv";
    link.click();
}

function clearData() {
    if(confirm("هل أنت متأكد من مسح جميع البيانات؟")) {
        localStorage.removeItem('presence_db');
        loadAdmin();
    }
}
</script>
</body>
</html>
