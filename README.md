<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Мій мобільний додаток</title>
    
    <script src="https://telegram.org/js/telegram-web-app.js"></script>

    <style>
        /* Стилі: кольори автоматично беруться з теми Telegram користувача */
        body {
            background-color: var(--tg-theme-bg-color, #ffffff);
            color: var(--tg-theme-text-color, #000000);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }

        .container {
            text-align: center;
        }

        h1 {
            font-size: 24px;
            margin-bottom: 10px;
        }

        p {
            font-size: 16px;
            opacity: 0.8;
            margin-bottom: 30px;
        }

        /* Кнопка теж підлаштовується під колір кнопок у Телеграмі */
        button {
            background-color: var(--tg-theme-button-color, #2481cc);
            color: var(--tg-theme-button-text-color, #ffffff);
            border: none;
            padding: 15px 30px;
            font-size: 18px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            transition: transform 0.1s ease;
        }

        button:active {
            transform: scale(0.95); /* Ефект натискання */
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>привіт, <span id="username">Друже</span>! 👋</h1>
        <p>Мій перший міні-додаток, створений на телефоні.</p>
        
        <button id="main-btn">Натисни мене!</button>
    </div>

    <script>
        // Ініціалізуємо Телеграм всередині нашого сайту
        const tg = window.Telegram.WebApp;
        
        // Кажемо Телеграму, що сайт завантажився і можна показувати додаток
        tg.ready();
        
        // Розгортаємо вікно додатка на максимум вгору
        tg.expand();

        // Перевіряємо, чи зайшов користувач саме з Телеграма
        if (tg.initDataUnsafe && tg.initDataUnsafe.user) {
            // Замінюємо слово "Друже" на реальне ім'я з Телеграм-профілю
            document.getElementById('username').innerText = tg.initDataUnsafe.user.first_name;
        }

        // Знаходимо нашу кнопку в коді
        const button = document.getElementById('main-btn');

        // Додаємо дію при натисканні на кнопку
        button.addEventListener('click', () => {
            // 1. Вібрація телефона (якщо телефон це підтримує)
            if (tg.HapticFeedback) {
                tg.HapticFeedback.impactOccurred('medium');
            }
            
            // 2. Спливаюче віконце Телеграму з повідомленням
            tg.showAlert('Привіт! Все працює ідеально! 🚀');
        });
    </script>
</body>
</html>
