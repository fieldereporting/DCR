<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Daily Call Reporting</title>
<style>
    @media (max-width: 768px) {
      .container { padding: 15px; }
      input, select, button, textarea { font-size: 1em; padding: 12px; }
    }
    @media (max-width: 480px) {
      .mtp-table th, .mtp-table td { font-size: 0.9em; }
    }
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f9f9f9; }
    .container { padding: 20px; max-width: 800px; margin: auto; }
    .section { display: none; }
    .section.active { display: block; background: #fff; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.05); }
    input, select, button, textarea {
      width: 100%; margin: 10px 0; padding: 12px;
      font-size: 1rem; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box;
    }
    button { background-color: #007bff; color: #fff; border: none; cursor: pointer; }
    button:hover { background-color: #0056b3; }
    button:disabled { background-color: #cccccc; cursor: not-allowed; } /* Added disabled style */
    label { font-weight: bold; display: block; margin-top: 10px; }
    .mtp-table {
      overflow-x: auto; display: block; width: 100%; border-collapse: collapse; margin-top: 20px;
    }
    .mtp-table th, .mtp-table td { padding: 10px; border: 1px solid #ccc; cursor: pointer; }
    .mtp-table select[multiple] { height: 100px; }
    .mtp-table td[contenteditable] { background: #eef; }
    .popup {
      display: none; position: fixed; top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      background: #fff; padding: 20px; border-radius: 10px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1); text-align: center; z-index: 1000;
      min-width: 300px; /* Ensure popup is readable */
    }
    .popup.active { display: block; }
    .popup .popup-btn {
      background-color: #007bff; color: white;
      padding: 10px 20px; font-size: 1rem; border: none; cursor: pointer; border-radius: 6px;
      width: auto; /* Allow buttons to size naturally */
      margin: 5px; /* Spacing between buttons */
    }
    .header {
      background-color: #004080; color: white;
      padding: 10px 20px;
      display: flex;
      justify-content: space-between;
      max-width: 500px;
      margin: 0 auto;
    }
    .header button {
      background: none; border: none; color: white; font-size: 1rem; cursor: pointer;
    }
    .header button:hover { text-decoration: underline; }
    .hidden { display: none; }
    /* Dropdown menu styles */
    .dropdown {
      position: relative;
      display: inline-block;
    }
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #004080;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;
    }
    .dropdown-content a {
      color: white;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      cursor: pointer;
    }
    .dropdown-content a:hover {
      background-color: #0056b3;
    }
    .dropdown:hover .dropdown-content {
      display: block;
    }
    .submenu {
      position: absolute;
      left: 100%;
      top: 0;
      display: none;
      background-color: #004080;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    }
    .dropdown-content .dropdown-item:hover .submenu {
      display: block;
    }
    #dayPlanDetails {
      background: #f9f9f9;
      padding: 15px;
      border-radius: 8px;
      margin-top: 20px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    #dayPlanDetails h3 {
      margin-top: 0;
    }
    #dayPlanDetails button {
      display: inline-block;
      width: auto;
      margin-right: 10px;
      margin-top: 15px;
    }
    /* Calendar styles */
    .calendar {
      margin: 20px 0;
      border-collapse: collapse;
      width: 100%;
    }
    .calendar th, .calendar td {
      border: 1px solid #ddd;
      text-align: center;
      padding: 8px;
    }
    .calendar th {
      background-color: #f2f2f2;
    }
    .calendar .today {
      background-color: #d4edda;
    }
    .calendar td {
      height: 80px;
      vertical-align: top;
      position: relative;
    }
    .calendar .day-number {
      font-weight: bold;
      margin-bottom: 5px;
    }
    .calendar .day-content {
      font-size: 0.8em;
    }
    .calendar td.has-plan {
      background-color: #e0f7fa;
    }
    .day-details {
      margin: 5px 0;
      font-size: 0.75em;
      color: #555;
    }
    .day-details strong {
      display: block;
      margin-top: 3px;
    }
    .stp-based {
      background-color: #ffecb3; /* Light yellow background to indicate STP-based plans */
    }
    /* Added style for frozen cells */
    .frozen-cell {
      background-color: #e0e0e0; /* Grey out frozen cells */
      cursor: not-allowed;
      opacity: 0.7;
    }
    #mtpStatusMessage {
      text-align: center;
      color: #d9534f; /* Red for warning/info */
      font-weight: bold;
      margin-bottom: 10px;
    }
    /* New styles for validation errors */
    input.error {
      border: 2px solid #d9534f; /* Red border for invalid input */
    }
    .error-message {
      color: #d9534f; /* Red text for error message */
      font-size: 0.9em;
      margin-top: -8px; /* Pull it closer to the input */
      margin-bottom: 10px;
      display: block; /* Ensure it takes its own line */
    }
    /* New popup for upcoming month prompt */
    #proceedUpcomingMonthPopup {
      background: #fff;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
      max-width: 350px;
      text-align: center;
    }
    #proceedUpcomingMonthPopup .popup-btn {
      margin: 10px;
      width: 120px;
    }
    /* DCR Tab Styles */
    .dcr-tabs {
        display: flex;
        margin-bottom: 20px;
    }
    .dcr-tab-button {
        flex: 1;
        padding: 15px;
        background-color: #f2f2f2;
        border: 1px solid #ddd;
        border-bottom: none;
        cursor: pointer;
        font-weight: bold;
        text-align: center;
        border-radius: 8px 8px 0 0;
        margin-right: 5px;
    }
    .dcr-tab-button:last-child {
        margin-right: 0;
    }
    .dcr-tab-button.active {
        background-color: #007bff;
        color: white;
        border-color: #007bff;
    }
    .dcr-tab-content {
        border: 1px solid #ddd;
        border-top: none;
        padding: 20px;
        border-radius: 0 0 8px 8px;
    }
    .product-qty-row {
        display: flex;
        align-items: center;
        margin-bottom: 10px;
    }
    .product-qty-row label {
        flex: 1;
        margin: 0;
        font-weight: normal;
    }
    .product-qty-row input[type="number"] {
        flex: 0 0 80px; /* Fixed width for quantity box */
        margin: 0 0 0 10px;
        padding: 8px;
        text-align: center;
    }
    .product-qty-header {
        display: flex;
        justify-content: space-between;
        font-weight: bold;
        margin-top: 15px;
        margin-bottom: 5px;
        padding-right: 90px; /* Align with input field */
    }

    /* Custom Modal Styles */
    .custom-modal-overlay {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        z-index: 1100;
        justify-content: center;
        align-items: center;
    }
    .custom-modal-content {
        background: #fff;
        padding: 30px;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        text-align: center;
        max-width: 400px;
        width: 90%;
        position: relative;
    }
    .custom-modal-content h3 {
        margin-top: 0;
        color: #333;
    }
    .custom-modal-content p {
        margin-bottom: 20px;
        color: #555;
    }
    .custom-modal-content .modal-buttons button {
        margin: 0 10px;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1em;
    }
    .custom-modal-content .modal-buttons .modal-ok-btn {
        background-color: #007bff;
        color: white;
    }
    .custom-modal-content .modal-buttons .modal-cancel-btn {
        background-color: #6c757d;
        color: white;
    }

    /* Report Specific Styles */
    .report-section h3 {
      margin-top: 20px;
      margin-bottom: 15px;
      color: #004080;
    }
    .report-section table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
    }
    .report-section th, .report-section td {
      border: 1px solid #ddd;
      padding: 8px;
      text-align: left;
    }
    .report-section th {
      background-color: #f2f2f2;
      font-weight: bold;
    }
    .report-filter-controls {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      align-items: center;
    }
    .report-filter-controls label {
      margin: 0;
      width: auto;
    }
    .report-filter-controls input[type="date"],
    .report-filter-controls select {
      flex: 1;
      max-width: 200px;
      margin: 0;
    }
    .report-summary-box {
        background-color: #e9ecef;
        padding: 15px;
        border-radius: 8px;
        margin-bottom: 20px;
        font-size: 0.95em;
    }
    .report-summary-box p {
        margin: 5px 0;
    }
    .report-summary-box strong {
        color: #004080;
    }

    /* STP View specific styles */
    #stpViewContent table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 20px;
    }
    #stpViewContent th, #stpViewContent td {
        border: 1px solid #ccc;
        padding: 8px;
        text-align: left;
    }
    #stpViewContent th {
        background-color: #f2f2f2;
    }
    #stpViewContent ul {
        padding-left: 20px;
        margin: 0;
    }
    #stpViewContent li {
        margin-bottom: 3px;
    }
</style>
</head>
<body>
<h1 style="text-align: center; padding-top: 20px;">Daily Call Reporting</h1>
<div class="header hidden" id="mainHeader">
<button onclick="goHome()">Home</button>
<div class="dropdown">
  <button>Activities</button>
  <div class="dropdown-content">
    <a href="#" onclick="nextSection('mtp')">MTP Entry</a>
    <a href="#" onclick="nextSection('dcr')">DCR Entry</a>
  </div>
