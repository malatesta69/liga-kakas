<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎰 LIGA KAKAS LEGENDARY</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow+Condensed:wght@300;400;600;700&display=swap');
  :root {
    --gold: #FFD700; --gold2: #FFA500; --dark: #0a0a0f; --dark2: #111118;
    --dark3: #1a1a25; --card: #15151f; --card2: #1e1e2e; --green: #00ff88;
    --red: #ff3355; --blue: #4488ff; --purple: #9944ff; --text: #e8e8f0; --muted: #888899;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:var(--dark); color:var(--text); font-family:'Barlow Condensed',sans-serif; min-height:100vh; overflow-x:hidden; }

  /* LOGIN */
  #loginScreen { position:fixed; inset:0; background:var(--dark); display:flex; align-items:center; justify-content:center; z-index:1000; background-image:radial-gradient(ellipse at 20% 50%,rgba(255,215,0,.05) 0%,transparent 50%),radial-gradient(ellipse at 80% 20%,rgba(153,68,255,.05) 0%,transparent 40%); }
  .login-box { background:var(--card); border:1px solid rgba(255,215,0,.2); border-radius:16px; padding:48px 40px; width:400px; max-width:95vw; text-align:center; box-shadow:0 0 60px rgba(255,215,0,.08),0 20px 60px rgba(0,0,0,.5); animation:loginAppear .6s cubic-bezier(.34,1.56,.64,1); }
  @keyframes loginAppear { from{opacity:0;transform:translateY(30px) scale(.95)} to{opacity:1;transform:translateY(0) scale(1)} }
  .login-logo { font-family:'Bebas Neue',sans-serif; font-size:52px; letter-spacing:4px; background:linear-gradient(135deg,var(--gold),var(--gold2)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; line-height:1; margin-bottom:4px; }
  .login-subtitle { color:var(--muted); font-size:13px; letter-spacing:3px; text-transform:uppercase; margin-bottom:28px; }
  .player-select { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:16px; }
  .player-btn { background:var(--dark3); border:1px solid rgba(255,255,255,.08); color:var(--text); padding:12px 8px; border-radius:10px; font-family:'Barlow Condensed',sans-serif; font-size:15px; font-weight:600; cursor:pointer; transition:all .2s; letter-spacing:1px; }
  .player-btn:hover { border-color:var(--gold); color:var(--gold); background:rgba(255,215,0,.06); transform:translateY(-2px); }
  .player-btn.selected { border-color:var(--gold); background:rgba(255,215,0,.12); color:var(--gold); }
  .admin-btn { background:rgba(153,68,255,.1); border-color:rgba(153,68,255,.3); color:#bb88ff; grid-column:1/-1; font-size:13px; letter-spacing:2px; }
  .admin-btn:hover,.admin-btn.selected { border-color:var(--purple); color:var(--purple); background:rgba(153,68,255,.2); }
  .password-input { width:100%; background:var(--dark3); border:1px solid rgba(255,255,255,.1); color:var(--text); padding:14px 16px; border-radius:10px; font-family:'Barlow Condensed',sans-serif; font-size:16px; letter-spacing:4px; margin-bottom:14px; text-align:center; transition:border-color .2s; }
  .password-input:focus { outline:none; border-color:var(--gold); }
  .login-btn { width:100%; background:linear-gradient(135deg,var(--gold),var(--gold2)); color:var(--dark); border:none; padding:15px; border-radius:10px; font-family:'Bebas Neue',sans-serif; font-size:20px; letter-spacing:3px; cursor:pointer; transition:all .2s; }
  .login-btn:hover { transform:translateY(-2px); box-shadow:0 8px 25px rgba(255,215,0,.3); }
  .login-error { color:var(--red); font-size:13px; margin-top:10px; min-height:20px; letter-spacing:1px; }
  @keyframes shake { 0%,100%{transform:translateX(0)} 25%{transform:translateX(-8px)} 75%{transform:translateX(8px)} }
  .shake { animation:shake .3s; }

  /* APP */
  #app { display:none; }
  .header { background:linear-gradient(180deg,rgba(255,215,0,.05) 0%,transparent 100%); border-bottom:1px solid rgba(255,215,0,.15); padding:0 24px; display:flex; align-items:center; justify-content:space-between; height:64px; position:sticky; top:0; z-index:100; backdrop-filter:blur(10px); }
  .header-logo { font-family:'Bebas Neue',sans-serif; font-size:28px; letter-spacing:3px; background:linear-gradient(135deg,var(--gold),var(--gold2)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; }
  .user-badge { background:rgba(255,215,0,.1); border:1px solid rgba(255,215,0,.2); color:var(--gold); padding:6px 14px; border-radius:20px; font-size:14px; font-weight:600; letter-spacing:1px; }
  .admin-badge { background:rgba(153,68,255,.15); border-color:rgba(153,68,255,.3); color:#bb88ff; }
  .logout-btn { background:none; border:1px solid rgba(255,255,255,.1); color:var(--muted); padding:6px 12px; border-radius:8px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:13px; letter-spacing:1px; transition:all .2s; margin-left:10px; }
  .logout-btn:hover { border-color:var(--red); color:var(--red); }
  .nav { background:var(--dark2); border-bottom:1px solid rgba(255,255,255,.05); padding:0 24px; display:flex; gap:4px; overflow-x:auto; }
  .nav-tab { background:none; border:none; color:var(--muted); padding:14px 16px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:15px; font-weight:600; letter-spacing:1px; border-bottom:2px solid transparent; transition:all .2s; white-space:nowrap; }
  .nav-tab:hover { color:var(--text); }
  .nav-tab.active { color:var(--gold); border-bottom-color:var(--gold); }
  .main { padding:24px; max-width:1100px; margin:0 auto; }
  
  /* CARDS */
  .card { background:var(--card); border:1px solid rgba(255,255,255,.06); border-radius:14px; padding:20px; margin-bottom:16px; }
  .card-title { font-size:14px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; margin-bottom:16px; }
  .card-value { font-family:'Bebas Neue',sans-serif; font-size:36px; letter-spacing:2px; }
  .positive { color:var(--green); }
  .negative { color:var(--red); }
  .section-title { font-family:'Bebas Neue',sans-serif; font-size:26px; letter-spacing:3px; color:var(--gold); margin-bottom:20px; }
  .grid-2 { display:grid; grid-template-columns:1fr 1fr; gap:16px; }
  .grid-3 { display:grid; grid-template-columns:1fr 1fr 1fr; gap:16px; }
  .grid-4 { display:grid; grid-template-columns:repeat(4,1fr); gap:12px; }
  @media(max-width:600px) { .grid-2,.grid-3,.grid-4 { grid-template-columns:1fr; } }
  
  /* RANKING */
  .rank-card { background:var(--card); border:1px solid rgba(255,255,255,.06); border-radius:14px; padding:16px 20px; display:flex; align-items:center; gap:16px; margin-bottom:10px; transition:all .2s; }
  .rank-card:hover { border-color:rgba(255,215,0,.2); }
  .rank-num { font-family:'Bebas Neue',sans-serif; font-size:32px; color:var(--muted); min-width:40px; }
  .rank-num.gold { color:var(--gold); }
  .rank-num.silver { color:#c0c0c0; }
  .rank-num.bronze { color:#cd7f32; }
  .player-name { font-size:20px; font-weight:700; letter-spacing:1px; flex:1; }
  .banca-val { font-family:'Bebas Neue',sans-serif; font-size:28px; }
  .profit-pos { color:var(--green); }
  .profit-neg { color:var(--red); }
  
  /* STATS */
  .mini-stat { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid rgba(255,255,255,.04); }
  .mini-stat:last-child { border-bottom:none; }
  .mini-stat-label { color:var(--muted); font-size:14px; letter-spacing:1px; }
  .mini-stat-value { font-weight:700; font-size:18px; }
  
  /* TABLE */
  .data-table { width:100%; border-collapse:collapse; font-size:14px; }
  .data-table th { color:var(--muted); font-size:12px; letter-spacing:2px; text-transform:uppercase; padding:10px 12px; text-align:left; border-bottom:1px solid rgba(255,255,255,.08); }
  .data-table td { padding:10px 12px; border-bottom:1px solid rgba(255,255,255,.03); }
  .data-table tr:hover td { background:rgba(255,255,255,.02); }
  
  /* BADGES */
  .badge-win { background:rgba(0,255,136,.15); color:var(--green); border:1px solid rgba(0,255,136,.3); padding:3px 10px; border-radius:20px; font-size:12px; font-weight:700; letter-spacing:1px; }
  .badge-lose { background:rgba(255,51,85,.15); color:var(--red); border:1px solid rgba(255,51,85,.3); padding:3px 10px; border-radius:20px; font-size:12px; font-weight:700; letter-spacing:1px; }
  .badge-pending { background:rgba(255,165,0,.15); color:var(--gold2); border:1px solid rgba(255,165,0,.3); padding:3px 10px; border-radius:20px; font-size:12px; font-weight:700; letter-spacing:1px; }
  .badge-approval { background:rgba(68,136,255,.15); color:var(--blue); border:1px solid rgba(68,136,255,.3); padding:3px 10px; border-radius:20px; font-size:12px; font-weight:700; letter-spacing:1px; }
  
  /* FORMS */
  .form-group { margin-bottom:16px; }
  .form-label { display:block; color:var(--muted); font-size:12px; letter-spacing:2px; text-transform:uppercase; margin-bottom:8px; }
  .form-input,.form-select { width:100%; background:var(--dark3); border:1px solid rgba(255,255,255,.1); color:var(--text); padding:12px 14px; border-radius:10px; font-family:'Barlow Condensed',sans-serif; font-size:16px; transition:border-color .2s; }
  .form-input:focus,.form-select:focus { outline:none; border-color:var(--gold); }
  .form-select option { background:var(--dark3); }
  .form-row { display:grid; grid-template-columns:1fr 1fr; gap:14px; }
  @media(max-width:500px) { .form-row { grid-template-columns:1fr; } }
  .btn-primary { background:linear-gradient(135deg,var(--gold),var(--gold2)); color:var(--dark); border:none; padding:14px 28px; border-radius:10px; font-family:'Bebas Neue',sans-serif; font-size:18px; letter-spacing:2px; cursor:pointer; transition:all .2s; }
  .btn-primary:hover { transform:translateY(-2px); box-shadow:0 8px 25px rgba(255,215,0,.25); }
  .btn-primary:disabled { opacity:.4; cursor:not-allowed; transform:none; }
  .btn-small { background:rgba(0,255,136,.15); border:1px solid rgba(0,255,136,.3); color:var(--green); padding:5px 12px; border-radius:6px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:13px; letter-spacing:1px; transition:all .2s; }
  .btn-small:hover { background:rgba(0,255,136,.25); }
  .btn-danger { background:rgba(255,51,85,.15); border:1px solid rgba(255,51,85,.3); color:var(--red); padding:5px 12px; border-radius:6px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:13px; letter-spacing:1px; transition:all .2s; }
  .btn-danger:hover { background:rgba(255,51,85,.25); }
  .btn-blue { background:rgba(68,136,255,.15); border:1px solid rgba(68,136,255,.3); color:var(--blue); padding:5px 12px; border-radius:6px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:13px; letter-spacing:1px; transition:all .2s; }
  .admin-panel { background:rgba(153,68,255,.06); border:1px solid rgba(153,68,255,.15); border-radius:14px; padding:20px; margin-bottom:16px; }
  .admin-title { color:#bb88ff; font-size:14px; letter-spacing:2px; text-transform:uppercase; margin-bottom:16px; }
  
  /* JACKPOT */
  .jackpot-display { background:linear-gradient(135deg,rgba(255,215,0,.1),rgba(255,165,0,.05)); border:1px solid rgba(255,215,0,.3); border-radius:16px; padding:32px; text-align:center; margin-bottom:20px; }
  .jackpot-label { color:var(--muted); font-size:13px; letter-spacing:3px; text-transform:uppercase; margin-bottom:8px; }
  .jackpot-amount { font-family:'Bebas Neue',sans-serif; font-size:64px; letter-spacing:4px; color:var(--gold); line-height:1; }
  
  /* RULETA */
  .ruleta-board { display:grid; grid-template-columns:repeat(7,1fr); gap:4px; max-width:360px; margin:0 auto 20px; }
  .ruleta-num { width:100%; aspect-ratio:1; border-radius:6px; display:flex; align-items:center; justify-content:center; font-weight:700; font-size:14px; cursor:pointer; transition:all .15s; border:2px solid transparent; user-select:none; }
  .ruleta-num.rojo { background:#c0392b; color:#fff; }
  .ruleta-num.negro { background:#1a1a1a; color:#fff; border-color:rgba(255,255,255,.2); }
  .ruleta-num.verde { background:#27ae60; color:#fff; }
  .ruleta-num.selected { transform:scale(1.15); border-color:var(--gold) !important; box-shadow:0 0 12px rgba(255,215,0,.5); }
  .ruleta-spinning { font-family:'Bebas Neue',sans-serif; font-size:80px; text-align:center; padding:20px; animation:spin .5s linear infinite; }
  @keyframes spin { from{transform:rotate(0deg)} to{transform:rotate(360deg)} }
  .ruleta-result { font-family:'Bebas Neue',sans-serif; font-size:80px; text-align:center; padding:20px 0; }
  
  /* CASINO TIPOS */
  .casino-tipo-btn { background:var(--dark3); border:1px solid rgba(255,255,255,.08); color:var(--text); padding:10px 14px; border-radius:10px; cursor:pointer; font-family:'Barlow Condensed',sans-serif; font-size:15px; font-weight:600; letter-spacing:1px; transition:all .2s; text-align:center; }
  .casino-tipo-btn:hover { border-color:var(--gold); color:var(--gold); }
  .casino-tipo-btn.active { border-color:var(--gold); background:rgba(255,215,0,.1); color:var(--gold); }
  
  /* RACHAS */
  .racha-pos { background:rgba(0,255,136,.1); color:var(--green); border:1px solid rgba(0,255,136,.2); padding:2px 8px; border-radius:4px; font-size:12px; font-weight:700; }
  .racha-neg { background:rgba(255,51,85,.1); color:var(--red); border:1px solid rgba(255,51,85,.2); padding:2px 8px; border-radius:4px; font-size:12px; font-weight:700; }
  
  /* TOAST */
  .toast { position:fixed; bottom:24px; left:50%; transform:translateX(-50%) translateY(80px); background:var(--card2); border:1px solid rgba(255,255,255,.1); border-radius:12px; padding:14px 24px; font-size:15px; font-weight:600; letter-spacing:1px; z-index:9999; transition:transform .3s cubic-bezier(.34,1.56,.64,1); pointer-events:none; }
  .toast.show { transform:translateX(-50%) translateY(0); }
  .toast.success { border-color:rgba(0,255,136,.4); color:var(--green); }
  .toast.error { border-color:rgba(255,51,85,.4); color:var(--red); }
  
  /* NOTIF BADGE */
  .notif-badge { background:var(--red); color:#fff; border-radius:50%; width:18px; height:18px; font-size:11px; font-weight:700; display:inline-flex; align-items:center; justify-content:center; margin-left:4px; vertical-align:middle; }
  
  /* PRESTAMOS */
  .loan-card { background:var(--dark3); border:1px solid rgba(255,255,255,.06); border-radius:10px; padding:14px; margin-bottom:10px; }
  
  /* TIENDA */
  .shop-item { background:var(--dark3); border:1px solid rgba(255,215,0,.1); border-radius:12px; padding:16px; text-align:center; cursor:pointer; transition:all .2s; }
  .shop-item:hover { border-color:rgba(255,215,0,.3); transform:translateY(-2px); }
  .shop-price { font-family:'Bebas Neue',sans-serif; font-size:28px; color:var(--gold); }

  /* RULETA 3D CANVAS */
  #roulette-canvas { border-radius:50%; box-shadow:0 0 40px rgba(255,215,0,.3), 0 0 80px rgba(0,0,0,.8); display:block; margin:0 auto; }
  #roulette-wrap { position:relative; display:inline-block; }
  #roulette-pointer { position:absolute; top:-12px; left:50%; transform:translateX(-50%); width:0; height:0; border-left:10px solid transparent; border-right:10px solid transparent; border-top:24px solid var(--gold); filter:drop-shadow(0 0 6px rgba(255,215,0,.8)); z-index:10; }
  #center-display { position:absolute; top:50%; left:50%; transform:translate(-50%,-50%); text-align:center; background:rgba(0,0,0,.85); border-radius:50%; width:80px; height:80px; display:flex; align-items:center; justify-content:center; border:3px solid rgba(255,215,0,.4); pointer-events:none; }
  #center-num { font-family:'Bebas Neue',sans-serif; font-size:36px; color:var(--gold); line-height:1; }

  /* EVENTOS POOL */
  .evento-card { background:var(--dark3); border:1px solid rgba(255,215,0,.15); border-radius:14px; padding:18px; margin-bottom:14px; }
  .evento-card.activo { border-color:rgba(0,255,136,.3); }
  .evento-card.cerrado { border-color:rgba(255,51,85,.2); opacity:.8; }
  .evento-cuota-badge { background:rgba(255,215,0,.1); color:var(--gold); border:1px solid rgba(255,215,0,.3); padding:4px 12px; border-radius:20px; font-family:'Bebas Neue',sans-serif; font-size:18px; letter-spacing:1px; }
  .apostadores-list { display:flex; flex-wrap:wrap; gap:8px; margin-top:10px; }
  .apostador-chip { background:rgba(255,255,255,.06); border:1px solid rgba(255,255,255,.1); border-radius:20px; padding:4px 12px; font-size:13px; font-weight:600; }
</style>
</head>
<body>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- LOGIN -->
<div id="loginScreen">
  <div class="login-box">
    <div class="login-logo">🎰 LIGA</div>
    <div class="login-logo" style="font-size:36px;margin-top:-8px">KAKAS</div>
    <div class="login-subtitle">Legendary · Temporada 2026</div>
    <div class="player-select">
      <button class="player-btn" onclick="selectUser('Alex')">🎯 Alex</button>
      <button class="player-btn" onclick="selectUser('Nicolas')">🎲 Nicolas</button>
      <button class="player-btn" onclick="selectUser('Raúl')">🔥 Raúl</button>
      <button class="player-btn" onclick="selectUser('Pablo')">⚡ Pablo</button>
      <button class="player-btn" onclick="selectUser('Mauro')">💀 Mauro</button>
      <button class="player-btn" onclick="selectUser('Manuel')">👑 Manuel</button>
      <button class="player-btn admin-btn" onclick="selectUser('ADMIN')">⚙️ ADMINISTRADOR</button>
    </div>
    <input type="password" class="password-input" id="pwInput" placeholder="Contraseña" onkeydown="if(event.key==='Enter')doLogin()">
    <button class="login-btn" onclick="doLogin()">ENTRAR</button>
    <div class="login-error" id="loginError"></div>
  </div>
</div>

<!-- APP -->
<div id="app">
  <div class="header">
    <div class="header-logo">🎰 Liga Kakas</div>
    <div style="display:flex;align-items:center;gap:8px">
      <span class="user-badge" id="userBadge"></span>
      <button class="logout-btn" onclick="logout()">SALIR</button>
    </div>
  </div>
  <div class="nav" id="mainNav"></div>
  <div class="main">
    <div id="mainContent"></div>
  </div>
</div>

<!-- SUPABASE VIA FETCH REST -->
<script>
// ============================================================
// CAPA DE PERSISTENCIA — Supabase REST API (fetch directo)
// ============================================================
const SUPABASE_URL = 'https://quskapvvehyhcssbbeog.supabase.co';
const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InF1c2thcHZ2ZWh5aGNzc2JiZW9nIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzE1OTM1NzksImV4cCI6MjA4NzE2OTU3OX0.BIKQOAK2a-VGT63kJn7RFEXVyxgek9dSOmSE5qvJciU';

async function sbFetch(path, method = 'GET', body = null, extraHeaders = {}) {
  const res = await fetch(`${SUPABASE_URL}/rest/v1/${path}`, {
    method,
    headers: {
      'apikey': SUPABASE_KEY,
      'Authorization': `Bearer ${SUPABASE_KEY}`,
      'Content-Type': 'application/json',
      'Prefer': method === 'POST' ? 'return=representation' : '',
      ...extraHeaders
    },
    body: body ? JSON.stringify(body) : undefined
  });
  if (!res.ok) {
    const err = await res.text();
    throw new Error(err);
  }
  const text = await res.text();
  return text ? JSON.parse(text) : null;
}

const DB = {
  async getAll(table) {
    const data = await sbFetch(`${table}?select=*&order=id.asc`);
    return data || [];
  },
  async insert(table, row) {
    const clean = { ...row };
    delete clean.id;
    const data = await sbFetch(table, 'POST', clean, { 'Prefer': 'return=representation' });
    return Array.isArray(data) ? data[0] : data;
  },
  async update(table, id, fields) {
    await sbFetch(`${table}?id=eq.${id}`, 'PATCH', fields, { 'Prefer': 'return=minimal' });
  },
  async delete(table, id) {
    await sbFetch(`${table}?id=eq.${id}`, 'DELETE', null, { 'Prefer': 'return=minimal' });
  },
  async getConfig(clave) {
    const data = await sbFetch(`config?clave=eq.${encodeURIComponent(clave)}&select=valor`);
    return data && data.length > 0 ? data[0].valor : null;
  },
  async setConfig(clave, valor) {
    await sbFetch('config', 'POST', { clave, va
