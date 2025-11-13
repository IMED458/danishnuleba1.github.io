<html lang="ka">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.min.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.snow.css" rel="stylesheet">
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

    /* Quill Editor - შემცირებული ხაზებს შორის */
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
      line-height: 1.35 !important;
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
      animation: slideIn 0.3s ease-out;
    }
    @keyframes slideIn {
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

    /* ლოგო – პატარა ინტერფეისში */
    .logo-container {
      width: 9rem;
      height: 6rem;
      margin: 0 auto 1rem;
      border-radius: 0.75rem;
      overflow: hidden;
      border: 3px solid #dbeafe;
      box-shadow: 0 6px 15px rgba(0,0,0,0.08);
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
    <!-- Header Card – პატარა ინტერფეისში -->
    <div class="card p-4 md:p-6 text-center mb-6">
      <div class="logo-container">
        <img src="tm_center_logo.png" alt="TM Center">
      </div>
      <h1 class="text-lg md:text-xl font-bold text-gray-800 leading-tight">
        თბილისის სახელმწიფო სამედიცინო უნივერსიტეტისა და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა
      </h1>
      <h2 class="text-lg md:text-xl font-bold text-blue-600 mt-2 flex items-center justify-center gap-2">
        სამედიცინო დანიშნულება
      </h2>
    </div>

    <!-- Main Form Card -->
    <div class="card p-6 md:p-8 mb-6">
      <form id="prescription-form">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
          <div class="input-group">
            <label>პაციენტი</label>
            <input type="text" id="patient-name" class="input-field w-full" placeholder="ნინო გელაშვილი">
          </div>
          <div class="input-group">
            <label>ისტორიის №</label>
            <input type="text" id="history-number" class="input-field w-full" placeholder="2024-001234">
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
          <button type="button" id="open-templates-btn" class="btn btn-primary">
            შაბლონები
          </button>
          <button type="button" id="save-template-btn" class="btn btn-success">
            შაბლონის შენახვა
          </button>
        </div>

        <div class="mb-6">
          <label class="block text-sm font-semibold text-gray-700 mb-2">დანიშნულება</label>
          <div id="editor" style="height: 220px;"></div>
        </div>

        <div class="flex flex-wrap gap-3 justify-end">
          <button type="button" id="clear-btn" class="btn btn-secondary">
            გასუფთავება
          </button>
          <button type="button" id="print-btn" class="btn btn-primary text-lg font-semibold">
            ბეჭდვა
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Templates Modal -->
  <div id="templates-modal" class="fixed inset-0 modal hidden items-center justify-center z-50">
    <div class="bg-white rounded-2xl shadow-2xl w-full max-w-3xl mx-4 max-h-[85vh] overflow-hidden flex flex-col">
      <div class="p-5 border-b border-gray-200 flex justify-between items-center bg-gradient-to-r from-blue-50 to-indigo-50">
        <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
          შაბლონები
        </h3>
        <button id="close-templates-modal" class="text-gray-500 hover:text-gray-700 p-2 rounded-lg hover:bg-white transition">
          <i class="fas fa-times text-xl"></i>
        </button>
      </div>
      <div id="templates-container" class="flex-1 overflow-y-auto p-5">
        <p id="no-templates" class="text-center text-gray-500 py-12 text-lg">შაბლონები არ არის შენახული</p>
        <div id="templates-grid" class="grid grid-cols-1 md:grid-cols-2 gap-4"></div>
      </div>
      <div class="p-4 border-t border-gray-200 bg-gray-50 text-right">
        <button id="close-templates-btn" class="btn btn-secondary">
          დახურვა
        </button>
      </div>
    </div>
  </div>

  <!-- Save Template Modal -->
  <div id="save-template-modal" class="fixed inset-0 modal hidden items-center justify-center z-50">
    <div class="bg-white rounded-2xl shadow-2xl p-6 w-full max-w-md mx-4">
      <h3 class="text-xl font-bold text-gray-800 mb-4 flex items-center gap-2">
        შაბლონის შენახვა
      </h3>
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

  <!-- Firebase + Script -->
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

    function formatGeorgianDate(dateString) {
      if (!dateString) return '-';
      const date = new Date(dateString);
      const day = String(date.getDate()).padStart(2, '0');
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const year = date.getFullYear();
      return `${day}/${month}/${year}`;
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
    });

    function setupEventListeners() {
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
      const modal = document.getElementById('templates-modal');
      modal.classList.remove('hidden');
      modal.classList.add('flex');
    }

    function closeTemplatesModal() {
      const modal = document.getElementById('templates-modal');
      modal.classList.add('hidden');
      modal.classList.remove('flex');
    }

    function showSaveTemplateModal() {
      const content = quill.root.innerHTML.trim();
      if (!content || content === '<p><br></p>') return showToast('დანიშნულება ცარიელია', 'error');
      const modal = document.getElementById('save-template-modal');
      modal.classList.remove('hidden');
      modal.classList.add('flex');
      document.getElementById('template-name-input').focus();
    }

    function hideSaveTemplateModal() {
      const modal = document.getElementById('save-template-modal');
      modal.classList.add('hidden');
      modal.classList.remove('flex');
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
      ['patient-name', 'history-number', 'doctor-name'].forEach(id => document.getElementById(id).value = '');
      document.getElementById('date').value = new Date().toISOString().split('T')[0];
      quill.setContents([]);
    }

    // === ბეჭდვა – ლოგო დიდი ===
    function handlePrint() {
      const data = {
        patient: document.getElementById('patient-name').value || '-',
        history: document.getElementById('history-number').value || '-',
        date: document.getElementById('date').value ? formatGeorgianDate(document.getElementById('date').value) : '-',
        doctor: document.getElementById('doctor-name').value || '-',
        content: quill.root.innerHTML || '<p>-</p>'
      };

      const printWin = window.open('', '_blank');
      printWin.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
          <meta charset="UTF-8">
          <title>დანიშნულება</title>
          <style>
            body { 
              font-family: 'BPG Nino Mtavruli', sans-serif; 
              margin: 2cm; 
              font-size: 12pt; 
              line-height: 1.35; 
            }
            .header { 
              text-align: center; 
              border-bottom: 3px double #000; 
              padding-bottom: 1.5rem; 
              margin-bottom: 1.8rem; 
            }
            .logo { 
              width: 220px; 
              height: 150px; 
              object-fit: contain; 
              margin-bottom: 0.8rem;
              border: 1px solid #ccc; 
              border-radius: 8px;
              padding: 8px;
              background: white;
            }
            .print-field { 
              display: flex; 
              gap: 1rem; 
              margin: 0.8rem 0; 
              font-size: 13pt;
            }
            .label { 
              font-weight: bold; 
              width: 130px; 
              flex-shrink: 0;
            }
            .prescription { 
              border: 1.5px solid #000; 
              padding: 1.2rem; 
              min-height: 220px; 
              margin: 1.8rem 0; 
              line-height: 1.35; 
              font-size: 12.5pt;
              background: #fafafa;
            }
            .signature { 
              margin-top: 4rem; 
              text-align: right; 
              font-size: 13pt;
            }
            @media print { 
              body { margin: 1.2cm; } 
              .logo { width: 200px; height: 135px; }
            }
          </style>
        </head>
        <body>
          <div class="header">
            <img src="tm_center_logo.png" class="logo" alt="Logo">
            <h1 style="font-size:15pt;margin:0.6rem 0;font-weight:bold;">
              თბილისის სახელმწიფო სამედიცინო უნივერსიტეტისა და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა
            </h1>
            <h2 style="font-size:17pt;margin:0.6rem 0;font-weight:bold;color:#1d4ed8;">
              სამედიცინო დანიშნულება
            </h2>
          </div>
          <div class="print-field"><span class="label">პაციენტი:</span> ${data.patient}</div>
          <div class="print-field"><span class="label">ისტორია №:</span> ${data.history}</div>
          <div class="print-field"><span class="label">თარიღი:</span> ${data.date}</div>
          <div class="prescription">${data.content}</div>
          <div class="signature">
            <p><strong>ექიმი:</strong> ${data.doctor}</p>
            <p style="margin-top:2.5rem;border-top:1px solid #000;padding-top:0.5rem;display:inline-block;">
              ხელმოწერა: _________________
            </p>
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
      toast.innerHTML = `${type === 'error' ? '<i class="fas fa-times-circle"></i>' : '<i class="fas fa-check-circle"></i>'} ${msg}`;
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
