<!doctype html>
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
      width: 80px;
      height: 80px;
      margin: 0 auto 16px;
    }
    .ql-editor {
      min-height: 200px;
      font-family: inherit;
    }
    .template-item {
      transition: all 0.2s ease;
    }
    .template-item:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    .loading {
      opacity: 0.6;
      pointer-events: none;
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
        თბილისის სახელმწიფო სამედიცინო უნივერსიტეტის და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა
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

      <!-- Templates Section -->
      <div class="mb-6">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-medium text-gray-800">შაბლონები</h3>
          <button id="save-template-btn" class="px-4 py-2 bg-green-600 text-white rounded-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 transition-colors">
            შაბლონის შენახვა
          </button>
        </div>
        <div id="templates-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3 mb-4">
          <!-- Templates will be loaded here -->
        </div>
      </div>

      <!-- Rich Text Editor -->
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

  <!-- Template Save Modal -->
  <div id="template-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
    <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
      <h3 class="text-lg font-medium text-gray-800 mb-4">შაბლონის შენახვა</h3>
      <input type="text" id="template-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-4" placeholder="შაბლონის სახელი">
      <div class="flex justify-end space-x-3">
        <button id="cancel-template" class="px-4 py-2 bg-gray-500 text-white rounded-md hover:bg-gray-600 transition-colors">გაუქმება</button>
        <button id="confirm-save-template" class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors">შენახვა</button>
      </div>
    </div>
  </div>

  <script>
    // Global variables
    let quill;
    let templates = JSON.parse(localStorage.getItem('medical_templates') || '[]');

    // Initialize Quill
    document.addEventListener('DOMContentLoaded', () => {
      document.getElementById('date').value = new Date().toISOString().split('T')[0];
      
      quill = new Quill('#editor', {
        theme: 'snow',
        modules: {
          toolbar: [
            [{ 'header': [1, 2, 3, false] }],
            ['bold', 'italic', 'underline'],
            [{ 'list': 'ordered'}, { 'list': 'bullet' }],
            ['clean']
          ]
        },
        placeholder: 'შეიყვანეთ დანიშნულება...'
      });

      renderTemplates();
      setupEventListeners();
    });

    function setupEventListeners() {
      document.getElementById('print-btn').addEventListener('click', handlePrint);
      document.getElementById('clear-btn').addEventListener('click', handleClear);
      document.getElementById('save-template-btn').addEventListener('click', showTemplateModal);
      document.getElementById('cancel-template').addEventListener('click', hideTemplateModal);
      document.getElementById('confirm-save-template').addEventListener('click', saveTemplate);
      document.getElementById('template-modal').addEventListener('click', (e) => {
        if (e.target.id === 'template-modal') hideTemplateModal();
      });
    }

    function renderTemplates() {
      const container = document.getElementById('templates-list');
      container.innerHTML = '';

      if (templates.length === 0) {
        container.innerHTML = '<p class="text-gray-500 col-span-full text-center py-4">შაბლონები არ არის შენახული</p>';
        return;
      }

      templates.forEach(template => {
        const el = document.createElement('div');
        el.className = 'template-item bg-gray-50 p-3 rounded-md border border-gray-200 cursor-pointer';
        el.innerHTML = `
          <div class="flex justify-between items-start">
            <div class="flex-1">
              <h4 class="font-medium text-gray-800 text-sm">${escapeHtml(template.name)}</h4>
              <p class="text-xs text-gray-500 mt-1">${new Date(template.created_at).toLocaleDateString('ka-GE')}</p>
            </div>
            <button class="delete-template text-red-500 hover:text-red-700 ml-2" data-id="${template.id}">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path>
              </svg>
            </button>
          </div>
        `;

        el.addEventListener('click', (e) => {
          if (!e.target.closest('.delete-template')) {
            loadTemplate(template);
          }
        });

        el.querySelector('.delete-template').addEventListener('click', (e) => {
          e.stopPropagation();
          deleteTemplate(template.id);
        });

        container.appendChild(el);
      });
    }

    function loadTemplate(template) {
      quill.root.innerHTML = template.content;
    }

    function deleteTemplate(id) {
      if (!confirm('ნამდვილად გსურთ შაბლონის წაშლა?')) return;
      templates = templates.filter(t => t.id !== id);
      localStorage.setItem('medical_templates', JSON.stringify(templates));
      renderTemplates();
      showMessage('შაბლონი წაიშალა', 'success');
    }

    function showTemplateModal() {
      const content = quill.root.innerHTML.trim();
      if (!content || content === '<p><br></p>') {
        showMessage('დანიშნულების ველი ცარიელია', 'error');
        return;
      }
      document.getElementById('template-modal').classList.remove('hidden');
      document.getElementById('template-modal').classList.add('flex');
      document.getElementById('template-name').focus();
    }

    function hideTemplateModal() {
      document.getElementById('template-modal').classList.add('hidden');
      document.getElementById('template-modal').classList.remove('flex');
      document.getElementById('template-name').value = '';
    }

    function saveTemplate() {
      const name = document.getElementById('template-name').value.trim();
      const content = quill.root.innerHTML;

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
        content: content,
        created_at: new Date().toISOString()
      };

      templates.push(newTemplate);
      localStorage.setItem('medical_templates', JSON.stringify(templates));
      hideTemplateModal();
      renderTemplates();
      showMessage('შაბლონი შეინახა', 'success');
    }

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
          <title>დანიშნულება - ბეჭდვა</title>
          <style>
            body { font-family: 'BPG Nino Mtavruli', 'Sylfaen', sans-serif; margin: 0; padding: 20px; font-size: 12pt; line-height: 1.5; }
            .header { text-align: center; margin-bottom: 30px; border-bottom: 2px solid #000; padding-bottom: 15px; }
            .logo { width: 60px; height: 60px; margin: 0 auto 10px; }
            .field { margin: 12px 0; }
            .label { font-weight: bold; display: inline-block; width: 120px; }
            .prescription { border: 1px solid #000; padding: 15px; margin: 20px 0; min-height: 180px; }
            .signature { margin-top: 50px; text-align: right; }
            @media print { body { margin: 0; } }
          </style>
        </head>
        <body>
          <div class="header">
            <img src="tm_center_logo.png" class="logo" alt="Logo">
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

      const printWin = window.open('', '_blank');
      if (printWin) {
        printWin.document.write(printContent);
        printWin.document.close();
        printWin.focus();
        setTimeout(() => printWin.print(), 500);
      } else {
        showMessage('ბეჭდვის ფანჯარა ვერ გაიხსნა', 'error');
      }
    }

    function showMessage(msg, type = 'success') {
      const el = document.createElement('div');
      el.className = `fixed top-4 right-4 px-4 py-2 rounded-md text-white z-50 ${type === 'error' ? 'bg-red-500' : 'bg-green-500'}`;
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
