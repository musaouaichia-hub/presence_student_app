[index.html](https://github.com/user-attachments/files/26359579/index.html)
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Présence QR — Étudiants</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Outfit:wght@300;400;500;600&display=swap');

:root {
  --bg: #f5f0e8;
  --surface: #ffffff;
  --card: #faf8f4;
  --border: #e2ddd4;
  --accent: #1a1a2e;
  --accent2: #16213e;
  --green: #2d6a4f;
  --green-light: #d8f3dc;
  --red: #c1121f;
  --red-light: #ffe5e5;
  --orange: #e85d04;
  --orange-light: #fff0e0;
  --blue: #0077b6;
  --blue-light: #e0f2fe;
  --text: #1a1a2e;
  --text-muted: #7a7a8c;
  --radius: 16px;
  --shadow: 0 2px 20px rgba(0,0,0,0.08);
  --shadow-lg: 0 8px 40px rgba(0,0,0,0.15);
}

* { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

body {
  font-family: 'Outfit', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  max-width: 430px;
  margin: 0 auto;
}

/* PAGES */
.page { display: none; min-height: 100vh; flex-direction: column; }
.page.active { display: flex; }

/* ========================
   LANDING PAGE
======================== */
#page-landing {
  background: var(--accent);
  align-items: center;
  justify-content: center;
  padding: 40px 24px;
  position: relative;
  overflow: hidden;
}
#page-landing::before {
  content: '';
  position: absolute;
  width: 300px; height: 300px;
  background: radial-gradient(circle, rgba(255,255,255,0.05) 0%, transparent 70%);
  top: -50px; right: -80px;
  border-radius: 50%;
}
#page-landing::after {
  content: '';
  position: absolute;
  width: 200px; height: 200px;
  background: radial-gradient(circle, rgba(255,255,255,0.04) 0%, transparent 70%);
  bottom: 60px; left: -40px;
  border-radius: 50%;
}
.landing-logo {
  font-family: 'Syne', sans-serif;
  font-size: 36px;
  font-weight: 800;
  color: #fff;
  text-align: center;
  margin-bottom: 8px;
  letter-spacing: -1px;
}
.landing-logo span { color: #ffd60a; }
.landing-sub {
  color: rgba(255,255,255,0.55);
  font-size: 14px;
  text-align: center;
  margin-bottom: 64px;
  font-weight: 400;
}
.landing-btns { width: 100%; display: flex; flex-direction: column; gap: 14px; position: relative; z-index: 1; }
.land-btn {
  width: 100%;
  padding: 18px 24px;
  border-radius: 14px;
  border: none;
  font-family: 'Syne', sans-serif;
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 14px;
  transition: transform 0.15s, box-shadow 0.15s;
}
.land-btn:active { transform: scale(0.97); }
.land-btn-student { background: #ffd60a; color: var(--accent); box-shadow: 0 4px 20px rgba(255,214,10,0.3); }
.land-btn-admin { background: rgba(255,255,255,0.08); color: #fff; border: 1px solid rgba(255,255,255,0.15); }
.land-btn-icon { font-size: 24px; }
.land-btn-text { text-align: left; }
.land-btn-title { font-size: 16px; display: block; }
.land-btn-desc { font-size: 11px; font-weight: 400; opacity: 0.7; font-family: 'Outfit', sans-serif; }

/* ========================
   STUDENT QR SCAN PAGE
======================== */
#page-scan {
  background: var(--bg);
}
.page-header {
  background: var(--accent);
  padding: 52px 20px 20px;
  color: #fff;
}
.back-btn {
  background: rgba(255,255,255,0.1);
  border: none;
  color: #fff;
  padding: 6px 12px;
  border-radius: 8px;
  font-family: 'Outfit', sans-serif;
  font-size: 13px;
  cursor: pointer;
  margin-bottom: 14px;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}
.page-title {
  font-family: 'Syne', sans-serif;
  font-size: 22px;
  font-weight: 800;
}
.page-subtitle { font-size: 13px; opacity: 0.6; margin-top: 4px; }

.scan-body { padding: 20px; flex: 1; }

.qr-box {
  background: var(--surface);
  border-radius: var(--radius);
  padding: 24px;
  text-align: center;
  box-shadow: var(--shadow);
  margin-bottom: 16px;
  border: 1px solid var(--border);
}
.qr-title { font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700; margin-bottom: 6px; }
.qr-desc { font-size: 12px; color: var(--text-muted); margin-bottom: 20px; }
#qr-display { display: flex; justify-content: center; margin-bottom: 16px; }
#qr-display canvas, #qr-display img { border-radius: 8px; }
.qr-url {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 10px 12px;
  font-size: 11px;
  color: var(--text-muted);
  word-break: break-all;
  text-align: left;
}
.copy-btn {
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 10px;
  font-family: 'Syne', sans-serif;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
}

/* ========================
   STUDENT FORM PAGE
======================== */
#page-student {
  background: var(--bg);
}
.student-body { padding: 20px; flex: 1; overflow-y: auto; padding-bottom: 30px; }

.form-card {
  background: var(--surface);
  border-radius: var(--radius);
  padding: 20px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  margin-bottom: 14px;
}
.form-section-title {
  font-family: 'Syne', sans-serif;
  font-size: 13px;
  font-weight: 700;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 14px;
}
.field { margin-bottom: 14px; }
.field:last-child { margin-bottom: 0; }
.field label { display: block; font-size: 12px; font-weight: 600; color: var(--text-muted); margin-bottom: 6px; text-transform: uppercase; letter-spacing: 0.5px; }
.field input {
  width: 100%;
  padding: 13px 16px;
  background: var(--card);
  border: 1.5px solid var(--border);
  border-radius: 12px;
  color: var(--text);
  font-family: 'Outfit', sans-serif;
  font-size: 16px;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.field input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(26,26,46,0.08); }

/* DAY PRESENCE */
.days-wrapper { display: flex; flex-direction: column; gap: 10px; }
.day-block {
  background: var(--card);
  border: 1.5px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}
.day-label {
  padding: 10px 14px;
  font-family: 'Syne', sans-serif;
  font-size: 13px;
  font-weight: 700;
  background: var(--accent);
  color: #fff;
  display: flex;
  align-items: center;
  gap: 8px;
}
.slots-row { display: grid; grid-template-columns: 1fr 1fr; }
.slot-pick {
  padding: 14px 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  cursor: pointer;
  border: none;
  background: transparent;
  font-family: 'Outfit', sans-serif;
  transition: background 0.15s;
  position: relative;
}
.slot-pick + .slot-pick { border-left: 1px solid var(--border); }
.slot-icon { font-size: 22px; }
.slot-name { font-size: 11px; font-weight: 600; color: var(--text-muted); }
.slot-status {
  font-size: 11px;
  font-weight: 700;
  padding: 3px 10px;
  border-radius: 20px;
  background: var(--border);
  color: var(--text-muted);
  transition: all 0.2s;
}
.slot-pick.present .slot-status { background: var(--green-light); color: var(--green); }
.slot-pick.absent .slot-status { background: var(--red-light); color: var(--red); }
.slot-pick.present { background: rgba(45,106,79,0.04); }
.slot-pick.absent { background: rgba(193,18,31,0.03); }

.submit-btn {
  width: 100%;
  padding: 16px;
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 14px;
  font-family: 'Syne', sans-serif;
  font-size: 16px;
  font-weight: 800;
  cursor: pointer;
  box-shadow: 0 4px 20px rgba(26,26,46,0.25);
  transition: transform 0.15s;
  letter-spacing: 0.3px;
}
.submit-btn:active { transform: scale(0.97); }

/* ========================
   SUCCESS PAGE
======================== */
#page-success {
  background: var(--accent);
  align-items: center;
  justify-content: center;
  padding: 40px 24px;
  text-align: center;
}
.success-icon { font-size: 72px; margin-bottom: 20px; animation: pop 0.4s ease; }
@keyframes pop { from { transform: scale(0); opacity: 0; } to { transform: scale(1); opacity: 1; } }
.success-title { font-family: 'Syne', sans-serif; font-size: 28px; font-weight: 800; color: #fff; margin-bottom: 10px; }
.success-name { color: #ffd60a; }
.success-sub { color: rgba(255,255,255,0.6); font-size: 14px; margin-bottom: 40px; line-height: 1.5; }
.success-summary {
  background: rgba(255,255,255,0.08);
  border-radius: 14px;
  padding: 16px;
  width: 100%;
  margin-bottom: 32px;
}
.sum-row { display: flex; justify-content: space-between; align-items: center; padding: 6px 0; }
.sum-row + .sum-row { border-top: 1px solid rgba(255,255,255,0.1); }
.sum-label { font-size: 12px; color: rgba(255,255,255,0.5); }
.sum-val { font-size: 13px; font-weight: 600; color: #fff; }
.new-reg-btn {
  padding: 14px 32px;
  background: #ffd60a;
  color: var(--accent);
  border: none;
  border-radius: 12px;
  font-family: 'Syne', sans-serif;
  font-size: 15px;
  font-weight: 800;
  cursor: pointer;
}

/* ========================
   ADMIN LOGIN
======================== */
#page-admin-login {
  background: var(--bg);
  align-items: center;
  justify-content: center;
  padding: 40px 24px;
}
.login-card {
  width: 100%;
  background: var(--surface);
  border-radius: 20px;
  padding: 32px 24px;
  box-shadow: var(--shadow-lg);
  border: 1px solid var(--border);
}
.login-logo {
  font-family: 'Syne', sans-serif;
  font-size: 24px;
  font-weight: 800;
  text-align: center;
  margin-bottom: 6px;
}
.login-sub { text-align: center; font-size: 13px; color: var(--text-muted); margin-bottom: 28px; }
.login-error { color: var(--red); font-size: 13px; text-align: center; margin-bottom: 10px; display: none; }
.login-btn {
  width: 100%;
  padding: 15px;
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 12px;
  font-family: 'Syne', sans-serif;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  margin-top: 8px;
}
.back-link { text-align: center; margin-top: 16px; font-size: 13px; color: var(--text-muted); cursor: pointer; text-decoration: underline; }

/* ========================
   ADMIN DASHBOARD
======================== */
#page-admin {
  background: var(--bg);
}
.admin-header {
  background: var(--accent);
  padding: 52px 20px 20px;
  color: #fff;
}
.admin-header-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 4px; }
.admin-title { font-family: 'Syne', sans-serif; font-size: 22px; font-weight: 800; }
.logout-btn {
  background: rgba(255,255,255,0.1);
  border: none;
  color: #fff;
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 12px;
  cursor: pointer;
  font-family: 'Outfit', sans-serif;
}
.admin-body { padding: 16px; flex: 1; overflow-y: auto; padding-bottom: 30px; }

