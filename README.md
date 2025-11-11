<html lang="ka">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>სამედიცინო დანიშნულების სისტემა</title>
  <script src="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.min.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/quill@1.3.7/dist/quill.snow.css" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      box-sizing: border-box;
      font-family: 'BPG Nino Mtavruli', 'Sylfaen', 'DejaVu Sans', sans-serif;
    }
    .medical-logo {
      width: 100px;
      height: 100px;
      margin: 0 auto 16px;
    }
    .ql-editor {
      min-height: 200px;
      font-family: inherit;
    }
    .template-item {
      transition: all 0.2s ease;
      cursor: pointer;
    }
    .template-item:hover {
      background-color: #f3f4f6;
    }
    .modal-backdrop {
      backdrop-filter: blur(4px);
    }
  </style>
</head>
<body class="bg-gray-50 min-h-screen">
  <div class="max-w-4xl mx-auto p-6">
    <!-- Header -->
    <header class="text-center mb-8 bg-white rounded-lg shadow-sm p-6">
      <div class="medical-logo mx-auto mb-4">
        <img src="tm_center_logo.png" alt="TM Center Logo" class="w-full h-full object-contain">
      </div>
      <h1 id="clinic-name" class="text-lg font-bold text-gray-800 leading-tight">
        იმედის სამედიცინო ცენტრი
      </h1>
      <h2 id="form-title" class="text-xl font-semibold text-blue-600 mt-4">სამედიცინო დანიშნულება</h2>
    </header>

    <!-- Main Form -->
    <div class="bg-white rounded-lg shadow-sm p-6 mb-6">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
        <div>
          <label for="patient-name" class="block text-sm font-medium text-gray-700 mb-2">პაციენტის სახელი და გვარი</label>
          <input type="text" id="patient-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="მაგ: ნინო გელაშვილი">
        </div>
        <div>
          <label for="history-number" class="block text-sm font-medium text-gray-700 mb-2">ისტორიის ნომერი</label>
          <input type="text" id="history-number" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="მაგ: 2024-001234">
        </div>
        <div>
          <label for="date" class="block text-sm font-medium text-gray-700 mb-2">თარიღი</label>
          <input type="date" id="date" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
        </div>
        <div>
          <label for="doctor-name" class="block text-sm font-medium text-gray-700 mb-2">ექიმი</label>
          <input type="text" id="doctor-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="მაგ: ნინო კიკვაძე">
        </div>
      </div>

      <!-- Buttons -->
      <div class="mb-6 flex justify-between items-center">
        <button id="open-templates-btn" class="px-5 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 transition-colors">
          შაბლონები
        </button>
        <button id="save-template-btn" class="px-5 py-2 bg-green-600 text-white rounded-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 transition-colors">
          შაბლონის შენახვა
        </button>
      </div>

      <!-- Editor -->
      <div class="mb-6">
        <label class="block text-sm font-medium text-gray-700 mb-2">დანიშნულება</label>
        <div id="editor" class="bg-white border border-gray-300 rounded-md"></div>
      </div>

      <!-- Action Buttons -->
      <div class="flex justify-end space-x-4">
        <button id="clear-btn" class="px-6 py-2 bg-gray-500 text-white rounded-md hover:bg-gray-600 focus:outline-none focus:ring-2 focus:ring-gray-500 transition-colors">
          გასუფთავება
        </button>
        <button id="print-btn" class="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-colors">
          ბეჭდვა
        </button>
      </div>
    </div>
  </div>

  <!-- Templates Modal -->
  <div id="templates-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50 modal-backdrop">
    <div class="bg-white rounded-lg shadow-xl w-full max-w-2xl mx-4 max-h-[80vh] overflow-hidden flex flex-col">
      <div class="p-5 border-b border-gray-200 flex justify-between items-center">
        <h3 class="text-lg font-semibold text-gray-800">შაბლონები</h3>
        <button id="close-templates-modal" class="text-gray-500 hover:text-gray-700">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
      <div id="templates-container" class="flex-1 overflow-y-auto p-5">
        <p id="no-templates" class="text-gray-500 text-center py-8">შაბლონები არ არის შენახული</p>
        <div id="templates-grid" class="grid grid-cols-1 gap-3"></div>
      </div>
      <div class="p-4 border-t border-gray-200 bg-gray-50 text-right">
        <button id="close-templates-btn" class="px-5 py-2 bg-gray-600 text-white rounded-md hover:bg-gray-700 transition-colors">
          დახურვა
        </button>
      </div>
    </div>
  </div>

  <!-- Save Template Modal -->
  <div id="save-template-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50 modal-backdrop">
    <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
      <h3 class="text-lg font-medium text-gray-800 mb-4">შაბლონის შენახვა</h3>
      <input type="text" id="template-name-input" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-4" placeholder="შაბლონის სახელი">
      <div class="flex justify-end space-x-3">
        <button id="cancel-save-template" class="px-4 py-2 bg-gray-500 text-white rounded-md hover:bg-gray-600 transition-colors">გაუქმება</button>
        <button id="confirm-save-template" class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors">შენახვა</button>
      </div>
    </div>
  </div>

  <script>
    // Global
    let quill;
    const STORAGE_KEY = 'medical_templates_tmcenter';
    let templates = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');

    document.addEventListener('DOMContentLoaded', () => {
      document.getElementById('date').value = new Date().toISOString().split('T')[0];

      quill = new Quill('#editor', {
        theme: 'snow',
        modules: {
          toolbar: [
            [{ 'header': [1, 2, 3, false] }],
            ['bold', 'italic', 'underline'],
            [{ 'list': 'ordered' }, { 'list': 'bullet' }],
            ['clean']
          ]
        },
        placeholder: 'შეიყვანეთ დანიშნულება...'
      });

      setupEventListeners();
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
      document.getElementById('templates-modal').addEventListener('click', (e) => {
        if (e.target.id === 'templates-modal') closeTemplatesModal();
      });
      document.getElementById('save-template-modal').addEventListener('click', (e) => {
        if (e.target.id === 'save-template-modal') hideSaveTemplateModal();
      });
    }

    // === Templates Modal ===
    function openTemplatesModal() {
      renderTemplatesInModal();
      document.getElementById('templates-modal').classList.remove('hidden');
      document.getElementById('templates-modal').classList.add('flex');
    }

    function closeTemplatesModal() {
      document.getElementById('templates-modal').classList.add('hidden');
      document.getElementById('templates-modal').classList.remove('flex');
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
        const item = document.createElement('div');
        item.className = 'template-item bg-gray-50 p-4 rounded-lg border border-gray-200 flex justify-between items-center';
        item.innerHTML = `
          <div>
            <h4 class="font-medium text-gray-800">${escapeHtml(t.name)}</h4>
            <p class="text-xs text-gray-500">${new Date(t.created_at).toLocaleDateString('ka-GE')}</p>
          </div>
          <div class="flex space-x-2">
            <button class="load-template text-blue-600 hover:text-blue-800 text-sm font-medium" data-id="${t.id}">ჩატვირთვა</button>
            <button class="delete-template text-red-600 hover:text-red-800 text-sm font-medium" data-id="${t.id}">წაშლა</button>
          </div>
        `;

        item.querySelector('.load-template').addEventListener('click', () => {
          loadTemplate(t);
          closeTemplatesModal();
          showMessage('შაბლონი ჩაიტვირთა', 'success');
        });

        item.querySelector('.delete-template').addEventListener('click', () => {
          if (confirm(`ნამდვილად გსურთ შაბლონის წაშლა: "${t.name}"?`)) {
            deleteTemplate(t.id);
            renderTemplatesInModal();
            showMessage('შაბლონი წაიშალა', 'success');
          }
        });

        grid.appendChild(item);
      });
    }

    function loadTemplate(template) {
      quill.root.innerHTML = template.content;
    }

    function deleteTemplate(id) {
      templates = templates.filter(t => t.id !== id);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(templates));
    }

    // === Save Template ===
    function showSaveTemplateModal() {
      const content = quill.root.innerHTML.trim();
      if (!content || content === '<p><br></p>') {
        showMessage('დანიშნულების ველი ცარიელია', 'error');
        return;
      }
      document.getElementById('save-template-modal').classList.remove('hidden');
      document.getElementById('save-template-modal').classList.add('flex');
      document.getElementById('template-name-input').focus();
    }

    function hideSaveTemplateModal() {
      document.getElementById('save-template-modal').classList.add('hidden');
      document.getElementById('save-template-modal').classList.remove('flex');
      document.getElementById('template-name-input').value = '';
    }

    function saveTemplate() {
      const name = document.getElementById('template-name-input').value.trim();
      if (!name) {
        showMessage('შეიყვანეთ შაბლონის სახელი', 'error');
        return;
      }
      if (templates.length >= 999) {
        showMessage('მაქსიმალური რაოდენობა (999)', 'error');
        return;
      }

      const newTemplate = {
        id: Date.now().toString(),
        name: name,
        content: quill.root.innerHTML,
        created_at: new Date().toISOString()
      };

      templates.push(newTemplate);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(templates));
      hideSaveTemplateModal();
      showMessage('შაბლონი შეინახა', 'success');
    }

    // === Other ===
    function handleClear() {
      document.getElementById('patient-name').value = '';
      document.getElementById('history-number').value = '';
      document.getElementById('date').value = new Date().toISOString().split('T')[0];
      document.getElementById('doctor-name').value = '';
      quill.setContents([]);
    }

    function handlePrint() {
      const patientName = document.getElementById('patient-name').value || '-';
      const historyNumber = document.getElementById('history-number').value || '-';
      const date = document.getElementById('date').value ? new Date(document.getElementById('date').value).toLocaleDateString('ka-GE') : '-';
      const doctor = document.getElementById('doctor-name').value || '-';
      const prescription = quill.root.innerHTML || '<p>-</p>';
      const clinicName = document.getElementById('clinic-name').textContent;
      const formTitle = document.getElementById('form-title').textContent;

      const printContent = `
        <!DOCTYPE html>
        <html lang="ka">
        <head>
          <meta charset="UTF-8">
          <title>დანიშნულება</title>
          <style>
            body { font-family: 'BPG Nino Mtavruli', 'Sylfaen', sans-serif; margin: 0; padding: 20px; font-size: 12pt; line-height: 1.5; }
            .header { text-align: center; margin-bottom: 30px; border-bottom: 2px solid #000; padding-bottom: 15px; }
            .logo { width: 80px; height: 80px; margin: 0 auto 10px; object-fit: contain; }
            .field { margin: 12px 0; }
            .label { font-weight: bold; display: inline-block; width: 120px; }
            .prescription { border: 1px solid #000; padding: 15px; margin: 20px 0; min-height: 180px; }
            .signature { margin-top: 50px; text-align: right; }
            @media print { body { margin: 0; } }
          </style>
        </head>
        <body>
          <div class="header">
            <img src="tm_center_logo.png" class="logo" alt="TM Center Logo">
            <h1 style="font-size: 14pt; margin: 8px 0;">${clinicName}</h1>
            <h2 style="font-size: 16pt; font-weight: bold; margin: 5px 0;">${formTitle}</h2>
          </div>
          <div class="field"><span class="label">პაციენტი:</span> ${patientName}</div>
          <div class="field"><span class="label">ისტორიის №:</span> ${historyNumber}</div>
          <div class="field"><span class="label">თარიღი:</span> ${date}</div>
          <div class="prescription">${prescription}</div>
          <div class="signature">
            <p><strong>ექიმი:</strong> ${doctor}</p>
            <p style="margin-top: 25px;">ხელმოწერა: _________________</p>
          </div>
        </body>
        </html>
      `;

      const win = window.open('', '_blank');
      if (win) {
        win.document.write(printContent);
        win.document.close();
        win.focus();
        setTimeout(() => win.print(), 500);
      } else {
        showMessage('ბეჭდვის ფანჯარა ვერ გაიხსნა', 'error');
      }
    }

    function showMessage(msg, type = 'success') {
      const el = document.createElement('div');
      el.className = `fixed top-4 right-4 px-4 py-2 rounded-md text-white z-50 shadow-lg ${type === 'error' ? 'bg-red-500' : 'bg-green-500'}`;
      el.textContent = msg;
      document.body.appendChild(el);
      setTimeout(() => el.remove(), 3000);
    }

    function escapeHtml(text) {
      const div = document.createElement('div');
      div.textContent = text;
      return div.innerHTML;
    }
  </script>
</body>
</html>
