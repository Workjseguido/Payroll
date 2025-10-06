<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Super Smasher Davao - Payroll System</title>
    <style>
        body {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: #f5f5dc;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #000000, #1a1a2e);
            color: #ffd700;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            margin: 0;
            font-size: 2.5rem;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            margin: 10px 0 0 0;
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .controls {
            padding: 30px;
            background: #f5f5dc;
            border-bottom: 2px solid #1a1a2e;
        }
        
        .control-group {
            display: flex;
            gap: 20px;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .control-item {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }
        
        .control-item label {
            font-weight: 600;
            color: #1a1a2e;
            font-size: 0.9rem;
        }
        
        .control-item input, .control-item select {
            padding: 10px 15px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        
        .control-item input:focus, .control-item select:focus {
            outline: none;
            border-color: #ffd700;
        }
        
        .btn {
            padding: 12px 25px;
            background: linear-gradient(135deg, #ffd700, #ffed4e);
            color: #1a1a2e;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.4);
        }
        
        .payroll-table {
            padding: 30px;
            overflow-x: auto;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 30px;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }
        
        th {
            background: linear-gradient(135deg, #1a1a2e, #000000);
            color: #ffd700;
            padding: 15px 10px;
            text-align: left;
            font-weight: 600;
            font-size: 0.9rem;
        }
        
        td {
            padding: 12px 10px;
            border-bottom: 1px solid #f1f3f4;
            font-size: 0.9rem;
        }
        
        tr:hover {
            background: #f8f9fa;
        }
        
        .payslip-section {
            padding: 30px;
            background: #f5f5dc;
            border-top: 2px solid #1a1a2e;
        }
        
        .payslip {
            background: white;
            border-radius: 10px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            display: none;
        }
        
        .payslip.active {
            display: block;
        }
        
        .payslip-header {
            text-align: center;
            border-bottom: 2px solid #ffd700;
            padding-bottom: 20px;
            margin-bottom: 25px;
        }
        
        .payslip-header h2 {
            color: #1a1a2e;
            margin: 0;
            font-size: 1.8rem;
        }
        
        .payslip-header p {
            color: #1a1a2e;
            margin: 5px 0 0 0;
        }
        
        .payslip-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 25px;
        }
        
        .detail-group h3 {
            color: #1a1a2e;
            margin: 0 0 15px 0;
            font-size: 1.2rem;
            border-bottom: 1px solid #ffd700;
            padding-bottom: 8px;
        }
        
        .detail-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #f8f9fa;
        }
        
        .detail-row:last-child {
            border-bottom: none;
            font-weight: 600;
            color: #1a1a2e;
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .summary-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border-left: 4px solid #ffd700;
        }
        
        .summary-card h3 {
            margin: 0 0 10px 0;
            color: #7f8c8d;
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .summary-card .amount {
            font-size: 1.8rem;
            font-weight: bold;
            color: #1a1a2e;
            margin: 0;
        }
        
        @media print {
            body {
                background: white !important;
                padding: 0 !important;
                margin: 0 !important;
            }
            
            .container {
                box-shadow: none !important;
                border-radius: 0 !important;
                background: white !important;
            }
            
            .header, .controls, .payroll-table, .summary-cards, .timesheet-section {
                display: none !important;
            }
            
            .payslip-section {
                padding: 20px !important;
                background: white !important;
                border: none !important;
            }
            
            .payslip {
                box-shadow: none !important;
                border: 2px solid #1a1a2e !important;
                page-break-inside: avoid;
            }
            
            .payslip-header {
                border-bottom: 2px solid #1a1a2e !important;
            }
            
            .detail-group h3 {
                border-bottom: 1px solid #1a1a2e !important;
            }
        }
        
        @media (max-width: 768px) {
            .control-group {
                flex-direction: column;
                align-items: stretch;
            }
            
            .payslip-details {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .summary-cards {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏢 SUPER SMASHER DAVAO</h1>
            <p>Automated Payroll & Payslip System</p>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <div class="control-item">
                    <label>Pay Period</label>
                    <select id="payPeriod">
                        <option value="twice-monthly" selected>Twice Monthly (15th/30th)</option>
                        <option value="monthly">Monthly</option>
                        <option value="bi-weekly">Bi-Weekly</option>
                        <option value="weekly">Weekly</option>
                    </select>
                </div>
                <div class="control-item">
                    <label>Pay Cut-off</label>
                    <select id="payCutoff">
                        <option value="1-15">1st - 15th</option>
                        <option value="16-30" selected>16th - 30th</option>
                    </select>
                </div>
                <div class="control-item">
                    <label>Pay Date</label>
                    <input type="date" id="payDate" value="2025-01-15">
                </div>
                <div class="control-item">
                    <label>Working Days</label>
                    <input type="number" id="workingDays" value="11" min="1" max="31">
                </div>
            </div>
            <button class="btn" onclick="calculatePayroll()">🧮 Calculate Payroll</button>
            <button class="btn" onclick="showTimesheet()" style="background: linear-gradient(135deg, #ffd700, #ffed4e); color: #1a1a2e; margin-left: 10px;">⏰ Manage Timesheet</button>
            <button class="btn" onclick="exportToGoogleSheets()" style="background: linear-gradient(135deg, #1a1a2e, #000000); color: #ffd700; margin-left: 10px;">📊 Export to Google Sheets</button>
            <button class="btn" onclick="showScheduleManager()" style="background: linear-gradient(135deg, #ffd700, #ffed4e); color: #1a1a2e; margin-left: 10px;">📅 Manage Schedule</button>
        </div>
        
        <div class="timesheet-section" id="timesheetSection" style="display: none; padding: 30px; background: #f5f5dc; border-bottom: 2px solid #1a1a2e;">
            <h2 style="color: #1a1a2e; margin-bottom: 20px;">📋 Employee Timesheet Management</h2>
            <div class="timesheet-controls" style="margin-bottom: 20px;">
                <select id="employeeSelect" style="padding: 10px 15px; border: 2px solid #1a1a2e; border-radius: 8px; margin-right: 10px;">
                    <option value="">Select Employee</option>
                </select>
                <button class="btn" onclick="loadEmployeeTimesheet()" style="margin: 0; padding: 10px 20px;">Load Timesheet</button>
            </div>
            
            <div id="timesheetTable" style="display: none;">
                <table style="margin-bottom: 20px;">
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Check In</th>
                            <th>Break Out</th>
                            <th>Break In</th>
                            <th>Check Out</th>
                            <th>Regular Hrs</th>
                            <th>OT Hrs</th>
                            <th>ND Hrs</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody id="timesheetBody">
                    </tbody>
                </table>
                <button class="btn" onclick="saveTimesheet()">💾 Save Timesheet</button>
                <button class="btn" onclick="hideTimesheet()" style="background: linear-gradient(135deg, #1a1a2e, #000000); color: #ffd700; margin-left: 10px;">❌ Close</button>
            </div>
        </div>
        
        <div class="schedule-section" id="scheduleSection" style="display: none; padding: 30px; background: #f5f5dc; border-bottom: 2px solid #1a1a2e;">
            <h2 style="color: #1a1a2e; margin-bottom: 20px;">📅 Employee Schedule Management</h2>
            <div class="schedule-controls" style="margin-bottom: 20px; display: flex; gap: 15px; align-items: center; flex-wrap: wrap;">
                <select id="scheduleEmployeeSelect" style="padding: 10px 15px; border: 2px solid #1a1a2e; border-radius: 8px;">
                    <option value="">Select Employee</option>
                </select>
                <select id="scheduleWeek" style="padding: 10px 15px; border: 2px solid #1a1a2e; border-radius: 8px;">
                    <option value="current">Current Week</option>
                    <option value="next">Next Week</option>
                </select>
                <button class="btn" onclick="loadEmployeeSchedule()" style="margin: 0; padding: 10px 20px;">Load Schedule</button>
                <button class="btn" onclick="markDayOff()" style="margin: 0; padding: 10px 20px; background: linear-gradient(135deg, #e74c3c, #c0392b); color: white;">🚫 Mark Day Off</button>
            </div>
            
            <div id="scheduleTable" style="display: none;">
                <table style="margin-bottom: 20px;">
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Day</th>
                            <th>Status</th>
                            <th>Shift Start</th>
                            <th>Shift End</th>
                            <th>Break Duration</th>
                            <th>Notes</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody id="scheduleBody">
                    </tbody>
                </table>
                <button class="btn" onclick="saveSchedule()">💾 Save Schedule</button>
                <button class="btn" onclick="hideScheduleManager()" style="background: linear-gradient(135deg, #1a1a2e, #000000); color: #ffd700; margin-left: 10px;">❌ Close</button>
            </div>
        </div>
        
        <div class="summary-cards" id="summaryCards" style="display: none;">
            <div class="summary-card">
                <h3>Total Employees</h3>
                <p class="amount" id="totalEmployees">0</p>
            </div>
            <div class="summary-card">
                <h3>Total Regular Pay</h3>
                <p class="amount" id="totalRegularPay">₱0</p>
            </div>
            <div class="summary-card">
                <h3>Total Overtime Pay</h3>
                <p class="amount" id="totalOvertimePay">₱0</p>
            </div>
            <div class="summary-card">
                <h3>Total Payroll</h3>
                <p class="amount" id="totalPayroll">₱0</p>
            </div>
        </div>
        
        <div class="payroll-table">
            <table id="payrollTable">
                <thead>
                    <tr>
                        <th>Employee Name</th>
                        <th>Position</th>
                        <th>Daily Rate</th>
                        <th>Regular Hours</th>
                        <th>OT Hours</th>
                        <th>ND Hours</th>
                        <th>Regular Pay</th>
                        <th>OT Pay</th>
                        <th>ND Pay</th>
                        <th>Gross Pay</th>
                        <th>Deductions</th>
                        <th>Net Pay</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="payrollBody">
                </tbody>
            </table>
        </div>
        
        <div class="payslip-section">
            <div id="payslipContainer"></div>
        </div>
    </div>

    <script>
        const employees = [
            {
                name: "JASMINE MANLIGRO MUYCO",
                position: "Receptionist",
                dailyRate: 510,
                regularHours: 0,
                otHours: 0,
                ndHours: 0,
                timesheet: [],
                schedule: []
            },
            {
                name: "APRIL MAY GODER TABAR",
                position: "Receptionist",
                dailyRate: 510,
                regularHours: 8,
                otHours: 0,
                ndHours: 0,
                timesheet: [],
                schedule: []
            },
            {
                name: "PRINCESS SEMPIO MESA",
                position: "Utility",
                dailyRate: 500,
                regularHours: 8,
                otHours: 0,
                ndHours: 0,
                timesheet: [],
                schedule: []
            },
            {
                name: "RODA MAE ALBERCA TEOPIS",
                position: "Supervisor",
                dailyRate: 510,
                regularHours: 8,
                otHours: 0,
                ndHours: 0,
                timesheet: [],
                schedule: []
            },
            {
                name: "ANGELICA NEÑEZ LANCIAN",
                position: "Attendant",
                dailyRate: 510,
                regularHours: 8,
                otHours: 0,
                ndHours: 0,
                timesheet: [],
                schedule: []
            }
        ];

        // Initialize employee dropdown
        function initializeEmployeeDropdown() {
            const select = document.getElementById('employeeSelect');
            const scheduleSelect = document.getElementById('scheduleEmployeeSelect');
            
            employees.forEach((employee, index) => {
                const option = document.createElement('option');
                option.value = index;
                option.textContent = employee.name;
                select.appendChild(option);
                
                const scheduleOption = document.createElement('option');
                scheduleOption.value = index;
                scheduleOption.textContent = employee.name;
                scheduleSelect.appendChild(scheduleOption);
            });
        }

        function showTimesheet() {
            document.getElementById('timesheetSection').style.display = 'block';
            document.getElementById('timesheetSection').scrollIntoView({ behavior: 'smooth' });
        }

        function hideTimesheet() {
            document.getElementById('timesheetSection').style.display = 'none';
        }

        function loadEmployeeTimesheet() {
            const employeeIndex = document.getElementById('employeeSelect').value;
            if (employeeIndex === '') {
                alert('Please select an employee first.');
                return;
            }

            const employee = employees[employeeIndex];
            const tbody = document.getElementById('timesheetBody');
            const workingDays = parseInt(document.getElementById('workingDays').value);
            const payCutoff = document.getElementById('payCutoff').value;
            
            // Generate dates for the pay period
            const currentDate = new Date();
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();
            
            let startDate, endDate;
            if (payCutoff === '1-15') {
                startDate = new Date(year, month, 1);
                endDate = new Date(year, month, 15);
            } else {
                startDate = new Date(year, month, 16);
                endDate = new Date(year, month + 1, 0); // Last day of month
            }

            tbody.innerHTML = '';
            
            // Generate timesheet rows for the period
            for (let d = new Date(startDate); d <= endDate; d.setDate(d.getDate() + 1)) {
                // Skip weekends (optional - remove if you work weekends)
                if (d.getDay() === 0 || d.getDay() === 6) continue;
                
                const dateStr = d.toISOString().split('T')[0];
                const existingEntry = employee.timesheet.find(entry => entry.date === dateStr);
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${d.toLocaleDateString('en-US', {month: 'short', day: 'numeric'})}</td>
                    <td><input type="time" value="${existingEntry?.checkIn || '08:00'}" data-field="checkIn" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="time" value="${existingEntry?.breakOut || '12:00'}" data-field="breakOut" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="time" value="${existingEntry?.breakIn || '13:00'}" data-field="breakIn" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="time" value="${existingEntry?.checkOut || '17:00'}" data-field="checkOut" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="number" value="${existingEntry?.regularHours || 8}" data-field="regularHours" data-date="${dateStr}" style="width: 60px; padding: 5px;" step="0.5" min="0"></td>
                    <td><input type="number" value="${existingEntry?.otHours || 0}" data-field="otHours" data-date="${dateStr}" style="width: 60px; padding: 5px;" step="0.5" min="0"></td>
                    <td><input type="number" value="${existingEntry?.ndHours || 0}" data-field="ndHours" data-date="${dateStr}" style="width: 60px; padding: 5px;" step="0.5" min="0"></td>
                    <td><button onclick="calculateDayHours('${dateStr}')" style="padding: 5px 10px; background: #ffd700; color: #1a1a2e; border: none; border-radius: 4px; cursor: pointer; font-weight: 600;">📊 Calc</button></td>
                `;
                tbody.appendChild(row);
            }
            
            document.getElementById('timesheetTable').style.display = 'block';
        }

        function calculateDayHours(dateStr) {
            const inputs = document.querySelectorAll(`[data-date="${dateStr}"]`);
            let checkIn, breakOut, breakIn, checkOut;
            
            inputs.forEach(input => {
                if (input.dataset.field === 'checkIn') checkIn = input.value;
                if (input.dataset.field === 'breakOut') breakOut = input.value;
                if (input.dataset.field === 'breakIn') breakIn = input.value;
                if (input.dataset.field === 'checkOut') checkOut = input.value;
            });
            
            if (checkIn && checkOut) {
                const checkInTime = new Date(`2000-01-01 ${checkIn}`);
                const checkOutTime = new Date(`2000-01-01 ${checkOut}`);
                const breakOutTime = breakOut ? new Date(`2000-01-01 ${breakOut}`) : null;
                const breakInTime = breakIn ? new Date(`2000-01-01 ${breakIn}`) : null;
                
                let totalMinutes = (checkOutTime - checkInTime) / (1000 * 60);
                
                // Subtract break time
                if (breakOutTime && breakInTime) {
                    const breakMinutes = (breakInTime - breakOutTime) / (1000 * 60);
                    totalMinutes -= breakMinutes;
                }
                
                const totalHours = totalMinutes / 60;
                const regularHours = Math.min(totalHours, 8);
                const otHours = Math.max(totalHours - 8, 0);
                
                // Update the inputs
                inputs.forEach(input => {
                    if (input.dataset.field === 'regularHours') input.value = regularHours.toFixed(1);
                    if (input.dataset.field === 'otHours') input.value = otHours.toFixed(1);
                });
            }
        }

        function saveTimesheet() {
            const employeeIndex = document.getElementById('employeeSelect').value;
            if (employeeIndex === '') return;
            
            const employee = employees[employeeIndex];
            const inputs = document.querySelectorAll('#timesheetBody input');
            
            // Clear existing timesheet
            employee.timesheet = [];
            
            // Group inputs by date
            const dateGroups = {};
            inputs.forEach(input => {
                const date = input.dataset.date;
                const field = input.dataset.field;
                
                if (!dateGroups[date]) dateGroups[date] = {};
                dateGroups[date][field] = input.value;
            });
            
            // Save to employee timesheet
            Object.keys(dateGroups).forEach(date => {
                employee.timesheet.push({
                    date: date,
                    ...dateGroups[date]
                });
            });
            
            // Update employee totals for payroll calculation
            let totalRegular = 0, totalOT = 0, totalND = 0;
            employee.timesheet.forEach(entry => {
                totalRegular += parseFloat(entry.regularHours || 0);
                totalOT += parseFloat(entry.otHours || 0);
                totalND += parseFloat(entry.ndHours || 0);
            });
            
            employee.regularHours = totalRegular / employee.timesheet.length || 8;
            employee.otHours = totalOT / employee.timesheet.length || 0;
            employee.ndHours = totalND / employee.timesheet.length || 0;
            
            alert(`Timesheet saved for ${employee.name}!\nTotal Regular Hours: ${totalRegular}\nTotal OT Hours: ${totalOT}\nTotal ND Hours: ${totalND}`);
            
            // Recalculate payroll
            calculatePayroll();
        }

        function calculatePayroll() {
            const workingDays = parseInt(document.getElementById('workingDays').value);
            const payDate = document.getElementById('payDate').value;
            const payPeriod = document.getElementById('payPeriod').value;
            
            const tbody = document.getElementById('payrollBody');
            tbody.innerHTML = '';
            
            let totalEmployees = 0;
            let totalRegularPay = 0;
            let totalOvertimePay = 0;
            let totalPayroll = 0;
            
            employees.forEach((employee, index) => {
                const regularPay = employee.regularHours * workingDays * (employee.dailyRate / 8);
                const overtimePay = employee.otHours * workingDays * (employee.dailyRate / 8) * 1.25;
                const nightDiffPay = employee.ndHours * workingDays * (employee.dailyRate / 8) * 0.10;
                const grossPay = regularPay + overtimePay + nightDiffPay;
                
                // Calculate deductions (SSS, PhilHealth, Pag-IBIG, Tax)
                const sss = Math.min(grossPay * 0.045, 1350); // 4.5% capped at 1350
                const philHealth = Math.min(grossPay * 0.0275, 1800); // 2.75% capped at 1800
                const pagibig = Math.min(grossPay * 0.02, 200); // 2% capped at 200
                const tax = grossPay > 20833 ? (grossPay - 20833) * 0.20 : 0; // Basic tax calculation
                const totalDeductions = sss + philHealth + pagibig + tax;
                const netPay = grossPay - totalDeductions;
                
                totalEmployees++;
                totalRegularPay += regularPay;
                totalOvertimePay += overtimePay;
                totalPayroll += netPay;
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td><strong>${employee.name}</strong></td>
                    <td>${employee.position}</td>
                    <td>₱${employee.dailyRate.toLocaleString()}</td>
                    <td>${employee.regularHours * workingDays}</td>
                    <td>${employee.otHours * workingDays}</td>
                    <td>${employee.ndHours * workingDays}</td>
                    <td>₱${regularPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td>₱${overtimePay.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td>₱${nightDiffPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td><strong>₱${grossPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</strong></td>
                    <td>₱${totalDeductions.toLocaleString('en-US', {minimumFractionDigits: 2})}</td>
                    <td><strong style="color: #27ae60;">₱${netPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</strong></td>
                    <td>
                        <button class="btn" style="margin: 0; padding: 8px 15px; font-size: 0.8rem;" onclick="generatePayslip(${index})">📄 View</button>
                        <button class="btn" style="margin: 0 0 0 5px; padding: 8px 15px; font-size: 0.8rem; background: linear-gradient(135deg, #1a1a2e, #000000); color: #ffd700;" onclick="printPayslip(${index})">🖨️ Print</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Update summary cards
            document.getElementById('totalEmployees').textContent = totalEmployees;
            document.getElementById('totalRegularPay').textContent = `₱${totalRegularPay.toLocaleString('en-US', {minimumFractionDigits: 2})}`;
            document.getElementById('totalOvertimePay').textContent = `₱${totalOvertimePay.toLocaleString('en-US', {minimumFractionDigits: 2})}`;
            document.getElementById('totalPayroll').textContent = `₱${totalPayroll.toLocaleString('en-US', {minimumFractionDigits: 2})}`;
            document.getElementById('summaryCards').style.display = 'grid';
        }

        function generatePayslip(employeeIndex) {
            const employee = employees[employeeIndex];
            const workingDays = parseInt(document.getElementById('workingDays').value);
            const payDate = document.getElementById('payDate').value;
            const payPeriod = document.getElementById('payPeriod').value;
            
            const regularPay = employee.regularHours * workingDays * (employee.dailyRate / 8);
            const overtimePay = employee.otHours * workingDays * (employee.dailyRate / 8) * 1.25;
            const nightDiffPay = employee.ndHours * workingDays * (employee.dailyRate / 8) * 0.10;
            const grossPay = regularPay + overtimePay + nightDiffPay;
            
            const sss = Math.min(grossPay * 0.045, 1350);
            const philHealth = Math.min(grossPay * 0.0275, 1800);
            const pagibig = Math.min(grossPay * 0.02, 200);
            const tax = grossPay > 20833 ? (grossPay - 20833) * 0.20 : 0;
            const totalDeductions = sss + philHealth + pagibig + tax;
            const netPay = grossPay - totalDeductions;
            
            const payCutoff = document.getElementById('payCutoff').value;
            const cutoffText = payCutoff === '1-15' ? '1st - 15th' : '16th - 30th';
            
            const payslipContainer = document.getElementById('payslipContainer');
            payslipContainer.innerHTML = `
                <div class="payslip active">
                    <div class="payslip-header">
                        <h2>🏢 SUPER SMASHER DAVAO</h2>
                        <p>Official Payslip - Twice Monthly (${cutoffText})</p>
                        <p><strong>Pay Date:</strong> ${new Date(payDate).toLocaleDateString('en-US', {year: 'numeric', month: 'long', day: 'numeric'})}</p>
                    </div>
                    
                    <div class="payslip-details">
                        <div class="detail-group">
                            <h3>👤 Employee Information</h3>
                            <div class="detail-row">
                                <span>Name:</span>
                                <span><strong>${employee.name}</strong></span>
                            </div>
                            <div class="detail-row">
                                <span>Position:</span>
                                <span>${employee.position}</span>
                            </div>
                            <div class="detail-row">
                                <span>Daily Rate:</span>
                                <span>₱${employee.dailyRate.toLocaleString()}</span>
                            </div>
                            <div class="detail-row">
                                <span>Working Days:</span>
                                <span>${workingDays} days</span>
                            </div>
                        </div>
                        
                        <div class="detail-group">
                            <h3>💰 Earnings</h3>
                            <div class="detail-row">
                                <span>Regular Pay:</span>
                                <span>₱${regularPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Overtime Pay:</span>
                                <span>₱${overtimePay.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Night Differential:</span>
                                <span>₱${nightDiffPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Gross Pay:</span>
                                <span><strong>₱${grossPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</strong></span>
                            </div>
                        </div>
                        
                        <div class="detail-group">
                            <h3>📉 Deductions</h3>
                            <div class="detail-row">
                                <span>SSS (4.5%):</span>
                                <span>₱${sss.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>PhilHealth (2.75%):</span>
                                <span>₱${philHealth.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Pag-IBIG (2%):</span>
                                <span>₱${pagibig.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Withholding Tax:</span>
                                <span>₱${tax.toLocaleString('en-US', {minimumFractionDigits: 2})}</span>
                            </div>
                            <div class="detail-row">
                                <span>Total Deductions:</span>
                                <span><strong>₱${totalDeductions.toLocaleString('en-US', {minimumFractionDigits: 2})}</strong></span>
                            </div>
                        </div>
                        
                        <div class="detail-group">
                            <h3>💵 Net Pay</h3>
                            <div class="detail-row" style="font-size: 1.2rem; color: #27ae60; background: #f8fff8; padding: 15px; border-radius: 8px; margin-top: 10px;">
                                <span><strong>Take Home Pay:</strong></span>
                                <span><strong>₱${netPay.toLocaleString('en-US', {minimumFractionDigits: 2})}</strong></span>
                            </div>
                        </div>
                    </div>
                    
                    <div style="text-align: center; margin-top: 30px; padding-top: 20px; border-top: 1px solid #ecf0f1; color: #7f8c8d; font-size: 0.9rem;">
                        <p>This is a computer-generated payslip. No signature required.</p>
                        <p>Generated on ${new Date().toLocaleDateString('en-US', {year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit'})}</p>
                    </div>
                </div>
            `;
            
            // Scroll to payslip
            payslipContainer.scrollIntoView({ behavior: 'smooth' });
        }

        function printPayslip(employeeIndex) {
            // Generate payslip first
            generatePayslip(employeeIndex);
            
            // Wait a moment for the payslip to render, then print
            setTimeout(() => {
                window.print();
            }, 500);
        }

        function exportToGoogleSheets() {
            const workingDays = parseInt(document.getElementById('workingDays').value);
            const payDate = document.getElementById('payDate').value;
            const payCutoff = document.getElementById('payCutoff').value;
            const cutoffText = payCutoff === '1-15' ? '1st - 15th' : '16th - 30th';
            
            // Prepare data for export
            let csvData = [];
            
            // Header row
            csvData.push([
                'Export Date',
                'Pay Period',
                'Pay Date',
                'Working Days',
                'Employee Name',
                'Position',
                'Daily Rate',
                'Regular Hours',
                'OT Hours',
                'ND Hours',
                'Regular Pay',
                'OT Pay',
                'ND Pay',
                'Gross Pay',
                'SSS',
                'PhilHealth',
                'Pag-IBIG',
                'Tax',
                'Total Deductions',
                'Net Pay'
            ]);
            
            // Data rows
            employees.forEach(employee => {
                const regularPay = employee.regularHours * workingDays * (employee.dailyRate / 8);
                const overtimePay = employee.otHours * workingDays * (employee.dailyRate / 8) * 1.25;
                const nightDiffPay = employee.ndHours * workingDays * (employee.dailyRate / 8) * 0.10;
                const grossPay = regularPay + overtimePay + nightDiffPay;
                
                const sss = Math.min(grossPay * 0.045, 1350);
                const philHealth = Math.min(grossPay * 0.0275, 1800);
                const pagibig = Math.min(grossPay * 0.02, 200);
                const tax = grossPay > 20833 ? (grossPay - 20833) * 0.20 : 0;
                const totalDeductions = sss + philHealth + pagibig + tax;
                const netPay = grossPay - totalDeductions;
                
                csvData.push([
                    new Date().toLocaleDateString(),
                    `Twice Monthly (${cutoffText})`,
                    payDate,
                    workingDays,
                    employee.name,
                    employee.position,
                    employee.dailyRate,
                    employee.regularHours * workingDays,
                    employee.otHours * workingDays,
                    employee.ndHours * workingDays,
                    regularPay.toFixed(2),
                    overtimePay.toFixed(2),
                    nightDiffPay.toFixed(2),
                    grossPay.toFixed(2),
                    sss.toFixed(2),
                    philHealth.toFixed(2),
                    pagibig.toFixed(2),
                    tax.toFixed(2),
                    totalDeductions.toFixed(2),
                    netPay.toFixed(2)
                ]);
            });
            
            // Convert to CSV format
            const csvContent = csvData.map(row => 
                row.map(field => `"${field}"`).join(',')
            ).join('\n');
            
            // Create and download CSV file
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', `Super_Smasher_Davao_Payroll_${payDate}_${cutoffText.replace(' - ', '-')}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            // Show instructions for Google Sheets
            alert(`📊 Payroll data exported successfully!\n\n📋 To import to Google Sheets:\n1. Open Google Sheets (sheets.google.com)\n2. Create a new spreadsheet\n3. Go to File → Import\n4. Upload the downloaded CSV file\n5. Choose "Replace spreadsheet" and click "Import data"\n\n✅ Your payroll masterlist is ready!`);
        }

        function showScheduleManager() {
            document.getElementById('scheduleSection').style.display = 'block';
            document.getElementById('scheduleSection').scrollIntoView({ behavior: 'smooth' });
        }

        function hideScheduleManager() {
            document.getElementById('scheduleSection').style.display = 'none';
        }

        function loadEmployeeSchedule() {
            const employeeIndex = document.getElementById('scheduleEmployeeSelect').value;
            if (employeeIndex === '') {
                alert('Please select an employee first.');
                return;
            }

            const employee = employees[employeeIndex];
            const tbody = document.getElementById('scheduleBody');
            const weekType = document.getElementById('scheduleWeek').value;
            
            // Calculate week dates
            const today = new Date();
            const currentWeekStart = new Date(today);
            currentWeekStart.setDate(today.getDate() - today.getDay()); // Start of current week (Sunday)
            
            const weekStart = weekType === 'current' ? currentWeekStart : new Date(currentWeekStart.getTime() + 7 * 24 * 60 * 60 * 1000);
            
            tbody.innerHTML = '';
            
            // Generate 7 days for the week
            for (let i = 0; i < 7; i++) {
                const date = new Date(weekStart);
                date.setDate(weekStart.getDate() + i);
                const dateStr = date.toISOString().split('T')[0];
                const dayName = date.toLocaleDateString('en-US', { weekday: 'long' });
                
                const existingSchedule = employee.schedule.find(entry => entry.date === dateStr);
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${date.toLocaleDateString('en-US', {month: 'short', day: 'numeric'})}</td>
                    <td>${dayName}</td>
                    <td>
                        <select data-field="status" data-date="${dateStr}" style="width: 100px; padding: 5px; border: 1px solid #1a1a2e; border-radius: 4px;">
                            <option value="scheduled" ${existingSchedule?.status === 'scheduled' ? 'selected' : ''}>Scheduled</option>
                            <option value="dayoff" ${existingSchedule?.status === 'dayoff' ? 'selected' : ''}>Day Off</option>
                            <option value="sick" ${existingSchedule?.status === 'sick' ? 'selected' : ''}>Sick Leave</option>
                            <option value="vacation" ${existingSchedule?.status === 'vacation' ? 'selected' : ''}>Vacation</option>
                        </select>
                    </td>
                    <td><input type="time" value="${existingSchedule?.shiftStart || '08:00'}" data-field="shiftStart" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="time" value="${existingSchedule?.shiftEnd || '17:00'}" data-field="shiftEnd" data-date="${dateStr}" style="width: 100px; padding: 5px;"></td>
                    <td><input type="number" value="${existingSchedule?.breakDuration || 60}" data-field="breakDuration" data-date="${dateStr}" style="width: 80px; padding: 5px;" min="0" step="15"> min</td>
                    <td><input type="text" value="${existingSchedule?.notes || ''}" data-field="notes" data-date="${dateStr}" style="width: 150px; padding: 5px;" placeholder="Notes..."></td>
                    <td><button onclick="toggleDayOff('${dateStr}')" style="padding: 5px 10px; background: #e74c3c; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: 600;">🚫 Day Off</button></td>
                `;
                tbody.appendChild(row);
            }
            
            document.getElementById('scheduleTable').style.display = 'block';
        }

        function toggleDayOff(dateStr) {
            const statusSelect = document.querySelector(`[data-field="status"][data-date="${dateStr}"]`);
            if (statusSelect.value === 'dayoff') {
                statusSelect.value = 'scheduled';
            } else {
                statusSelect.value = 'dayoff';
            }
            
            // Disable/enable time inputs based on status
            const shiftInputs = document.querySelectorAll(`[data-date="${dateStr}"]`);
            shiftInputs.forEach(input => {
                if (input.dataset.field === 'shiftStart' || input.dataset.field === 'shiftEnd') {
                    input.disabled = statusSelect.value === 'dayoff';
                    if (statusSelect.value === 'dayoff') {
                        input.style.background = '#f0f0f0';
                    } else {
                        input.style.background = 'white';
                    }
                }
            });
        }

        function markDayOff() {
            const employeeIndex = document.getElementById('scheduleEmployeeSelect').value;
            if (employeeIndex === '') {
                alert('Please select an employee and load their schedule first.');
                return;
            }
            
            const selectedDates = [];
            const checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
            
            if (checkboxes.length === 0) {
                // If no checkboxes, mark all visible days as day off
                const statusSelects = document.querySelectorAll('[data-field="status"]');
                statusSelects.forEach(select => {
                    select.value = 'dayoff';
                    toggleDayOff(select.dataset.date);
                });
                alert('All days in the current view have been marked as Day Off.');
            }
        }

        function saveSchedule() {
            const employeeIndex = document.getElementById('scheduleEmployeeSelect').value;
            if (employeeIndex === '') return;
            
            const employee = employees[employeeIndex];
            const inputs = document.querySelectorAll('#scheduleBody input, #scheduleBody select');
            
            // Clear existing schedule for the week
            const weekType = document.getElementById('scheduleWeek').value;
            const today = new Date();
            const currentWeekStart = new Date(today);
            currentWeekStart.setDate(today.getDate() - today.getDay());
            const weekStart = weekType === 'current' ? currentWeekStart : new Date(currentWeekStart.getTime() + 7 * 24 * 60 * 60 * 1000);
            
            // Remove existing entries for this week
            employee.schedule = employee.schedule.filter(entry => {
                const entryDate = new Date(entry.date);
                const weekEnd = new Date(weekStart.getTime() + 6 * 24 * 60 * 60 * 1000);
                return entryDate < weekStart || entryDate > weekEnd;
            });
            
            // Group inputs by date
            const dateGroups = {};
            inputs.forEach(input => {
                const date = input.dataset.date;
                const field = input.dataset.field;
                
                if (date && field) {
                    if (!dateGroups[date]) dateGroups[date] = {};
                    dateGroups[date][field] = input.value;
                }
            });
            
            // Save to employee schedule
            Object.keys(dateGroups).forEach(date => {
                employee.schedule.push({
                    date: date,
                    ...dateGroups[date]
                });
            });
            
            alert(`Schedule saved for ${employee.name}!`);
            
            // Update working days calculation based on scheduled days
            updateWorkingDaysFromSchedule();
        }

        function updateWorkingDaysFromSchedule() {
            // Count scheduled days across all employees for the current pay period
            const payCutoff = document.getElementById('payCutoff').value;
            const currentDate = new Date();
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();
            
            let startDate, endDate;
            if (payCutoff === '1-15') {
                startDate = new Date(year, month, 1);
                endDate = new Date(year, month, 15);
            } else {
                startDate = new Date(year, month, 16);
                endDate = new Date(year, month + 1, 0);
            }
            
            let totalScheduledDays = 0;
            let employeeCount = 0;
            
            employees.forEach(employee => {
                let scheduledDays = 0;
                for (let d = new Date(startDate); d <= endDate; d.setDate(d.getDate() + 1)) {
                    const dateStr = d.toISOString().split('T')[0];
                    const scheduleEntry = employee.schedule.find(entry => entry.date === dateStr);
                    
                    if (!scheduleEntry || scheduleEntry.status === 'scheduled') {
                        // Skip weekends by default
                        if (d.getDay() !== 0 && d.getDay() !== 6) {
                            scheduledDays++;
                        }
                    }
                }
                if (scheduledDays > 0) {
                    totalScheduledDays += scheduledDays;
                    employeeCount++;
                }
            });
            
            if (employeeCount > 0) {
                const averageWorkingDays = Math.round(totalScheduledDays / employeeCount);
                document.getElementById('workingDays').value = averageWorkingDays;
            }
        }

        // Initialize with default calculation
        window.onload = function() {
            initializeEmployeeDropdown();
            calculatePayroll();
        };
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'98a292223544a9a2',t:'MTc1OTcyNjU3Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