/* STATS GRID */
.stats-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-bottom: 16px; }
.stat-tile {
  background: var(--surface);
  border-radius: 14px;
  padding: 16px;
  box-shadow: var(--shadow);
  border: 1px solid var(--border);
  text-align: center;
}
.stat-n { font-family: 'Syne', sans-serif; font-size: 34px; font-weight: 800; }
.stat-l { font-size: 11px; color: var(--text-muted); font-weight: 500; margin-top: 2px; }
.n-blue { color: var(--blue); }
.n-green { color: var(--green); }
.n-orange { color: var(--orange); }
.n-red { color: var(--red); }

/* ADMIN TABS */
.admin-tabs { display: flex; gap: 6px; margin-bottom: 14px; }
.atab {
  flex: 1;
  padding: 9px 6px;
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: 10px;
  font-family: 'Syne', sans-serif;
  font-size: 12px;
  font-weight: 700;
  color: var(--text-muted);
  cursor: pointer;
  text-align: center;
  transition: all 0.2s;
}
.atab.active { background: var(--accent); color: #fff; border-color: var(--accent); }

/* STUDENT TABLE */
.section-lbl { font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 800; margin-bottom: 12px; }
.student-row {
  background: var(--surface);
  border-radius: 12px;
  margin-bottom: 8px;
  border: 1px solid var(--border);
  overflow: hidden;
}
.srow-header {
  display: flex;
  align-items: center;
  padding: 12px 14px;
  gap: 12px;
  cursor: pointer;
}
.srow-avatar {
  width: 36px; height: 36px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif;
  font-size: 13px;
  font-weight: 800;
  flex-shrink: 0;
}
.srow-info { flex: 1; }
.srow-name { font-family: 'Syne', sans-serif; font-size: 14px; font-weight: 700; }
.srow-meta { font-size: 11px; color: var(--text-muted); margin-top: 2px; }
.srow-dots { display: flex; gap: 3px; }
.sdot { width: 9px; height: 9px; border-radius: 50%; background: var(--border); }
.sdot.p { background: var(--green); }
.sdot.a { background: var(--red); }
.sdot.h { background: var(--orange); }

.srow-detail { display: none; padding: 0 14px 14px; border-top: 1px solid var(--border); padding-top: 12px; }
.srow-detail.open { display: block; }
.detail-slots { display: grid; grid-template-columns: repeat(3,1fr); gap: 6px; margin-bottom: 10px; }
.ds-col { background: var(--card); border-radius: 8px; padding: 8px 6px; text-align: center; }
.ds-day { font-size: 10px; font-weight: 700; color: var(--text-muted); margin-bottom: 5px; font-family: 'Syne', sans-serif; }
.ds-tag {
  display: inline-block;
  font-size: 9px;
  font-weight: 700;
  padding: 2px 6px;
  border-radius: 4px;
  margin: 1px;
}
.ds-p-m { background: var(--orange-light); color: var(--orange); }
.ds-p-e { background: var(--blue-light); color: var(--blue); }
.ds-absent { background: var(--red-light); color: var(--red); }
.ds-none { background: var(--card); color: var(--text-muted); border: 1px solid var(--border); }
.del-row-btn {
  width: 100%;
  padding: 8px;
  background: var(--red-light);
  color: var(--red);
  border: 1px solid var(--red);
  border-radius: 8px;
  font-family: 'Syne', sans-serif;
  font-size: 12px;
  font-weight: 700;
  cursor: pointer;
}

/* EXPORT */
.export-section { }
.exp-btn {
  width: 100%;
  padding: 14px;
  border-radius: 12px;
  border: none;
  font-family: 'Syne', sans-serif;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}
.exp-btn-csv { background: var(--green); color: #fff; }
.exp-btn-reset { background: var(--red-light); color: var(--red); border: 1px solid var(--red); }
.table-wrap { overflow-x: auto; border-radius: 10px; border: 1px solid var(--border); }
table { width: 100%; border-collapse: collapse; font-size: 11px; min-width: 480px; }
th {
  background: var(--card);
  padding: 9px 10px;
  text-align: left;
  font-family: 'Syne', sans-serif;
  font-size: 10px;
  font-weight: 700;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  border-bottom: 1px solid var(--border);
  white-space: nowrap;
}
td { padding: 8px 10px; border-bottom: 1px solid var(--border); white-space: nowrap; }
tr:last-child td { border-bottom: none; }
.tp { color: var(--green); font-weight: 700; }
.ta { color: var(--red); font-weight: 700; }
.tn { color: var(--text-muted); }

/* QR page inside admin */
.qr-section {
  background: var(--surface);
  border-radius: 16px;
  padding: 24px;
  border: 1px solid var(--border);
  text-align: center;
}
.qr-section-title { font-family: 'Syne', sans-serif; font-size: 16px; font-weight: 800; margin-bottom: 6px; }
.qr-section-desc { font-size: 13px; color: var(--text-muted); margin-bottom: 20px; }
#admin-qr { display: flex; justify-content: center; margin-bottom: 16px; }

/* TOAST */
.toast {
  position: fixed;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%) translateY(20px);
  background: var(--accent);
  color: #fff;
  padding: 11px 22px;
  border-radius: 30px;
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 13px;
  opacity: 0;
  transition: all 0.3s;
  z-index: 9999;
  white-space: nowrap;
  box-shadow: 0 4px 20px rgba(0,0,0,0.2);
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

/* EMPTY */
.empty-state { text-align: center; padding: 40px 20px; color: var(--text-muted); }
.empty-icon { font-size: 42px; margin-bottom: 10px; }
.empty-t { font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700; margin-bottom: 4px; color: var(--text); }
.empty-s { font-size: 13px; }

/* CHEVRON */
.chev { transition: transform 0.2s; color: var(--text-muted); font-size: 12px; }
.chev.open { transform: rotate(90deg); }

/* SLOT BARS - stats */
.slot-bar-row { margin-bottom: 10px; }
.slot-bar-label { display: flex; justify-content: space-between; font-size: 12px; margin-bottom: 4px; }
.slot-bar-label span:last-child { font-weight: 700; }
.slot-bar-track { height: 6px; background: var(--border); border-radius: 3px; overflow: hidden; }
.slot-bar-fill { height: 100%; border-radius: 3px; transition: width 0.6s ease; }

.info-badge {
  background: var(--orange-light);
  border: 1px solid var(--orange);
  border-radius: 10px;
  padding: 10px 14px;
  font-size: 12px;
  color: var(--orange);
  margin-bottom: 14px;
  display: flex;
  align-items: flex-start;
  gap: 8px;
}

</style>
</head>
<body>

<!-- =================== LANDING =================== -->
<div class="page active" id="page-landing">
  <div class="landing-logo">Prés<span>.</span>QR</div>
  <div class="landing-sub">Système de présence par QR Code</div>
  <div class="landing-btns">
    <button class="land-btn land-btn-student" onclick="goStudentFlow()">
      <span class="land-btn-icon">📱</span>
      <span class="land-btn-text">
        <span class="land-btn-title">Je suis étudiant</span>
        <span class="land-btn-desc">Scanner le QR code du prof et marquer ma présence</span>
      </span>
    </button>
    <button class="land-btn land-btn-admin" onclick="showPage('page-admin-login')">
      <span class="land-btn-icon">🔐</span>
      <span class="land-btn-text">
        <span class="land-btn-title">Espace professeur</span>
        <span class="land-btn-desc">Voir les présences et gérer la liste</span>
      </span>
    </button>
  </div>
</div>

<!-- =================== SCAN / QR INFO =================== -->
<div class="page" id="page-scan">
  <div class="page-header">
    <button class="back-btn" onclick="showPage('page-landing')">← Retour</button>
    <div class="page-title">📱 QR Code d'accès</div>
    <div class="page-subtitle">À afficher aux étudiants</div>
  </div>
  <div class="scan-body">
    <div class="info-badge">
      ℹ️ Montrez ce QR code aux étudiants. Ils scannent et remplissent leur présence directement sur leur téléphone.
    </div>
    <div class="qr-box">
      <div class="qr-title">QR Code de présence</div>
      <div class="qr-desc">Les étudiants scannent ce code avec leur téléphone</div>
      <div id="qr-display"></div>
      <div class="qr-url" id="qr-url-text"></div>
      <button class="copy-btn" onclick="copyLink()">📋 Copier le lien</button>
    </div>
    <button class="submit-btn" onclick="showPage('page-student')">
      ✏️ Ou ouvrir le formulaire directement
    </button>
  </div>
</div>

<!-- =================== STUDENT FORM =================== -->
<div class="page" id="page-student">
  <div class="page-header">
    <button class="back-btn" onclick="showPage('page-landing')">← Retour</button>
    <div class="page-title">✏️ Marquer ma présence</div>
    <div class="page-subtitle">Remplissez votre nom et vos créneaux</div>
  </div>
  <div class="student-body">

    <div class="form-card">
      <div class="form-section-title">Identité</div>
      <div class="field">
        <label>Nom de famille</label>
        <input type="text" id="s-nom" placeholder="ex: Benali" autocomplete="family-name">
      </div>
      <div class="field">
        <label>Prénom</label>
        <input type="text" id="s-prenom" placeholder="ex: Amina" autocomplete="given-name">
      </div>
    </div>

    <div class="form-card">
      <div class="form-section-title">Présence — appuyez pour changer</div>
      <div class="days-wrapper">
        <!-- DAY 1 -->
        <div class="day-block">
          <div class="day-label">📅 Jour 1</div>
          <div class="slots-row">
            <button class="slot-pick" id="sp-j1m" onclick="cycleSlot('j1m')">
              <span class="slot-icon">☀️</span>
              <span class="slot-name">Avant 20h</span>
              <span class="slot-status" id="ss-j1m">Non marqué</span>
            </button>
            <button class="slot-pick" id="sp-j1e" onclick="cycleSlot('j1e')">
              <span class="slot-icon">🌙</span>
              <span class="slot-name">Après 20h</span>
              <span class="slot-status" id="ss-j1e">Non marqué</span>
            </button>
          </div>
        </div>
        <!-- DAY 2 -->
        <div class="day-block">
          <div class="day-label">📅 Jour 2</div>
          <div class="slots-row">
            <button class="slot-pick" id="sp-j2m" onclick="cycleSlot('j2m')">
              <span class="slot-icon">☀️</span>
              <span class="slot-name">Avant 20h</span>
              <span class="slot-status" id="ss-j2m">Non marqué</span>
            </button>
            <button class="slot-pick" id="sp-j2e" onclick="cycleSlot('j2e')">
              <span class="slot-icon">🌙</span>
              <span class="slot-name">Après 20h</span>
              <span class="slot-status" id="ss-j2e">Non marqué</span>
            </button>
          </div>
        </div>
        <!-- DAY 3 -->
        <div class="day-block">
          <div class="day-label">📅 Jour 3</div>
          <div class="slots-row">
            <button class="slot-pick" id="sp-j3m" onclick="cycleSlot('j3m')">
              <span class="slot-icon">☀️</span>
              <span class="slot-name">Avant 20h</span>
              <span class="slot-status" id="ss-j3m">Non marqué</span>
            </button>
            <button class="slot-pick" id="sp-j3e" onclick="cycleSlot('j3e')">
              <span class="slot-icon">🌙</span>
              <span class="slot-name">Après 20h</span>
              <span class="slot-status" id="ss-j3e">Non marqué</span>
            </button>
          </div>
        </div>
      </div>
    </div>

    <button class="submit-btn" onclick="submitPresence()">✅ Confirmer ma présence</button>
  </div>
</div>

<!-- =================== SUCCESS =================== -->
<div class="page" id="page-success">
  <div class="success-icon">🎉</div>
  <div class="success-title">Présence <span class="success-name" id="suc-name"></span><br>enregistrée !</div>
  <div class="success-sub">Votre présence a été sauvegardée avec succès.<br>Merci !</div>
  <div class="success-summary" id="suc-summary"></div>
  <button class="new-reg-btn" onclick="resetStudentForm()">+ Nouvelle inscription</button>
</div>

<!-- =================== ADMIN LOGIN =================== -->
<div class="page" id="page-admin-login">
  <div class="login-card">
    <div class="login-logo">🔐 Espace Prof</div>
    <div class="login-sub">Entrez le mot de passe administrateur</div>
    <div class="login-error" id="login-err">Mot de passe incorrect</div>
    <div class="field">
      <label>Mot de passe</label>
      <input type="password" id="admin-pwd" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <button class="login-btn" onclick="doLogin()">🔓 Accéder</button>
    <div class="back-link" onclick="showPage('page-landing')">← Retour à l'accueil</div>
  </div>
</div>

<!-- =================== ADMIN DASHBOARD =================== -->
<div class="page" id="page-admin">
  <div class="admin-header">
    <div class="admin-header-top">
      <div class="admin-title">📊 Tableau de bord</div>
      <button class="logout-btn" onclick="logout()">Déconnexion</button>
    </div>
    <div style="font-size:12px;opacity:0.5;margin-top:4px" id="admin-date"></div>
  </div>
  <div class="admin-body">
    <div class="stats-grid">
      <div class="stat-tile"><div class="stat-n n-blue" id="a-total">0</div><div class="stat-l">Inscrits</div></div>
      <div class="stat-tile"><div class="stat-n n-green" id="a-full">0</div><div class="stat-l">Complet (6/6)</div></div>
      <div class="stat-tile"><div class="stat-n n-orange" id="a-partial">0</div><div class="stat-l">Partiel</div></div>
      <div class="stat-tile"><div class="stat-n n-red" id="a-zero">0</div><div class="stat-l">Absent total</div></div>
    </div>

    <div class="admin-tabs">
      <button class="atab active" onclick="switchTab('list')">👥 Liste</button>
      <button class="atab" onclick="switchTab('stats')">📈 Stats</button>
      <button class="atab" onclick="switchTab('qr')">📱 QR</button>
      <button class="atab" onclick="switchTab('export')">⬇️ Export</button>
    </div>

    <!-- LIST TAB -->
    <div id="atab-list">
      <div class="section-lbl" id="list-count-lbl">Étudiants</div>
      <div id="admin-list-container"></div>
    </div>

    <!-- STATS TAB -->
    <div id="atab-stats" style="display:none">
      <div class="section-lbl">Taux de présence par créneau</div>
      <div class="form-card" style="padding:16px">
        <div id="slot-bars"></div>
      </div>
    </div>

    <!-- QR TAB -->
    <div id="atab-qr" style="display:none">
      <div class="qr-section">
        <div class="qr-section-title">QR Code à afficher</div>
        <div class="qr-section-desc">Projetez ce QR code en classe. Les étudiants le scannent pour s'enregistrer.</div>
        <div id="admin-qr"></div>
        <div class="qr-url" id="admin-qr-url"></div>
        <button class="copy-btn" style="margin-top:10px" onclick="copyLink()">📋 Copier le lien</button>
      </div>
    </div>

    <!-- EXPORT TAB -->
    <div id="atab-export" style="display:none">
      <div class="export-section">
        <button class="exp-btn exp-btn-csv" onclick="exportCSV()">⬇️ Exporter en CSV (Excel)</button>
        <button class="exp-btn exp-btn-reset" onclick="resetAll()">🗑️ Effacer toutes les données</button>
        <div class="table-wrap">
          <table>
            <thead><tr>
              <th>Nom</th><th>Prénom</th>
              <th>J1☀️</th><th>J1🌙</th>
              <th>J2☀️</th><th>J2🌙</th>
              <th>J3☀️</th><th>J3🌙</th>
              <th>Score</th>
            </tr></thead>
            <tbody id="exp-body"></tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ===========================
// CONFIG
// ===========================
const ADMIN_PASSWORD = 'prof2024'; // 🔑 Changez ce mot de passe !
const STORAGE_KEY = 'presenceQR_v2';
const APP_URL = window.location.href.split('?')[0];

// ===========================
// DATA
// ===========================
function loadStudents() {
  return JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
}
function saveStudents(arr) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(arr));
}

