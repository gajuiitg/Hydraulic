<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-TND589HSEC"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-TND589HSEC');
</script>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">
<title>Hydraulic Line Sizing &amp; Pressure Drop Calculator</title>
<style>
  :root{
    --navy:#1b3a5c; --steel:#2f6690; --lt:#eef3f7; --line:#d4dce5; --ok:#1e7d34; --warn:#b34700; --bad:#a4161a;
    --txt:#000000; --dim:#4a5a6a; --accent:#0066cc; --accent2:#0052a3; --panel:#f8fafb; --panel2:#f0f2f5; --mono:'Courier New',monospace;
  }
  *{box-sizing:border-box;}
  body{margin:0;background:linear-gradient(180deg,#f5f7fa,#eff1f5 200px);color:var(--txt);
       font-family:'Segoe UI',Tahoma,Arial,sans-serif;font-size:14px;padding-bottom:60px;}
  header{padding:18px 26px;border-bottom:1px solid var(--line);background:var(--panel2);
         display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;}
  header h1{font-size:18px;margin:0;letter-spacing:.3px;font-weight:600;}
  header h1 span{color:var(--accent);font-family:var(--mono);}
  header .sub{color:var(--dim);font-size:12px;margin-top:3px;}
  .tag{font-family:var(--mono);font-size:11px;color:#d97706;border:1px solid #fef3c7;
       background:#fffbeb;padding:3px 8px;border-radius:3px;}
  main{max-width:1280px;margin:0 auto;padding:20px 22px;}
  .grid{display:grid;grid-template-columns:340px 1fr;gap:18px;}
  @media(max-width:980px){.grid{grid-template-columns:1fr;}}
  .card{background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:16px;margin-bottom:16px;}
  .card h2{font-size:13px;text-transform:uppercase;letter-spacing:.8px;color:var(--accent);
           margin:0 0 12px;border-bottom:1px solid var(--line);padding-bottom:8px;}
  label{display:block;font-size:12px;color:var(--dim);margin-bottom:3px;margin-top:10px;}
  input,select{width:100%;background:var(--panel2);border:1px solid var(--line);color:var(--txt);
        padding:7px 8px;border-radius:4px;font-family:var(--mono);font-size:13px;}
  input:focus,select:focus{outline:none;border-color:var(--accent);}
  .row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
  .row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;}
  .row4{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:10px;}
  button{cursor:pointer;border:none;border-radius:5px;font-family:'Segoe UI',sans-serif;font-weight:600;
         font-size:12.5px;padding:8px 14px;}
  .btn-accent{background:var(--accent);color:#ffffff;}
  .btn-accent:hover{background:#0052a3;}
  .btn-ghost{background:transparent;border:1px solid var(--line);color:var(--txt);}
  .btn-ghost:hover{border-color:var(--accent);color:var(--accent);}
  .btn-danger{background:transparent;border:1px solid #f87171;color:#dc2626;padding:5px 9px;font-size:11px;}
  .btn-danger:hover{background:#fee2e2;}
  .btn-small{padding:5px 9px;font-size:11px;}
  .segment{background:var(--panel2);border:1px solid var(--line);border-radius:6px;padding:12px;margin-bottom:12px;}
  .segment-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;}
  .segment-head input{width:auto;flex:1;background:transparent;border:none;font-size:13.5px;
        font-weight:600;color:var(--accent2);padding:2px 0;font-family:'Segoe UI',sans-serif;}
  .segment-head input:focus{border-bottom:1px solid var(--accent);}
  .fit-row{display:grid;grid-template-columns:1fr 60px 70px 30px;gap:6px;align-items:center;margin-top:6px;}
  .fit-list{margin-top:10px;padding-top:8px;border-top:1px dashed var(--line);}
  .fit-list-title{font-size:11px;color:var(--dim);text-transform:uppercase;letter-spacing:.5px;margin-bottom:4px;}
  table{width:100%;border-collapse:collapse;font-size:12.5px;}
  th{text-align:left;color:var(--dim);font-weight:600;font-size:11px;text-transform:uppercase;
     letter-spacing:.4px;padding:8px 8px;border-bottom:1px solid var(--line);white-space:nowrap;}
  td{padding:8px 8px;border-bottom:1px solid #e5e7eb;font-family:var(--mono);white-space:nowrap;}
  tbody tr:hover{background:#f3f4f6;}
  .pill{display:inline-block;padding:2px 8px;border-radius:20px;font-size:11px;font-weight:700;font-family:'Segoe UI',sans-serif;}
  .pill-ok{background:#dcfce7;color:#166534;border:1px solid #bbf7d0;}
  .pill-warn{background:#fef3c7;color:#92400e;border:1px solid #fcd34d;}
  .pill-bad{background:#fee2e2;color:#991b1b;border:1px solid #fecaca;}
  .summary{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;margin-top:4px;}
  .kpi{background:var(--panel2);border:1px solid var(--line);border-radius:6px;padding:12px;}
  .kpi .val{font-family:var(--mono);font-size:20px;font-weight:700;color:var(--txt);}
  .kpi .lbl{font-size:11px;color:var(--dim);text-transform:uppercase;letter-spacing:.5px;margin-top:2px;}
  .kpi.bad .val{color:var(--bad);} .kpi.warn .val{color:var(--warn);} .kpi.ok .val{color:var(--ok);}
  .note{font-size:11.5px;color:var(--dim);line-height:1.5;margin-top:10px;}
  .divider{height:1px;background:var(--line);margin:14px 0;}
  .actions{display:flex;gap:10px;margin-top:6px;}
  .empty{color:var(--dim);font-size:12.5px;text-align:center;padding:30px 0;}
  footer{max-width:1280px;margin:10px auto 0;padding:0 22px;color:var(--dim);font-size:11px;line-height:1.6;}
  a.link{color:var(--accent);text-decoration:none;}

/* ---------- PRINT REPORT (A4) ---------- */
#printReport{display:none;}
@media print{
  @page{ size:A4; margin:14mm 12mm; }
  body *{ visibility:hidden; }
  #printReport, #printReport *{ visibility:visible; }
  #printReport{
    display:block; position:absolute; top:0; left:0; width:100%;
    color:#000; background:#fff; font-family:Arial,Helvetica,sans-serif; font-size:11px;
  }
  #printReport h1{font-size:16px;margin:0 0 2px;}
  #printReport .psub{font-size:10px;color:#444;margin-bottom:10px;}
  #printReport table{width:100%;border-collapse:collapse;margin-bottom:12px;font-size:10px;}
  #printReport th,#printReport td{border:1px solid #999;padding:4px 5px;text-align:left;}
  #printReport th{background:#eee;}
  #printReport h2{font-size:12.5px;margin:14px 0 6px;border-bottom:1px solid #000;padding-bottom:3px;}
  #printReport .meta{display:flex;justify-content:space-between;font-size:10px;color:#333;margin-bottom:8px;}
  #printReport .status-tag{font-weight:bold;}
  #printReport .segblock{margin-bottom:8px;border:1px solid #ccc;padding:6px 8px;page-break-inside:avoid;}
  #printReport .segblock b{font-size:11px;}
  #printReport .fitline{font-size:9.5px;color:#333;margin-top:3px;}
  #printReport .footer-note{font-size:9px;color:#555;margin-top:16px;border-top:1px solid #ccc;padding-top:6px;}
}
</style>
</head>
<body>

<header>
  <div>
    <h1>Hydraulic Line Sizing <span>// dP · Velocity · Erosion</span></h1>
    <div class="sub">Multi-segment pipeline pressure drop calculator — Darcy-Weisbach + Crane TP-410 K-method</div>
  </div>
</header>

<main>
<div class="grid">

  <!-- LEFT: FLUID & GLOBAL INPUTS -->
  <div>
    <div class="card">
      <h2>Fluid &amp; Process Data</h2>

      <label>Fluid Phase</label>
      <select id="phase">
        <option value="liquid">Liquid (incompressible)</option>
        <option value="gas">Gas / Vapour (compressible, isothermal)</option>
      </select>

      <label>Inlet Pressure</label>
      <div class="row2">
        <input type="number" id="pIn" value="5.0" step="0.01">
        <select id="pInUnit">
          <option value="kgcm2g" selected>kg/cm²(g)</option>
          <option value="barg">bar(g)</option>
        </select>
      </div>

      <div class="row2">
        <div><label>Temperature (°C)</label><input type="number" id="temp" value="40"></div>
        <div><label>Density @ inlet (kg/m³)</label><input type="number" id="rho" value="850" step="0.1"></div>
      </div>

      <div class="row2">
        <div><label>Viscosity (cP)</label><input type="number" id="visc" value="0.5" step="0.001"></div>
        <div><label>Mass Flow (kg/hr)</label><input type="number" id="mflow" value="20000" step="1"></div>
      </div>

      <label>Erosional Velocity Constant "C" (API RP 14E)</label>
      <select id="cConst">
        <option value="100">C = 100 (continuous service, general)</option>
        <option value="122">C = 122 (solids-free, non-corrosive)</option>
        <option value="150">C = 150 (solids-free, corrosion-resistant / intermittent)</option>
        <option value="200">C = 200 (continuously corrosion-resistant, solids-free)</option>
      </select>
      <div class="note">Ve (m/s) = 0.3048 × C / √(ρ<sub>lb/ft³</sub>). Lower C = more conservative (erosive/corrosive/two-phase service).</div>
    </div>

    <div class="card">
      <h2>Global Notes</h2>
      <div class="note">
        • Pipe ID/WT table follows ASME B36.10/19 nominal values — verify against the project piping class for critical lines.<br>
        • Gas phase uses isothermal ideal-gas density correction segment-to-segment (2-pass iteration).<br>
        • Control valve / orifice ΔP is entered manually (size separately using Cv/Cg methods).<br>
        • Friction factor: Colebrook-White (Swamee-Jain explicit form); laminar below Re 2300.
      </div>
    </div>
  </div>

  <!-- RIGHT: SEGMENTS + RESULTS -->
  <div>
    <div class="card">
      <h2>Pipeline Segments</h2>
      <div id="segments"></div>
      <div class="actions">
        <button class="btn-accent" onclick="addSegment()">+ Add Pipe Segment</button>
        <button class="btn-ghost" onclick="calcAll()">▶ Calculate</button>
        <button class="btn-ghost" onclick="printReport()">🖨 Print Report (A4)</button>
      </div>
    </div>

    <div class="card" id="resultsCard" style="display:none;">
      <h2>Results Summary</h2>
      <div class="summary" id="kpis"></div>
      <div class="divider"></div>
      <table>
        <thead><tr>
          <th>Segment</th><th>Q in (kg/hr)</th><th>T in (°C)</th><th>P in (barg)</th><th>NPS</th><th>ID (mm)</th><th>Vel (m/s)</th><th>Re</th><th>f</th>
          <th>ΣK fit.</th><th>ΔP fric. (bar)</th><th>ΔP fit. (bar)</th><th>ΔP elev. (bar)</th><th>ΔP total (bar)</th>
          <th>P out (barg)</th><th>Ve eros. (m/s)</th><th>%Ve</th><th>Status</th>
        </tr></thead>
        <tbody id="resultsBody"></tbody>
      </table>
    </div>
  </div>

</div>
</main>

<div id="printReport"></div>
<footer class="no-print">
  <h3>Developer Information</h3>
  <p><strong>Gajanand Yadav</strong></p>
  <p>Chemical Engineer, IIT Guwahati</p>
  <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a> |
     Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
  <p>For property calculation, Density,Cp, saturation condition visit below link</p>
  <a href="https://gajuiitg.github.io/Thermocal/">Clickable Here</a>
</footer>
<footer>
  Built for internal engineering use — cross-check critical / API 570 / relief-line calculations against Aspen Hydraulics, HTRI, or Crane TP-410 hand calc before issuing for construction.
</footer>

<script>
/* ---------------- PIPE DIMENSION DATABASE (ASME B36.10/19, mm) ---------------- */
const pipeOD = {
  0.5:21.3, 0.75:26.7, 1:33.4, 1.25:42.2, 1.5:48.3, 2:60.3, 2.5:73.0, 3:88.9, 4:114.3,
  5:141.3, 6:168.3, 8:219.1, 10:273.0, 12:323.8, 14:355.6, 16:406.4, 18:457.2, 20:508.0, 24:609.6,
  26:660.4, 28:711.2, 30:762.0, 32:812.8, 34:863.6, 36:914.4, 40:1016.0, 42:1066.8, 44:1117.6,
  48:1219.2, 52:1320.8, 56:1422.4, 60:1524.0, 64:1625.6
};

const pipeWT = {
 0.5:{'SCH10':2.11,'SCH40/STD':2.77,'SCH80/XS':3.73,'SCH160':4.78,'XXS':7.47},
 0.75:{'SCH10':2.11,'SCH40/STD':2.87,'SCH80/XS':3.91,'SCH160':5.56,'XXS':7.82},
 1:{'SCH10':2.77,'SCH40/STD':3.38,'SCH80/XS':4.55,'SCH160':6.35,'XXS':9.09},
 1.25:{'SCH10':2.77,'SCH40/STD':3.56,'SCH80/XS':4.85,'SCH160':6.35,'XXS':9.70},
 1.5:{'SCH10':2.77,'SCH40/STD':3.68,'SCH80/XS':5.08,'SCH160':7.14,'XXS':10.15},
 2:{'SCH10':2.77,'SCH40/STD':3.91,'SCH80/XS':5.54,'SCH160':8.74,'XXS':11.07},
 2.5:{'SCH10':3.05,'SCH40/STD':5.16,'SCH80/XS':7.01,'SCH160':9.53,'XXS':14.02},
 3:{'SCH10':3.05,'SCH40/STD':5.49,'SCH80/XS':7.62,'SCH160':11.13,'XXS':15.24},
 4:{'SCH10':3.05,'SCH40/STD':6.02,'SCH80/XS':8.56,'SCH120':11.13,'SCH160':13.49,'XXS':17.12},
 5:{'SCH10':3.40,'SCH40/STD':6.55,'SCH80/XS':9.53,'SCH160':15.88,'XXS':19.05},
 6:{'SCH10':3.40,'SCH40/STD':7.11,'SCH80/XS':10.97,'SCH120':14.27,'SCH160':18.26,'XXS':21.95},
 8:{'SCH10':3.76,'SCH20':6.35,'SCH30':7.04,'SCH40/STD':8.18,'SCH60':10.31,'SCH80/XS':12.70,
    'SCH100':15.09,'SCH120':18.26,'SCH140':20.62,'SCH160':23.01,'XXS':22.23},
 10:{'SCH10':4.19,'SCH20':6.35,'SCH30':7.80,'SCH40/STD':9.27,'SCH60':12.70,'SCH80/XS':15.09,
     'SCH100':18.26,'SCH120':21.44,'SCH140':25.40,'SCH160':28.58,'XXS':25.40},
 12:{'SCH10':4.57,'SCH20':6.35,'SCH30':8.38,'STD':9.53,'XS':12.70,'SCH60':14.27,'SCH80':17.48,
     'SCH100':21.44,'SCH120':25.40,'SCH140':28.58,'SCH160':33.32,'XXS':25.40},
 14:{'SCH10':6.35,'SCH20':7.92,'STD':9.53,'SCH30':9.53,'SCH40':11.13,'XS':12.70,'SCH60':15.09,'SCH80':19.05},
 16:{'SCH10':6.35,'SCH20':7.92,'STD':9.53,'SCH30':9.53,'SCH40':12.70,'XS':12.70,'SCH60':16.66,'SCH80':21.44},
 18:{'SCH10':6.35,'SCH20':7.92,'STD':9.53,'SCH30':11.13,'XS':12.70,'SCH40':14.27,'SCH60':19.05,'SCH80':23.83},
 20:{'SCH10':6.35,'SCH20':9.53,'STD':9.53,'SCH30':12.70,'XS':12.70,'SCH40':15.09,'SCH60':20.62,'SCH80':26.19},
 24:{'SCH10':6.35,'SCH20':9.53,'STD':9.53,'SCH30':14.27,'XS':12.70,'SCH40':17.48,'SCH60':24.61,'SCH80':30.96},
 26:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':19.05},
 28:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':20.62},
 30:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':22.22},
 32:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':23.83},
 34:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':25.40},
 36:{'SCH10':7.92,'STD':9.53,'SCH20':12.70,'XS':12.70,'SCH30':15.88,'SCH40':25.40},
 40:{'STD':9.53,'XS':12.70},
 42:{'STD':9.53,'XS':12.70},
 44:{'STD':9.53,'XS':12.70},
 48:{'STD':9.53,'XS':12.70},
 52:{'STD':9.53,'XS':12.70},
 56:{'STD':9.53,'XS':12.70},
 60:{'STD':9.53,'XS':12.70},
 64:{'STD':9.53,'XS':12.70}
};

const roughness = { // mm, absolute
 'cs_new':0.045,'cs_service':0.15,'ss':0.002,'galv':0.15,'ci':0.26,'pvc':0.0015
};
const roughLabels = {cs_new:'Carbon Steel (new)',cs_service:'Carbon Steel (in service)',
  ss:'Stainless Steel',galv:'Galvanized Steel',ci:'Cast Iron',pvc:'PVC / Lined'};

const fT = {
  0.5:.027, 0.75:.027, 1:.027, 1.25:.023, 1.5:.023, 2:.021, 2.5:.019, 3:.018, 4:.017,
  5:.016, 6:.015, 8:.014, 10:.014, 12:.013, 14:.013, 16:.012, 18:.012, 20:.012, 24:.011,
  26:.011, 28:.011, 30:.011, 32:.010, 34:.010, 36:.010, 40:.009, 42:.009, 44:.009,
  48:.009, 52:.008, 56:.008, 60:.008, 64:.008
};

const fittingTypes = [
 {id:'elbow90', label:"90° Elbow (Standard)", method:'LD', ld:30},
 {id:'elbow90lr', label:"90° Elbow (Long Radius)", method:'LD', ld:20},
 {id:'elbow45', label:"45° Elbow", method:'LD', ld:16},
 {id:'tee_run', label:"Tee — Through Run", method:'LD', ld:20},
 {id:'tee_branch', label:"Tee — Branch Flow", method:'LD', ld:60},
 {id:'gate', label:"Gate / Isolation Valve (full open)", method:'LD', ld:8},
 {id:'ball', label:"Ball Valve (full bore)", method:'LD', ld:3},
 {id:'plug', label:"Plug Valve (full bore)", method:'LD', ld:18},
 {id:'globe', label:"Globe Valve", method:'LD', ld:340},
 {id:'butterfly', label:"Butterfly Valve", method:'LD', ld:45},
 {id:'nrv_swing', label:"NRV / Check Valve (Swing)", method:'LD', ld:100},
 {id:'nrv_lift', label:"NRV / Check Valve (Lift/Piston)", method:'LD', ld:600},
 {id:'entrance', label:"Pipe Entrance (sharp, from vessel)", method:'K', k:0.5},
 {id:'exit', label:"Pipe Exit (to vessel)", method:'K', k:1.0},
 {id:'reducer', label:"Reducer (gradual)", method:'K', k:0.15},
 {id:'cv', label:"Control Valve — manual ΔP (bar)", method:'manual'},
 {id:'orifice', label:"Orifice Plate — manual ΔP (bar)", method:'manual'},
 {id:'custom', label:"Custom Fitting — enter K value", method:'Kcustom'}
];

/* ---------------- STATE ---------------- */
let segCounter=0, segments=[];

function npsOptions(sel){
  return Object.keys(pipeOD).map(n=>`<option value="${n}" ${sel==n?'selected':''}>${n}"</option>`).join('');
}
function schOptions(nps,sel){
  const s=pipeWT[nps]||{};
  return Object.keys(s).map(k=>`<option value="${k}" ${sel==k?'selected':''}>${k} (${s[k]}mm WT)</option>`).join('')
    + `<option value="CUSTOM" ${sel=='CUSTOM'?'selected':''}>Custom ID (enter directly)</option>`;
}
function roughOptions(sel){
  return Object.keys(roughness).map(k=>`<option value="${k}" ${sel==k?'selected':''}>${roughLabels[k]}</option>`).join('');
}
function fitOptions(){
  return fittingTypes.map(f=>`<option value="${f.id}">${f.label}</option>`).join('');
}

function addSegment(){
  segCounter++;
  const seg={id:segCounter,name:'Segment '+segCounter,nps:2,sch:'SCH40/STD',customID:null,
             length:10,elevation:0,rough:'cs_new',fittings:[],
             ovFlow:{on:false,val:null}, ovTemp:{on:false,val:null}, ovPress:{on:false,val:null}};
  segments.push(seg);
  renderSegments();
}
function removeSegment(id){segments=segments.filter(s=>s.id!==id);renderSegments();}
function addFitting(segId){
  const seg=segments.find(s=>s.id===segId);
  seg.fittings.push({fid:seg.fittings.length+1,type:'elbow90',qty:1,val:0});
  renderSegments();
}
function removeFitting(segId,fid){
  const seg=segments.find(s=>s.id===segId);
  seg.fittings=seg.fittings.filter(f=>f.fid!==fid);
  renderSegments();
}

function renderSegments(){
  const el=document.getElementById('segments');
  if(segments.length===0){el.innerHTML='<div class="empty">No pipe segments yet — click "Add Pipe Segment" to begin.</div>';return;}
  el.innerHTML=segments.map(seg=>`
    <div class="segment" id="seg-${seg.id}">
      <div class="segment-head">
        <input value="${seg.name}" onchange="segments.find(s=>s.id===${seg.id}).name=this.value">
        <button class="btn-danger" onclick="removeSegment(${seg.id})">Remove ✕</button>
      </div>
      <div class="row4">
        <div><label>NPS</label>
          <select onchange="onNpsChange(${seg.id},this.value)">${npsOptions(seg.nps)}</select>
        </div>
        <div><label>Schedule</label>
          <select onchange="segments.find(s=>s.id===${seg.id}).sch=this.value; renderSegments();">
            ${schOptions(seg.nps,seg.sch)}
          </select>
        </div>
        <div><label>Length (m)</label>
          <input type="number" value="${seg.length}" step="0.1"
            onchange="segments.find(s=>s.id===${seg.id}).length=parseFloat(this.value)||0">
        </div>
        <div><label>Elevation Δ (m) ↑+/↓−</label>
          <input type="number" value="${seg.elevation}" step="0.1"
            onchange="segments.find(s=>s.id===${seg.id}).elevation=parseFloat(this.value)||0">
        </div>
      </div>
      ${seg.sch==='CUSTOM'?`
      <label>Custom Internal Diameter (mm)</label>
      <input type="number" value="${seg.customID||''}" step="0.1"
        onchange="segments.find(s=>s.id===${seg.id}).customID=parseFloat(this.value)||0">`:''}
      <label>Pipe MOC / Roughness</label>
      <select onchange="segments.find(s=>s.id===${seg.id}).rough=this.value">${roughOptions(seg.rough)}</select>

      <div class="fit-list">
        <div class="fit-list-title">Inlet Conditions for this Segment</div>
        <div class="note" style="margin-top:0;">By default this segment inherits flow / temperature / pressure from the upstream segment's outlet (or the global inputs, for the first segment). Tick to override any of them here.</div>
        <div class="row3" style="margin-top:8px;">
          <div>
            <label><input type="checkbox" style="width:auto;display:inline-block;margin-right:5px;"
              ${seg.ovFlow.on?'checked':''}
              onchange="segments.find(s=>s.id===${seg.id}).ovFlow.on=this.checked; renderSegments();">Override Flow (kg/hr)</label>
            <input type="number" ${seg.ovFlow.on?'':'disabled'} value="${seg.ovFlow.val??''}" step="1"
              onchange="segments.find(s=>s.id===${seg.id}).ovFlow.val=parseFloat(this.value)||0">
          </div>
          <div>
            <label><input type="checkbox" style="width:auto;display:inline-block;margin-right:5px;"
              ${seg.ovTemp.on?'checked':''}
              onchange="segments.find(s=>s.id===${seg.id}).ovTemp.on=this.checked; renderSegments();">Override Temp (°C)</label>
            <input type="number" ${seg.ovTemp.on?'':'disabled'} value="${seg.ovTemp.val??''}" step="0.1"
              onchange="segments.find(s=>s.id===${seg.id}).ovTemp.val=parseFloat(this.value)||0">
          </div>
          <div>
            <label><input type="checkbox" style="width:auto;display:inline-block;margin-right:5px;"
              ${seg.ovPress.on?'checked':''}
              onchange="segments.find(s=>s.id===${seg.id}).ovPress.on=this.checked; renderSegments();">Override Pressure (barg)</label>
            <input type="number" ${seg.ovPress.on?'':'disabled'} value="${seg.ovPress.val??''}" step="0.01"
              onchange="segments.find(s=>s.id===${seg.id}).ovPress.val=parseFloat(this.value)||0">
          </div>
        </div>
      </div>

      <div class="fit-list">
        <div class="fit-list-title">Fittings / Valves in this segment</div>
        ${seg.fittings.map(f=>`
          <div class="fit-row">
            <select onchange="segments.find(s=>s.id===${seg.id}).fittings.find(x=>x.fid===${f.fid}).type=this.value; renderSegments();">
              ${fittingTypes.map(ft=>`<option value="${ft.id}" ${ft.id===f.type?'selected':''}>${ft.label}</option>`).join('')}
            </select>
            ${(()=>{const ft=fittingTypes.find(x=>x.id===f.type);
              if(ft.method==='manual') return `<input type="number" placeholder="ΔP bar" value="${f.val||''}" step="0.01"
                 onchange="segments.find(s=>s.id===${seg.id}).fittings.find(x=>x.fid===${f.fid}).val=parseFloat(this.value)||0">`;
              if(ft.method==='Kcustom') return `<input type="number" placeholder="K" value="${f.val||''}" step="0.01"
                 onchange="segments.find(s=>s.id===${seg.id}).fittings.find(x=>x.fid===${f.fid}).val=parseFloat(this.value)||0">`;
              return `<div></div>`;
            })()}
            <input type="number" placeholder="Qty" value="${f.qty}" min="1" step="1"
              onchange="segments.find(s=>s.id===${seg.id}).fittings.find(x=>x.fid===${f.fid}).qty=parseInt(this.value)||1">
            <button class="btn-danger" style="padding:5px 7px;" onclick="removeFitting(${seg.id},${f.fid})">✕</button>
          </div>`).join('')}
        <button class="btn-ghost btn-small" style="margin-top:8px;" onclick="addFitting(${seg.id})">+ Add Fitting</button>
      </div>
    </div>
  `).join('');
}
function onNpsChange(segId,val){
  const seg=segments.find(s=>s.id===segId);
  seg.nps=parseFloat(val);
  const scheds=Object.keys(pipeWT[seg.nps]||{});
  if(!scheds.includes(seg.sch)) seg.sch=scheds[0]||'CUSTOM';
  renderSegments();
}

/* ---------------- PRESSURE UNIT HELPER ---------------- */
const KGCM2_TO_BAR = 0.980665; // 1 kgf/cm2 = 0.980665 bar
function pInToBarg(){
  const val = parseFloat(document.getElementById('pIn').value)||0;
  const unit = document.getElementById('pInUnit').value;
  return unit==='kgcm2g' ? val*KGCM2_TO_BAR : val;
}

/* ---------------- CALCULATION ---------------- */
function nearestFT(nps){
  const keys=Object.keys(fT).map(Number).sort((a,b)=>a-b);
  let best=keys[0];
  keys.forEach(k=>{if(Math.abs(k-nps)<Math.abs(best-nps)) best=k;});
  return fT[best];
}
function frictionFactor(re, relRough){
  if(re<2300) return 64/re;
  // Swamee-Jain explicit approximation of Colebrook-White
  const term = relRough/3.7 + 5.74/Math.pow(re,0.9);
  const f = 0.25/Math.pow(Math.log10(term),2);
  return f;
}

function calcAll(){
  if(segments.length===0){alert('Add at least one pipe segment first.');return;}

  const phase=document.getElementById('phase').value;
  const pIn_barg=pInToBarg();
  const tempIn=parseFloat(document.getElementById('temp').value);
  const rho0=parseFloat(document.getElementById('rho').value); // density @ global reference P & T
  const muCp=parseFloat(document.getElementById('visc').value);
  const mflowIn=parseFloat(document.getElementById('mflow').value); // kg/hr
  const Cconst=parseFloat(document.getElementById('cConst').value);
  const mu=muCp/1000; // Pa.s

  const P0_bara = pIn_barg + 1.01325;   // reference abs pressure at which rho0 was specified
  const T0_K = tempIn + 273.15;          // reference temperature at which rho0 was specified

  // running "upstream outlet" carry-over values, updated after each segment
  let curFlow = mflowIn;
  let curTemp = tempIn;
  let curPress_barg = pIn_barg;

  const results=[];

  segments.forEach(seg=>{
    // resolve this segment's inlet conditions: override if ticked, else inherit upstream
    const flowSeg = (seg.ovFlow.on && seg.ovFlow.val!=null) ? seg.ovFlow.val : curFlow;
    const tempSeg = (seg.ovTemp.on && seg.ovTemp.val!=null) ? seg.ovTemp.val : curTemp;
    const pressSeg_barg = (seg.ovPress.on && seg.ovPress.val!=null) ? seg.ovPress.val : curPress_barg;
    const pressSeg_bara = pressSeg_barg + 1.01325;

    // ID determination
    let ID_mm;
    if(seg.sch==='CUSTOM'){ ID_mm = seg.customID||0; }
    else { const OD=pipeOD[seg.nps]; const WT=pipeWT[seg.nps][seg.sch]; ID_mm = OD - 2*WT; }
    const ID = ID_mm/1000; // m
    const area = Math.PI/4*ID*ID;
    const eps = roughness[seg.rough]/1000; // m
    const relRough = ID>0? eps/ID : 0;

    // density at this segment's inlet conditions (gas: isothermal+ideal-gas P & T scaling from reference)
    let rhoSeg = phase==='gas'
      ? rho0 * (pressSeg_bara/P0_bara) * (T0_K/(tempSeg+273.15))
      : rho0;

    let dP_bar_total=0, v=0, Re=0, f=0, Ktot=0, dPfriction_bar=0, dPfittings_bar=0, dPelev_bar=0, manualDP=0;

    // 2-pass iteration for gas (recompute avg density using outlet estimate)
    for(let pass=0; pass<2; pass++){
      const Qvol = (flowSeg/3600)/rhoSeg; // m3/s
      v = ID>0 ? Qvol/area : 0;
      Re = ID>0 ? (rhoSeg*v*ID)/mu : 0;
      f = ID>0 && v>0 ? frictionFactor(Re, relRough) : 0;

      Ktot=0; manualDP=0;
      seg.fittings.forEach(fit=>{
        const ft=fittingTypes.find(x=>x.id===fit.type);
        const qty=fit.qty||1;
        if(ft.method==='LD'){ Ktot += ft.ld*nearestFT(seg.nps)*qty; }
        else if(ft.method==='K'){ Ktot += ft.k*qty; }
        else if(ft.method==='Kcustom'){ Ktot += (fit.val||0)*qty; }
        else if(ft.method==='manual'){ manualDP += (fit.val||0)*qty; }
      });

      const dPfric_Pa = ID>0 ? f*(seg.length/ID)*(rhoSeg*v*v/2) : 0;
      const dPfit_Pa = ID>0 ? Ktot*(rhoSeg*v*v/2) : 0;
      const dPelev_Pa = rhoSeg*9.81*(seg.elevation||0); // +ve elevation (uphill) = pressure loss
      dPfriction_bar = dPfric_Pa/1e5;
      dPfittings_bar = dPfit_Pa/1e5;
      dPelev_bar = dPelev_Pa/1e5;
      dP_bar_total = dPfriction_bar + dPfittings_bar + dPelev_bar + manualDP;

      if(phase==='gas'){
        const pOut_bara_est = Math.max(pressSeg_bara - dP_bar_total, 0.05);
        const rhoOut_est = rho0*(pOut_bara_est/P0_bara)*(T0_K/(tempSeg+273.15));
        const rhoIn = rho0*(pressSeg_bara/P0_bara)*(T0_K/(tempSeg+273.15));
        rhoSeg = (rhoIn + rhoOut_est)/2;
      } else break;
    }

    const pOut_barg = pressSeg_barg - dP_bar_total;
    const pOut_bara = pOut_barg + 1.01325;

    // erosional velocity (API RP14E), based on segment fluid density
    const rho_lbft3 = rhoSeg/16.0185;
    const Ve = rho_lbft3>0 ? (Cconst/Math.sqrt(rho_lbft3))*0.3048 : 0;
    const pctVe = Ve>0 ? (v/Ve*100) : 0;

    let status='OK', pillClass='pill-ok';
    if(pctVe>=100){status='EROSIVE';pillClass='pill-bad';}
    else if(pctVe>=80){status='CAUTION';pillClass='pill-warn';}
    if(pOut_barg<0){status='NEG. PRESS.';pillClass='pill-bad';}

    results.push({name:seg.name,nps:seg.nps,ID_mm,v,Re,f,Ktot,dPfriction_bar,dPfittings_bar,dPelev_bar,
      elevation:seg.elevation||0,
      dP_total:dP_bar_total,pOut_barg,Ve,pctVe,status,pillClass,
      flowSeg,tempSeg,pressSeg_barg});

    // carry forward to next segment's default inlet conditions
    curFlow = flowSeg;
    curTemp = tempSeg;
    curPress_barg = pOut_barg;
  });

  renderResults(results, pIn_barg, curPress_barg);
}

let lastResults=null, lastTotals=null;

function renderResults(results, pIn, pOut){
  document.getElementById('resultsCard').style.display='block';
  const totalDP = pIn-pOut;
  const maxPctVe = Math.max(...results.map(r=>r.pctVe));
  const maxV = Math.max(...results.map(r=>r.v));
  lastResults = results;
  lastTotals = {pIn, pOut, totalDP, maxV, maxPctVe};
  let kpiClass = maxPctVe>=100?'bad':(maxPctVe>=80?'warn':'ok');

  document.getElementById('kpis').innerHTML=`
    <div class="kpi"><div class="val">${totalDP.toFixed(3)} bar</div><div class="lbl">Total ΔP (line)</div></div>
    <div class="kpi"><div class="val">${pOut.toFixed(3)} barg</div><div class="lbl">Outlet Pressure</div></div>
    <div class="kpi"><div class="val">${maxV.toFixed(2)} m/s</div><div class="lbl">Max Velocity</div></div>
    <div class="kpi ${kpiClass}"><div class="val">${maxPctVe.toFixed(0)}%</div><div class="lbl">Max % of Erosional Vel.</div></div>
  `;

  document.getElementById('resultsBody').innerHTML = results.map(r=>`
    <tr>
      <td>${r.name}</td>
      <td>${r.flowSeg.toFixed(0)}</td>
      <td>${r.tempSeg.toFixed(1)}</td>
      <td>${r.pressSeg_barg.toFixed(3)}</td>
      <td>${r.nps}"</td>
      <td>${r.ID_mm.toFixed(1)}</td>
      <td>${r.v.toFixed(2)}</td>
      <td>${r.Re.toFixed(0)}</td>
      <td>${r.f.toFixed(4)}</td>
      <td>${r.Ktot.toFixed(2)}</td>
      <td>${r.dPfriction_bar.toFixed(4)}</td>
      <td>${r.dPfittings_bar.toFixed(4)}</td>
      <td>${r.dPelev_bar.toFixed(4)}</td>
      <td>${r.dP_total.toFixed(4)}</td>
      <td>${r.pOut_barg.toFixed(3)}</td>
      <td>${r.Ve.toFixed(2)}</td>
      <td>${r.pctVe.toFixed(0)}%</td>
      <td><span class="pill ${r.pillClass}">${r.status}</span></td>
    </tr>
  `).join('');
}

/* ---------------- PRINT REPORT ---------------- */
function fitLabel(fit){
  const ft=fittingTypes.find(x=>x.id===fit.type);
  let extra='';
  if(ft.method==='manual') extra=` — ΔP ${fit.val||0} bar each`;
  if(ft.method==='Kcustom') extra=` — K=${fit.val||0}`;
  return `${ft.label} × ${fit.qty}${extra}`;
}

function printReport(){
  calcAll(); // always recalculate on current inputs before printing
  if(!lastResults){ alert('Add at least one pipe segment and calculate first.'); return; }

  const phase=document.getElementById('phase').value==='gas' ? 'Gas / Vapour (compressible)' : 'Liquid (incompressible)';
  const pInVal=document.getElementById('pIn').value;
  const pInUnitSel=document.getElementById('pInUnit');
  const pInUnitLabel=pInUnitSel.options[pInUnitSel.selectedIndex].text;
  const pInBargEq=pInToBarg().toFixed(3);
  const temp=document.getElementById('temp').value;
  const rho=document.getElementById('rho').value;
  const visc=document.getElementById('visc').value;
  const mflow=document.getElementById('mflow').value;
  const cSel=document.getElementById('cConst');
  const cLabel=cSel.options[cSel.selectedIndex].text;
  const now=new Date();
  const dateStr=now.toLocaleDateString('en-IN',{day:'2-digit',month:'short',year:'numeric'})+' '+now.toLocaleTimeString('en-IN',{hour:'2-digit',minute:'2-digit'});

  let html = `
    <h1>Hydraulic Line Sizing Report</h1>
    <div class="psub">dP / Velocity / Erosion Velocity Calculation — Darcy-Weisbach + Crane TP-410 K-method</div>
    <div class="meta"><span>Generated: ${dateStr}</span><span>Prepared by: Gajanand</span></div>

    <h2>1. Fluid &amp; Process Input</h2>
    <table>
      <tr><th>Fluid Phase</th><td>${phase}</td><th>Inlet Pressure</th><td>${pInVal} ${pInUnitLabel} (= ${pInBargEq} bar(g))</td></tr>
      <tr><th>Temperature</th><td>${temp} °C</td><th>Density @ inlet</th><td>${rho} kg/m³</td></tr>
      <tr><th>Viscosity</th><td>${visc} cP</td><th>Mass Flow</th><td>${mflow} kg/hr</td></tr>
      <tr><th>Erosional Velocity Basis</th><td colspan="3">${cLabel}</td></tr>
    </table>

    <h2>2. Pipeline Segment Configuration</h2>
    ${segments.map(seg=>{
      const idTxt = seg.sch==='CUSTOM' ? `Custom ID = ${seg.customID||0} mm` : `${seg.sch} (${(pipeWT[seg.nps][seg.sch]||0)} mm WT)`;
      const overrides=[];
      if(seg.ovFlow.on) overrides.push(`Flow override = ${seg.ovFlow.val||0} kg/hr`);
      if(seg.ovTemp.on) overrides.push(`Temp override = ${seg.ovTemp.val||0} °C`);
      if(seg.ovPress.on) overrides.push(`Pressure override = ${seg.ovPress.val||0} barg`);
      return `<div class="segblock">
        <b>${seg.name}</b> — NPS ${seg.nps}", ${idTxt}, Length ${seg.length} m, Elevation Δ ${seg.elevation>=0?'+':''}${seg.elevation} m, MOC: ${roughLabels[seg.rough]}
        ${overrides.length? `<div class="fitline">Inlet overrides: ${overrides.join(' · ')}</div>` : '<div class="fitline">Inlet conditions: inherited from upstream segment</div>'}
        ${seg.fittings.length? `<div class="fitline">Fittings: ${seg.fittings.map(fitLabel).join(' · ')}</div>` : '<div class="fitline">Fittings: none</div>'}
      </div>`;
    }).join('')}

    <h2>3. Calculation Results</h2>
    <table>
      <thead><tr>
        <th>Segment</th><th>Q in (kg/hr)</th><th>T in (°C)</th><th>P in (barg)</th><th>NPS</th><th>ID (mm)</th><th>Vel (m/s)</th><th>Re</th><th>f</th>
        <th>ΣK fit.</th><th>ΔP fric. (bar)</th><th>ΔP fit. (bar)</th><th>ΔP elev. (bar)</th><th>ΔP tot. (bar)</th>
        <th>P out (barg)</th><th>Ve eros. (m/s)</th><th>%Ve</th><th>Status</th>
      </tr></thead>
      <tbody>
      ${lastResults.map(r=>`
        <tr>
          <td>${r.name}</td><td>${r.flowSeg.toFixed(0)}</td><td>${r.tempSeg.toFixed(1)}</td><td>${r.pressSeg_barg.toFixed(3)}</td>
          <td>${r.nps}"</td><td>${r.ID_mm.toFixed(1)}</td><td>${r.v.toFixed(2)}</td>
          <td>${r.Re.toFixed(0)}</td><td>${r.f.toFixed(4)}</td><td>${r.Ktot.toFixed(2)}</td>
          <td>${r.dPfriction_bar.toFixed(4)}</td><td>${r.dPfittings_bar.toFixed(4)}</td><td>${r.dPelev_bar.toFixed(4)}</td>
          <td>${r.dP_total.toFixed(4)}</td><td>${r.pOut_barg.toFixed(3)}</td>
          <td>${r.Ve.toFixed(2)}</td><td>${r.pctVe.toFixed(0)}%</td>
          <td class="status-tag">${r.status}</td>
        </tr>`).join('')}
      </tbody>
    </table>

    <h2>4. Summary</h2>
    <table>
      <tr><th>Total Line ΔP</th><td>${lastTotals.totalDP.toFixed(3)} bar</td>
          <th>Outlet Pressure</th><td>${lastTotals.pOut.toFixed(3)} bar(g)</td></tr>
      <tr><th>Max Velocity</th><td>${lastTotals.maxV.toFixed(2)} m/s</td>
          <th>Max % of Erosional Velocity</th><td>${lastTotals.maxPctVe.toFixed(0)}%</td></tr>
    </table>

    <div class="footer-note">
      Pipe ID/WT per ASME B36.10/19 nominal values. Friction factor via Swamee-Jain (Colebrook-White approximation);
      fitting losses via Crane TP-410 L/D × f_T method. Control valve/orifice ΔP entered manually.
      For gas service, isothermal ideal-gas density correction applied segment-to-segment (compressibility Z not modeled).
      Verify against project piping class and Aspen Hydraulics / Crane TP-410 hand calculation before use for issued engineering documents.
    </div>
  `;
  document.getElementById('printReport').innerHTML = html;
  window.print();
}

/* init with one example segment */
addSegment();
</script>
</body>
</html>
