<div dir="rtl"># </div>  
<!DOCTYPE html>  
  
<html lang="ar" dir="rtl">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>نظام التحقق من الدخول — Zed West v2</title>  
<meta name="version" content="2.0-1777934490">  
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">  
<style>  
  :root {  
    --bg: #0a0e14; --surface: #111822; --surface2: #162030;  
    --border: #1e3a5f; --accent: #00b4d8; --accent2: #0077a8;  
    --success: #00e676; --danger: #ff1744; --warning: #ffc400;  
    --text: #e8f4fd; --muted: #5a7a99;  
  }  
  * { margin:0; padding:0; box-sizing:border-box; }  
  body { background:var(--bg); color:var(--text); font-family:'Cairo',sans-serif; min-height:100vh; overflow-x:hidden; position:relative; }  
  body::before {  
    content:''; position:fixed; inset:0;  
    background-image: linear-gradient(rgba(0,180,216,0.04) 1px,transparent 1px), linear-gradient(90deg,rgba(0,180,216,0.04) 1px,transparent 1px);  
    background-size:40px 40px; pointer-events:none; z-index:0;  
  }  
  body::after {  
    content:''; position:fixed; top:0; left:0; right:0; height:2px;  
    background:linear-gradient(90deg,transparent,var(--accent),transparent);  
    animation:scanline 5s linear infinite; z-index:1; opacity:0.5;  
  }  
  @keyframes scanline { 0%{transform:translateY(0)} 100%{transform:translateY(100vh)} }  
  
.container { position:relative; z-index:2; max-width:720px; margin:0 auto; padding:36px 20px; }  
  
/* HEADER */  
.header { text-align:center; margin-bottom:32px; animation:fadeDown 0.6s ease both; }  
.logo-ring {  
width:68px; height:68px; border:2px solid var(–accent); border-radius:50%;  
margin:0 auto 14px; display:flex; align-items:center; justify-content:center;  
position:relative; animation:pulse-ring 3s ease infinite;  
}  
.logo-ring::before { content:’’; position:absolute; inset:-6px; border-radius:50%; border:1px solid rgba(0,180,216,0.2); animation:pulse-ring 3s ease infinite 0.5s; }  
@keyframes pulse-ring { 0%,100%{box-shadow:0 0 0 0 rgba(0,180,216,0.3)} 50%{box-shadow:0 0 0 8px rgba(0,180,216,0)} }  
.shield-icon { font-size:28px; line-height:1; }  
.header h1 { font-size:1.8rem; font-weight:700; }  
.header h1 span { color:var(–accent); }  
.header p { margin-top:4px; color:var(–muted); font-size:0.82rem; font-family:‘Rajdhani’,sans-serif; letter-spacing:3px; text-transform:uppercase; }  
  
/* CONNECTION STATUS */  
.conn-bar {  
display:flex; align-items:center; justify-content:center; gap:8px;  
background:var(–surface); border:1px solid var(–border); border-radius:8px;  
padding:8px 16px; margin-bottom:24px; font-size:0.78rem;  
font-family:‘Rajdhani’,sans-serif; letter-spacing:1px;  
animation:fadeUp 0.5s ease 0.1s both;  
}  
.conn-dot { width:7px; height:7px; border-radius:50%; flex-shrink:0; }  
.conn-dot.live { background:var(–success); box-shadow:0 0 6px var(–success); animation:blink 2s infinite; }  
.conn-dot.loading { background:var(–warning); animation:blink 0.6s infinite; }  
.conn-dot.error { background:var(–danger); }  
.conn-dot.idle { background:var(–muted); }  
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }  
.conn-text { color:var(–muted); }  
.conn-text.live { color:var(–success); }  
.conn-text.error { color:var(–danger); }  
.conn-refresh {  
margin-right: auto; background:transparent; border:1px solid var(–border);  
color:var(–muted); padding:2px 10px; border-radius:6px; cursor:pointer;  
font-family:‘Rajdhani’,sans-serif; font-size:0.72rem; letter-spacing:1px;  
transition:all 0.2s;  
}  
.conn-refresh:hover { border-color:var(–accent); color:var(–accent); }  
.conn-count { color:var(–accent); font-weight:700; margin-right:4px; }  
  