// ===========================
// PAGES
// ===========================
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0, 0);
}

function goStudentFlow() {
  // Check if came from QR (URL param)
  showPage('page-student');
}

// ===========================
// QR CODE
// ===========================
function generateQR(containerId) {
  const container = document.getElementById(containerId);
  container.innerHTML = '';
  try {
    new QRCode(container, {
      text: APP_URL + '?student=1',
      width: 200, height: 200,
      colorDark: '#1a1a2e',
      colorLight: '#ffffff',
      correctLevel: QRCode.CorrectLevel.H
    });
  } catch(e) {
    container.innerHTML = `<div style="width:200px;height:200px;background:#f0f0f0;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:12px;color:#666;text-align:center;padding:10px">QR Code<br>(ouvrir depuis un serveur)</div>`;
  }
}

function initQRs() {
  generateQR('qr-display');
  generateQR('admin-qr');
  const url = APP_URL + '?student=1';
  document.getElementById('qr-url-text').textContent = url;
  document.getElementById('admin-qr-url').textContent = url;
}

function copyLink() {
  const url = APP_URL + '?student=1';
  if (navigator.clipboard) {
    navigator.clipboard.writeText(url).then(() => showToast('🔗 Lien copié !'));
  } else {
    const el = document.createElement('textarea');
    el.value = url;
    document.body.appendChild(el);
    el.select();
    document.execCommand('copy');
    document.body.removeChild(el);
    showToast('🔗 Lien copié !');
  }
}

