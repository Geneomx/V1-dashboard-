<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Geneomx — Consumer Portal V1 (Functional + Check-ins + Feedback)</title>
  <style>
    :root{
      --bg0:#070A12;
      --bg1:#0B1022;
      --txt:#EAF0FF;
      --muted:#A9B4D6;

      --card:#0F1736E6;
      --stroke:#24325E;

      --cyan:#28E1FF;
      --violet:#A78BFA;
      --pink:#FF4FD8;
      --amber:#FBBF24;
      --green:#34D399;
      --red:#FB7185;

      --r:18px;
      --shadow: 0 18px 55px rgba(0,0,0,.35);
      --sans: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
    }

    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:var(--sans);
      color:var(--txt);
      background:
        radial-gradient(1200px 700px at 20% -10%, rgba(40,225,255,.12), transparent 60%),
        radial-gradient(900px 600px at 80% 10%, rgba(167,139,250,.12), transparent 55%),
        radial-gradient(900px 700px at 30% 110%, rgba(255,79,216,.10), transparent 55%),
        linear-gradient(180deg, var(--bg0), var(--bg1));
      min-height:100vh;
    }

    .wrap{max-width:1180px;margin:0 auto;padding:22px 18px 44px}
    .top{display:flex;align-items:center;justify-content:space-between;gap:14px;margin-bottom:14px}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{
      width:44px;height:44px;border-radius:14px;
      background: linear-gradient(135deg, rgba(40,225,255,.95), rgba(167,139,250,.92));
      box-shadow: 0 14px 34px rgba(40,225,255,.16);
      border: 1px solid rgba(255,255,255,.14);
    }
    h1{margin:0;font-size:16px;letter-spacing:.2px}
    .sub{margin:4px 0 0 0;color:var(--muted);font-size:14px;line-height:1.4}

    .status{display:flex;gap:10px;flex-wrap:wrap;justify-content:flex-end}
    .badge{
      border:1px solid rgba(255,255,255,.12);
      background: rgba(15,23,54,.60);
      border-radius:999px;
      padding:9px 12px;
      font-size:13px;
      color:var(--muted);
      box-shadow: 0 10px 22px rgba(0,0,0,.18);
    }
    .badge strong{color:var(--txt);font-weight:900}

    .grid{
      display:grid;
      grid-template-columns: 1.2fr .8fr;
      gap:16px;
    }
    @media (max-width: 980px){ .grid{grid-template-columns:1fr} }

    .card{
      border-radius: var(--r);
      border:1px solid rgba(255,255,255,.12);
      background: linear-gradient(180deg, rgba(15,23,54,.72), rgba(16,27,64,.58));
      box-shadow: var(--shadow);
      overflow:hidden;
    }
    .hd{
      padding:16px 16px 12px 16px;
      border-bottom:1px solid rgba(255,255,255,.10);
      display:flex;align-items:flex-start;justify-content:space-between;gap:12px;
    }
    .hd h2{margin:0;font-size:15px}
    .hd .desc{margin:6px 0 0 0;color:var(--muted);font-size:14px;line-height:1.45}
    .bd{padding:18px}

    /* colorful tabs */
    .steps{display:flex;gap:8px;flex-wrap:wrap;justify-content:flex-end}
    .step{
      padding:9px 12px;border-radius:999px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(7,10,18,.35);
      color: var(--muted);
      font-size:13px;cursor:pointer;user-select:none;
      box-shadow: 0 10px 20px rgba(0,0,0,.16);
      transition: transform .05s ease, filter .15s ease;
    }
    .step:hover{filter:brightness(1.05)}
    .step:active{transform:translateY(1px)}
    .step.on{color:#061018;font-weight:950}
    .c1.on{background: linear-gradient(135deg, rgba(40,225,255,.92), rgba(21,101,192,.65))}
    .c2.on{background: linear-gradient(135deg, rgba(251,191,36,.92), rgba(239,108,0,.70))}
    .c3.on{background: linear-gradient(135deg, rgba(52,211,153,.92), rgba(16,185,129,.65))}
    .c4.on{background: linear-gradient(135deg, rgba(167,139,250,.92), rgba(99,102,241,.65))}
    .c5.on{background: linear-gradient(135deg, rgba(255,79,216,.92), rgba(236,72,153,.65))}
    .c6.on{background: linear-gradient(135deg, rgba(148,163,184,.92), rgba(100,116,139,.65))}
    .c7.on{background: linear-gradient(135deg, rgba(251,113,133,.92), rgba(244,63,94,.65))}
    .c8.on{background: linear-gradient(135deg, rgba(59,130,246,.92), rgba(34,211,238,.65))}
    .c9.on{background: linear-gradient(135deg, rgba(16,185,129,.92), rgba(40,225,255,.65))}

    .section{
      padding:16px;
      border:1px solid rgba(255,255,255,.12);
      border-radius:16px;
      background: rgba(7,10,18,.28);
    }
    .section + .section{margin-top:14px}
    .row{display:flex;gap:12px;flex-wrap:wrap}
    .col{flex:1;min-width:220px}

    label{display:block;font-size:13px;color:var(--muted);margin:0 0 8px}
    input, select, textarea{
      width:100%;
      padding:11px 12px;
      border-radius: 12px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(7,10,18,.45);
      color: var(--txt);
      outline:none;
      font-size:14px;
    }
    textarea{min-height:115px;resize:vertical}
    input::placeholder, textarea::placeholder{color: rgba(169,180,214,.75)}

    .btns{display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-top:14px}
    button{
      border:none;padding:11px 14px;border-radius: 12px;
      cursor:pointer;font-size:14px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(15,23,54,.55);
      color:var(--txt);
      box-shadow: 0 10px 22px rgba(0,0,0,.18);
      transition: transform .05s ease, filter .15s ease;
    }
    button:hover{filter:brightness(1.06)}
    button:active{transform: translateY(1px)}
    .primary{
      border-color: rgba(255,255,255,.18);
      background: linear-gradient(135deg, rgba(40,225,255,.92), rgba(167,139,250,.86));
      color:#061018;
      font-weight:950;
    }
    .ghost{background: rgba(7,10,18,.35)}
    .danger{background: rgba(251,113,133,.18);border-color: rgba(251,113,133,.35)}

    .fineprint{font-size:14px;line-height:1.5;color: var(--muted)}
    .divider{height:1px;background: rgba(255,255,255,.10);margin:14px 0}

    .chips{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
    .chip{
      padding:9px 12px;border-radius:999px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(15,23,54,.45);
      color: var(--txt);
      font-size:14px;cursor:pointer;user-select:none;
      box-shadow: 0 10px 18px rgba(0,0,0,.14);
    }
    .chip[aria-pressed="true"]{
      background: rgba(40,225,255,.18);
      border-color: rgba(40,225,255,.45);
      font-weight:950;
    }

    .list{display:flex;flex-direction:column;gap:10px}
    .item{
      border:1px solid rgba(255,255,255,.12);
      border-radius:14px;
      background: rgba(7,10,18,.22);
      padding:12px;
    }
    .k{font-size:13px;color:var(--muted);margin-bottom:5px}
    .v{font-size:14px;line-height:1.45}

    .pill{
      display:inline-flex;align-items:center;gap:8px;
      padding:7px 10px;border-radius:999px;
      background: rgba(40,225,255,.14);
      border:1px solid rgba(40,225,255,.25);
      color: var(--txt);
      font-size:13px;
      font-weight:950;
    }

    .tagline{
      padding:12px 14px;border-radius:14px;
      border:1px solid rgba(40,225,255,.22);
      background: rgba(40,225,255,.10);
      color: var(--txt);
      font-size:14px;line-height:1.5;
    }

    /* evidence ui */
    .evrow{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-top:10px;}
    .sourceBadge{
      font-size:12px;padding:6px 10px;border-radius:999px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(7,10,18,.30);
      color: var(--muted);
      white-space:nowrap;
    }
    .sourceBadge strong{color:var(--txt)}
    .sourceBadge.high{border-color: rgba(52,211,153,.28); background: rgba(52,211,153,.10)}
    .sourceBadge.mod{border-color: rgba(251,191,36,.28); background: rgba(251,191,36,.08)}
    .sourceBadge.pre{border-color: rgba(251,113,133,.28); background: rgba(251,113,133,.08)}

    .evbtn{
      padding:9px 12px;border-radius:12px;
      font-size:14px;font-weight:900;
      background: rgba(167,139,250,.14);
      border:1px solid rgba(167,139,250,.25);
      cursor:pointer;user-select:none;
      display:inline-flex;align-items:center;gap:8px;
    }

    .evidence{
      margin-top:10px;
      padding:12px;border-radius:14px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(15,23,54,.40);
    }

    .citeList{display:flex;flex-direction:column;gap:8px;margin-top:10px}
    .cite{
      font-family: var(--mono);
      font-size:12.5px;
      color: rgba(234,240,255,.90);
      padding:8px 10px;
      border-radius:12px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(7,10,18,.30);
      width: fit-content;
      max-width: 100%;
      overflow-x:auto;
      text-decoration:none;
      display:inline-block;
    }
    a.cite:hover{filter:brightness(1.08)}

    .inlineCites{
      display:flex;gap:8px;flex-wrap:wrap;
      margin-top:8px;
    }
    .inlineCites .cite{
      padding:6px 8px;
      font-size:12px;
      opacity:.95;
    }

    .note{margin-top:10px;color: var(--muted);font-size:14px;line-height:1.5;}

    /* registry */
    .toolbar{display:flex;gap:10px;flex-wrap:wrap;align-items:center;justify-content:space-between}
    .lefttools{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
    .smallbtn{padding:9px 12px;font-size:13px;border-radius:12px}
    .countPill{
      display:inline-flex;align-items:center;gap:8px;
      padding:7px 10px;border-radius:999px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(7,10,18,.30);
      color: var(--muted);
      font-size:13px;
      white-space:nowrap;
    }
    .countPill strong{color:var(--txt)}
    .groupTitle{margin:14px 0 8px 0;font-size:13px;color:var(--muted)}
    .grid2{display:grid;grid-template-columns:1fr;gap:10px}

    /* summary improvements */
    .quickActions{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}
    .qaBtn{padding:9px 12px;font-size:13px;border-radius:12px}

    /* supplement tiers */
    .tierPill{
      display:inline-flex;align-items:center;gap:8px;
      padding:6px 10px;border-radius:999px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(7,10,18,.30);
      color: var(--muted);
      font-size:12.5px;
      white-space:nowrap;
    }
    .tierHigh{border-color: rgba(52,211,153,.30); background: rgba(52,211,153,.10)}
    .tierMod{border-color: rgba(251,191,36,.30); background: rgba(251,191,36,.08)}
    .tierLow{border-color: rgba(148,163,184,.28); background: rgba(148,163,184,.07)}

    /* contact box */
    .contactBox{
      border:1px solid rgba(255,255,255,.12);
      border-radius:16px;
      background: rgba(7,10,18,.24);
      padding:14px;
    }
    .mailto{
      color: var(--txt);
      text-decoration:none;
      border-bottom:1px dashed rgba(234,240,255,.55);
    }
    .mailto:hover{filter:brightness(1.08)}
  </style>
</head>

<body>
  <div class="wrap">
    <div class="top">
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div>
          <h1>Geneomx — Medication Completion Infrastructure (V1)</h1>
          <p class="sub">Consumer Portal V1 • functional check-ins + feedback capture • evidence + clickable citations</p>
        </div>
      </div>
      <div class="status">
        <div class="badge">User: <strong id="pillUser">Guest</strong></div>
        <div class="badge">Plan: <strong id="pillPlan">Not started</strong></div>
        <div class="badge">Check-ins: <strong id="pillChecks">0</strong></div>
      </div>
    </div>

    <div class="grid">
      <!-- MAIN -->
      <div class="card">
        <div class="hd">
          <div>
            <h2 id="mainTitle">Account</h2>
            <div class="desc" id="mainSub">Enter basic details to begin.</div>
          </div>
          <div class="steps" id="steps"></div>
        </div>
        <div class="bd" id="main"></div>
      </div>

      <!-- SIDE -->
      <div class="card">
        <div class="hd">
          <div>
            <h2>Summary</h2>
            <div class="desc">What you’ve entered so far</div>
          </div>
          <div>
            <button class="ghost" id="btnReset">Reset</button>
          </div>
        </div>
        <div class="bd">
          <div class="section" id="summaryTop"></div>
          <div style="height:14px"></div>
          <div class="list" id="side"></div>
          <div style="height:14px"></div>
          <div class="contactBox" id="contactBox"></div>
        </div>
      </div>
    </div>
  </div>

<script>
/* ===========================
   MED DATABASE (sample set)
   NOTE: Replace/expand with top 25 meds + full claim sets
   =========================== */
const MED_DB = [
  { id:"atorvastatin", name:"Atorvastatin (statin)", symptomChips:["Muscle aches","Fatigue","Brain fog","Sleep changes"],
    claims:[{ nutrient:"CoQ10", source_quality:"High", citations:["PMID:26192349"],
      notes:["Statins are associated with lower plasma CoQ10; symptom benefit from supplementation varies."]}]},

  { id:"metformin", name:"Metformin", symptomChips:["Fatigue","Tingling hands/feet","Brain fog","Low mood","GI discomfort"],
    claims:[{ nutrient:"Vitamin B12", source_quality:"High", citations:["PMID:26900641"],
      notes:["Long-term metformin is associated with B12 deficiency risk; consider monitoring if symptoms present."]}]},

  { id:"omeprazole", name:"Omeprazole (PPI)", symptomChips:["GI discomfort","Fatigue","Dizziness","Muscle cramps","Brain fog"],
    claims:[
      { nutrient:"Magnesium", source_quality:"High", citations:["FDA:PPI-Mg-2011"],
        notes:["Long-term PPI use has a hypomagnesemia warning signal; consider Mg evaluation if symptoms/risk factors."]},
      { nutrient:"Vitamin B12", source_quality:"Moderate", citations:["PMID:37060552","PMCID:PMC4110863"],
        notes:["Association depends on duration and population; labs help clarify."]},
    ]},

  { id:"hydrochlorothiazide", name:"Hydrochlorothiazide (thiazide diuretic)", symptomChips:["Muscle cramps","Dizziness","Fatigue","Heart palpitations"],
    claims:[
      { nutrient:"Potassium", source_quality:"High", citations:["PMID:3551599"],
        notes:["Diuretics can increase urinary potassium loss; consider electrolytes if symptomatic."]},
      { nutrient:"Magnesium", source_quality:"High", citations:["PMID:3551599"],
        notes:["Magnesium loss may occur alongside potassium shifts."]},
    ]},

  { id:"prednisone", name:"Prednisone (corticosteroid)", symptomChips:["Mood changes","Sleep changes","Muscle weakness","Bone/joint discomfort"],
    claims:[
      { nutrient:"Calcium", source_quality:"High", citations:["PMCID:PMC7046131"],
        notes:["Often used for steroid-induced bone loss prevention (not a ‘depletion’ claim)."]},
      { nutrient:"Vitamin D", source_quality:"High", citations:["PMCID:PMC7046131"],
        notes:["Commonly paired with calcium for bone protection in chronic steroid exposure."]},
    ]},

  // placeholders (no claims yet)
  { id:"lisinopril", name:"Lisinopril (ACE inhibitor)", symptomChips:["Dizziness","Fatigue"], claims:[] },
  { id:"sertraline", name:"Sertraline (SSRI)", symptomChips:["Mood changes","Sleep changes","Brain fog"], claims:[] },
  { id:"levothyroxine", name:"Levothyroxine", symptomChips:["Fatigue","Brain fog","Mood changes"], claims:[] },
];

const GENERIC_SYMPTOMS = [
  "Fatigue","Low energy","Brain fog","Poor focus","Mood changes","Sleep changes",
  "GI discomfort","Constipation","Dizziness","Headache","Muscle cramps","Tingling hands/feet",
  "Heart palpitations","Easy bruising"
];

const SUPPLEMENT_MAP = {
  "CoQ10": ["CoQ10 (ubiquinol)"],
  "Vitamin D": ["Vitamin D3 (consider K2)"],
  "Vitamin B12": ["Methyl B12"],
  "Magnesium": ["Magnesium glycinate"],
  "Potassium": ["Electrolytes / potassium foods"],
  "Calcium": ["Calcium + bone support"],
  "B vitamins": ["B-complex (methylated)"],
};

/* ===========================
   STATE
   =========================== */
const STORAGE_KEY = "cpv1_state_v1_3";
const defaultState = () => ({
  step: 0,
  account: { email:"", consent:false },
  profile: { age:"", gender:"", pregnant:false },
  meds: [], // {medId, dose, durationMonths}
  symptoms: { selected:[], severity:"mild" },
  wellbeingBaseline: { energy:5, mood:5, sleep:5, focus:5, notes:"" },
  plan: { started:false, startDate:null, recommendedSupplements:[] },
  checkins: [], // {dateISO, adherencePct, supplementsTaken:[], wellbeing:{}, symptoms:{items:[]}, sideEffects:[], notes:""}
  feedback: []  // {dateISO, type, message, canContact, email}
});

let state = load();

function save(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); renderAll(); }
function load(){
  try{ const raw = localStorage.getItem(STORAGE_KEY); return raw ? JSON.parse(raw) : defaultState(); }
  catch(e){ return defaultState(); }
}
function resetDemo(){ localStorage.removeItem(STORAGE_KEY); state = defaultState(); renderAll(); }

function clamp(n,min,max){ return Math.max(min, Math.min(max, n)); }
function uniq(arr){ return [...new Set(arr)]; }
function escapeHtml(s){
  return String(s||"")
    .replaceAll("&","&amp;").replaceAll("<","&lt;")
    .replaceAll(">","&gt;")
    .replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}
function fmtDate(iso){
  if(!iso) return "";
  const d = new Date(iso);
  return d.toLocaleDateString(undefined, {year:"numeric",month:"short",day:"numeric"});
}

/* ===========================
   Citations -> Clickable Links
   =========================== */
function citationToLink(token){
  const t = String(token||"").trim();
  if(/^PMID:\d+$/i.test(t)){
    const id = t.split(":")[1];
    return `https://pubmed.ncbi.nlm.nih.gov/${id}/`;
  }
  if(/^PMCID:PMC\d+$/i.test(t)){
    const id = t.split(":")[1].toUpperCase(); // PMC####
    return `https://pmc.ncbi.nlm.nih.gov/articles/${id}/`;
  }
  return "";
}
function renderCitationChip(token){
  const url = citationToLink(token);
  const safeTok = escapeHtml(token);
  if(url){
    return `<a class="cite" href="${url}" target="_blank" rel="noopener noreferrer">${safeTok}</a>`;
  }
  return `<span class="cite">${safeTok}</span>`;
}

/* ===========================
   Scoring (kept simple)
   =========================== */
function doseFactor(d){ return d==="low" ? 0.85 : (d==="high" ? 1.25 : 1.0); }
function durationFactor(months){ const m = clamp(months||0, 0, 24); return 0.55 + (m/24)*0.75; }
function severityFactor(sev){ return sev==="severe" ? 1.35 : (sev==="moderate" ? 1.15 : 1.0); }
function qualityWeight(q){ return q==="High" ? 4 : (q==="Moderate" ? 3 : 2); }

function computeNutrientScores(){
  const scores = {};
  const sevF = severityFactor(state.symptoms.severity);

  for(const mi of state.meds){
    const med = MED_DB.find(x => x.id===mi.medId);
    if(!med) continue;

    const f = doseFactor(mi.dose) * durationFactor(mi.durationMonths) * sevF;

    for(const cl of (med.claims||[])){
      const w = qualityWeight(cl.source_quality) * 10 * f;
      scores[cl.nutrient] = (scores[cl.nutrient]||0) + w;
    }
  }

  if(Object.keys(scores).length===0 && state.symptoms.selected.length){
    const burden = state.symptoms.selected.length * 9 * sevF;
    scores["Magnesium"] = (scores["Magnesium"]||0) + burden;
    scores["B vitamins"] = (scores["B vitamins"]||0) + burden * 0.85;
    scores["Vitamin D"] = (scores["Vitamin D"]||0) + burden * 0.60;
  }

  return Object.entries(scores)
    .map(([k,v]) => [k, clamp(Math.round(v), 0, 100)])
    .sort((a,b)=>b[1]-a[1]);
}

function tierFromScore(score){
  if(score >= 70) return "High";
  if(score >= 45) return "Moderate";
  return "Low";
}

/* Recommend supplements for Low/Moderate as well */
function recommendSupplements(nutrientScores){
  const out = []; // {nutrient, tier, supplement, score}
  for(const [nut, score] of nutrientScores.slice(0,10)){
    const tier = tierFromScore(score);
    const sups = (SUPPLEMENT_MAP[nut] || []);
    for(const s of sups){
      out.push({ nutrient: nut, tier, supplement: s, score });
    }
  }

  const rank = { High:3, Moderate:2, Low:1 };
  const best = new Map();
  for(const item of out){
    const prev = best.get(item.supplement);
    if(!prev || rank[item.tier] > rank[prev.tier]) best.set(item.supplement, item);
  }

  return [...best.values()].sort((a,b)=>{
    if(rank[b.tier] !== rank[a.tier]) return rank[b.tier]-rank[a.tier];
    return (b.score||0) - (a.score||0);
  }).slice(0,10);
}

function getSymptomUniverse(){
  if(state.meds.length){
    const chips = [];
    state.meds.forEach(mi=>{
      const med = MED_DB.find(x=>x.id===mi.medId);
      if(med) chips.push(...med.symptomChips);
    });
    return uniq(chips).slice(0,24);
  }
  return GENERIC_SYMPTOMS;
}

/* ===========================
   Evidence aggregation
   =========================== */
function claimsForSelectedMeds(){
  const out = [];
  for(const mi of state.meds){
    const med = MED_DB.find(x => x.id===mi.medId);
    if(!med) continue;
    for(const cl of (med.claims||[])){
      out.push({ medId: med.id, medName: med.name, ...cl });
    }
  }
  return out;
}
function aggregateEvidenceByNutrient(claims){
  const map = {};
  for(const cl of claims){
    if(!map[cl.nutrient]) map[cl.nutrient] = [];
    map[cl.nutrient].push(cl);
  }
  return map;
}
function summarizeSourceQuality(claims){
  const qs = (claims||[]).map(c=>c.source_quality).filter(Boolean);
  if(qs.includes("High")) return "High";
  if(qs.includes("Moderate")) return "Moderate";
  if(qs.includes("Preliminary")) return "Preliminary";
  return "Pending";
}
function badgeClass(q){ return q==="High" ? "high" : (q==="Moderate" ? "mod" : "pre"); }

function renderEvidencePanel(nutrient, claims){
  if(!claims || !claims.length){
    return `<div class="fineprint">Evidence for this relationship is not loaded yet for your selected medications.</div>`;
  }

  const seen = new Set();
  const citations = [];
  const notes = [];

  for(const cl of claims){
    (cl.citations||[]).forEach(id=>{
      const key = String(id||"").trim();
      if(!key || seen.has(key)) return;
      seen.add(key);
      citations.push(key);
    });
    if(cl.notes && String(cl.notes).trim()) notes.push(String(cl.notes).trim());
  }

  const noteText = uniq(notes).slice(0,3).join(" ");
  const citeHtml = citations.slice(0,6).map(id => renderCitationChip(id)).join("");

  return `
    <div class="fineprint">Citations (click to open):</div>
    <div class="citeList">${citeHtml || `<div class="fineprint">No citations attached yet.</div>`}</div>
    ${noteText ? `<div class="note"><strong>Notes:</strong> ${escapeHtml(noteText)}</div>` : ``}
  `;
}

/* ===========================
   Citations Registry
   =========================== */
function buildCitationsRegistry(){
  const claims = claimsForSelectedMeds();
  const seen = new Set();
  const all = [];
  for(const cl of claims){
    for(const id of (cl.citations||[])){
      const tok = String(id||"").trim();
      if(!tok || seen.has(tok)) continue;
      seen.add(tok);
      all.push(tok);
    }
  }

  const pmid=[], pmcid=[], fda=[], other=[];
  all.forEach(tok=>{
    if(/^PMID:\d+$/i.test(tok)) pmid.push(tok.toUpperCase());
    else if(/^PMCID:PMC\d+$/i.test(tok)) pmcid.push(tok.toUpperCase());
    else if(/^FDA:/i.test(tok)) fda.push(tok);
    else other.push(tok);
  });

  pmid.sort(); pmcid.sort(); fda.sort(); other.sort();
  return { all, pmid, pmcid, fda, other };
}
function coverageStats(){
  const selected = state.meds.map(m=>m.medId);
  const withEvidence = selected.filter(id=>{
    const med = MED_DB.find(x=>x.id===id);
    return med && (med.claims||[]).some(c => (c.citations||[]).length>0);
  });
  return { selectedCount: selected.length, evidenceCount: withEvidence.length };
}

/* ===========================
   FEEDBACK (mailto + local log)
   =========================== */
function sendFeedbackEmail({type, message, canContact, email}){
  const subj = `Geneomx Portal Feedback (${type})`;
  const bodyLines = [
    `Type: ${type}`,
    `From: ${email || "anonymous"}`,
    `Can we contact you?: ${canContact ? "Yes" : "No"}`,
    ``,
    `Message:`,
    message || ""
  ];
  const body = encodeURIComponent(bodyLines.join("\n"));
  const subject = encodeURIComponent(subj);
  const to = "info@geneomx.com";
  window.location.href = `mailto:${to}?subject=${subject}&body=${body}`;
}

/* ===========================
   UI plumbing
   =========================== */
const mainEl = document.getElementById("main");
const sideEl = document.getElementById("side");
const stepsEl = document.getElementById("steps");
const pillUser = document.getElementById("pillUser");
const pillPlan = document.getElementById("pillPlan");
const pillChecks = document.getElementById("pillChecks");
const mainTitle = document.getElementById("mainTitle");
const mainSub = document.getElementById("mainSub");
const summaryTop = document.getElementById("summaryTop");
const contactBox = document.getElementById("contactBox");

document.getElementById("btnReset").addEventListener("click", resetDemo);

/* Added "Feedback" tab as last */
const STEP_LABELS = ["Account","Medications","Symptoms","Wellbeing","Results","Check-in","Progress","Citations","Feedback"];

function setStep(n){
  state.step = clamp(n, 0, STEP_LABELS.length-1);
  save();
}

function renderSteps(){
  const colors = ["c1","c2","c3","c4","c5","c6","c7","c8","c9"];
  stepsEl.innerHTML = "";
  STEP_LABELS.forEach((lbl,i)=>{
    const s = document.createElement("div");
    s.className = `step ${colors[i]} ${i===state.step ? "on":""}`;
    s.textContent = lbl;
    s.addEventListener("click", ()=> setStep(i));
    stepsEl.appendChild(s);
  });
}

function renderPills(){
  pillUser.textContent = state.account.email ? state.account.email : "Guest";
  pillPlan.textContent = state.plan.started ? `Started ${fmtDate(state.plan.startDate)}` : "Not started";
  pillChecks.textContent = String(state.checkins.length);
}

function renderContactBox(){
  contactBox.innerHTML = `
    <div class="k">Your feedback is valuable</div>
    <div class="v">
      Found something confusing? Want to suggest an improvement?
      Email us at <a class="mailto" href="mailto:info@geneomx.com">info@geneomx.com</a>.
    </div>
    <div class="fineprint" style="margin-top:10px">
      You can also use the Feedback tab to send structured notes.
    </div>
  `;
}

function renderSummaryTop(){
  const medsCount = state.meds.length;
  const symCount = state.symptoms.selected.length;
  const cov = coverageStats();

  const next =
    !state.account.consent ? "Complete Account"
    : medsCount===0 ? "Add Medications"
    : symCount===0 ? "Select Symptoms"
    : !state.plan.started ? "Review Results"
    : "Log a Check-in";

  const demoLine = (state.profile.age || state.profile.gender)
    ? `Age: <strong>${escapeHtml(state.profile.age||"—")}</strong> • Gender: <strong>${escapeHtml(state.profile.gender||"—")}</strong>`
    : `Age: <strong>—</strong> • Gender: <strong>—</strong>`;

  summaryTop.innerHTML = `
    <div class="tagline">
      <strong>Quick status</strong><br>
      ${demoLine}<br>
      Medications: <strong>${medsCount}</strong> • Symptoms: <strong>${symCount}</strong> • Evidence coverage: <strong>${cov.evidenceCount}/${cov.selectedCount}</strong>
      <div class="fineprint" style="margin-top:8px">
        Next suggested step: <strong>${escapeHtml(next)}</strong>
      </div>
      <div class="quickActions">
        <button class="qaBtn ghost" data-go="0">Account</button>
        <button class="qaBtn ghost" data-go="1">Medications</button>
        <button class="qaBtn ghost" data-go="2">Symptoms</button>
        <button class="qaBtn ghost" data-go="4">Results</button>
        <button class="qaBtn ghost" data-go="5">Check-in</button>
        <button class="qaBtn ghost" data-go="8">Feedback</button>
      </div>
    </div>
  `;
  summaryTop.querySelectorAll("[data-go]").forEach(b=>{
    b.addEventListener("click", ()=> setStep(parseInt(b.getAttribute("data-go"),10)));
  });
}

function renderSide(){
  const meds = state.meds.map(m=>{
    const med = MED_DB.find(x=>x.id===m.medId);
    return med ? med.name : m.medId;
  });

  sideEl.innerHTML = "";

  const lastCheck = state.checkins.length ? state.checkins[state.checkins.length-1] : null;
  const lastCheckLine = lastCheck
    ? `Latest: ${fmtDate(lastCheck.dateISO)} • Adherence ${lastCheck.adherencePct}%`
    : "No check-ins yet.";

  const blocks = [
    {k:"Account", v: `${state.account.email ? state.account.email : "Guest"} • Consent: ${state.account.consent ? "Yes" : "No"}`},
    {k:"Age / Gender", v: `${state.profile.age || "—"} / ${state.profile.gender || "—"}`},
    {k:"Medications", v: meds.length ? meds.join(", ") : "None yet — add at least 1 to personalize recommendations."},
    {k:"Symptoms selected", v: state.symptoms.selected.length ? state.symptoms.selected.join(", ") : "None yet — symptoms help refine suggestions."},
    {k:"Baseline wellbeing", v: `Energy ${state.wellbeingBaseline.energy}/10 • Mood ${state.wellbeingBaseline.mood}/10 • Sleep ${state.wellbeingBaseline.sleep}/10 • Focus ${state.wellbeingBaseline.focus}/10`},
    {k:"Plan", v: state.plan.started ? `Started ${fmtDate(state.plan.startDate)}` : "Not started yet — start after reviewing Results."},
    {k:"Supplements", v: state.plan.recommendedSupplements.length ? state.plan.recommendedSupplements.join(", ") : "No active plan supplements yet."},
    {k:"Check-ins", v: lastCheckLine},
  ];

  blocks.forEach(x=>{
    const div = document.createElement("div");
    div.className = "item";
    div.innerHTML = `<div class="k">${x.k}</div><div class="v">${escapeHtml(x.v)}</div>`;
    sideEl.appendChild(div);
  });
}

function navButtons(prev=true,next=true,nextLabel="Continue"){
  const wrap = document.createElement("div");
  wrap.className = "btns";
  if(prev){
    const b = document.createElement("button");
    b.textContent = "Back";
    b.className = "ghost";
    b.addEventListener("click", ()=> setStep(state.step-1));
    wrap.appendChild(b);
  }
  if(next){
    const b = document.createElement("button");
    b.textContent = nextLabel;
    b.className = "primary";
    b.addEventListener("click", ()=> setStep(state.step+1));
    wrap.appendChild(b);
  }
  return wrap;
}

function renderMain(){
  mainEl.innerHTML = "";
  mainTitle.textContent = STEP_LABELS[state.step];

  const subMap = {
    "Account":"Set basics + consent.",
    "Medications":"Add meds so recommendations are personalized.",
    "Symptoms":"Pick symptoms and severity.",
    "Wellbeing":"Set baseline to track improvement over time.",
    "Results":"Nutrient signals + citations; start plan if ready.",
    "Check-in":"Log symptoms + adherence + wellbeing (functional).",
    "Progress":"Compare baseline vs latest check-in (text).",
    "Citations":"All sources referenced in your session.",
    "Feedback":"Send feedback/questions to Geneomx."
  };
  mainSub.textContent = subMap[STEP_LABELS[state.step]] || "";

  if(state.step===0) return renderAccount();
  if(state.step===1) return renderMeds();
  if(state.step===2) return renderSymptoms();
  if(state.step===3) return renderWellbeing();
  if(state.step===4) return renderResults();
  if(state.step===5) return renderCheckin();
  if(state.step===6) return renderProgress();
  if(state.step===7) return renderCitations();
  if(state.step===8) return renderFeedback();
}

/* ===== STEP 0 ===== */
function renderAccount(){
  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="tagline">
      <strong>Welcome</strong> — enter your details to begin a personalized supplement companion experience.
    </div>

    <div style="height:12px"></div>

    <div class="row">
      <div class="col">
        <label>Email</label>
        <input id="email" placeholder="name@email.com" value="${escapeHtml(state.account.email||"")}" />
      </div>
      <div class="col">
        <label>Consent</label>
        <select id="consent">
          <option value="no" ${state.account.consent? "": "selected"}>Not yet</option>
          <option value="yes" ${state.account.consent? "selected": ""}>I agree</option>
        </select>
      </div>
    </div>

    <div style="height:12px"></div>

    <div class="row">
      <div class="col">
        <label>Age</label>
        <input id="age" type="number" min="0" max="120" placeholder="e.g., 42" value="${escapeHtml(state.profile.age || "")}" />
      </div>
      <div class="col">
        <label>Gender</label>
        <select id="gender">
          <option value="">Select…</option>
          <option value="Female" ${state.profile.gender==="Female"?"selected":""}>Female</option>
          <option value="Male" ${state.profile.gender==="Male"?"selected":""}>Male</option>
          <option value="Non-binary" ${state.profile.gender==="Non-binary"?"selected":""}>Non-binary</option>
          <option value="Prefer not to say" ${state.profile.gender==="Prefer not to say"?"selected":""}>Prefer not to say</option>
        </select>
      </div>
      <div class="col">
        <label>Pregnant / breastfeeding</label>
        <select id="preg">
          <option value="no" ${!state.profile.pregnant?"selected":""}>No</option>
          <option value="yes" ${state.profile.pregnant?"selected":""}>Yes</option>
        </select>
      </div>
    </div>

    <div class="fineprint" style="margin-top:10px">
      Privacy note: This prototype stores data in your browser only. Production will use secure accounts + encrypted storage.
    </div>
  `;

  const nav = navButtons(false,true,"Continue");
  nav.querySelector(".primary").addEventListener("click", ()=>{
    state.account.email = document.getElementById("email").value.trim();
    state.account.consent = document.getElementById("consent").value==="yes";
    const ageVal = parseInt(document.getElementById("age").value || "", 10);
    state.profile.age = Number.isFinite(ageVal) ? String(ageVal) : "";
    state.profile.gender = document.getElementById("gender").value || "";
    state.profile.pregnant = document.getElementById("preg").value==="yes";
    save();
    setStep(1);
  });

  mainEl.appendChild(s1);
  mainEl.appendChild(nav);
}

/* ===== STEP 1 ===== */
function renderMeds(){
  const s1 = document.createElement("div");
  s1.className="section";

  const medOptions = MED_DB.slice().sort((a,b)=>a.name.localeCompare(b.name))
    .map(m=>`<option value="${m.id}">${escapeHtml(m.name)}</option>`).join("");

  s1.innerHTML = `
    <div class="row">
      <div class="col">
        <label>Medication</label>
        <select id="medPick">
          <option value="">Select…</option>
          ${medOptions}
        </select>
      </div>
      <div class="col">
        <label>Dose</label>
        <select id="dosePick">
          <option value="low">Low</option>
          <option value="medium" selected>Medium</option>
          <option value="high">High</option>
        </select>
      </div>
      <div class="col">
        <label>Duration (months)</label>
        <input id="durPick" type="number" min="0" max="360" placeholder="e.g., 18" value="12" />
      </div>
    </div>

    <div class="btns">
      <button class="primary" id="btnAddMed">Add medication</button>
      <button class="ghost" id="btnNoMeds">No medications</button>
    </div>

    <div class="fineprint" style="margin-top:10px">
      Tip: If you select a medication and forget to click “Add”, hitting “Continue” will add it automatically.
    </div>
  `;
  mainEl.appendChild(s1);

  const s2 = document.createElement("div");
  s2.className="section";
  s2.innerHTML = `<div class="list" id="medList"></div>`;
  mainEl.appendChild(s2);

  const medList = s2.querySelector("#medList");

  function drawList(){
    medList.innerHTML = "";
    if(!state.meds.length){
      medList.innerHTML = `<div class="fineprint">No medications added yet.</div>`;
      return;
    }
    state.meds.forEach((m,idx)=>{
      const med = MED_DB.find(x=>x.id===m.medId);
      const div = document.createElement("div");
      div.className="item";
      div.innerHTML = `
        <div class="k">${escapeHtml(med?med.name:m.medId)}</div>
        <div class="v">Dose: <strong>${m.dose}</strong> • Duration: <strong>${m.durationMonths||0} months</strong></div>
        <div class="btns">
          <button class="danger" data-del="${idx}">Remove</button>
        </div>
      `;
      div.querySelector("[data-del]").addEventListener("click", ()=>{
        state.meds.splice(idx,1);
        save();
        drawList();
      });
      medList.appendChild(div);
    });
  }
  drawList();

  function addFromPickerIfValid(){
    const medId = s1.querySelector("#medPick").value;
    if(!medId) return false;

    if(state.meds.some(x => x.medId === medId)) return true;

    const dose = s1.querySelector("#dosePick").value;
    const dur = parseInt(s1.querySelector("#durPick").value||"0",10);
    state.meds.push({medId, dose, durationMonths: clamp(isNaN(dur)?0:dur, 0, 360)});
    return true;
  }

  s1.querySelector("#btnAddMed").addEventListener("click", ()=>{
    const ok = addFromPickerIfValid();
    if(!ok) return alert("Please select a medication first.");
    save(); drawList();
  });

  s1.querySelector("#btnNoMeds").addEventListener("click", ()=>{
    state.meds = [];
    save();
    setStep(2);
  });

  const nav = navButtons(true,true,"Continue");
  nav.querySelector(".primary").addEventListener("click", ()=>{
    addFromPickerIfValid(); // auto-add fix
    save();
    setStep(2);
  });

  mainEl.appendChild(nav);
}

/* ===== STEP 2 ===== */
function renderSymptoms(){
  const universe = getSymptomUniverse();
  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="row">
      <div class="col" style="min-width:360px">
        <label>Select symptoms</label>
        <div class="fineprint">Choose what you’ve noticed recently (we’ll use this to personalize results).</div>
        <div class="chips" id="chips"></div>
        <div class="btns">
          <button class="ghost" id="clear">Clear</button>
        </div>
      </div>

      <div class="col" style="max-width:320px">
        <label>Severity</label>
        <select id="sevSel">
          <option value="mild" ${state.symptoms.severity==="mild"?"selected":""}>Mild</option>
          <option value="moderate" ${state.symptoms.severity==="moderate"?"selected":""}>Moderate</option>
          <option value="severe" ${state.symptoms.severity==="severe"?"selected":""}>Severe</option>
        </select>
      </div>
    </div>
  `;
  mainEl.appendChild(s1);

  const chipsEl = s1.querySelector("#chips");
  function drawChips(){
    chipsEl.innerHTML = "";
    universe.forEach(sym=>{
      const c = document.createElement("div");
      c.className="chip";
      const on = state.symptoms.selected.includes(sym);
      c.setAttribute("aria-pressed", on ? "true":"false");
      c.textContent = sym;
      c.addEventListener("click", ()=>{
        const i = state.symptoms.selected.indexOf(sym);
        if(i>=0) state.symptoms.selected.splice(i,1);
        else state.symptoms.selected.push(sym);
        save(); drawChips();
      });
      chipsEl.appendChild(c);
    });
  }
  drawChips();

  s1.querySelector("#clear").addEventListener("click", ()=>{
    state.symptoms.selected = [];
    save(); drawChips();
  });

  const nav = navButtons(true,true,"Continue");
  nav.querySelector(".primary").addEventListener("click", ()=>{
    state.symptoms.severity = s1.querySelector("#sevSel").value;
    save();
    setStep(3);
  });
  mainEl.appendChild(nav);
}

/* ===== STEP 3 ===== */
function renderWellbeing(){
  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="fineprint">This baseline lets the platform measure improvement over time.</div>
    <div style="height:10px"></div>

    <div class="row">
      <div class="col">
        <label>Energy (0–10)</label>
        <input id="energy" type="number" min="0" max="10" value="${state.wellbeingBaseline.energy}" />
      </div>
      <div class="col">
        <label>Mood (0–10)</label>
        <input id="mood" type="number" min="0" max="10" value="${state.wellbeingBaseline.mood}" />
      </div>
      <div class="col">
        <label>Sleep (0–10)</label>
        <input id="sleep" type="number" min="0" max="10" value="${state.wellbeingBaseline.sleep}" />
      </div>
      <div class="col">
        <label>Focus (0–10)</label>
        <input id="focus" type="number" min="0" max="10" value="${state.wellbeingBaseline.focus}" />
      </div>
    </div>
  `;
  mainEl.appendChild(s1);

  const nav = navButtons(true,true,"Continue");
  nav.querySelector(".primary").addEventListener("click", ()=>{
    state.wellbeingBaseline.energy = clamp(parseInt(s1.querySelector("#energy").value||"0",10),0,10);
    state.wellbeingBaseline.mood = clamp(parseInt(s1.querySelector("#mood").value||"0",10),0,10);
    state.wellbeingBaseline.sleep = clamp(parseInt(s1.querySelector("#sleep").value||"0",10),0,10);
    state.wellbeingBaseline.focus = clamp(parseInt(s1.querySelector("#focus").value||"0",10),0,10);
    save();
    setStep(4);
  });
  mainEl.appendChild(nav);
}

/* ===== STEP 4 ===== */
function renderResults(){
  const scores = computeNutrientScores();
  const rec = recommendSupplements(scores);

  const claims = claimsForSelectedMeds();
  const evByNut = aggregateEvidenceByNutrient(claims);

  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="tagline">
      <strong>Your Results</strong><br>
      We estimate nutrient support needs based on your medications (evidence-linked) and symptom selections.
      <div class="fineprint" style="margin-top:8px">
        Citations are clickable (PMID/PMCID) so users can verify sources.
      </div>
    </div>
  `;
  mainEl.appendChild(s1);

  const s2 = document.createElement("div");
  s2.className="section";

  function topInlineCites(nutrient){
    const claimsForNut = evByNut[nutrient] || [];
    const seen = new Set();
    const cites = [];
    for(const c of claimsForNut){
      for(const id of (c.citations||[])){
        const t = String(id||"").trim();
        if(!t || seen.has(t)) continue;
        seen.add(t);
        cites.push(t);
      }
    }
    const top = cites.slice(0,2);
    if(!top.length) return `<div class="fineprint">Citations: Not loaded yet for this nutrient.</div>`;
    return `
      <div class="fineprint">Citations:</div>
      <div class="inlineCites">${top.map(x=>renderCitationChip(x)).join("")}</div>
    `;
  }

  let nutrientHtml = "";
  if(!scores.length){
    nutrientHtml = `
      <div class="fineprint">
        No nutrient signals yet. To generate results:
        <strong>(1)</strong> add at least one medication, or <strong>(2)</strong> select symptoms.
      </div>
    `;
  } else {
    nutrientHtml = scores.slice(0,10).map(([n,score], idx)=>{
      const label = tierFromScore(score);
      const claimsForNut = evByNut[n] || [];
      const q = claimsForNut.length ? summarizeSourceQuality(claimsForNut) : "Pending";
      const evId = `ev_${idx}`;
      const badge =
        q==="Pending"
          ? `<div class="sourceBadge pre"><strong>Source quality:</strong> Pending</div>`
          : `<div class="sourceBadge ${badgeClass(q)}"><strong>Source quality:</strong> ${escapeHtml(q)}</div>`;

      return `
        <div class="item">
          <div class="k">${escapeHtml(n)}</div>
          <div class="v"><strong>${escapeHtml(label)}</strong> signal (${score}%)</div>
          ${topInlineCites(n)}
          <div class="evrow">
            ${badge}
            <div class="evbtn" data-evbtn="${evId}">Evidence ▾</div>
          </div>
          <div class="evidence" id="${evId}" style="display:none">
            ${renderEvidencePanel(n, claimsForNut)}
          </div>
        </div>
      `;
    }).join("");
  }

  const tierClass = (tier) => tier==="High" ? "tierHigh" : (tier==="Moderate" ? "tierMod" : "tierLow");

  const supplementsHtml = rec.length
    ? `<div class="list">
        ${rec.map(r => `
          <div class="item">
            <div class="k">${escapeHtml(r.supplement)}</div>
            <div class="v">
              <span class="tierPill ${tierClass(r.tier)}">Tier: <strong style="color:var(--txt)">${escapeHtml(r.tier)}</strong></span>
              <span style="color: var(--muted)"> • driven by ${escapeHtml(r.nutrient)} (${r.score}%)</span>
            </div>
          </div>
        `).join("")}
      </div>
      <div class="fineprint" style="margin-top:10px">
        “High” = strong signal • “Moderate” = supportive • “Low” = optional watch-list.
        If pregnant, on anticoagulants, have kidney disease, or under specialist care, confirm with your clinician.
      </div>`
    : `<div class="fineprint">
         No suggestions yet. Add medications and/or symptoms to generate signals.
       </div>`;

  s2.innerHTML = `
    <div class="row">
      <div class="col">
        <div class="pill">Nutrient signals</div>
        <div style="height:10px"></div>
        <div class="list">${nutrientHtml}</div>
      </div>

      <div class="col">
        <div class="pill" style="background: rgba(167,139,250,.14); border-color: rgba(167,139,250,.25);">Supplement suggestions</div>
        <div style="height:10px"></div>
        <div class="item">${supplementsHtml}</div>

        <div class="divider"></div>

        <div class="item">
          <div class="k">Start your plan</div>
          <div class="fineprint">Starting the plan saves the current supplement set so we can track outcomes over time.</div>
          <div style="height:10px"></div>
          <input id="startDate" type="date" />
          <div class="btns">
            <button class="primary" id="startPlanBtn">${state.plan.started ? "Update plan" : "Start plan"}</button>
          </div>
        </div>
      </div>
    </div>
  `;
  mainEl.appendChild(s2);

  // Evidence toggles
  s2.querySelectorAll("[data-evbtn]").forEach(btn=>{
    btn.addEventListener("click", ()=>{
      const id = btn.getAttribute("data-evbtn");
      const panel = document.getElementById(id);
      if(!panel) return;
      panel.style.display = (panel.style.display==="none") ? "block" : "none";
    });
  });

  // Plan start
  const sd = s2.querySelector("#startDate");
  const today = new Date().toISOString().slice(0,10);
  sd.value = state.plan.startDate ? state.plan.startDate.slice(0,10) : today;

  s2.querySelector("#startPlanBtn").addEventListener("click", ()=>{
    state.plan.started = true;
    state.plan.startDate = new Date((sd.value || today) + "T00:00:00").toISOString();
    state.plan.recommendedSupplements = rec.map(x => x.supplement); // lock in list
    save();
    alert("Plan saved.");
  });

  mainEl.appendChild(navButtons(true,true,"Continue"));
}

/* ===========================
   NEW: FUNCTIONAL CHECK-IN
   Captures symptom improvement + adherence + wellbeing
   =========================== */

function latestCheckin(){
  if(!state.checkins.length) return null;
  return state.checkins[state.checkins.length-1];
}

function renderCheckin(){
  const planSupps = state.plan.recommendedSupplements || [];
  const symptomUniverse = getSymptomUniverse(); // based on meds if present, else generic
  const baseSymptoms = state.symptoms.selected.length ? state.symptoms.selected : symptomUniverse.slice(0,12);

  const last = latestCheckin();

  const defaultAdh = last ? last.adherencePct : 70;
  const defaultWell = last ? last.wellbeing : { energy: state.wellbeingBaseline.energy, mood: state.wellbeingBaseline.mood, sleep: state.wellbeingBaseline.sleep, focus: state.wellbeingBaseline.focus };

  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="tagline">
      <strong>Weekly Check-in</strong><br>
      Log adherence + symptom improvement + overall wellbeing so the system can measure your journey.
    </div>

    <div style="height:12px"></div>

    <div class="row">
      <div class="col">
        <label>Check-in date</label>
        <input id="ciDate" type="date" />
      </div>
      <div class="col">
        <label>Adherence (approx % of recommended supplements taken)</label>
        <input id="ciAdh" type="number" min="0" max="100" value="${escapeHtml(String(defaultAdh))}" />
        <div class="fineprint" style="margin-top:6px">Example: 80% means you took most doses this week.</div>
      </div>
    </div>
  `;
  mainEl.appendChild(s1);

  const today = new Date().toISOString().slice(0,10);
  s1.querySelector("#ciDate").value = today;

  // Supplements taken
  const sSupp = document.createElement("div");
  sSupp.className="section";
  sSupp.innerHTML = `
    <div class="pill" style="background: rgba(167,139,250,.14); border-color: rgba(167,139,250,.25);">Supplements taken</div>
    <div class="fineprint" style="margin-top:8px">Select what you actually took this week (helps adherence accuracy).</div>
    <div class="chips" id="suppChips"></div>
    <div class="btns">
      <button class="ghost" id="suppAll">Select all</button>
      <button class="ghost" id="suppNone">Clear</button>
    </div>
  `;
  mainEl.appendChild(sSupp);

  const suppChips = sSupp.querySelector("#suppChips");
  let taken = last?.supplementsTaken?.length ? [...last.supplementsTaken] : [];

  function drawSuppChips(){
    suppChips.innerHTML = "";
    if(!planSupps.length){
      suppChips.innerHTML = `<div class="fineprint">No plan supplements saved yet. Start your plan on the Results tab first.</div>`;
      return;
    }
    planSupps.forEach(name=>{
      const c = document.createElement("div");
      c.className="chip";
      const on = taken.includes(name);
      c.setAttribute("aria-pressed", on ? "true":"false");
      c.textContent = name;
      c.addEventListener("click", ()=>{
        const i = taken.indexOf(name);
        if(i>=0) taken.splice(i,1); else taken.push(name);
        drawSuppChips();
      });
      suppChips.appendChild(c);
    });
  }
  drawSuppChips();

  sSupp.querySelector("#suppAll").addEventListener("click", ()=>{
    taken = [...planSupps];
    drawSuppChips();
  });
  sSupp.querySelector("#suppNone").addEventListener("click", ()=>{
    taken = [];
    drawSuppChips();
  });

  // Symptoms improvement (simple but powerful)
  const sSym = document.createElement("div");
  sSym.className="section";
  sSym.innerHTML = `
    <div class="pill">Symptom improvement</div>
    <div class="fineprint" style="margin-top:8px">
      For each symptom, rate how it changed this week compared to last week.
    </div>
    <div class="list" id="symList"></div>
    <div class="fineprint" style="margin-top:10px">
      Tip: If you didn’t have a symptom this week, choose “Not present”.
    </div>
  `;
  mainEl.appendChild(sSym);

  const symList = sSym.querySelector("#symList");

  const IMPACT = ["Worse","No change","Slightly better","Much better","Not present"];
  const impactValue = { "Worse":-2, "No change":0, "Slightly better":1, "Much better":2, "Not present":0 };

  function symRow(sym, idx){
    const row = document.createElement("div");
    row.className="item";
    row.innerHTML = `
      <div class="k">${escapeHtml(sym)}</div>
      <div class="row">
        <div class="col">
          <label>Change</label>
          <select data-sym="${escapeHtml(sym)}" id="symChange_${idx}">
            ${IMPACT.map(x=>`<option value="${x}">${x}</option>`).join("")}
          </select>
        </div>
        <div class="col">
          <label>Severity now (0–10)</label>
          <input type="number" min="0" max="10" value="5" id="symSev_${idx}" />
        </div>
      </div>
    `;
    return row;
  }

  const symBase = baseSymptoms.slice(0,10);
  symBase.forEach((sym, idx)=> symList.appendChild(symRow(sym, idx)));

  // Wellbeing now
  const sWell = document.createElement("div");
  sWell.className="section";
  sWell.innerHTML = `
    <div class="pill" style="background: rgba(40,225,255,.14); border-color: rgba(40,225,255,.25);">Wellbeing this week</div>
    <div style="height:10px"></div>

    <div class="row">
      <div class="col">
        <label>Energy (0–10)</label>
        <input id="ciEnergy" type="number" min="0" max="10" value="${escapeHtml(String(defaultWell.energy ?? 5))}" />
      </div>
      <div class="col">
        <label>Mood (0–10)</label>
        <input id="ciMood" type="number" min="0" max="10" value="${escapeHtml(String(defaultWell.mood ?? 5))}" />
      </div>
      <div class="col">
        <label>Sleep (0–10)</label>
        <input id="ciSleep" type="number" min="0" max="10" value="${escapeHtml(String(defaultWell.sleep ?? 5))}" />
      </div>
      <div class="col">
        <label>Focus (0–10)</label>
        <input id="ciFocus" type="number" min="0" max="10" value="${escapeHtml(String(defaultWell.focus ?? 5))}" />
      </div>
    </div>

    <div style="height:10px"></div>
    <div class="row">
      <div class="col">
        <label>Side effects (optional)</label>
        <input id="ciSide" placeholder="e.g., nausea, headache, constipation" />
      </div>
      <div class="col">
        <label>Notes (optional)</label>
        <input id="ciNotes" placeholder="Anything that might explain changes (travel, stress, illness, diet)..." />
      </div>
    </div>
  `;
  mainEl.appendChild(sWell);

  // Save check-in + simple computed summary
  const sSave = document.createElement("div");
  sSave.className="section";
  sSave.innerHTML = `
    <div class="btns">
      <button class="ghost" id="ciBack">Back to Results</button>
      <button class="primary" id="ciSave">Save check-in</button>
      <button class="ghost" id="ciExport">Export check-ins (JSON)</button>
      <button class="danger" id="ciDeleteLast">Delete last check-in</button>
    </div>
    <div class="fineprint" style="margin-top:10px">
      Export helps you share anonymized logs with your team while we’re in prototype mode.
    </div>
  `;
  mainEl.appendChild(sSave);

  sSave.querySelector("#ciBack").addEventListener("click", ()=> setStep(4));

  sSave.querySelector("#ciSave").addEventListener("click", ()=>{
    const dateISO = new Date((s1.querySelector("#ciDate").value || today) + "T00:00:00").toISOString();
    const adherencePct = clamp(parseInt(s1.querySelector("#ciAdh").value || "0", 10), 0, 100);

    // gather symptom ratings
    const items = [];
    symBase.forEach((sym, idx)=>{
      const change = document.getElementById(`symChange_${idx}`).value;
      const sevNow = clamp(parseInt(document.getElementById(`symSev_${idx}`).value || "0", 10), 0, 10);
      items.push({ symptom: sym, change, changeScore: impactValue[change] ?? 0, severityNow: sevNow });
    });

    const wellbeing = {
      energy: clamp(parseInt(document.getElementById("ciEnergy").value || "0", 10), 0, 10),
      mood: clamp(parseInt(document.getElementById("ciMood").value || "0", 10), 0, 10),
      sleep: clamp(parseInt(document.getElementById("ciSleep").value || "0", 10), 0, 10),
      focus: clamp(parseInt(document.getElementById("ciFocus").value || "0", 10), 0, 10),
    };

    const sideEffects = (document.getElementById("ciSide").value || "").split(",").map(s=>s.trim()).filter(Boolean);
    const notes = (document.getElementById("ciNotes").value || "").trim();

    // simple improvement score (for now): sum changeScore, normalized
    const improvementScore = items.reduce((acc,x)=>acc + (x.changeScore||0), 0);

    state.checkins.push({
      dateISO,
      adherencePct,
      supplementsTaken: [...taken],
      wellbeing,
      symptoms: { items, improvementScore },
      sideEffects,
      notes
    });

    save();
    alert("Check-in saved.");
    setStep(6); // jump to Progress after save
  });

  sSave.querySelector("#ciExport").addEventListener("click", ()=>{
    const blob = new Blob([JSON.stringify(state.checkins, null, 2)], {type:"application/json"});
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = "geneomx_checkins.json";
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(url);
  });

  sSave.querySelector("#ciDeleteLast").addEventListener("click", ()=>{
    if(!state.checkins.length) return alert("No check-ins to delete.");
    state.checkins.pop();
    save();
    alert("Deleted last check-in.");
    setStep(5);
  });

  mainEl.appendChild(navButtons(true,true,"Continue"));
}

/* ===== STEP 6 ===== */
function renderProgress(){
  const last = latestCheckin();
  const base = state.wellbeingBaseline;

  const s1 = document.createElement("div");
  s1.className="section";

  if(!last){
    s1.innerHTML = `
      <div class="tagline"><strong>Progress</strong><br>No check-ins yet. Log your first check-in to see trends.</div>
      <div class="btns"><button class="primary" onclick="setStep(5)">Go to Check-in</button></div>
    `;
    mainEl.appendChild(s1);
    mainEl.appendChild(navButtons(true,true,"Continue"));
    return;
  }

  const dEnergy = last.wellbeing.energy - base.energy;
  const dMood = last.wellbeing.mood - base.mood;
  const dSleep = last.wellbeing.sleep - base.sleep;
  const dFocus = last.wellbeing.focus - base.focus;

  const symScore = last.symptoms?.improvementScore ?? 0;

  s1.innerHTML = `
    <div class="tagline">
      <strong>Progress Snapshot</strong><br>
      Baseline vs latest check-in (${fmtDate(last.dateISO)}).
    </div>

    <div style="height:12px"></div>

    <div class="list">
      <div class="item">
        <div class="k">Adherence</div>
        <div class="v"><strong>${last.adherencePct}%</strong> of recommended supplements taken</div>
      </div>

      <div class="item">
        <div class="k">Wellbeing change (latest - baseline)</div>
        <div class="v">
          Energy: <strong>${dEnergy>=0?"+":""}${dEnergy}</strong> •
          Mood: <strong>${dMood>=0?"+":""}${dMood}</strong> •
          Sleep: <strong>${dSleep>=0?"+":""}${dSleep}</strong> •
          Focus: <strong>${dFocus>=0?"+":""}${dFocus}</strong>
        </div>
        <div class="fineprint" style="margin-top:8px">
          Baseline: E${base.energy}/10 M${base.mood}/10 S${base.sleep}/10 F${base.focus}/10 •
          Latest: E${last.wellbeing.energy}/10 M${last.wellbeing.mood}/10 S${last.wellbeing.sleep}/10 F${last.wellbeing.focus}/10
        </div>
      </div>

      <div class="item">
        <div class="k">Symptom improvement score</div>
        <div class="v"><strong>${symScore}</strong> (sum of symptom change ratings this week)</div>
        <div class="fineprint" style="margin-top:8px">
          Positive score indicates overall improvement; negative indicates worsening.
        </div>
      </div>

      <div class="item">
        <div class="k">Side effects</div>
        <div class="v">${escapeHtml((last.sideEffects||[]).join(", ") || "None reported")}</div>
      </div>

      <div class="item">
        <div class="k">Notes</div>
        <div class="v">${escapeHtml(last.notes || "—")}</div>
      </div>
    </div>

    <div class="btns">
      <button class="ghost" onclick="setStep(5)">Add another check-in</button>
      <button class="primary" onclick="setStep(8)">Send feedback</button>
    </div>
  `;
  mainEl.appendChild(s1);
  mainEl.appendChild(navButtons(true,true,"Continue"));
}

/* ===== STEP 7 ===== */
function renderCitations(){
  const reg = buildCitationsRegistry();
  const cov = coverageStats();

  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="tagline">
      <strong>Citations Registry</strong><br>
      This is the complete list of source identifiers used for your current medication-based evidence (click PMID/PMCID to open).
    </div>
  `;
  mainEl.appendChild(s1);

  const s2 = document.createElement("div");
  s2.className="section";
  s2.innerHTML = `
    <div class="toolbar">
      <div class="lefttools">
        <div class="countPill"><strong>Total citations:</strong> ${reg.all.length}</div>
        <div class="countPill"><strong>Coverage:</strong> ${cov.evidenceCount}/${cov.selectedCount} meds with evidence</div>
      </div>
      <div class="lefttools">
        <input id="search" placeholder="Search citations…" style="min-width:240px" />
        <button class="smallbtn ghost" id="copyAll">Copy all</button>
      </div>
    </div>

    <div class="divider"></div>

    <div class="groupTitle">PMID (${reg.pmid.length})</div>
    <div class="grid2" id="pmidGrid"></div>

    <div class="groupTitle">PMCID (${reg.pmcid.length})</div>
    <div class="grid2" id="pmcidGrid"></div>

    <div class="groupTitle">FDA (${reg.fda.length})</div>
    <div class="grid2" id="fdaGrid"></div>

    <div class="groupTitle">Other (${reg.other.length})</div>
    <div class="grid2" id="otherGrid"></div>
  `;
  mainEl.appendChild(s2);

  const grids = {
    pmid: s2.querySelector("#pmidGrid"),
    pmcid: s2.querySelector("#pmcidGrid"),
    fda: s2.querySelector("#fdaGrid"),
    other: s2.querySelector("#otherGrid"),
  };

  function renderList(list, el, filter){
    el.innerHTML = "";
    const shown = (list||[]).filter(x => !filter || x.toLowerCase().includes(filter.toLowerCase()));
    if(!shown.length){
      el.innerHTML = `<div class="fineprint">No matches.</div>`;
      return;
    }
    shown.forEach(x=>{
      const div = document.createElement("div");
      div.innerHTML = renderCitationChip(x);
      el.appendChild(div);
    });
  }

  function redraw(filter=""){
    renderList(reg.pmid, grids.pmid, filter);
    renderList(reg.pmcid, grids.pmcid, filter);
    renderList(reg.fda, grids.fda, filter);
    renderList(reg.other, grids.other, filter);
  }

  redraw("");

  s2.querySelector("#search").addEventListener("input", (e)=> redraw(e.target.value || ""));
  s2.querySelector("#copyAll").addEventListener("click", async ()=>{
    const txt = reg.all.join("\n");
    try{
      await navigator.clipboard.writeText(txt);
      alert("Copied citations to clipboard.");
    } catch(e){
      const ta = document.createElement("textarea");
      ta.value = txt;
      document.body.appendChild(ta);
      ta.select();
      document.execCommand("copy");
      ta.remove();
      alert("Copied citations to clipboard.");
    }
  });

  mainEl.appendChild(navButtons(true,true,"Continue"));
}

/* ===== STEP 8 ===== */
function renderFeedback(){
  const s1 = document.createElement("div");
  s1.className="section";
  s1.innerHTML = `
    <div class="tagline">
      <strong>Your feedback is valuable</strong><br>
      Help us make this more useful, user-friendly, and innovative.
    </div>

    <div style="height:12px"></div>

    <div class="row">
      <div class="col">
        <label>Feedback type</label>
        <select id="fbType">
          <option value="Bug">Bug / something not working</option>
          <option value="Suggestion">Suggestion / improvement</option>
          <option value="Question">Question</option>
          <option value="Other">Other</option>
        </select>
      </div>
      <div class="col">
        <label>Can we contact you?</label>
        <select id="fbContact">
          <option value="yes">Yes</option>
          <option value="no">No</option>
        </select>
      </div>
    </div>

    <div style="height:12px"></div>

    <label>Message</label>
    <textarea id="fbMsg" placeholder="Tell us what you liked, what was confusing, and what you want next..."></textarea>

    <div class="btns">
      <button class="primary" id="fbSend">Send email to info@geneomx.com</button>
      <button class="ghost" id="fbSaveLocal">Save feedback (local)</button>
    </div>

    <div class="divider"></div>

    <div class="fineprint">
      <strong>Tip for reviewers:</strong> If you can, mention which tab you were on and what you expected to happen.
    </div>

    <div style="height:14px"></div>
    <div class="item">
      <div class="k">Email</div>
      <div class="v">You can always email us directly: <a class="mailto" href="mailto:info@geneomx.com">info@geneomx.com</a></div>
    </div>
  `;
  mainEl.appendChild(s1);

  s1.querySelector("#fbSend").addEventListener("click", ()=>{
    const type = s1.querySelector("#fbType").value;
    const canContact = s1.querySelector("#fbContact").value === "yes";
    const message = (s1.querySelector("#fbMsg").value || "").trim();
    const email = state.account.email || "";

    // local record
    state.feedback.push({ dateISO: new Date().toISOString(), type, message, canContact, email });
    save();

    // send mailto
    sendFeedbackEmail({type, message, canContact, email});
  });

  s1.querySelector("#fbSaveLocal").addEventListener("click", ()=>{
    const type = s1.querySelector("#fbType").value;
    const canContact = s1.querySelector("#fbContact").value === "yes";
    const message = (s1.querySelector("#fbMsg").value || "").trim();
    const email = state.account.email || "";
    state.feedback.push({ dateISO: new Date().toISOString(), type, message, canContact, email });
    save();
    alert("Saved locally. (In production this would be submitted to Geneomx.)");
  });

  // show last few feedback notes (local)
  const s2 = document.createElement("div");
  s2.className="section";
  const recent = state.feedback.slice(-5).reverse();
  s2.innerHTML = `
    <div class="pill" style="background: rgba(255,79,216,.14); border-color: rgba(255,79,216,.25);">Recent feedback (local)</div>
    <div style="height:10px"></div>
    <div class="list">
      ${recent.length ? recent.map(f=>`
        <div class="item">
          <div class="k">${escapeHtml(f.type)} • ${fmtDate(f.dateISO)}</div>
          <div class="v">${escapeHtml(f.message || "—")}</div>
        </div>
      `).join("") : `<div class="fineprint">No feedback saved yet.</div>`}
    </div>
  `;
  mainEl.appendChild(s2);

  mainEl.appendChild(navButtons(true,false,""));
}

/* ===========================
   Minimal stubs for not-yet-shown earlier steps in this file
   (We kept them already above)
   =========================== */

/* ===== STEP helpers not shown earlier in this file: Results evidence toggle */
function renderResultsEvidenceToggleBind(container){
  container.querySelectorAll("[data-evbtn]").forEach(btn=>{
    btn.addEventListener("click", ()=>{
      const id = btn.getAttribute("data-evbtn");
      const panel = document.getElementById(id);
      if(!panel) return;
      panel.style.display = (panel.style.display==="none") ? "block" : "none";
    });
  });
}

/* ===== STEP 4 Evidence toggles already bound inline */

/* ===========================
   PLACEHOLDER: (Medications & Results were already rendered above)
   (No duplicate defs here)
   =========================== */

/* ===========================
   (IMPORTANT) Missing functions from previous version:
   - renderMeds already defined
   - renderSymptoms already defined
   - renderWellbeing already defined
   - renderResults already defined
   - renderCitations already defined
   - renderFeedback already defined
   - renderAccount already defined
   We still need renderSteps/renderPills/side/summary renderers
   =========================== */

function renderMainRouter(){
  renderMain();
}

function renderAll(){
  renderSteps();
  renderPills();
  renderSummaryTop();
  renderSide();
  renderContactBox();
  renderMainRouter();
}

renderAll();
</script>
</body>
</html># V1-dashboard-
