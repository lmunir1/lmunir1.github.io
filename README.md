<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RD Surgery Risk Calculator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8f9fa; /* Lighter gray, similar to STS */
        }
        .form-select, .form-input {
            @apply w-full rounded-md border-gray-300 shadow-sm focus:border-blue-600 focus:ring-blue-600 sm:text-sm;
        }
        .form-label {
            @apply block text-sm font-medium text-gray-700;
        }
        .form-label-inline {
            @apply text-sm font-medium text-gray-700;
        }
        .info-bubble {
            @apply relative inline-block align-middle;
        }
        .info-bubble-icon {
            @apply cursor-pointer w-4 h-4 ml-1 text-gray-400 hover:text-gray-600;
        }
        .info-bubble-text {
            @apply absolute z-10 w-48 p-2 -mt-10 ml-6 text-xs text-white bg-gray-900 rounded-md shadow-lg opacity-0 invisible transition-opacity duration-300;
            left: -0.5rem;
            bottom: 1.25rem;
        }
        .info-bubble:hover .info-bubble-text {
            @apply opacity-100 visible;
        }
        .section-header {
            @apply text-lg font-semibold text-gray-900 mb-4 border-b border-gray-200 pb-2;
        }
        .checkbox-label {
             @apply ml-2 text-sm font-medium text-gray-700;
        }
        .checkbox-item {
            @apply relative flex items-start;
        }
        .checkbox-input {
            @apply h-4 w-4 rounded border-gray-300 text-blue-600 focus:ring-blue-500;
        }
    </style>
