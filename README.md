# aitilabs
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мини-CRM для продажников</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            transition: background-color 0.3s, color 0.3s;
        }
        .container {
            display: flex;
            height: 100vh;
            overflow: hidden;
        }
        .left-frame, .right-frame {
            padding: 20px;
            overflow-y: auto;
        }
        .left-frame {
            flex: 1;
            border-right: 2px solid #FFD700;
        }
        .right-frame {
            flex: 1;
            background: #f9f9f9;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .save-btn {
            background: #28a745;
            color: white;
        }
        .update-btn {
            background: #007bff;
            color: white;
        }
        .filter-btn {
            background: #FFD700;
            margin: 5px;
            padding: 8px 15px;
            border-radius: 20px;
        }
        .client-list {
            margin-top: 20px;
        }
        .client-item {
            background: #fff;
            padding: 10px;
            margin: 10px 0;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .progress-bar {
            height: 10px;
            border-radius: 5px;
            width: 100px;
        }
        .theme-toggle {
            position: fixed;
            top: 10px;
            right: 10px;
            padding: 10px;
            background: #333;
            color: white;
            border-radius: 5px;
        }
        body.night {
            background: #1a1a1a;
            color: #fff;
        }
        .right-frame.night {
            background: #2a2a2a;
        }
        .client-item.night {
            background: #333;
        }
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            .left-frame {
                border-right: none;
                border-bottom: 2px solid #FFD700;
            }
        }
    </style>
