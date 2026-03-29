<html lang="ka">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>სამედიცინო დანიშნულება</title>
  <script src="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.min.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.snow.css" rel="stylesheet">
  <link rel="icon" type="image/png" href="danishnuleba.png">
  <link rel="shortcut icon" type="image/png" href="danishnuleba.png">
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    :root {
      --primary: #2563eb;
      --primary-dark: #1d4ed8;
      --success: #10b981;
      --danger: #ef4444;
      --gray: #6b7280;
      --light: #f8fafc;
      --border: #e2e8f0;
    }
    body {
      font-family: 'Roboto', 'BPG Nino Mtavruli', 'Sylfaen', sans-serif;
      background: linear-gradient(to bottom, #f1f5f9, #e0e7ff);
      min-height: 100vh;
    }
    .card {
      background: white;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.08);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .card:hover {
      transform: translateY(-2px);
      box-shadow: 0 15px 35px rgba(0,0,0,0.12);
    }
    .btn {
      font-weight: 500;
      border-radius: 8px;
      padding: 0.5rem 1rem;
      transition: all 0.2s;
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
    }
    .btn-primary { background: var(--primary); color: white; }
    .btn-primary:hover { background: var(--primary-dark); }
    .btn-success { background: var(--success); color: white; }
    .btn-success:hover { background: #059669; }
    .btn-secondary { background: #64748b; color: white; }
    .btn-secondary:hover { background: #475569; }
    .input-group {
      position: relative;
    }
    .input-group label {
      position: absolute;
      top: -8px;
      left: 12px;
      background: white;
      padding: 0 4px;
      font-size: 0.75rem;
      color: var(--primary);
      font-weight: 500;
    }
    .input-field {
      border: 2px solid var(--border);
      border-radius: 8px;
      padding: 0.75rem 1rem;
      transition: border 0.2s;
    }
    .input-field:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(37,99,235,0.1);
    }
    .input-field.lookup-loading {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(37,99,235,0.08);
    }
    .status-hint {
      min-height: 1.25rem;
      margin-top: 0.5rem;
      font-size: 0.875rem;
      color: var(--gray);
    }
    .status-hint[data-state="loading"] { color: var(--primary); }
    .status-hint[data-state="success"] { color: #059669; }
    .status-hint[data-state="error"] { color: var(--danger); }
    .ql-toolbar {
      border-top-left-radius: 8px;
      border-top-right-radius: 8px;
      border: 2px solid var(--border);
      border-bottom: none;
    }
    .ql-container {
      border-bottom-left-radius: 8px;
      border-bottom-right-radius: 8px;
      border: 2px solid var(--border);
      border-top: none;
    }
    .ql-editor {
      min-height: 220px;
      font-family: inherit;
      line-height: 1.2 !important;
      padding: 14px 16px;
      font-size: 15px;
    }
    .modal {
      backdrop-filter: blur(8px);
      background: rgba(0,0,0,0.4);
    }
    .toast {
      position: fixed;
      top: 1rem;
      right: 1rem;
      z-index: 1000;
      animation: slide1 0.3s ease-out;
    }
    @keyframes slide1 {
      from { transform: translateX(100%); opacity: 0; }
      to { transform: translateX(0); opacity: 1; }
    }
    .template-card {
      background: #f8fafc;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1rem;
      transition: all 0.2s;
    }
    .template-card:hover {
      background: #eff6ff;
      border-color: var(--primary);
      transform: translateY(-2px);
    }
    .logo-container {
      width: 9rem;
      height: 6rem;
      margin: 0 auto 1rem;
      overflow: hidden;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .logo-container img {
      max-width: 88%;
      max-height: 88%;
      object-fit: contain;
    }
  </style>
</head>
<body class="min-h-screen">
  <div class="max-w-5xl mx-auto p-4 md:p-8">
    <div class="card p-4 md:p-6 text-center mb-6">
      <div class="logo-container">
        <img src="tm_center_logo.png" alt="TM Center">
      </div>
      <h1 class="text-lg md:text-xl font-bold text-gray-800 leading-tight">
        თბილისის სახელმწიფო სამედიცინო უნივერსიტეტისა და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა
      </h1>
      <h2 class="text-lg md:text-xl font-bold text-blue-600 mt-2">სამედიცინო დანიშნულება</h2>
    </div>

    <div class="card p-6 md:p-8 mb-6">
      <form id="pres魚-form">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
          <div class="input-group">
            <label>პაციენტი</label>
            <input type="text" id="patient-name" class="input-field w-full" placeholder="ნინო გელაშვილი">
          </div>
          <div class="input-group">
            <label>ისტორიის №</label>
            <input type="text" id="history-number" class="input-field w-full" placeholder="2024-001234">
            <p id="history-lookup-status" class="status-hint" aria-live="polite"></p>
          </div>
          <div class="input-group">
            <label>თარიღი</label>
            <input type="date" id="date" class="input-field w-full">
          </div>
          <div class="input-group">
            <label>ექიმი</label>
            <input type="text" id="doctor-name" class="input-field w-full" placeholder="ნინო კიკვაძე">
          </div>
        </div>

        <div class="flex flex-wrap gap-3 mb-6">
          <button type="button" id="open-templates-btn" class="btn btn-primary">შაბლონები</button>
          <button type="button" id="save-template-btn" class="btn btn-success">შაბლონის შენახვა</button>
        </div>

        <div class="mb-6">
          <label class="block text-sm font-semibold text-gray-700 mb-2">დანიშნულება</label>
          <div id="editor" style="height: 220px;"></div>
        </div>

        <div class="mb-5 flex items-center">
          <input type="checkbox" id="require-patient-signature" class="mr-2">
          <label for="require-patient-signature" class="text-sm font-medium text-gray-700">პაციენტის ხელმოწერა</label>
        </div>

        <div class="flex flex-wrap gap-3 justify-end">
          <button type="button" id="clear-btn" class="btn btn-secondary">გასუფთავება</button>
          <button type="button" id="print-btn" class="btn btn-primary text-lg font-semibold">ბეჭდვა</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Templates Modal -->
  <div id="templates-modal" class="fixed inset-0 modal hidden items-center justify-center z-50">
    <div class="bg-white rounded-2xl shadow-2xl w-full max-w-3xl mx-4 max-h-[85vh] overflow-hidden flex flex-col">
      <div class="p-5 border-b border-gray-200 flex justify-between items-center bg-gradient-to-r from-blue-50 to-indigo-50">
        <h3 class="text-xl font-bold text-gray-800">შაბლონები</h3>
        <button id="close-templates-modal" class="text-gray-500 hover:text-gray-700 p-2 rounded-lg hover:bg-white transition">
          <i class="fas fa-times text-xl"></i>
        </button>
      </div>
      <div id="templates-container" class="flex-1 overflow-y-auto p-5">
        <p id="no-templates" class="text-center text-gray-500 py-12 text-lg">შაბლონები არ არის შენახული</p>
        <div id="templates-grid" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>
      </div>
      <div class="p-4 border-t border-gray-200 bg-gray-50 text-right">
        <button id="close-templates-btn" class="btn btn-secondary">დახურვა</button>
      </div>
    </div>
  </div>

  <!-- Save Template Modal -->
  <div id="save-template-modal" class="fixed inset-0 modal hidden items-center justify-center z-50">
    <div class="bg-white rounded-2xl shadow-2xl p-6 w-full max-w-md mx-4">
      <h3 class="text-xl font-bold text-gray-800 mb-4">შაბლონის შენახვა</h3>
      <div class="input-group mb-5">
        <label>შაბლონის სახელი</label>
        <input type="text" id="template-name-input" class="input-field w-full" placeholder="მაგ: ანტიბიოტიკები">
      </div>
      <div class="flex justify-end gap-3">
        <button id="cancel-save-template" class="btn btn-secondary">გაუქმება</button>
        <button id="confirm-save-template" class="btn btn-success">შენახვა</button>
      </div>
    </div>
  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
    import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc, query, orderBy } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCqNceaV85lJXAHcv7fEUtqYFDWl-g-GAc",
      authDomain: "danishnuleba1.firebaseapp.com",
      projectId: "danishnuleba1",
      storageBucket: "danishnuleba1.firebasestorage.app",
      messagingSenderId: "439396384140",
      appId: "1:439396384140:web:a2c6327fb5e3f3035daaa9"
    };
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    let quill;
    let templates = [];
    let historyLookupTimer = null;
    let historyLookupRequestSeq = 0;
    let lastAutoFilledPatientName = '';
    const REGISTRATION_XLSX_IMPORT_URL = 'https://cdn.jsdelivr.net/npm/xlsx@0.18.5/+esm';
    const REGISTRATION_SETTINGS = {
      googleSheetsId: 'https://docs.google.com/spreadsheets/d/1zsuLPC1hDVJ1pzGMsk_LY1bILCF6Dbd7/edit?gid=226530235#gid=226530235',
      sheetName: '',
      columnMapping: {
        firstName: 'C',
        lastName: 'B',
        historyNumber: 'F'
      }
    };
    const registrationWorkbookSheetsPromiseByKey = new Map();

    function formatGeorgianDate(dateString) {
      if (!dateString) return '-';
      const date = new Date(dateString);
      const day = String(date.getDate()).padStart(2, '0');
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const year = date.getFullYear();
      return `${day}/${month}/${year}`;
    }

    function normalizeHistoryNumber(value) {
      return String(value || '').trim().replace(/\.0+$/, '');
    }

    function normalizeSheetCellValue(value) {
      if (value === null || value === undefined) return '';
      if (typeof value === 'number') {
        return Number.isInteger(value) ? String(value) : String(value).replace(/\.0+$/, '');
      }
      return String(value).trim().replace(/\.0+$/, '');
    }

    function extractSpreadsheetId(value) {
      const trimmedValue = String(value || '').trim();
      const match = trimmedValue.match(/\/spreadsheets\/d\/([a-zA-Z0-9-_]+)/);
      return match ? match[1] : trimmedValue;
    }

    function columnLetterToIndex(columnName) {
      const normalizedColumnName = String(columnName || '').trim().toUpperCase();
      if (!/^[A-Z]+$/.test(normalizedColumnName)) return -1;

      let index = 0;
      for (const character of normalizedColumnName) {
        index = index * 26 + (character.charCodeAt(0) - 64);
      }
      return index - 1;
    }

    function prioritizeSheetNames(sheetNames, preferredSheetName) {
      const normalizedPreferredSheetName = String(preferredSheetName || '').trim();
      if (!normalizedPreferredSheetName || !sheetNames.includes(normalizedPreferredSheetName)) {
        return sheetNames;
      }
      return [
        normalizedPreferredSheetName,
        ...sheetNames.filter(sheetName => sheetName !== normalizedPreferredSheetName)
      ];
    }

    function setHistoryLookupStatus(message = '', state = '') {
      const statusEl = document.getElementById('history-lookup-status');
      const historyInput = document.getElementById('history-number');
      if (!statusEl || !historyInput) return;
      statusEl.textContent = message;
      statusEl.dataset.state = state || '';
      historyInput.classList.toggle('lookup-loading', state === 'loading');
    }

    async function fetchRegistrationWorkbookSheets(settings) {
      const spreadsheetId = extractSpreadsheetId(settings.googleSheetsId);
      if (!spreadsheetId) return [];

      const preferredSheetName = String(settings.sheetName || '').trim();
      const cacheKey = `${spreadsheetId}::${preferredSheetName || '*'}`;
      let workbookSheetsPromise = registrationWorkbookSheetsPromiseByKey.get(cacheKey);

      if (!workbookSheetsPromise) {
        workbookSheetsPromise = (async () => {
          const workbookUrl = `https://docs.google.com/spreadsheets/d/${spreadsheetId}/export?format=xlsx`;
          const response = await fetch(workbookUrl, { cache: 'no-store' });
          if (!response.ok) {
            throw new Error(`Workbook fetch failed with status ${response.status}`);
          }

          const buffer = await response.arrayBuffer();
          const XLSX = await import(REGISTRATION_XLSX_IMPORT_URL);
          const workbook = XLSX.read(buffer, { type: 'array' });
          const orderedSheetNames = prioritizeSheetNames(workbook.SheetNames, preferredSheetName);

          return orderedSheetNames.map(sheetName => ({
            sheetName,
            rows: XLSX.utils.sheet_to_json(workbook.Sheets[sheetName], {
              header: 1,
              defval: '',
              raw: false
            })
          }));
        })().catch(error => {
          registrationWorkbookSheetsPromiseByKey.delete(cacheKey);
          throw error;
        });

        registrationWorkbookSheetsPromiseByKey.set(cacheKey, workbookSheetsPromise);
      }

      return workbookSheetsPromise;
    }

    function mapRegistryPatientFromRows(rows, settings, historyNumber) {
      if (!Array.isArray(rows) || !rows.length) return null;

      const firstNameIndex = columnLetterToIndex(settings.columnMapping.firstName || 'C');
      const lastNameIndex = columnLetterToIndex(settings.columnMapping.lastName || 'B');
      const historyNumberIndex = columnLetterToIndex(settings.columnMapping.historyNumber || 'F');
      const normalizedTargetHistoryNumber = normalizeHistoryNumber(historyNumber);
      if (!normalizedTargetHistoryNumber) return null;

      const row = rows.find(currentRow => {
        const rowHistoryNumber = normalizeSheetCellValue(currentRow?.[historyNumberIndex]);
        return rowHistoryNumber === normalizedTargetHistoryNumber;
      });
      if (!row) return null;

      return {
        firstName: normalizeSheetCellValue(row[firstNameIndex]),
        lastName: normalizeSheetCellValue(row[lastNameIndex]),
        historyNumber: normalizeSheetCellValue(row[historyNumberIndex])
      };
    }

    async function lookupRegistryPatientByHistory(historyNumber) {
      const normalizedHistoryNumber = normalizeHistoryNumber(historyNumber);
      if (!normalizedHistoryNumber) return null;

      const workbookSheets = await fetchRegistrationWorkbookSheets(REGISTRATION_SETTINGS);
      for (const sheet of workbookSheets) {
        const patient = mapRegistryPatientFromRows(sheet.rows, REGISTRATION_SETTINGS, normalizedHistoryNumber);
        if (patient) return patient;
      }
      return null;
    }

    function buildRegistryPatientName(patient) {
      return [patient?.firstName, patient?.lastName]
        .map(value => String(value || '').trim())
        .filter(Boolean)
        .join(' ');
    }

    function clearAutoFilledPatientName() {
      const patientNameInput = document.getElementById('patient-name');
      if (!patientNameInput) return;
      if (lastAutoFilledPatientName && patientNameInput.value.trim() === lastAutoFilledPatientName) {
        patientNameInput.value = '';
      }
      lastAutoFilledPatientName = '';
    }

    function applyRegistryPatientIdentity(patient) {
      const patientNameInput = document.getElementById('patient-name');
      if (!patientNameInput) return;

      const fullName = buildRegistryPatientName(patient);
      if (!fullName) return;

      patientNameInput.value = fullName;
      lastAutoFilledPatientName = fullName;
    }

    async function hydratePatientIdentityByHistory(historyNumber) {
      const normalizedHistoryNumber = normalizeHistoryNumber(historyNumber);
      const lookupSeq = ++historyLookupRequestSeq;

      if (!normalizedHistoryNumber) {
        clearAutoFilledPatientName();
        setHistoryLookupStatus('', '');
        return false;
      }

      setHistoryLookupStatus('პაციენტს ვეძებ ცხრილში...', 'loading');

      try {
        const patient = await lookupRegistryPatientByHistory(normalizedHistoryNumber);
        if (lookupSeq !== historyLookupRequestSeq) return false;

        if (!patient) {
          clearAutoFilledPatientName();
          setHistoryLookupStatus('ასეთი ისტორიის ნომერი ვერ მოიძებნა.', 'error');
          return false;
        }

        applyRegistryPatientIdentity(patient);
        setHistoryLookupStatus(`ნაპოვნია: ${buildRegistryPatientName(patient)}`, 'success');
        return true;
      } catch (error) {
        console.warn('Google Sheets lookup failed:', error);
        setHistoryLookupStatus('Google Sheets-იდან მონაცემის წამოღება ვერ მოხერხდა.', 'error');
        return false;
      }
    }

    function scheduleHistoryLookup(immediate = false) {
      if (historyLookupTimer) clearTimeout(historyLookupTimer);
      historyLookupTimer = setTimeout(() => {
        hydratePatientIdentityByHistory(document.getElementById('history-number')?.value || '');
      }, immediate ? 0 : 320);
    }

    document.addEventListener('DOMContentLoaded', async () => {
      document.getElementById('date').value = new Date().toISOString().split('T')[0];
      quill = new Quill('#editor', {
        theme: 'snow',
        modules: { toolbar: [['bold', 'italic'], ['link'], [{ 'list': 'ordered'}, { 'list': 'bullet' }], ['clean']] },
        placeholder: 'დაიწყეთ დანიშნულების აკრეფა...'
      });
      setupEventListeners();
      await loadTemplates();
      scheduleHistoryLookup(true);
    });

    function setupEventListeners() {
      const historyNumberInput = document.getElementById('history-number');
      document.getElementById('print-btn').addEventListener('click', handlePrint);
      document.getElementById('clear-btn').addEventListener('click', handleClear);
      document.getElementById('save-template-btn').addEventListener('click', showSaveTemplateModal);
      document.getElementById('open-templates-btn').addEventListener('click', openTemplatesModal);
      document.getElementById('cancel-save-template').addEventListener('click', hideSaveTemplateModal);
      document.getElementById('confirm-save-template').addEventListener('click', saveTemplate);
      document.getElementById('close-templates-modal').addEventListener('click', closeTemplatesModal);
      document.getElementById('close-templates-btn').addEventListener('click', closeTemplatesModal);
      document.getElementById('templates-modal').addEventListener('click', e => e.target.id === 'templates-modal' && closeTemplatesModal());
      document.getElementById('save-template-modal').addEventListener('click', e => e.target.id === 'save-template-modal' && hideSaveTemplateModal());
      historyNumberInput.addEventListener('input', () => scheduleHistoryLookup(false));
      historyNumberInput.addEventListener('blur', () => scheduleHistoryLookup(true));
    }

    async function loadTemplates() {
      try {
        const q = query(collection(db, "medical_templates"), orderBy("created_at", "desc"));
        const snapshot = await getDocs(q);
        templates = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
        renderTemplatesInModal();
      } catch (error) {
        showToast('შაბლონების ჩატვირთვა ვერ მოხერხდა', 'error');
      }
    }

    async function saveTemplate() {
      const name = document.getElementById('template-name-input').value.trim();
      const content = quill.root.innerHTML.trim();
      if (!name || !content || content === '<p><br></p>') {
        showToast('შეავსეთ სახელი და დანიშნულება', 'error');
        return;
      }
      try {
        await addDoc(collection(db, "medical_templates"), { name, content, created_at: new Date().toISOString() });
        hideSaveTemplateModal();
        await loadTemplates();
        showToast('შაბლონი შეინახა!', 'success');
      } catch (error) {
        showToast('შენახვა ვერ მოხერხდა', 'error');
      }
    }

    async function deleteTemplate(id) {
      if (!confirm('წაშლა?')) return;
      try {
        await deleteDoc(doc(db, "medical_templates", id));
        await loadTemplates();
        showToast('შაბლონი წაიშალა', 'success');
      } catch (error) {
        showToast('წაშლა ვერ მოხერხდა', 'error');
      }
    }

    function openTemplatesModal() {
      renderTemplatesInModal();
      document.getElementById('templates-modal').classList.remove('hidden');
      document.getElementById('templates-modal').classList.add('flex');
    }

    function closeTemplatesModal() {
      document.getElementById('templates-modal').classList.add('hidden');
      document.getElementById('templates-modal').classList.remove('flex');
    }

    function showSaveTemplateModal() {
      const content = quill.root.innerHTML.trim();
      if (!content || content === '<p><br></p>') return showToast('დანიშნულება ცარიელია', 'error');
      document.getElementById('save-template-modal').classList.remove('hidden');
      document.getElementById('save-template-modal').classList.add('flex');
      document.getElementById('template-name-input').focus();
    }

    function hideSaveTemplateModal() {
      document.getElementById('save-template-modal').classList.add('hidden');
      document.getElementById('save-template-modal').classList.remove('flex');
      document.getElementById('template-name-input').value = '';
    }

    function renderTemplatesInModal() {
      const grid = document.getElementById('templates-grid');
      const noTemplates = document.getElementById('no-templates');
      grid.innerHTML = '';
      if (templates.length === 0) {
        noTemplates.classList.remove('hidden');
        return;
      }
      noTemplates.classList.add('hidden');
      templates.forEach(t => {
        const card = document.createElement('div');
        card.className = 'template-card p-4';
        card.innerHTML = `
          <div class="flex justify-between items-start">
            <div class="flex-1">
              <h4 class="font-semibold text-gray-800">${escapeHtml(t.name)}</h4>
              <p class="text-xs text-gray-500 mt-1">${formatGeorgianDate(t.created_at)}</p>
            </div>
            <div class="flex gap-2">
              <button class="text-blue-600 hover:text-blue-800 font-medium text-sm">ჩატვირთვა</button>
              <button class="text-red-600 hover:text-red-800 font-medium text-sm">წაშლა</button>
            </div>
          </div>
        `;
        card.querySelector('.text-blue-600').onclick = () => {
          quill.root.innerHTML = t.content;
          closeTemplatesModal();
          showToast('შაბლონი ჩაიტვირთა', 'success');
        };
        card.querySelector('.text-red-600').onclick = () => deleteTemplate(t.id);
        grid.appendChild(card);
      });
    }

    function handleClear() {
      if (historyLookupTimer) clearTimeout(historyLookupTimer);
      historyLookupRequestSeq += 1;
      lastAutoFilledPatientName = '';
      ['patient-name', 'history-number', 'doctor-name'].forEach(id => document.getElementById(id).value = '');
      document.getElementById('date').value = new Date().toISOString().split('T')[0];
      quill.setContents([]);
      document.getElementById('require-patient-signature').checked = false;
      setHistoryLookupStatus('', '');
    }

    function handlePrint() {
      const data = {
        patient: document.getElementById('patient-name').value || '-',
        history: document.getElementById('history-number').value || '-',
        date: document.getElementById('date').value ? formatGeorgianDate(document.getElementById('date').value) : '-',
        doctor: document.getElementById('doctor-name').value || '-',
        content: quill.root.innerHTML || '<p>-</p>'
      };
      const requirePatientSig = document.getElementById('require-patient-signature').checked;

      const patientSigHtml = requirePatientSig ? `
        <div style="margin-top: 1.2rem; text-align: right; font-size: 12pt;">
          <p style="margin:0;">გავეცანი, ჩავიბარე,</p>
          <p style="margin-top: 0.4rem;">
            პაციენტის ხელმოწერა: _________________
          </p>
        </div>` : '';

      const printWin = window.open('', '_blank');
      printWin.document.write(`
         <!doctype html>
  <html>
  <head>
    <meta charset="UTF-8">
    <title>დანიშნულება</title>
    <style>
      @page { margin: 1.5cm 1.5cm 2cm 1.5cm; }
      body { font-family: 'BPG Nino Mtavruli', sans-serif; font-size: 12pt; line-height: 1.2; margin: 0; }
      .header { text-align: center; margin-top: -1cm; padding-bottom: 0.5rem; border-bottom: 2px solid #000; }
      .logo { width: 150px; height: 100px; object-fit: contain; margin-bottom: 0.3rem; }
      .clinic-name { font-size: 12pt; font-weight: bold; margin: 0.2rem 0; }
      .print-field { display: flex; gap: 1rem; margin: 0.8rem 0; font-size: 12pt; }
      .label { font-weight: bold; width: 120px; flex-shrink: 0; }
      .prescription {
        border: 1.5px solid #000;
        padding: 1rem;
        min-height: 200px;
        margin: 1.5rem 0;
        line-height: 1.2;
        font-size: 12pt;
        background: #fafafa;
      }
      .signatures {
        margin-top: 1.5rem;
        display: flex;
        justify-content: space-between;
        font-size: 12pt;
      }
      .doctor-sign, .patient-sign { width: 48%; }
      .doctor-sign { text-align: left; }
      .patient-sign { text-align: right; }
      .sign-line { margin-top: 0.4rem; }
    </style>
  </head>
  <body>
    <div class="header">
      <img src="tm_center_logo.png" class="logo" alt="Logo">
      <div class="clinic-name">
        თბილისის სახელმწიფო სამედიცინო უნივერსიტეტისა და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა
      </div>
    </div>
    <div class="print-field"><span class="label">პაციენტი:</span> ${data.patient}</div>
    <div class="print-field"><span class="label">ისტორია №:</span> ${data.history}</div>
    <div class="print-field"><span class="label">თარიღი:</span> ${data.date}</div>
    <div class="prescription">${data.content}</div>

    <div class="signatures">
      <div class="doctor-sign">
        <p style="margin:0;"><strong>ექიმი:</strong> ${data.doctor}</p>
        <p class="sign-line">ხელმოწერა: _________________</p>
      </div>
      <div class="patient-sign">
        ${requirePatientSig ? `
        <p style="margin:0;">გავეცანი, ჩავიბარე,</p>
        <p class="sign-line">პაციენტის ხელმოწერა: _________________</p>
        ` : ''}
      </div>
    </div>
  </body>
  </html>
      `);
      printWin.document.close();
      setTimeout(() => printWin.print(), 600);
    }

    function showToast(msg, type = 'success') {
      const toast = document.createElement('div');
      toast.className = `toast px-5 py-3 rounded-lg text-white font-medium shadow-lg flex items-center gap-2 ${type === 'error' ? 'bg-red-500' : 'bg-green-500'}`;
      toast.innerHTML = `${type === 'error' ? 'გაფრთხილება' : 'წარმატებული'} ${msg}`;
      document.body.appendChild(toast);
      setTimeout(() => toast.remove(), 3000);
    }

    function escapeHtml(text) {
      const div = document.createElement('div');
      div.textContent = text;
      return div.innerHTML;
    }
  </script>
</body>
</html>