/* SEARCH */  
.search-wrap { margin-bottom:20px; animation:fadeUp 0.6s ease 0.2s both; }  
.search-label { font-size:0.78rem; color:var(–muted); font-family:‘Rajdhani’,sans-serif; letter-spacing:2px; text-transform:uppercase; margin-bottom:8px; display:block; }  
.search-box { display:flex; gap:10px; }  
.search-input-wrap { flex:1; position:relative; }  
#unitInput {  
width:100%; background:var(–surface); border:1.5px solid var(–border);  
color:var(–text); padding:15px 20px; border-radius:12px;  
font-family:‘Rajdhani’,sans-serif; font-size:1.6rem; font-weight:700;  
letter-spacing:3px; text-align:center; outline:none;  
transition:border-color 0.25s, box-shadow 0.25s; direction:ltr;  
}  
#unitInput::placeholder { color:var(–muted); font-weight:400; letter-spacing:1px; font-size:1rem; }  
#unitInput:focus { border-color:var(–accent); box-shadow:0 0 0 3px rgba(0,180,216,0.15); }  
#unitInput:disabled { opacity:0.4; cursor:not-allowed; }  
.search-btn {  
background:var(–accent); color:var(–bg); border:none; padding:0 26px;  
border-radius:12px; font-family:‘Cairo’,sans-serif; font-size:1rem;  
font-weight:700; cursor:pointer; transition:background 0.2s,transform 0.1s; white-space:nowrap;  
}  
.search-btn:hover { background:#00d4f8; }  
.search-btn:active { transform:scale(0.96); }  
.search-btn:disabled { opacity:0.4; cursor:not-allowed; }  
.clear-btn {  
background:transparent; color:var(–muted); border:1px solid var(–border);  
padding:0 16px; border-radius:12px; font-family:‘Cairo’,sans-serif;  
font-size:0.9rem; cursor:pointer; transition:all 0.2s;  
}  
.clear-btn:hover { border-color:var(–muted); color:var(–text); }  
  
/* SUGGESTIONS */  
.suggestions {  
position:absolute; top:calc(100% + 4px); left:0; right:0;  
background:var(–surface2); border:1px solid var(–border); border-radius:10px;  
z-index:100; max-height:200px; overflow-y:auto; box-shadow:0 8px 24px rgba(0,0,0,0.5);  
}  
.suggestion-item { padding:10px 16px; cursor:pointer; font-family:‘Rajdhani’,sans-serif; font-size:1rem; letter-spacing:1px; transition:background 0.15s; direction:ltr; text-align:left; }  
.suggestion-item:hover, .suggestion-item.active { background:rgba(0,180,216,0.1); color:var(–accent); }  
.suggestion-item mark { background:transparent; color:var(–accent); font-weight:700; }  
  
/* RESULTS */  
.results-area { margin-top:24px; }  
.result-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:16px; }  
.unit-badge { background:var(–surface2); border:1px solid var(–accent); color:var(–accent); padding:6px 18px; border-radius:20px; font-family:‘Rajdhani’,sans-serif; font-size:1.1rem; font-weight:700; letter-spacing:2px; }  
.status-pill { padding:5px 14px; border-radius:20px; font-size:0.72rem; font-family:‘Rajdhani’,sans-serif; font-weight:700; letter-spacing:1px; text-transform:uppercase; }  
.status-occupied-owner { background:rgba(0,230,118,0.1); color:var(–success); border:1px solid rgba(0,230,118,0.3); }  
.status-occupied-tenant { background:rgba(255,196,0,0.1); color:var(–warning); border:1px solid rgba(255,196,0,0.3); }  
.status-not-occupied { background:rgba(90,122,153,0.15); color:var(–muted); border:1px solid rgba(90,122,153,0.3); }  
  
.cards-grid { display:grid; gap:10px; }  
.info-card { background:var(–surface); border:1px solid var(–border); border-radius:12px; padding:16px 20px; animation:slideIn 0.3s ease both; transition:border-color 0.2s; }  
.info-card:hover { border-color:var(–accent2); }  
@keyframes slideIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }  
  