</div>
<div class="dropdown">
<button>Reports</button>
<div class="dropdown-content">
<a href="#" onclick="showDayReport()">Day Report</a>
<a href="#" onclick="showMonthlyReport()">Monthly Report</a>
<a href="#" onclick="showMTPView()">MTP View</a> <!-- New MTP View Link -->
<a href="#" onclick="showSTPView()">STP View</a> <!-- New STP View Link -->
</div>
</div>
<button onclick="logout()">Logout</button>
</div>
<div class="container">
<div class="section active" id="login">
<h2>Login</h2>
<input id="username" placeholder="Username" type="text"/>
<input id="password" placeholder="Password" type="password"/>
<button onclick="login()">Login</button>
</div>
<div class="section" id="dashboard">
<h2>Welcome</h2>
<p style="text-align: center; font-size: 1.2em;">
<span id="dashboardMessage">Submit your STP in order to proceed further.</span>
<a href="#" id="stpLink" onclick="nextSection('stp')">Submit STP</a>
</p>
<div class="hidden" id="dashboardOptions">
</div>
</div>
<div class="section" id="stp">
<h2>STP Submission</h2>
<div style="display: grid; grid-template-columns: 1fr 1fr 1fr 1fr; gap: 10px; font-weight: bold; margin-bottom: 10px;">
<div>Day/Week</div>
<div>Territory</div>
<div>Doctor</div>
<div>Chemist</div>
</div>
<form id="stpForm"></form>
<button onclick="validateSTP()">Submit STP</button>
</div>
<div class="section" id="mtp">
<h2>MTP - Monthly Tour Plan</h2>
<div id="monthDisplay"></div>
<div id="mtpStatusMessage"></div> <div id="mtpCalendar"></div>
<div class="hidden" id="dayPlanDetails">
<h3>Edit Day Plan</h3>
<div id="selectedDayInfo"></div>
<label>Territory</label>
<select id="dayPlanTerritory">
<option value="">Select Territory</option>
</select>
<label>Doctors</label>
<select id="dayPlanDoctors" multiple=""></select>
<label>Chemists</label>
<select id="dayPlanChemists" multiple=""></select>
<button onclick="saveDayPlan()">Save Day Plan</button>
<button onclick="cancelDayPlan()">Cancel</button>
</div>
<button onclick="submitMTP()" id="submitMTPButton">Submit MTP</button> </div>
<div class="section" id="checkin">
<h2 style="text-align: center;">Select Your Mode of Travel for the Day</h2>
<label>Date</label>
<input id="checkinDate" readonly="" type="date"/>
<label>Select Mode</label>
<select id="modeSelect" onchange="handleMode()">
<option value="">Select</option>
<option value="car">Car</option>
<option value="others">Others</option>
</select>
</div>
<div class="section" id="carMode">
<h2>Car Mode</h2>
<label>Starting KM</label>
<input id="startKM" placeholder="Enter Starting KM" type="number"/>
<label>Territory</label>
<select id="carTerritory" multiple="">
<option>Colombo1</option><option>Colombo2</option><option>Colombo3</option><option>Colombo4</option><option>Colombo5</option>
</select>
<label>Remarks</label>
<textarea id="carRemarks" placeholder="Enter Remarks"></textarea>
<button onclick="nextSection('dcr')">Submit</button>
</div>
<div class="section" id="otherMode">
<h2>Others Mode</h2>
<label>Territory</label>
<select id="otherTerritory" multiple="">
<option>Colombo1</option><option>Colombo2</option><option>Colombo3</option><option>Colombo4</option><option>Colombo5</option>
</select>
<label>Remarks</label>
<textarea id="otherRemarks" placeholder="Enter Remarks"></textarea>
<button onclick="nextSection('dcr')">Submit</button>
</div>
<div class="section" id="dcr">
    <h2>DCR Submission</h2>
    
    <label for="dcrTerritory">Territory</label>
    <select id="dcrTerritory" onchange="handleDcrTerritoryChange()">
        <option>Colombo1</option><option>Colombo2</option><option>Colombo3</option><option>Colombo4</option><option>Colombo5</option>
    </select>

    <div class="dcr-tabs">
        <button class="dcr-tab-button active" onclick="showDcrTab('doctor')">Doctor</button>
        <button class="dcr-tab-button" onclick="showDcrTab('chemist')">Chemist</button>
    </div>

    <div id="doctorDcrContent" class="dcr-tab-content">
        <label for="dcrDoctor">Select Doctor</label>
        <select id="dcrDoctor"></select>

        <label for="jointWork">Joint Work Selection</label>
        <select id="jointWork" multiple>
            <option value="ASM">ASM</option>
            <option value="RSM">RSM</option>
            <option value="ZSM">ZSM</option>
        </select>

        <div class="product-qty-header">
            <span>Product</span>
            <span>Sample Qty</span>
        </div>
        <div id="productQuantities">
            </div>

        <label for="dcrDoctorRemarks">Remarks</label>
        <textarea id="dcrDoctorRemarks" placeholder="Enter Remarks"></textarea>

        <button onclick="submitDCR('doctor')">Submit Doctor DCR</button>
    </div>

    <div id="chemistDcrContent" class="dcr-tab-content hidden">
        <label for="dcrChemist">Select Chemist</label>
        <select id="dcrChemist"></select>

        <label for="dcrChemistRemarks">Remarks</label>
        <textarea id="dcrChemistRemarks" placeholder="Enter Remarks"></textarea>

        <button onclick="submitDCR('chemist')">Submit Chemist DCR</button>
    </div>
</div>
<div class="section" id="checkout">
    <h2>Check-Out</h2>
    <div id="endKMContainer" class="hidden"> 
        <label>Ending KM</label>
        <input id="endKM" type="number"/>
        <span class="error-message" id="endKMError"></span> 
    </div>
    <label>Territory</label>
    <select id="checkoutTerritory"></select> 
    <label>Remarks</label>
    <textarea id="checkoutRemarks"></textarea>
    <button onclick="finalSubmit()">Submit</button>
</div>
<div class="section report-section" id="dayReport">
    <h2>Day Report</h2>
    <div class="report-filter-controls">
        <label for="dayReportDate">Select Date:</label>
        <input type="date" id="dayReportDate" onchange="generateDayReport()">
    </div>
    <div id="dayReportContent">
        <p>Select a date to view the day report.</p>
    </div>
    <button onclick="goHome()">Back to Home</button>
</div>
<div class="section report-section" id="monthlyReport">
    <h2>Monthly Report</h2>
    <div class="report-filter-controls">
        <label for="monthReportMonth">Select Month:</label>
        <select id="monthReportMonth" onchange="generateMonthlyReport()">
            <option value="0">January</option>
            <option value="1">February</option>
            <option value="2">March</option>
            <option value="3">April</option>
            <option value="4">May</option>
            <option value="5">June</option>
            <option value="6">July</option>
            <option value="7">August</option>
            <option value="8">September</option>
            <option value="9">October</option>
            <option value="10">November</option>
            <option value="11">December</option>
        </select>
        <label for="monthReportYear">Select Year:</label>
        <select id="monthReportYear" onchange="generateMonthlyReport()"></select>
    </div>
    <div id="monthlyReportContent">
        <p>Select a month and year to view the monthly report.</p>
    </div>
    <button onclick="goHome()">Back to Home</button>
</div>

<!-- New MTP View Section -->
<div class="section report-section" id="mtpView">
    <h2>MTP View</h2>
    <div class="report-filter-controls">
        <label for="mtpViewMonth">Select Month:</label>
        <select id="mtpViewMonth" onchange="generateMTPView()">
            <option value="0">January</option>
            <option value="1">February</option>
            <option value="2">March</option>
            <option value="3">April</option>
            <option value="4">May</option>
            <option value="5">June</option>
            <option value="6">July</option>
            <option value="7">August</option>
            <option value="8">September</option>
            <option value="9">October</option>
            <option value="10">November</option>
            <option value="11">December</option>
        </select>
        <label for="mtpViewYear">Select Year:</label>
        <select id="mtpViewYear" onchange="generateMTPView()"></select>
    </div>
    <div id="mtpViewCalendarContent">
        <p>Select a month and year to view the submitted MTP.</p>
    </div>
    <button onclick="goHome()">Back to Home</button>
</div>

<!-- New STP View Section -->
<div class="section report-section" id="stpView">
    <h2>STP View</h2>
    <div id="stpViewContent">
        <p>No STP data submitted yet.</p>
    </div>
    <button onclick="goHome()">Back to Home</button>
</div>

</div>

<!-- Custom Modal for Alerts and Confirms -->
<div class="custom-modal-overlay" id="customAlertModal">
    <div class="custom-modal-content">
        <h3 id="customAlertTitle"></h3>
        <p id="customAlertMessage"></p>
        <div class="modal-buttons">
            <button class="modal-ok-btn" onclick="closeCustomModal('customAlertModal')">OK</button>
        </div>
    </div>
</div>

<div class="custom-modal-overlay" id="customConfirmModal">
    <div class="custom-modal-content">
        <h3 id="customConfirmTitle"></h3>
        <p id="customConfirmMessage"></p>
        <div class="modal-buttons">
            <button class="modal-ok-btn" id="confirmOkBtn">Yes</button>
            <button class="modal-cancel-btn" id="confirmCancelBtn">No</button>
        </div>
    </div>
</div>

<!-- Original Popups (kept for compatibility with existing calls, but will be replaced by custom modals) -->
<div class="popup" id="successPopup">
<h3 id="popupMessage">DCR submitted successfully</h3>
<button class="popup-btn" onclick="closePopup('successPopup')">OK</button>
</div>
<div class="popup" id="proceedUpcomingMonthPopup">
    <h3>MTP for the current month is already submitted.</h3>
    <p>Do you want to proceed to plan for the upcoming month, or view the current month's submitted plan?</p>
    <button class="popup-btn" onclick="proceedToUpcomingMonth(true)">Proceed to Upcoming Month</button>
    <button class="popup-btn" onclick="proceedToUpcomingMonth(false)">View Current Month</button>
</div>

<script>
// --- DEBUGGING: Script Loaded confirmation ---
console.log("Script Loaded and running!"); 
// --- END DEBUGGING ---

const days = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
const weekdays = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
const weeks = ['1','2','3','4'];
const territories = ['Colombo1','Colombo2','Colombo3','Colombo4','Colombo5'];
const products = ['Product1', 'Product2', 'Product3', 'Product4']; // Added more products for demonstration

// Doctor list with territory mappings
const doctorsByTerritory = {
  'Colombo1': ['Ramesh', 'Suresh', 'Ganesh'],
  'Colombo2': ['Kumar', 'Dinesh', 'Gopi'],
  'Colombo3': ['Ajesh', 'Ram Kumar'],
  'Colombo4': ['Senthil', 'Paramesh'],
  'Colombo5': ['Ganesh', 'Kumar', 'Senthil']
};