// ===========================
// STUDENT FORM
// ===========================
const slotState = { j1m: null, j1e: null, j2m: null, j2e: null, j3m: null, j3e: null };

function cycleSlot(key) {
  const cur = slotState[key];
  if (cur === null) slotState[key] = 'present';
  else if (cur === 'present') slotState[key] = 'absent';
  else slotState[key] = null;
  updateSlotUI(key);
}

function updateSlotUI(key) {
  const btn = document.getElementById('sp-' + key);
  const lbl = document.getElementById('ss-' + key);
  const val = slotState[key];
  btn.className = 'slot-pick';
  if (val === 'present') { btn.classList.add('present'); lbl.textContent = '✓ Présent'; }
  else if (val === 'absent') { btn.classList.add('absent'); lbl.textContent = '✗ Absent'; }
  else { lbl.textContent = 'Non marqué'; }
}

function submitPresence() {
  const nom = document.getElementById('s-nom').value.trim();
  const prenom = document.getElementById('s-prenom').value.trim();
  if (!nom || !prenom) { showToast('⚠️ Entrez votre Nom et Prénom', '#e85d04'); return; }

  const student = {
    id: Date.now(),
    nom, prenom,
    date: new Date().toLocaleString('fr-FR'),
    slots: { ...slotState }
  };

  const students = loadStudents();
  students.push(student);
  saveStudents(students);

  // Show success
  document.getElementById('suc-name').textContent = prenom + ' ' + nom;
  const keys = ['j1m','j1e','j2m','j2e','j3m','j3e'];
  const names = ['Jour 1 ☀️','Jour 1 🌙','Jour 2 ☀️','Jour 2 🌙','Jour 3 ☀️','Jour 3 🌙'];
  let sumHtml = '';
  keys.forEach((k,i) => {
    const v = student.slots[k];
    const disp = v === 'present' ? '<span style="color:#2d6a4f;font-weight:700">✓ Présent</span>'
                 : v === 'absent' ? '<span style="color:#c1121f;font-weight:700">✗ Absent</span>'
                 : '<span style="color:#7a7a8c">— Non marqué</span>';
    sumHtml += `<div class="sum-row"><span class="sum-label">${names[i]}</span>${disp}</div>`;
  });
  document.getElementById('suc-summary').innerHTML = sumHtml;
  showPage('page-success');
}