.card-section-label { font-size:0.68rem; color:var(–muted); font-family:‘Rajdhani’,sans-serif; letter-spacing:2px; text-transform:uppercase; margin-bottom:10px; display:flex; align-items:center; gap:8px; }  
.card-section-label::after { content:’’; flex:1; height:1px; background:var(–border); }  
  
.person-row { display:flex; align-items:center; gap:12px; padding:8px 0; }  
.person-row:not(:last-child) { border-bottom:1px solid rgba(30,58,95,0.5); }  
.avatar { width:40px; height:40px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:1rem; font-weight:700; color:white; flex-shrink:0; }  
.avatar.owner-av { background:linear-gradient(135deg,#005f8a,#00b4d8); }  
.avatar.tenant-av { background:linear-gradient(135deg,#7a5c00,#ffc400); color:#1a1000; }  
.avatar.delegate-av { background:linear-gradient(135deg,#2a2a5a,#6464c8); }  
.avatar.pm-av { background:linear-gradient(135deg,#2a5a2a,#00c853); }  
.person-info { flex:1; min-width:0; }  
.person-name { font-size:0.95rem; font-weight:700; color:var(–text); }  
.person-sub { font-size:0.75rem; color:var(–muted); font-family:‘Rajdhani’,sans-serif; margin-top:2px; }  
.person-tag { padding:3px 10px; border-radius:12px; font-size:0.68rem; font-family:‘Rajdhani’,sans-serif; font-weight:700; letter-spacing:1px; white-space:nowrap; }  
.tag-owner { background:rgba(0,180,216,0.12); color:var(–accent); border:1px solid rgba(0,180,216,0.25); }  
.tag-tenant { background:rgba(255,196,0,0.12); color:var(–warning); border:1px solid rgba(255,196,0,0.25); }  
.tag-delegate { background:rgba(100,100,200,0.12); color:#9898e8; border:1px solid rgba(100,100,200,0.25); }  
.tag-pm { background:rgba(0,200,83,0.12); color:#00c853; border:1px solid rgba(0,200,83,0.25); }  
  
/* WP */  
.wp-row { display:flex; align-items:flex-start; gap:12px; padding:10px 0; }  
.wp-row:not(:last-child) { border-bottom:1px solid rgba(30,58,95,0.5); }  
.wp-icon { font-size:1.1rem; flex-shrink:0; margin-top:2px; }  
.wp-info { flex:1; min-width:0; }  
.wp-desc { font-size:0.92rem; font-weight:700; color:var(–text); margin-bottom:3px; }  
.wp-meta { font-size:0.73rem; color:var(–muted); font-family:‘Rajdhani’,sans-serif; }  
.wp-days { padding:3px 10px; border-radius:12px; font-size:0.7rem; font-family:‘Rajdhani’,sans-serif; font-weight:700; white-space:nowrap; flex-shrink:0; }  
.wp-active { background:rgba(0,230,118,0.1); color:var(–success); border:1px solid rgba(0,230,118,0.3); }  
.wp-expired { background:rgba(255,23,68,0.08); color:#ff6b8a; border:1px solid rgba(255,23,68,0.2); }  
  
/* STATES */  
.state-card { background:var(–surface); border:1px solid var(–border); border-radius:12px; padding:48px 24px; text-align:center; }  
.state-icon { font-size:2.5rem; margin-bottom:12px; }  
.state-title { font-size:1.1rem; font-weight:700; margin-bottom:6px; }  
.state-sub { font-size:0.85rem; color:var(–muted); }  
.state-card.not-found .state-title { color:var(–danger); }  
  
/* LOADING SKELETON */  
.skeleton { background:linear-gradient(90deg,var(–surface) 25%,var(–surface2) 50%,var(–surface) 75%); background-size:200% 100%; animation:shimmer 1.2s infinite; border-radius:8px; }  
@keyframes shimmer { 0%{background-position:200% 0} 100%{background-position:-200% 0} }  
  
@keyframes fadeDown { from{opacity:0;transform:translateY(-16px)} to{opacity:1;transform:translateY(0)} }  
@keyframes fadeUp { from{opacity:0;transform:translateY(14px)} to{opacity:1;transform:translateY(0)} }  
  
.hidden { display:none!important; }  
.footer { text-align:center; margin-top:40px; font-size:0.7rem; color:var(–muted); font-family:‘Rajdhani’,sans-serif; letter-spacing:1px; opacity:0.4; }  
</style>  
  
</head>  
<body>  
<div class="container">  
  
  <div class="header">  
    <div class="logo-ring"><span class="shield-icon">🛡</span></div>  
    <h1>نظام التحقق من <span>الدخول</span></h1>  
    <p>ZED WEST — LIVE ACCESS CONTROL</p>  
  </div>  
  
  <!-- Connection Bar -->  
  
  <div class="conn-bar" id="connBar">  
    <div class="conn-dot idle" id="connDot"></div>  
    <span class="conn-text" id="connText">جاري تحميل البيانات...</span>  
    <span id="connCount" class="hidden"><span class="conn-count" id="unitCountEl">0</span> وحدة</span>  
    <button class="conn-refresh" onclick="loadAllData()" id="refreshBtn">↻ تحديث</button>  
  </div>  
  
  <!-- Search -->  
  
  <div class="search-wrap">  
    <label class="search-label">رقم الوحدة</label>  
    <div class="search-box">  
      <div class="search-input-wrap">  
        <input type="text" id="unitInput" placeholder="E1-A1-1-1" autocomplete="off"  
          oninput="onInput()" onkeydown="onKey(event)" disabled>  
        <div class="suggestions hidden" id="suggestions"></div>  
      </div>  
      <button class="search-btn" onclick="doSearch()" id="searchBtn" disabled>بحث</button>  
      <button class="clear-btn" onclick="clearSearch()">✕</button>  
    </div>  
  </div>  
  
  <div class="results-area hidden" id="results"></div>  
  
  <div class="footer">OPM — COMMUNITY MANAGEMENT | ZED WEST | LIVE DATA</div>  
</div>  
  
<script>  
// ============================================================  
//  CONFIG  
// ============================================================  
const SHEET_ID = '1iLKP5in6B3j7HvxlF7WYJa4lGA-P4tFRacl-zbdWydU';  
const API_KEY  = 'AIzaSyAOOAQXGjowVp-O8zsrtiw9RlN2IJKficQ';  
  
const SHEETS = {  
  occ:  [' Occupation Status Final1B', ' Occupation Status Final2B', ' Occupation Status Final1A'],  
  ten:  ['Tenats Occupancy rate 1B',   'Tenats Occupancy rate 2B ', 'Tenats Occupancy rate 1A '],  
  del:  'Delegators',  
  pm:   'PM',  
  wp:   'WP',  
};  
  
// ============================================================  
//  STATE  
// ============================================================  
let DB_MAP = {};  
let DB_UNITS = [];  
let dataLoaded = false;  
let selectedIdx = -1;  
let filteredUnits = [];  
  
// ============================================================  
//  API HELPERS  
// ============================================================  
async function fetchRange(sheetName, range) {  
  const enc = encodeURIComponent(`${sheetName}!${range}`);  
  const url = `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/${enc}?key=${API_KEY}`;  
  const res = await fetch(url);  
  if (!res.ok) {  
    const err = await res.json();  
    throw new Error(err.error?.message || `HTTP ${res.status}`);  
  }  
  const data = await res.json();  
  return data.values || [];  
}  
  
function fmt(val) {  
  if (!val || val === 'nan') return '';  
  // handle date strings like "2025-10-01T00:00:00"  
  const d = new Date(val);  
  if (!isNaN(d.getTime()) && val.includes('-') && val.length > 8) {  
    return d.toLocaleDateString('ar-EG', {day:'2-digit',month:'2-digit',year:'numeric'}).replace(/\//g,'/');  
  }  
  return val.trim();  
}  
  
function daysDiff(toStr) {  
  if (!toStr) return null;  
  const d = new Date(toStr);  
  if (isNaN(d)) return null;  
  return Math.round((d - new Date()) / 86400000);  
}  
  
// ============================================================  
//  LOAD ALL DATA  
// ============================================================  
async function loadAllData() {  
  setConn('loading', 'جاري تحميل البيانات من Google Sheets...');  
  document.getElementById('unitInput').disabled = true;  
  document.getElementById('searchBtn').disabled = true;  
  
  try {  
    // 1. Occupation status  
    const occMap = {};  
    for (const s of SHEETS.occ) {  
      const rows = await fetchRange(s, 'A1:F2000');  
      for (const row of rows.slice(1)) {  
        const unit = (row[1]||'').trim();  
        if (unit && unit !== 'Unit Name') {  
          occMap[unit] = { owner: (row[2]||'').trim(), status: (row[3]||'').trim() };  
        }  
      }  
    }  
  
    // 2. Tenants  
    const tenMap = {};  
    for (const s of SHEETS.ten) {  
      const rows = await fetchRange(s, 'A1:H2000');  
      for (const row of rows.slice(4)) {  
        const unit = (row[1]||'').trim();  
        const tenant = (row[3]||'').trim();  
        if (unit && unit !== 'nan' && tenant) {  
          tenMap[unit] = { tenant, from: fmt(row[5]||''), to: fmt(row[6]||''), toRaw: row[6]||'' };  
        }  
      }  
    }  
  
    // 3. Delegators  
    const delMap = {};  
    const delRows = await fetchRange(SHEETS.del, 'A1:B2000');  
    for (const row of delRows.slice(1)) {  
      const unit = (row[0]||'').trim();  
      const name = (row[1]||'').trim();  
      if (unit && name) {  
        if (!delMap[unit]) delMap[unit] = [];  
        delMap[unit].push(name);  
      }  
    }  
  
    // 4. PM  
    const pmMap = {};  
    const pmRows = await fetchRange(SHEETS.pm, 'A1:B2000');  
    for (const row of pmRows.slice(1)) {  
      const unit = (row[0]||'').trim();  
      const pm = (row[1]||'').trim();  
      if (unit && pm) pmMap[unit] = pm;  
    }  
  
    // 5. Work Permits  
    const wpMap = {};  
    const wpRows = await fetchRange(SHEETS.wp, 'A1:F2000');  
    for (const row of wpRows.slice(3)) {  
      const unit = (row[0]||'').trim();  
      const desc = (row[1]||'').trim();  
      if (!unit || unit === 'رقم الوحدة' || !desc) continue;  
      const toRaw = row[4]||'';  
      const days = daysDiff(toRaw);  
      if (!wpMap[unit]) wpMap[unit] = [];  
      wpMap[unit].push({  
        desc,  
        resp: (row[2]||'').trim().replace(/^(nan|لا يوجد)$/i,''),  
        from: fmt(row[3]||''),  
        to:   fmt(toRaw),  
        days,  
      });  
    }  
  
    // 6. Build unified DB  
    DB_MAP = {};  
    const allUnits = new Set([...Object.keys(occMap), ...Object.keys(wpMap)]);  
    for (const u of allUnits) {  
      const occ = occMap[u] || { owner:'', status:'' };  
      const ten = tenMap[u] || {};  
      DB_MAP[u.toLowerCase()] = {  
        unit: u,  
        owner: occ.owner,  
        status: occ.status,  
        tenant: ten.tenant||'',  
        tenantFrom: ten.from||'',  
        tenantTo: ten.to||'',  
        delegates: delMap[u]||[],  
        pm: pmMap[u]||'',  
        workPermits: wpMap[u]||[],  
      };  
    }  
  
    DB_UNITS = Object.values(DB_MAP).map(r => r.unit).sort();  
    dataLoaded = true;  
  
    setConn('live', `متصل — آخر تحديث ${new Date().toLocaleTimeString('ar-EG')}`, DB_UNITS.length);  
    document.getElementById('unitInput').disabled = false;  
    document.getElementById('searchBtn').disabled = false;  
    document.getElementById('unitInput').focus();  
  
  } catch(e) {  
    setConn('error', 'فشل الاتصال: ' + e.message);  
    console.error(e);  
  }  
}  
  
// ============================================================  
//  UI STATUS  
// ============================================================  
function setConn(type, text, count) {  
  const dot = document.getElementById('connDot');  
  const txt = document.getElementById('connText');  
  const cnt = document.getElementById('connCount');  
  const num = document.getElementById('unitCountEl');  
  dot.className = 'conn-dot ' + type;  
  txt.className = 'conn-text ' + type;  
  txt.textContent = text;  
  if (count !== undefined) {  
    num.textContent = count.toLocaleString('ar-EG');  
    cnt.classList.remove('hidden');  
  }  
}  
  
// ============================================================  
//  SEARCH  
// ============================================================  
function onInput() {  
  const q = document.getElementById('unitInput').value.trim();  
  if (q.length < 2) { hideSugs(); return; }  
  filteredUnits = DB_UNITS.filter(u => u.toLowerCase().includes(q.toLowerCase())).slice(0,10);  
  renderSugs(q);  
}  
  
function onKey(e) {  
  const items = document.querySelectorAll('.suggestion-item');  
  if (e.key==='ArrowDown') { selectedIdx=Math.min(selectedIdx+1,items.length-1); hilite(items); e.preventDefault(); }  
  else if (e.key==='ArrowUp') { selectedIdx=Math.max(selectedIdx-1,0); hilite(items); e.preventDefault(); }  
  else if (e.key==='Enter') {  
    if (selectedIdx>=0 && filteredUnits[selectedIdx]) {  
      document.getElementById('unitInput').value=filteredUnits[selectedIdx];  
      hideSugs(); doSearch();  
    } else { hideSugs(); doSearch(); }  
  } else if (e.key==='Escape') hideSugs();  
}  
  
function hilite(items) {  
  items.forEach((el,i) => el.classList.toggle('active', i===selectedIdx));  
}  
  
function renderSugs(q) {  
  const el = document.getElementById('suggestions');  
  if (!filteredUnits.length) { hideSugs(); return; }  
  el.innerHTML = filteredUnits.map((u,i) => {  
    const hi = u.replace(new RegExp('('+escRe(q)+')','gi'), '<mark>$1</mark>');  
    return `<div class="suggestion-item" onclick="selectUnit('${u}')">${hi}</div>`;  
  }).join('');  
  el.classList.remove('hidden');  
  selectedIdx = -1;  
}  
  
function hideSugs() { document.getElementById('suggestions').classList.add('hidden'); filteredUnits=[]; selectedIdx=-1; }  
function selectUnit(u) { document.getElementById('unitInput').value=u; hideSugs(); doSearch(); }  
function escRe(s) { return s.replace(/[.*+?^${}()|[\]\\]/g,'\\$&'); }  
  
function doSearch() {  
  hideSugs();  
  if (!dataLoaded) { return; }  
  const q = document.getElementById('unitInput').value.trim();  
  if (!q) return;  
  const rec = DB_MAP[q.toLowerCase()];  
  if (!rec) { showNotFound(q); return; }  
  showResult(rec);  
}  
  
function clearSearch() {  
  document.getElementById('unitInput').value='';  
  document.getElementById('results').classList.add('hidden');  
  hideSugs();  
  document.getElementById('unitInput').focus();  
}  
  
// ============================================================  
//  RENDER  
// ============================================================  
function statusClass(s) {  
  if (!s) return 'status-not-occupied';  
  const l = s.toLowerCase();  
  if (l.includes('owner')) return 'status-occupied-owner';  
  if (l.includes('tenant')) return 'status-occupied-tenant';  
  return 'status-not-occupied';  
}  
function statusLabel(s) {  
  if (!s) return 'غير محدد';  
  const l = s.toLowerCase();  
  if (l.includes('owner')) return 'مالك مقيم';  
  if (l.includes('tenant')) return 'مستأجر';  
  if (l.includes('not')) return 'غير مؤجرة';  
  return s;  
}  
function initials(name) {  
  const p = (name||'').trim().split(/[\s،,]+/);  
  return p.length>=2 ? p[0][0]+(p[1][0]||'') : (p[0]||'?')[0];  
}  
  
function showResult(r) {  
  let html = `  
    <div class="result-header">  
      <span class="unit-badge">${r.unit}</span>  
      <span class="status-pill ${statusClass(r.status)}">${statusLabel(r.status)}</span>  
    </div>  
    <div class="cards-grid">`;  
  
  // Owner  
  if (r.owner) {  
    html += `<div class="info-card">  
      <div class="card-section-label">المالك</div>  
      <div class="person-row">  
        <div class="avatar owner-av">${initials(r.owner)}</div>  
        <div class="person-info"><div class="person-name">${r.owner}</div><div class="person-sub">OWNER</div></div>  
        <span class="person-tag tag-owner">مالك</span>  
      </div></div>`;  
  }  
  
  // Tenants  
  if (r.tenant) {  
    const names = r.tenant.split(/[,،]+/).map(n=>n.trim()).filter(Boolean);  
    const rows = names.map(n=>`  
      <div class="person-row">  
        <div class="avatar tenant-av">${initials(n)}</div>  
        <div class="person-info">  
          <div class="person-name">${n}</div>  
          <div class="person-sub">${r.tenantFrom} ← → ${r.tenantTo}</div>  
        </div>  
        <span class="person-tag tag-tenant">مستأجر</span>  
      </div>`).join('');  
    html += `<div class="info-card"><div class="card-section-label">المستأجر</div>${rows}</div>`;  
  }  
  
  // Delegates  
  if (r.delegates.length) {  
    const rows = r.delegates.map(d=>`  
      <div class="person-row">  
        <div class="avatar delegate-av">${initials(d)}</div>  
        <div class="person-info"><div class="person-name">${d}</div><div class="person-sub">DELEGATE</div></div>  
        <span class="person-tag tag-delegate">مفوّض</span>  
      </div>`).join('');  
    html += `<div class="info-card"><div class="card-section-label">المفوّضون</div>${rows}</div>`;  
  }  
  
  // PM  
  if (r.pm) {  
    html += `<div class="info-card">  
      <div class="card-section-label">مدير العقار (PM)</div>  
      <div class="person-row">  
        <div class="avatar pm-av">${initials(r.pm)}</div>  
        <div class="person-info"><div class="person-name">${r.pm}</div><div class="person-sub">PROPERTY MANAGER</div></div>  
        <span class="person-tag tag-pm">PM</span>  
      </div></div>`;  
  }  
  
  // Work Permits  
  if (r.workPermits.length) {  
    const rows = r.workPermits.map(wp => {  
      const expired = wp.days !== null && wp.days < 0;  
      const active  = wp.days !== null && wp.days >= 0;  
      const daysLabel = wp.days !== null  
        ? (expired ? `منتهي منذ ${Math.abs(wp.days)} يوم` : `متبقي ${wp.days} يوم`) : '';  
      const daysClass = expired ? 'wp-expired' : (active ? 'wp-active' : '');  
      return `<div class="wp-row">  
        <div class="wp-icon">🔧</div>  
        <div class="wp-info">  
          <div class="wp-desc">${wp.desc}</div>  
          <div class="wp-meta">${wp.from} ← → ${wp.to}${wp.resp ? ' | ' + wp.resp : ''}</div>  
        </div>  
        ${daysLabel ? `<span class="wp-days ${daysClass}">${daysLabel}</span>` : ''}  
      </div>`;  
    }).join('');  
    html += `<div class="info-card"><div class="card-section-label">تصاريح الأعمال (${r.workPermits.length})</div>${rows}</div>`;  
  }  
  
  html += '</div>';  
  const el = document.getElementById('results');  
  el.innerHTML = html;  
  el.classList.remove('hidden');  
}  
  
function showNotFound(q) {  
  const el = document.getElementById('results');  
  el.innerHTML = `<div class="state-card not-found">  
    <div class="state-icon">🚫</div>  
    <div class="state-title">وحدة غير موجودة</div>  
    <div class="state-sub">لا توجد بيانات مسجلة للوحدة: <strong>${q}</strong></div>  
  </div>`;  
  el.classList.remove('hidden');  
}  
  
document.addEventListener('click', e => { if (!e.target.closest('.search-input-wrap')) hideSugs(); });  
  
// ============================================================  
//  INIT + AUTO-REFRESH every 5 min  
// ============================================================  
loadAllData();  
setInterval(loadAllData, 5 * 60 * 1000);  
</script>  
  
</body>  
</html>  