// Chemist list with territory mappings
const chemistsByTerritory = {
  'Colombo1': ['Senthil Pharmacy', 'Kumar Medical store'],
  'Colombo2': ['Ajesh Medicals', 'Santanu Medical Agency'],
  'Colombo3': ['Senthil Medical Store', 'Johnson Pharmacy'],
  'Colombo4': ['Kumar Medical store', 'Senthil Pharmacy'],
  'Colombo5': ['Santanu Medical Agency', 'Johnson Pharmacy']
};

let stpPlan = [];
let mtpPlansData = {}; 
let stpSubmitted = false; // Managed by localStorage
let lastCheckoutDate = null; // Stored as "YYYY-MM-DD" in localStorage to track daily completion

let currentMTPViewedMonthKey = null; 
let selectedDate = null; 

// Store the selected travel mode for the current day, important for checkout logic
let currentTravelMode = '';

// Global MTP entry click counter (persists across sessions)
let mtpEntryGlobalClickCounter = 0; 

// --- New Global Variables for DCR and Daily Summaries ---
let dcrSubmissions = []; // Array to store all DCR entries
let dailySummaries = {}; // Object to store daily checkout summaries, keyed by date (YYYY-MM-DD)

/**
 * Displays a custom alert modal.
 * @param {string} message The message to display.
 * @param {string} [title='Alert'] The title of the alert.
 */
function showAlert(message, title = 'Alert') {
    const modal = document.getElementById('customAlertModal');
    document.getElementById('customAlertTitle').textContent = title;
    document.getElementById('customAlertMessage').textContent = message;
    modal.style.display = 'flex';
}

/**
 * Displays a custom confirmation modal.
 * @param {string} message The message to display.
 * @param {string} [title='Confirm'] The title of the confirmation.
 * @returns {Promise<boolean>} A promise that resolves to true if 'Yes' is clicked, false if 'No'.
 */
function showConfirm(message, title = 'Confirm') {
    return new Promise(resolve => {
        const modal = document.getElementById('customConfirmModal');
        document.getElementById('customConfirmTitle').textContent = title;
        document.getElementById('customConfirmMessage').textContent = message;
        modal.style.display = 'flex';

        const okBtn = document.getElementById('confirmOkBtn');
        const cancelBtn = document.getElementById('confirmCancelBtn');

        const handleOk = () => {
            closeCustomModal('customConfirmModal');
            okBtn.removeEventListener('click', handleOk);
            cancelBtn.removeEventListener('click', handleCancel);
            resolve(true);
        };

        const handleCancel = () => {
            closeCustomModal('customConfirmModal');
            okBtn.removeEventListener('click', handleOk);
            cancelBtn.removeEventListener('click', handleCancel);
            resolve(false);
        };

        okBtn.addEventListener('click', handleOk);
        cancelBtn.addEventListener('click', handleCancel);
    });
}

/**
 * Closes a custom modal.
 * @param {string} modalId The ID of the modal to close.
 */
function closeCustomModal(modalId) {
    document.getElementById(modalId).style.display = 'none';
}


// Set current date in the check-in input field
function setCurrentDate() {
  const today = new Date();
  const dateString = today.toISOString().split('T')[0]; 
  const dateInput = document.getElementById("checkinDate");
  dateInput.value = dateString;
}

async function login() { // Changed to async to await custom confirm
  const u = document.getElementById('username').value;
  const p = document.getElementById('password').value;

  // Simple hardcoded login for demonstration
  if (u === "test" && p === "test") { 
    document.getElementById('mainHeader').classList.remove('hidden');

    // Load current status from localStorage
    stpSubmitted = localStorage.getItem('stpSubmitted') === 'true'; 
    lastCheckoutDate = localStorage.getItem('lastCheckoutDate'); 

    const todayString = new Date().toISOString().split('T')[0]; // Get today's date in "YYYY-MM-DD" format

    // Determine if the user has completed their daily flow for today
    const hasCompletedDayForToday = stpSubmitted && (lastCheckoutDate === todayString);

    // --- DEBUGGING LOGS ---
    console.log("--- Login Attempt Debug ---");
    console.log("stpSubmitted from localStorage:", localStorage.getItem('stpSubmitted'));
    console.log("stpSubmitted (variable):", stpSubmitted);
    console.log("lastCheckoutDate from localStorage:", localStorage.getItem('lastCheckoutDate'));
    console.log("lastCheckoutDate (variable):", lastCheckoutDate);
    console.log("todayString:", todayString);
    console.log("hasCompletedDayForToday:", hasCompletedDayForToday);
    // --- END DEBUGGING LOGS ---

    currentTravelMode = ''; // Reset travel mode on login
    document.getElementById('modeSelect').value = ''; // Clear mode selection on login

    if (!stpSubmitted) {
      console.log("LOGIN PATH: STP NOT SUBMITTED. Redirecting to Dashboard for STP.");
      updateDashboard(); // Sets the correct message and visibility
      nextSection('dashboard');
    } else if (!hasCompletedDayForToday) {
      console.log("LOGIN PATH: STP SUBMITTED, BUT DAY NOT COMPLETED. Redirecting to Check-in.");
      setCurrentDate();
      nextSection('checkin');
    } else {
      console.log("LOGIN PATH: STP SUBMITTED AND DAY COMPLETED. Redirecting to Dashboard.");
      updateDashboard(); // Sets the correct "Welcome" message and shows options
      nextSection('dashboard');
    }

  } else {
    showAlert("Invalid username or password.", "Login Failed"); // Replaced alert
  }
}

function updateDashboard() {
  stpSubmitted = localStorage.getItem('stpSubmitted') === 'true'; // Re-fetch from localStorage
  lastCheckoutDate = localStorage.getItem('lastCheckoutDate'); // Re-fetch from localStorage
  const todayString = new Date().toISOString().split('T')[0];

  if (stpSubmitted && (lastCheckoutDate === todayString)) {
    // If STP is submitted AND the day is completed for today
    document.getElementById('dashboardMessage').textContent = "Welcome to the Daily Call Reporting System (Day Completed)";
    document.getElementById('stpLink').classList.add('hidden');
    document.getElementById('dashboardOptions').classList.remove('hidden');
  } else if (stpSubmitted) {
    // If STP is submitted, but the day is NOT completed for today
    document.getElementById('dashboardMessage').textContent = "Welcome to the Daily Call Reporting System (Please continue your day)";
    document.getElementById('stpLink').classList.add('hidden');
    document.getElementById('dashboardOptions').classList.remove('hidden');
  }
  else {
    // If STP is NOT submitted
    document.getElementById('dashboardMessage').textContent = "Submit your STP in order to proceed further.";
    document.getElementById('stpLink').classList.remove('hidden');
    document.getElementById('dashboardOptions').classList.add('hidden');
  }
}

function logout() {
  document.getElementById('username').value = '';
  document.getElementById('password').value = '';
  document.getElementById('mainHeader').classList.add('hidden');
  
  // STP submitted status persists across logins. DO NOT clear this.
  // localStorage.removeItem('stpSubmitted');

  // MTP plans data should persist across sessions (per requirement 8)
  // localStorage.removeItem('mtpPlansData'); 

  // lastCheckoutDate should persist across sessions (per requirement 7)
  // localStorage.removeItem('lastCheckoutDate'); 

  // Reset in-memory variables for the new session's state
  stpPlan = [];
  currentMTPViewedMonthKey = null;
  currentTravelMode = ''; // Also reset travel mode on logout
  
  nextSection('login');
}

function goHome() {
  updateDashboard();
  nextSection('dashboard');
}

