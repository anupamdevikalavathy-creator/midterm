// Combined prototype logic (client-only).  
// - Feed + Dashboard (full page) switching  
// - Emotional Tone controls (calm / positive / inspiring / neutral)  
// - Calm Mode (softens visuals, de-emphasizes certain posts)  
// - EHM Toggle (global on/off) from old prototype  
// - Auto-blur toxic posts + tap-to-reveal  
// - Posts have simulated emotional tags, weight, compare flag  
// - Dashboard shows Digital Wellness Score & inspector  
  
/* ---------- Data ---------- */  
const posts = [  
  { id: 1, img: 'https://picsum.photos/600?image=1011', author: 'mindful_creator', time: '2h', tone: 'calm', toxic: false, weight: 10, compare: false, auth: 92 },  
  { id: 2, img: 'https://picsum.photos/600?image=1025', author: 'viral_hype', time: '5h', tone: 'inspiring', toxic: true, weight: 30, compare: true, auth: 48 },  
  { id: 3, img: 'https://picsum.photos/600?image=1035', author: 'studygram', time: '1d', tone: 'positive', toxic: false, weight: 8, compare: false, auth: 88 },  
  { id: 4, img: 'https://picsum.photos/600?image=1052', author: 'trendwatch', time: '3d', tone: 'neutral', toxic: false, weight: 20, compare: true, auth: 76 },  
  { id: 5, img: 'https://picsum.photos/600?image=1060', author: 'calmcorner', time: '6h', tone: 'calm', toxic: false, weight: 6, compare: false, auth: 95 },  
  { id: 6, img: 'https://picsum.photos/600?image=1074', author: 'hotdebate', time: '2h', tone: 'inspiring', toxic: true, weight: 40, compare: true, auth: 35 }  
];  
  
/* ---------- State ---------- */  
let state = {  
  tone: 'calm',  
  calmMode: true,  
  filterToxic: true,  
  filterCompare: true,  
  ehmOn: true,  
  score: 85  
};  
  
/* ---------- DOM refs ---------- */  
const feedEl = document.getElementById('feed');  
const pills = document.querySelectorAll('.pill');  
const calmModeCheckbox = document.getElementById('calmMode');  
const filterToxicCheckbox = document.getElementById('filterToxic');  
const filterCompareCheckbox = document.getElementById('filterCompare');  
const previewTone = document.getElementById('previewTone');  
const prefCompare = document.getElementById('prefCompare');  
const prefLearn = document.getElementById('prefLearn');  
const prefPolar = document.getElementById('prefPolar');  
  
const viewFeedBtn = document.getElementById('viewFeed');  
const viewDashBtn = document.getElementById('viewDash');  
const feedView = document.getElementById('feedView');  
const dashboardView = document.getElementById('dashboardView');  
const ehmToggle = document.getElementById('ehmToggle');  
  
const scoreText = document.getElementById('scoreText');  
const arc = document.getElementById('arc');  
const scoreMsg = document.getElementById('scoreMsg');  
const whyPost = document.getElementById('whyPost');  
const metaPanel = document.getElementById('metaPanel');  
  
/* ---------- Helpers ---------- */  
function el(tag, attrs = {}, children = []) {  
  const e = document.createElement(tag);  
  for (let k in attrs) {  
    if (k === 'class') e.className = attrs[k];  
    else if (k === 'html') e.innerHTML = attrs[k];  
    else e.setAttribute(k, attrs[k]);  
  }  
  children.forEach(c => e.appendChild(c));  
  return e;  
}  
function cap(s){ return s.charAt(0).toUpperCase() + s.slice(1); }  
function renderArc(percent){  
  if(!arc) return;  
  const circumference = 2 * Math.PI * 15;  
  const filled = (percent/100) * circumference;  
  arc.style.strokeDasharray = filled + ' ' + (circumference - filled);  
}  
  