function resetStudentForm() {
  document.getElementById('s-nom').value = '';
  document.getElementById('s-prenom').value = '';
  Object.keys(slotState).forEach(k => { slotState[k] = null; updateSlotUI(k); });
  showPage('page-student');
}

// ===========================
// ADMIN
// ===========================
function doLogin() {
  const pwd = document.getElementById('admin-pwd').value;
  if (pwd === ADMIN_PASSWORD) {
    document.getElementById('login-err').style.display = 'none';
    document.getElementById('admin-pwd').value = '';
    loadAdmin();
    showPage('page-admin');
  } else {
    document.getElementById('login-err').style.display = 'block';
  }
}

function logout() {
  showPage('page-landing');
}

function loadAdmin() {
  document.getElementById('admin-date').textContent = new Date().toLocaleString('fr-FR');
  const students = loadStudents();
  renderAdminStats(students);
  renderAdminList(students);
  renderSlotBars(students);
  renderExportTable(students);
  generateQR('admin-qr');
  document.getElementById('admin-qr-url').textContent = APP_URL + '?student=1';
}

function calcScore(slots) {
  return Object.values(slots).filter(v => v === 'present').length;
}

function renderAdminStats(students) {
  const total = students.length;
  const full = students.filter(s => calcScore(s.slots) === 6).length;
  const zero = students.filter(s => calcScore(s.slots) === 0).length;
  const partial = total - full - zero;
  document.getElementById('a-total').textContent = total;
  document.getElementById('a-full').textContent = full;
  document.getElementById('a-partial').textContent = partial;
  document.getElementById('a-zero').textContent = zero;
  document.getElementById('list-count-lbl').textContent = `Étudiants (${total})`;
}