function nextSection(id) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');

  // Additional actions based on section
  if (id === 'mtp') {
    console.log("MTP Entry: Entered MTP section.");
    const isStpSubmittedPersistent = localStorage.getItem('stpSubmitted') === 'true'; 

    if (!isStpSubmittedPersistent) { 
        showAlert("Please submit your STP first to access MTP.", "Access Denied"); // Replaced alert
        goHome();
        return;
    }

    const today = new Date();
    let month = today.getMonth();
    let year = today.getFullYear();
    const currentMonthKey = `${year}-${month}`;
    console.log("Current Month Key for MTP:", currentMonthKey);

    // Ensure mtpPlansData[currentMonthKey] is initialized if it doesn't exist
    if (!mtpPlansData[currentMonthKey]) {
        const lastDay = new Date(year, month + 1, 0);
        let newMonthPlan = [];
        for (let day = 1; day <= lastDay.getDate(); day++) {
          newMonthPlan.push({
            date: new Date(year, month, day),
            territory: '',
            doctors: [],
            chemists: [],
            fromSTP: false
          });
        }
        mtpPlansData[currentMonthKey] = { plan: newMonthPlan, isSubmitted: false };
        applySTPtoMTP(month, year, mtpPlansData[currentMonthKey].plan);
    }
    
    const isFrozen = mtpPlansData[currentMonthKey].isSubmitted;
    console.log("Is MTP for current month submitted (isFrozen):", isFrozen);

    // Increment global MTP click counter and store it
    mtpEntryGlobalClickCounter = parseInt(localStorage.getItem('mtpEntryGlobalClickCounter') || '0', 10);
    mtpEntryGlobalClickCounter++;
    localStorage.setItem('mtpEntryGlobalClickCounter', mtpEntryGlobalClickCounter);
    console.log("Global MTP Entry Click Counter:", mtpEntryGlobalClickCounter);


    // LOGIC REVISED FOR POPUP BEHAVIOR based on "third time" rule
    if (isFrozen) {
        // If MTP is submitted/frozen for the current month
        // Show popup only for the 1st and 2nd global clicks (mtpEntryGlobalClickCounter values 1 and 2)
        if (mtpEntryGlobalClickCounter <= 2) { 
            console.log("Showing popup due to first/second global click and frozen MTP.");
            document.getElementById('proceedUpcomingMonthPopup').classList.add('active');
            // buildMTPCalendar will be called by proceedToUpcomingMonth(true/false)
        } else {
            // For the 3rd global click and onwards, suppress the popup
            console.log("Suppressing popup due to global click counter exceeding limit.");
            buildMTPCalendar(month, year); // Directly show the submitted month
        }
    } else {
        // MTP is NOT submitted/frozen for the current month.
        // Always build the calendar directly for planning. No popup needed here.
        buildMTPCalendar(month, year);
    }
  }
  if (id === 'dcr') {
    // Ensure the territory dropdown is populated if it's not already
    const dcrTerritorySelect = document.getElementById('dcrTerritory');
    // Clear existing options first to prevent duplicates on re-entry to DCR screen
    dcrTerritorySelect.innerHTML = ''; 
    territories.forEach(t => {
        const option = document.createElement('option');
        option.value = t;
        option.text = t;
        dcrTerritorySelect.appendChild(option);
    });
    dcrTerritorySelect.value = territories[0]; // Set a default selected territory

    // Set the initial active tab (Doctor by default)
    showDcrTab('doctor'); 
    // Manually trigger the territory change handler to populate doctors/chemists initially
    handleDcrTerritoryChange(); 

    // Populate product quantities for doctor tab on initial load
    const productQuantitiesDiv = document.getElementById('productQuantities');
    productQuantitiesDiv.innerHTML = ''; // Clear previous content
    products.forEach(product => {
        const row = document.createElement('div');
        row.className = 'product-qty-row';
        row.innerHTML = `
            <label>${product}</label>
            <input type="number" id="qty_${product.replace(/\s/g, '')}" min="0" value="0">
        `;
        productQuantitiesDiv.appendChild(row);
    });
  }
  if (id === 'checkout') {
    // Conditionally show/hide ending KM field based on currentTravelMode
    const endKMContainer = document.getElementById('endKMContainer');
    if (currentTravelMode === 'car') {
        endKMContainer.classList.remove('hidden');
    } else {
        endKMContainer.classList.add('hidden');
        document.getElementById('endKM').value = ''; // Clear value if hidden
        document.getElementById('endKMError').textContent = ''; // Clear error if hidden
    }
    // Call the function to populate the checkout territory dropdown
    populateCheckoutTerritory();
  }
  if (id === 'dayReport') {
      // Set default date to today for day report
      const today = new Date();
      const dateString = today.toISOString().split('T')[0];
      document.getElementById('dayReportDate').value = dateString;
      generateDayReport(); // Generate report for today
  }
  if (id === 'monthlyReport') {
      // Set default month/year for monthly report
      const today = new Date();
      document.getElementById('monthReportMonth').value = today.getMonth();
      const yearSelect = document.getElementById('monthReportYear');
      yearSelect.innerHTML = ''; // Clear previous options
      // Populate years (e.g., current year +/- 5 years)
      for (let i = today.getFullYear() - 5; i <= today.getFullYear() + 5; i++) {
          const option = document.createElement('option');
          option.value = i;
          option.textContent = i;
          yearSelect.appendChild(option);
      }
      yearSelect.value = today.getFullYear();
      generateMonthlyReport(); // Generate report for current month/year
  }
  if (id === 'mtpView') {
      const today = new Date();
      const monthSelect = document.getElementById('mtpViewMonth');
      const yearSelect = document.getElementById('mtpViewYear');

      monthSelect.value = today.getMonth();
      yearSelect.innerHTML = ''; // Clear previous options
      for (let i = today.getFullYear() - 5; i <= today.getFullYear() + 5; i++) {
          const option = document.createElement('option');
          option.value = i;
          option.textContent = i;
          yearSelect.appendChild(option);
      }
      yearSelect.value = today.getFullYear();
      generateMTPView(); // Generate MTP view for current month/year
  }
  if (id === 'stpView') {
      generateSTPView(); // Generate STP view
  }
}

function showDcrTab(tabName) {
    // Hide all tab contents
    document.getElementById('doctorDcrContent').classList.add('hidden');
    document.getElementById('chemistDcrContent').classList.add('hidden');

    // Deactivate all tab buttons
    document.querySelectorAll('.dcr-tab-button').forEach(button => {
        button.classList.remove('active');
    });

    // Show the selected tab content and activate its button
    if (tabName === 'doctor') {
        document.getElementById('doctorDcrContent').classList.remove('hidden');
        document.querySelector('.dcr-tab-button:nth-child(1)').classList.add('active');
        // Re-populate doctors based on current dcrTerritory selection
        const selectedTerritory = document.getElementById('dcrTerritory').value;
        if (selectedTerritory) populateDcrDoctors(selectedTerritory);
    } else if (tabName === 'chemist') {
        document.getElementById('chemistDcrContent').classList.remove('hidden'); // Ensure doctor content is hidden
        document.getElementById('chemistDcrContent').classList.remove('hidden');
        document.querySelector('.dcr-tab-button:nth-child(2)').classList.add('active');
        // Re-populate chemists based on current dcrTerritory selection
        const selectedTerritory = document.getElementById('dcrTerritory').value;
        if (selectedTerritory) populateDcrChemists(selectedTerritory);
    }
}

// Handles change in the main DCR Territory dropdown
function handleDcrTerritoryChange() {
    const selectedTerritory = document.getElementById('dcrTerritory').value;
    // Update doctor and chemist lists based on the active tab
    if (!document.getElementById('doctorDcrContent').classList.contains('hidden')) {
        populateDcrDoctors(selectedTerritory);
    } else if (!document.getElementById('chemistDcrContent').classList.contains('hidden')) {
        populateDcrChemists(selectedTerritory);
    }
}

// Function to populate doctor dropdown for DCR
function populateDcrDoctors(territory) {
    const doctorSelect = document.getElementById('dcrDoctor');
    doctorSelect.innerHTML = '<option value="">Select Doctor</option>';
    if (doctorsByTerritory[territory]) {
        doctorsByTerritory[territory].forEach(doctor => {
            const option = document.createElement('option');
            option.value = doctor;
            option.text = doctor;
            doctorSelect.appendChild(option);
        });
    }
}

// Function to populate chemist dropdown for DCR
function populateDcrChemists(territory) {
    const chemistSelect = document.getElementById('dcrChemist');
    chemistSelect.innerHTML = '<option value="">Select Chemist</option>';
    if (chemistsByTerritory[territory]) {
        chemistsByTerritory[territory].forEach(chemist => {
            const option = document.createElement('option');
            option.value = chemist;
            option.text = chemist;
            chemistSelect.appendChild(option);
        });
    }
}

function proceedToUpcomingMonth(proceed) {
    document.getElementById('proceedUpcomingMonthPopup').classList.remove('active');

    const today = new Date();
    let month = today.getMonth();
    let year = today.getFullYear();
    // The currentMonthKey is implicitly the one that triggered the popup

    if (proceed) {
        // User clicked OK, proceed to next month
        month = (month + 1) % 12;
        if (month === 0) year++; 
        buildMTPCalendar(month, year); 
    } else {
        // User clicked Cancel, stay on the current month's view (which is submitted/frozen)
        buildMTPCalendar(month, year); 
    }
}

function getDayOfWeekString(date) {
  return weekdays[date.getDay()];
}

function getWeekNumberInMonth(date) {
  return Math.ceil(date.getDate() / 7).toString();
}

function updateDoctorsAndChemists(territorySelect, doctorSelect, chemistSelect) {
  const selectedTerritories = Array.from(territorySelect.selectedOptions).map(opt => opt.value);

  doctorSelect.innerHTML = '';
  chemistSelect.innerHTML = '';

  const doctorSet = new Set();
  const chemistSet = new Set();

  selectedTerritories.forEach(territory => {
    if (doctorsByTerritory[territory]) {
      doctorsByTerritory[territory].forEach(doctor => doctorSet.add(doctor));
    }
    if (chemistsByTerritory[territory]) {
      chemistsByTerritory[territory].forEach(chemist => chemistSet.add(chemist));
    }
  });

  doctorSet.forEach(doctor => {
    const option = document.createElement('option');
    option.value = doctor;
    option.text = doctor;
    doctorSelect.appendChild(option);
  });

  chemistSet.forEach(chemist => {
    const option = document.createElement('option');
    option.value = chemist;
    option.text = chemist;
    chemistSelect.appendChild(option);
  });
}

function applySTPtoMTP(month, year, targetMtpPlanArray) {
  if (stpPlan.length === 0) return;

  const lastDay = new Date(year, month + 1, 0);
  const totalDaysInMonth = lastDay.getDate();

  for (let day = 1; day <= totalDaysInMonth; day++) {
    const currentDate = new Date(year, month, day);
    if (currentDate.getMonth() !== month) continue; 

    const dayOfWeek = getDayOfWeekString(currentDate);
    const weekNum = getWeekNumberInMonth(currentDate);

    if (dayOfWeek !== 'Sunday') {
      const stpEntry = stpPlan.find(entry => {
        const [entryDay, entryWeek] = entry.dayWeek.split(' ');
        return entryDay === dayOfWeek && entryWeek === weekNum;
      });

      if (stpEntry) {
        const mtpIndex = targetMtpPlanArray.findIndex(plan =>
          plan.date &&
          plan.date.getDate() === currentDate.getDate() &&
          plan.date.getMonth() === month &&
          plan.date.getFullYear() === year
        );

        if (mtpIndex >= 0) {
          if (!targetMtpPlanArray[mtpIndex].territory || targetMtpPlanArray[mtpIndex].fromSTP || (targetMtpPlanArray[mtpIndex].doctors.length === 0 && targetMtpPlanArray[mtpIndex].chemists.length === 0)) {
            targetMtpPlanArray[mtpIndex] = {
              date: new Date(currentDate),
              territory: stpEntry.territories.join(', '),
              doctors: [...stpEntry.doctors],
              chemists: [...stpEntry.chemists],
              fromSTP: true
            };
          }
        }
      }
    }
  }
}

