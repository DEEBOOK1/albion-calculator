<!DOCTYPE html>

<html lang="th">

<head>

&#x20;   <meta charset="UTF-8">

&#x20;   <meta name="viewport" content="width=device-width, initial-scale=1.0">

&#x20;   <title>Albion Crafting Profit Calculator</title>

&#x20;   <style>

&#x20;       :root { --primary: #e67e22; --dark: #2c3e50; --success: #27ae60; --danger: #c0392b; }

&#x20;       body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #ecf0f1; display: flex; justify-content: center; padding: 20px; }

&#x20;       .container { background: white; padding: 30px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); width: 100%; max-width: 450px; }

&#x20;       h2 { color: var(--dark); border-bottom: 3px solid var(--primary); padding-bottom: 10px; margin-top: 0; }

&#x20;       .input-group { margin-bottom: 15px; }

&#x20;       label { display: block; font-size: 0.9rem; font-weight: bold; margin-bottom: 5px; color: var(--dark); }

&#x20;       input, select { width: 100%; padding: 12px; border: 1px solid #ddd; border-radius: 6px; font-size: 1rem; box-sizing: border-box; }

&#x20;       .info-text { font-size: 0.8rem; color: #7f8c8d; margin-top: 4px; }

&#x20;       .result-box { margin-top: 25px; padding: 20px; border-radius: 8px; background: #f9f9f9; text-align: center; }

&#x20;       .val { font-size: 1.5rem; font-weight: bold; margin: 10px 0; }

&#x20;       .pos { color: var(--success); }

&#x20;       .neg { color: var(--danger); }

&#x20;   </style>

</head>

<body>



<div class="container">

&#x20;   <h2>🛠️ Albion Profit Calc</h2>

&#x20;   

&#x20;   <div class="input-group">

&#x20;       <label>ราคาขายต่อชิ้น (Market Price)</label>

&#x20;       <input type="number" id="sellPrice" placeholder="เช่น 15000" oninput="calculate()">

&#x20;   </div>



&#x20;   <div class="input-group">

&#x20;       <label>ต้นทุนวัตถุดิบทั้งหมด (Total Raw Mats)</label>

&#x20;       <input type="number" id="costPrice" placeholder="เช่น 12000" oninput="calculate()">

&#x20;   </div>



&#x20;   <div class="input-group">

&#x20;       <label>RRR % (การคืนทรัพยากร)</label>

&#x20;       <select id="rrr" onchange="calculate()">

&#x20;           <option value="0">0% (คราฟต์นอกเมือง/เกาะ)</option>

&#x20;           <option value="15.2">15.2% (ในเมือง - No Focus)</option>

&#x20;           <option value="43.5">43.5% (ในเมือง - Use Focus)</option>

&#x20;           <option value="53.9">53.9% (ในเมืองมี Bonus - Use Focus)</option>

&#x20;       </select>

&#x20;       <div class="info-text">\*ค่า RRR ช่วยลดต้นทุนวัตถุดิบจริงลง</div>

&#x20;   </div>



&#x20;   <div class="input-group">

&#x20;       <label>ภาษีขาย (Market Tax)</label>

&#x20;       <select id="tax" onchange="calculate()">

&#x20;           <option value="4">4% (มี Premium)</option>

&#x20;           <option value="8">8% (ไม่มี Premium)</option>

&#x20;       </select>

&#x20;   </div>



&#x20;   <div class="result-box" id="resultArea">

&#x20;       กรอกข้อมูลเพื่อเริ่มคำนวณ

&#x20;   </div>

</div>



<script>

function calculate() {

&#x20;   const sellPrice = parseFloat(document.getElementById('sellPrice').value) || 0;

&#x20;   const rawCost = parseFloat(document.getElementById('costPrice').value) || 0;

&#x20;   const rrr = parseFloat(document.getElementById('rrr').value) / 100;

&#x20;   const taxRate = parseFloat(document.getElementById('tax').value) / 100;



&#x20;   // 1. คำนวณต้นทุนจริงหลังจากได้ของคืน (Effective Cost)

&#x20;   // สูตร: ต้นทุนจริง = ต้นทุนดิบ \* (1 - RRR)

&#x20;   const effectiveCost = rawCost \* (1 - rrr);



&#x20;   // 2. คำนวณรายรับหลังหักภาษี (Net Revenue)

&#x20;   const revenue = sellPrice \* (1 - taxRate);



&#x20;   // 3. กำไรสุทธิ

&#x20;   const profit = revenue - effectiveCost;



&#x20;   // 4. เปอร์เซ็นต์กำไร

&#x20;   const margin = effectiveCost > 0 ? (profit / effectiveCost) \* 100 : 0;



&#x20;   const resultArea = document.getElementById('resultArea');

&#x20;   const colorClass = profit >= 0 ? 'pos' : 'neg';



&#x20;   if (sellPrice > 0 \&\& rawCost > 0) {

&#x20;       resultArea.innerHTML = `

&#x20;           <div style="color:#7f8c8d">กำไรสุทธิต่อชิ้น:</div>

&#x20;           <div class="val ${colorClass}">${Math.floor(profit).toLocaleString()} Silver</div>

&#x20;           <div style="color:#7f8c8d">กำไรเป็นเปอร์เซ็นต์:</div>

&#x20;           <div class="${colorClass}" style="font-weight:bold">${margin.toFixed(2)}%</div>

&#x20;       `;

&#x20;   } else {

&#x20;       resultArea.innerHTML = "กรอกราคาขายและต้นทุน";

&#x20;   }

}

</script>



</body>

</html>