function renderAdminList(students) {
  const container = document.getElementById('admin-list-container');
  if (!students.length) {
    container.innerHTML = `<div class="empty-state"><div class="empty-icon">🎓</div><div class="empty-t">Aucun étudiant inscrit</div><div class="empty-s">Les étudiants apparaîtront ici après avoir scanné le QR code</div></div>`;
    return;
  }
  container.innerHTML = students.map((s, i) => {
    const keys = ['j1m','j1e','j2m','j2e','j3m','j3e'];
    const dayKeys = [['j1m','j1e'],['j2m','j2e'],['j3m','j3e']];
    const dotClass = ([m,e]) => {
      const mv = s.slots[m], ev = s.slots[e];
      if (mv==='present'&&ev==='present') return 'p';
      if (mv==='absent'&&ev==='absent') return 'a';
      if (mv==='present'||ev==='present') return 'h';
      return '';
    };
    const dots = dayKeys.map(d => `<div class="sdot ${dotClass(d)}"></div>`).join('');
    const score = calcScore(s.slots);
    const initials = (s.nom[0]||'') + (s.prenom[0]||'');

    const detailRows = dayKeys.map(([mk,ek],di) => `
      <div class="ds-col">
        <div class="ds-day">Jour ${di+1}</div>
        ${slotTag2(s.slots[mk],'m')}
        ${slotTag2(s.slots[ek],'e')}
      </div>`).join('');

    return `
    <div class="student-row">
      <div class="srow-header" onclick="toggleRow(${s.id})">
        <div class="srow-avatar">${initials.toUpperCase()}</div>
        <div class="srow-info">
          <div class="srow-name">${s.nom} ${s.prenom}</div>
          <div class="srow-meta">${score}/6 présences · ${s.date||''}</div>
        </div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:5px">
          <div class="srow-dots">${dots}</div>
          <span class="chev" id="chev-${s.id}">›</span>
        </div>
      </div>
      <div class="srow-detail" id="row-${s.id}">
        <div class="detail-slots">${detailRows}</div>
        <button class="del-row-btn" onclick="deleteStudent(${s.id})">🗑️ Supprimer cet étudiant</button>
      </div>
    </div>`;
  }).join('');
}