/* ---------- Render Feed ---------- */  
function renderFeed(){  
  feedEl.innerHTML = '';  
  // sort: prefer lower weight and posts matching tone  
  const list = posts.slice().sort((a,b) => {  
    let scoreA = a.weight + (a.tone === state.tone ? -8 : 0);  
    let scoreB = b.weight + (b.tone === state.tone ? -8 : 0);  
    return scoreA - scoreB;  
  });  
  
  list.forEach(p => {  
    // decide blur / de-emphasis  
    const shouldBlur = state.filterToxic && p.toxic && state.ehmOn;  
    const hideForCompare = state.filterCompare && p.compare && state.calmMode && state.ehmOn;  
  
    const card = el('article', { class: 'post', 'data-tone': p.tone });  
    const img = el('img', { class: 'media', src: p.img, alt: p.author + ' post' });  
  
    // overlay and tint  
    const overlay = el('div', { class: 'overlay' });  
    const tint = el('div', { class: 'overlay-tint' });  
    overlay.appendChild(tint);  
  
    // blur layer & reveal  
    const blurLayer = el('div', { class: 'blur-layer' });  
    if (shouldBlur){  
      card.classList.add('blurred');  
      const reveal = el('button', { class: 'reveal-btn', type: 'button', html: 'Tap to reveal' });  
      reveal.addEventListener('click', (ev) => {  
        ev.stopPropagation();  
        if (card.classList.contains('blurred')) {  
          card.classList.remove('blurred');  
          reveal.textContent = 'Hidden (tap to hide)';  
        } else {  
          card.classList.add('blurred');  
          reveal.textContent = 'Tap to reveal';  
        }  
      });  
      blurLayer.appendChild(reveal);  
    }  
  
    // meta row  
    const meta = el('div', { class: 'meta' });  
    const left = el('div', {});  
    left.appendChild(el('div', { class: 'title', html: p.author }));  
    left.appendChild(el('div', { class: 'meta-sub', html: p.time }));  
    const right = el('div', {});  
    const badge = el('div', { class: 'badge', html: cap(p.tone) });  
    right.appendChild(badge);  
    if (p.toxic) right.appendChild(el('div', { class: 'info', html: '⚠️' }));  
    if (p.compare) right.appendChild(el('div', { class: 'info', html: '⇅' }));  
    meta.appendChild(left);  
    meta.appendChild(right);  
  
    // calmMode visual tweaks  
    if (state.calmMode && state.ehmOn){  
      if (p.weight > 25 || p.compare) {  
        card.style.opacity = 0.7;  
        card.style.filter = 'saturate(.88) contrast(.96)';  
      } else {  
        card.style.opacity = 1;  
        card.style.filter = '';  
      }  
    } else {  
      card.style.opacity = 1;  
      card.style.filter = '';  
    }  
  
    // hide for compare heavy  
    if (hideForCompare){  
      card.style.opacity = 0.36;  
      card.style.filter = 'grayscale(.6) blur(.6px)';  
      card.dataset.deemphasized = 'true';  
    } else {  
      card.dataset.deemphasized = 'false';  
    }  
  
    card.appendChild(img);  
    card.appendChild(overlay);  
    if (shouldBlur) card.appendChild(blurLayer);  
    card.appendChild(meta);  
  
    // click to inspect in sidebar preview  
    card.addEventListener('click', () => {  
      showPreviewForPost(p);  
    });  
  
    feedEl.appendChild(card);  
  });  
  
  applyToneVisuals();  
}  
  
/* ---------- Tone visuals ---------- */  
function applyToneVisuals(){  
  previewTone.textContent = 'Tone: ' + cap(state.tone);  
  // background per tone  
  if (state.tone === 'calm') document.body.style.background = '#f7fbfa';  
  else if (state.tone === 'positive') document.body.style.background = '#fffaf6';  
  else if (state.tone === 'inspiring') document.body.style.background = '#fbfbff';  
  else document.body.style.background = '#f7fafc';  
  
  // pill states  
  pills.forEach(b => b.classList.toggle('active', b.dataset.tone === state.tone));  
  
  // highlight posts that match tone  
  document.querySelectorAll('.post').forEach(card => {  
    if (card.getAttribute('data-tone') === state.tone) {  
      card.style.boxShadow = '0 8px 30px rgba(127,191,255,0.12)';  
      card.style.transform = 'translateY(-2px)';  
    } else {  
      card.style.boxShadow = '';  
      card.style.transform = '';  
    }  
  });  
}  
  