function validateSTP() {
  const entries = document.querySelectorAll('#stpForm div');
  stpPlan = [];

  let allValid = true;
  for (const div of entries) {
    const selects = div.querySelectorAll('select');
    if (selects.length !== 3) continue;

    const territorySelect = selects[0];
    const doctorSelect = selects[1];
    const chemistSelect = selects[2];

    const territories = Array.from(territorySelect.selectedOptions).map(opt => opt.value);
    const doctors = Array.from(doctorSelect.selectedOptions).map(opt => opt.value);
    const chemists = Array.from(chemistSelect.selectedOptions).map(opt => opt.value);

    if (territories.length === 0 || doctors.length === 0 || chemists.length === 0) {
      allValid = false;
      break;
    }

    const label = div.querySelector('label').innerText;
    stpPlan.push({ dayWeek: label, territories, doctors, chemists });
  }

  if (!allValid) {
      showAlert("All STP days must be fully filled with at least one territory, one doctor and one chemist.", "Validation Error"); // Replaced alert
      return;
  }

  stpSubmitted = true;
  localStorage.setItem('stpSubmitted', 'true'); // Persist STP status
  localStorage.setItem('stpPlan', JSON.stringify(stpPlan)); // Persist STP data
  updateDashboard();
  
  nextSection('mtp'); 
}

function buildMTPCalendar(month, year) {
  const today = new Date();
  
  currentMTPViewedMonthKey = `${year}-${month}`;

  const monthNames = ["January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"];

  document.getElementById('monthDisplay').innerHTML = `<h3>${monthNames[month]} ${year}</h3>`;
  const submitMTPButton = document.getElementById('submitMTPButton');
  const mtpStatusMessage = document.getElementById('mtpStatusMessage');

  console.log("MTP Data (from global) at buildMTPCalendar start:", JSON.parse(JSON.stringify(mtpPlansData)));

  // This check is already done in nextSection('mtp') and should initialize if needed.
  // We re-check here for robustness, though it implies a potential flow issue if not already created.
  if (!mtpPlansData[currentMTPViewedMonthKey]) {
      const lastDay = new Date(year, month + 1, 0);
      let newMonthPlan = [];
      for (let day = 1; day <= lastDay.getDate(); day++) {
        newMonthPlan.push({
          date: new Date(year, month, day),
          territory: '',
          doctors: [],
          chemists: [],
          fromSTP: false
        });
      }
      mtpPlansData[currentMTPViewedMonthKey] = { plan: newMonthPlan, isSubmitted: false };
      applySTPtoMTP(month, year, mtpPlansData[currentMTPViewedMonthKey].plan);
  }

  const currentMonthPlan = mtpPlansData[currentMTPViewedMonthKey].plan;
  const isFrozen = mtpPlansData[currentMTPViewedMonthKey].isSubmitted;

  if (isFrozen) {
    submitMTPButton.disabled = true;
    mtpStatusMessage.textContent = `MTP for ${monthNames[month]} ${year} has already been submitted and is frozen.`;
    mtpStatusMessage.style.color = '#28a745';
  } else {
    submitMTPButton.disabled = false;
    mtpStatusMessage.textContent = "Please plan your monthly tour.";
    mtpStatusMessage.style.color = '#d9534f';
  }

  const firstDay = new Date(year, month, 1);
  const lastDay = new Date(year, month + 1, 0);

  let html = '<table class="calendar"><tr><th>Sun</th><th>Mon</th><th>Tue</th><th>Wed</th><th>Thu</th><th><th>Fri</th><th>Sat</th></tr><tr>';

  // Fill leading empty cells
  for (let i = 0; i < firstDay.getDay(); i++) {
    html += '<td></td>';
  }

  for (let day = 1; day <= lastDay.getDate(); day++) {
    const date = new Date(year, month, day);
    const dayOfWeek = date.getDay(); // 0 for Sunday, 6 for Saturday
    const isToday = date.toDateString() === today.toDateString();
    const dayName = weekdays[dayOfWeek];

    const dayPlan = currentMonthPlan.find(plan => 
        plan.date && 
        plan.date.getDate() === day &&
        plan.date.getMonth() === month &&
        plan.date.getFullYear() === year
    );

    const hasPlan = dayPlan && dayPlan.territory && (dayPlan.doctors.length > 0 || dayPlan.chemists.length > 0);
    const fromSTP = dayPlan && dayPlan.fromSTP;

    const cellClasses = [];
    if (isToday) cellClasses.push('today');
    if (hasPlan) cellClasses.push('has-plan');
    if (fromSTP) cellClasses.push('stp-based');
    if (isFrozen) cellClasses.push('frozen-cell'); // Apply frozen to all days once submitted
    if (dayOfWeek === 0) cellClasses.push('sunday-cell'); // Mark Sundays

    // Corrected template literal for the cell content
    html += `<td class="${cellClasses.join(' ')}"
                 data-date="${year}-${month+1}-${day}"
                 onclick="editDayPlan(this)">
               <div class="day-number">${day}</div>
               <div class="day-content">
                 <div class="day-name">${dayName}</div>`;

    if (hasPlan) {
      html += `<div class="day-details">
                 <strong>Territory:</strong> ${dayPlan.territory}
                 <strong>Doctors:</strong> ${dayPlan.doctors.length > 0 ? dayPlan.doctors.join(', ') : 'None'}
                 <strong>Chemists:</strong> ${dayPlan.chemists.length > 0 ? dayPlan.chemists.join(', ') : 'None'}
                 ${fromSTP ? '<strong style="color:#aa6600;">(STP)</strong>' : ''}
               </div>`;
    } else if (dayOfWeek === 0) { // If it's Sunday and no specific plan is present, show "Sunday"
        html += `<div class="day-details">Sunday</div>`; 
    }

    html += `</div>
             </td>`;

    if (date.getDay() === 6 && day < lastDay.getDate()) { // If it's Saturday and not the last day of the month
      html += '</tr><tr>'; // Start a new row
    }
  }

  // Fill any remaining cells in the last week
  for (let i = lastDay.getDay(); i < 6; i++) {
    html += '<td></td>';
  }

  html += '</tr></table>';
  document.getElementById('mtpCalendar').innerHTML = html;
}

function editDayPlan(cell) {
  const dateStr = cell.getAttribute('data-date');
  if (!dateStr) return;

  const dateParts = dateStr.split('-');
  const year = parseInt(dateParts[0]);
  const month = parseInt(dateParts[1]) - 1;
  const day = parseInt(dateParts[2]);

  selectedDate = new Date(year, month, day);
  const monthKey = `${year}-${month}`;

  if (mtpPlansData[monthKey] && mtpPlansData[monthKey].isSubmitted) {
    showAlert('MTP for this month is already submitted and frozen. You cannot edit individual day plans.', "MTP Frozen"); // Replaced alert
    return;
  }

  if (selectedDate.getDay() === 0) { // Check if it's Sunday
    showAlert("Sundays cannot be planned.", "Planning Restricted"); // Replaced alert
    return;
  }

  const currentMonthPlan = mtpPlansData[monthKey].plan;
  const dayPlan = currentMonthPlan.find(plan =>
    plan.date &&
    plan.date.getDate() === day &&
    plan.date.getMonth() === month &&
    plan.date.getFullYear() === year
  );

  if (dayPlan) {
    document.getElementById('dayPlanDetails').classList.remove('hidden');
    document.getElementById('selectedDayInfo').innerHTML = `
      <p>Planning for: ${weekdays[selectedDate.getDay()]}, ${selectedDate.getDate()} ${
        ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'][selectedDate.getMonth()]
      }, ${selectedDate.getFullYear()}</p>
      ${dayPlan.fromSTP ? '<p style="color:#aa6600;"><strong>Note:</strong> This plan is based on your STP submission.</p>' : ''}
    `;

    const territorySelect = document.getElementById('dayPlanTerritory');
    territorySelect.innerHTML = '<option value="">Select Territory</option>';
    territories.forEach(territory => {
      const option = document.createElement('option');
      option.value = territory;
      option.text = territory;
      if (dayPlan.territory && dayPlan.territory.includes(territory)) {
        option.selected = true;
      }
      territorySelect.appendChild(option);
    });
    territorySelect.onchange = () => {
      updateDoctorsAndChemists(
        territorySelect,
        document.getElementById('dayPlanDoctors'),
        document.getElementById('dayPlanChemists')
      );
    };

    // Call updateDoctorsAndChemists immediately to populate dropdowns based on initial territory selection
    updateDoctorsAndChemists(
      territorySelect,
      document.getElementById('dayPlanDoctors'),
      document.getElementById('dayPlanChemists')
    );

    const doctorSelect = document.getElementById('dayPlanDoctors');
    const chemistSelect = document.getElementById('dayPlanChemists');

    // Pre-select doctors and chemists
    for (let i = 0; i < doctorSelect.options.length; i++) {
      doctorSelect.options[i].selected =
        dayPlan.doctors && dayPlan.doctors.includes(doctorSelect.options[i].value);
    }

    for (let i = 0; i < chemistSelect.options.length; i++) {
      chemistSelect.options[i].selected =
        dayPlan.chemists && dayPlan.chemists.includes(chemistSelect.options[i].value);
    }
  }
}

function saveDayPlan() {
  if (!selectedDate) return;

  const monthKey = `${selectedDate.getFullYear()}-${selectedDate.getMonth()}`;
  if (mtpPlansData[monthKey] && mtpPlansData[monthKey].isSubmitted) {
    showAlert('MTP for this month is already submitted and frozen. Cannot save changes.', "MTP Frozen"); // Replaced alert
    return;
  }

  const territorySelect = document.getElementById('dayPlanTerritory');
  const doctorSelect = document.getElementById('dayPlanDoctors');
  const chemistSelect = document.getElementById('dayPlanChemists');

  const territory = territorySelect.value;
  const doctors = Array.from(doctorSelect.selectedOptions).map(opt => opt.value);
  const chemists = Array.from(chemistSelect.selectedOptions).map(opt => opt.value);

  if (!territory || doctors.length === 0 || chemists.length === 0) {
    showAlert("Please select at least one Territory, one Doctor, and one Chemist for the day plan.", "Validation Error"); // Replaced alert
    return;
  }

  const currentMonthPlan = mtpPlansData[monthKey].plan;
  const planIndex = currentMonthPlan.findIndex(plan =>
    plan.date &&
    plan.date.getDate() === selectedDate.getDate() &&
    plan.date.getMonth() === selectedDate.getMonth() &&
    plan.date.getFullYear() === selectedDate.getFullYear()
  );

  if (planIndex >= 0) {
    currentMonthPlan[planIndex] = {
      ...currentMonthPlan[planIndex],
      territory: territory,
      doctors: doctors,
      chemists: chemists,
      fromSTP: false
    };
  } else {
    currentMonthPlan.push({
      date: new Date(selectedDate),
      territory: territory,
      doctors: doctors,
      chemists: chemists,
      fromSTP: false
    });
  }

  localStorage.setItem('mtpPlansData', JSON.stringify(mtpPlansData)); // Persist MTP plan data

  document.getElementById('dayPlanDetails').classList.add('hidden');
  buildMTPCalendar(selectedDate.getMonth(), selectedDate.getFullYear());
}

