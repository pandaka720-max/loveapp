<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Для любимой 🩷</title>
    <!-- Telegram WebApp SDK -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        :root {
            --bg-color: #ffd6e0;
            --card-bg: rgba(255, 255, 255, 0.85);
            --text-color: #5c2231;
            --accent-color: #ff4d6d;
            --accent-hover: #ff758f;
            --shadow: 0 10px 30px rgba(255, 77, 109, 0.2);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #ffccd5 0%, #ffb3c1 50%, #ff8fa3 100%);
            color: var(--text-color);
            margin: 0;
            padding: 16px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            box-sizing: border-box;
            user-select: none;
            overflow-x: hidden;
            position: relative;
        }

        /* Анимация падающих / летающих сердечек на фоне */
        .heart-bg {
            position: fixed;
            top: -10vh;
            color: rgba(255, 255, 255, 0.6);
            font-size: 20px;
            user-select: none;
            pointer-events: none;
            animation: fall linear infinite;
            z-index: 0;
        }

        @keyframes fall {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 0.8;
            }
            100% {
                transform: translateY(115vh) rotate(360deg);
                opacity: 0.1;
            }
        }

        .container {
            width: 100%;
            max-width: 400px;
            display: flex;
            flex-direction: column;
            gap: 16px;
            z-index: 1;
        }

        .header h1 {
            font-size: 22px;
            margin: 8px 0 12px 0;
            color: #c9184a;
            text-align: center;
            text-shadow: 0 2px 4px rgba(255, 255, 255, 0.5);
        }

        .tabs {
            display: flex;
            gap: 6px;
            justify-content: center;
            background: rgba(255, 255, 255, 0.3);
            padding: 6px;
            border-radius: 16px;
            backdrop-filter: blur(8px);
        }

        .tab-btn {
            flex: 1;
            padding: 10px 4px;
            border: none;
            border-radius: 12px;
            background: transparent;
            color: var(--text-color);
            font-weight: 600;
            font-size: 13px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .tab-btn.active {
            background: #ffffff;
            color: var(--accent-color);
            box-shadow: var(--shadow);
            transform: scale(1.02);
        }

        .card {
            background: var(--card-bg);
            border-radius: 24px;
            overflow: hidden;
            box-shadow: var(--shadow);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.6);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding-bottom: 20px;
            transition: transform 0.3s ease;
        }

        .card img {
            width: 100%;
            height: 330px;
            object-fit: cover;
            border-bottom: 3px solid #ffccd5;
        }

        .card-text {
            padding: 18px 16px;
            font-size: 17px;
            text-align: center;
            line-height: 1.4;
            font-weight: 700;
            color: #800f2f;
            min-height: 55px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .action-btn {
            width: 88%;
            padding: 14px;
            border: none;
            border-radius: 16px;
            background: linear-gradient(135deg, #ff4d6d 0%, #ff758f 100%);
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 6px 16px rgba(255, 77, 109, 0.4);
            transition: all 0.2s ease;
        }

        .action-btn:active {
            transform: scale(0.96);
            background: var(--accent-hover);
        }
    </style>
</head>
<body>

<!-- Анимированные сердечки на фоне -->
<div id="hearts-container"></div>

<div class="container">
    <div class="header">
        <h1>Для моей любимой зайки 💖</h1>
    </div>

    <!-- Переключатели категорий -->
    <div class="tabs">
        <button class="tab-btn active" onclick="switchCategory('compliments', this)">Комплименты</button>
        <button class="tab-btn" onclick="switchCategory('care', this)">Забота</button>
        <button class="tab-btn" onclick="switchCategory('memories', this)">Воспоминания</button>
    </div>

    <!-- Карточка с контентом -->
    <div class="card">
        <img id="card-img" src="" alt="Фото">
        <div id="card-text" class="card-text">Загрузка...</div>
        <button class="action-btn" onclick="nextSlide()">Ещё 🩷</button>
    </div>
</div>

<script>
    const tg = window.Telegram.WebApp;
    tg.expand();

    // Генерация сердечек на фоне
    function createHearts() {
        const container = document.getElementById('hearts-container');
        const hearts = ['🩷', '💖', '💕', '💗', '🌸'];
        for (let i = 0; i < 15; i++) {
            const heart = document.createElement('div');
            heart.classList.add('heart-bg');
            heart.innerText = hearts[Math.floor(Math.random() * hearts.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
            heart.style.animationDelay = Math.random() * 5 + 's';
            heart.style.fontSize = (Math.random() * 10 + 15) + 'px';
            container.appendChild(heart);
        }
    }
    createHearts();

    // Ваши данные
    const DATA = {
        compliments: [
            { text: "Ты делаешь мой мир ярче просто тем, что ты есть 🩷", img: "photos/compliment1.jpg" },
            { text: "Ты самая лучшая девушка 🩷", img: "photos/compliment2.jpg" },
            { text: "Ты невероятно милая девочка 🩷", img: "photos/compliment3.jpg" },
            { text: "Ты самая красивая зайка 🩷", img: "photos/compliment4.jpg" },
            { text: "Ты мое солнышко, сияй ярче всех 🩷", img: "photos/compliment5.jpg" },
            { text: "У тебя очень красивая фигура 🩷", img: "photos/compliment6.jpg" },
            { text: "Я очень рад, что мы вместе 🩷", img: "photos/compliment7.jpg" },
            { text: "Ты делаешь мой день лучше 🩷", img: "photos/compliment8.jpg" },
            { text: "Пиши и звони в любое время — я всегда буду рад 🩷", img: "photos/compliment9.jpg" },
            { text: "Ты делаешь мою жизнь намного ярче и теплее 🩷", img: "photos/compliment10.jpg" },
            { text: "С тобой очень комфортно и весело проводить время 🩷", img: "photos/compliment11.jpg" },
            { text: "Мне очень нравится как ты смеёшься и мило улыбаешься 🩷", img: "photos/compliment12.jpg" }
        ],
        care: [
            { text: "Покушай и отдохни обязательно 🩷", img: "photos/zabota1.jpg" },
            { text: "Много не работай, тебе нельзя 🩷", img: "photos/zabota2.jpg" },
            { text: "Если что-то понадобится - говори, пиши, звони 🩷", img: "photos/zabota3.jpg" },
            { text: "Береги себя, моя кошечка 🩷", img: "photos/zabota4.jpg" },
            { text: "Пиши мне о любых проблемах, я всегда выслушаю 🩷", img: "photos/zabota5.jpg" },
            { text: "Не сиди до поздней ночи, а то не выспишься 🩷", img: "photos/zabota6.jpg" },
            { text: "Не нервничай по пустякам 🩷", img: "photos/zabota7.jpg" },
            { text: "Рассказывай как прошёл твой день, мне интересно 🩷", img: "photos/zabota8.jpg" }
        ],
        memories: [
            { text: "Помнишь, как мы весело гуляли? 🩷", img: "photos/love1.jpg" },
            { text: "Помнишь, как мы кушали шаурму на 8 марта? 🩷", img: "photos/love2.jpg" },
            { text: "Помнишь, как мы пошли смотреть на речку? Вот полностью обновленная и готовая **Mini App** версия вашего бота с нежно-розовым интерфейсом, летающими сердечками на фоне, красивыми карточками с эффектом размытия (Glassmorphic design) и полной сохранностью всех ваших текстовых сообщений и названий фото!

Интерфейс разделен на **Frontend (`index.html`)** и **Backend (`bot.py`)**.

---

### 1. `index.html` (Розовый Mini App с анимированными сердечками)

Загрузите этот файл и вашу папку `photos/` на любой веб-хостинг (например, **GitHub Pages**, **Vercel** или **Netlify**).

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Для любимой 🩷</title>
    <!-- Telegram WebApp SDK -->
    <script src="[https://telegram.org/js/telegram-web-app.js](https://telegram.org/js/telegram-web-app.js)"></script>
    <style>
        :root {
            --bg-color: #ffd6e0;
            --card-bg: rgba(255, 255, 255, 0.88);
            --text-color: #5c2231;
            --accent-color: #ff4d6d;
            --accent-hover: #ff758f;
            --shadow: 0 10px 30px rgba(255, 77, 109, 0.25);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #ffccd5 0%, #ffb3c1 50%, #ff8fa3 100%);
            color: var(--text-color);
            margin: 0;
            padding: 16px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            box-sizing: border-box;
            user-select: none;
            overflow-x: hidden;
            position: relative;
        }

        /* Анимация летающих сердечек на фоне */
        .heart-bg {
            position: fixed;
            top: -10vh;
            color: rgba(255, 255, 255, 0.65);
            font-size: 20px;
            user-select: none;
            pointer-events: none;
            animation: fall linear infinite;
            z-index: 0;
        }

        @keyframes fall {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 0.8;
            }
            100% {
                transform: translateY(115vh) rotate(360deg);
                opacity: 0.1;
            }
        }

        .container {
            width: 100%;
            max-width: 400px;
            display: flex;
            flex-direction: column;
            gap: 16px;
            z-index: 1;
        }

        .header h1 {
            font-size: 22px;
            margin: 8px 0 12px 0;
            color: #c9184a;
            text-align: center;
            text-shadow: 0 2px 4px rgba(255, 255, 255, 0.5);
        }

        .tabs {
            display: flex;
            gap: 6px;
            justify-content: center;
            background: rgba(255, 255, 255, 0.35);
            padding: 6px;
            border-radius: 16px;
            backdrop-filter: blur(8px);
        }

        .tab-btn {
            flex: 1;
            padding: 10px