</head>
<body>
    <button class="theme-toggle" onclick="toggleTheme()">Переключить тему</button>
    <div class="container">
        <div class="left-frame">
            <h2>Добавить клиента</h2>
            <div class="form-group">
                <label>Наименование Клиента</label>
                <input type="text" id="clientName">
            </div>
            <div class="form-group">
                <label>Юр. Лицо</label>
                <input type Luxembourgishtext" id="legalEntity">
            </div>
            <div class="form-group">
                <label>ИНН</label>
                <input type="text" id="inn">
            </div>
            <div class="form-group">
                <label>КПП</label>
                <input type="text" id="kpp">
            </div>
            <div class="form-group">
                <label>Сайт</label>
                <input type="text" id="website">
            </div>
            <div class="form-group">
                <label>Контактный телефон/e-mail</label>
                <input type="text" id="contact">
            </div>
            <div class="form-group">
                <label>Отрасль</label>
                <input type="text" id="industry">
            </div>
            <div class="form-group">
                <label>Местонахождение</label>
                <input type="text" id="location">
            </div>
            <div class="form-group">
                <label>Количество Сотрудников</label>
                <input type="number" id="employees">
            </div>
            <div class="form-group">
                <label>Филиальная Сеть (кол-во)</label>
                <input type="number" id="branches">
            </div>
            <div class="form-group">
                <label>Материнская Компания</label>
                <input type="text" id="parentCompany">
            </div>
            <div class="form-group">
                <label>Годовой оборот (СР)</label>
                <input type="number" id="turnover">
            </div>
            <div class="form-group">
                <label>ИТ Бюджет на нынешний год</label>
                <input type="number" id="itBudgetCurrent">
            </div>
            <div class="form-group">
                <label>ИТ Бюджет на прошлый год</label>
                <input type="number" id="itBudgetLast">
            </div>
            <div class="form-group">
                <label>Бюджет ИТ Внешний</label>
                <input type="number" id="itBudgetExternal">
            </div>
            <div class="form-group">
                <label>Предприятие Принятия Решений</label>
                <input type="text" id="decisionMaker">
            </div>
            <div class="form-group">
                <label>Статус</label>
                <select id="status">
                    <option value="Холодный">Холодный</option>
                    <option value="Тёплый">Тёплый</option>
                    <option value="Горячий">Горячий</option>
                </select>
            </div>
            <button class="save-btn" onclick="saveClient()">Сохранить</button>
        </div>
        <div class="right-frame">
            <h2>Клиенты</h2>
            <div class="filters">
                <button class="filter-btn" onclick="filterClients('Все')">Все</button>
                <button class="filter-btn" onclick="filterClients('Холодный')">Холодный</button>
                <button class="filter-btn" onclick="filterClients('Тёплый')">Тёплый</button>
                <button class="filter-btn" onclick="filterClients('Горячий')">Горячий</button>
                <button class="filter-btn" onclick="filterClients('Не заполненные')">Не заполненные</button>
                <div class="form-group">
                    <label>Поиск по названию</label>
                    <select id="searchClient">
                        <option value="">Выберите клиента</option>
                    </select>
                    <button onclick="searchByName()">ОК</button>
                </div>
            </div>
            <div class="client-list" id="clientList"></div>
        </div>
    </div>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/[твой_ID]/exec"; // Вставь сюда URL из Apps Script
        let clients = [];

        async function loadClients() {
            try {
                const response = await fetch(SCRIPT_URL);
                clients = await response.json();
                updateClientList();
            } catch (e) {
                console.error('Ошибка загрузки клиентов:', e);
                alert('Не могу загрузить клиентов, пиздец где-то в скрипте!');
            }
        }

        async function saveClient() {
            const client = {
                clientName: document.getElementById('clientName').value,
                legalEntity: document.getElementById('legalEntity').value,
                inn: document.getElementById('inn').value,
                kpp: document.getElementById('kpp').value,
                website: document.getElementById('website').value,
                contact: document.getElementById('contact').value,
                industry: document.getElementById('industry').value,
                location: document.getElementById('location').value,
                employees: document.getElementById('employees').value,
                branches: document.getElementById('branches').value,
                parentCompany: document.getElementById('parentCompany').value,
                turnover: document.getElementById('turnover').value,
                itBudgetCurrent: document.getElementById('itBudgetCurrent').value,
                itBudgetLast: document.getElementById('itBudgetLast').value,
                itBudgetExternal: document.getElementById('itBudgetExternal').value,
                decisionMaker: document.getElementById('decisionMaker').value,
                status: document.getElementById('status').value
            };
            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST',
                    body: JSON.stringify(client),
                    headers: { 'Content-Type': 'application/json' }
                });
                clearForm();
                alert('Клиент сохранён, пиздец как круто!');
                loadClients();
            } catch (e) {
                console.error('Ошибка сохранения:', e);
                alert('Не удалось сохранить, пиздец где-то в соединении!');
            }
        }

        async function updateClient(index) {
            const client = {
                clientName: document.getElementById('clientName').value,
                legalEntity: document.getElementById('legalEntity').value,
                inn: document.getElementById('inn').value,
                kpp: document.getElementById('kpp').value,
                website: document.getElementById('website').value,
                contact: document.getElementById('contact').value,
                industry: document.getElementById('industry').value,
                location: document.getElementById('location').value,
                employees: document.getElementById('employees').value,
                branches: document.getElementById('branches').value,
                parentCompany: document.getElementById('parentCompany').value,
                turnover: document.getElementById('turnover').value,
                itBudgetCurrent: document.getElementById('itBudgetCurrent').value,
                itBudgetLast: document.getElementById('itBudgetLast').value,
                itBudgetExternal: document.getElementById('itBudgetExternal').value,
                decisionMaker: document.getElementById('decisionMaker').value,
                status: document.getElementById('status').value
            };
            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST',
                    body: JSON.stringify(client),
                    headers: { 'Content-Type': 'application/json' }
                });
                clearForm();
                document.querySelector('.update-btn').outerHTML = `<button class="save-btn" onclick="saveClient()">Сохранить</button>`;
                alert('Клиент обновлён, нихуя себе!');
                loadClients();
            } catch (e) {
                console.error('Ошибка обновления:', e);
                alert('Не удалось обновить, пиздец где-то в коде!');
            }
        }

        function clearForm() {
            document.querySelectorAll('.left-frame input, .left-frame select').forEach(el => el.value = '');
        }

        function updateClientList(filteredClients = clients) {
            const clientList = document.getElementById('clientList');
            clientList.innerHTML = '';
            filteredClients.forEach((client, index) => {
                const progress = calculateProgress(client);
                const color = progress === 100 ? 'green' : progress >= 45 ? 'orange' : 'red';
                const item = document.createElement('div');
                item.className = 'client-item';
                item.innerHTML = `
                    ${client["Наименование Клиента"]} | ИНН: ${client["ИНН"]} 
                    <div class="progress-bar" style="background: ${color}; width: ${progress}%"></div>
                    <button onclick="editClient(${index})">Редактировать</button>
                `;
                clientList.appendChild(item);
            });
            updateSearchDropdown();
        }

        function calculateProgress(client) {
            const fields = Object.values(client);
            const filled = fields.filter(f => f !== '' && f !== null && f !== undefined).length;
            return Math.round((filled / fields.length) * 100);
        }

        function editClient(index) {
            const client = clients[index];
            document.getElementById('clientName').value = client["Наименование Клиента"] || '';
            document.getElementById('legalEntity').value = client["Юр. Лицо"] || '';
            document.getElementById('inn').value = client["ИНН"] || '';
            document.getElementById('kpp').value = client["КПП"] || '';
            document.getElementById('website').value = client["Сайт"] || '';
            document.getElementById('contact').value = client["Контактный телефон/e-mail"] || '';
            document.getElementById('industry').value = client["Отрасль"] || '';
            document.getElementById('location').value = client["Местонахождение"] || '';
            document.getElementById('employees').value = client["Количество Сотрудников"] || '';
            document.getElementById('branches').value = client["Филиальная Сеть (кол-во)"] || '';
            document.getElementById('parentCompany').value = client["Материнская Компания"] || '';
            document.getElementById('turnover').value = client["Годовой оборот (СР)"] || '';
            document.getElementById('itBudgetCurrent').value = client["ИТ Бюджет на нынешний год"] || '';
            document.getElementById('itBudgetLast').value = client["ИТ Бюджет на прошлый год"] || '';
            document.getElementById('itBudgetExternal').value = client["Бюджет ИТ Внешний"] || '';
            document.getElementById('decisionMaker').value = client["Предприятие Принятия Решений"] || '';
            document.getElementById('status').value = client["Статус"] || 'Холодный';
            document.querySelector('.save-btn').outerHTML = `<button class="update-btn" onclick="updateClient(${index})">Обновить</button>`;
        }

        function filterClients(filter) {
            let filtered = [];
            if (filter === 'Все') filtered = clients;
            else if (filter === 'Не заполненные') filtered = clients.filter(c => calculateProgress(c) < 100);
            else filtered = clients.filter(c => c["Статус"] === filter);
            updateClientList(filtered);
        }

        function updateSearchDropdown() {
            const search = document.getElementById('searchClient');
            search.innerHTML = '<option value="">Выберите клиента</option>';
            clients.forEach(client => {
                const option = document.createElement('option');
                option.value = client["Наименование Клиента"];
                option.textContent = client["Наименование Клиента"];
                search.appendChild(option);
            });
        }

        function searchByName() {
            const name = document.getElementById('searchClient').value;
            if (name) {
                const filtered = clients.filter(c => c["Наименование Клиента"] === name);
                updateClientList(filtered);
            }
        }

        function toggleTheme() {
            document.body.classList.toggle('night');
            document.querySelector('.right-frame').classList.toggle('night');
            document.querySelectorAll('.client-item').forEach(item => item.classList.toggle('night'));
        }

        loadClients();
    </script>
</body>
</html>
