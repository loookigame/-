<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Небоскребы · Сохранение</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
            user-select: none;
        }
        body {
            background: linear-gradient(145deg, #0B1A2E 0%, #1A2F3F 100%);
            min-height: 100vh;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 10px;
        }
        .game-window {
            max-width: 420px;
            width: 100%;
            background: #132433;
            border-radius: 36px;
            box-shadow: 0 25px 50px -8px rgba(0,0,0,0.8), inset 0 0 0 2px rgba(255,215,0,0.2);
            overflow: hidden;
            border: 1px solid #F4B64240;
            padding: 18px 15px 20px 15px;
        }
        .header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            gap: 8px;
        }
        .currency-card {
            background: #0D1C2B;
            border-radius: 60px;
            padding: 8px 18px;
            display: flex;
            align-items: center;
            gap: 8px;
            border: 1px solid #F4B64260;
            box-shadow: 0 4px 0 #0a141f;
            flex: 1;
            justify-content: center;
        }
        .currency-icon {
            font-size: 24px;
            filter: drop-shadow(0 2px 2px black);
        }
        .currency-value {
            font-weight: 800;
            font-size: 22px;
            color: white;
            text-shadow: 0 2px 3px black;
        }
        .currency-value.coins { color: #FFD966; }
        .currency-value.cash { color: #B3E0FF; }
        .elevator-shaft {
            background: #1E3347;
            border-radius: 30px;
            padding: 15px 12px;
            margin-bottom: 15px;
            border: 2px solid #F4B642;
            box-shadow: inset 0 -3px 0 #0F1E2C, 0 6px 0 #0F1E2C;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .elevator-door {
            background: #5C4E3D;
            width: 70px;
            height: 80px;
            border-radius: 20px;
            display: flex;
            flex-wrap: wrap;
            overflow: hidden;
            border: 3px solid #C9A34B;
            box-shadow: 0 5px 0 #6b4f2a;
            position: relative;
        }
        .door-left, .door-right {
            width: 50%;
            height: 100%;
            background: linear-gradient(145deg, #AA8E5C, #7B623C);
            transition: transform 0.2s;
            border: 1px solid #E3B160;
        }
        .door-left { border-radius: 15px 0 0 15px; }
        .door-right { border-radius: 0 15px 15px 0; }
        .elevator-info {
            flex: 1;
            color: white;
        }
        .elevator-floor {
            font-size: 36px;
            font-weight: 800;
            line-height: 1;
            background: #253B4B;
            display: inline-block;
            padding: 5px 20px;
            border-radius: 30px;
            margin-bottom: 6px;
            border: 1px solid #ffb347;
        }
        .btn-elevator {
            background: #F4B642;
            border: none;
            border-radius: 40px;
            padding: 10px 25px;
            font-weight: 800;
            color: #0B1A2E;
            box-shadow: 0 5px 0 #B87C1B;
            transition: 0.07s linear;
            font-size: 18px;
            width: 100%;
            cursor: pointer;
        }
        .btn-elevator:active {
            transform: translateY(4px);
            box-shadow: 0 1px 0 #B87C1B;
        }
        .floors-container {
            background: #10212E;
            border-radius: 30px;
            padding: 10px 8px;
            margin-bottom: 12px;
            max-height: 340px;
            overflow-y: auto;
            border: 2px solid #3D5A73;
            box-shadow: inset 0 2px 5px #00000050;
        }
        .floor-item {
            background: #1B3345;
            border-radius: 28px;
            margin-bottom: 8px;
            padding: 12px 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid #F4B642;
            box-shadow: 0 4px 0 #0e1b24;
            color: white;
        }
        .floor-left {
            display: flex;
            align-items: center;
            gap: 15px;
            flex: 2;
        }
        .floor-number-badge {
            background: #F4B642;
            color: #132433;
            font-weight: 900;
            width: 45px;
            height: 45px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            box-shadow: 0 4px 0 #b47d31;
        }
        .floor-name {
            font-weight: 700;
            font-size: 18px;
        }
        .floor-profit {
            background: #2C4C3E;
            padding: 5px 12px;
            border-radius: 30px;
            color: #CDFFCD;
            font-weight: 600;
            border: 1px solid #7AA67E;
        }
        .upgrade-btn {
            background: #EBB13C;
            border: none;
            border-radius: 30px;
            padding: 10px 18px;
            font-weight: 800;
            color: #1E2F3A;
            box-shadow: 0 4px 0 #9E741F;
            cursor: pointer;
            transition: 0.05s linear;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 5px;
            margin-left: 8px;
        }
        .upgrade-btn:active {
            transform: translateY(4px);
            box-shadow: 0 0 0 #9E741F;
        }
        .upgrade-btn:disabled {
            opacity: 0.4;
            transform: none;
            box-shadow: 0 4px 0 #9E741F;
            pointer-events: none;
        }
        .lemonade-stand {
            background: #2C3E50;
            border-radius: 30px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            border: 2px solid #FFC857;
            margin-top: 10px;
        }
        .manager-emoji {
            font-size: 48px;
            background: #445c6e;
            border-radius: 60px;
            padding: 5px;
        }
        .manager-info {
            flex: 1;
            color: white;
        }
        .manager-name {
            font-weight: 800;
            font-size: 20px;
        }
        .manager-earn {
            color: #FFD966;
            font-weight: 600;
        }
        .btn-manager {
            background: #4CAF50;
            border: none;
            border-radius: 40px;
            padding: 12px 22px;
            font-weight: 800;
            color: white;
            box-shadow: 0 5px 0 #2d6e31;
            cursor: pointer;
            font-size: 16px;
        }
        .btn-manager:active { transform: translateY(4px); box-shadow: none; }
        .banner-ad {
            background: #281f0f;
            border-radius: 18px;
            padding: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 15px 0 5px;
            border: 1px dashed #F4B642;
        }
        .btn-ad {
            background: #4a6fa5;
            border: none;
            border-radius: 30px;
            padding: 8px 20px;
            font-weight: 700;
            color: white;
            box-shadow: 0 3px 0 #1e3a5f;
            cursor: pointer;
        }
        .save-panel {
            display: flex;
            gap: 8px;
            margin-top: 12px;
            justify-content: center;
        }
        .save-btn {
            background: #3D5A73;
            border: none;
            border-radius: 30px;
            padding: 10px 18px;
            font-weight: 600;
            color: white;
            box-shadow: 0 3px 0 #1e3347;
            cursor: pointer;
            font-size: 14px;
            flex: 1;
        }
        .save-btn.reset {
            background: #8B3A3A;
            box-shadow: 0 3px 0 #5f2929;
        }
        .save-btn:hover {
            filter: brightness(1.1);
        }
        .save-status {
            text-align: center;
            color: #F4B642;
            font-size: 12px;
            margin-top: 8px;
            min-height: 18px;
        }
    </style>
</head>
<body>
<div class="game-window">
    <!-- Верхняя панель валют -->
    <div class="header">
        <div class="currency-card"><span class="currency-icon">💰</span><span class="currency-value coins" id="coinDisplay">200</span></div>
        <div class="currency-card"><span class="currency-icon">💎</span><span class="currency-value cash" id="cashDisplay">5</span></div>
    </div>

    <!-- Лифт -->
    <div class="elevator-shaft">
        <div class="elevator-door">
            <div class="door-left" id="doorLeft"></div>
            <div class="door-right" id="doorRight"></div>
        </div>
        <div class="elevator-info">
            <div class="elevator-floor" id="currentFloorDisplay">1</div>
            <button class="btn-elevator" id="callElevatorBtn">🚪 Купить этаж (250💰)</button>
        </div>
    </div>

    <!-- Список этажей -->
    <div class="floors-container" id="floorList"></div>

    <!-- Менеджер (Продавец лимонада) -->
    <div class="lemonade-stand">
        <div class="manager-emoji">🍋</div>
        <div class="manager-info">
            <div class="manager-name">Лимонадный Джо</div>
            <div class="manager-earn" id="managerProfit">+5💰/мин</div>
        </div>
        <button class="btn-manager" id="hireManagerBtn">Нанять (5💎)</button>
    </div>

    <!-- Симуляция рекламного бонуса -->
    <div class="banner-ad">
        <span style="color: #FFD966;">📺 Бонус за рекламу</span>
        <button class="btn-ad" id="adBonusBtn">➕ x2 доход (30 сек)</button>
    </div>

    <!-- Панель сохранения -->
    <div class="save-panel">
        <button class="save-btn" id="saveGameBtn">💾 Сохранить</button>
        <button class="save-btn reset" id="resetGameBtn">🔄 Сброс</button>
    </div>
    <div class="save-status" id="saveStatus"></div>
</div>

<script>
    (function() {
        // --- СОСТОЯНИЕ ИГРЫ ---
        let gameState = {
            coins: 200,
            cash: 5,
            currentElevatorFloor: 1,
            managerHired: false,
            adMultiplier: 1,
            adTimer: 0,
            floors: [
                { id: 1, name: '🥐 Пекарня', level: 2, baseIncome: 8, multiplier: 1.0, business: 'food' },
                { id: 2, name: '👕 Магазин', level: 3, baseIncome: 12, multiplier: 1.0, business: 'clothes' },
                { id: 3, name: '🎮 Комп. клуб', level: 5, baseIncome: 20, multiplier: 1.0, business: 'games' },
                { id: 4, name: '🍔 Фастфуд', level: 7, baseIncome: 30, multiplier: 1.0, business: 'food' },
                { id: 5, name: '💼 Офис', level: 9, baseIncome: 40, multiplier: 1.0, business: 'office' }
            ],
            nextId: 6
        };

        // Константы
        const UPGRADE_COST_COINS = 80;
        const MANAGER_COST = 5;
        const NEW_FLOOR_COST = 250;
        const SAVE_KEY = 'neboMobiSave';

        // --- ФУНКЦИИ СОХРАНЕНИЯ ---
        function saveGame(showMessage = true) {
            try {
                // Сохраняем всё состояние, кроме функций (их нет)
                const saveData = {
                    coins: gameState.coins,
                    cash: gameState.cash,
                    currentElevatorFloor: gameState.currentElevatorFloor,
                    managerHired: gameState.managerHired,
                    adMultiplier: gameState.adMultiplier,
                    adTimer: gameState.adTimer,
                    floors: gameState.floors,
                    nextId: gameState.nextId
                };
                localStorage.setItem(SAVE_KEY, JSON.stringify(saveData));
                if (showMessage) {
                    document.getElementById('saveStatus').textContent = '✅ Игра сохранена';
                    setTimeout(() => {
                        document.getElementById('saveStatus').textContent = '';
                    }, 2000);
                }
            } catch (e) {
                console.error('Ошибка сохранения:', e);
                document.getElementById('saveStatus').textContent = '❌ Ошибка сохранения';
            }
        }

        function loadGame() {
            try {
                const saved = localStorage.getItem(SAVE_KEY);
                if (!saved) {
                    document.getElementById('saveStatus').textContent = 'Нет сохранения';
                    return false;
                }

                const loadedState = JSON.parse(saved);
                
                // Восстанавливаем состояние
                gameState.coins = loadedState.coins ?? 200;
                gameState.cash = loadedState.cash ?? 5;
                gameState.currentElevatorFloor = loadedState.currentElevatorFloor ?? 1;
                gameState.managerHired = loadedState.managerHired ?? false;
                gameState.adMultiplier = loadedState.adMultiplier ?? 1;
                gameState.adTimer = loadedState.adTimer ?? 0;
                gameState.floors = loadedState.floors ?? [];
                gameState.nextId = loadedState.nextId ?? 6;

                // Обновим менеджера в интерфейсе
                if (gameState.managerHired) {
                    document.getElementById('hireManagerBtn').disabled = true;
                    document.getElementById('hireManagerBtn').innerText = 'Нанят ✅';
                } else {
                    document.getElementById('hireManagerBtn').disabled = false;
                    document.getElementById('hireManagerBtn').innerText = 'Нанять (5💎)';
                }

                document.getElementById('saveStatus').textContent = '📂 Загружено';
                setTimeout(() => {
                    document.getElementById('saveStatus').textContent = '';
                }, 1500);

                return true;
            } catch (e) {
                console.error('Ошибка загрузки:', e);
                document.getElementById('saveStatus').textContent = '❌ Ошибка загрузки';
                return false;
            }
        }

        function resetGame() {
            if (confirm('Сбросить весь прогресс? Это удалит все этажи и валюту.')) {
                // Сбрасываем на начальное состояние
                gameState = {
                    coins: 200,
                    cash: 5,
                    currentElevatorFloor: 1,
                    managerHired: false,
                    adMultiplier: 1,
                    adTimer: 0,
                    floors: [
                        { id: 1, name: '🥐 Пекарня', level: 2, baseIncome: 8, multiplier: 1.0, business: 'food' },
                        { id: 2, name: '👕 Магазин', level: 3, baseIncome: 12, multiplier: 1.0, business: 'clothes' },
                        { id: 3, name: '🎮 Комп. клуб', level: 5, baseIncome: 20, multiplier: 1.0, business: 'games' },
                        { id: 4, name: '🍔 Фастфуд', level: 7, baseIncome: 30, multiplier: 1.0, business: 'food' },
                        { id: 5, name: '💼 Офис', level: 9, baseIncome: 40, multiplier: 1.0, business: 'office' }
                    ],
                    nextId: 6
                };
                
                // Обновляем интерфейс
                document.getElementById('hireManagerBtn').disabled = false;
                document.getElementById('hireManagerBtn').innerText = 'Нанять (5💎)';
                
                // Сохраняем сброс в localStorage
                saveGame(false);
                
                // Перерисовываем всё
                updateHeader();
                renderFloors();
                moveElevatorToFloor(gameState.currentElevatorFloor);
                
                document.getElementById('saveStatus').textContent = '🔄 Прогресс сброшен';
                setTimeout(() => {
                    document.getElementById('saveStatus').textContent = '';
                }, 2000);
            }
        }

        // Автосохранение каждые 10 секунд
        function setupAutosave() {
            setInterval(() => {
                saveGame(false);
            }, 10000);
        }

        // Сохраняем при закрытии вкладки (на всякий случай)
        window.addEventListener('beforeunload', () => {
            saveGame(false);
        });

        // --- ВСПОМОГАТЕЛЬНЫЕ ФУНКЦИИ ---
        function formatNumber(num) { return Math.floor(num); }

        function updateHeader() {
            document.getElementById('coinDisplay').innerText = formatNumber(gameState.coins);
            document.getElementById('cashDisplay').innerText = formatNumber(gameState.cash);
        }

        function animateElevatorDoors(open) {
            const left = document.getElementById('doorLeft');
            const right = document.getElementById('doorRight');
            if (open) {
                left.style.transform = 'translateX(-100%)';
                right.style.transform = 'translateX(100%)';
            } else {
                left.style.transform = 'translateX(0)';
                right.style.transform = 'translateX(0)';
            }
        }

        function moveElevatorToFloor(floorNumber) {
            gameState.currentElevatorFloor = floorNumber;
            document.getElementById('currentFloorDisplay').innerText = floorNumber;
            animateElevatorDoors(true);
            setTimeout(() => animateElevatorDoors(false), 800);
        }

        function renderFloors() {
            const container = document.getElementById('floorList');
            container.innerHTML = '';

            const sorted = [...gameState.floors].sort((a,b) => a.level - b.level);
            for (let floor of sorted) {
                const profit = Math.floor(floor.baseIncome * floor.multiplier);
                const div = document.createElement('div');
                div.className = 'floor-item';
                div.innerHTML = `
                    <div class="floor-left">
                        <span class="floor-number-badge">${floor.level}</span>
                        <div>
                            <div class="floor-name">${floor.name}</div>
                            <div class="floor-profit">💰 ${profit}/мин</div>
                        </div>
                    </div>
                    <button class="upgrade-btn" data-id="${floor.id}" ${gameState.coins < UPGRADE_COST_COINS ? 'disabled' : ''}>
                        ⬆️ Улучшить (${UPGRADE_COST_COINS}💰)
                    </button>
                `;
                container.appendChild(div);
            }

            document.querySelectorAll('.upgrade-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const id = Number(btn.dataset.id);
                    upgradeFloor(id);
                });
            });
        }

        function upgradeFloor(floorId) {
            const floor = gameState.floors.find(f => f.id === floorId);
            if (!floor) return;
            if (gameState.coins < UPGRADE_COST_COINS) {
                alert('❌ Не хватает монет!');
                return;
            }

            gameState.coins -= UPGRADE_COST_COINS;
            floor.multiplier = Math.min(3.0, floor.multiplier + 0.15);
            updateHeader();
            renderFloors();
            saveGame(false); // автосохранение после действия
        }

        function addNewFloor() {
            if (gameState.coins < NEW_FLOOR_COST) {
                alert('💰 Нужно больше монет для нового этажа!');
                return false;
            }

            gameState.coins -= NEW_FLOOR_COST;

            const businessNames = [
                '👨‍⚕️ Клиника', '👮 Полиция', '🎨 Галерея', '🛋️ Мебель', '💎 Банк', 
                '🍕 Пиццерия', '🐶 Зоомагазин', '📚 Библиотека', '🎰 Казино', '🚗 Автосалон'
            ];
            const randName = businessNames[Math.floor(Math.random() * businessNames.length)];
            const newLevel = gameState.floors.length > 0 ? Math.max(...gameState.floors.map(f => f.level)) + 2 : 2;
            const newBase = 25 + Math.floor(Math.random() * 40);

            const newFloor = {
                id: gameState.nextId++,
                name: randName,
                level: newLevel,
                baseIncome: newBase,
                multiplier: 1.0,
                business: 'mixed'
            };
            gameState.floors.push(newFloor);
            renderFloors();
            updateHeader();
            saveGame(false);
            return true;
        }

        function callElevatorAction() {
            const maxLevel = Math.max(...gameState.floors.map(f => f.level));
            const newFloorLevel = maxLevel + 1;

            const success = addNewFloor();
            if (success) {
                const newFloor = gameState.floors.find(f => f.level === newFloorLevel);
                if (newFloor) moveElevatorToFloor(newFloor.level);
                else moveElevatorToFloor(newFloorLevel);
            } else {
                animateElevatorDoors(true);
                setTimeout(() => animateElevatorDoors(false), 500);
            }
        }

        function hireManager() {
            if (gameState.managerHired) {
                alert('Джо уже работает на тебя!');
                return;
            }
            if (gameState.cash < MANAGER_COST) {
                alert('Не хватает баксов (💎). Копи баксы!');
                return;
            }
            gameState.cash -= MANAGER_COST;
            gameState.managerHired = true;
            updateHeader();
            document.getElementById('hireManagerBtn').disabled = true;
            document.getElementById('hireManagerBtn').innerText = 'Нанят ✅';
            saveGame(false);
            alert('🍋 Лимонадный Джо теперь приносит +5 монет каждую минуту!');
        }

        function collectTick() {
            let total = 0;
            for (let f of gameState.floors) {
                total += f.baseIncome * f.multiplier;
            }

            if (gameState.managerHired) total += 5;

            if (gameState.adTimer > 0) {
                total *= 2;
                gameState.adTimer -= 2;
                if (gameState.adTimer <= 0) {
                    gameState.adMultiplier = 1;
                }
            }

            gameState.coins += Math.floor(total);
            updateHeader();
        }

        function activateAdBonus() {
            if (gameState.adTimer > 0) {
                alert('Бонус уже активен!');
                return;
            }
            gameState.adTimer = 30;
            gameState.adMultiplier = 2;
            alert('🎁 Бонус активирован: доход x2 на 30 секунд!');
            document.getElementById('adBonusBtn').innerText = '✅ Активировано';
            setTimeout(() => {
                document.getElementById('adBonusBtn').innerText = '➕ x2 доход (30 сек)';
            }, 30000);
            saveGame(false);
        }

        // --- ИНИЦИАЛИЗАЦИЯ ---
        window.addEventListener('load', () => {
            // Пытаемся загрузить сохранение
            loadGame();

            // Обновляем интерфейс
            updateHeader();
            renderFloors();
            moveElevatorToFloor(gameState.currentElevatorFloor);

            // Назначаем обработчики
            document.getElementById('callElevatorBtn').addEventListener('click', callElevatorAction);
            document.getElementById('hireManagerBtn').addEventListener('click', hireManager);
            document.getElementById('adBonusBtn').addEventListener('click', activateAdBonus);
            document.getElementById('saveGameBtn').addEventListener('click', () => saveGame(true));
            document.getElementById('resetGameBtn').addEventListener('click', resetGame);

            // Запускаем игровой цикл
            setInterval(collectTick, 2000);
            setInterval(updateHeader, 1000);
            
            // Автосохранение по таймеру
            setupAutosave();
        });
    })();
</script>
</body>
</html>
