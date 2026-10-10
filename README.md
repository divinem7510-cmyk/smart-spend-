<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0a1628">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>SmartSpend – Personal Expense Tracker</title>
<style>
:root{
  --bg:#0a1628;--bg2:#0f2038;--card:#132743;--card2:#1a3254;--text:#eaf2ff;--muted:#8fa6c4;
  --green:#2ee59d;--green-d:#14b87a;--red:#ff6b7a;--amber:#ffc24d;--border:rgba(255,255,255,.08);
  --shadow:0 10px 30px rgba(0,0,0,.35);--nav-h:68px;
  --sat:env(safe-area-inset-top,0px);--sab:env(safe-area-inset-bottom,0px);
}
[data-theme="light"]{
  --bg:#f2f6fb;--bg2:#e8eff8;--card:#ffffff;--card2:#eef3fa;--text:#0e2038;--muted:#5d7391;
  --green:#0fa968;--green-d:#0b8a54;--red:#d83a4e;--amber:#c98400;--border:rgba(14,32,56,.1);
  --shadow:0 10px 30px rgba(14,32,56,.12);
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;padding:0;max-width:100%;overflow-x:hidden}
body{
  font-family:-apple-system,BlinkMacSystemFont,"SF Pro Text","Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  background:radial-gradient(1200px 600px at 80% -10%,rgba(46,229,157,.12),transparent 60%),var(--bg);
  color:var(--text);line-height:1.45;-webkit-font-smoothing:antialiased;min-height:100vh;
}
button,input,select,textarea{font:inherit;color:inherit}
button{cursor:pointer;border:0;background:none}
.app{max-width:560px;margin:0 auto;padding:calc(var(--sat) + 16px) 16px calc(var(--nav-h) + var(--sab) + 96px)}
header.top{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px}
.brand{display:flex;align-items:center;gap:10px}
.logo{width:40px;height:40px;border-radius:12px;background:linear-gradient(135deg,var(--green),var(--green-d));display:grid;place-items:center;color:#04281a;font-weight:800;font-size:20px}
.brand h1{font-size:20px;margin:0;letter-spacing:.2px}
.brand small{display:block;color:var(--muted);font-size:12px}
.datebox{text-align:right;font-size:12px;color:var(--muted)}
.datebox strong{display:block;color:var(--text);font-size:14px}
.view{display:none;animation:fade .35s ease}
.view.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
h2{font-size:18px;margin:22px 0 10px}
.card{background:var(--card);border:1px solid var(--border);border-radius:20px;padding:16px;box-shadow:var(--shadow);margin-bottom:14px}
.hero{background:linear-gradient(145deg,var(--card2),var(--card));position:relative;overflow:hidden}
.hero::after{content:"";position:absolute;right:-40px;top:-40px;width:140px;height:140px;border-radius:50%;background:radial-gradient(var(--green),transparent 70%);opacity:.18}
.label{color:var(--muted);font-size:13px}
.big{font-size:32px;font-weight:800;letter-spacing:-.5px;word-break:break-word}
.grid3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:10px;margin-bottom:14px}
.mini{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:12px 10px;min-width:0}
.mini .v{font-weight:700;font-size:14px;margin-top:4px;word-break:break-word}
.pos{color:var(--green)}.neg{color:var(--red)}
.bar{height:10px;background:var(--card2);border-radius:99px;overflow:hidden;margin:10px 0 6px}
.bar>i{display:block;height:100%;width:0;border-radius:99px;background:linear-gradient(90deg,var(--green-d),var(--green));transition:width .8s cubic-bezier(.2,.8,.2,1)}
.bar.warn>i{background:linear-gradient(90deg,#e09b1a,var(--amber))}
.bar.over>i{background:linear-gradient(90deg,#d93a4d,var(--red))}
.alert{margin-top:8px;padding:10px 12px;border-radius:12px;font-size:13px;background:rgba(255,107,122,.14);color:var(--red);border:1px solid rgba(255,107,122,.35)}
.alert.amber{background:rgba(255,194,77,.14);color:var(--amber);border-color:rgba(255,194,77,.35)}
.row{display:flex;justify-content:space-between;align-items:center;gap:10px}
.tx{display:flex;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid var(--border)}
.tx:last-child{border-bottom:0}
.ico{width:42px;height:42px;border-radius:14px;display:grid;place-items:center;font-size:20px;flex:none;background:var(--card2)}
.tx .info{flex:1;min-width:0}
.tx .t{font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tx .m{font-size:12px;color:var(--muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tx .amt{font-weight:700;font-size:15px;white-space:nowrap}
.actions{display:flex;gap:6px;margin-top:6px}
.chip{min-height:36px;padding:6px 12px;border-radius:99px;background:var(--card2);font-size:13px;border:1px solid var(--border)}
.chip.danger{color:var(--red)}
.empty{text-align:center;color:var(--muted);padding:26px 10px;font-size:14px}
.empty b{display:block;font-size:30px;margin-bottom:6px}
.seg{display:flex;background:var(--card2);border-radius:14px;padding:4px;gap:4px;margin-bottom:14px}
.seg button,.seg label{flex:1;text-align:center;min-height:42px;border-radius:11px;font-weight:600;font-size:14px;color:var(--muted);display:grid;place-items:center;transition:.25s}
.seg .on{background:var(--green);color:#04281a}
.seg input{position:absolute;opacity:0;pointer-events:none}
.field{margin-bottom:14px}
.field label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
input[type=text],input[type=number],input[type=date],input[type=search],select,textarea{
  width:100%;min-height:48px;padding:12px 14px;border-radius:14px;background:var(--card2);
  border:1.5px solid var(--border);font-size:16px;outline:none;-webkit-appearance:none;appearance:none;transition:border .2s}
input:focus,select:focus,textarea:focus{border-color:var(--green)}
select{background-image:linear-gradient(45deg,transparent 50%,var(--muted) 50%),linear-gradient(135deg,var(--muted) 50%,transparent 50%);background-position:calc(100% - 20px) 21px,calc(100% - 15px) 21px;background-size:5px 5px;background-repeat:no-repeat;padding-right:36px}
textarea{min-height:70px;resize:vertical}
.err{color:var(--red);font-size:12px;min-height:16px;margin-top:4px}
.invalid{border-color:var(--red)!important}
.btn{min-height:50px;width:100%;border-radius:14px;font-weight:700;font-size:16px;background:linear-gradient(135deg,var(--green),var(--green-d));color:#04281a;transition:transform .15s}
.btn:active{transform:scale(.97)}
.btn.sec{background:var(--card2);color:var(--text);border:1px solid var(--border)}
.btn.dng{background:rgba(255,107,122,.15);color:var(--red);border:1px solid rgba(255,107,122,.4)}
.btns{display:grid;gap:10px}
.filters{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px}
.filters .full{grid-column:1/-1}
nav.bottom{position:fixed;left:0;right:0;bottom:0;z-index:20;background:var(--bg2);border-top:1px solid var(--border);padding-bottom:var(--sab);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px)}
nav.bottom ul{list-style:none;margin:0 auto;padding:0;max-width:560px;display:grid;grid-template-columns:repeat(4,1fr)}
nav.bottom button{width:100%;height:var(--nav-h);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;color:var(--muted);font-size:11px;font-weight:600}
nav.bottom button span.i{font-size:21px;line-height:1}
nav.bottom button[aria-current=page]{color:var(--green)}
.fab{position:fixed;right:max(18px,calc(50% - 262px));bottom:calc(var(--nav-h) + var(--sab) + 16px);width:58px;height:58px;border-radius:50%;z-index:25;
  background:linear-gradient(135deg,var(--green),var(--green-d));color:#04281a;font-size:32px;font-weight:300;box-shadow:0 10px 26px rgba(46,229,157,.4);display:grid;place-items:center;transition:transform .2s}
.fab:active{transform:scale(.92) rotate(90deg)}
.overlay{position:fixed;inset:0;background:rgba(2,8,20,.65);z-index:40;display:none;align-items:flex-end;justify-content:center;opacity:0;transition:opacity .25s}
.overlay.show{display:flex;opacity:1}
.sheet{width:100%;max-width:560px;max-height:92vh;overflow-y:auto;-webkit-overflow-scrolling:touch;background:var(--bg2);border-radius:26px 26px 0 0;padding:18px 16px calc(20px + var(--sab));animation:up .3s ease}
@keyframes up{from{transform:translateY(60px);opacity:0}to{transform:none;opacity:1}}
.sheet h3{margin:0 0 14px;font-size:19px}
.dialog{align-items:center;padding:20px}
.dialog .sheet{border-radius:22px;max-width:380px;padding:22px}
.toast{position:fixed;left:50%;bottom:calc(var(--nav-h) + var(--sab) + 84px);transform:translate(-50%,20px);background:var(--card2);border:1px solid var(--green);padding:10px 16px;border-radius:99px;font-size:14px;z-index:60;opacity:0;transition:.3s;pointer-events:none;max-width:90%;text-align:center}
.toast.show{opacity:1;transform:translate(-50%,0)}
svg{display:block;width:100%;height:auto;overflow:visible}
svg .b{transform-box:fill-box;transform-origin:bottom;animation:grow .7s ease both}
@keyframes grow{from{transform:scaleY(0)}to{transform:scaleY(1)}}
svg text{fill:var(--muted);font-size:9px}
.catrow{margin-bottom:12px}
.catrow .row{font-size:14px;margin-bottom:4px}
.legend{display:flex;gap:14px;font-size:12px;color:var(--muted);margin-top:8px}
.legend i{display:inline-block;width:10px;height:10px;border-radius:3px;margin-right:5px}
.stat2{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px}
.notice{font-size:13px;color:var(--muted)}
.hint{font-size:12px;color:var(--muted);margin:4px 0 0}
:focus-visible{outline:2px solid var(--green);outline-offset:2px}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style>
</head>
<body>
<div class="app">
  <header class="top">
    <div class="brand"><div class="logo" aria-hidden="true">S</div><div><h1>SmartSpend</h1><small>Your money, simplified</small></div></div>
    <div class="datebox"><strong id="todayDate">—</strong><span id="curMonth">—</span></div>
  </header>

  <main>
    <!-- DASHBOARD -->
    <section id="view-dashboard" class="view active" aria-label="Dashboard">
      <div class="card hero">
        <div class="label">Total balance</div>
        <div class="big" id="dBalance">₹0</div>
      </div>
      <div class="grid3">
        <div class="mini"><div class="label">Income</div><div class="v pos" id="dIncome">₹0</div></div>
        <div class="mini"><div class="label">Expenses</div><div class="v neg" id="dExpense">₹0</div></div>
        <div class="mini"><div class="label">Saved (month)</div><div class="v" id="dSavings">₹0</div></div>
      </div>
      <div class="card" id="dBudgetCard"></div>
      <div class="card">
        <div class="row"><strong>Expenses this month</strong><span class="label" id="dMonthTotal"></span></div>
        <div id="dChart" role="img" aria-label="Daily expense chart for this month"></div>
      </div>
      <div class="row"><h2>Recent transactions</h2><button class="chip" data-go="transactions">See all</button></div>
      <div class="card" id="dRecent"></div>
    </section>

    <!-- TRANSACTIONS -->
    <section id="view-transactions" class="view" aria-label="Transactions">
      <h2 style="margin-top:0">Transactions</h2>
      <div class="filters">
        <div class="full"><label class="label" for="fSearch" style="display:none">Search</label><input type="search" id="fSearch" placeholder="🔍 Search title, notes, amount…" autocomplete="off"></div>
        <div><label for="fCat" class="label" style="display:none">Category</label><select id="fCat" aria-label="Filter by category"></select></div>
        <div><label for="fType" class="label" style="display:none">Type</label>
          <select id="fType" aria-label="Filter by type"><option value="all">All types</option><option value="income">Income</option><option value="expense">Expense</option></select></div>
      </div>
      <div class="card" id="txList"></div>
    </section>

    <!-- ANALYTICS -->
    <section id="view-analytics" class="view" aria-label="Analytics">
      <h2 style="margin-top:0">Analytics</h2>
      <div class="seg" role="tablist" id="periodSeg" aria-label="Period">
        <button data-p="day" class="on" role="tab">Daily</button>
        <button data-p="week" role="tab">Weekly</button>
        <button data-p="month" role="tab">Monthly</button>
        <button data-p="year" role="tab">Yearly</button>
      </div>
      <div class="label" id="rangeLabel" style="margin:-6px 0 10px"></div>
      <div class="stat2">
        <div class="mini"><div class="label">Income</div><div class="v pos" id="aInc">₹0</div></div>
        <div class="mini"><div class="label">Expenses</div><div class="v neg" id="aExp">₹0</div></div>
        <div class="mini"><div class="label">Net savings</div><div class="v" id="aNet">₹0</div></div>
        <div class="mini"><div class="label">Savings rate</div><div class="v" id="aRate">—</div></div>
      </div>
      <div class="card"><strong>Income vs expense</strong><div class="label">Last 6 months</div><div id="aChart" role="img" aria-label="Income versus expense chart"></div>
        <div class="legend"><span><i style="background:var(--green)"></i>Income</span><span><i style="background:var(--red)"></i>Expense</span></div></div>
      <div class="card"><strong>Expense by category</strong><div class="label" style="margin-bottom:12px">For selected period</div><div id="aCats"></div></div>
    </section>

    <!-- SETTINGS -->
    <section id="view-settings" class="view" aria-label="Settings">
      <h2 style="margin-top:0">Settings</h2>
      <div class="card">
        <strong>Theme</strong>
        <div class="seg" style="margin:10px 0 0" id="themeSeg">
          <button data-t="dark">🌙 Dark</button><button data-t="light">☀️ Light</button>
        </div>
      </div>
      <div class="card">
        <strong>Monthly budget (₹)</strong>
        <div class="field" style="margin-top:10px"><label for="budgetInput" class="label">Amount (0 = no budget)</label>
          <input type="number" id="budgetInput" inputmode="decimal" min="0" step="1" placeholder="e.g. 25000"><div class="err" id="budgetErr"></div></div>
        <button class="btn" id="saveBudget">Save budget</button>
      </div>
      <div class="card">
        <strong>Export data</strong>
        <div class="btns" style="margin-top:10px"><button class="btn sec" id="expCsv">⬇ Export CSV</button><button class="btn sec" id="expJson">⬇ Export JSON</button></div>
      </div>
      <div class="card">
        <strong>Demo data</strong>
        <p class="hint">Sample transactions help you explore the app. Removing demo data keeps your own entries.</p>
        <div class="btns" style="margin-top:10px"><button class="btn sec" id="removeDemo">Remove demo data</button><button class="btn sec" id="resetDemo">Reset demo data</button></div>
      </div>
      <div class="card">
        <strong>Danger zone</strong>
        <div class="btns" style="margin-top:10px"><button class="btn dng" id="clearAll">Clear all data</button></div>
      </div>
      <div class="card"><strong>🔒 Privacy</strong>
        <p class="notice">SmartSpend has no account, no server and no cloud sync. Everything you enter is stored only in this browser on this device (localStorage). Clearing Safari website data or using Private mode can erase it, so export a backup now and then.</p></div>
    </section>
  </main>
</div>

<button class="fab" id="fab" aria-label="Add transaction">+</button>

<nav class="bottom" aria-label="Main navigation"><ul>
  <li><button data-go="dashboard" aria-current="page"><span class="i" aria-hidden="true">🏠</span>Dashboard</button></li>
  <li><button data-go="transactions"><span class="i" aria-hidden="true">🧾</span>Transactions</button></li>
  <li><button data-go="analytics"><span class="i" aria-hidden="true">📊</span>Analytics</button></li>
  <li><button data-go="settings"><span class="i" aria-hidden="true">⚙️</span>Settings</button></li>
</ul></nav>

<!-- Add/Edit sheet -->
<div class="overlay" id="txOverlay" role="dialog" aria-modal="true" aria-labelledby="txTitleH">
  <form class="sheet" id="txForm" novalidate>
    <h3 id="txTitleH">Add transaction</h3>
    <div class="seg" id="typeSeg" role="radiogroup" aria-label="Transaction type">
      <label class="on" id="lblExpense"><input type="radio" name="type" value="expense" checked>Expense</label>
      <label id="lblIncome"><input type="radio" name="type" value="income">Income</label>
    </div>
    <div class="field"><label for="fTitle">Title *</label><input type="text" id="fTitle" maxlength="60" autocomplete="off" placeholder="e.g. Lunch at Annapoorna"><div class="err" id="eTitle"></div></div>
    <div class="field"><label for="fAmount">Amount (₹) *</label><input type="number" id="fAmount" inputmode="decimal" step="0.01" min="0" placeholder="0.00"><div class="err" id="eAmount"></div></div>
    <div class="field"><label for="fCategory">Category *</label><select id="fCategory"></select></div>
    <div class="field"><label for="fDate">Date *</label><input type="date" id="fDate"><div class="err" id="eDate"></div></div>
    <div class="field"><label for="fMethod">Payment method</label>
      <select id="fMethod"><option>UPI</option><option>Cash</option><option>Debit Card</option><option>Credit Card</option><option>Net Banking</option><option>Other</option></select></div>
    <div class="field"><label for="fNotes">Notes (optional)</label><textarea id="fNotes" maxlength="200" placeholder="Anything to remember…"></textarea></div>
    <div class="btns"><button type="submit" class="btn" id="txSubmit">Save transaction</button><button type="button" class="btn sec" id="txCancel">Cancel</button></div>
  </form>
</div>

<!-- Confirm dialog -->
<div class="overlay dialog" id="cfOverlay" role="alertdialog" aria-modal="true" aria-labelledby="cfTitle">
  <div class="sheet">
    <h3 id="cfTitle">Are you sure?</h3>
    <p class="notice" id="cfMsg"></p>
    <div class="btns"><button class="btn dng" id="cfOk">Delete</button><button class="btn sec" id="cfNo">Cancel</button></div>
  </div>
</div>
<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
(function(){
"use strict";
var KEY="smartspend_v1";
var EXP_CATS=["Food","Transport","Shopping","Bills","Healthcare","Education","Entertainment","Other"];
var INC_CATS=["Salary","Freelance","Other"];
var ALL_CATS=["Food","Transport","Shopping","Bills","Healthcare","Education","Entertainment","Salary","Freelance","Other"];
var ICONS={Food:"🍽️",Transport:"🚌",Shopping:"🛍️",Bills:"💡",Healthcare:"💊",Education:"🎓",Entertainment:"🎬",Salary:"💼",Freelance:"💻",Other:"📦"};
var COLORS={Food:"#2ee59d",Transport:"#4db8ff",Shopping:"#ff7eb6",Bills:"#ffc24d",Healthcare:"#ff6b7a",Education:"#a78bfa",Entertainment:"#ff9f5a",Salary:"#34d399",Freelance:"#22d3ee",Other:"#94a3b8"};

var state={transactions:[],settings:{theme:"dark",budget:0,demoLoaded:false}};
var period="day", editingId=null, confirmCb=null;
var $=function(id){return document.getElementById(id)};

/* ---------- helpers ---------- */
function esc(s){return String(s==null?"":s).replace(/[&<>"']/g,function(c){return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]})}
function pad(n){return n<10?"0"+n:""+n}
function ds(d){return d.getFullYear()+"-"+pad(d.getMonth()+1)+"-"+pad(d.getDate())}
function today(){return ds(new Date())}
function uid(){return Date.now().toString(36)+Math.random().toString(36).slice(2,8)}
function parseD(s){var p=s.split("-");return new Date(+p[0],+p[1]-1,+p[2])}
var inr;
try{inr=new Intl.NumberFormat("en-IN",{style:"currency",currency:"INR",maximumFractionDigits:2})}catch(e){inr=null}
function money(n){
  n=Math.round(n*100)/100;
  if(inr){var s=inr.format(n);return s.replace(/\.00$/,"")}
  var neg=n<0;n=Math.abs(n);var parts=n.toFixed(2).split("."),x=parts[0],last=x.slice(-3),rest=x.slice(0,-3);
  if(rest)last=rest.replace(/\B(?=(\d{2})+(?!\d))/g,",")+","+last;
  return (neg?"-":"")+"₹"+last+(parts[1]==="00"?"":"."+parts[1]);
}
function fmtDate(s){return parseD(s).toLocaleDateString("en-IN",{day:"numeric",month:"short",year:"numeric"})}
function toast(msg){var t=$("toast");t.textContent=msg;t.classList.add("show");clearTimeout(toast.t);toast.t=setTimeout(function(){t.classList.remove("show")},2200)}

/* ---------- storage ---------- */
function save(){try{localStorage.setItem(KEY,JSON.stringify(state))}catch(e){toast("Could not save: storage is full or blocked")}}
function load(){
  try{
    var raw=localStorage.getItem(KEY);
    if(raw){
      var d=JSON.parse(raw);
      if(d&&Array.isArray(d.transactions)){
        state.transactions=d.transactions.filter(function(t){return t&&t.id&&t.date&&isFinite(t.amount)});
        state.settings=Object.assign(state.settings,d.settings||{});
        return;
      }
    }
  }catch(e){}
  state.transactions=demoData();state.settings.demoLoaded=true;save();
}
function demoData(){
  var now=new Date(),y=now.getFullYear(),m=now.getMonth(),out=[];
  function add(off,mo,type,title,amt,cat,method){
    var d=new Date(y,m-mo,1);var day=Math.max(1,Math.min(off,new Date(d.getFullYear(),d.getMonth()+1,0).getDate()));
    var dt=new Date(d.getFullYear(),d.getMonth(),day);
    if(mo===0&&dt>now)dt=new Date(now);
    out.push({id:uid(),type:type,title:title,amount:amt,category:cat,date:ds(dt),method:method,notes:"",demo:true});
  }
  for(var k=0;k<4;k++){
    add(1,k,"income","Monthly salary",42000,"Salary","Net Banking");
    add(3,k,"expense","House rent & bills",9500,"Bills","UPI");
    add(5,k,"expense","Groceries",2350+k*120,"Food","UPI");
    add(8,k,"expense","Metro & auto",780,"Transport","Cash");
    add(12,k,"expense","Online shopping",3200-k*300,"Shopping","Credit Card");
    add(15,k,"expense","Movie night",640,"Entertainment","UPI");
    add(18,k,"income","Freelance project",k%2?6500:9000,"Freelance","UPI");
    add(21,k,"expense","Online course",k===0?1499:799,"Education","Debit Card");
    add(24,k,"expense","Pharmacy",k===1?1250:420,"Healthcare","Cash");
  }
  add(now.getDate(),0,"expense","Tea & snacks",120,"Food","Cash");
  return out;
}

/* ---------- calculations ---------- */
function sum(list,type){return list.reduce(function(a,t){return t.type===type?a+Number(t.amount):a},0)}
function monthPrefix(d){return d.getFullYear()+"-"+pad(d.getMonth()+1)}
function inMonth(d){var p=monthPrefix(d||new Date());return state.transactions.filter(function(t){return t.date.slice(0,7)===p})}
function getRange(p){
  var n=new Date(),y=n.getFullYear(),m=n.getMonth(),d=n.getDate(),s,e;
  if(p==="day"){s=e=new Date(y,m,d)}
  else if(p==="week"){var off=(n.getDay()+6)%7;s=new Date(y,m,d-off);e=new Date(y,m,d-off+6)}
  else if(p==="month"){s=new Date(y,m,1);e=new Date(y,m+1,0)}
  else{s=new Date(y,0,1);e=new Date(y,11,31)}
  return [ds(s),ds(e)];
}
function inRange(r){return state.transactions.filter(function(t){return t.date>=r[0]&&t.date<=r[1]})}

/* ---------- charts (inline SVG, no library) ---------- */
function dailyChart(){
  var n=new Date(),dim=new Date(n.getFullYear(),n.getMonth()+1,0).getDate(),arr=[],i;
  for(i=0;i<dim;i++)arr.push(0);
  inMonth().forEach(function(t){if(t.type==="expense"){arr[+t.date.slice(8,10)-1]+=Number(t.amount)}});
  var max=Math.max.apply(null,arr),W=300,H=120,bw=W/dim;
  if(max<=0)return '<div class="empty">No expenses recorded this month.</div>';
  var s='<svg viewBox="0 0 '+W+' '+(H+16)+'" preserveAspectRatio="xMidYMid meet">';
  s+='<line x1="0" y1="'+H+'" x2="'+W+'" y2="'+H+'" stroke="var(--border)"/>';
  arr.forEach(function(v,i){
    var h=Math.max(v>0?3:0,v/max*(H-8));
    s+='<rect class="b" x="'+(i*bw+bw*.15).toFixed(2)+'" y="'+(H-h).toFixed(2)+'" width="'+(bw*.7).toFixed(2)+'" height="'+h.toFixed(2)+'" rx="2" fill="'+(i+1===n.getDate()?'var(--green)':'var(--green-d)')+'" opacity="'+(i+1===n.getDate()?1:.65)+'" style="animation-delay:'+(i*12)+'ms"><title>Day '+(i+1)+': '+esc(money(v))+'</title></rect>';
  });
  [1,Math.ceil(dim/3),Math.ceil(dim*2/3),dim].forEach(function(d){s+='<text x="'+((d-.5)*bw).toFixed(1)+'" y="'+(H+12)+'" text-anchor="middle">'+d+'</text>'});
  return s+'</svg>';
}
function incExpChart(){
  var n=new Date(),months=[],i;
  for(i=5;i>=0;i--){var d=new Date(n.getFullYear(),n.getMonth()-i,1);var list=inMonth(d);
    months.push({l:d.toLocaleDateString("en-IN",{month:"short"}),inc:sum(list,"income"),exp:sum(list,"expense")})}
  var max=Math.max.apply(null,months.map(function(m){return Math.max(m.inc,m.exp)}));
  if(max<=0)return '<div class="empty">No data yet.</div>';
  var W=300,H=130,gw=W/6,bw=gw*.3,s='<svg viewBox="0 0 '+W+' '+(H+18)+'">';
  s+='<line x1="0" y1="'+H+'" x2="'+W+'" y2="'+H+'" stroke="var(--border)"/>';
  months.forEach(function(m,i){
    var x=i*gw+gw*.15,hi=m.inc/max*(H-8),he=m.exp/max*(H-8);
    s+='<rect class="b" x="'+x.toFixed(1)+'" y="'+(H-hi).toFixed(1)+'" width="'+bw.toFixed(1)+'" height="'+hi.toFixed(1)+'" rx="3" fill="var(--green)"><title>'+esc(m.l)+' income: '+esc(money(m.inc))+'</title></rect>';
    s+='<rect class="b" x="'+(x+bw+3).toFixed(1)+'" y="'+(H-he).toFixed(1)+'" width="'+bw.toFixed(1)+'" height="'+he.toFixed(1)+'" rx="3" fill="var(--red)"><title>'+esc(m.l)+' expense: '+esc(money(m.exp))+'</title></rect>';
    s+='<text x="'+(i*gw+gw/2).toFixed(1)+'" y="'+(H+13)+'" text-anchor="middle">'+esc(m.l)+'</text>';
  });
  return s+'</svg>';
}

/* ---------- rendering ---------- */
function txRow(t,withActions){
  var inc=t.type==="income";
  return '<div class="tx"><div class="ico" aria-hidden="true">'+(ICONS[t.category]||"📦")+'</div>'+
    '<div class="info"><div class="t">'+esc(t.title)+'</div><div class="m">'+esc(t.category)+' · '+esc(t.method||"—")+' · '+esc(fmtDate(t.date))+'</div>'+
    (t.notes?'<div class="m">📝 '+esc(t.notes)+'</div>':'')+
    (withActions?'<div class="actions"><button class="chip" data-edit="'+esc(t.id)+'" aria-label="Edit '+esc(t.title)+'">✏️ Edit</button><button class="chip danger" data-del="'+esc(t.id)+'" aria-label="Delete '+esc(t.title)+'">🗑 Delete</button></div>':'')+
    '</div><div class="amt '+(inc?'pos':'neg')+'">'+(inc?'+':'−')+esc(money(Number(t.amount)))+'</div></div>';
}
function sorted(list){return list.slice().sort(function(a,b){return a.date<b.date?1:a.date>b.date?-1:(a.id<b.id?1:-1)})}

function renderDashboard(){
  var n=new Date(),all=state.transactions,inc=sum(all,"income"),exp=sum(all,"expense");
  $("todayDate").textContent=n.toLocaleDateString("en-IN",{weekday:"short",day:"numeric",month:"short",year:"numeric"});
  $("curMonth").textContent=n.toLocaleDateString("en-IN",{month:"long",year:"numeric"});
  $("dBalance").textContent=money(inc-exp);
  $("dIncome").textContent=money(inc);$("dExpense").textContent=money(exp);
  var ml=inMonth(),mi=sum(ml,"income"),me=sum(ml,"expense"),sv=mi-me;
  var sEl=$("dSavings");sEl.textContent=money(sv);sEl.className="v "+(sv>=0?"pos":"neg");
  $("dMonthTotal").textContent=money(me);
  $("dChart").innerHTML=dailyChart();
  var b=Number(state.settings.budget)||0,card=$("dBudgetCard");
  if(b<=0){card.innerHTML='<strong>Monthly budget</strong><p class="notice">No budget set yet. Add one to track your spending.</p><button class="chip" data-go="settings">Set budget</button>'}
  else{
    var pct=me/b*100,cls=pct>100?"over":pct>=80?"warn":"";
    card.innerHTML='<div class="row"><strong>Monthly budget</strong><span class="label">'+pct.toFixed(0)+'% used</span></div>'+
      '<div class="bar '+cls+'" role="progressbar" aria-valuemin="0" aria-valuemax="100" aria-valuenow="'+Math.min(100,pct).toFixed(0)+'"><i style="width:0"></i></div>'+
      '<div class="row label"><span>'+esc(money(me))+' spent</span><span>of '+esc(money(b))+'</span></div>'+
      (pct>100?'<div class="alert">⚠️ You have exceeded your budget by '+esc(money(me-b))+'.</div>':
       pct>=80?'<div class="alert amber">Heads up: you have used '+pct.toFixed(0)+'% of your budget. '+esc(money(b-me))+' left.</div>':
       '<div class="label" style="margin-top:6px">'+esc(money(b-me))+' remaining this month.</div>');
    var bar=card.querySelector(".bar>i");setTimeout(function(){bar.style.width=Math.min(100,pct)+"%"},60);
  }
  var rec=sorted(all).slice(0,5);
  $("dRecent").innerHTML=rec.length?rec.map(function(t){return txRow(t,false)}).join(""):'<div class="empty"><b>🪙</b>No transactions yet.<br>Tap + to add your first one.</div>';
}
function renderFilters(){
  var sel=$("fCat"),cur=sel.value||"all";
  sel.innerHTML='<option value="all">All categories</option>'+ALL_CATS.map(function(c){return '<option>'+c+'</option>'}).join("");
  sel.value=cur;
}
function renderTx(){
  var q=$("fSearch").value.trim().toLowerCase(),c=$("fCat").value,ty=$("fType").value;
  var list=sorted(state.transactions).filter(function(t){
    if(c!=="all"&&t.category!==c)return false;
    if(ty!=="all"&&t.type!==ty)return false;
    if(q){var hay=(t.title+" "+(t.notes||"")+" "+t.category+" "+t.method+" "+t.amount).toLowerCase();if(hay.indexOf(q)<0)return false}
    return true;
  });
  $("txList").innerHTML=list.length?list.map(function(t){return txRow(t,true)}).join(""):
    (state.transactions.length?'<div class="empty"><b>🔎</b>No transactions match your filters.</div>':'<div class="empty"><b>🧾</b>Nothing here yet.<br>Tap + to add a transaction.</div>');
}
function renderAnalytics(){
  var r=getRange(period),list=inRange(r),inc=sum(list,"income"),exp=sum(list,"expense"),net=inc-exp;
  $("rangeLabel").textContent=r[0]===r[1]?fmtDate(r[0]):fmtDate(r[0])+" – "+fmtDate(r[1]);
  $("aInc").textContent=money(inc);$("aExp").textContent=money(exp);
  var nEl=$("aNet");nEl.textContent=money(net);nEl.className="v "+(net>=0?"pos":"neg");
  var rEl=$("aRate");
  if(inc>0){var rate=net/inc*100;rEl.textContent=rate.toFixed(1)+"%";rEl.className="v "+(rate>=0?"pos":"neg")}else{rEl.textContent="—";rEl.className="v"}
  $("aChart").innerHTML=incExpChart();
  var cats={};list.forEach(function(t){if(t.type==="expense")cats[t.category]=(cats[t.category]||0)+Number(t.amount)});
  var keys=Object.keys(cats).sort(function(a,b){return cats[b]-cats[a]});
  $("aCats").innerHTML=keys.length?keys.map(function(k){
    var p=exp>0?cats[k]/exp*100:0;
    return '<div class="catrow"><div class="row"><span>'+(ICONS[k]||"")+' '+esc(k)+'</span><span><strong>'+esc(money(cats[k]))+'</strong> <span class="label">'+p.toFixed(1)+'%</span></span></div>'+
      '<div class="bar" style="margin:0"><i style="width:'+p.toFixed(1)+'%;background:'+(COLORS[k]||"#2ee59d")+'"></i></div></div>';
  }).join(""):'<div class="empty"><b>📊</b>No expenses in this period.</div>';
}
function renderSettings(){
  $("budgetInput").value=state.settings.budget>0?state.settings.budget:"";
  Array.prototype.forEach.call($("themeSeg").children,function(b){b.classList.toggle("on",b.dataset.t===state.settings.theme)});
}
function renderAll(){renderDashboard();renderTx();renderAnalytics();renderSettings()}

/* ---------- theme & nav ---------- */
function applyTheme(){
  document.documentElement.setAttribute("data-theme",state.settings.theme);
  var m=document.querySelector('meta[name="theme-color"]');if(m)m.setAttribute("content",state.settings.theme==="light"?"#f2f6fb":"#0a1628");
}
function go(name){
  document.querySelectorAll(".view").forEach(function(v){v.classList.toggle("active",v.id==="view-"+name)});
  document.querySelectorAll("nav.bottom button").forEach(function(b){if(b.dataset.go===name)b.setAttribute("aria-current","page");else b.removeAttribute("aria-current")});
  window.scrollTo(0,0);
  if(name==="analytics")renderAnalytics();
}

/* ---------- modal: add/edit ---------- */
function fillCats(type,sel){
  var list=type==="income"?INC_CATS:EXP_CATS,c=$("fCategory");
  c.innerHTML=list.map(function(x){return '<option>'+x+'</option>'}).join("");
  if(sel&&list.indexOf(sel)>=0)c.value=sel;
}
function setType(type){
  document.querySelector('input[name=type][value='+type+']').checked=true;
  $("lblExpense").classList.toggle("on",type==="expense");$("lblIncome").classList.toggle("on",type==="income");
  fillCats(type);
}
function clearErr(){["eTitle","eAmount","eDate"].forEach(function(i){$(i).textContent=""});["fTitle","fAmount","fDate"].forEach(function(i){$(i).classList.remove("invalid")})}
function openTx(id){
  clearErr();editingId=id||null;
  var t=id?state.transactions.filter(function(x){return x.id===id})[0]:null;
  $("txTitleH").textContent=t?"Edit transaction":"Add transaction";
  $("txSubmit").textContent=t?"Update transaction":"Save transaction";
  setType(t?t.type:"expense");
  if(t)fillCats(t.type,t.category);
  $("fTitle").value=t?t.title:"";$("fAmount").value=t?t.amount:"";
  $("fDate").value=t?t.date:today();$("fMethod").value=t?(t.method||"UPI"):"UPI";$("fNotes").value=t?(t.notes||""):"";
  $("txOverlay").classList.add("show");document.body.style.overflow="hidden";
  setTimeout(function(){$("fTitle").focus()},120);
}
function closeTx(){$("txOverlay").classList.remove("show");document.body.style.overflow="";editingId=null}
function bad(inp,err,msg){$(inp).classList.add("invalid");$(err).textContent=msg;return false}
function submitTx(e){
  e.preventDefault();clearErr();
  var type=document.querySelector("input[name=type]:checked").value,
      title=$("fTitle").value.trim(),amtRaw=$("fAmount").value.trim(),amt=parseFloat(amtRaw),date=$("fDate").value,ok=true;
  if(!title)ok=bad("fTitle","eTitle","Please enter a title.");
  if(!amtRaw||!isFinite(amt)||amt<=0)ok=bad("fAmount","eAmount","Enter an amount greater than 0.");
  else if(amt>1000000000)ok=bad("fAmount","eAmount","Amount is too large.");
  if(!date||isNaN(parseD(date).getTime()))ok=bad("fDate","eDate","Please choose a valid date.");
  if(!ok)return;
  var rec={type:type,title:title,amount:Math.round(amt*100)/100,category:$("fCategory").value,date:date,method:$("fMethod").value,notes:$("fNotes").value.trim()};
  if(editingId){
    state.transactions=state.transactions.map(function(t){return t.id===editingId?Object.assign({},t,rec,{demo:false}):t});
    toast("Transaction updated ✓");
  }else{rec.id=uid();rec.demo=false;state.transactions.push(rec);toast("Transaction added ✓")}
  save();closeTx();renderAll();
}

/* ---------- confirm ---------- */
function ask(title,msg,okLabel,cb){
  $("cfTitle").textContent=title;$("cfMsg").textContent=msg;$("cfOk").textContent=okLabel;confirmCb=cb;
  $("cfOverlay").classList.add("show");
}
function closeAsk(){$("cfOverlay").classList.remove("show");confirmCb=null}

/* ---------- export ---------- */
function download(name,text,mime){
  try{
    var blob=new Blob([text],{type:mime}),url=URL.createObjectURL(blob),a=document.createElement("a");
    a.href=url;a.download=name;document.body.appendChild(a);a.click();
    setTimeout(function(){document.body.removeChild(a);URL.revokeObjectURL(url)},1500);
    toast("Export ready – check Downloads / Share sheet");
  }catch(e){toast("Export not supported in this browser")}
}
function csvCell(v){v=String(v==null?"":v);if(/^[=+\-@]/.test(v))v="'"+v;return '"'+v.replace(/"/g,'""')+'"'}
function exportCsv(){
  if(!state.transactions.length){toast("No transactions to export");return}
  var rows=[["Date","Type","Title","Category","Amount (INR)","Payment Method","Notes"]];
  sorted(state.transactions).forEach(function(t){rows.push([t.date,t.type,t.title,t.category,t.amount,t.method,t.notes])});
  download("smartspend-"+today()+".csv","\ufeff"+rows.map(function(r){return r.map(csvCell).join(",")}).join("\r\n"),"text/csv;charset=utf-8");
}
function exportJson(){
  download("smartspend-"+today()+".json",JSON.stringify({exportedAt:new Date().toISOString(),settings:state.settings,transactions:state.transactions},null,2),"application/json");
}

/* ---------- events ---------- */
function bind(){
  document.addEventListener("click",function(e){
    var g=e.target.closest("[data-go]");if(g){go(g.dataset.go);return}
    var ed=e.target.closest("[data-edit]");if(ed){openTx(ed.dataset.edit);return}
    var dl=e.target.closest("[data-del]");
    if(dl){
      var id=dl.dataset.del,t=state.transactions.filter(function(x){return x.id===id})[0];if(!t)return;
      ask("Delete transaction?",'"'+t.title+'" ('+money(Number(t.amount))+') will be permanently deleted.',"Delete",function(){
        state.transactions=state.transactions.filter(function(x){return x.id!==id});save();renderAll();toast("Transaction deleted");
      });
    }
  });
  $("fab").addEventListener("click",function(){openTx()});
  $("txForm").addEventListener("submit",submitTx);
  $("txCancel").addEventListener("click",closeTx);
  $("txOverlay").addEventListener("click",function(e){if(e.target===this)closeTx()});
  $("typeSeg").addEventListener("change",function(e){if(e.target.name==="type")setType(e.target.value)});
  $("cfNo").addEventListener("click",closeAsk);
  $("cfOk").addEventListener("click",function(){var cb=confirmCb;closeAsk();if(cb)cb()});
  $("cfOverlay").addEventListener("click",function(e){if(e.target===this)closeAsk()});
  document.addEventListener("keydown",function(e){if(e.key==="Escape"){closeAsk();closeTx()}});
  ["fSearch","fCat","fType"].forEach(function(i){$(i).addEventListener("input",renderTx);$(i).addEventListener("change",renderTx)});
  $("periodSeg").addEventListener("click",function(e){
    var b=e.target.closest("button");if(!b)return;period=b.dataset.p;
    Array.prototype.forEach.call($("periodSeg").children,function(x){x.classList.toggle("on",x===b)});renderAnalytics();
  });
  $("themeSeg").addEventListener("click",function(e){
    var b=e.target.closest("button");if(!b)return;state.settings.theme=b.dataset.t;save();applyTheme();renderSettings();
  });
  $("saveBudget").addEventListener("click",function(){
    var raw=$("budgetInput").value.trim(),v=raw===""?0:parseFloat(raw);
    if(!isFinite(v)||v<0||v>1000000000){$("budgetErr").textContent="Enter a valid amount (0 or more).";$("budgetInput").classList.add("invalid");return}
    $("budgetErr").textContent="";$("budgetInput").classList.remove("invalid");
    state.settings.budget=Math.round(v*100)/100;save();renderAll();toast(v>0?"Budget saved ✓":"Budget removed");
  });
  $("expCsv").addEventListener("click",exportCsv);
  $("expJson").addEventListener("click",exportJson);
  $("removeDemo").addEventListener("click",function(){
    var n=state.transactions.filter(function(t){return t.demo}).length;
    if(!n){toast("No demo data found");return}
    ask("Remove demo data?",n+" sample transactions will be deleted. Your own entries stay safe.","Remove",function(){
      state.transactions=state.transactions.filter(function(t){return !t.demo});save();renderAll();toast("Demo data removed");
    });
  });
  $("resetDemo").addEventListener("click",function(){
    ask("Reset demo data?","Existing demo transactions are replaced with fresh samples. Your own entries are kept.","Reset",function(){
      state.transactions=state.transactions.filter(function(t){return !t.demo}).concat(demoData());state.settings.demoLoaded=true;save();renderAll();toast("Demo data reloaded");
    });
  });
  $("clearAll").addEventListener("click",function(){
    ask("Clear ALL data?","All transactions and settings will be permanently erased from this browser. This cannot be undone. Export a backup first if needed.","Erase everything",function(){
      state={transactions:[],settings:{theme:state.settings.theme,budget:0,demoLoaded:true}};save();renderAll();applyTheme();toast("All data cleared");
    });
  });
}

/* ---------- init ---------- */
load();applyTheme();renderFilters();bind();renderAll();
})();
</script>
</body>
</html>