function cancelDayPlan() {
  document.getElementById('dayPlanDetails').classList.add('hidden');
}

function submitMTP() {
  const submitMTPButton = document.getElementById('submitMTPButton');
  if (submitMTPButton.disabled) {
      showAlert("MTP for this month has already been submitted and is frozen.", "Submission Restricted"); // Replaced alert
      return;
  }

  const currentMonthPlanData = mtpPlansData[currentMTPViewedMonthKey];
  if (!currentMonthPlanData || !currentMonthPlanData.plan) {
      showAlert("Error: MTP plan data not found for the current month. Please try re-entering MTP section.", "Error"); // Replaced alert
      return;
  }

  let validDaysCount = 0;
  const viewedYear = parseInt(currentMTPViewedMonthKey.split('-')[0], 10);
  const viewedMonth = parseInt(currentMTPViewedMonthKey.split('-')[1], 10);

  const workingDaysInCurrentMonth = currentMonthPlanData.plan.filter(plan => {
    if (!plan.date || isNaN(plan.date.getTime())) {
        console.error("Invalid date object found in mtpPlan for submitMTP:", plan);
        return false;
    }
    const planYear = plan.date.getFullYear();
    const planMonth = plan.date.getMonth();

    const dayOfWeek = plan.date.getDay();

    return planYear === viewedYear && planMonth === viewedMonth && dayOfWeek >= 1 && dayOfWeek <= 6;
  });

  workingDaysInCurrentMonth.forEach(plan => {
    if (plan.territory && plan.doctors.length > 0 && plan.chemists.length > 0) {
      validDaysCount++;
    }
  });

  if (validDaysCount < workingDaysInCurrentMonth.length) {
    showAlert(`All working days must be fully planned before submitting MTP. Currently planned: ${validDaysCount} of ${workingDaysInCurrentMonth.length}.`, "MTP Validation"); // Replaced alert
    return;
  }

  console.log("MTP Data before save:", JSON.parse(JSON.stringify(mtpPlansData))); // Log before saving
  currentMonthPlanData.isSubmitted = true;
  const mtpDataString = JSON.stringify(mtpPlansData);
  localStorage.setItem('mtpPlansData', mtpDataString); // Persist MTP plan data
  console.log("MTP Data stringified for localStorage:", mtpDataString);
  console.log("MTP Data after submission and saving to localStorage:", JSON.parse(JSON.stringify(mtpPlansData))); // Log after saving
  console.log("Is Submitted status in mtpPlansData:", mtpPlansData[currentMTPViewedMonthKey].isSubmitted);


  document.getElementById('popupMessage').textContent = "MTP submitted successfully";
  document.getElementById('successPopup').classList.add('active');

  setTimeout(() => {
    closePopup('successPopup');
    const parts = currentMTPViewedMonthKey.split('-');
    const submittedMTPMonth = parseInt(parts[1], 10);
    const submittedMTPYear = parseInt(parts[0], 10);

    const today = new Date();
    const currentMonth = today.getMonth();
    const currentYear = today.getFullYear();

    // Rebuild calendar for the submitted month to show its frozen state
    buildMTPCalendar(submittedMTPMonth, submittedMTPYear); 

    if (submittedMTPYear === currentYear && submittedMTPMonth === currentMonth) {
        // If MTP for the current month was submitted, proceed to check-in
        setCurrentDate(); 
        nextSection('checkin'); 
    } else {
        // If MTP for an upcoming month was submitted, go to the Home (Dashboard) page
        goHome(); 
    }
  }, 2000);
}

function handleMode() {
  currentTravelMode = document.getElementById('modeSelect').value; // Store the selected mode
  if (currentTravelMode === 'car') {
    nextSection('carMode');
  } else if (currentTravelMode === 'others') {
    nextSection('otherMode');
  }
}

async function submitDCR(tabType) { // Changed to async to await custom confirm
  let selectedId = '';
  let remarks = '';
  let productsAndQuantities = [];
  let jointWork = [];
  let isValid = true;

  const dcrTerritory = document.getElementById('dcrTerritory').value;
  if (!dcrTerritory) {
    showAlert("Please select a Territory for DCR.", "Validation Error"); // Replaced alert
    return;
  }

  const submissionDate = new Date().toISOString().split('T')[0]; // Get current date for DCR entry

  if (tabType === 'doctor') {
    selectedId = document.getElementById('dcrDoctor').value;
    remarks = document.getElementById('dcrDoctorRemarks').value;
    jointWork = Array.from(document.getElementById('jointWork').selectedOptions).map(opt => opt.value);

    // Collect product quantities
    products.forEach(product => {
        const qtyInput = document.getElementById(`qty_${product.replace(/\s/g, '')}`);
        const qty = parseInt(qtyInput.value, 10);
        if (!isNaN(qty) && qty > 0) {
            productsAndQuantities.push({ product: product, quantity: qty });
        }
    });

    if (!selectedId) {
      showAlert("Please select a Doctor.", "Validation Error"); // Replaced alert
      isValid = false;
    }
    // Validation for products: at least one product with quantity > 0
    if (productsAndQuantities.length === 0) {
      showAlert("Please enter a quantity for at least one Product.", "Validation Error"); // Replaced alert
      isValid = false;
    }

  } else if (tabType === 'chemist') {
    selectedId = document.getElementById('dcrChemist').value;
    remarks = document.getElementById('dcrChemistRemarks').value;
    // No products or joint work for chemists in this requirement

    if (!selectedId) {
      showAlert("Please select a Chemist.", "Validation Error"); // Replaced alert
      isValid = false;
    }
  }

  if (!isValid) {
    return;
  }

  // Create DCR entry object
  const dcrEntry = {
      date: submissionDate,
      type: tabType,
      territory: dcrTerritory,
      id: selectedId,
      remarks: remarks
  };

  if (tabType === 'doctor') {
      dcrEntry.productsAndQuantities = productsAndQuantities;
      dcrEntry.jointWork = jointWork;
  }

  // Store DCR entry
  dcrSubmissions.push(dcrEntry);
  localStorage.setItem('dcrSubmissions', JSON.stringify(dcrSubmissions));
  console.log("DCR Submissions after new entry:", JSON.parse(JSON.stringify(dcrSubmissions)));

  document.getElementById('popupMessage').textContent = `DCR submitted successfully for ${tabType}.`;
  document.getElementById('successPopup').classList.add('active');

  setTimeout(async () => { // Use async here
    closePopup('successPopup');
    const addMore = await showConfirm("Do you want to add more DCR entries?", "Add More DCR?"); // Replaced confirm
    if (addMore) {
      // Clear relevant fields based on the tab
      if (tabType === 'doctor') {
        document.getElementById('dcrDoctor').value = '';
        document.getElementById('dcrDoctorRemarks').value = '';
        document.getElementById('jointWork').selectedIndex = -1; // Deselect all joint work
        products.forEach(product => { // Reset product quantities
            document.getElementById(`qty_${product.replace(/\s/g, '')}`).value = '0';
        });
      } else { // chemist
        document.getElementById('dcrChemist').value = '';
        document.getElementById('dcrChemistRemarks').value = '';
      }
      // Re-populate doctors/chemists after territory change simulation if needed
      const currentTerritory = document.getElementById('dcrTerritory').value;
      if (tabType === 'doctor') populateDcrDoctors(currentTerritory);
      else populateDcrChemists(currentTerritory);

    } else {
      nextSection('checkout');
    }
  }, 2000);
}

function finalSubmit() {
  const endKMInput = document.getElementById('endKM');
  const endKMError = document.getElementById('endKMError');
  const checkoutTerritorySelect = document.getElementById('checkoutTerritory');
  const checkoutRemarksInput = document.getElementById('checkoutRemarks');

  // Clear previous errors
  endKMInput.classList.remove('error');
  endKMError.textContent = '';

  let isValid = true;

  const todayString = new Date().toISOString().split('T')[0];

  // Conditional validation for Ending KM based on currentTravelMode
  let startKM = 0;
  let endKM = 0;
  if (currentTravelMode === 'car') {
    startKM = parseInt(document.getElementById('startKM').value, 10);
    endKM = parseInt(endKMInput.value, 10);

    if (isNaN(endKM)) {
      endKMInput.classList.add('error');
      endKMError.textContent = 'Enter the End KM';
      isValid = false;
    } else if (endKM <= startKM) {
      endKMInput.classList.add('error');
      endKMError.textContent = 'Ending KM must be greater than Starting KM.';
      isValid = false;
    }
  }

  if (!checkoutTerritorySelect.value) {
    showAlert("Please select a territory for checkout.", "Validation Error"); // Replaced alert
    isValid = false;
  }

  if (!isValid) {
    return;
  }

  // Store daily summary
  dailySummaries[todayString] = {
      travelMode: currentTravelMode,
      startKM: currentTravelMode === 'car' ? startKM : null,
      endKM: currentTravelMode === 'car' ? endKM : null,
      territory: checkoutTerritorySelect.value,
      remarks: checkoutRemarksInput.value
  };
  localStorage.setItem('dailySummaries', JSON.stringify(dailySummaries));
  console.log("Daily Summaries after new entry:", JSON.parse(JSON.stringify(dailySummaries)));

  // Set the last checkout date for today
  localStorage.setItem('lastCheckoutDate', todayString); 

  document.getElementById('popupMessage').textContent = "Day completed successfully!";
  document.getElementById('successPopup').classList.add('active');

  setTimeout(() => {
    closePopup('successPopup');
    updateDashboard(); // Updates message to "Welcome...Day Completed"
    nextSection('dashboard');
  }, 2000);
}