/* ---------- Preview inspector ---------- */  
function showPreviewForPost(p){  
  const preview = document.getElementById('previewTone');  
  preview.innerHTML = `  
    <strong>${p.author}</strong>  
    <div style="font-size:13px;color:#556">${p.time} • Tone: ${cap(p.tone)}</div>  
    <div style="margin-top:8px;font-size:13px;color:#334">Authenticity: ${p.auth ? '<strong style="color:#2a8">High</strong>' : '<strong style="color:#c44">Low</strong>'}</div>  
    <div style="margin-top:6px;font-size:13px;color:#556">Weight: ${p.weight} • Compare: ${p.compare ? 'Yes' : 'No'}</div>  
  `;  
}  
  
/* ---------- Dashboard helpers ---------- */  
function updateScore(delta){  
  state.score = Math.max(30, Math.min(98, state.score + delta));  
  if (scoreText) scoreText.textContent = state.score;  
  renderArc(state.score);  
  if(scoreMsg){  
    if(state.score >= 80) scoreMsg.textContent = 'Great job staying mindful!';  
    else if(state.score >= 60) scoreMsg.textContent = 'Some balance needed — try filters.';  
    else scoreMsg.textContent = 'Consider taking a break and adjusting preferences.';  
  }  
}  
  
/* ---------- Event bindings ---------- */  
// tone pills  
pills.forEach(b => {  
  b.addEventListener('click', () => {  
    state.tone = b.dataset.tone;  
    applyToneVisuals();  
    renderFeed();  
  });  
});  
  
// calm mode + filters + EHM toggle  
calmModeCheckbox.addEventListener('change', (e) => {  
  state.calmMode = e.target.checked;  
  renderFeed();  
});  
filterToxicCheckbox.addEventListener('change', (e) => {  
  state.filterToxic = e.target.checked;  
  renderFeed();  
});  
filterCompareCheckbox.addEventListener('change', (e) => {  
  state.filterCompare = e.target.checked;  
  renderFeed();  
});  
ehmToggle.addEventListener('change', (e) => {  
  state.ehmOn = e.target.checked;  
  // toggling EHM nudges score mildly  
  updateScore(state.ehmOn ? 6 : -8);  
  renderFeed();  
});  
  
// view switching (Feed <-> Dashboard)  
viewFeedBtn.addEventListener('click', () => {  
  viewFeedBtn.classList.add('active');  
  viewDashBtn.classList.remove('active');  
  document.getElementById('feedView').classList.remove('hidden');  
  document.getElementById('controlsPanel').classList.remove('hidden');  
  document.getElementById('dashboardView').classList.add('hidden');  
});  
viewDashBtn.addEventListener('click', () => {  
  viewFeedBtn.classList.remove('active');  
  viewDashBtn.classList.add('active');  
  document.getElementById('feedView').classList.add('hidden');  
  document.getElementById('controlsPanel').classList.add('hidden');  
  document.getElementById('dashboardView').classList.remove('hidden');  
});  
  
// dashboard buttons  
document.getElementById('boostLearning').addEventListener('click', () => { updateScore(3); prefLearn.checked = true; });  
document.getElementById('reduceCompare').addEventListener('click', () => { updateScore(3); prefCompare.checked = true; });  
  
// inspector explain  
document.getElementById('inspectBoost').addEventListener('click', () => {  
  whyPost.innerHTML = '<strong>Why posts appear:</strong><ul><li>Followed creators</li><li>Engagement signals</li><li>Your tone preference</li></ul>';  
});  
  
// back to feed button  
document.getElementById('backToFeed').addEventListener('click', () => {  
  viewFeedBtn.click();  
});  
  
// initial render  
renderFeed();  
updateScore(0);  
applyToneVisuals();  
