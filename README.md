```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Risk Factor Analytics Dashboard</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBg: '#0f0f12',
                        cardBg: '#16161a',
                        cardBorder: '#26262e',
                        goldAccent: '#f3ba2f',
                        goldDark: '#b8860b',
                        goldLight: '#ffe082',
                        textMuted: '#9ca3af'
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #0f0f12;
            color: #ffffff;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        /* Custom Scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #16161a;
        }
        ::-webkit-scrollbar-thumb {
            background: #f3ba2f;
            border-radius: 3px;
        }
        /* Styling range slider */
        input[type=range] {
            accent-color: #f3ba2f;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col p-3 lg:p-5 gap-4">

    <!-- Top Executive Header -->
    <header class="flex flex-col md:flex-row justify-between items-center bg-cardBg border border-cardBorder p-4 rounded-xl shadow-lg gap-4">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 border-2 border-goldAccent flex items-center justify-center rounded-lg bg-black/40">
                <svg class="w-6 h-6 text-goldAccent" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path>
                </svg>
            </div>
            <h1 class="text-2xl md:text-3xl font-bold tracking-tight text-white">
                Risk <span class="text-goldAccent">Factor</span> Analytics Dashboard
            </h1>
        </div>

        <!-- Hexagon Logo Container -->
        <div class="flex items-center gap-3 bg-black/50 px-4 py-2 rounded-lg border border-goldAccent/30">
            <div class="relative w-8 h-8 flex items-center justify-center">
                <div class="absolute inset-0 border-2 border-goldAccent transform rotate-45 rounded-sm"></div>
                <span class="text-xs font-bold text-goldAccent z-10">RF</span>
            </div>
            <div class="text-right">
                <div class="text-xs font-bold tracking-widest text-goldAccent">RISK FACTOR</div>
                <div class="text-[9px] text-textMuted uppercase tracking-wider">PRODUCT VOICE & RISK INTELLIGENCE</div>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">

        <!-- Left Sidebar / Filters Panel -->
        <aside class="lg:col-span-2 bg-cardBg border border-cardBorder p-4 rounded-xl flex flex-col gap-4">
            <h2 class="text-xs font-bold uppercase tracking-wider text-goldAccent border-b border-cardBorder pb-2">Filters</h2>
            
            <div class="space-y-3 text-xs">
                <div>
                    <label class="block text-textMuted mb-1">Governorate</label>
                    <select id="filterGov" class="w-full bg-black/60 border border-cardBorder text-white p-2 rounded focus:border-goldAccent outline-none">
                        <option value="All">All</option>
                        <option value="Assiut">Assiut</option>
                        <option value="Kafr El Sheikh">Kafr El Sheikh</option>
                        <option value="Gharbia">Gharbia</option>
                        <option value="Sohag">Sohag</option>
                        <option value="Giza">Giza</option>
                    </select>
                </div>

                <div>
                    <label class="block text-textMuted mb-1">Center</label>
                    <select id="filterCenter" class="w-full bg-black/60 border border-cardBorder text-white p-2 rounded focus:border-goldAccent outline-none">
                        <option value="All">All</option>
                        <option value="Abnub">Abnub</option>
                        <option value="Qalin">Qalin</option>
                        <option value="Akhmim">Akhmim</option>
                        <option value="Tahta">Tahta</option>
                    </select>
                </div>

                <div>
                    <label class="block text-textMuted mb-1">Date</label>
                    <select class="w-full bg-black/60 border border-cardBorder text-white p-2 rounded focus:border-goldAccent outline-none">
                        <option value="All">All</option>
                    </select>
                </div>

                <div>
                    <label class="block text-textMuted mb-1">Product</label>
                    <select class="w-full bg-black/60 border border-cardBorder text-white p-2 rounded focus:border-goldAccent outline-none">
                        <option value="All">All</option>
                    </select>
                </div>

                <div>
                    <label class="block text-textMuted mb-1">Segment</label>
                    <select class="w-full bg-black/60 border border-cardBorder text-white p-2 rounded focus:border-goldAccent outline-none">
                        <option value="All">All</option>
                    </select>
                </div>

                <div class="pt-2 border-t border-cardBorder">
                    <label class="block text-textMuted mb-1">RATING RANGE</label>
                    <div class="flex gap-2 mb-2">
                        <input type="text" value="3" class="w-1/2 bg-black/60 border border-cardBorder text-center text-xs text-white p-1 rounded" readonly>
                        <input type="text" value="10" class="w-1/2 bg-black/60 border border-cardBorder text-center text-xs text-white p-1 rounded" readonly>
                    </div>
                    <input type="range" min="3" max="10" value="10" class="w-full">
                </div>
            </div>

            <!-- Risk Radar Visual -->
            <div class="mt-auto pt-4 border-t border-cardBorder text-center">
                <div class="text-[10px] uppercase tracking-widest text-goldAccent mb-2 font-semibold">Risk Radar</div>
                <div class="relative w-28 h-28 mx-auto rounded-full border border-goldAccent/40 flex items-center justify-center bg-black/40">
                    <div class="absolute w-20 h-20 rounded-full border border-goldAccent/20"></div>
                    <div class="absolute w-10 h-10 rounded-full border border-goldAccent/20"></div>
                    <div class="absolute w-full h-[1px] bg-goldAccent/30"></div>
                    <div class="absolute h-full w-[1px] bg-goldAccent/30"></div>
                    <!-- Radar Scanner Sweep -->
                    <div class="w-2 h-2 rounded-full bg-goldAccent shadow-[0_0_8px_#f3ba2f] absolute top-6 left-16"></div>
                    <span class="text-[9px] font-bold text-goldAccent z-10 bg-black/80 px-1 border border-goldAccent/40 rounded">Score: 8.3</span>
                </div>
            </div>
        </aside>

        <!-- Main Dashboard Content -->
        <main class="lg:col-span-10 flex flex-col gap-4">

            <!-- KPI Cards Row -->
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-3">
                <div class="bg-cardBg border border-goldAccent/40 rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Risk Score</span>
                    <div class="flex items-baseline gap-2 mt-1">
                        <span id="kpiRiskScore" class="text-2xl font-extrabold text-goldAccent">8.3</span>
                        <span class="text-[10px] text-textMuted">/ 100</span>
                    </div>
                </div>

                <div class="bg-cardBg border border-cardBorder rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Quality Score</span>
                    <span class="text-2xl font-extrabold text-goldAccent mt-1">91.72</span>
                </div>

                <div class="bg-cardBg border border-cardBorder rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Open Critical Risks</span>
                    <span class="text-2xl font-extrabold text-goldAccent mt-1">0</span>
                </div>

                <div class="bg-cardBg border border-cardBorder rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Total Ratings</span>
                    <span class="text-2xl font-extrabold text-white mt-1">784</span>
                </div>

                <div class="bg-cardBg border border-cardBorder rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Monthly Quality Score /5</span>
                    <span class="text-2xl font-extrabold text-goldAccent mt-1">4.8</span>
                </div>

                <div class="bg-cardBg border border-cardBorder rounded-xl p-3 flex flex-col justify-between shadow-md">
                    <span class="text-xs text-textMuted">Max_Severity_Val</span>
                    <span class="text-2xl font-extrabold text-white mt-1">4</span>
                </div>
            </div>

            <!-- Page Tabs / Views Toggle -->
            <div class="flex border-b border-cardBorder gap-2">
                <button id="tab1Btn" onclick="switchTab(1)" class="px-4 py-2 text-xs font-bold text-black bg-goldAccent rounded-t-lg">Overview Analytics</button>
                <button id="tab2Btn" onclick="switchTab(2)" class="px-4 py-2 text-xs font-bold text-textMuted bg-cardBg rounded-t-lg hover:text-white">Matrix & Gauges View</button>
            </div>

            <!-- VIEW 1: Overview Analytics (Image 1 Content) -->
            <div id="view1" class="grid grid-cols-1 md:grid-cols-3 gap-4">
                
                <!-- Chart 1: Total Rating by Risk -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col">
                    <h3 class="text-xs font-bold text-white mb-3">Total Rating by Risk</h3>
                    <div class="h-48 relative">
                        <canvas id="chartTotalRatingRisk"></canvas>
                    </div>
                </div>

                <!-- Chart 2: Contribution by Source -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col">
                    <h3 class="text-xs font-bold text-white mb-3">Contribution by Source</h3>
                    <div class="h-48 relative">
                        <canvas id="chartContribSource"></canvas>
                    </div>
                </div>

                <!-- Chart 3: Breakdown by Risk level -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col items-center justify-center">
                    <h3 class="text-xs font-bold text-white mb-1 w-full text-left">Breakdown by Risk level</h3>
                    <div class="h-48 w-full relative flex items-center justify-center">
                        <canvas id="chartRiskLevel"></canvas>
                    </div>
                </div>

                <!-- Chart 4: Rating count by source -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col">
                    <h3 class="text-xs font-bold text-white mb-3">Rating count by source</h3>
                    <div class="h-48 relative">
                        <canvas id="chartRatingCountSource"></canvas>
                    </div>
                </div>

                <!-- Chart 5: High Risk Governorates -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col">
                    <h3 class="text-xs font-bold text-white mb-3">High Risk Governorates</h3>
                    <div class="h-48 relative">
                        <canvas id="chartHighRiskGov"></canvas>
                    </div>
                </div>

                <!-- Chart 6: Risk score by Center -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col">
                    <h3 class="text-xs font-bold text-white mb-3">Risk score by Center</h3>
                    <div class="h-48 relative">
                        <canvas id="chartRiskCenter"></canvas>
                    </div>
                </div>

                <!-- Chart 7: Hierarchy Tree / Risk Score Flow (Spans 3 Columns) -->
                <div class="md:col-span-3 bg-cardBg border border-cardBorder rounded-xl p-4">
                    <h3 class="text-xs font-bold text-white mb-3">Decomposition Tree: Risk Score Hierarchy (Governorate &rarr; Center)</h3>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-xs bg-black/40 p-4 rounded-lg border border-cardBorder">
                        <div class="border-r border-cardBorder/60 pr-2">
                            <div class="text-goldAccent font-bold border-b border-cardBorder pb-1 mb-2">Kafr El Sheikh (16.2)</div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Abnub:</span> <span class="text-white font-semibold">21.2</span></div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Qalin:</span> <span class="text-white font-semibold">16.2</span></div>
                        </div>
                        <div class="border-r border-cardBorder/60 pr-2">
                            <div class="text-goldAccent font-bold border-b border-cardBorder pb-1 mb-2">Minya (12.5)</div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Assiut:</span> <span class="text-white font-semibold">20.0</span></div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Mallawi:</span> <span class="text-white font-semibold">12.5</span></div>
                        </div>
                        <div class="border-r border-cardBorder/60 pr-2">
                            <div class="text-goldAccent font-bold border-b border-cardBorder pb-1 mb-2">Gharbia & Giza (10.0)</div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Sahel Selim:</span> <span class="text-white font-semibold">15.7</span></div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; El Fateh:</span> <span class="text-white font-semibold">9.8</span></div>
                        </div>
                        <div>
                            <div class="text-goldAccent font-bold border-b border-cardBorder pb-1 mb-2">Assiut (9.1)</div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; Abu Tig:</span> <span class="text-white font-semibold">8.1</span></div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; El Badari:</span> <span class="text-white font-semibold">7.4</span></div>
                            <div class="flex justify-between text-textMuted py-0.5"><span>&bull; El Qusiya:</span> <span class="text-white font-semibold">5.1</span></div>
                        </div>
                    </div>
                </div>

            </div>

            <!-- VIEW 2: Matrix & Gauges View (Image 2 Content) -->
            <div id="view2" class="hidden grid-cols-1 md:grid-cols-2 gap-4">
                
                <!-- Matrix Table -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 overflow-x-auto">
                    <h3 class="text-xs font-bold text-white mb-3">Governorate Matrix Breakdown</h3>
                    <table class="w-full text-xs text-left text-white border-collapse">
                        <thead>
                            <tr class="border-b border-cardBorder text-goldAccent">
                                <th class="p-2">Governorate</th>
                                <th class="p-2">Assiut</th>
                                <th class="p-2">Mohandes</th>
                                <th class="p-2">Moqawem</th>
                                <th class="p-2">Not recorded</th>
                                <th class="p-2">Saeed</th>
                                <th class="p-2">Total</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-cardBorder/50 text-textMuted">
                            <tr><td class="p-2 font-bold text-white">Assiut</td><td class="p-2">12.9</td><td class="p-2">11.9</td><td class="p-2">8.5</td><td class="p-2">0.0</td><td class="p-2">3.6</td><td class="p-2 font-bold text-goldAccent">9.1</td></tr>
                            <tr><td class="p-2 font-bold text-white">Dakahlia</td><td class="p-2">7.3</td><td class="p-2">0.0</td><td class="p-2">10.0</td><td class="p-2">0.0</td><td class="p-2">0.0</td><td class="p-2 font-bold text-goldAccent">3.6</td></tr>
                            <tr><td class="p-2 font-bold text-white">Gharbia</td><td class="p-2">10.0</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2 font-bold text-goldAccent">10.0</td></tr>
                            <tr><td class="p-2 font-bold text-white">Giza</td><td class="p-2">10.0</td><td class="p-2">10.0</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2 font-bold text-goldAccent">10.0</td></tr>
                            <tr><td class="p-2 font-bold text-white">Kafr El Sheikh</td><td class="p-2">16.4</td><td class="p-2">10.0</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2 font-bold text-goldAccent">16.2</td></tr>
                            <tr><td class="p-2 font-bold text-white">Luxor</td><td class="p-2">8.2</td><td class="p-2">2.9</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2 font-bold text-goldAccent">5.0</td></tr>
                            <tr><td class="p-2 font-bold text-white">Minya</td><td class="p-2">1.0</td><td class="p-2">0.1</td><td class="p-2">14.6</td><td class="p-2">5.3</td><td class="p-2">0.8</td><td class="p-2 font-bold text-goldAccent">12.5</td></tr>
                            <tr><td class="p-2 font-bold text-white">Qena</td><td class="p-2">10.0</td><td class="p-2">7.0</td><td class="p-2">5.5</td><td class="p-2">-</td><td class="p-2">-</td><td class="p-2 font-bold text-goldAccent">7.0</td></tr>
                            <tr><td class="p-2 font-bold text-white">Sohag</td><td class="p-2">10.5</td><td class="p-2">1.6</td><td class="p-2">9.3</td><td class="p-2">10.0</td><td class="p-2">12.6</td><td class="p-2 font-bold text-goldAccent">8.8</td></tr>
                            <tr class="font-bold text-white bg-black/40"><td class="p-2">Total</td><td class="p-2">11.4</td><td class="p-2">9.7</td><td class="p-2">7.9</td><td class="p-2">8.5</td><td class="p-2">11.4</td><td class="p-2 text-goldAccent">8.3</td></tr>
                        </tbody>
                    </table>
                </div>

                <!-- Half-Gauge Meter (Risk Score Gauge) -->
                <div class="bg-cardBg border border-cardBorder rounded-xl p-4 flex flex-col items-center justify-center">
                    <h3 class="text-xs font-bold text-white mb-2 w-full text-left">Risk Score Gauge</h3>
                    <div class="h-56 w-full relative flex items-center justify-center">
                        <canvas id="gaugeRiskScore"></canvas>
                    </div>
                </div>

                <!-- Chart 8: Count of Rating by Center (Spans Full Width) -->
                <div class="md:col-span-2 bg-cardBg border border-cardBorder rounded-xl p-4">
                    <h3 class="text-xs font-bold text-white mb-3">Count of Rating by Center</h3>
                    <div class="h-64 relative">
                        <canvas id="chartRatingCenter"></canvas>
                    </div>
                </div>

            </div>

        </main>

    </div>

    <!-- Chart Configuration Script -->
    <script>
        // Global Chart Defaults
        Chart.defaults.color = '#9ca3af';
        Chart.defaults.font.family = "'Segoe UI', sans-serif";

        const goldColor = '#f3ba2f';
        const goldHover = '#ffb703';
        const darkBorder = '#26262e';

        // 1. Total Rating by Risk (Vertical Bar Chart)
        new Chart(document.getElementById('chartTotalRatingRisk'), {
            type: 'bar',
            data: {
                labels: ['Contractor Site Visits', 'External Engineers', 'Monthly Quality Survey', 'Technical Visits'],
                datasets: [{
                    data: [75, 18, 7, 0],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { display: false }, ticks: { font: { size: 9 } } },
                    y: { grid: { color: darkBorder }, ticks: { callback: v => v + '%' } }
                }
            }
        });

        // 2. Contribution by Source (Horizontal Bar Chart)
        new Chart(document.getElementById('chartContribSource'), {
            type: 'bar',
            indexAxis: 'y',
            data: {
                labels: ['Technical Visits', 'Monthly Quality Survey', 'Contractors Site Visits', 'External Engineers'],
                datasets: [{
                    data: [100, 96, 90, 83],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { color: darkBorder } },
                    y: { grid: { display: false }, ticks: { font: { size: 9 } } }
                }
            }
        });

        // 3. Breakdown by Risk level (Doughnut Chart)
        new Chart(document.getElementById('chartRiskLevel'), {
            type: 'doughnut',
            data: {
                labels: ['Medium (2.81%)', 'Low (97.19%)'],
                datasets: [{
                    data: [22, 762],
                    backgroundColor: ['#e53e3e', goldColor],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '75%',
                plugins: {
                    legend: { position: 'right', labels: { boxWidth: 10, font: { size: 10 } } }
                }
            },
            plugins: [{
                id: 'centerText',
                beforeDraw(chart) {
                    const { width, height, ctx } = chart;
                    ctx.save();
                    ctx.font = "bold 22px sans-serif";
                    ctx.fillStyle = "#ffffff";
                    ctx.textAlign = "center";
                    ctx.textBaseline = "middle";
                    ctx.fillText("784", width / 3.2, height / 2);
                    ctx.restore();
                }
            }]
        });

        // 4. Rating count by source (Horizontal Bar Chart)
        new Chart(document.getElementById('chartRatingCountSource'), {
            type: 'bar',
            indexAxis: 'y',
            data: {
                labels: ['Contractors Site Visit', 'Monthly Quality Survey', 'External Engineers', 'Technical Visits'],
                datasets: [{
                    data: [384, 380, 19, 1],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { color: darkBorder } },
                    y: { grid: { display: false }, ticks: { font: { size: 9 } } }
                }
            }
        });

        // 5. High Risk Governorates (Horizontal Bar Chart)
        new Chart(document.getElementById('chartHighRiskGov'), {
            type: 'bar',
            indexAxis: 'y',
            data: {
                labels: ['Assiut', 'Kafr El Sheikh', 'Gharbia', 'Sohag', 'Giza', 'Qena', 'Luxor', 'Minya', 'Dakahlia'],
                datasets: [{
                    data: [21.2, 16.2, 10.0, 10.0, 7.5, 7.0, 5.0, 0.2, 0.0],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { color: darkBorder } },
                    y: { grid: { display: false }, ticks: { font: { size: 9 } } }
                }
            }
        });

        // 6. Risk score by Center (Horizontal Bar Chart)
        new Chart(document.getElementById('chartRiskCenter'), {
            type: 'bar',
            indexAxis: 'y',
            data: {
                labels: ['Abnub', 'Qalin', 'Akhmim', 'Ausim', 'Abu Tesht', 'Luxor', 'Abu Qirqas', 'Beni Ebeid'],
                datasets: [{
                    data: [21.2, 16.2, 10.0, 7.5, 7.1, 5.0, 0.2, 0.0],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { color: darkBorder } },
                    y: { grid: { display: false }, ticks: { font: { size: 9 } } }
                }
            }
        });

        // 7. Gauge Meter for Risk Score
        new Chart(document.getElementById('gaugeRiskScore'), {
            type: 'doughnut',
            data: {
                labels: ['Score', 'Remaining'],
                datasets: [{
                    data: [8.3, 91.7],
                    backgroundColor: [goldColor, '#33333e'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                rotation: -90,
                circumference: 180,
                cutout: '80%',
                plugins: { legend: { display: false } }
            },
            plugins: [{
                id: 'gaugeText',
                beforeDraw(chart) {
                    const { width, height, ctx } = chart;
                    ctx.save();
                    ctx.font = "bold 28px sans-serif";
                    ctx.fillStyle = goldColor;
                    ctx.textAlign = "center";
                    ctx.textBaseline = "middle";
                    ctx.fillText("8.3", width / 2, height / 1.4);
                    ctx.restore();
                }
            }]
        });

        // 8. Count of Rating by Center
        new Chart(document.getElementById('chartRatingCenter'), {
            type: 'bar',
            indexAxis: 'y',
            data: {
                labels: ['Tahta', 'El Fateh', 'El Qusiya', 'Mallawi', 'Abnub', 'Abu Qirqas', 'Deir Mawas', 'Manfalut', 'Abu Tesht', 'Luxor', 'Juhayna'],
                datasets: [{
                    data: [71, 51, 51, 49, 48, 46, 46, 41, 30, 28, 27],
                    backgroundColor: goldColor,
                    borderRadius: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { color: darkBorder } },
                    y: { grid: { display: false }, ticks: { font: { size: 10 } } }
                }
            }
        });

        // Tab Switching Logic
        function switchTab(tabIndex) {
            const v1 = document.getElementById('view1');
            const v2 = document.getElementById('view2');
            const b1 = document.getElementById('tab1Btn');
            const b2 = document.getElementById('tab2Btn');

            if (tabIndex === 1) {
                v1.classList.remove('hidden');
                v1.classList.add('grid');
                v2.classList.add('hidden');
                v2.classList.remove('grid');

                b1.className = "px-4 py-2 text-xs font-bold text-black bg-goldAccent rounded-t-lg";
                b2.className = "px-4 py-2 text-xs font-bold text-textMuted bg-cardBg rounded-t-lg hover:text-white";
            } else {
                v2.classList.remove('hidden');
                v2.classList.add('grid');
                v1.classList.add('hidden');
                v1.classList.remove('grid');

                b2.className = "px-4 py-2 text-xs font-bold text-black bg-goldAccent rounded-t-lg";
                b1.className = "px-4 py-2 text-xs font-bold text-textMuted bg-cardBg rounded-t-lg hover:text-white";
            }
        }
    </script>
</body>
</html>
```
