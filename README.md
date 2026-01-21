<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>QBE – Quantum Business Explorer</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Poppins,sans-serif;background:#0b0f1a;color:#fff;overflow-x:hidden}
header{padding:40px;text-align:center;background:linear-gradient(135deg,#111827,#020617)}
header h1{margin:0;font-size:40px}
header p{opacity:.7}
.container{max-width:1400px;margin:auto;padding:30px}

.filter{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:25px}
.filter button{padding:8px 14px;border:none;border-radius:20px;background:#22c55e;color:#000;font-weight:600;cursor:pointer;transition:.3s}
.filter button:hover{transform:scale(1.05)}

.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:20px}
.card{background:rgba(255,255,255,.06);border-radius:18px;padding:20px;cursor:pointer;transition:.4s;position:relative;overflow:hidden}
.card::before{content:'';position:absolute;inset:0;background:linear-gradient(120deg,transparent,rgba(34,197,94,.15),transparent);transform:translateX(-100%)}
.card:hover::before{animation:shine 1s}
@keyframes shine{to{transform:translateX(100%)}}
.card:hover{transform:translateY(-10px)}
.card h3{margin:0 0 8px}
.card span{font-size:12px;opacity:.7}

.detail{margin-top:40px;background:rgba(0,0,0,.6);border-radius:25px;padding:30px;display:none;animation:fadeUp .6s}
@keyframes fadeUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}

.badge{display:inline-block;padding:6px 14px;border-radius:20px;background:#22c55e;color:#000;font-size:12px;font-weight:700}
section{margin-top:20px}
section h4{margin-bottom:8px;color:#22c55e}
li{margin-bottom:6px}
.progress{height:10px;background:#1f2937;border-radius:10px;overflow:hidden}
.progress div{height:100%;background:#22c55e}

footer{text-align:center;padding:30px;opacity:.6}
</style>
</head>
<body>
<header>
<h1>QBE</h1>
<p>Quantum Business Explorer – Jalan Nyata Menjadi Business Owner</p>
</header>

<div class="container">
<div class="filter" id="filter"></div>
<div class="grid" id="grid"></div>
<div class="detail" id="detail"></div>
</div>

<footer>© QBE Framework Indonesia</footer>

<script>
const categories=[
'F&B','Peternakan','Pertanian','Properti','Jasa','Manufaktur','Teknologi','Edukasi','Kesehatan','Logistik',
'Fashion','Kosmetik','Kuliner Lokal','Agribisnis','Perikanan','Retail','E-Commerce','Startup','Media','Kreatif',
'Pariwisata','Travel','Event','Percetakan','Laundry','Otomotif','Bengkel','Energi','Tambang','Recycling',
'Keuangan','Asuransi','Fintech','Konstruksi','Interior','Arsitektur','Ekspor','Impor','Distributor','Supplier',
'Waralaba','UMKM','Industri Rumah','Cold Storage','Cloud Kitchen','Co-Working','Properti Digital','AI Service'
];

const businesses=categories.map((c,i)=>({
 name:`Bisnis ${c}`,
 category:c,
 modalIDR:`Rp${(50+i*15).toLocaleString()} juta`,
 modalUSD:`$${(3000+i*800).toLocaleString()}`,
 level:i<15?'Pemula':i<35?'Siap Jalan':'Siap Scale',
 market:`Target market ${c} Indonesia`,
 risk:['Cashflow tidak stabil','Salah lokasi','SDM kurang kompeten'],
 solution:['Kontrol arus kas','Riset lokasi','Pelatihan SDM'],
 steps:['Riset pasar','Siapkan modal','Bangun sistem','Operasional'],
 checklist:['Modal siap','Legalitas','Supplier','Pasar jelas'],
 mistakes:['Terlalu cepat ekspansi','Tidak hitung risiko'],
 progress:Math.min(100,30+i)
}));

const grid=document.getElementById('grid');
const filter=document.getElementById('filter');
const detail=document.getElementById('detail');

function renderFilter(){
 filter.innerHTML='<button onclick="showAll()">Semua</button>';
 categories.forEach(c=>{
  filter.innerHTML+=`<button onclick="filterCat('${c}')">${c}</button>`;
 });
}

function renderGrid(list){
 grid.innerHTML='';
 list.forEach((b,i)=>{
  const d=document.createElement('div');
  d.className='card';
  d.innerHTML=`<h3>${b.name}</h3><span>${b.category}</span>`;
  d.onclick=()=>showDetail(b);
  grid.appendChild(d);
 });
}

function showDetail(b){
 detail.style.display='block';
 detail.innerHTML=`
 <span class="badge">${b.level}</span>
 <h2>${b.name}</h2>
 <p><b>Target Market:</b> ${b.market}</p>
 <p><b>Modal:</b> ${b.modalIDR} | ${b.modalUSD}</p>
 <section><h4>Progress Modal</h4><div class="progress"><div style="width:${b.progress}%"></div></div></section>
 <section><h4>Risiko</h4><ul>${b.risk.map(r=>`<li>${r}</li>`).join('')}</ul></section>
 <section><h4>Solusi</h4><ul>${b.solution.map(r=>`<li>${r}</li>`).join('')}</ul></section>
 <section><h4>Langkah Bisnis</h4><ul>${b.steps.map(r=>`<li>${r}</li>`).join('')}</ul></section>
 <section><h4>Checklist Owner</h4><ul>${b.checklist.map(r=>`<li>${r}</li>`).join('')}</ul></section>
 <section><h4>Kesalahan Umum</h4><ul>${b.mistakes.map(r=>`<li>${r}</li>`).join('')}</ul></section>`;
 detail.scrollIntoView({behavior:'smooth'});
}

function filterCat(c){renderGrid(businesses.filter(b=>b.category===c))}
function showAll(){renderGrid(businesses)}

renderFilter();
showAll();
</script>
</body>
</html>
