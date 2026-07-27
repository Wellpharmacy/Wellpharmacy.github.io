<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบจัดการราคาขายและต้นทุน</title>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <style> body { font-family: 'Sarabun', sans-serif; } </style>
</head>
<body class="bg-slate-100 min-h-screen py-6 px-4 flex justify-center">
    
    <!-- บีบความกว้างไม่ให้ยืดกว้างเกินไปบนจอคอม ให้แสดงผลเป็นทรงมือถือสวยๆ -->
    <div class="w-full max-w-md space-y-4">
        
        <!-- Header & Main Navigation Tabs -->
        <div class="bg-white p-5 rounded-3xl shadow-sm border border-slate-200 space-y-4">
            <div class="text-center space-y-1">
                <h1 class="text-base font-bold text-slate-800 flex items-center justify-center gap-1.5">
                    <svg class="w-5 h-5 text-emerald-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"></path></svg>
                    ระบบจัดการราคาและต้นทุน
                </h1>
                <p class="text-[11px] text-slate-500">คำนวณหน้าร้าน, ช่องทางออนไลน์ และวิเคราะห์ต้นทุนซื้อผ่านบัตรเครดิต/ผ่อนชำระ</p>
            </div>
            <div class="grid grid-cols-3 gap-1 bg-slate-100 p-1.5 rounded-2xl">
                <button onclick="switchMainTab('store')" id="btnMainStore" class="py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm">🏪 หน้าร้าน</button>
                <button onclick="switchMainTab('online')" id="btnMainOnline" class="py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200">🛵 ออนไลน์</button>
                <button onclick="switchMainTab('credit')" id="btnMainCredit" class="py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200">💳 วิเคราะห์บัตร</button>
            </div>
        </div>

        <!-- ================= PAGE 1: STORE CALCULATOR ================= -->
        <div id="pageStore" class="bg-white p-6 rounded-3xl shadow-sm border border-slate-200 space-y-4">
            <h2 class="text-xs font-bold text-slate-800 border-b pb-3 flex items-center gap-1.5 uppercase tracking-wider">
                <svg class="w-4 h-4 text-emerald-600" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path></svg>
                คำนวณราคายา/สินค้า และ %GP หน้าร้าน
            </h2>
            
            <div class="space-y-3.5">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">ราคาทุนตั้งต้น (บาท)</label>
                    <input type="number" id="s_cost" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore()">
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">ราคาขาย / ราคาป้าย</label>
                        <input type="number" id="s_price" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore('price')">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">เป้าหมาย %GP หน้าร้าน</label>
                        <input type="number" id="s_gp" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:bg-white outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" oninput="calculateStore('gp')">
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">ส่วนลดหน้าร้าน / คูปอง</label>
                        <div class="flex">
                            <input type="number" id="s_disc" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-l-xl focus:ring-2 focus:ring-emerald-500 outline-none font-semibold text-slate-800 text-sm" placeholder="0" oninput="calculateStore()">
                            <select id="s_disc_type" onchange="calculateStore()" class="bg-slate-200 border border-slate-200 rounded-r-xl px-2 text-xs font-bold text-slate-700 outline-none">
                                <option value="percent">%</option>
                                <option value="baht">บาท</option>
                            </select>
                        </div>
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">ค่าธรรมเนียมรับชำระ (%)</label>
                        <input type="number" id="s_fee" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500 outline-none font-semibold text-slate-800 text-sm" placeholder="0.00" value="0" oninput="calculateStore()">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">ภาษีมูลค่าเพิ่ม (VAT 7%)</label>
                    <select id="s_vat_type" onchange="calculateStore()" class="w-full p-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold text-slate-700 outline-none">
                        <option value="none">ไม่คิด VAT (ยกเว้น)</option>
                        <option value="exclude">ยังไม่รวม VAT (บวกเพิ่ม 7%)</option>
                        <option value="include">รวม VAT แล้ว (ถอดออก)</option>
                    </select>
                </div>

                <!-- Results Box -->
                <div class="bg-slate-900 text-white p-5 rounded-2xl space-y-3.5 shadow-inner mt-2">
                    <div class="flex justify-between items-center border-b border-slate-800 pb-2">
                        <h3 class="text-slate-400 text-xs font-bold uppercase tracking-wider">ผลการคำนวณหน้าร้าน</h3>
                        <span class="px-2 py-0.5 bg-emerald-500/20 text-emerald-400 text-[10px] rounded-full font-bold">Retail Store</span>
                    </div>
                    <div class="space-y-2.5 text-xs">
                        <div class="flex justify-between items-center pb-2 border-b border-slate-800">
                            <span class="text-slate-300">ราคาขายหน้าร้านสุทธิ:</span>
                            <span id="res_store_price" class="text-base font-bold text-emerald-400">0.00 บาท</span>
                        </div>
                        <div class="flex justify-between items-center pb-2 border-b border-slate-800">
                            <span class="text-slate-300">กำไรสุทธิเข้ากระเป๋า:</span>
                            <span id="res_store_profit" class="text-sm font-bold text-white">0.00 บาท</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-slate-300">อัตรากำไรสุทธิ (%GP):</span>
                            <span id="res_store_gp" class="text-sm font-bold text-cyan-400">0.00%</span>
                        </div>
                    </div>
                    <div class="p-2 bg-slate-800 rounded-xl text-[11px] text-slate-300 text-center">
                        💡 ราคานี้จะลิงก์ไปหน้าออนไลน์อัตโนมัติ
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= PAGE 2: ONLINE CHANNELS ================= -->
        <div id="pageOnline" class="hidden bg-white p-6 rounded-3xl shadow-sm border border-slate-200 space-y-4">
            <div class="flex flex-col gap-2 border-b pb-3">
                <h2 class="text-xs font-bold text-slate-800 uppercase tracking-wider">🛵 ระบบคำนวณราคาช่องทางออนไลน์</h2>
                <div class="grid grid-cols-2 gap-1.5 bg-slate-100 p-1 rounded-xl">
                    <button onclick="switchOnlineTab('lineman')" id="btnSubLineman" class="py-1.5 text-xs font-bold rounded-lg transition-all bg-amber-500 text-white shadow-sm">LINE MAN Mart</button>
                    <button onclick="switchOnlineTab('tele')" id="btnSubTele" class="py-1.5 text-xs font-bold rounded-lg transition-all text-slate-600 hover:bg-slate-200">Telepharmacy</button>
                </div>
            </div>

            <div class="space-y-3">
                <div class="p-3 bg-emerald-50 rounded-2xl border border-emerald-100 flex flex-col gap-2">
                    <div class="flex justify-between items-center">
                        <span class="text-[11px] font-bold text-emerald-800 uppercase">ราคาอ้างอิง (หน้าร้าน):</span>
                        <span class="text-sm font-bold text-emerald-900" id="refStorePriceDisplay">0.00 บาท</span>
                    </div>
                    <div>
                        <label class="block text-[11px] font-bold text-emerald-700 mb-1">หรือกรอกราคาเอง:</label>
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
                    <div class="bg-slate-900 text-white p-4 rounded-2xl space-y-2">
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
                    <div class="bg-slate-900 text-white p-4 rounded-2xl space-y-2">
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

        <!-- ================= PAGE 3: CREDIT CARD & INSTALLMENT ================= -->
        <div id="pageCredit" class="hidden bg-white p-6 rounded-3xl shadow-sm border border-slate-200 space-y-4">
            <h2 class="text-xs font-bold text-slate-800 border-b pb-3 uppercase tracking-wider">💳 วิเคราะห์ต้นทุนซื้อสินค้าผ่านบัตรเครดิต / ผ่อนชำระ</h2>
            
            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">ราคาสินค้าตั้งต้น (บาท)</label>
                    <input type="number" id="c_base_cost" class="w-full px-3.5 py-2.5 bg-slate-50 border border-slate-200 rounded-xl font-bold text-slate-800 outline-none focus:ring-2 focus:ring-indigo-500 text-sm" placeholder="60.00" value="60" oninput="calculateCreditCost()">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">ค่าธรรมเนียมรูด (%)</label>
                        <input type="number" id="c_card_fee" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl font-bold text-slate-800 outline-none focus:ring-2 focus:ring-indigo-500 text-sm" placeholder="1.00" value="1.00" oninput="calculateCreditCost()">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-600 mb-1">ดอกเบี้ยผ่อน/เดือน (%)</label>
                        <input type="number" id="c_interest_rate" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl font-bold text-slate-800 outline-none focus:ring-2 focus:ring-indigo-500 text-sm" placeholder="0.74" value="0.74" oninput="calculateCreditCost()">
                    </div>
                </div>
            </div>

            <div class="p-4 bg-indigo-50 rounded-2xl border border-indigo-100 space-y-3">
                <div class="flex flex-col gap-1.5">
                    <span class="text-xs font-bold text-indigo-900">เลือกจำนวนเดือนที่ต้องการผ่อน:</span>
                    <select id="c_selected_months" onchange="calculateCreditCost()" class="w-full px-3 py-2 bg-white border border-indigo-200 rounded-xl text-xs font-bold text-indigo-900 outline-none">
                        <option value="3">3 เดือน</option>
                        <option value="4">4 เดือน</option>
                        <option value="6" selected>6 เดือน</option>
                        <option value="10">10 เดือน</option>
                        <option value="12">12 เดือน</option>
                    </select>
                </div>
                <div class="bg-white p-3 rounded-xl border border-indigo-100 text-center space-y-1">
                    <div class="text-[11px] font-bold text-slate-500">ต้นทุนใหม่ต่อหน่วย (งวดที่เลือก):</div>
                    <div class="text-lg font-extrabold text-indigo-600" id="c_res_total_cost">0.00 บาท</div>
                    <div class="text-[10px] text-slate-400" id="c_res_monthly_pay">ผ่อนชำระเดือนละ 0.00 บาท</div>
                </div>
            </div>

            <div class="space-y-2">
                <h3 class="text-xs font-bold text-slate-700 uppercase tracking-wider">📊 ตารางเปรียบเทียบทุกระยะเวลา</h3>
                <div class="overflow-x-auto border border-slate-200 rounded-2xl">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-50 text-slate-700 font-bold border-b border-slate-200">
                            <tr>
                                <th class="p-2.5">รูปแบบ</th>
                                <th class="p-2.5 text-right">ยอดรวม</th>
                                <th class="p-2.5 text-right">ต่อเดือน</th>
                                <th class="p-2.5 text-right">ต้นทุนใหม่</th>
                            </tr>
                        </thead>
                        <tbody id="c_table_body" class="divide-y divide-slate-100 font-medium text-slate-800">
                            <!-- Populated by JS -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </div>

    <script>
        let currentStoreNetPrice = 0;
        let currentStoreCost = 0;

        window.onload = function() { 
            calculateStore(); 
            calculateCreditCost();
        };

        function switchMainTab(tab) {
            const pageStore = document.getElementById('pageStore');
            const pageOnline = document.getElementById('pageOnline');
            const pageCredit = document.getElementById('pageCredit');
            
            const btnMainStore = document.getElementById('btnMainStore');
            const btnMainOnline = document.getElementById('btnMainOnline');
            const btnMainCredit = document.getElementById('btnMainCredit');

            btnMainStore.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200";
            btnMainOnline.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200";
            btnMainCredit.className = "py-2 text-xs font-bold rounded-xl transition-all text-slate-600 hover:bg-slate-200";

            pageStore.classList.add('hidden');
            pageOnline.classList.add('hidden');
            pageCredit.classList.add('hidden');

            if (tab === 'store') {
                pageStore.classList.remove('hidden');
                btnMainStore.className = "py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm";
            } else if (tab === 'online') {
                pageOnline.classList.remove('hidden');
                btnMainOnline.className = "py-2 text-xs font-bold rounded-xl transition-all bg-emerald-600 text-white shadow-sm";
                
                document.getElementById('refStorePriceDisplay').innerText = currentStoreNetPrice.toFixed(2) + " บาท";
                if(!document.getElementById('manual_ref_price').value && currentStoreNetPrice > 0) {
                    document.getElementById('manual_ref_price').value = currentStoreNetPrice.toFixed(2);
                }
                calculateOnlineChannels();
            } else if (tab === 'credit') {
                pageCredit.classList.remove('hidden');
                btnMainCredit.className = "py-2 text-xs font-bold rounded-xl transition-all bg-indigo-600 text-white shadow-sm";
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

        function calculateCreditCost() {
            const baseCost = parseFloat(document.getElementById('c_base_cost').value) || 0;
            const cardFeePercent = parseFloat(document.getElementById('c_card_fee').value) || 0;
            const interestPerMonth = parseFloat(document.getElementById('c_interest_rate').value) || 0;
            const selectedMonths = parseInt(document.getElementById('c_selected_months').value) || 6;

            const tableBody = document.getElementById('c_table_body');
            tableBody.innerHTML = "";

            const plans = [
                { months: 0, label: "รูดเต็ม" },
                { months: 3, label: "3 เดือน" },
                { months: 4, label: "4 เดือน" },
                { months: 6, label: "6 เดือน" },
                { months: 10, label: "10 เดือน" },
                { months: 12, label: "12 เดือน" }
            ];

            let selectedTotalCost = 0;
            let selectedMonthlyPay = 0;

            plans.forEach(plan => {
                let totalCost = baseCost;
                let totalInterestPercent = 0;
                let monthlyPay = 0;

                if (plan.months === 0) {
                    totalCost = baseCost * (1 + (cardFeePercent / 100));
                    monthlyPay = totalCost;
                } else {
                    totalInterestPercent = interestPerMonth * plan.months;
                    let interestAmount = baseCost * (totalInterestPercent / 100);
                    let cardFeeAmount = baseCost * (cardFeePercent / 100);
                    totalCost = baseCost + cardFeeAmount + interestAmount;
                    monthlyPay = totalCost / plan.months;
                }

                let unitCost = totalCost;

                if (plan.months === selectedMonths || (plan.months === 0 && selectedMonths === 0)) {
                    selectedTotalCost = unitCost;
                    selectedMonthlyPay = monthlyPay;
                }

                let isSelected = (plan.months === selectedMonths);
                let rowClass = isSelected ? "bg-indigo-50/80 font-bold text-indigo-900" : "hover:bg-slate-50";

                let row = `<tr class="${rowClass}">
                    <td class="p-2.5">${plan.label} ${isSelected ? '⭐' : ''}</td>
                    <td class="p-2.5 text-right">${totalCost.toFixed(2)}</td>
                    <td class="p-2.5 text-right">${monthlyPay.toFixed(2)}</td>
                    <td class="p-2.5 text-right font-bold text-indigo-600">${unitCost.toFixed(2)}</td>
                </tr>`;
                tableBody.innerHTML += row;
            });

            let selInterest = interestPerMonth * selectedMonths;
            let selTotal = baseCost * (1 + (cardFeePercent/100)) + (baseCost * (selInterest/100));
            let selMonthly = selTotal / selectedMonths;

            document.getElementById('c_res_total_cost').innerText = selTotal.toFixed(2) + " บาท";
            document.getElementById('c_res_monthly_pay').innerText = `ผ่อนเดือนละ ${selMonthly.toFixed(2)} บาท (${selectedMonths} งวด)`;
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