</head>
<body class="bg-gray-100">

    <div class="container mx-auto max-w-7xl p-4 sm:p-8">
        <!-- Header -->
        <div class="text-center mb-10">
            <h1 class="text-4xl font-bold text-gray-800 mb-2">Retinal Detachment Repair Risk Calculator</h1>
            <p class="text-lg text-gray-600">Prototype for clinical model development. <strong class="text-red-600">Not for clinical use.</strong></p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            <!-- Input Form Section (Spans 2 columns) -->
            <div class="lg:col-span-2 bg-white p-6 rounded-lg shadow-lg border border-gray-200">
                <form id="risk-form" class="space-y-6">
                    
                    <!-- Section 1: Demographics -->
                    <div>
                        <h2 class="section-header">Demographics & History</h2>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
                            <div>
                                <label for="age" class="form-label">Age (years)</label>
                                <input type="number" id="age" class="form-input" value="60">
                            </div>
                            <div>
                                <label for="gender" class="form-label">Gender</label>
                                <select id="gender" class="form-select">
                                    <option value="male">Male</option>
                                    <option value="female">Female</option>
                                    <option value="other">Other / Not specified</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- Section 2: Ocular History -->
                    <div class="pt-4 border-t border-gray-200">
                        <h2 class="section-header">Ocular History</h2>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
                            <!-- Column 1 -->
                            <div class="space-y-3">
                                <div class="checkbox-item">
                                    <input id="myopia" type="checkbox" class="checkbox-input">
                                    <label for="myopia" class="checkbox-label">Myopia</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="cataract_sx" type="checkbox" class="checkbox-input">
                                    <label for="cataract_sx" class="checkbox-label">Pseudophakic (Prior Cataract Sx)</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="lattice" type="checkbox" class="checkbox-input">
                                    <label for="lattice" class="checkbox-label">Lattice Degeneration</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="prev_rd_affected" type="checkbox" class="checkbox-input">
                                    <label for="prev_rd_affected" class="checkbox-label">Prior RD Repair (Affected Eye)</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="prev_rd_fellow" type="checkbox" class="checkbox-input">
                                    <label for="prev_rd_fellow" class="checkbox-label">History of RD (Fellow Eye)</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="family_history_rd" type="checkbox" class="checkbox-input">
                                    <label for="family_history_rd" class="checkbox-label">Family History of RD</label>
                                </div>
                            </div>
                            <!-- Column 2 -->
                            <div class="space-y-3">
                                <div class="checkbox-item">
                                    <input id="diabetes" type="checkbox" class="checkbox-input">
                                    <label for="diabetes" class="checkbox-label">Diabetes</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="uveitis" type="checkbox" class="checkbox-input">
                                    <label for="uveitis" class="checkbox-label">History of Uveitis</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="retinitis" type="checkbox" class="checkbox-input">
                                    <label for="retinitis" class="checkbox-label">History of Retinitis (e.g., CMV)</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="rop" type="checkbox" class="checkbox-input">
                                    <label for="rop" class="checkbox-label">History of ROP</label>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Section 3: Presenting Exam & Surgical Plan -->
                    <div class="pt-4 border-t border-gray-200">
                        <h2 class="section-header">Presenting Exam & Surgical Plan</h2>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-4">
                            <div>
                                <label for="preop_va" class="form-label">Pre-operative VA (LogMAR)</label>
                                <input type="number" id="preop_va" class="form-input" value="1.0" step="0.1" min="0" max="3.0">
                                <p id="va-helper" class="text-xs text-gray-500 mt-1">Snellen: 20/200</p>
                            </div>
                            <div>
                                <label for="repair_method" class="form-label">Method of Repair</label>
                                <select id="repair_method" class="form-select">
                                    <option value="ppv">Pars Plana Vitrectomy (PPV)</option>
                                    <option value="sb">Scleral Buckle (SB)</option>
                                    <option value="ppv_sb">PPV + Scleral Buckle</option>
                                    <option value="pnr">Pneumatic Retinopexy (PnR)</option>
                                </select>
                            </div>
                            <div>
                                <label for="macula_status" class="form-label">Macula Status</label>
                                <select id="macula_status" class="form-select">
                                    <option value="on">Macula-On</option>
                                    <option value="off">Macula-Off</option>
                                </select>
                            </div>
                            <div>
                                <label for="duration" class="form-label">Duration of Detachment (days)</label>
                                <input type="number" id="duration" class="form-input" value="3" min="0">
                            </div>
                            <div>
                                <label for="extent" class="form-label">Extent of Detachment (Clock Hours)</label>
                                <input type="number" id="extent" class="form-input" value="4" min="1" max="12" step="1">
                            </div>
                            <div>
                                <label for="location" class="form-label">Detachment Location</label>
                                <select id="location" class="form-select">
                                    <option value="superior">Superior (10-2)</option>
                                    <option value="temporal">Temporal (2-4 or 8-10)</option>
                                    <option value="inferior">Inferior (4-8)</option>
                                    <option value="nasal">Nasal</option>
                                    <option value="total">Total</option>
                                </select>
                            </div>

                            <!-- Exam Checkboxes -->
                            <div class="space-y-3 md:col-span-2 grid grid-cols-2 gap-x-6">
                                <div class="checkbox-item">
                                    <input id="pvr" type="checkbox" class="checkbox-input">
                                    <label for="pvr" class="checkbox-label">Presence of PVR (Grade C+)</label>
                                    <div class="info-bubble">
                                        <svg class="info-bubble-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" /></svg>
                                        <span class="info-bubble-text">Proliferative Vitreoretinopathy Grade C or worse at presentation.</span>
                                    </div>
                                </div>
                                <div class="checkbox-item">
                                    <input id="trauma" type="checkbox" class="checkbox-input">
                                    <label for="trauma" class="checkbox-label">Traumatic Cause</label>
                                </div>
                                <div class="checkbox-item">
                                    <input id="pvd" type="checkbox" class="checkbox-input">
                                    <label for="pvd" class="checkbox-label">Posterior Vitreous Detachment</label>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Calculate Button -->
                    <div class="pt-6 mt-6 border-t border-gray-300">
                        <button id="calculate-btn" type="button" class="w-full rounded-md bg-blue-600 px-4 py-3 text-lg font-semibold text-white shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
                            Calculate Risk
                        </button>
                    </div>
                </form>
            </div>

            <!-- Results Section (Spans 1 column) -->
            <div class="lg:col-span-1">
                <div class="bg-white p-6 rounded-lg shadow-lg border border-gray-200 sticky top-8">
                    <h2 class="section-header">Predicted Outcomes</h2>
                    <div id="results-placeholder" class="text-center text-gray-500 py-16">
                        <p>Results will be displayed here after calculation.</p>
                    </div>
                    <div id="results-container" class="space-y-6 hidden">
                        <!-- Single Surgery Success -->
                        <div class="text-center">
                            <div class="text-base font-medium text-gray-600">Chance of Single Surgery Success</div>
                            <div id="result-sss" class="text-6xl font-bold text-blue-600">--%</div>
                            <p class="text-sm text-gray-500">(Primary anatomic success at 90 days)</p>
                        </div>

                        <!-- Predicted VA -->
                        <div class="text-center pt-4 border-t">
                            <div class="text-base font-medium text-gray-600">Predicted 6-Month Visual Acuity</div>
                            <div id="result-va" class="text-4xl font-semibold text-gray-800">20/---</div>
                            <p id="result-va-logmar" class="text-sm text-gray-500">(LogMAR: --)</p>
                        </div>

                        <!-- Complications -->
                        <div class="pt-4 border-t">
                            <h3 class="text-lg font-semibold text-gray-800 mb-3 text-center">Estimated Complication Risk</h3>
                            <div class="space-y-3">
                                <div class="flex justify-between items-center bg-gray-50 p-3 rounded-md">
                                    <span class="font-medium text-gray-700">Epiretinal Membrane (ERM)</span>
                                    <span id="result-erm" class="font-bold text-lg text-red-600">--%</span>
                                </div>
                                <div class="flex justify-between items-center bg-gray-50 p-3 rounded-md">
                                    <span class="font-medium text-gray-700">Post-op Cataract (within 2yrs)</span>
                                    <span id="result-cataract" class="font-bold text-lg text-red-600">--%</span>
                                </div>
                                <div class="flex justify-between items-center bg-gray-50 p-3 rounded-md">
                                    <span class="font-medium text-gray-700">Other Complications</span>
                                    <span id="result-other" class="font-bold text-lg text-red-600">--%</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>

    <script>
        document.getElementById('calculate-btn').addEventListener('click', calculateRisk);
        document.getElementById('preop_va').addEventListener('input', updateVaHelper);

        function logMarToSnellen(logMAR) {
            const snellenDenominator = 20 * Math.pow(10, logMAR);
            if (snellenDenominator <= 20) return "20/20";
            if (snellenDenominator < 30) return "20/25";
            if (snellenDenominator < 50) return "20/40";
            if (snellenDenominator < 70) return "20/60";
            if (snellenDenominator < 90) return "20/80";
            if (snellenDenominator < 150) return "20/100";
            if (snellenDenominator < 300) return "20/200";
            if (snellenDenominator < 600) return "20/400";
            if (snellenDenominator < 1000) return "20/800";
            if (logMAR >= 1.8 && logMAR < 2.3) return "Count Fingers";
            if (logMAR >= 2.3 && logMAR < 2.8) return "Hand Motion";
            if (logMAR >= 2.8 && logMAR < 3.0) return "Light Perception";
            if (logMAR >= 3.0) return "No Light Perception";
            return ">20/800";
        }

        function updateVaHelper() {
            const logMAR = parseFloat(document.getElementById('preop_va').value);
            const helper = document.getElementById('va-helper');
            if (isNaN(logMAR)) {
                helper.textContent = 'Please enter a LogMAR value.';
            } else {
                helper.textContent = `Snellen: ${logMarToSnellen(logMAR)}`;
            }
        }

        function calculateRisk() {
            // 1. GET ALL INPUTS FROM THE FORM
            // ===================================
            const inputs = {
                // Demographics
                age: parseFloat(document.getElementById('age').value) || 60,
                gender: document.getElementById('gender').value,
                
                // Ocular History
                myopia: document.getElementById('myopia').checked ? 1 : 0,
                cataract_sx: document.getElementById('cataract_sx').checked ? 1 : 0,
                lattice: document.getElementById('lattice').checked ? 1 : 0,
                prev_rd_affected: document.getElementById('prev_rd_affected').checked ? 1 : 0,
                prev_rd_fellow: document.getElementById('prev_rd_fellow').checked ? 1 : 0,
                family_history_rd: document.getElementById('family_history_rd').checked ? 1 : 0,
                diabetes: document.getElementById('diabetes').checked ? 1 : 0,
                uveitis: document.getElementById('uveitis').checked ? 1 : 0,
                retinitis: document.getElementById('retinitis').checked ? 1 : 0,
                rop: document.getElementById('rop').checked ? 1 : 0,

                // Presenting Exam & Plan
                preop_va: parseFloat(document.getElementById('preop_va').value) || 1.0,
                method: document.getElementById('repair_method').value,
                macula_status: document.getElementById('macula_status').value,
                duration: parseFloat(document.getElementById('duration').value) || 0,
                extent: parseInt(document.getElementById('extent').value) || 1,
                location: document.getElementById('location').value,
                pvr: document.getElementById('pvr').checked ? 1 : 0,
                trauma: document.getElementById('trauma').checked ? 1 : 0,
                pvd: document.getElementById('pvd').checked ? 1 : 0
            };

            // 2. DEFINE YOUR STATISTICAL MODELS
            // =================================================================
            // !!! IMPORTANT: PLACEHOLDER COEFFICIENTS !!!
            // These MUST be replaced with real coefficients from your statistical model.

            // --- Model 1: Single Surgery Success (Logistic Regression) ---
            const sssCoeffs = {
                intercept: 3.0,
                age: -0.015,
                gender_male: 0.1,
                preop_va: -0.25,
                method_ppv: 0.1,
                method_sb: 0.0,
                method_ppv_sb: 0.2,
                method_pnr: -0.15,
                macula_off: -0.6,
                duration: -0.01,
                extent: -0.1,
                location_inferior: -0.3,
                pvr: -1.8,
                myopia: -0.1,
                lattice: -0.05,
                trauma: -0.4,
                cataract_sx: 0.1,
                prev_rd_affected: -1.2,
                prev_rd_fellow: -0.1,
                family_history_rd: -0.05,
                diabetes: -0.2,
                uveitis: -0.3,
                retinitis: -0.4,
                rop: -0.3,
                pvd: 0.1
            };

            // --- Model 2: Visual Acuity Outcome (Linear Regression, predicts LogMAR) ---
            const vaCoeffs = {
                intercept: 1.0,
                age: 0.005,
                preop_va: 0.45,
                macula_on: -0.7,
                macula_off_duration: 0.01, // Interaction term
                pvr: 0.3,
                trauma: 0.2,
                extent: 0.05
            };

            // --- Model 3: ERM Complication (Logistic Regression) ---
            const ermCoeffs = {
                intercept: -3.5,
                method_ppv: 0.6,
                method_ppv_sb: 0.7,
                pvr: 0.8,
                lattice: 0.1,
                diabetes: 0.2,
                age: 0.01
            };
            
            // --- Model 4: Cataract Complication (Logistic Regression) ---
            const cataractCoeffs = {
                intercept: -2.5,
                method_ppv: 1.8,
                method_ppv_sb: 1.9,
                age: 0.03,
                diabetes: 0.1
            };

            // 3. RUN THE CALCULATIONS
            // ===================================
            
            // --- SSS Calculation ---
            let sssLogOdds = sssCoeffs.intercept;
            sssLogOdds += sssCoeffs.age * inputs.age;
            if (inputs.gender === 'male') sssLogOdds += sssCoeffs.gender_male;
            sssLogOdds += sssCoeffs.preop_va * inputs.preop_va;
            if (inputs.method === 'ppv') sssLogOdds += sssCoeffs.method_ppv;
            if (inputs.method === 'sb') sssLogOdds += sssCoeffs.method_sb;
            if (inputs.method === 'ppv_sb') sssLogOdds += sssCoeffs.method_ppv_sb;
            if (inputs.method === 'pnr') sssLogOdds += sssCoeffs.method_pnr;
            if (inputs.macula_status === 'off') sssLogOdds += sssCoeffs.macula_off;
            sssLogOdds += sssCoeffs.duration * inputs.duration;
            sssLogOdds += sssCoeffs.extent * inputs.extent;
            if (inputs.location === 'inferior') sssLogOdds += sssCoeffs.location_inferior;
            sssLogOdds += sssCoeffs.pvr * inputs.pvr;
            sssLogOdds += sssCoeffs.myopia * inputs.myopia;
            sssLogOdds += sssCoeffs.lattice * inputs.lattice;
            sssLogOdds += sssCoeffs.trauma * inputs.trauma;
            sssLogOdds += sssCoeffs.cataract_sx * inputs.cataract_sx;
            sssLogOdds += sssCoeffs.prev_rd_affected * inputs.prev_rd_affected;
            sssLogOdds += sssCoeffs.prev_rd_fellow * inputs.prev_rd_fellow;
            sssLogOdds += sssCoeffs.family_history_rd * inputs.family_history_rd;
            sssLogOdds += sssCoeffs.diabetes * inputs.diabetes;
            sssLogOdds += sssCoeffs.uveitis * inputs.uveitis;
            sssLogOdds += sssCoeffs.retinitis * inputs.retinitis;
            sssLogOdds += sssCoeffs.rop * inputs.rop;
            sssLogOdds += sssCoeffs.pvd * inputs.pvd;
            
            const sssProbability = 1 / (1 + Math.exp(-sssLogOdds));
            
            // --- VA Calculation ---
            let vaLogMar = vaCoeffs.intercept;
            vaLogMar += vaCoeffs.age * inputs.age;
            vaLogMar += vaCoeffs.preop_va * inputs.preop_va;
            if (inputs.macula_status === 'on') {
                vaLogMar += vaCoeffs.macula_on;
            } else {
                vaLogMar += vaCoeffs.macula_off_duration * inputs.duration;
            }
            vaLogMar += vaCoeffs.pvr * inputs.pvr;
            vaLogMar += vaCoeffs.trauma * inputs.trauma;
            vaLogMar += vaCoeffs.extent * inputs.extent;
            vaLogMar = Math.max(0, vaLogMar); // Cap at 20/20 (LogMAR 0)
            vaLogMar = Math.min(3.0, vaLogMar); // Cap at NLP (LogMAR 3.0)
            
            // --- ERM Calculation ---
            let ermLogOdds = ermCoeffs.intercept;
            if (inputs.method === 'ppv') ermLogOdds += ermCoeffs.method_ppv;
            if (inputs.method === 'ppv_sb') ermLogOdds += ermCoeffs.method_ppv_sb;
            ermLogOdds += ermCoeffs.pvr * inputs.pvr;
            ermLogOdds += ermCoeffs.lattice * inputs.lattice;
            ermLogOdds += ermCoeffs.diabetes * inputs.diabetes;
            ermLogOdds += ermCoeffs.age * inputs.age;
            const ermProbability = 1 / (1 + Math.exp(-ermLogOdds));

            // --- Cataract Calculation ---
            let cataractProbability = 0;
            if (inputs.cataract_sx === 0) { // Only if patient is phakic
                let cataractLogOdds = cataractCoeffs.intercept;
                if (inputs.method === 'ppv') cataractLogOdds += cataractCoeffs.method_ppv;
                if (inputs.method === 'ppv_sb') cataractLogOdds += cataractCoeffs.method_ppv_sb;
                cataractLogOdds += cataractCoeffs.age * inputs.age;
                cataractLogOdds += cataractCoeffs.diabetes * inputs.diabetes;
                cataractProbability = 1 / (1 + Math.exp(-cataractLogOdds));
            }

            // 4. DISPLAY THE RESULTS
            // ===================================
            document.getElementById('results-placeholder').classList.add('hidden');
            document.getElementById('results-container').classList.remove('hidden');

            document.getElementById('result-sss').textContent = `${(sssProbability * 100).toFixed(0)}%`;
            
            const snellen = logMarToSnellen(vaLogMar);
            document.getElementById('result-va').textContent = `${snellen}`;
            document.getElementById('result-va-logmar').textContent = `(LogMAR: ${vaLogMar.toFixed(2)})`;

            document.getElementById('result-erm').textContent = `${(ermProbability * 100).toFixed(0)}%`;
            document.getElementById('result-cataract').textContent = (inputs.cataract_sx === 1) ? 'N/A' : `${(cataractProbability * 100).toFixed(0)}%`;
            
            // Placeholder for other risks (diplopia, ptosis, etc.)
            const otherRisk = Math.max(0.01, (ermProbability * 0.2) + (inputs.method === 'sb' ? 0.03 : 0) + (inputs.trauma * 0.02));
            document.getElementById('result-other').textContent = `${(otherRisk * 100).toFixed(0)}%`;
        }

        // Initial call to set helper text
        updateVaHelper();
    </script>

</body>
</html>