function closePopup(popupId) {
  document.getElementById(popupId).classList.remove('active');
}

function showDayReport() {
  nextSection('dayReport');
}

function showMonthlyReport() {
  nextSection('monthlyReport');
}

/**
 * Generates and displays the Day Report for the selected date.
 */
function generateDayReport() {
    const selectedDateStr = document.getElementById('dayReportDate').value;
    const reportContentDiv = document.getElementById('dayReportContent');
    reportContentDiv.innerHTML = ''; // Clear previous content

    if (!selectedDateStr) {
        reportContentDiv.innerHTML = '<p>Please select a date to view the day report.</p>';
        return;
    }

    const dailySummary = dailySummaries[selectedDateStr];
    const dcrEntriesForDay = dcrSubmissions.filter(entry => entry.date === selectedDateStr);

    let html = `<h3>Report for ${selectedDateStr}</h3>`;

    if (!dailySummary && dcrEntriesForDay.length === 0) {
        html += '<p>No DCR entries or daily summary found for this date.</p>';
        reportContentDiv.innerHTML = html;
        return;
    }

    // --- Daily Summary ---
    html += `
        <div class="report-summary-box">
            <h4>Daily Summary</h4>
            <p><strong>Date:</strong> ${selectedDateStr}</p>
    `;
    if (dailySummary) {
        html += `
            <p><strong>Travel Mode:</strong> ${dailySummary.travelMode}</p>
        `;
        if (dailySummary.travelMode === 'car') {
            html += `
                <p><strong>Starting KM:</strong> ${dailySummary.startKM || 'N/A'}</p>
                <p><strong>Ending KM:</strong> ${dailySummary.endKM || 'N/A'}</p>
                <p><strong>Total KM:</strong> ${dailySummary.startKM !== null && dailySummary.endKM !== null ? (dailySummary.endKM - dailySummary.startKM) : 'N/A'}</p>
            `;
        }
        html += `
            <p><strong>Checkout Territory:</strong> ${dailySummary.territory || 'N/A'}</p>
            <p><strong>Remarks:</strong> ${dailySummary.remarks || 'None'}</p>
        `;
    } else {
        html += '<p>No daily checkout summary recorded for this date.</p>';
    }
    html += `</div>`;

    // --- Doctor Calls ---
    const doctorCalls = dcrEntriesForDay.filter(entry => entry.type === 'doctor');
    if (doctorCalls.length > 0) {
        html += `
            <h3>Doctor Calls</h3>
            <table>
                <thead>
                    <tr>
                        <th>Doctor</th>
                        <th>Territory</th>
                        <th>Products (Qty)</th>
                        <th>Joint Work</th>
                        <th>Remarks</th>
                    </tr>
                </thead>
                <tbody>
        `;
        doctorCalls.forEach(call => {
            const productsList = call.productsAndQuantities && call.productsAndQuantities.length > 0
                ? call.productsAndQuantities.map(p => `${p.product} (${p.quantity})`).join(', ')
                : 'None';
            const jointWorkList = call.jointWork && call.jointWork.length > 0
                ? call.jointWork.join(', ')
                : 'None';
            html += `
                <tr>
                    <td>${call.id}</td>
                    <td>${call.territory}</td>
                    <td>${productsList}</td>
                    <td>${jointWorkList}</td>
                    <td>${call.remarks || 'None'}</td>
                </tr>
            `;
        });
        html += `
                </tbody>
            </table>
        `;
    } else {
        html += '<p>No doctor calls recorded for this date.</p>';
    }

    // --- Chemist Calls ---
    const chemistCalls = dcrEntriesForDay.filter(entry => entry.type === 'chemist');
    if (chemistCalls.length > 0) {
        html += `
            <h3>Chemist Calls</h3>
            <table>
                <thead>
                    <tr>
                        <th>Chemist</th>
                        <th>Territory</th>
                        <th>Remarks</th>
                    </tr>
                </thead>
                <tbody>
        `;
        chemistCalls.forEach(call => {
            html += `
                <tr>
                    <td>${call.id}</td>
                    <td>${call.territory}</td>
                    <td>${call.remarks || 'None'}</td>
                </tr>
            `;
        });
        html += `
                </tbody>
            </table>
        `;
    } else {
        html += '<p>No chemist calls recorded for this date.</p>';
    }

    reportContentDiv.innerHTML = html;
}

/**
 * Generates and displays the Monthly Report for the selected month and year.
 */
function generateMonthlyReport() {
    const selectedMonth = parseInt(document.getElementById('monthReportMonth').value, 10);
    const selectedYear = parseInt(document.getElementById('monthReportYear').value, 10);
    const reportContentDiv = document.getElementById('monthlyReportContent');
    reportContentDiv.innerHTML = ''; // Clear previous content

    if (isNaN(selectedMonth) || isNaN(selectedYear)) {
        reportContentDiv.innerHTML = '<p>Please select a month and year to view the monthly report.</p>';
        return;
    }

    const monthNames = ["January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"];
    const monthYearString = `${monthNames[selectedMonth]} ${selectedYear}`;

    const dcrEntriesForMonth = dcrSubmissions.filter(entry => {
        const entryDate = new Date(entry.date);
        return entryDate.getMonth() === selectedMonth && entryDate.getFullYear() === selectedYear;
    });

    const dailySummariesForMonth = Object.entries(dailySummaries).filter(([dateStr, summary]) => {
        const summaryDate = new Date(dateStr);
        return summaryDate.getMonth() === selectedMonth && summaryDate.getFullYear() === selectedYear;
    }).map(([dateStr, summary]) => summary);

    let html = `<h3>Monthly Report for ${monthYearString}</h3>`;

    if (dcrEntriesForMonth.length === 0 && dailySummariesForMonth.length === 0) {
        html += '<p>No DCR entries or daily summaries found for this month.</p>';
        reportContentDiv.innerHTML = html;
        return;
    }

    // --- Monthly Summary ---
    let totalDoctorCalls = 0;
    let totalChemistCalls = 0;
    const totalProductsSampled = {}; // { 'Product1': 10, 'Product2': 5 }
    let totalKmTraveled = 0;
    const uniqueTerritories = new Set();
    const uniqueDoctorsVisited = new Set();
    const uniqueChemistsVisited = new Set();

    dcrEntriesForMonth.forEach(entry => {
        uniqueTerritories.add(entry.territory);
        if (entry.type === 'doctor') {
            totalDoctorCalls++;
            uniqueDoctorsVisited.add(entry.id);
            if (entry.productsAndQuantities) {
                entry.productsAndQuantities.forEach(prod => {
                    totalProductsSampled[prod.product] = (totalProductsSampled[prod.product] || 0) + prod.quantity;
                });
            }
        } else if (entry.type === 'chemist') {
            totalChemistCalls++;
            uniqueChemistsVisited.add(entry.id);
        }
    });

    dailySummariesForMonth.forEach(summary => {
        if (summary.travelMode === 'car' && summary.startKM !== null && summary.endKM !== null) {
            totalKmTraveled += (summary.endKM - summary.startKM);
        }
    });

    html += `
        <div class="report-summary-box">
            <h4>Summary for ${monthYearString}</h4>
            <p><strong>Total Doctor Calls:</strong> ${totalDoctorCalls}</p>
            <p><strong>Total Chemist Calls:</strong> ${totalChemistCalls}</p>
            <p><strong>Total KM Traveled (Car Mode):</strong> ${totalKmTraveled} KM</p>
            <p><strong>Unique Territories Visited:</strong> ${Array.from(uniqueTerritories).join(', ') || 'None'}</p>
            <p><strong>Unique Doctors Visited:</strong> ${Array.from(uniqueDoctorsVisited).join(', ') || 'None'}</p>
            <p><strong>Unique Chemists Visited:</strong> ${Array.from(uniqueChemistsVisited).join(', ') || 'None'}</p>
            <h4>Products Sampled:</h4>
            <ul>
    `;
    const sortedProducts = Object.keys(totalProductsSampled).sort();
    if (sortedProducts.length > 0) {
        sortedProducts.forEach(product => {
            html += `<li><strong>${product}:</strong> ${totalProductsSampled[product]}</li>`;
        });
    } else {
        html += '<li>No products sampled.</li>';
    }
    html += `
            </ul>
        </div>
    `;

    // Optionally, you could add detailed tables for each day's DCR within the month here,
    // but for a summary report, the above is usually sufficient.

    reportContentDiv.innerHTML = html;
}

/**
 * Initiates the MTP View section.
 */
function showMTPView() {
    nextSection('mtpView');
}

/**
 * Generates and displays the MTP View for the selected month and year.
 */
