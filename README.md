# Winding-Test-Master-Pro
<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Laporan Pengujian Transformer (5 Tap Pro + Edu)</title>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-delta: #e67e22;
            --accent-star: #9b59b6;
            --accent-earth: #27ae60;
            --bg-color: #f4f7f6;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            margin: 0;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            border-radius: 8px;
        }

        /* HEADER */
        header {
            text-align: center;
            border-bottom: 3px solid var(--primary-color);
            margin-bottom: 20px;
            padding-bottom: 10px;
        }
        h1 { margin: 0; color: var(--primary-color); text-transform: uppercase; }
        .sub-header { color: #7f8c8d; font-size: 0.9rem; }

        /* GLOBAL SETTINGS */
        .settings-panel {
            background: #2c3e50;
            color: white;
            padding: 15px;
            border-radius: 6px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: space-around;
            margin-bottom: 25px;
        }
        .setting-group { display: flex; flex-direction: column; }
        .setting-group label { font-size: 0.8rem; font-weight: bold; margin-bottom: 3px; color: #bdc3c7; }
        .setting-group input, .setting-group select {
            padding: 8px; border: none; border-radius: 4px; font-weight: bold; text-align: center;
        }

        /* SECTION STYLES */
        .section-block {
            margin-bottom: 30px;
            border: 1px solid #ddd;
            border-radius: 6px;
            overflow: hidden;
        }
        .section-title {
            padding: 10px 15px;
            color: white;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
        }
        .delta-header { background-color: var(--accent-delta); }
        .star-header { background-color: var(--accent-star); }
        .earth-header { background-color: var(--accent-earth); }

        .section-content {
            padding: 15px;
            background: #fff;
            display: none; /* Hidden by default for accordion effect */
        }
        .section-content.active { display: block; }

        /* TAP INPUT GRID */
        .tap-row {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 1fr; /* Label, R-Y, Y-B, B-R */
            gap: 10px;
            margin-bottom: 15px;
            align-items: center;
            padding-bottom: 10px;
            border-bottom: 1px dashed #ccc;
        }
        @media (max-width: 600px) {
            .tap-row { grid-template-columns: 1fr; border: 1px solid #eee; padding: 10px; margin-bottom: 10px; }
        }

        .tap-label { font-weight: bold; color: var(--primary-color); }
        input[type="number"] {
            width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px;
        }

        /* BUTTONS */
        .btn-main {
            width: 100%;
            padding: 15px;
            background-color: var(--primary-color);
            color: white;
            font-size: 1.1rem;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            margin-top: 20px;
            transition: background 0.3s;
        }
        .btn-main:hover { background-color: #1a252f; }
        
        .btn-print {
            background-color: #95a5a6;
            margin-top: 10px;
        }

        /* REPORT OUTPUT */
        #finalReport { display: none; margin-top: 40px; border-top: 4px solid #000; padding-top: 20px; }
        
        .report-card {
            border: 2px solid #333;
            margin-bottom: 20px;
            page-break-inside: avoid;
        }
        .report-header {
            background: #eee;
            padding: 8px;
            font-weight: bold;
            border-bottom: 2px solid #333;
            display: flex;
            justify-content: space-between;
        }
        .formula-box {
            font-family: 'Courier New', monospace;
            font-size: 0.8rem;
            background: #fff3cd;
            padding: 5px;
            border-bottom: 1px solid #ddd;
            text-align: center;
            color: #856404;
        }

        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; }
        th, td { border: 1px solid #ccc; padding: 8px; text-align: center; }
        th { background-color: #f8f9fa; }

        /* ANALYSIS BOX */
        .analysis-result { padding: 10px; text-align: left; border-top: 1px solid #000; }
        .safe { background-color: #d4edda; color: #155724; }
        .unsafe { background-color: #f8d7da; color: #721c24; }
        .analysis-text { margin-top: 5px; font-size: 0.9rem; }

        /* TUTORIAL SECTION STYLE */
        .tutorial-section {
            margin-top: 30px;
            border: 2px dashed #555;
            background-color: #fdfdfd;
            padding: 20px;
            page-break-inside: avoid;
        }
        .tutorial-title {
            text-align: center;
            font-weight: bold;
            font-size: 1.2rem;
            margin-bottom: 15px;
            text-decoration: underline;
            color: #d35400;
        }
        .step-box {
            margin-bottom: 15px;
            padding-left: 10px;
            border-left: 4px solid #d35400;
        }
        .math-line {
            font-family: 'Courier New', monospace;
            background: #eee;
            padding: 5px;
            margin: 5px 0;
            display: block;
            font-weight: bold;
        }

        /* PRINT MODE */
        @media print {
            body { background: white; padding: 0; }
            .container { box-shadow: none; max-width: 100%; width: 100%; margin: 0; border: none; }
            .settings-panel, .section-block, .btn-main, h1, .sub-header { display: none; }
            #finalReport { display: block !important; border: none; margin-top: 0; }
            .report-card { break-inside: avoid; }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Winding Test Master Pro</h1>
        <div class="sub-header">Kalkulator 5 Tap (Delta & Star) + Ujian Penebatan</div>
    </header>

    <!-- 1. TETAPAN GLOBAL -->
    <div class="settings-panel">
        <div class="setting-group">
            <label>Suhu Ukur (Tm)</label>
            <input type="number" id="tm" value="30">
        </div>
        <div class="setting-group">
            <label>Suhu Piawai (Ts)</label>
            <input type="number" id="ts" value="75">
        </div>
        <div class="setting-group">
            <label>Pemalar (Tk)</label>
            <input type="number" id="tk" value="234.5">
        </div>
        <div class="setting-group">
            <label>Unit Rintangan</label>
            <select id="unit">
                <option value="mΩ">mΩ (Milli-Ohm)</option>
                <option value="µΩ">µΩ (Micro-Ohm)</option>
                <option value="Ω">Ω (Ohm)</option>
            </select>
        </div>
    </div>

    <div style="text-align:center; margin-bottom: 20px; font-style:italic; color:red;">
        * Klik pada tajuk berwarna untuk membuka/tutup borang input.
    </div>

    <!-- 2. INPUT DELTA (5 TAPS) -->
    <div class="section-block">
        <div class="section-title delta-header" onclick="toggleSection('deltaInput')">
            BAHAGIAN 1: UJIAN DELTA (5 TAPS) <span>▼</span>
        </div>
        <div id="deltaInput" class="section-content">
            <p style="font-size:0.9em; color:#666; text-align:center;">Biasanya untuk Bahagian Voltan Tinggi (HV)</p>
            <div id="deltaContainer"></div> <!-- JS generates inputs here -->
        </div>
    </div>

    <!-- 3. INPUT STAR (5 TAPS) -->
    <div class="section-block">
        <div class="section-title star-header" onclick="toggleSection('starInput')">
            BAHAGIAN 2: UJIAN STAR (5 TAPS) <span>▼</span>
        </div>
        <div id="starInput" class="section-content">
            <p style="font-size:0.9em; color:#666; text-align:center;">Biasanya untuk Bahagian Voltan Rendah (LV)</p>
            <div id="starContainer"></div> <!-- JS generates inputs here -->
        </div>
    </div>

    <!-- 4. INPUT PENEBATAN (MEGGER) -->
    <div class="section-block">
        <div class="section-title earth-header" onclick="toggleSection('earthInput')">
            BAHAGIAN 3: UJIAN PENEBATAN (MEGGER) <span>▼</span>
        </div>
        <div id="earthInput" class="section-content active">
            <div class="tap-row">
                <span class="tap-label">Fasa - Bumi/Neutral</span>
                <input type="number" id="megger_r" placeholder="R - Earth (MΩ)">
                <input type="number" id="megger_y" placeholder="Y - Earth (MΩ)">
                <input type="number" id="megger_b" placeholder="B - Earth (MΩ)">
            </div>
            <div style="text-align:center; font-size:0.85rem; margin-top:5px;">
                * Masukkan bacaan dalam MegaOhm (MΩ). Standard Minimum: 1.0 MΩ.
            </div>
        </div>
    </div>

    <!-- ACTIONS -->
    <button class="btn-main" onclick="janaLaporan()">JANA SEMUA LAPORAN & ANALISIS</button>
    <button class="btn-main btn-print" onclick="window.print()">CETAK / SIMPAN PDF</button>


    <!-- REPORT OUTPUT AREA -->
    <div id="finalReport">
        <h2 style="text-align:center; text-decoration:underline;">LAPORAN PENGUJIAN LENGKAP</h2>
        <div id="reportContent"></div>
        <!-- Tutorial Section will be appended here -->
        <div id="tutorialContent"></div>
    </div>
</div>

<script>
    // --- 1. SETUP: Generate Input Fields Automatically ---
    window.onload = function() {
        generateTapInputs('deltaContainer', 'delta', 5, ['R-Y', 'Y-B', 'B-R']);
        generateTapInputs('starContainer', 'star', 5, ['R-n/Y', 'Y-n/B', 'B-n/R']); 
    };

    function generateTapInputs(containerId, prefix, count, labels) {
        let html = '';
        for (let i = 1; i <= count; i++) {
            html += `
            <div class="tap-row">
                <span class="tap-label">TAP ${i}</span>
                <input type="number" id="${prefix}_t${i}_1" placeholder="${labels[0]}" step="any">
                <input type="number" id="${prefix}_t${i}_2" placeholder="${labels[1]}" step="any">
                <input type="number" id="${prefix}_t${i}_3" placeholder="${labels[2]}" step="any">
            </div>`;
        }
        document.getElementById(containerId).innerHTML = html;
    }

    function toggleSection(id) {
        let el = document.getElementById(id);
        el.classList.toggle('active');
    }

    // --- 2. CALCULATION LOGIC ---
    function janaLaporan() {
        // Get Globals
        let Tm = parseFloat(document.getElementById('tm').value);
        let Ts = parseFloat(document.getElementById('ts').value);
        let Tk = parseFloat(document.getElementById('tk').value);
        let unit = document.getElementById('unit').value;
        let factor = (Ts + Tk) / (Tm + Tk);
        
        let reportHTML = "";
        let currentDate = new Date().toLocaleString('ms-MY');
        let firstValidData = null; // To store data for tutorial

        reportHTML += `<p style="text-align:center; margin-bottom:20px;">Tarikh Ujian: ${currentDate}</p>`;

        // --- PROCESS DELTA (5 Taps) ---
        for(let i=1; i<=5; i++) {
            let result = processWindingBlock('DELTA', i, `delta_t${i}`, factor, unit, Tm, Ts, Tk);
            reportHTML += result.html;
            if (!firstValidData && result.data) firstValidData = result.data;
        }

        // --- PROCESS STAR (5 Taps) ---
        for(let i=1; i<=5; i++) {
            let result = processWindingBlock('STAR', i, `star_t${i}`, factor, unit, Tm, Ts, Tk);
            reportHTML += result.html;
            if (!firstValidData && result.data) firstValidData = result.data;
        }

        // --- PROCESS MEGGER ---
        reportHTML += processMeggerBlock();

        // Display Report
        document.getElementById('reportContent').innerHTML = reportHTML;

        // --- GENERATE TUTORIAL (EDUCATIONAL SECTION) ---
        if (firstValidData) {
            let tutorialHTML = generateTutorial(firstValidData, Tm, Ts, Tk, factor, unit);
            document.getElementById('tutorialContent').innerHTML = tutorialHTML;
        } else {
            document.getElementById('tutorialContent').innerHTML = "";
        }

        document.getElementById('finalReport').style.display = "block";
        
        // Auto scroll
        document.getElementById('finalReport').scrollIntoView({behavior: 'smooth'});
    }

    function processWindingBlock(type, tapNum, idPrefix, factor, unit, Tm, Ts, Tk) {
        // Get Values
        let r1 = document.getElementById(`${idPrefix}_1`).value;
        let r2 = document.getElementById(`${idPrefix}_2`).value;
        let r3 = document.getElementById(`${idPrefix}_3`).value;

        // If empty, return empty
        if(r1 === "" && r2 === "" && r3 === "") return { html: "", data: null };

        r1 = parseFloat(r1 || 0); r2 = parseFloat(r2 || 0); r3 = parseFloat(r3 || 0);

        // Calculate Corrected
        let rc1 = r1 * factor;
        let rc2 = r2 * factor;
        let rc3 = r3 * factor;

        // Calculate Unbalance
        let avg = (r1 + r2 + r3) / 3;
        let maxDiff = Math.max(Math.abs(r1 - avg), Math.abs(r2 - avg), Math.abs(r3 - avg));
        let unbalance = 0;
        if(avg > 0) unbalance = (maxDiff / avg) * 100;

        // Analyze Safety
        let isSafe = unbalance <= 5.0 && avg > 0;
        let statusClass = isSafe ? "safe" : "unsafe";
        let statusIcon = isSafe ? "✅ SELAMAT" : "⛔ TIDAK SELAMAT";
        
        let analysisText = "";
        if(isSafe) {
            analysisText = `<strong>KENAPA SELAMAT:</strong> Ketidakseimbangan rintangan ialah <strong>${unbalance.toFixed(2)}%</strong> (bawah 5%).<br>Ini bermakna sambungan Tap ${tapNum} bagi sambungan ${type} adalah kemas, spring tap changer kuat, dan tiada litar pintas antara lilitan.`;
        } else {
            analysisText = `<strong>KENAPA BAHAYA:</strong> Ketidakseimbangan tinggi <strong>${unbalance.toFixed(2)}%</strong>.<br>Punca mungkin: Contact point pada Tap ${tapNum} kotor/karbon, spring longgar, atau lilitan mula mengalami litar pintas. Risiko panas melampau.`;
        }

        let formulaStr = `Formula Suhu: R(${Ts}°C) = R(${Tm}°C) × [(${Ts}+${Tk}) / (${Tm}+${Tk})]`;

        let html = `
        <div class="report-card">
            <div class="report-header">
                <span>${type} - TAP ${tapNum}</span>
                <span>Unit: ${unit}</span>
            </div>
            <div class="formula-box">${formulaStr}</div>
            <table>
                <thead>
                    <tr>
                        <th>Fasa</th>
                        <th>Bacaan Asal (${Tm}°C)</th>
                        <th>Dibetulkan (${Ts}°C)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td>Fasa 1</td><td>${r1.toFixed(3)}</td><td>${rc1.toFixed(3)}</td></tr>
                    <tr><td>Fasa 2</td><td>${r2.toFixed(3)}</td><td>${rc2.toFixed(3)}</td></tr>
                    <tr><td>Fasa 3</td><td>${r3.toFixed(3)}</td><td>${rc3.toFixed(3)}</td></tr>
                </tbody>
            </table>
            <div class="analysis-result ${statusClass}">
                <div style="font-weight:bold; font-size:1.1rem;">STATUS: ${statusIcon}</div>
                <div style="border-bottom:1px solid #999; margin:5px 0;">% Unbalance: ${unbalance.toFixed(2)}%</div>
                <div class="analysis-text">${analysisText}</div>
            </div>
        </div>
        `;

        // Return data object for tutorial
        return {
            html: html,
            data: { type: type, tap: tapNum, r1: r1, r2: r2, r3: r3, rc1: rc1 }
        };
    }

    function processMeggerBlock() {
        let mr = document.getElementById('megger_r').value;
        let my = document.getElementById('megger_y').value;
        let mb = document.getElementById('megger_b').value;

        if(mr === "" && my === "" && mb === "") return "";

        mr = parseFloat(mr || 0); my = parseFloat(my || 0); mb = parseFloat(mb || 0);
        let minVal = Math.min(mr, my, mb); // Check lowest insulation
        let isSafe = minVal >= 1.0;
        
        let statusClass = isSafe ? "safe" : "unsafe";
        let statusIcon = isSafe ? "✅ SELAMAT" : "⛔ TIDAK SELAMAT";
        let analysisText = isSafe 
            ? `<strong>KENAPA SELAMAT:</strong> Bacaan penebatan terendah ialah <strong>${minVal} MΩ</strong> (Melebihi had 1.0 MΩ). Penebatan winding ke bumi adalah baik dan tiada kebocoran.`
            : `<strong>KENAPA BAHAYA:</strong> Bacaan penebatan <strong>${minVal} MΩ</strong> adalah terlalu rendah (Bawah 1.0 MΩ). Terdapat kebocoran arus ke bumi (Earth Fault). Berisiko meletup jika dihidupkan.`;

        return `
        <div class="report-card">
            <div class="report-header">
                <span>UJIAN PENEBATAN (MEGGER)</span>
                <span>Unit: MΩ</span>
            </div>
            <div class="formula-box">Formula: Nilai Mesti > 1.0 MΩ (Untuk Voltan Rendah)</div>
            <table>
                <thead><tr><th>Titik Ujian</th><th>Bacaan (MΩ)</th></tr></thead>
                <tbody>
                    <tr><td>R - Bumi</td><td>${mr}</td></tr>
                    <tr><td>Y - Bumi</td><td>${my}</td></tr>
                    <tr><td>B - Bumi</td><td>${mb}</td></tr>
                </tbody>
            </table>
            <div class="analysis-result ${statusClass}">
                <div style="font-weight:bold;">STATUS: ${statusIcon}</div>
                <div class="analysis-text">${analysisText}</div>
            </div>
        </div>
        `;
    }

    function generateTutorial(data, Tm, Ts, Tk, factor, unit) {
        let avg = (data.r1 + data.r2 + data.r3) / 3;
        let diff1 = Math.abs(data.r1 - avg);
        let diff2 = Math.abs(data.r2 - avg);
        let diff3 = Math.abs(data.r3 - avg);
        let maxDiff = Math.max(diff1, diff2, diff3);
        let unbalance = (maxDiff / avg) * 100;

        return `
        <div class="tutorial-section">
            <div class="tutorial-title">🎓 TUTORIAL: CONTOH PENGIRAAN MANUAL</div>
            <p style="text-align:center; margin-bottom:20px;">
                Di bawah adalah jalan kerja matematik untuk data yang diambil daripada: <br>
                <strong>${data.type} - TAP ${data.tap}</strong>
            </p>

            <div class="step-box">
                <strong>LANGKAH 1: KIRA FAKTOR SUHU</strong>
                <p>Kita perlu mencari pekali (multiplier) untuk menukar bacaan suhu ${Tm}°C kepada suhu piawai ${Ts}°C.</p>
                <span class="math-line">Formula = (Ts + Tk) / (Tm + Tk)</span>
                <span class="math-line">Kiraan = (${Ts} + ${Tk}) / (${Tm} + ${Tk})</span>
                <span class="math-line">Kiraan = ${Ts+Tk} / ${Tm+Tk}</span>
                <span class="math-line">Faktor = ${factor.toFixed(5)}</span>
            </div>

            <div class="step-box">
                <strong>LANGKAH 2: BETULKAN BACAAN RINTANGAN</strong>
                <p>Darabkan bacaan asal (Measured) dengan Faktor Suhu di atas. Contoh Fasa 1:</p>
                <span class="math-line">R(betul) = R(asal) × Faktor</span>
                <span class="math-line">R(betul) = ${data.r1} × ${factor.toFixed(5)}</span>
                <span class="math-line">Jawapan = ${data.rc1.toFixed(3)} ${unit}</span>
            </div>

            <div class="step-box">
                <strong>LANGKAH 3: KIRA KETIDAKSEIMBANGAN (% UNBALANCE)</strong>
                <p>Pertama, cari Purata (Average):</p>
                <span class="math-line">Purata = (R1 + R2 + R3) / 3</span>
                <span class="math-line">Purata = (${data.r1} + ${data.r2} + ${data.r3}) / 3</span>
                <span class="math-line">Purata = ${avg.toFixed(3)}</span>
                
                <p>Kedua, cari Beza Paling Besar (Max Deviation) dari Purata:</p>
                <span class="math-line">Beza = |Nilai Tertinggi/Terendah - Purata|</span>
                <span class="math-line">Beza Maksimum = ${maxDiff.toFixed(3)}</span>

                <p>Ketiga, kira Peratus:</p>
                <span class="math-line">% Unbalance = (Beza Maksimum / Purata) × 100</span>
                <span class="math-line">% Unbalance = (${maxDiff.toFixed(3)} / ${avg.toFixed(3)}) × 100</span>
                <span class="math-line">Jawapan Akhir = ${unbalance.toFixed(2)}%</span>
            </div>
            
            <div style="text-align:center; font-style:italic; margin-top:10px;">
                * Jika jawapan akhir > 5%, peralatan dikira GAGAL.
            </div>
        </div>
        `;
    }
</script>

</body>
</html>
