<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ok_Pro - расчет ПВХ окон</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --orange: #FF9800;
            --light-orange: #FFE0B2;
            --dark-gray: #455A64;
            --gray: #78909C;
            --light-gray: #ECEFF1;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Roboto', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
        }
        
        .app-container {
            max-width: 100%;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            position: relative;
            padding-bottom: 70px;
        }
        
        .header {
            background: var(--dark-gray);
            color: white;
            padding: 16px;
            text-align: center;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .logo {
            font-weight: bold;
            font-size: 24px;
            color: var(--orange);
        }
        
        .tabs {
            display: flex;
            background: var(--gray);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .tab {
            flex: 1;
            padding: 16px;
            text-align: center;
            background: var(--gray);
            color: white;
            cursor: pointer;
            transition: background 0.3s;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
            font-size: 14px;
        }
        
        .tab i {
            font-size: 20px;
        }
        
        .tab.active {
            background: var(--orange);
            font-weight: bold;
        }
        
        .tab-content {
            display: none;
            padding: 16px;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .calculator-form {
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 16px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark-gray);
        }
        
        .form-group select, .form-group input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: white;
            font-size: 16px;
        }
        
        .size-inputs {
            display: flex;
            gap: 12px;
        }
        
        .size-input {
            flex: 1;
        }
        
        .window-preview {
            margin: 20px 0;
            text-align: center;
            height: 220px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--light-gray);
            border-radius: 12px;
            padding: 10px;
            box-shadow: inset 0 0 5px rgba(0,0,0,0.1);
        }
        
        .window-svg {
            max-width: 100%;
            max-height: 200px;
        }
        
        .result-box {
            background: var(--light-orange);
            padding: 20px;
            border-radius: 12px;
            margin: 20px 0;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .result-price {
            font-size: 28px;
            font-weight: bold;
            color: var(--dark-gray);
            margin: 10px 0;
        }
        
        .service-list {
            list-style: none;
            margin-top: 20px;
        }
        
        .service-item {
            padding: 16px;
            border-bottom: 1px solid #ddd;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: background 0.3s;
        }
        
        .service-item:hover {
            background: var(--light-gray);
        }
        
        .service-item i {
            color: var(--orange);
            font-size: 20px;
            margin-right: 10px;
        }
        
        .service-info {
            display: flex;
            align-items: center;
        }
        
        .service-price {
            font-weight: bold;
            color: var(--dark-gray);
        }
        
        .contact-info {
            padding: 20px;
            background: var(--light-gray);
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .contact-info p {
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .contact-info i {
            color: var(--orange);
            width: 24px;
        }
        
        .btn {
            display: block;
            width: 100%;
            padding: 16px;
            background: var(--orange);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 20px;
            transition: background 0.3s;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .btn:hover {
            background: #F57C00;
        }
        
        .social-icons {
            display: flex;
            justify-content: center;
            gap: 16px;
            margin-top: 30px;
        }
        
        .social-icon {
            width: 50px;
            height: 50px;
            background: var(--dark-gray);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            transition: background 0.3s;
        }
        
        .social-icon:hover {
            background: var(--orange);
            transform: scale(1.1);
        }
        
        .sash-config {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-top: 12px;
        }
        
        .sash-option {
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }
        
        .sash-option.selected {
            border-color: var(--orange);
            background-color: var(--light-orange);
            transform: scale(1.05);
        }
        
        .sash-option i {
            font-size: 24px;
            color: var(--dark-gray);
        }
        
        .sash-layout {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-top: 12px;
        }
        
        .layout-option {
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }
        
        .layout-option.selected {
            border-color: var(--orange);
            background-color: var(--light-orange);
        }
        
        .layout-preview {
            width: 100%;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .layout-preview svg {
            max-width: 100%;
            max-height: 70px;
        }
        
        .section-title {
            font-size: 20px;
            color: var(--dark-gray);
            margin: 20px 0 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--orange);
        }
        
        .price-details {
            font-size: 14px;
            color: var(--dark-gray);
            margin-top: 10px;
            text-align: left;
        }
        
        .price-details div {
            margin-bottom: 5px;
        }
        
        .surcharge-info {
            color: #d32f2f;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="header">
            <div class="logo">Ok_Pro</div>
            <h1>Расчет стоимости ПВХ окон</h1>
        </div>
        
        <div class="tabs">
            <div class="tab active" data-tab="calculator">
                <i class="fas fa-calculator"></i>
                <span>Калькулятор</span>
            </div>
            <div class="tab" data-tab="services">
                <i class="fas fa-concierge-bell"></i>
                <span>Услуги</span>
            </div>
            <div class="tab" data-tab="contacts">
                <i class="fas fa-address-book"></i>
                <span>Контакты</span>
            </div>
        </div>
        
        <!-- Вкладка калькулятора -->
        <div class="tab-content active" id="calculator">
            <div class="calculator-form">
                <div class="form-group">
                    <label><i class="fas fa-layer-group"></i> Тип стеклопакета</label>
                    <select id="glass-type">
                        <option value="24">24 мм (однокамерный)</option>
                        <option value="32">32 мм (двухкамерный)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-border-style"></i> Количество створок</label>
                    <select id="sash-count">
                        <option value="1">Одностворчатое</option>
                        <option value="2">Двухстворчатое</option>
                        <option value="3">Трехстворчатое</option>
                    </select>
                </div>
                
                <div class="form-group" id="sash-layout-container" style="display: none;">
                    <label><i class="fas fa-th"></i> Расположение створок</label>
                    <div class="sash-layout" id="sash-layout">
                        <!-- Динамически заполнится в зависимости от выбора -->
                    </div>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-door-open"></i> Тип открывания</label>
                    <select id="opening-type">
                        <option value="fixed">Глухое</option>
                        <option value="swing">Поворотное</option>
                        <option value="tilt">Поворотно-откидное</option>
                        <option value="transom">Фрамужное</option>
                    </select>
                </div>
                
                <div class="form-group" id="sash-position-container" style="display: none;">
                    <label><i class="fas fa-arrows-alt-h"></i> Расположение открывания</label>
                    <div class="sash-config">
                        <div class="sash-option" data-value="left">
                            <i class="fas fa-arrow-left"></i>
                            <div>Слева</div>
                        </div>
                        <div class="sash-option" data-value="right">
                            <i class="fas fa-arrow-right"></i>
                            <div>Справа</div>
                        </div>
                    </div>
                </div>
                
                <div class="form-group">
                    <label><i class="fas fa-ruler-combined"></i> Размеры (мм)</label>
                    <div class="size-inputs">
                        <div class="size-input">
                            <input type="number" id="width" placeholder="Ширина" min="400" max="3000">
                        </div>
                        <div class="size-input">
                            <input type="number" id="height" placeholder="Высота" min="400" max="3000">
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="window-preview">
                <svg class="window-svg" id="window-svg" viewBox="0 0 300 200"></svg>
            </div>
            
            <div class="result-box">
                <p>Примерная стоимость:</p>
                <div class="result-price" id="result-price">0 руб.</div>
                <div class="price-details" id="price-details"></div>
                <p>Точную стоимость уточняйте у менеджера</p>
            </div>
            
            <button class="btn"><i class="fas fa-check-circle"></i> Заказать расчет</button>
        </div>
        
        <!-- Вкладка услуг -->
        <div class="tab-content" id="services">
            <h2 class="section-title"><i class="fas fa-concierge-bell"></i> Наши услуги</h2>
            
            <ul class="service-list">
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-window-restore"></i>
                        <span>Замена стеклопакета</span>
                    </div>
                    <div class="service-price">от 4500 руб.</div>
                </li>
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-cog"></i>
                        <span>Замена фурнитуры</span>
                    </div>
                    <div class="service-price">от 2500 руб.</div>
                </li>
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-border-style"></i>
                        <span>Замена резинок</span>
                    </div>
                    <div class="service-price">от 2000 руб.</div>
                </li>
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-tools"></i>
                        <span>Ремонт оконных конструкций</span>
                    </div>
                    <div class="service-price">от 1500 руб.</div>
                </li>
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-tint-slash"></i>
                        <span>Изготовление отливов</span>
                    </div>
                    <div class="service-price">индивидуальный расчет</div>
                </li>
                <li class="service-item">
                    <div class="service-info">
                        <i class="fas fa-hammer"></i>
                        <span>Демонтаж/монтаж оконных конструкций</span>
                    </div>
                    <div class="service-price">индивидуальный расчет</div>
                </li>
            </ul>
            
            <button class="btn"><i class="fas fa-clipboard-list"></i> Заказать услугу</button>
        </div>
        
        <!-- Вкладка контактов -->
        <div class="tab-content" id="contacts">
            <h2 class="section-title"><i class="fas fa-address-book"></i> Контакты</h2>
            
            <div class="contact-info">
                <p>
                    <i class="fas fa-map-marker-alt"></i>
                    <strong>Адрес:</strong> г.Пермь, ул.Воронежская 58 к12
                </p>
                <p>
                    <i class="fas fa-phone"></i>
                    <strong>Телефон:</strong> 8 (922) 309-63-73
                </p>
                <p>
                    <i class="fas fa-clock"></i>
                    <strong>Режим работы:</strong> Пн-Пт: 9:00-18:00, Сб: 10:00-15:00
                </p>
            </div>
            
            <div class="social-icons">
                <div class="social-icon"><i class="fab fa-vk"></i></div>
                <div class="social-icon"><i class="fab fa-instagram"></i></div>
                <div class="social-icon"><i class="fab fa-facebook-f"></i></div>
                <div class="social-icon"><i class="fab fa-whatsapp"></i></div>
            </div>
            
            <button class="btn"><i class="fas fa-phone-alt"></i> Позвонить нам</button>
        </div>
    </div>
 
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Переключение вкладок
            const tabs = document.querySelectorAll('.tab');
            const tabContents = document.querySelectorAll('.tab-content');
            
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const tabId = tab.getAttribute('data-tab');
                    
                    // Убираем активный класс у всех вкладок и контента
                    tabs.forEach(t => t.classList.remove('active'));
                    tabContents.forEach(c => c.classList.remove('active'));
                    
                    // Добавляем активный класс к выбранной вкладке и контенту
                    tab.classList.add('active');
                    document.getElementById(tabId).classList.add('active');
                });
            });
            
            // Элементы для расчета
            const glassType = document.getElementById('glass-type');
            const sashCount = document.getElementById('sash-count');
            const sashLayoutContainer = document.getElementById('sash-layout-container');
            const sashLayout = document.getElementById('sash-layout');
            const openingType = document.getElementById('opening-type');
            const sashPositionContainer = document.getElementById('sash-position-container');
            const sashOptions = document.querySelectorAll('.sash-option');
            const widthInput = document.getElementById('width');
            const heightInput = document.getElementById('height');
            const resultPrice = document.getElementById('result-price');
            const priceDetails = document.getElementById('price-details');
            const windowSvg = document.getElementById('window-svg');
            
            // Текущая конфигурация
            let currentConfig = {
                glassType: '24',
                sashCount: '1',
                sashLayout: 'all', // all, left, right, left-right, left-middle, right-middle, left-right-middle
                openingType: 'fixed',
                sashPosition: 'right',
                width: 0,
                height: 0
            };
            
            // Цены за м² в зависимости от типа открывания и стеклопакета
            const prices = {
                'fixed': { '24': 3921, '32': 4622 },
                'swing': { '24': 5302, '32': 5670 },
                'tilt': { '24': 5650, '32': 5784 },
                'transom': { '24': 6500, '32': 7000 }
            };
            
            // Варианты расположения створок
            const layoutOptions = {
                '1': [
                    { id: 'all', name: 'Одна створка', icon: createSingleSashSVG('all') }
                ],
                '2': [
                    { id: 'all', name: 'Две створки', icon: createDoubleSashSVG('all') },
                    { id: 'left', name: 'Только левая', icon: createDoubleSashSVG('left') },
                    { id: 'right', name: 'Только правая', icon: createDoubleSashSVG('right') },
                    { id: 'none', name: 'Без створок', icon: createDoubleSashSVG('none') }
                ],
                '3': [
                    { id: 'all', name: 'Три створки', icon: createTripleSashSVG('all') },
                    { id: 'left-right', name: 'Левая и правая', icon: createTripleSashSVG('left-right') },
                    { id: 'left-middle', name: 'Левая и средняя', icon: createTripleSashSVG('left-middle') },
                    { id: 'right-middle', name: 'Правая и средняя', icon: createTripleSashSVG('right-middle') },
                    { id: 'left', name: 'Только левая', icon: createTripleSashSVG('left') },
                    { id: 'right', name: 'Только правая', icon: createTripleSashSVG('right') },
                    { id: 'middle', name: 'Только средняя', icon: createTripleSashSVG('middle') },
                    { id: 'none', name: 'Без створок', icon: createTripleSashSVG('none') }
                ]
            };
            
            // Функции для создания SVG превью вариантов створок
            function createSingleSashSVG(type) {
                const svgNS = "http://www.w3.org/2000/svg";
                const svg = document.createElementNS(svgNS, "svg");
                svg.setAttribute("viewBox", "0 0 100 70");
                
                // Рамка
                const frame = document.createElementNS(svgNS, "rect");
                frame.setAttribute("x", "5");
                frame.setAttribute("y", "5");
                frame.setAttribute("width", "90");
                frame.setAttribute("height", "60");
                frame.setAttribute("fill", "none");
                frame.setAttribute("stroke", "#455A64");
                frame.setAttribute("stroke-width", "2");
                svg.appendChild(frame);
                
                if (type === 'all') {
                    const sash = document.createElementNS(svgNS, "rect");
                    sash.setAttribute("x", "10");
                    sash.setAttribute("y", "10");
                    sash.setAttribute("width", "80");
                    sash.setAttribute("height", "50");
                    sash.setAttribute("fill", "#B3E5FC");
                    sash.setAttribute("stroke", "#29B6F6");
                    sash.setAttribute("stroke-width", "1");
                    svg.appendChild(sash);
                }
                
                return svg;
            }
            
            function createDoubleSashSVG(type) {
                const svgNS = "http://www.w3.org/2000/svg";
                const svg = document.createElementNS(svgNS, "svg");
                svg.setAttribute("viewBox", "0 0 100 70");
                
                // Рамка
                const frame = document.createElementNS(svgNS, "rect");
                frame.setAttribute("x", "5");
                frame.setAttribute("y", "5");
                frame.setAttribute("width", "90");
                frame.setAttribute("height", "60");
                frame.setAttribute("fill", "none");
                frame.setAttribute("stroke", "#455A64");
                frame.setAttribute("stroke-width", "2");
                svg.appendChild(frame);
                
                // Импост
                const impost = document.createElementNS(svgNS, "line");
                impost.setAttribute("x1", "50");
                impost.setAttribute("y1", "5");
                impost.setAttribute("x2", "50");
                impost.setAttribute("y2", "65");
                impost.setAttribute("stroke", "#455A64");
                impost.setAttribute("stroke-width", "2");
                svg.appendChild(impost);
                
                // Левая створка
                if (type === 'all' || type === 'left') {
                    const leftSash = document.createElementNS(svgNS, "rect");
                    leftSash.setAttribute("x", "10");
                    leftSash.setAttribute("y", "10");
                    leftSash.setAttribute("width", "35");
                    leftSash.setAttribute("height", "50");
                    leftSash.setAttribute("fill", "#B3E5FC");
                    leftSash.setAttribute("stroke", "#29B6F6");
                    leftSash.setAttribute("stroke-width", "1");
                    svg.appendChild(leftSash);
                }
                
                // Правая створка
                if (type === 'all' || type === 'right') {
                    const rightSash = document.createElementNS(svgNS, "rect");
                    rightSash.setAttribute("x", "55");
                    rightSash.setAttribute("y", "10");
                    rightSash.setAttribute("width", "35");
                    rightSash.setAttribute("height", "50");
                    rightSash.setAttribute("fill", "#B3E5FC");
                    rightSash.setAttribute("stroke", "#29B6F6");
                    rightSash.setAttribute("stroke-width", "1");
                    svg.appendChild(rightSash);
                }
                
                return svg;
            }
            
            function createTripleSashSVG(type) {
                const svgNS = "http://www.w3.org/2000/svg";
                const svg = document.createElementNS(svgNS, "svg");
                svg.setAttribute("viewBox", "0 0 100 70");
                
                // Рамка
                const frame = document.createElementNS(svgNS, "rect");
                frame.setAttribute("x", "5");
                frame.setAttribute("y", "5");
                frame.setAttribute("width", "90");
                frame.setAttribute("height", "60");
                frame.setAttribute("fill", "none");
                frame.setAttribute("stroke", "#455A64");
                frame.setAttribute("stroke-width", "2");
                svg.appendChild(frame);
                
                // Импосты
                const impost1 = document.createElementNS(svgNS, "line");
                impost1.setAttribute("x1", "35");
                impost1.setAttribute("y1", "5");
                impost1.setAttribute("x2", "35");
                impost1.setAttribute("y2", "65");
                impost1.setAttribute("stroke", "#455A64");
                impost1.setAttribute("stroke-width", "2");
                svg.appendChild(impost1);
                
                const impost2 = document.createElementNS(svgNS, "line");
                impost2.setAttribute("x1", "65");
                impost2.setAttribute("y1", "5");
                impost2.setAttribute("x2", "65");
                impost2.setAttribute("y2", "65");
                impost2.setAttribute("stroke", "#455A64");
                impost2.setAttribute("stroke-width", "2");
                svg.appendChild(impost2);
                
                // Левая створка
                if (type === 'all' || type === 'left' || type === 'left-right' || type === 'left-middle') {
                    const leftSash = document.createElementNS(svgNS, "rect");
                    leftSash.setAttribute("x", "10");
                    leftSash.setAttribute("y", "10");
                    leftSash.setAttribute("width", "20");
                    leftSash.setAttribute("height", "50");
                    leftSash.setAttribute("fill", '#B3E5FC');
                    leftSash.setAttribute("stroke", "#29B6F6");
                    leftSash.setAttribute("stroke-width", "1");
                    svg.appendChild(leftSash);
                }
                
                // Средняя створка
                if (type === 'all' || type === 'middle' || type === 'left-middle' || type === 'right-middle') {
                    const middleSash = document.createElementNS(svgNS, "rect");
                    middleSash.setAttribute("x", "40");
                    middleSash.setAttribute("y", "10");
                    middleSash.setAttribute("width", "20");
                    middleSash.setAttribute("height", "50");
                    middleSash.setAttribute("fill", '#B3E5FC');
                    middleSash.setAttribute("stroke", "#29B6F6");
                    middleSash.setAttribute("stroke-width", "1");
                    svg.appendChild(middleSash);
                }
                
                // Правая створка
                if (type === 'all' || type === 'right' || type === 'left-right' || type === 'right-middle') {
                    const rightSash = document.createElementNS(svgNS, "rect");
                    rightSash.setAttribute("x", "70");
                    rightSash.setAttribute("y", "10");
                    rightSash.setAttribute("width", "20");
                    rightSash.setAttribute("height", "50");
                    rightSash.setAttribute("fill", '#B3E5FC');
                    rightSash.setAttribute("stroke", "#29B6F6");
                    rightSash.setAttribute("stroke-width", "1");
                    svg.appendChild(rightSash);
                }
                
                return svg;
            }
            
            // Функция для подсчета количества активных створок
            function countActiveSashes() {
                const count = parseInt(currentConfig.sashCount);
                const layout = currentConfig.sashLayout;
                
                if (count === 1) return 1;
                
                if (count === 2) {
                    if (layout === 'all') return 2;
                    if (layout === 'left' || layout === 'right') return 1;
                    return 0;
                }
                
                if (count === 3) {
                    if (layout === 'all') return 3;
                    if (layout === 'left-right' || layout === 'left-middle' || layout === 'right-middle') return 2;
                    if (layout === 'left' || layout === 'right' || layout === 'middle') return 1;
                    return 0;
                }
                
                return 0;
            }
            
            // Функция для расчета наценки на малые окна
            function calculateSmallWindowSurcharge(area, basePrice) {
                if (currentConfig.sashCount !== '1') return 0; // Наценка только для одностворчатых окон
                
                if (area >
= 0.2 && area < 0.5) {
                    return basePrice * 1.35; // +135% наценка
                } else if (area >= 0.5 && area < 1.0) {
                    return basePrice * 0.95; // +95% наценка
                }
                
                return 0;
            }
            
            // Обновление опций расположения створок
            function updateSashLayoutOptions() {
                const count = sashCount.value;
                currentConfig.sashCount = count;
                
                if (count === '1') {
                    sashLayoutContainer.style.display = 'none';
                    currentConfig.sashLayout = 'all';
                } else {
                    sashLayoutContainer.style.display = 'block';
                    sashLayout.innerHTML = '';
                    
                    layoutOptions[count].forEach(layout => {
                        const option = document.createElement('div');
                        option.className = 'layout-option';
                        option.setAttribute('data-value', layout.id);
                        
                        const preview = document.createElement('div');
                        preview.className = 'layout-preview';
                        preview.appendChild(layout.icon);
                        
                        const name = document.createElement('div');
                        name.textContent = layout.name;
                        
                        option.appendChild(preview);
                        option.appendChild(name);
                        
                        option.addEventListener('click', () => {
                            document.querySelectorAll('.layout-option').forEach(o => o.classList.remove('selected'));
                            option.classList.add('selected');
                            currentConfig.sashLayout = layout.id;
                            calculatePrice();
                            updateWindowPreview();
                        });
                        
                        sashLayout.appendChild(option);
                        
                        // Выбираем первый вариант по умолчанию
                        if (layout.id === 'all') {
                            option.classList.add('selected');
                            currentConfig.sashLayout = 'all';
                        }
                    });
                }
                
                calculatePrice();
                updateWindowPreview();
            }
            
            // Обработчики выбора расположения открывания
            sashOptions.forEach(option => {
                option.addEventListener('click', () => {
                    sashOptions.forEach(o => o.classList.remove('selected'));
                    option.classList.add('selected');
                    currentConfig.sashPosition = option.getAttribute('data-value');
                    updateWindowPreview();
                });
            });
            
            // Показ/скрытие опции выбора расположения открывания
            openingType.addEventListener('change', function() {
                const openingValue = this.value;
                currentConfig.openingType = openingValue;
                
                if (openingValue === 'fixed') {
                    sashPositionContainer.style.display = 'none';
                } else {
                    sashPositionContainer.style.display = 'block';
                }
                
                calculatePrice();
                updateWindowPreview();
            });
            
            // Функция расчета стоимости
            function calculatePrice() {
                const glassValue = glassType.value;
                const openingValue = openingType.value;
                const width = parseInt(widthInput.value) || 0;
                const height = parseInt(heightInput.value) || 0;
                
                currentConfig.glassType = glassValue;
                currentConfig.width = width;
                currentConfig.height = height;
                
                if (width > 0 && height > 0) {
                    const area = (width * height) / 1000000; // м²
                    const pricePerM2 = prices[openingValue][glassValue];
                    
                    // Базовая стоимость
                    let basePrice = Math.round(area * pricePerM2);
                    
                    // Подсчитываем количество активных створок
                    const activeSashes = countActiveSashes();
                    
                    // Наценка за створки (10% за каждую дополнительную створку)
                    let sashSurcharge = 0;
                    let sashDetails = '';
                    
                    if (activeSashes > 1) {
                        // Для первой створки нет наценки, для каждой последующей +10%
                        sashSurcharge = basePrice * 0.1 * (activeSashes - 1);
                        sashDetails = `<div>Наценка за ${activeSashes} створки: +${Math.round(sashSurcharge).toLocaleString('ru-RU')} руб. (10% за каждую дополнительную створку)</div>`;
                    }
                    
                    // Наценка за малые окна (только для одностворчатых)
                    let smallWindowSurcharge = 0;
                    let smallWindowDetails = '';
                    
                    if (currentConfig.sashCount === '1') {
                        smallWindowSurcharge = calculateSmallWindowSurcharge(area, basePrice);
                        
                        if (smallWindowSurcharge > 0) {
                            const surchargePercentage = area >= 0.2 && area < 0.5 ? 135 : 95;
                            smallWindowDetails = `<div class="surcharge-info">Наценка за малое окно (${area.toFixed(2)} м²): +${surchargePercentage}% = +${Math.round(smallWindowSurcharge).toLocaleString('ru-RU')} руб.</div>`;
                        }
                    }
                    
                    // Итоговая стоимость
                    const total = Math.round(basePrice + sashSurcharge + smallWindowSurcharge);
                    
                    // Формируем детализацию стоимости
                    let detailsHtml = `
                        <div>Площадь: ${area.toFixed(2)} м²</div>
                        <div>Базовая цена: ${Math.round(basePrice).toLocaleString('ru-RU')} руб.</div>
                    `;
                    
                    if (sashDetails) {
                        detailsHtml += sashDetails;
                    }
                    
                    if (smallWindowDetails) {
                        detailsHtml += smallWindowDetails;
                    }
                    
                    detailsHtml += `<div><strong>Итого: ${total.toLocaleString('ru-RU')} руб.</strong></div>`;
                    
                    resultPrice.textContent = total.toLocaleString('ru-RU') + ' руб.';
                    priceDetails.innerHTML = detailsHtml;
                } else {
                    resultPrice.textContent = '0 руб.';
                    priceDetails.innerHTML = '';
                }
            }
            
            // Функция обновления preview окна
            function updateWindowPreview() {
                const sashCountValue = parseInt(sashCount.value);
                const sashLayoutValue = currentConfig.sashLayout;
                const openingValue = openingType.value;
                const sashPosition = currentConfig.sashPosition;
                
                // Очищаем SVG
                windowSvg.innerHTML = '';
                
                // Рисуем внешнюю раму
                const frame = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                frame.setAttribute('x', '10');
                frame.setAttribute('y', '10');
                frame.setAttribute('width', '280');
                frame.setAttribute('height', '180');
                frame.setAttribute('fill', 'none');
                frame.setAttribute('stroke', '#455A64');
                frame.setAttribute('stroke-width', '5');
                windowSvg.appendChild(frame);
                
                if (sashCountValue === 1) {
                    drawSingleSashWindow(openingValue, sashPosition);
                } else if (sashCountValue === 2) {
                    drawDoubleSashWindow(sashLayoutValue, openingValue, sashPosition);
                } else if (sashCountValue === 3) {
                    drawTripleSashWindow(sashLayoutValue, openingValue, sashPosition);
                }
            }
            
            // Рисуем одностворчатое окно
            function drawSingleSashWindow(openingValue, sashPosition) {
                if (openingValue === 'fixed') {
                    // Глухое
                    const glass = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    glass.setAttribute('x', '15');
                    glass.setAttribute('y', '15');
                    glass.setAttribute('width', '270');
                    glass.setAttribute('height', '170');
                    glass.setAttribute('fill', '#B3E5FC');
                    glass.setAttribute('stroke', '#29B6F6');
                    glass.setAttribute('stroke-width', '2');
                    windowSvg.appendChild(glass);
                } else {
                    // Со створкой
                    const sash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    sash.setAttribute('x', '15');
                    sash.setAttribute('y', '15');
                    sash.setAttribute('width', '270');
                    sash.setAttribute('height', '170');
                    sash.setAttribute('fill', '#B3E5FC');
                    sash.setAttribute('stroke', '#29B6F6');
                    sash.setAttribute('stroke-width', '2');
                    windowSvg.appendChild(sash);
                    
                    // Ручка (расположение зависит от выбранной стороны)
                    const handleX = sashPosition === 'left' ? 40 : 250;
                    const handle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                    handle.setAttribute('cx', handleX);
                    handle.setAttribute('cy', '100');
                    handle.setAttribute('r', '5');
                    handle.setAttribute('fill', '#FF9800');
                    windowSvg.appendChild(handle);
                    
                    // Стрелка направления открывания
                    const arrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                    if (sashPosition === 'left') {
                        arrow.setAttribute('d', 'M40,100 L20,90 L20,110 Z');
                    } else {
                        arrow.setAttribute('d', 'M250,100 L270,90 L270,110 Z');
                    }
                    arrow.setAttribute('fill', '#FF9800');
                    windowSvg.appendChild(arrow);
                }
            }
            
            // Рисуем двухстворчатое окно
            function drawDoubleSashWindow(layoutValue, openingValue, sashPosition) {
                // Импост
                 const impost = document.createElementNS('http://www.w3.org/2000/svg', 'line');
                impost.setAttribute('x1', '150');
                impost.setAttribute('y1', '15');
                impost.setAttribute('x2', '150');
                impost.setAttribute('y2', '185');
                impost.setAttribute('stroke', '#455A64');
                impost.setAttribute('stroke-width', '3');
                windowSvg.appendChild(impost);
                
                // Левая створка
                if (layoutValue === 'all' || layoutValue === 'left') {
                    const leftSash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    leftSash.setAttribute('x', '15');
                    leftSash.setAttribute('y', '15');
                    leftSash.setAttribute('width', '130');
                    leftSash.setAttribute('height', '170');
                    leftSash.setAttribute('fill', '#B3E5FC');
                    leftSash.setAttribute('stroke', '#29B6F6');
                    leftSash.setAttribute('stroke-width', openingValue === 'fixed' ? '2' : '2');
                    windowSvg.appendChild(leftSash);
                    
                    if (openingValue !== 'fixed' && (layoutValue === 'all' || layoutValue === 'left')) {
                        // Ручка для левой створки
                        const leftHandleX = sashPosition === 'left' ? 40 : 130;
                        const leftHandle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                        leftHandle.setAttribute('cx', leftHandleX);
                        leftHandle.setAttribute('cy', '100');
                        leftHandle.setAttribute('r', '5');
                        leftHandle.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(leftHandle);
                        
                        // Стрелка для левой створки
                        const leftArrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                        if (sashPosition === 'left') {
                            leftArrow.setAttribute('d', 'M40,100 L20,90 L20,110 Z');
                        } else {
                            leftArrow.setAttribute('d', 'M130,100 L110,90 L110,110 Z');
                        }
                        leftArrow.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(leftArrow);
                    }
                }
                
                // Правая створка
                if (layoutValue === 'all' || layoutValue === 'right') {
                    const rightSash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    rightSash.setAttribute('x', '155');
                    rightSash.setAttribute('y', '15');
                    rightSash.setAttribute('width', '130');
                    rightSash.setAttribute('height', '170');
                    rightSash.setAttribute('fill', '#B3E5FC');
                    rightSash.setAttribute('stroke', '#29B6F6');
                    rightSash.setAttribute('stroke-width', openingValue === 'fixed' ? '2' : '2');
                    windowSvg.appendChild(rightSash);
                    
                    if (openingValue !== 'fixed' && (layoutValue === 'all' || layoutValue === 'right')) {
                        // Ручка для правой створки
                        const rightHandleX = sashPosition === 'left' ? 170 : 260;
                        const rightHandle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                        rightHandle.setAttribute('cx', rightHandleX);
                        rightHandle.setAttribute('cy', '100');
                        rightHandle.setAttribute('r', '5');
                        rightHandle.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(rightHandle);
                        
                        // Стрелка для правой створки
                        const rightArrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                        if (sashPosition === 'left') {
                            rightArrow.setAttribute('d', 'M170,100 L190,90 L190,110 Z');
                        } else {
                            rightArrow.setAttribute('d', 'M260,100 L280,90 L280,110 Z');
                        }
                        rightArrow.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(rightArrow);
                    }
                }
            }
            
            // Рисуем трехстворчатое окно
            function drawTripleSashWindow(layoutValue, openingValue, sashPosition) {
                // Импосты
                const impost1 = document.createElementNS('http://www.w3.org/2000/svg', 'line');
                impost1.setAttribute('x1', '110');
                impost1.setAttribute('y1', '15');
                impost1.setAttribute('x2', '110');
                impost1.setAttribute('y2', '185');
                impost1.setAttribute('stroke', '#455A64');
                impost1.setAttribute('stroke-width', '3');
                windowSvg.appendChild(impost1);
                
                const impost2 = document.createElementNS('http://www.w3.org/2000/svg', 'line');
                impost2.setAttribute('x1', '190');
                impost2.setAttribute('y1', '15');
                impost2.setAttribute('x2', '190');
                impost2.setAttribute('y2', '185');
                impost2.setAttribute('stroke', '#455A64');
                impost2.setAttribute('stroke-width', '3');
                windowSvg.appendChild(impost2);
                
                // Левая створка
                if (layoutValue === 'all' || layoutValue === 'left' || layoutValue === 'left-right' || layoutValue === 'left-middle') {
                    const leftSash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    leftSash.setAttribute('x', '15');
                    leftSash.setAttribute('y', '15');
                    leftSash.setAttribute('width', '90');
                    leftSash.setAttribute('height', '170');
                    leftSash.setAttribute('fill', '#B3E5FC');
                    leftSash.setAttribute('stroke', '#29B6F6');
                    leftSash.setAttribute('stroke-width', openingValue === 'fixed' ? '2' : '2');
                    windowSvg.appendChild(leftSash);
                    
                    if (openingValue !== 'fixed' && (layoutValue === 'all' || layoutValue === 'left' || layoutValue === 'left-right' || layoutValue === 'left-middle')) {
                        // Ручка для левой створки
                        const leftHandleX = sashPosition === 'left' ? 40 : 90;
                        const leftHandle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                        leftHandle.setAttribute('cx', leftHandleX);
                        leftHandle.setAttribute('cy', '100');
                        leftHandle.setAttribute('r', '5');
                        leftHandle.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(leftHandle);
                        
                        // Стрелка для левой створки
                        const leftArrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                        if (sashPosition === 'left') {
                            leftArrow.setAttribute('d', 'M40,100 L20,90 L20,110 Z');
                        } else {
                            leftArrow.setAttribute('d', 'M90,100 L110,90 L110,110 Z');
                        }
                        leftArrow.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(leftArrow);
                    }
                }
                
                // Средняя створка
                if (layoutValue === 'all' || layoutValue === 'middle' || layoutValue === 'left-middle' || layoutValue === 'right-middle') {
                    const middleSash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    middleSash.setAttribute('x', '115');
                    middleSash.setAttribute('y', '15');
                    middleSash.setAttribute('width', '70');
                    middleSash.setAttribute('height', '170');
                    middleSash.setAttribute('fill', '#B3E5FC');
                    middleSash.setAttribute('stroke', '#29B6F6');
                    middleSash.setAttribute('stroke-width', openingValue === 'fixed' ? '2' : '2');
                    windowSvg.appendChild(middleSash);
                    
                    if (openingValue !== 'fixed' && (layoutValue === 'all' || layoutValue === 'middle' || layoutValue === 'left-middle' || layoutValue === 'right-middle')) {
                        // Ручка для средней створки
                        const middleHandleX = sashPosition === 'left' ? 130 : 160;
                        const middleHandle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                        middleHandle.setAttribute('cx', middleHandleX);
                        middleHandle.setAttribute('cy', '100');
                        middleHandle.setAttribute('r', '5');
                        middleHandle.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(middleHandle);
                        
                        // Стрелка для средней створки
                        const middleArrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                        if (sashPosition === 'left') {
                            middleArrow.setAttribute('d', 'M130,100 L110,90 L110,110 Z');
                        } else {
                            middleArrow.setAttribute('d', 'M160,100 L180,90 L180,110 Z');
                        }
                        middleArrow.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(middleArrow);
                    }
                }
                
                // Правая створка
                if (layoutValue === 'all' || layoutValue === 'right' || layoutValue === 'left-right' || layoutValue === 'right-middle') {
                    const rightSash = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                    rightSash.setAttribute('x', '195');
                    rightSash.setAttribute('y', '15');
                    rightSash.setAttribute('width', '90');
                    rightSash.setAttribute('height', '170');
                    rightSash.setAttribute('fill', '#B3E5FC');
                    rightSash.setAttribute('stroke', '#29B6F6');
                    rightSash.setAttribute('stroke-width', openingValue === 'fixed' ? '2' : '2');
                    windowSvg.appendChild(rightSash);
                    
                    if (openingValue !== 'fixed' && (layoutValue === 'all' || layoutValue === 'right' || layoutValue === 'left-right' || layoutValue === 'right-middle')) {
                        // Ручка для правой створки
                        const rightHandleX = sashPosition === 'left' ? 210 : 260;
                        const rightHandle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                        rightHandle.setAttribute('cx', rightHandleX);
                        rightHandle.setAttribute('cy', '100');
                        rightHandle.setAttribute('r', '5');
                        rightHandle.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(rightHandle);
                        
                        // Стрелка для правой створки
                        const rightArrow = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                        if (sashPosition === 'left') {
                            rightArrow.setAttribute('d', 'M210,100 L190,90 L190,110 Z');
                        } else {
                            rightArrow.setAttribute('d', 'M260,100 L280,90 L280,110 Z');
                        }
                        rightArrow.setAttribute('fill', '#FF9800');
                        windowSvg.appendChild(rightArrow);
                    }
                }
            }
            
            // Слушатели событий для элементов формы
            glassType.addEventListener('change', calculatePrice);
            sashCount.addEventListener('change', function() {
                currentConfig.sashCount = this.value;
                updateSashLayoutOptions();
                calculatePrice();
            });
            openingType.addEventListener('change', calculatePrice);
            widthInput.addEventListener('input', calculatePrice);
            heightInput.addEventListener('input', calculatePrice);
            
            // Инициализация
            document.querySelector('.sash-option[data-value="right"]').classList.add('selected');
            updateSashLayoutOptions();
        });
    </script>
 
</body>
</html>