function slotTag2(val, period) {
  const icon = period==='m'?'☀️':'🌙';
  if (val==='present') return `<span class="ds-tag ${period==='m'?'ds-p-m':'ds-p-e'}">${icon} Présent</span>`;
  if (val==='absent') return `<span class="ds-tag ds-absent">${icon} Absent</span>`;
  return `<span class="ds-tag ds-none">${icon} —</span>`;
}

function toggleRow(id) {
  const d = document.getElementById('row-' + id);
  const c = document.getElementById('chev-' + id);
  d.classList.toggle('open');
  c.classList.toggle('open');
}

function deleteStudent(id) {
  if (!confirm('Supprimer cet étudiant ?')) return;
  let students = loadStudents();
  students = students.filter(s => s.id !== id);
  saveStudents(students);
  loadAdmin();
  showToast('🗑️ Supprimé');
}

function renderSlotBars(students) {
  const total = students.length;
  const keys = ['j1m','j1e','j2m','j2e','j3m','j3e'];
  const names = ['Jour 1 ☀️ Avant 20h','Jour 1 🌙 Après 20h','Jour 2 ☀️ Avant 20h','Jour 2 🌙 Après 20h','Jour 3 ☀️ Avant 20h','Jour 3 🌙 Après 20h'];
  const colors = ['#e85d04','#0077b6','#e85d04','#0077b6','#e85d04','#0077b6'];
  const container = document.getElementById('slot-bars');
  if (!total) { container.innerHTML = '<div style="color:var(--text-muted);text-align:center;font-size:13px;padding:16px">Aucune donnée</div>'; return; }
  container.innerHTML = keys.map((k,i) => {
    const count = students.filter(s => s.slots[k]==='present').length;
    const pct = Math.round((count/total)*100);
    return `
    <div class="slot-bar-row">
      <div class="slot-bar-label"><span>${names[i]}</span><span style="color:${colors[i]}">${count}/${total} (${pct}%)</span></div>
      <div class="slot-bar-track"><div class="slot-bar-fill" style="width:${pct}%;background:${colors[i]}"></div></div>
    </div>`;
  }).join('');
}

