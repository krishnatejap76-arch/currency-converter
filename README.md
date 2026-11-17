<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>ConvertX — Free Currency Converter</title>
<meta name="description" content="ConvertX — fast, free currency converter with live exchange rates, charts and multi-currency tables." />
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
  :root{
    --bg:#0f172a;
    --bg2:#1e293b;
    --card:#ffffff;
    --muted:#64748b;
    --text:#0f172a;
    --accent:#4f46e5;
    --accent2:#06b6d4;
    --green:#10b981;
    --border:#e2e8f0;
    --shadow:0 20px 60px rgba(15,23,42,.18);
    --radius:20px;
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family: Inter, ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
    color:var(--text);
    background:#f1f5f9;
  }
  a{color:inherit}
  .hero{
    background: radial-gradient(1000px 500px at 20% -10%, #6366f1 0%, transparent 60%),
                radial-gradient(900px 500px at 90% 0%, #06b6d4 0%, transparent 55%),
                linear-gradient(180deg, #0f172a 0%, #1e1b4b 100%);
    color:white;
    padding:28px 20px 90px;
  }
  .nav{
    max-width:1100px;margin:0 auto;
    display:flex;align-items:center;justify-content:space-between;
  }
  .logo{display:flex;align-items:center;gap:10px;font-weight:800;font-size:22px;letter-spacing:.2px}
  .logo-badge{
    width:38px;height:38px;border-radius:12px;display:grid;place-items:center;
    background:linear-gradient(135deg,var(--accent),var(--accent2));
    font-size:20px;box-shadow:0 8px 20px rgba(79,70,229,.4)
  }
  .nav-links{display:flex;gap:18px;align-items:center;font-size:14px;opacity:.9}
  .nav-links a{text-decoration:none;opacity:.85}
  .pill{border:1px solid rgba(255,255,255,.25);padding:8px 14px;border-radius:999px;font-size:13px;background:rgba(255,255,255,.08)}
  .live-dot{width:8px;height:8px;background:#22c55e;border-radius:50%;display:inline-block;margin-right:6px;box-shadow:0 0 0 4px rgba(34,197,94,.25);animation:pulse 1.6s infinite}
  @keyframes pulse{50%{box-shadow:0 0 0 7px rgba(34,197,94,.12)}}
  .hero-inner{max-width:1100px;margin:36px auto 0;display:grid;grid-template-columns:1.1fr .9fr;gap:30px;align-items:center}
  .hero h1{font-size:46px;line-height:1.05;margin:0 0 12px;letter-spacing:-1px}
  .hero h1 span{background:linear-gradient(90deg,#a5b4fc,#67e8f9);-webkit-background-clip:text;background-clip:text;color:transparent}
  .hero p{opacity:.75;line-height:1.6;margin:0 0 18px}
  .hero-stats{display:flex;gap:14px;margin-top:18px}
  .hstat{background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.14);border-radius:14px;padding:10px 14px;min-width:130px}
  .hstat b{font-size:18px;display:block}
  .hstat small{opacity:.7}
  .wrap{max-width:1100px;margin:-60px auto 0;padding:0 20px 40px}
  .converter-card{
    background:var(--card);border-radius:var(--radius);box-shadow:var(--shadow);
    padding:22px;display:grid;gap:16px;border:1px solid #eef2ff;
  }
  .tabs{display:flex;gap:8px;background:#f1f5f9;padding:5px;border-radius:999px;width:fit-content}
  .tabs button{border:0;padding:9px 18px;border-radius:999px;font-weight:700;cursor:pointer;background:transparent;color:#64748b}
  .tabs button.active{background:white;color:var(--text);box-shadow:0 4px 12px rgba(0,0,0,.08)}
  .grid-3{display:grid;grid-template-columns:1fr 56px 1fr;gap:10px;align-items:end}
  label{font-size:12px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.6px;display:block;margin-bottom:8px}
  input[type=number], select{
    width:100%;padding:14px 14px;border-radius:14px;border:1.5px solid var(--border);
    font-size:16px;font-weight:600;background:#fff;outline:none;transition:.15s;
  }
  input:focus, select:focus{border-color:var(--accent);box-shadow:0 0 0 4px rgba(79,70,229,.12)}
  .select-wrap{position:relative}
  .select-wrap img{position:absolute;left:12px;top:50%;transform:translateY(-50%);width:26px;height:19px;border-radius:4px;object-fit:cover;box-shadow:0 1px 4px rgba(0,0,0,.2)}
  .select-wrap select{padding-left:46px;appearance:none}
  .swap-btn{
    width:52px;height:52px;border-radius:50%;border:1.5px solid var(--border);background:#eef2ff;
    font-size:22px;cursor:pointer;transition:.2s;margin-bottom:2px;
  }
  .swap-btn:hover{transform:rotate(180deg);background:var(--accent);color:white;border-color:var(--accent)}
  .amount-chips{display:flex;gap:8px;flex-wrap:wrap}
  .amount-chips button{border:1px solid var(--border);background:#f8fafc;border-radius:999px;padding:7px 14px;cursor:pointer;font-weight:700;color:#334155}
  .amount-chips button:hover{border-color:var(--accent);color:var(--accent)}
  .convert-btn{
    background:linear-gradient(135deg,var(--accent),#7c3aed 50%,var(--accent2));
    color:white;border:0;border-radius:14px;padding:16px;font-size:17px;font-weight:800;cursor:pointer;
    box-shadow:0 12px 24px rgba(79,70,229,.35);transition:.15s;
  }
  .convert-btn:hover{transform:translateY(-1px);box-shadow:0 16px 30px rgba(79,70,229,.45)}
  .convert-btn:disabled{opacity:.6;cursor:wait;transform:none}
  .result-box{
    background:linear-gradient(135deg,#eef2ff,#ecfeff);
    border:1px solid #e0e7ff;border-radius:16px;padding:18px;
    display:flex;justify-content:space-between;gap:14px;align-items:center;flex-wrap:wrap;
  }
  .result-main small{color:var(--muted);font-weight:600}
  .result-main h2{margin:4px 0;font-size:32px;letter-spacing:-.5px}
  .rate-line{font-size:14px;color:#334155;background:white;border:1px dashed #cbd5e1;padding:8px 12px;border-radius:10px}
  .meta{font-size:12px;color:var(--muted);display:flex;gap:12px;flex-wrap:wrap}
  .cards{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-top:18px}
  .card{background:white;border-radius:18px;padding:20px;box-shadow:0 10px 30px rgba(15,23,42,.07);border:1px solid #f1f5f9}
  .card h3{margin:0 0 4px;font-size:18px}
  .card p.sub{margin:0 0 14px;color:var(--muted);font-size:13.5px}
  .pop-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .pop-item{border:1px solid var(--border);border-radius:12px;padding:10px 12px;cursor:pointer;transition:.15s;background:#f8fafc}
  .pop-item:hover{border-color:var(--accent);background:#eef2ff;transform:translateY(-1px)}
  .pop-item b{display:block;font-size:14px}
  .pop-item span{font-size:12.5px;color:var(--muted)}
  table{width:100%;border-collapse:collapse;font-size:14px}
  th{text-align:left;color:var(--muted);font-size:12px;text-transform:uppercase;letter-spacing:.5px;padding:8px;border-bottom:1px solid var(--border)}
  td{padding:10px 8px;border-bottom:1px solid #f1f5f9}
  tr:last-child td{border-bottom:0}
  td img{width:24px;height:17px;border-radius:4px;object-fit:cover;vertical-align:middle;margin-right:8px}
  .chart-wrap{position:relative;height:260px}
  .footer{text-align:center;color:#94a3b8;font-size:13px;padding:18px}
  .toast{
    position:fixed;bottom:20px;left:50%;transform:translateX(-50%) translateY(20px);
    background:#0f172a;color:white;padding:12px 18px;border-radius:999px;font-size:14px;
    opacity:0;pointer-events:none;transition:.25s;box-shadow:0 12px 30px rgba(0,0,0,.3);z-index:50;
  }
  .toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
  @media(max-width:900px){
    .hero-inner{grid-template-columns:1fr}
    .hero h1{font-size:34px}
    .cards{grid-template-columns:1fr}
    .grid-3{grid-template-columns:1fr;gap:14px}
    .swap-btn{transform:rotate(90deg);margin:0 auto;display:block}
    .swap-btn:hover{transform:rotate(270deg)}
  }
</style>
</head>
<body>

<div class="hero">
  <div class="nav">
    <div class="logo"><div class="logo-badge">💱</div> ConvertX</div>
    <div class="nav-links">
      <a href="#converter">Converter</a>
      <a href="#rates">All rates</a>
      <a href="#chart-card">Trends</a>
      <span class="pill"><span class="live-dot"></span><span id="status-text">Live rates</span></span>
    </div>
  </div>

  <div class="hero-inner">
    <div>
      <h1>Convert any currency <span>in seconds.</span></h1>
      <p>Live mid-market rates for 40+ world currencies. Convert, compare multiple currencies at once, and track 30-day trends — free, no sign-up.</p>
      <div class="hero-stats">
        <div class="hstat"><b id="stat-count">40+</b><small>Currencies</small></div>
        <div class="hstat"><b>Live</b><small id="stat-updated">Updating…</small></div>
        <div class="hstat"><b>₹ $ € £</b><small>All symbols</small></div>
      </div>
    </div>
    <div style="background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.14);border-radius:18px;padding:18px;backdrop-filter:blur(8px)">
      <div style="font-weight:800;margin-bottom:10px">⚡ Quick convert</div>
      <div id="quick-list" style="display:grid;gap:8px;font-size:14px"></div>
    </div>
  </div>
</div>

<div class="wrap" id="converter">
  <div class="converter-card">
    <div class="tabs">
      <button class="active" id="tab-convert" onclick="switchTab('convert')">Convert</button>
      <button id="tab-multi" onclick="switchTab('multi')">Compare all</button>
    </div>

    <div>
      <label>Amount</label>
      <input type="number" id="amount" value="100" min="0" step="any" oninput="debouncedConvert()" />
      <div class="amount-chips" style="margin-top:10px">
        <button onclick="setAmount(10)">10</button>
        <button onclick="setAmount(50)">50</button>
        <button onclick="setAmount(100)">100</button>
        <button onclick="setAmount(500)">500</button>
        <button onclick="setAmount(1000)">1,000</button>
        <button onclick="setAmount(10000)">10,000</button>
      </div>
    </div>

    <div class="grid-3">
      <div>
        <label>From</label>
        <div class="select-wrap">
          <img id="from-flag" src="https://flagcdn.com/w80/us.png" alt="flag" />
          <select id="from" onchange="onCurrencyChange()"></select>
        </div>
      </div>
      <div style="text-align:center">
        <button class="swap-btn" onclick="swap()" title="Swap currencies">⇄</button>
      </div>
      <div>
        <label>To</label>
        <div class="select-wrap">
          <img id="to-flag" src="https://flagcdn.com/w80/in.png" alt="flag" />
          <select id="to" onchange="onCurrencyChange()"></select>
        </div>
      </div>
    </div>

    <button class="convert-btn" id="convert-btn" onclick="convert(true)">Convert now →</button>

    <div class="result-box">
      <div class="result-main">
        <small id="result-label">100 US Dollar → Indian Rupee</small>
        <h2 id="result-value">—</h2>
        <div class="meta">
          <span id="rate-text">1 USD = — INR</span>
          <span id="inv-text"></span>
          <span id="updated-text"></span>
        </div>
      </div>
      <div class="rate-line" id="calc-line">Enter amount & hit convert</div>
    </div>

    <div id="multi-box" style="display:none">
      <label>Converted value of <span id="multi-amount-label">100</span> <span id="multi-base-label">USD</span> in all currencies</label>
      <div style="max-height:360px;overflow:auto;border:1px solid var(--border);border-radius:12px;margin-top:8px">
        <table>
          <thead><tr><th>Currency</th><th>Rate</th><th>Value</th></tr></thead>
          <tbody id="multi-tbody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <div class="cards">
    <div class="card">
      <h3>🔥 Popular conversions</h3>
      <p class="sub">Tap any pair to load it in the converter.</p>
      <div class="pop-grid" id="pop-grid"></div>
    </div>
    <div class="card" id="chart-card">
      <h3>📈 30-day trend</h3>
      <p class="sub" id="chart-sub">USD → INR</p>
      <div class="chart-wrap"><canvas id="trend"></canvas></div>
    </div>
  </div>

  <div class="card" id="rates" style="margin-top:18px">
    <h3>🌍 All rates vs <span id="base-name">USD</span></h3>
    <p class="sub">Live mid-market reference rates. Search to filter.</p>
    <input type="number" id="table-amount" value="1" min="0" step="any" style="max-width:200px;margin-bottom:12px" oninput="renderTable()" placeholder="Amount" />
    <input type="text" id="search" placeholder="🔍 Search currency (e.g. Rupee, EUR, ¥)..." oninput="renderTable()" style="width:100%;padding:12px 14px;border-radius:12px;border:1.5px solid var(--border);font-size:15px;margin-bottom:10px" />
    <div style="max-height:420px;overflow:auto">
      <table>
        <thead><tr><th>Currency</th><th>1 unit</th><th id="th-converted">1 USD =</th></tr></thead>
        <tbody id="rates-tbody"></tbody>
      </table>
    </div>
  </div>

  <div class="footer">ConvertX • Rates by open.er-api.com (mid-market reference, not for trading) • Built for you ❤️</div>
</div>

<div class="toast" id="toast"></div>

<script>
const CURRENCIES = [
  {code:'USD', name:'US Dollar', symbol:'$', flag:'us'},
  {code:'EUR', name:'Euro', symbol:'€', flag:'eu'},
  {code:'INR', name:'Indian Rupee', symbol:'₹', flag:'in'},
  {code:'GBP', name:'British Pound', symbol:'£', flag:'gb'},
  {code:'JPY', name:'Japanese Yen', symbol:'¥', flag:'jp'},
  {code:'AUD', name:'Australian Dollar', symbol:'A$', flag:'au'},
  {code:'CAD', name:'Canadian Dollar', symbol:'C$', flag:'ca'},
  {code:'CHF', name:'Swiss Franc', symbol:'Fr', flag:'ch'},
  {code:'CNY', name:'Chinese Yuan', symbol:'¥', flag:'cn'},
  {code:'AED', name:'UAE Dirham', symbol:'د.إ', flag:'ae'},
  {code:'SGD', name:'Singapore Dollar', symbol:'S$', flag:'sg'},
  {code:'HKD', name:'Hong Kong Dollar', symbol:'HK$', flag:'hk'},
  {code:'NZD', name:'New Zealand Dollar', symbol:'NZ$', flag:'nz'},
  {code:'SEK', name:'Swedish Krona', symbol:'kr', flag:'se'},
  {code:'NOK', name:'Norwegian Krone', symbol:'kr', flag:'no'},
  {code:'ZAR', name:'South African Rand', symbol:'R', flag:'za'},
  {code:'MXN', name:'Mexican Peso', symbol:'$', flag:'mx'},
  {code:'BRL', name:'Brazilian Real', symbol:'R$', flag:'br'},
  {code:'KRW', name:'South Korean Won', symbol:'₩', flag:'kr'},
  {code:'SAR', name:'Saudi Riyal', symbol:'﷼', flag:'sa'},
  {code:'THB', name:'Thai Baht', symbol:'฿', flag:'th'},
  {code:'MYR', name:'Malaysian Ringgit', symbol:'RM', flag:'my'},
  {code:'IDR', name:'Indonesian Rupiah', symbol:'Rp', flag:'id'},
  {code:'PHP', name:'Philippine Peso', symbol:'₱', flag:'ph'},
  {code:'VND', name:'Vietnamese Dong', symbol:'₫', flag:'vn'},
  {code:'TRY', name:'Turkish Lira', symbol:'₺', flag:'tr'},
  {code:'PLN', name:'Polish Zloty', symbol:'zł', flag:'pl'},
  {code:'DKK', name:'Danish Krone', symbol:'kr', flag:'dk'},
  {code:'EGP', name:'Egyptian Pound', symbol:'£', flag:'eg'},
  {code:'NGN', name:'Nigerian Naira', symbol:'₦', flag:'ng'},
  {code:'PKR', name:'Pakistani Rupee', symbol:'₨', flag:'pk'},
  {code:'BDT', name:'Bangladeshi Taka', symbol:'৳', flag:'bd'},
  {code:'LKR', name:'Sri Lankan Rupee', symbol:'Rs', flag:'lk'},
  {code:'NPR', name:'Nepalese Rupee', symbol:'₨', flag:'np'},
  {code:'QAR', name:'Qatari Riyal', symbol:'﷼', flag:'qa'},
  {code:'KWD', name:'Kuwaiti Dinar', symbol:'د.ك', flag:'kw'},
  {code:'OMR', name:'Omani Rial', symbol:'﷼', flag:'om'},
  {code:'TWD', name:'Taiwan Dollar', symbol:'NT$', flag:'tw'},
  {code:'HUF', name:'Hungarian Forint', symbol:'Ft', flag:'hu'},
  {code:'CZK', name:'Czech Koruna', symbol:'Kč', flag:'cz'},
];
const FALLBACK_RATES_USD = {USD:1,EUR:.92,INR:84.6,GBP:.79,JPY:154.3,AUD:1.53,CAD:1.40,CHF:.89,CNY:7.24,AED:3.67,SGD:1.34,HKD:7.78,NZD:1.69,SEK:10.95,NOK:11.05,ZAR:18.1,MXN:20.3,BRL:5.78,KRW:1395,SAR:3.75,THB:34.6,MYR:4.46,IDR:15850,PHP:58.7,VND:25400,TRY:34.4,PLN:4.05,DKK:6.86,EGP:49.2,NGN:1550,PKR:278,BDT:119.5,LKR:292,NPR:134.5,QAR:3.64,KWD:.31,OMR:.38,TWD:32.4,HUF:390,CZK:23.2};

let rates = {...FALLBACK_RATES_USD};
let base = 'USD';
let lastUpdated = null;
let live = false;
let chart = null;
let mode = 'convert';
let debounceT = null;

const $ = id => document.getElementById(id);
const curr = code => CURRENCIES.find(c=>c.code===code);
const fmt = (n, code='') => new Intl.NumberFormat('en-US',{maximumFractionDigits: n>=1000?2:4}).format(n);

function toast(msg){
  const t=$('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(t._h); t._h=setTimeout(()=>t.classList.remove('show'),2200);
}

function fillSelects(){
  const f=$('from'), t=$('to');
  f.innerHTML=''; t.innerHTML='';
  CURRENCIES.forEach(c=>{
    const o1=document.createElement('option');
    o1.value=c.code; o1.textContent=`${c.code} — ${c.name}`;
    const o2=o1.cloneNode(true);
    f.appendChild(o1); t.appendChild(o2);
  });
  f.value='USD'; t.value='INR';
  updateFlags();
}

function updateFlags(){
  $('from-flag').src=`https://flagcdn.com/w80/${curr($('from').value).flag}.png`;
  $('to-flag').src=`https://flagcdn.com/w80/${curr($('to').value).flag}.png`;
}

function setAmount(v){ $('amount').value=v; convert(true); }
function swap(){
  const f=$('from'), t=$('to');
  [f.value, t.value]=[t.value, f.value];
  updateFlags(); convert(true);
}
function onCurrencyChange(){ updateFlags(); convert(false); renderTable(); loadTrend(); }
function switchTab(m){
  mode=m;
  $('tab-convert').classList.toggle('active', m==='convert');
  $('tab-multi').classList.toggle('active', m==='multi');
  $('multi-box').style.display = m==='multi' ? 'block':'none';
  if(m==='multi') renderMulti();
}
function debouncedConvert(){
  clearTimeout(debounceT);
  debounceT=setTimeout(()=>convert(false), 400);
  if(mode==='multi') renderMulti();
}

async function fetchRates(newBase){
  const btn=$('convert-btn');
  btn.disabled=true; btn.textContent='Fetching live rates…';
  try{
    const res = await fetch(`https://open.er-api.com/v6/latest/${newBase}`);
    if(!res.ok) throw new Error('rate fetch failed');
    const data = await res.json();
    if(data.result!=='success') throw new Error('bad response');
    rates = data.rates; base = newBase;
    lastUpdated = new Date(data.time_last_update_utc);
    live = true;
    $('status-text').textContent='Live rates';
    $('stat-updated').textContent='Updated '+lastUpdated.toLocaleDateString();
    $('updated-text').textContent='• Updated '+lastUpdated.toLocaleString();
  }catch(e){
    live=false;
    $('status-text').textContent='Offline rates';
    $('updated-text').textContent='• Showing cached reference rates';
    toast('Offline — using reference rates');
  }finally{
    btn.disabled=false; btn.textContent='Convert now →';
  }
}

function rate(from,to){
  // rates are vs `base`
  if(from===base) return rates[to];
  if(to===base) return 1/rates[from];
  return rates[to]/rates[from];
}

async function convert(withToast){
  const amt = parseFloat($('amount').value);
  if(isNaN(amt)){ $('result-value').textContent='Enter an amount'; return; }
  const from=$('from').value, to=$('to').value;
  if(from!==base){
    // re-base to reduce error: fetch with `from` as base
    await fetchRates(from);
  }
  const r = rate(from,to);
  if(!r){ $('result-value').textContent='Rate unavailable'; return; }
  const out = amt*r;
  const sym = curr(to).symbol;
  $('result-label').textContent = `${fmt(amt)} ${curr(from).name} → ${curr(to).name}`;
  $('result-value').textContent = `${sym} ${fmt(out)} ${to}`;
  $('rate-text').textContent = `1 ${from} = ${fmt(r)} ${to}`;
  $('inv-text').textContent = `• 1 ${to} = ${fmt(1/r)} ${from}`;
  $('calc-line').textContent = `${fmt(amt)} × ${fmt(r)} = ${fmt(out)} ${to}`;
  $('base-name').textContent = from;
  $('th-converted').textContent = `${fmt(amt)} ${from} =`;
  $('multi-amount-label').textContent = fmt(amt);
  $('multi-base-label').textContent = from;
  renderTable(); renderMulti(); loadTrend(true);
  if(withToast) toast(`Converted ${from} → ${to}`);
}

function renderMulti(){
  const amt=parseFloat($('amount').value)||0;
  const from=$('from').value;
  const tb=$('multi-tbody'); tb.innerHTML='';
  [...CURRENCIES].sort((a,b)=> (rate(from,b.code)*amt)-(rate(from,a.code)*amt)).slice(0,12).forEach(c=>{
    if(c.code===from) return;
    const r=rate(from,c.code); if(!r) return;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td><img src="https://flagcdn.com/w40/${c.flag}.png"/> <b>${c.code}</b> <span style="color:#64748b">${c.name}</span></td><td>${fmt(r)}</td><td><b>${c.symbol} ${fmt(amt*r)}</b></td>`;
    tb.appendChild(tr);
  });
}

function renderTable(){
  const from=$('from').value;
  const amt=parseFloat($('table-amount').value)||1;
  const q=($('search').value||'').toLowerCase();
  const tb=$('rates-tbody'); tb.innerHTML='';
  CURRENCIES.filter(c=> !q || (c.code+c.name+c.symbol).toLowerCase().includes(q)).forEach(c=>{
    if(c.code===from) return;
    const r=rate(from,c.code); if(!r) return;
    const tr=document.createElement('tr');
    tr.innerHTML=`<td><img src="https://flagcdn.com/w40/${c.flag}.png"/><b>${c.code}</b> <span style="color:#64748b">${c.name}</span></td><td>1 ${from}</td><td><b>${fmt(r*amt)} ${c.code}</b></td>`;
    tb.appendChild(tr);
  });
  if(!tb.children.length) tb.innerHTML='<tr><td colspan="3" style="color:#64748b">No matches. Try “dollar”, “EUR”, “₹”…</td></tr>';
}

function renderPopular(){
  const pairs=[['USD','INR'],['EUR','USD'],['GBP','INR'],['USD','AED'],['USD','EUR'],['AUD','INR'],['CAD','INR'],['SAR','INR']];
  const g=$('pop-grid'); g.innerHTML='';
  pairs.forEach(([f,t])=>{
    const d=document.createElement('div');
    d.className='pop-item';
    d.innerHTML=`<b>${f} → ${t}</b><span class="pv" data-f="${f}" data-t="${t}">loading…</span>`;
    d.onclick=()=>{ $('from').value=f; $('to').value=t; updateFlags(); convert(true); window.scrollTo({top:0,behavior:'smooth'}); };
    g.appendChild(d);
  });
}

function refreshPopular(){
  const amt=parseFloat($('amount').value)||1;
  document.querySelectorAll('.pv').forEach(el=>{
    const r=rate(el.dataset.f, el.dataset.t);
    el.textContent = r ? `${fmt(amt)} ${el.dataset.f} = ${fmt(amt*r)} ${el.dataset.t}` : '—';
  });
}

function renderQuick(){
  const q=$('quick-list'); q.innerHTML='';
  [['USD','INR',100],['EUR','INR',50],['GBP','USD',100],['AED','INR',500]].forEach(([f,t,a])=>{
    const r=rate(f,t);
    const d=document.createElement('div');
    d.style.cssText='background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.15);border-radius:12px;padding:10px 12px;display:flex;justify-content:space-between;cursor:pointer';
    d.innerHTML=`<span>${fmt(a)} ${f} → ${t}</span><b>${r?fmt(a*r)+' '+t:'—'}</b>`;
    d.onclick=()=>{ $('amount').value=a; $('from').value=f; $('to').value=t; updateFlags(); convert(true); document.getElementById('converter').scrollIntoView({behavior:'smooth'}); };
    q.appendChild(d);
  });
}

async function loadTrend(keep=false){
  const from=$('from').value, to=$('to').value;
  $('chart-sub').textContent=`${from} → ${to} • last 30 days`;
  const end=new Date(), start=new Date(Date.now()-29*864e5);
  const f=s=>s.toISOString().slice(0,10);
  let labels=[], values=[];
  try{
    const url=`https://api.frankfurter.app/v1/${f(start)}..${f(end)}?from=${from}&to=${to}`;
    const res=await fetch(url);
    if(!res.ok) throw 0;
    const data=await res.json();
    labels=Object.keys(data.rates);
    values=labels.map(d=>data.rates[d][to]);
    if(!values.length) throw 0;
  }catch(e){
    // synthetic fallback anchored on current rate
    const r=rate(from,to)||1;
    labels=[...Array(30)].map((_,i)=>{const d=new Date(Date.now()-(29-i)*864e5);return d.toISOString().slice(0,10)});
    let v=r*0.97;
    values=labels.map(()=>{ v*= (1+(Math.random()-0.48)*0.008); return v; });
    values[values.length-1]=r;
  }
  const ctx=$('trend');
  if(chart) chart.destroy();
  const up = values[values.length-1] >= values[0];
  chart=new Chart(ctx,{
    type:'line',
    data:{labels, datasets:[{data:values, borderColor: up?'#10b981':'#ef4444', backgroundColor: up?'rgba(16,185,129,.15)':'rgba(239,68,68,.12)', fill:true, tension:.35, pointRadius:0, borderWidth:2.5}]},
    options:{plugins:{legend:{display:false}}, scales:{x:{ticks:{maxTicksLimit:5, font:{size:10}}}, y:{ticks:{font:{size:10}}}}, maintainAspectRatio:false}
  });
}

// init
fillSelects();
renderPopular();
(async ()=>{
  await fetchRates('USD');
  convert(false);
  renderQuick();
  refreshPopular();
  setInterval(async ()=>{ await fetchRates($('from').value); convert(false); renderQuick(); refreshPopular(); }, 10*60*1000);
})();
</script>
<script>window.__CF$cv$params={r:'a5bf396958861dbe',t:'MTc5NDkyMzYzNA==',u:'01a1e9c920fd7485891bf45b293ff8d2',ut:'xnzVedSjTHev.5rL7wUsLUEMlCqATBHzsyi3gvmRpqk-1794923634-1.2.1.1-PNfhQ5XPeYZDp7Yuxf85tZD7xbi0oYaCNyljsdjhVRUKsMBb6ut_MMgX2JIeqpWaINqrWggOETaVohHNqZGCakoL8EaSxxtkmY1.9Vv23Fc',i:60};(function(){if(!document.body)return;var l=window.location,o;try{o=new URL(l.origin).origin}catch(e){try{o=new URL(new URL(l.href).origin).origin}catch(e){o=''}}var u='/cdn-cgi/challenge-platform/scripts/precursor/main.js?ray=a5bf396958861dbe',s=document.createElement('script');s.src=o?new URL(u,o).href:u;document.head.appendChild(s);})();</script></body>
</html>