function generateMTPView() {
    const selectedMonth = parseInt(document.getElementById('mtpViewMonth').value, 10);
    const selectedYear = parseInt(document.getElementById('mtpViewYear').value, 10);
    const mtpViewContentDiv = document.getElementById('mtpViewCalendarContent');
    mtpViewContentDiv.innerHTML = ''; // Clear previous content

    if (isNaN(selectedMonth) || isNaN(selectedYear)) {
        mtpViewContentDiv.innerHTML = '<p>Please select a month and year to view the MTP.</p>';
        return;
    }

    const monthNames = ["January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"];
    const monthKey = `${selectedYear}-${selectedMonth}`;

    const monthPlanData = mtpPlansData[monthKey];

    if (!monthPlanData || !monthPlanData.plan || !monthPlanData.isSubmitted) {
        mtpViewContentDiv.innerHTML = `
            <h3>MTP for ${monthNames[selectedMonth]} ${selectedYear}</h3>
            <p>No submitted MTP found for this month, or it has not been submitted yet.</p>
        `;
        return;
    }

    const currentMonthPlan = monthPlanData.plan;
    const firstDay = new Date(selectedYear, selectedMonth, 1);
    const lastDay = new Date(selectedYear, selectedMonth + 1, 0);

    let html = `<h3>Submitted MTP for ${monthNames[selectedMonth]} ${selectedYear}</h3>`;
    html += '<table class="calendar"><tr><th>Sun</th><th>Mon</th><th>Tue</th><th>Wed</th><th>Thu</th><th><th>Fri</th><th>Sat</th></tr><tr>';

    // Fill leading empty cells
    for (let i = 0; i < firstDay.getDay(); i++) {
        html += '<td></td>';
    }

    for (let day = 1; day <= lastDay.getDate(); day++) {
        const date = new Date(selectedYear, selectedMonth, day);
        const dayOfWeek = date.getDay(); // 0 for Sunday, 6 for Saturday
        const dayName = weekdays[dayOfWeek];

        const dayPlan = currentMonthPlan.find(plan => 
            plan.date && 
            plan.date.getDate() === day &&
            plan.date.getMonth() === selectedMonth &&
            plan.date.getFullYear() === selectedYear
        );

        const hasPlan = dayPlan && dayPlan.territory && (dayPlan.doctors.length > 0 || dayPlan.chemists.length > 0);
        const fromSTP = dayPlan && dayPlan.fromSTP;

        // All cells in MTP View are "frozen" as it's a submitted plan
        const cellClasses = ['frozen-cell'];
        if (hasPlan) cellClasses.push('has-plan');
        if (fromSTP) cellClasses.push('stp-based');
        if (dayOfWeek === 0) cellClasses.push('sunday-cell'); // Mark Sundays

        html += `<td class="${cellClasses.join(' ')}" data-date="${selectedYear}-${selectedMonth+1}-${day}">
                   <div class="day-number">${day}</div>
                   <div class="day-content">
                     <div class="day-name">${dayName}</div>`;

        if (hasPlan) {
            html += `<div class="day-details">
                       <strong>Territory:</strong> ${dayPlan.territory}
                       <strong>Doctors:</strong> ${dayPlan.doctors.length > 0 ? dayPlan.doctors.join(', ') : 'None'}
                       <strong>Chemists:</strong> ${dayPlan.chemists.length > 0 ? dayPlan.chemists.join(', ') : 'None'}
                       ${fromSTP ? '<strong style="color:#aa6600;">(STP)</strong>' : ''}
                     </div>`;
        } else if (dayOfWeek === 0) { // If it's Sunday and no specific plan is present, show "Sunday"
            html += `<div class="day-details">Sunday</div>`; 
        } else {
            html += `<div class="day-details">No Plan</div>`;
        }

        html += `</div>
                 </td>`;

        if (date.getDay() === 6 && day < lastDay.getDate()) {
            html += '</tr><tr>';
        }
    }

    // Fill any remaining cells in the last week
    for (let i = lastDay.getDay(); i < 6; i++) {
        html += '<td></td>';
    }

    html += '</tr></table>';
    mtpViewContentDiv.innerHTML = html;
}

/**
 * Initiates the STP View section.
 */
function showSTPView() {
    nextSection('stpView');
}

/**
 * Generates and displays the STP View.
 */
function generateSTPView() {
    const stpViewContentDiv = document.getElementById('stpViewContent');
    stpViewContentDiv.innerHTML = ''; // Clear previous content

    // Ensure stpPlan is loaded from localStorage if not already in memory
    const storedStpPlan = localStorage.getItem('stpPlan');
    if (storedStpPlan) {
        stpPlan = JSON.parse(storedStpPlan);
    }

    if (!stpPlan || stpPlan.length === 0) {
        stpViewContentDiv.innerHTML = '<p>No STP data submitted yet.</p>';
        return;
    }

    let html = `<h3>Submitted STP</h3>`;
    html += `
        <table>
            <thead>
                <tr>
                    <th>Day/Week</th>
                    <th>Territories</th>
                    <th>Doctors</th>
                    <th>Chemists</th>
                </tr>
            </thead>
            <tbody>
    `;

    stpPlan.forEach(entry => {
        html += `
            <tr>
                <td>${entry.dayWeek}</td>
                <td>${entry.territories.join(', ')}</td>
                <td>
                    <ul>
                        ${entry.doctors.map(doc => `<li>${doc}</li>`).join('')}
                    </ul>
                </td>
                <td>
                    <ul>
                        ${entry.chemists.map(chem => `<li>${chem}</li>`).join('')}
                    </ul>
                </td>
            </tr>
        `;
    });

    html += `
            </tbody>
        </table>
    `;
    stpViewContentDiv.innerHTML = html;
}


// Initialize the STP form
function initSTPForm() {
  const form = document.getElementById('stpForm');
  form.innerHTML = '';

  days.forEach(day => {
    weeks.forEach(week => {
      const formGroup = document.createElement('div');
      formGroup.style = 'display: grid; grid-template-columns: 1fr 1fr 1fr 1fr; gap: 10px; margin-bottom: 15px;';

      const label = document.createElement('label');
      label.textContent = `${day} ${week}`;
      label.style = 'margin-top: 10px;';
      formGroup.appendChild(label);

      const territorySelect = document.createElement('select');
      territorySelect.setAttribute('multiple', 'multiple');
      territories.forEach(t => {
        const option = document.createElement('option');
        option.value = t;
        option.text = t;
        territorySelect.appendChild(option);
      });
      formGroup.appendChild(territorySelect);

      const doctorSelect = document.createElement('select');
      doctorSelect.setAttribute('multiple', 'multiple');
      formGroup.appendChild(doctorSelect);

      const chemistSelect = document.createElement('select');
      chemistSelect.setAttribute('multiple', 'multiple');
      formGroup.appendChild(chemistSelect);

      territorySelect.addEventListener('change', () => {
        updateDoctorsAndChemists(territorySelect, doctorSelect, chemistSelect);
      });

      form.appendChild(formGroup);
    });
  });
}

// Function to populate the checkout territory dropdown
function populateCheckoutTerritory() {
    const checkoutTerritorySelect = document.getElementById('checkoutTerritory');
    checkoutTerritorySelect.innerHTML = '<option value="">Select Territory</option>';
    territories.forEach(t => {
        const option = document.createElement('option');
        option.value = t;
        option.text = t;
        checkoutTerritorySelect.appendChild(option);
    });
    // Set a default value if desired, e.g., the first territory
    if (territories.length > 0) {
        checkoutTerritorySelect.value = territories[0];
    }
}

// Initialize the application
window.onload = function() {
  console.log("window.onload: Starting initialization.");
  try {
      const storedMtpPlans = localStorage.getItem('mtpPlansData');
      console.log("MTP Data loaded from localStorage (raw):", storedMtpPlans);
      mtpPlansData = storedMtpPlans ? JSON.parse(storedMtpPlans) : {};

      for (const monthKey in mtpPlansData) {
          if (mtpPlansData.hasOwnProperty(monthKey) && mtpPlansData[monthKey].plan) {
              mtpPlansData[monthKey].plan.forEach(dayPlan => {
                  if (typeof dayPlan.date === 'string') {
                      const tempDate = new Date(dayPlan.date);
                      if (isNaN(tempDate.getTime())) {
                          console.error("Failed to re-hydrate invalid date string on onload:", dayPlan.date, "for month:", monthKey);
                          dayPlan.date = null; 
                      } else {
                          dayPlan.date = tempDate;
                      }
                  } else if (dayPlan.date !== null && typeof dayPlan.date !== 'object' && !(dayPlan.date instanceof Date)) {
                      console.warn("Unexpected type for dayPlan.date during re-hydration on onload:", typeof dayPlan.date, "Value:", dayPlan.date, "for month:", monthKey);
                      dayPlan.date = null;
                  }
              });
          }
      }
      console.log("MTP Data after re-hydration:", JSON.parse(JSON.stringify(mtpPlansData))); // Deep copy for console log
  } catch (e) {
      console.error("Error parsing stored MTP plans from localStorage on onload:", e);
      mtpPlansData = {}; 
  }
  console.log("MTP status after onload:", mtpPlansData);

  // --- Load DCR Submissions and Daily Summaries ---
  try {
      const storedDcrSubmissions = localStorage.getItem('dcrSubmissions');
      dcrSubmissions = storedDcrSubmissions ? JSON.parse(storedDcrSubmissions) : [];
      console.log("DCR Submissions loaded from localStorage:", JSON.parse(JSON.stringify(dcrSubmissions)));
  } catch (e) {
      console.error("Error parsing stored DCR submissions from localStorage on onload:", e);
      dcrSubmissions = [];
  }

  try {
      const storedDailySummaries = localStorage.getItem('dailySummaries');
      dailySummaries = storedDailySummaries ? JSON.parse(storedDailySummaries) : {};
      console.log("Daily Summaries loaded from localStorage:", JSON.parse(JSON.stringify(dailySummaries)));
  } catch (e) {
      console.error("Error parsing stored daily summaries from localStorage on onload:", e);
      dailySummaries = {};
  }
  // --- End Load DCR Submissions and Daily Summaries ---

  // Load persistence variables from localStorage on page load
  stpSubmitted = localStorage.getItem('stpSubmitted') === 'true'; 
  lastCheckoutDate = localStorage.getItem('lastCheckoutDate');
  mtpEntryGlobalClickCounter = parseInt(localStorage.getItem('mtpEntryGlobalClickCounter') || '0', 10);

  // Load STP Plan from localStorage
  try {
      const storedStpPlan = localStorage.getItem('stpPlan');
      stpPlan = storedStpPlan ? JSON.parse(storedStpPlan) : [];
      console.log("STP Plan loaded from localStorage:", JSON.parse(JSON.stringify(stpPlan)));
  } catch (e) {
      console.error("Error parsing stored STP plan from localStorage on onload:", e);
      stpPlan = [];
  }


  initSTPForm();
  updateDashboard(); // Initial dashboard update based on persisted state
  console.log("window.onload: Initialization complete.");
};
</script>
</body>
</html>
