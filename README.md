<!doctype html>
<html lang="ka">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>სამედიცინო დანიშნულების სისტემა</title>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="/_sdk/data_sdk.js"></script>
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
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body class="bg-gray-50 min-h-full">
  <div class="max-w-4xl mx-auto p-6"><!-- Header -->
   <header class="text-center mb-8 bg-white rounded-lg shadow-sm p-6">
    <div class="medical-logo mx-auto mb-4"><img src="https://drive.google.com/uc?id=1Jbp9uUVcoaYy0t38qy-Esq-Y1dkYP-pa" alt="კლინიკის ლოგო" class="w-full h-full object-contain" onerror="this.src=''; this.alt='ლოგო ვერ ჩაიტვირთა'; this.style.display='none';">
    </div>
    <h1 id="clinic-name" class="text-lg font-bold text-gray-800 leading-tight">თბილისის სახელმწიფო სამედიცინო უნივერსიტეტის და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა</h1>
    <h2 id="form-title" class="text-xl font-semibold text-blue-600 mt-4">სამედიცინო დანიშნულება</h2>
   </header><!-- Main Form -->
   <div class="bg-white rounded-lg shadow-sm p-6 mb-6">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
     <div><label for="patient-name" class="block text-sm font-medium text-gray-700 mb-2"> პაციენტის სახელი და გვარი </label> <input type="text" id="patient-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="მაგ: ნინო გელაშვილი">
     </div>
     <div><label for="history-number" class="block text-sm font-medium text-gray-700 mb-2"> ისტორიის ნომერი </label> <input type="text" id="history-number" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="მაგ: 2024-001234">
     </div>
     <div><label for="date" class="block text-sm font-medium text-gray-700 mb-2"> თარიღი </label> <input type="date" id="date" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
     </div>
     <div><label for="doctor-name" class="block text-sm font-medium text-gray-700 mb-2"> ექიმი </label> <input type="text" id="doctor-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="მაგ: ნინო კიკვაძე">
     </div>
    </div><!-- Templates Section -->
    <div class="mb-6">
     <div class="flex justify-between items-center mb-4">
      <h3 class="text-lg font-medium text-gray-800">შაბლონები</h3><button id="save-template-btn" class="px-4 py-2 bg-green-600 text-white rounded-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 transition-colors"> შაბლონის შენახვა </button>
     </div>
     <div id="templates-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3 mb-4"><!-- Templates will be loaded here -->
     </div>
    </div><!-- Rich Text Editor -->
    <div class="mb-6"><label class="block text-sm font-medium text-gray-700 mb-2"> დანიშნულება </label>
     <div id="editor" class="bg-white border border-gray-300 rounded-md"></div>
    </div><!-- Action Buttons -->
    <div class="flex justify-end space-x-4"><button id="clear-btn" class="px-6 py-2 bg-gray-500 text-white rounded-md hover:bg-gray-600 focus:outline-none focus:ring-2 focus:ring-gray-500 transition-colors"> გასუფთავება </button> <button id="print-btn" class="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-colors"> ბეჭდვა </button>
    </div>
   </div>
  </div><!-- Template Save Modal -->
  <div id="template-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
   <div class="bg-white rounded-lg p-6 w-full max-w-md mx-4">
    <h3 class="text-lg font-medium text-gray-800 mb-4">შაბლონის შენახვა</h3><input type="text" id="template-name" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-4" placeholder="შაბლონის სახელი">
    <div class="flex justify-end space-x-3"><button id="cancel-template" class="px-4 py-2 bg-gray-500 text-white rounded-md hover:bg-gray-600 transition-colors"> გაუქმება </button> <button id="confirm-save-template" class="px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors"> შენახვა </button>
    </div>
   </div>
  </div>
  <script>
        // Configuration
        const defaultConfig = {
            clinic_name: "თბილისის სახელმწიფო სამედიცინო უნივერსიტეტის და ინგოროყვას მაღალი სამედიცინო ტექნოლოგიების საუნივერსიტეტო კლინიკა",
            form_title: "სამედიცინო დანიშნულება"
        };

        // Global variables
        let quill;
        let templates = [];
        let isLoading = false;

        // Data SDK Handler
        const dataHandler = {
            onDataChanged(data) {
                templates = data;
                renderTemplates();
            }
        };

        // Initialize application
        async function initApp() {
            // Set current date
            document.getElementById('date').value = new Date().toISOString().split('T')[0];
            
            // Initialize Quill editor
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

            // Initialize Data SDK
            if (window.dataSdk) {
                const initResult = await window.dataSdk.init(dataHandler);
                if (!initResult.isOk) {
                    console.error('Failed to initialize data SDK');
                }
            }

            // Initialize Element SDK
            if (window.elementSdk) {
                await window.elementSdk.init({
                    defaultConfig,
                    onConfigChange: async (config) => {
                        document.getElementById('clinic-name').textContent = config.clinic_name || defaultConfig.clinic_name;
                        document.getElementById('form-title').textContent = config.form_title || defaultConfig.form_title;
                    },
                    mapToCapabilities: (config) => ({
                        recolorables: [],
                        borderables: [],
                        fontEditable: undefined,
                        fontSizeable: undefined
                    }),
                    mapToEditPanelValues: (config) => new Map([
                        ["clinic_name", config.clinic_name || defaultConfig.clinic_name],
                        ["form_title", config.form_title || defaultConfig.form_title]
                    ])
                });
            }

            setupEventListeners();
        }

        function setupEventListeners() {
            // Print button
            document.getElementById('print-btn').addEventListener('click', handlePrint);
            
            // Clear button
            document.getElementById('clear-btn').addEventListener('click', handleClear);
            
            // Template save button
            document.getElementById('save-template-btn').addEventListener('click', showTemplateModal);
            
            // Template modal buttons
            document.getElementById('cancel-template').addEventListener('click', hideTemplateModal);
            document.getElementById('confirm-save-template').addEventListener('click', saveTemplate);
            
            // Close modal on outside click
            document.getElementById('template-modal').addEventListener('click', (e) => {
                if (e.target.id === 'template-modal') {
                    hideTemplateModal();
                }
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
                const templateEl = document.createElement('div');
                templateEl.className = 'template-item bg-gray-50 p-3 rounded-md border border-gray-200 cursor-pointer';
                templateEl.innerHTML = `
                    <div class="flex justify-between items-start">
                        <div class="flex-1">
                            <h4 class="font-medium text-gray-800 text-sm">${template.name}</h4>
                            <p class="text-xs text-gray-500 mt-1">${new Date(template.created_at).toLocaleDateString('ka-GE')}</p>
                        </div>
                        <button class="delete-template text-red-500 hover:text-red-700 ml-2" data-id="${template.__backendId}">
                            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                                <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path>
                            </svg>
                        </button>
                    </div>
                `;
                
                // Add click handler for template selection
                templateEl.addEventListener('click', (e) => {
                    if (!e.target.closest('.delete-template')) {
                        loadTemplate(template);
                    }
                });
                
                // Add delete handler
                const deleteBtn = templateEl.querySelector('.delete-template');
                deleteBtn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    deleteTemplate(template);
                });
                
                container.appendChild(templateEl);
            });
        }

        function loadTemplate(template) {
            quill.root.innerHTML = template.content;
        }

        async function deleteTemplate(template) {
            if (!window.dataSdk) return;
            
            setLoading(true);
            const result = await window.dataSdk.delete(template);
            setLoading(false);
            
            if (!result.isOk) {
                showMessage('შაბლონის წაშლა ვერ მოხერხდა', 'error');
            }
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

        async function saveTemplate() {
            const name = document.getElementById('template-name').value.trim();
            const content = quill.root.innerHTML;
            
            if (!name) {
                showMessage('შეიყვანეთ შაბლონის სახელი', 'error');
                return;
            }
            
            if (!window.dataSdk) {
                hideTemplateModal();
                return;
            }
            
            if (templates.length >= 999) {
                showMessage('შაბლონების მაქსიმალური რაოდენობა (999) მიღწეულია', 'error');
                return;
            }
            
            setLoading(true);
            const result = await window.dataSdk.create({
                id: Date.now().toString(),
                name: name,
                content: content,
                created_at: new Date().toISOString()
            });
            setLoading(false);
            
            if (result.isOk) {
                hideTemplateModal();
                showMessage('შაბლონი წარმატებით შეინახა', 'success');
            } else {
                showMessage('შაბლონის შენახვა ვერ მოხერხდა', 'error');
            }
        }

        function handleClear() {
            document.getElementById('patient-name').value = '';
            document.getElementById('history-number').value = '';
            document.getElementById('date').value = new Date().toISOString().split('T')[0];
            document.getElementById('doctor-name').value = '';
            quill.setContents([]);
        }

        function handlePrint() {
            const patientName = document.getElementById('patient-name').value;
            const historyNumber = document.getElementById('history-number').value;
            const date = document.getElementById('date').value;
            const doctor = document.getElementById('doctor-name').value;
            const prescription = quill.root.innerHTML;
            
            // Get current config
            const config = window.elementSdk ? window.elementSdk.config : defaultConfig;
            
            // Create print window content
            const printContent = `
                <!DOCTYPE html>
                <html lang="ka">
                <head>
                    <meta charset="UTF-8">
                    <title>სამედიცინო დანიშნულება - ბეჭდვა</title>
                    <style>
                        body {
                            font-family: 'BPG Nino Mtavruli', 'Sylfaen', 'DejaVu Sans', sans-serif;
                            margin: 0;
                            padding: 20px;
                            background: white;
                            color: black;
                            font-size: 12pt;
                            line-height: 1.4;
                        }
                        
                        .print-header {
                            text-align: center;
                            margin-bottom: 30px;
                            border-bottom: 2px solid #000;
                            padding-bottom: 20px;
                        }
                        
                        .medical-logo {
                            width: 60px;
                            height: 60px;
                            margin: 0 auto 16px;
                        }
                        
                        .print-content {
                            margin: 20px 0;
                        }
                        
                        .print-field {
                            margin-bottom: 15px;
                        }
                        
                        .print-label {
                            font-weight: bold;
                            display: inline-block;
                            width: 120px;
                        }
                        
                        .prescription-content {
                            border: 1px solid #000;
                            padding: 15px;
                            margin: 20px 0;
                            min-height: 200px;
                        }
                        
                        .doctor-signature {
                            margin-top: 40px;
                            text-align: right;
                        }
                        
                        @media print {
                            body { margin: 0; }
                        }
                    </style>
                </head>
                <body>
                    <div class="print-header">
                        <div class="medical-logo">
                            <img src="https://drive.google.com/uc?id=1Jbp9uUVcoaYy0t38qy-Esq-Y1dkYP-pa" 
                                 alt="კლინიკის ლოგო" 
                                 style="width: 60px; height: 60px; object-fit: contain;"
                                 onerror="this.style.display='none';">
                        </div>
                        <h1 style="font-size: 14pt; font-weight: bold; margin-bottom: 10px;">${config.clinic_name || defaultConfig.clinic_name}</h1>
                        <h2 style="font-size: 16pt; font-weight: bold;">${config.form_title || defaultConfig.form_title}</h2>
                    </div>
                    
                    <div class="print-content">
                        <div class="print-field">
                            <span class="print-label">პაციენტი:</span>
                            <span>${patientName || '-'}</span>
                        </div>
                        <div class="print-field">
                            <span class="print-label">ისტორიის №:</span>
                            <span>${historyNumber || '-'}</span>
                        </div>
                        <div class="print-field">
                            <span class="print-label">თარიღი:</span>
                            <span>${date ? new Date(date).toLocaleDateString('ka-GE') : '-'}</span>
                        </div>
                        
                        <div class="prescription-content">
                            ${prescription || '<p>-</p>'}
                        </div>
                        
                        <div class="doctor-signature">
                            <p><strong>ექიმი:</strong> ${doctor || '-'}</p>
                            <p style="margin-top: 20px;">ხელმოწერა: _________________</p>
                        </div>
                    </div>
                </body>
                </html>
            `;
            
            // Open new window and write content
            const printWindow = window.open('', '_blank', 'width=800,height=600,scrollbars=yes,resizable=yes');
            if (printWindow) {
                printWindow.document.write(printContent);
                printWindow.document.close();
            } else {
                showMessage('ბეჭდვის ფანჯრის გახსნა ვერ მოხერხდა', 'error');
            }
        }

        function setLoading(loading) {
            isLoading = loading;
            const elements = document.querySelectorAll('button, input, select');
            elements.forEach(el => {
                if (loading) {
                    el.classList.add('loading');
                } else {
                    el.classList.remove('loading');
                }
            });
        }

        function showMessage(message, type) {
            const messageEl = document.createElement('div');
            messageEl.className = `fixed top-4 right-4 px-4 py-2 rounded-md text-white z-50 ${
                type === 'error' ? 'bg-red-500' : 'bg-green-500'
            }`;
            messageEl.textContent = message;
            
            document.body.appendChild(messageEl);
            
            setTimeout(() => {
                messageEl.remove();
            }, 3000);
        }

        // Initialize app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9996b92d55e795a0',t:'MTc2MjI4NjY5Ni4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
