<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Well Pharmacy - โปรแกรมคํานวณราคาขายและ %GP ระดับมืออาชีพ</title>
<link
href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;50
0;600;700&display=swap" rel="stylesheet">
<style>
:root {
--bg-slate-50: #f8fafc;
--bg-white: #ffffff;
--border-slate-100: #f1f5f9;
--border-slate-200: #e2e8f0;
--text-slate-500: #64748b;
--text-slate-600: #475569;
--text-slate-700: #334155;
--text-slate-800: #1e293b;
--emerald-50: #ecfdf5;
--emerald-200: #a7f3d0;
--emerald-300: #6ee7b7;
--emerald-600: #059669;
--emerald-700: #047857;
--emerald-800: #065f46;
--emerald-900: #064e3b;
--blue-50: #eff6ff;
--blue-200: #bfdbfe;
--blue-300: #93c5fd;
--blue-800: #1e40af;
}

* { box-sizing: border-box; margin: 0; padding: 0; }
body {
font-family: 'Sarabun', sans-serif;
background-color: var(--bg-slate-50);
color: var(--text-slate-800);
min-height: 100vh;
padding: 32px 16px;
line-height: 1.5;
}
.container { max-width: 1024px; margin: 0 auto; display: flex;
flex-direction: column; gap: 24px; }
.card { background-color: var(--bg-white); padding: 24px;
border-radius: 16px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); border:
1px solid var(--border-slate-100); }
.header-card { display: flex; flex-direction: row; justify-content:
space-between; align-items: center; gap: 16px; }
@media (max-width: 768px) { .header-card { flex-direction: column;
align-items: flex-start; } }
h1 { font-size: 24px; font-weight: 700; color:
var(--text-slate-800); display: flex; align-items: center; gap: 8px; }
p.subtitle { font-size: 14px; color: var(--text-slate-500);
margin-top: 4px; }
.btn-group { display: flex; gap: 12px; }
.btn { padding: 8px 16px; font-size: 14px; font-weight: 500;
border-radius: 12px; border: none; cursor: pointer; transition: all
0.2s; }
.btn-primary { background-color: var(--emerald-600); color: white;
box-shadow: 0 1px 2px rgba(0,0,0,0.05); }
.btn-primary:hover { background-color: var(--emerald-700); }
.btn-secondary { background-color: var(--border-slate-100); color:
var(--text-slate-600); }
.btn-secondary:hover { background-color: var(--border-slate-200); }
.hidden { display: none !important; }
.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 24px;
}
@media (max-width: 768px) { .grid-2 { grid-template-columns: 1fr; }
}
.space-y-4 > * + * { margin-top: 16px; }
.space-y-6 > * + * { margin-top: 24px; }
.form-group label { display: block; font-size: 14px; font-weight:
500; color: var(--text-slate-600); margin-bottom: 4px; }
.form-control { width: 100%; padding: 10px 16px; background-color:
var(--bg-slate-50); border: 1px solid var(--border-slate-200);
border-radius: 12px; font-family: 'Sarabun', sans-serif; font-size:
14px; outline: none; transition: all 0.2s; }
.form-control:focus { border-color: var(--emerald-600);
background-color: var(--bg-white); box-shadow: 0 0 0 2px rgba(5, 150,
105, 0.15); }

.box-emerald { background-color: var(--emerald-50); border: 1px
solid var(--emerald-200); padding: 12px; border-radius: 12px; }
.box-blue { background-color: var(--blue-50); border: 1px solid
var(--blue-200); padding: 12px; border-radius: 12px; }
.section-title { font-size: 18px; font-weight: 700; color:
var(--text-slate-700); border-bottom: 1px solid
var(--border-slate-100); padding-bottom: 12px; margin-bottom: 16px; }
</style>
</head>
<body>
<div class="container">
<div class="card header-card">
<div>
<h1><span>💊</span> เวลล์ ฟาร์มาซี - ระบบคํานวณราคาขาย & %GP Pro</h1>
<p class="subtitle">เวอร์ชัน Pure CSS แสดงผลสวยงามครบถ้วน ไม่พึ่งพาสคริ
ปต์ภายนอก</p>
</div>
<div class="btn-group">
<button onclick="toggleMode('single')" id="btnSingle" class="btn
btn-primary">คํานวณเดี่ยว</button>
<button onclick="toggleMode('multi')" id="btnMulti" class="btn
btn-secondary">ตารางหลายรายการ</button>
</div>
</div>
<div id="singleSection" class="card space-y-6">
<h2 class="section-title">🧮 คํานวณราคายาและสินค้า (หน้าร้าน / LINE MAN /
Telepharmacy)</h2>
<div class="grid-2">
<div class="space-y-4">
<div class="box-emerald space-y-4">
<label class="form-group" style="font-size: 12px;
font-weight: 600; color: var(--emerald-800);">เลือกช่องทางการขาย /
แพลตฟอร์ม</label>

<select id="s_channel" onchange="onChannelChange();
calculateSingle();" class="form-control" style="border-color:
var(--emerald-300); color: var(--emerald-900); font-weight: 500;">

<option value="store">🏪 หน้าร้านปกติ (Retail /

Store)</option>

<option value="lineman">🛵 LINE MAN (Food/Delivery

GP)</option>

<option value="telepharmacy">💻 Telepharmacy ผ่าน LINE

MAN</option>
</select>
</div>
<div class="form-group">
<label>ราคาทุน (บาท)</label>
<input type="number" id="s_cost" class="form-control"

placeholder="0.00" oninput="calculateSingle()">

</div>
<div class="grid-2" style="gap: 12px;">
<div class="form-group">
<label>ราคาป้าย / ราคาตั้งต้น (บาท)</label>
<input type="number" id="s_price" class="form-control"

placeholder="0.00" oninput="calculateSingle('price')">

</div>
<div class="form-group">
<label>เป้าหมาย %GP</label>
<input type="number" id="s_gp" class="form-control"

placeholder="0.00" oninput="calculateSingle('gp')">

</div>
</div>
</div>
<div class="box-emerald">
<p style="font-weight: 600; color: var(--emerald-900);">ผลลัพธ์

การคํานวณ</p>

<p style="margin-top: 8px; font-size: 14px; color: var(--
emerald-800);">กําไรสุทธิ: <span id="totalProfit" style="font-weight:
bold; color: var(--emerald-600);">0.00 บาท</span></p>
</div>
</div>
</div>
</div>
</script>
