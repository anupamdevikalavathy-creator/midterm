:root{  
  --bg: #f7fafc;  
  --card: #ffffff;  
  --muted: #64748b;  
  --pastel-calm: #dff6f0;  
  --pastel-positive: #fff3db;  
  --pastel-inspiring: #e9e7ff;  
  --shadow: 0 8px 20px rgba(12,18,30,0.06);  
  --radius: 14px;  
  --accent: #7fbfff;  
}  
  
/* global */  
*{box-sizing:border-box}  
body{ margin:0; font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial; background:var(--bg); color:#0f172a; -webkit-font-smoothing:antialiased; }  
a { color:var(--accent); text-decoration:none; }  
  
/* top nav */  
.top-nav{ display:flex; justify-content:space-between; align-items:center; padding:10px 18px; background:#fff; border-bottom:1px solid #eee; position:sticky; top:0; z-index:40 }  
.nav-btn{ background:transparent; border:none; padding:8px 12px; border-radius:8px; cursor:pointer; font-weight:700; color:#0b1530 }  
.nav-btn.active{ background:linear-gradient(90deg,#e8f6ff,#f0fbff); box-shadow:0 6px 18px rgba(127,191,255,0.06) }  
  
/* layout */  
.container{ max-width:1100px; margin:20px auto; display:flex; gap:20px; padding:0 16px; align-items:flex-start; position:relative; }  
.main-col{ flex:1 1 640px; min-width:320px; }  
.sidebar{ width:320px; flex:0 0 320px; }  
.header{ display:flex; justify-content:space-between; align-items:center; margin-bottom:12px }  
.brand{ font-weight:800; font-size:20px; color:#0b1530 }  
.small-note{ font-size:13px; color:var(--muted) }  
  
/* stories */  
.stories-row{ display:flex; gap:12px; overflow:auto; padding:10px 4px 16px 4px; margin-bottom:10px }  
.story{ width:76px; text-align:center; font-size:13px; color:var(--muted) }  
.story img{ width:76px; height:76px; border-radius:50%; object-fit:cover; border:4px solid #fff; box-shadow:var(--shadow) }  
.st-name{ margin-top:6px }  
  
/* feed grid */  
.feed-grid{ display:grid; grid-template-columns: repeat(3, 1fr); gap:8px; }  
  
/* post card */  
.post{ position:relative; border-radius:12px; overflow:hidden; background:linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.8)); box-shadow:var(--shadow); min-height:160px; display:flex; flex-direction:column; transition:all .22s }  
.media{ width:100%; height:160px; object-fit:cover; display:block; }  
  
/* overlays & tint */  
.overlay{ position:absolute; inset:0; pointer-events:none; }  
.overlay-tint{ position:absolute; inset:0; mix-blend-mode:normal; transition:all .28s; pointer-events:none; }  
.post[data-tone="calm"] .overlay-tint{ background: linear-gradient(180deg, rgba(223,246,240,0.45), rgba(223,246,240,0.28)); }  
.post[data-tone="positive"] .overlay-tint{ background: linear-gradient(180deg, rgba(255,243,219,0.45), rgba(255,243,219,0.28)); }  
.post[data-tone="inspiring"] .overlay-tint{ background: linear-gradient(180deg, rgba(233,231,255,0.45), rgba(233,231,255,0.28)); }  
.post[data-tone="neutral"] .overlay-tint{ background: transparent; }  
  
/* blur layer + reveal button */  
.blur-layer{ position:absolute; inset:0; display:flex; align-items:center; justify-content:center; transition:backdrop-filter .28s, background .28s; }  
.blurred .media{ filter:blur(6px) grayscale(.15); transform:scale(1.02); transition:filter .28s, transform .28s; }  
.reveal-btn{ position:absolute; left:50%; top:50%; transform:translate(-50%,-50%); background:rgba(255,255,255,0.95); padding:8px 12px; border-radius:999px; font-weight:700; cursor:pointer; border:none; box-shadow:0 6px 20px rgba(8,18,40,0.08) }  
  
/* meta */  
.meta{ padding:8px 10px; display:flex; gap:8px; align-items:center; justify-content:space-between; }  
.title{ font-weight:700; font-size:13px; color:#08102a }  
.meta-sub{ font-size:12px; color:var(--muted) }  
.badge{ font-size:11px; padding:6px 8px; border-radius:999px; background:rgba(12,18,30,0.05); color:#072029 }  
  
/* sidebar card */  
.card{ background:var(--card); border-radius:var(--radius); padding:16px; box-shadow:var(--shadow) }  
.controls-card h3{ margin:0 0 10px 0; font-size:16px }  
.tone-pills{ display:flex; gap:8px; margin-bottom:10px }  
.pill{ padding:8px 12px; border-radius:999px; background:#f1f5f9; border:none; cursor:pointer; font-weight:600; color:#0b1530; transition:transform .15s, box-shadow .15s }  
.pill.active{ box-shadow:0 8px 20px rgba(127,191,255,0.18); transform:translateY(-2px) ; background:var(--pastel-calm) }  
  
/* switch */  
.switch{ display:inline-block; width:46px; height:28px; position:relative }  
.switch input{ display:none }  
.switch-knob{ position:absolute; inset:0; border-radius:999px; background:#eee }  
.switch-knob:after{ content:""; position:absolute; left:4px; top:4px; width:20px; height:20px; background:#fff; border-radius:50%; transition:transform .18s }  
.switch input:checked + .switch-knob{ background: linear-gradient(90deg,var(--accent), #9bd7ff) }  
.switch input:checked + .switch-knob:after{ transform: translateX(18px) }  
  
/* footer */  
.footer{ margin-top:16px; display:flex; justify-content:space-between; align-items:center; color:var(--muted); font-size:13px }  
  
/* dashboard full page */  
.dashboard-page{ position:fixed; inset:0; background:linear-gradient(180deg,#fbfdff,#f7fbfa); display:flex; align-items:flex-start; justify-content:center; padding:48px; z-index:80; overflow:auto }  
.dashboard-page .dash-wrap{ max-width:980px; width:100% }  
.dash-header{ display:flex; justify-content:space-between; align-items:center; margin-bottom:16px }  
.dash-grid{ display:grid; grid-template-columns: 1fr 320px; gap:12px }  
.score-card{ display:flex; flex-direction:column; align-items:center; padding:18px }  
.circular{ width:120px; height:120px }  
.circular .bg{ fill:none; stroke:#111827; stroke-width:3.8 }  
.circular .arc{ fill:none; stroke:#7afcff; stroke-width:3.8; stroke-linecap:round; transform:rotate(-90deg); transform-origin:center; stroke-dasharray: 0 100 }  
#scoreText{ font-size:20px; fill:#0b1530; text-anchor:middle; font-weight:700 }  
.prefs{ padding:12px }  
.trans-controls{ display:flex; gap:8px; margin-top:8px }  
.primary{ background:linear-gradient(90deg,#7fbfff,#9bd7ff); color:#032; border:none; padding:10px 14px; border-radius:8px; cursor:pointer }  
  
/* hidden class */  
.hidden{ display:none !important }  
  
/* responsiveness */  
@media (max-width:980px){  
  .container{ padding:0 12px }  
  .sidebar{ display:none }  
  .feed-grid{ grid-template-columns: repeat(2, 1fr) }  
}  
@media (max-width:560px){  
  .feed-grid{ grid-template-columns: repeat(1, 1fr) }  
  .dash-grid{ grid-template-columns: 1fr }  
  .dashboard-page{ padding:18px }  
}  