function renderExportTable(students) {
  const keys = ['j1m','j1e','j2m','j2e','j3m','j3e'];
  const body = document.getElementById('exp-body');
  if (!students.length) { body.innerHTML = '<tr><td colspan="9" style="text-align:center;color:var(--text-muted);padding:16px">Aucune donnée</td></tr>'; return; }
  body.innerHTML = students.map(s => {
    const cells = keys.map(k => {
      const v = s.slots[k];
      if (v==='present') return `<td class="tp">✓</td>`;
      if (v==='absent') return `<td class="ta">✗</td>`;
      return `<td class="tn">—</td>`;
    }).join('');
    const score = calcScore(s.slots);
    return `<tr><td><strong>${s.nom}</strong></td><td>${s.prenom}</td>${cells}<td><strong>${score}/6</strong></td></tr>`;
  }).join('');
}

function exportCSV() {
  const students = loadStudents();
  const headers = ['Nom','Prénom','J1 Avant20h','J1 Après20h','J2 Avant20h','J2 Après20h','J3 Avant20h','J3 Après20h','Score','Date'];
  const keys = ['j1m','j1e','j2m','j2e','j3m','j3e'];
  const rows = students.map(s => [
    s.nom, s.prenom,
    ...keys.map(k => s.slots[k]==='present'?'P':s.slots[k]==='absent'?'A':'—'),
    calcScore(s.slots)+'/6',
    s.date||''
  ]);
  const csv = [headers,...rows].map(r=>r.join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'presence_etudiants.csv';
  a.click();
  showToast('⬇️ CSV exporté !');
}

function resetAll() {
  if (!confirm('Effacer TOUTES les données ? Cette action est irréversible.')) return;
  saveStudents([]);
  loadAdmin();
  showToast('🗑️ Données effacées', '#c1121f');
}

// ===========================
// ADMIN TABS
// ===========================
const tabs = ['list','stats','qr','export'];
function switchTab(name) {
  tabs.forEach(t => {
    document.getElementById('atab-'+t).style.display = t===name?'block':'none';
  });
  document.querySelectorAll('.atab').forEach((b,i) => {
    b.classList.toggle('active', tabs[i]===name);
  });
  if (name==='stats') renderSlotBars(loadStudents());
  if (name==='export') { renderExportTable(loadStudents()); }
  if (name==='qr') { generateQR('admin-qr'); }
}

// ===========================
// TOAST
// ===========================
function showToast(msg, bg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.style.background = bg || 'var(--accent)';
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

// ===========================
// INIT
// ===========================
window.onload = function() {
  initQRs();
  // Auto-redirect if QR param
  const params = new URLSearchParams(window.location.search);
  if (params.get('student') === '1') {
    showPage('page-student');
  }
};
</script>
</body>
</html>
