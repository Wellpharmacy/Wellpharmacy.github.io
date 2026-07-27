<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบจัดการราคาและต้นทุน</title>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <style> 
        body { font-family: 'Sarabun', sans-serif; } 
        @media print {
            body * { visibility: hidden; }
            #printableArea, #printableArea * { visibility: visible; }
            #printableArea { position: absolute; left: 0; top: 0; width: 100%; }
            .no-print { display: none; }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-slate-100 to-emerald-50 min-h-screen py-6 px-4 flex justify-center">
    
    <div class="w-full max-w-4xl space-y-4">
        
        <!-- Header & Main Navigation Tabs -->
        <div class="bg-white p-5 rounded-3xl shadow-md border border-slate-200 space-y-4 max-w-md mx-auto no-print">
            <div class="text-center space-y-1">
                <h1 class="text-base font-bold text-slate-800 flex items-center justify-center gap-1.5">
                    <span class="text-xl">💊</span>
                    ระบบจัดการราคาและต้นทุน
                </h1>
                <p class="text-[11px] text-slate-500">✨ คำนวณหน้าร้าน, ช่องทางออนไลน์ และวิเคราะห์ต้นทุนซื้อผ่านบัตรเครดิต/ผ่อนชำระ 🚀</p>
            </div>
            <div class="grid grid-cols-3 gap-1 bg-slate-100 p-1.5 rounded-2xl">
                <button onclick="switchMainTab('store')" id="btnMainStore" class="py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm flex items-center justify-center gap-1">🏪 หน้าร้าน</button>
                <button onclick="switchMainTab('online')" id="btnMainOnline" class="py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200 flex items-center justify-center gap-1">🛵 ออนไลน์</button>
                <button onclick="switchMainTab('credit')" id="btnMainCredit" class="py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200 flex items-center justify-center gap-1">💳 วิเคราะห์บัตร</button>
            </div>
        </div>

        <!-- ================= PAGE 1: STORE CALCULATOR ================= -->
        <div id="pageStore" class="bg-white p-6 rounded-3xl shadow-md border border-slate-200 space-y-4 max-w-md mx-auto">
            <h2 class="text-xs font-bold text-slate-800 border-b pb-3 flex items-center gap-1.5 uppercase tracking-wider">
                <span class="text-base">🏷️</span>
                คำนวณราคายา/สินค้า และ %GP หน้าร้าน
            </h2>
            
            <div class="space-y-3.5">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">💰 ราคาทุนตั้งต้น (บาท)</label>
                    <input type="number" id="s_cost" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore()">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">🏷️ ราคาขาย / ราคาป้าย</label>
                        <input type="number" id="s_price" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore('price')">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">🎯 เป้าหมาย %GP หน้าร้าน</label>
                        <input type="number" id="s_gp" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore('gp')">
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">🎟️ ส่วนลดหน้าร้าน / คูปอง</label>
                        <div class="flex">
                            <input type="number" id="s_disc" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-l-xl focus:ring-2 focus:ring-emerald-500 outline-none font-semibold text-slate-800 text-sm" placeholder="0" oninput="calculateStore()">
                            <select id="s_disc_type" onchange="calculateStore()" class="bg-slate-200 border border-slate-200 rounded-r-xl px-2 text-xs font-bold text-slate-700 outline-none">
                                <option value="percent">%</option>
                                <option value="baht">บาท</option>
                            </select>
                        </div>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">💸 ค่าธรรมเนียมรับชำระ (%)</label>
                        <input type="number" id="s_fee" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" value="0" oninput="calculateStore()">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">🧾 ภาษีมูลค่าเพิ่ม (VAT 7%)</label>
                    <select id="s_vat_type" onchange="calculateStore()" class="w-full p-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold text-slate-700 outline-none">
                        <option value="none">ไม่คิด VAT (ยกเว้น)</option>
                        <option value="exclude">ยังไม่รวม VAT (บวกเพิ่ม 7%)</option>
                        <option value="include">รวม VAT แล้ว (ถอดออก)</option>
                    </select>
                </div>

                <!-- Results Box -->
                <div class="bg-slate-900 text-white p-5 rounded-2xl space-y-3.5 shadow-inner mt-2 border border-slate-800">
                    <div class="flex justify-between items-center border-b border-slate-800 pb-2">
                        <h3 class="text-slate-300 text-xs font-bold uppercase tracking-wider flex items-center gap-1">📊 ผลการคำนวณหน้าร้าน</h3>
                        <span class="px-2.5 py-0.5 bg-emerald-500/20 text-emerald-400 text-[10px] rounded-full font-bold">✨ Retail Store</span>
                    </div>
                    <div class="space-y-2.5 text-xs">
                        <div class="flex justify-between items-center pb-2 border-b border-slate-800">
                            <span class="text-slate-300">💰 ราคาขายหน้าร้านสุทธิ:</span>
                            <span id="res_store_price" class="text-base font-bold text-emerald-400">0.00 บาท</span>
                        </div>
                        <div class="flex justify-between items-center pb-2 border-b border-slate-800">
                            <span class="text-slate-300">💎 กำไรสุทธิเข้ากระเป๋า:</span>
                            <span id="res_store_profit" class="text-sm font-bold text-white">0.00 บาท</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-slate-300">🔥 อัตรากำไรสุทธิ (%GP):</span>
                            <span id="res_store_gp" class="text-sm font-bold text-cyan-400">0.00%</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= PAGE 2: ONLINE CHANNELS ================= -->
        <div id="pageOnline" class="hidden bg-white p-6 rounded-3xl shadow-md border border-slate-200 space-y-4 max-w-md mx-auto">
            <div class="flex flex-col gap-2 border-b pb-3">
                <h2 class="text-xs font-bold text-slate-800 uppercase tracking-wider flex items-center gap-1">🛵 ระบบคำนวณราคาช่องทางออนไลน์</h2>
                <div class="grid grid-cols-2 gap-1.5 bg-slate-100 p-1 rounded-xl">
                    <button onclick="switchOnlineTab('lineman')" id="btnSubLineman" class="py-1.5 text-xs font-bold rounded-lg transition-all bg-amber-500 text-white shadow-sm">🛵 LINE MAN Mart</button>
                    <button onclick="switchOnlineTab('tele')" id="btnSubTele" class="py-1.5 text-xs font-bold rounded-lg transition-all text-slate-600 hover:bg-slate-200">💻 Telepharmacy</button>
                </div>
            </div>

            <div class="space-y-3">
                <div class="p-3 bg-emerald-50 rounded-2xl border border-emerald-100 flex flex-col gap-2">
                    <div class="flex justify-between items-center">
                        <span class="text-[11px] font-bold text-emerald-800 uppercase">🏪 ราคาอ้างอิง (หน้าร้าน):</span>
                        <span class="text-sm font-bold text-emerald-900" id="refStorePriceDisplay">0.00 บาท</span>
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-emerald-700 mb-1">✍️ หรือกรอกราคาเอง:</label>
                        <input type="number" id="manual_ref_price" class="w-full px-3 py-2 bg-white border border-emerald-200 rounded-xl text-xs outline-none font-bold text-emerald-900" placeholder="0.00" oninput="calculateOnlineChannels()">
                    </div>
                </div>

                <div class="p-3 bg-amber-50 rounded-2xl border border-amber-100 flex flex-col gap-2">
                    <span class="text-[11px] font-bold text-amber-800 uppercase">🏷️ ส่วนลดเพิ่มเติมสำหรับออนไลน์</span>
                    <div class="flex gap-2">
                        <input type="number" id="online_disc" class="w-full px-3 py-2 bg-white border border-amber-200 rounded-xl text-xs outline-none font-bold text-amber-900" placeholder="0" oninput="calculateOnlineChannels()">
                        <select id="online_disc_type" onchange="calculateOnlineChannels()" class="bg-amber-200 border border-amber-200 rounded-xl px-2.5 text-xs font-bold text-amber-900 outline-none">
                            <option value="baht">บาท (-)</option>
                            <option value="percent">% (-)</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- SUB-TAB 1: LINE MAN -->
            <div id="subTabLineman" class="space-y-3">
                <div class="p-2.5 bg-amber-50 rounded-xl border border-amber-200 text-[11px] text-amber-900 font-semibold text-center">
                    🛵 LINE MAN Mart (ราคาหน้าร้าน × 1.38) | หัก GP 32.1%
                </div>
                <div class="space-y-3">
                    <div class="bg-slate-900 text-white p-4 rounded-2xl space-y-2 border border-slate-800">
                        <div class="text-[11px] font-bold text-amber-400 uppercase">1. ราคาหลังหักส่วนลด (มีเศษ)</div>
                        <div class="text-base font-bold text-white" id="lm_dec_price">0.00 บาท</div>
                        <div class="text-[11px] text-slate-400 pt-1 border-t border-slate-800 flex justify-between">
                            <span>ค่า GP LINE MAN:</span>
                            <span id="lm_dec_gp_amt" class="text-rose-400 font-bold">0.00 บาท</span>
                        </div>
                    </div>
                    <div class="bg-emerald-900 text-white p-4 rounded-2xl space-y-2 border border-emerald-500">
                        <div class="text-[11px] font-bold text-emerald-300 uppercase">2. ราคาหลังปัดเศษจำนวนเต็ม</div>
                        <div class="text-lg font-bold text-emerald-300" id="lm_round_price">0 บาท</div>
                        <div class="text-[11px] text-emerald-200 pt-1 border-t border-emerald-800 flex justify-between">
                            <span>กำไรสุทธิหลังหัก GP:</span>
                            <span id="lm_round_profit" class="text-cyan-300 font-bold">0.00 บาท</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- SUB-TAB 2: TELEPHARMACY -->
            <div id="subTabTele" class="hidden space-y-3">
                <div class="p-2.5 bg-blue-50 rounded-xl border border-blue-200 text-[11px] text-blue-900 font-semibold text-center">
                    💻 Telepharmacy (ราคาหน้าร้าน × 1.48) | หัก GP 37.45%
                </div>
                <div class="space-y-3">
                    <div class="bg-slate-900 text-white p-4 rounded-2xl space-y-2 border border-slate-800">
                        <div class="text-[11px] font-bold text-blue-400 uppercase">1. ราคาหลังหักส่วนลด (มีเศษ)</div>
                        <div class="text-base font-bold text-white" id="tele_dec_price">0.00 บาท</div>
                        <div class="text-[11px] text-slate-400 pt-1 border-t border-slate-800 flex justify-between">
                            <span>ค่า GP Telepharmacy:</span>
                            <span id="tele_dec_gp_amt" class="text-rose-400 font-bold">0.00 บาท</span>
                        </div>
                    </div>
                    <div class="bg-blue-950 text-white p-4 rounded-2xl space-y-2 border border-blue-500">
                        <div class="text-[11px] font-bold text-blue-300 uppercase">2. ราคาหลังปัดเศษจำนวนเต็ม</div>
                        <div class="text-lg font-bold text-blue-300" id="tele_round_price">0 บาท</div>
                        <div class="text-[11px] text-blue-200 pt-1 border-t border-slate-800 flex justify-between">
                            <span>กำไรสุทธิหลังหัก GP:</span>
                            <span id="tele_round_profit" class="text-cyan-300 font-bold">0.00 บาท</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= PAGE 3: CREDIT CARD & INSTALLMENT (WITH EXPORT & PRINT) ================= -->
        <div id="pageCredit" class="hidden bg-white p-6 rounded-3xl shadow-md border border-slate-200 space-y-4">
            
            <!-- พื้นที่สำหรับสั่งพิมพ์และ Export -->
            <div id="printableArea" class="space-y-4">
                
                <div class="flex justify-between items-center border-b pb-3">
                    <div>
                        <h2 class="text-xs font-bold text-slate-800 uppercase tracking-wider flex items-center gap-1">💳 วิเคราะห์ต้นทุนซื้อสินค้าผ่านบัตรเครดิต / ผ่อนชำระ</h2>
                        <p class="text-[10px] text-slate-500">✨ บันทึกวิเคราะห์การสั่งซื้อและผ่อนชำระสินค้า 📊</p>
                    </div>
                    <!-- ปุ่ม Export และ Print (ซ่อนเวลาสั่งพิมพ์จริง) -->
                    <div class="flex gap-1.5 no-print">
                        <button onclick="exportToCSV()" class="px-3 py-1.5 bg-emerald-600 hover:bg-emerald-700 text-white text-[11px] font-bold rounded-xl shadow-sm flex items-center gap-1 transition-all">
                            📥 Export CSV
                        </button>
                        <button onclick="window.print()" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-900 text-white text-[11px] font-bold rounded-xl shadow-sm flex items-center gap-1 transition-all">
                            🖨️ พิมพ์รายงาน
                        </button>
                    </div>
                </div>

                <!-- ข้อมูลผู้จำหน่ายและเลขที่บิลเพิ่มเติม -->
                <div class="grid grid-cols-2 gap-3 no-print bg-slate-50 p-3 rounded-2xl border border-slate-200">
                    <div>
                        <label class="block text-[11px] font-bold text-slate-700 mb-1">🏢 ชื่อผู้จำหน่าย / บริษัทเซลล์</label>
                        <input type="text" id="c_supplier" class="w-full px-3 py-1.5 bg-white border border-slate-200 rounded-xl text-xs outline-none font-semibold text-slate-800" placeholder="เช่น บริษัท ดีเคเอสเอช จำกัด">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-slate-700 mb-1">📄 เลขที่ใบเสนอราคา / บิล</label>
                        <input type="text" id="c_bill_no" class="w-full px-3 py-1.5 bg-white border border-slate-200 rounded-xl text-xs outline-none font-semibold text-slate-800" placeholder="เช่น INV-2026-001">
                    </div>
                </div>

                <!-- ตั้งค่าส่วนกลางของบิล -->
                <div class="grid grid-cols-3 gap-3 p-3 bg-indigo-50/50 rounded-2xl border border-indigo-100">
                    <div>
                        <label class="block text-[11px] font-bold text-indigo-900 mb-1">💳 ค่าธรรมเนียมรูด (%)</label>
                        <input type="number" id="c_card_fee" class="w-full px-3 py-2 bg-white border border-indigo-200 rounded-xl font-bold text-indigo-900 outline-none text-xs" value="1.00" oninput="renderBillRows()">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-indigo-900 mb-1">📈 ดอกเบี้ยผ่อน/เดือน (%)</label>
                        <input type="number" id="c_interest_rate" class="w-full px-3 py-2 bg-white border border-indigo-200 rounded-xl font-bold text-indigo-900 outline-none text-xs" value="0.74" oninput="renderBillRows()">
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-indigo-900 mb-1">🏷️ ส่วนลดบิล (บริษัท)</label>
                        <div class="flex">
                            <input type="number" id="c_bill_disc" class="w-full px-2 py-2 bg-white border border-indigo-200 rounded-l-xl font-bold text-indigo-900 outline-none text-xs" value="0" placeholder="ส่วนลด" oninput="renderBillRows()">
                            <select id="c_bill_disc_type" onchange="renderBillRows()" class="bg-indigo-100 border border-indigo-200 rounded-r-xl px-1.5 text-[11px] font-bold text-indigo-900 outline-none">
                                <option value="baht">บาท</option>
                                <option value="percent">%</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- ตารางรายการสินค้าแบบกว้าง -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center">
                        <span class="text-xs font-bold text-slate-700 flex items-center gap-1">📋 ตารางวิเคราะห์แยกรายสินค้าและงวดผ่อน</span>
                        <button onclick="addBillRow()" class="px-3 py-1 bg-indigo-600 text-white text-[11px] font-bold rounded-xl shadow-sm hover:bg-indigo-700 no-print transition-all">+ เพิ่มรายการยา/สินค้า</button>
                    </div>

                    <div class="overflow-x-auto border border-slate-200 rounded-2xl">
                        <table class="w-full text-left text-xs whitespace-nowrap">
                            <thead class="bg-slate-50 text-slate-700 font-bold border-b border-slate-200">
                                <tr>
                                    <th class="p-2.5">ชื่อสินค้า / ยา</th>
                                    <th class="p-2.5 text-center w-16">จำนวน</th>
                                    <th class="p-2.5 text-right w-24">ทุนตั้งต้น (รวม)</th>
                                    <th class="p-2.5 text-right w-24 text-indigo-600">รวมค่ารูดบัตร</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 3 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 4 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 6 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 8 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 9 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 10 ด.</th>
                                    <th class="p-2.5 text-right w-24">ผ่อน 12 ด.</th>
                                    <th class="p-2.5 text-center w-10 no-print">ลบ</th>
                                </tr>
                            </thead>
                            <tbody id="billItemsContainer" class="divide-y divide-slate-100 font-medium text-slate-800">
                                <!-- Rows injected by JS -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- สรุปยอดรวมทั้งบิล -->
                <div class="p-4 bg-indigo-900 text-white rounded-2xl space-y-2 shadow-inner border border-indigo-800">
                    <div class="flex justify-between items-center text-xs border-b border-indigo-800 pb-2">
                        <span class="text-indigo-200 font-bold">✨ สรุปยอดรวมทั้งบิล (หลังหักส่วนลดและคิดค่าธรรมเนียมแล้ว):</span>
                        <span id="bill_total_net" class="font-extrabold text-amber-400 text-sm">0.00 บาท</span>
                    </div>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-2 pt-1 text-[11px] text-indigo-200">
                        <div>ทุนตั้งต้นรวม: <span id="bill_total_base" class="text-white font-bold">0.00</span></div>
                        <div>หลังหักส่วนลด: <span id="bill_total_after_disc" class="text-white font-bold">0.00</span></div>
                        <div>ค่าธรรมเนียมรูด: <span id="bill_total_fee_amt" class="text-white font-bold">0.00</span></div>
                        <div>สถานะส่วนลด: <span id="bill_disc_status" class="text-emerald-300 font-bold">ไม่มีส่วนลด</span></div>
                    </div>
                </div>

                <!-- ส่วนสรุปผลการผ่อนชำระแยกตามจำนวนเดือน -->
                <div class="p-4 bg-slate-900 text-white rounded-2xl space-y-3 border border-slate-800 shadow-sm">
                    <div class="text-xs font-bold text-amber-400 uppercase flex items-center gap-1.5 border-b border-slate-800 pb-2">
                        <span>📊 สรุปยอดรวมและค่างวดรายเดือน สำหรับการตัดสินใจผ่อนชำระ</span>
                    </div>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-3 text-xs" id="installmentSummaryGrid">
                        <!-- Injected by JS -->
                    </div>
                </div>

            </div>

        </div>

    </div>

    <script>
        let currentStoreNetPrice = 0;
        let currentStoreCost = 0;

        let billItems = [
            { name: "Amoxycillin 500mg", cost: 600, qty: 10 },
            { name: "Paracetamol 500mg", cost: 250, qty: 20 }
        ];

        window.onload = function() { 
            calculateStore(); 
            renderBillRows();
        };

        function switchMainTab(tab) {
            const pageStore = document.getElementById('pageStore');
            const pageOnline = document.getElementById('pageOnline');
            const pageCredit = document.getElementById('pageCredit');
            
            const btnMainStore = document.getElementById('btnMainStore');
            const btnMainOnline = document.getElementById('btnMainOnline');
            const btnMainCredit = document.getElementById('btnMainCredit');

            btnMainStore.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200 flex items-center justify-center gap-1";
            btnMainOnline.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200 flex items-center justify-center gap-1";
            btnMainCredit.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200 flex items-center justify-center gap-1";

            pageStore.classList.add('hidden');
            pageOnline.classList.add('hidden');
            pageCredit.classList.add('hidden');

            if (tab === 'store') {
                pageStore.classList.remove('hidden');
                btnMainStore.className = "py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm flex items-center justify-center gap-1";
            } else if (tab === 'online') {
                pageOnline.classList.remove('hidden');
                btnMainOnline.className = "py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm flex items-center justify-center gap-1";
                
                document.getElementById('refStorePriceDisplay').innerText = currentStoreNetPrice.toFixed(2) + " บาท";
                if(!document.getElementById('manual_ref_price').value && currentStoreNetPrice > 0) {
                    document.getElementById('manual_ref_price').value = currentStoreNetPrice.toFixed(2);
                }
                calculateOnlineChannels();
            } else if (tab === 'credit') {
                pageCredit.classList.remove('hidden');
                btnMainCredit.className = "py-2 text-xs font-bold rounded-xl transition-all bg-indigo-600 text-white shadow-sm flex items-center justify-center gap-1";
            }
        }

        function switchOnlineTab(sub) {
            const subTabLineman = document.getElementById('subTabLineman');
            const subTabTele = document.getElementById('subTabTele');
            const btnSubLineman = document.getElementById('btnSubLineman');
            const btnSubTele = document.getElementById('btnSubTele');

            if (sub === 'lineman') {
                subTabLineman.classList.remove('hidden');
                subTabTele.classList.add('hidden');
                btnSubLineman.className = "py-1.5 text-xs font-bold rounded-lg transition-all bg-amber-500 text-white shadow-sm";
                btnSubTele.className = "py-1.5 text-xs font-bold rounded-lg transition-all text-slate-600 hover:bg-slate-200";
            } else {
                subTabLineman.classList.add('hidden');
                subTabTele.classList.remove('hidden');
                btnSubTele.className = "py-1.5 text-xs font-bold rounded-lg transition-all bg-blue-600 text-white shadow-sm";
                btnSubLineman.className = "py-1.5 text-xs font-bold rounded-lg transition-all text-slate-600 hover:bg-slate-200";
            }
        }

        function renderBillRows() {
            const container = document.getElementById('billItemsContainer');
            container.innerHTML = "";
            
            const cardFeePercent = parseFloat(document.getElementById('c_card_fee').value) || 0;
            const interestPerMonth = parseFloat(document.getElementById('c_interest_rate').value) || 0;
            const billDiscVal = parseFloat(document.getElementById('c_bill_disc').value) || 0;
            const billDiscType = document.getElementById('c_bill_disc_type').value;

            let totalBaseAmount = 0;
            billItems.forEach(item => {
                totalBaseAmount += (item.cost * item.qty);
            });

            let totalDiscountAmount = 0;
            if (billDiscVal > 0) {
                totalDiscountAmount = (billDiscType === 'percent') ? totalBaseAmount * (billDiscVal / 100) : billDiscVal;
            }
            let netBaseAfterDisc = Math.max(0, totalBaseAmount - totalDiscountAmount);
            let discountRatio = totalBaseAmount > 0 ? (netBaseAfterDisc / totalBaseAmount) : 1;

            let grandTotalNet = 0;
            let grandTotalFee = 0;

            let summaryMonths = [3, 4, 6, 8, 9, 10, 12];
            let installmentTotals = {};
            summaryMonths.forEach(m => installmentTotals[m] = 0);

            billItems.forEach((item, index) => {
                let itemBaseTotal = item.cost * item.qty;
                let itemNetBase = itemBaseTotal * discountRatio;
                let itemCardFee = itemNetBase * (cardFeePercent / 100);
                let itemTotalWithFee = itemNetBase + itemCardFee;

                grandTotalNet += itemTotalWithFee;
                grandTotalFee += itemCardFee;

                let getInstallment = (m) => {
                    let totalInterestPercent = interestPerMonth * m;
                    let interestAmt = itemNetBase * (totalInterestPercent / 100);
                    let totalWithInterest = itemNetBase + itemCardFee + interestAmt;
                    installmentTotals[m] += totalWithInterest;
                    return totalWithInterest.toFixed(2);
                };

                let row = `<tr class="hover:bg-slate-50">
                    <td class="p-2">
                        <input type="text" value="${item.name}" oninput="updateBillItem(${index}, 'name', this.value)" class="w-full px-2 py-1 bg-slate-50 border border-slate-200 rounded-lg text-xs outline-none focus:bg-white" placeholder="ชื่อยา/สินค้า">
                    </td>
                    <td class="p-2">
                        <input type="number" value="${item.qty}" oninput="updateBillItem(${index}, 'qty', this.value)" class="w-full px-2 py-1 bg-slate-50 border border-slate-200 rounded-lg text-xs outline-none text-center font-bold focus:bg-white" placeholder="1">
                    </td>
                    <td class="p-2">
                        <input type="number" value="${item.cost}" oninput="updateBillItem(${index}, 'cost', this.value)" class="w-full px-2 py-1 bg-slate-50 border border-slate-200 rounded-lg text-xs outline-none text-right font-bold focus:bg-white" placeholder="0.00">
                    </td>
                    <td class="p-2 text-right font-bold text-indigo-600">${itemTotalWithFee.toFixed(2)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(3)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(4)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(6)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(8)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(9)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(10)}</td>
                    <td class="p-2 text-right text-slate-700">${getInstallment(12)}</td>
                    <td class="p-2 text-center no-print">
                        <button onclick="removeBillRow(${index})" class="text-rose-500 hover:text-rose-700 font-bold px-1.5 py-0.5 rounded">✕</button>
                    </td>
                </tr>`;
                container.innerHTML += row;
            });

            document.getElementById('bill_total_base').innerText = totalBaseAmount.toFixed(2) + " บาท";
            document.getElementById('bill_total_after_disc').innerText = netBaseAfterDisc.toFixed(2) + " บาท";
            document.getElementById('bill_total_fee_amt').innerText = grandTotalFee.toFixed(2) + " บาท";
            document.getElementById('bill_total_net').innerText = grandTotalNet.toFixed(2) + " บาท";
            document.getElementById('bill_disc_status').innerText = billDiscVal > 0 ? `ลด ${billDiscVal} ${billDiscType === 'percent' ? '%' : 'บาท'}` : "ไม่มีส่วนลด";

            const sumGrid = document.getElementById('installmentSummaryGrid');
            sumGrid.innerHTML = "";
            summaryMonths.forEach(m => {
                let totalAmt = installmentTotals[m];
                let perMonthAmt = totalAmt / m;
                sumGrid.innerHTML += `
                    <div class="bg-slate-800 p-3 rounded-xl border border-slate-700 space-y-1">
                        <div class="text-slate-400 font-bold">ผ่อน ${m} เดือน</div>
                        <div class="text-white font-bold text-sm">${perMonthAmt.toFixed(2)} <span class="text-[10px] text-slate-400">บาท/เดือน</span></div>
                        <div class="text-[10px] text-indigo-300 pt-1 border-t border-slate-700 flex justify-between">
                            <span>รวมทั้งหมด:</span>
                            <span class="font-semibold">${totalAmt.toFixed(2)} ฿</span>
                        </div>
                    </div>
                `;
            });
        }

        function addBillRow() {
            billItems.push({ name: "", cost: 0, qty: 1 });
            renderBillRows();
        }

        function removeBillRow(index) {
            billItems.splice(index, 1);
            renderBillRows();
        }

        function updateBillItem(index, field, value) {
            if (field === 'cost' || field === 'qty') {
                billItems[index][field] = parseFloat(value) || 0;
            } else {
                billItems[index][field] = value;
            }
            renderBillRows();
        }

        function exportToCSV() {
            let supplier = document.getElementById('c_supplier').value || "ไม่ระบุผู้จำหน่าย";
            let billNo = document.getElementById('c_bill_no').value || "ไม่ระบุเลขบิล";
            
            let csvContent = "\uFEFF";
            csvContent += `ผู้จำหน่าย: ${supplier}, เลขที่บิล: ${billNo}\n`;
            csvContent += "ชื่อสินค้า,จำนวน,ราคาทุนรวม,ราคารวมค่ารูดบัตร,ผ่อน 3 ด.,ผ่อน 4 ด.,ผ่อน 6 ด.,ผ่อน 8 ด.,ผ่อน 9 ด.,ผ่อน 10 ด.,ผ่อน 12 ด.\n";

            const cardFeePercent = parseFloat(document.getElementById('c_card_fee').value) || 0;
            const interestPerMonth = parseFloat(document.getElementById('c_interest_rate').value) || 0;
            const billDiscVal = parseFloat(document.getElementById('c_bill_disc').value) || 0;
            const billDiscType = document.getElementById('c_bill_disc_type').value;

            let totalBaseAmount = 0;
            billItems.forEach(item => totalBaseAmount += (item.cost * item.qty));
            let totalDiscountAmount = (billDiscVal > 0) ? (billDiscType === 'percent' ? totalBaseAmount * (billDiscVal / 100) : billDiscVal) : 0;
            let netBaseAfterDisc = Math.max(0, totalBaseAmount - totalDiscountAmount);
            let discountRatio = totalBaseAmount > 0 ? (netBaseAfterDisc / totalBaseAmount) : 1;

            billItems.forEach(item => {
                let itemBaseTotal = item.cost * item.qty;
                let itemNetBase = itemBaseTotal * discountRatio;
                let itemCardFee = itemNetBase * (cardFeePercent / 100);
                let itemTotalWithFee = itemNetBase + itemCardFee;

                let getInst = (m) => (itemNetBase + itemCardFee + (itemNetBase * (interestPerMonth * m) / 100)).toFixed(2);

                let rowString = `"${item.name}",${item.qty},${itemBaseTotal.toFixed(2)},${itemTotalWithFee.toFixed(2)},${getInst(3)},${getInst(4)},${getInst(6)},${getInst(8)},${getInst(9)},${getInst(10)},${getInst(12)}`;
                csvContent += rowString + "\n";
            });

            let encodedUri = encodeURI("data:text/csv;charset=utf-8," + csvContent);
            let link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `credit_analysis_${billNo}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function calculateStore(source) {
            const cost = parseFloat(document.getElementById('s_cost').value) || 0;
            let price = parseFloat(document.getElementById('s_price').value) || 0;
            let targetGp = parseFloat(document.getElementById('s_gp').value) || 0;
            const discValue = parseFloat(document.getElementById('s_disc').value) || 0;
            const discType = document.getElementById('s_disc_type').value;
            const feePercent = parseFloat(document.getElementById('s_fee').value) || 0;
            const vatType = document.getElementById('s_vat_type').value;

            currentStoreCost = cost;
            let listPrice = price;
            let calculatedProfit = 0;
            let calculatedGp = 0;
            let discAmount = 0;
            let feeAmount = 0;

            if (cost > 0) {
                if (source === 'gp' && targetGp > 0 && targetGp < 100) {
                    listPrice = cost / (1 - (targetGp / 100));
                    document.getElementById('s_price').value = listPrice.toFixed(2);
                } else if (source === 'price' && price > 0) {
                    if (price >= cost) {
                        calculatedGp = ((price - cost) / price) * 100;
                        document.getElementById('s_gp').value = calculatedGp.toFixed(2);
                    }
                    listPrice = price;
                } else if (!source && price > 0) {
                    calculatedGp = ((price - cost) / price) * 100;
                    document.getElementById('s_gp').value = calculatedGp.toFixed(2);
                    listPrice = price;
                }

                if (discValue > 0) {
                    discAmount = (discType === 'percent') ? listPrice * (discValue / 100) : discValue;
                }

                let finalSellingPrice = Math.max(0, listPrice - discAmount);

                if (feePercent > 0) {
                    feeAmount = finalSellingPrice * (feePercent / 100);
                }

                let basePriceForProfit = finalSellingPrice - feeAmount;

                if (vatType === 'include') {
                    basePriceForProfit = (finalSellingPrice / 1.07) - feeAmount;
                }

                calculatedProfit = basePriceForProfit - cost;
                if (basePriceForProfit > 0) {
                    calculatedGp = (calculatedProfit / basePriceForProfit) * 100;
                }

                currentStoreNetPrice = finalSellingPrice;

                document.getElementById('res_store_price').innerText = finalSellingPrice.toFixed(2) + " บาท";
                document.getElementById('res_store_profit').innerText = calculatedProfit.toFixed(2) + " บาท";
                document.getElementById('res_store_gp').innerText = calculatedGp.toFixed(2) + "%";
            } else {
                currentStoreNetPrice = 0;
                document.getElementById('res_store_price').innerText = "0.00 บาท";
                document.getElementById('res_store_profit').innerText = "0.00 บาท";
                document.getElementById('res_store_gp').innerText = "0.00%";
            }
        }

        function calculateOnlineChannels() {
            let baseRef = parseFloat(document.getElementById('manual_ref_price').value) || currentStoreNetPrice;
            let onlineDiscVal = parseFloat(document.getElementById('online_disc').value) || 0;
            let onlineDiscType = document.getElementById('online_disc_type').value;

            function applyDiscount(rawPrice) {
                let discountAmt = 0;
                if (onlineDiscVal > 0) {
                    discountAmt = (onlineDiscType === 'percent') ? rawPrice * (onlineDiscVal / 100) : onlineDiscVal;
                }
                return Math.max(0, rawPrice - discountAmt);
            }

            let lmRawPrice = baseRef * 1.38;
            let lmDecPrice = applyDiscount(lmRawPrice);
            let lmRoundPrice = Math.round(lmDecPrice);
            let lmGpAmt = lmRoundPrice * 0.321;
            let lmProfit = lmRoundPrice - lmGpAmt - currentStoreCost;

            document.getElementById('lm_dec_price').innerText = lmDecPrice.toFixed(2) + " บาท";
            document.getElementById('lm_dec_gp_amt').innerText = "-" + (lmRoundPrice * 0.321).toFixed(2) + " บาท";
            document.getElementById('lm_round_price').innerText = lmRoundPrice.toLocaleString() + " บาท";
            document.getElementById('lm_round_profit').innerText = (currentStoreCost > 0 ? lmProfit.toFixed(2) + " บาท" : "กรุณากรอกราคาทุน");

            let teleRawPrice = baseRef * 1.48;
            let teleDecPrice = applyDiscount(teleRawPrice);
            let teleRoundPrice = Math.round(teleDecPrice);
            let teleGpAmt = teleRoundPrice * 0.3745;
            let teleProfit = teleRoundPrice - teleGpAmt - currentStoreCost;

            document.getElementById('tele_dec_price').innerText = teleDecPrice.toFixed(2) + " บาท";
            document.getElementById('tele_dec_gp_amt').innerText = "-" + (teleRoundPrice * 0.3745).toFixed(2) + " บาท";
            document.getElementById('tele_round_price').innerText = teleRoundPrice.toLocaleString() + " บาท";
            document.getElementById('tele_round_profit').innerText = (currentStoreCost > 0 ? teleProfit.toFixed(2) + " บาท" : "กรุณากรอกราคาทุน");
        }
    </script>
</body>
</html>
