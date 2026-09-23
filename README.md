<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Для моей любимой 💖</title>
  <!-- Telegram Web App SDK -->
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #ffdde1 0%, #ee9ca7 100%);
      --pink-primary: #ff4b72;
      --pink-accent: #ff758c;
      --card-bg: rgba(255, 255, 255, 0.85);
      --text-color: #4a2c35;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      background: var(--bg-gradient);
      min-height: 100vh;
      color: var(--text-color);
      display: flex;
      flex-direction: column;
      overflow-x: hidden;
      position: relative;
    }

    /* Анимация летающих сердечек на фоне */
    .heart-bg {
      position: fixed;
      top: -10%;
      font-size: 20px;
      opacity: 0.6;
      animation: fall 7s linear infinite;
      z-index: 0;
      pointer-events: none;
    }

    @keyframes fall {
      0% {
        transform: translateY(0) rotate(0deg);
        opacity: 0.8;
      }
      100% {
        transform: translateY(110vh) rotate(360deg);
        opacity: 0;
      }
    }

    /* Верхняя шапка */
    header {
      text-align: center;
      padding: 15px 10px 5px;
      z-index: 1;
    }

    header h1 {
      font-size: 22px;
      color: #d6335c;
      text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.8);
    }

    /* Табы (Переключатели) */
    .tabs-container {
      display: flex;
      justify-content: space-around;
      background: rgba(255, 255, 255, 0.6);
      backdrop-filter: blur(8px);
      margin: 10px 15px;
      padding: 5px;
      border-radius: 25px;
      box-shadow: 0 4px 15px rgba(255, 75, 114, 0.15);
      z-index: 1;
    }

    .tab-btn {
      flex: 1;
      padding: 10px 5px;
      border: none;
      background: transparent;
      border-radius: 20px;
      font-size: 13px;
      font-weight: 600;
      color: #884b5e;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 5px;
    }

    .tab-btn.active {
      background: var(--pink-primary);
      color: white;
      box-shadow: 0 3px 10px rgba(255, 75, 114, 0.3);
      transform: scale(1.02);
    }

    /* Контент вкладок */
    .content {
      flex: 1;
      padding: 10px 15px 30px;
      z-index: 1;
    }

    .tab-content {
      display: none;
      animation: fadeIn 0.4s ease forwards;
    }

    .tab-content.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Карточки слайдов */
    .card-container {
      background: var(--card-bg);
      backdrop-filter: blur(10px);
      border-radius: 20px;
      padding: 15px;
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
      border: 1px solid rgba(255, 255, 255, 0.6);
      text-align: center;
    }

    .card-image-wrapper {
      width: 100%;
      height: 320px;
      border-radius: 15px;
      overflow: hidden;
      margin-bottom: 15px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      background: #ffd3dd;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .card-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.3s ease;
    }

    .card-text {
      font-size: 16px;
      font-weight: 600;
      line-height: 1.4;
      color: #5a2232;
      min-height: 48px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 15px;
    }

    /* Кнопка "Следующее" */
    .next-btn {
      width: 100%;
      padding: 12px;
      border: none;
      border-radius: 15px;
      background: linear-gradient(135deg, var(--pink-primary), var(--pink-accent));
      color: white;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(255, 75, 114, 0.3);
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }

    .next-btn:active {
      transform: scale(0.97);
    }
  </style>
</head>
<body>

  <!-- Фон с летающими сердечками -->
  <div id="hearts-container"></div>

  <header>
    <h1>Для моей любимой 💖</h1>
  </header>

  <!-- Меню Табов -->
  <div class="tabs-container">
    <button class="tab-btn active" onclick="switchTab('compliments')">
      <span>🌸</span> Комплименты
    </button>
    <button class="tab-btn" onclick="switchTab('care')">
      <span>🧸</span> Забота
    </button>
    <button class="tab-btn" onclick="switchTab('memories')">
      <span>📸</span> Память
    </button>
  </div>

  <!-- Контент -->
  <div class="content">

    <!-- Вкладка Комплименты -->
    <div id="tab-compliments" class="tab-content active">
      <div class="card-container">
        <div class="card-image-wrapper">
          <img id="img-compliments" class="card-image" src="" alt="Фото" />
        </div>
        <div id="text-compliments" class="card-text"></div>
        <button class="next-btn" onclick="nextSlide('compliments')">Еще комплимент 💕</button>
      </div>
    </div>

    <!-- Вкладка Забота -->
    <div id="tab-care" class="tab-content">
      <div class="card-container">
        <div class="card-image-wrapper">
          <img id="img-care" class="card-image" src="" alt="Фото" />
        </div>
        <div id="text-care" class="card-text"></div>
        <button class="next-btn" onclick="nextSlide('care')">Ещё забота 🌷</button>
      </div>
    </div>

    <!-- Вкладка Воспоминания -->
    <div id="tab-memories" class="tab-content">
      <div class="card-container">
        <div class="card-image-wrapper">
          <img id="img-memories" class="card-image" src="" alt="Фото" />
        </div>
        <div id="text-memories" class="card-text"></div>
        <button class="next-btn" onclick="nextSlide('memories')">Ещё воспоминание ✨</button>
      </div>
    </div>

  </div>

  <script>
    // Инициализация Telegram WebApp
    const tg = window.Telegram?.WebApp;
    if (tg) {
      tg.ready();
      tg.expand();
    }

    // Данные для слайдов
    const data = {
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
        { text: "Береги себя моя кошечка 🩷", img: "photos/zabota4.jpg" },
        { text: "Пиши мне о любых проблемах, я всегда выслушаю 🩷", img: "photos/zabota5.jpg" },
        { text: "Не сиди до поздней ночи, а то не выспишься 🩷", img: "photos/zabota6.jpg" },
        { text: "Не нервничай по пустякам 🩷", img: "photos/zabota7.jpg" },
        { text: "Рассказывай как прошёл твой день, мне интересно 🩷", img: "photos/zabota8.jpg" }
      ],
      memories: [
        { text: "Помнишь, как мы весело гуляли? 🩷", img: "photos/love1.jpg" },
        { text: "Помнишь, как мы кушали шаурму на 8 марта? 🩷", img: "photos/love2.jpg" },
        { text: "Помнишь, как мы пошли смотреть на речку? 🩷", img: "photos/love3.jpg" },
        { text: "Помнишь, когда ты подарила мне красивый браслетик? 🩷", img: "photos/love4.jpg" },
        { text: "Помнишь, когда мы вместе разукрашивали? 🩷", img: "photos/love5.jpg" },
        { text: "Помнишь, когда я тебя круто сфоткал на закате? 🩷", img: "photos/love6.jpg" },
        { text: "Помнишь, как мы гуляли зимой и ты рисовала сердечки? 🩷", img: "photos/love7.jpg" },
        { text: "Помнишь, когда ты поехала со мной, чтоб я постригся? 🩷", img: "photos/love8.jpg" },
        { text: "Помнишь, когда я подарил тебе самодельный букетик? 🩷", img: "photos/love9.jpg" },
        { text: "Помнишь, когда ты нацепила на меня заколки? 🩷", img: "photos/love10.jpg" },
        { text: "Помнишь, когда мы поехали покупать мне батник? 🩷", img: "photos/love11.jpg" },
        { text: "Помнишь, когда мы зимой грелись в шерифе? 🩷", img: "photos/love12.jpg" },
        { text: "Помнишь, когда мы гуляли в парке? 🩷", img: "photos/love13.jpg" },
        { text: "Помнишь, когда мы зимой встретили красивого котика? 🩷", img: "photos/love14.jpg" },
        { text: "Помнишь, когда мы зимой пошли покупать донеры? 🩷", img: "photos/love15.jpg" },
        { text: "Помнишь, как я привёз тебе павер, когда ты была на свадьбе? 🩷", img: "photos/love16.jpg" }
      ]
    };

    // Индексы текущих картинок
    const indices = {
      compliments: 0,
      care: 0,
      memories: 0
    };

    // Переключение табов
    function switchTab(tabName) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

      event.currentTarget.classList.add('active');
      document.getElementById(`tab-${tabName}`).classList.add('active');
    }

    // Показ текущего слайда
    function renderSlide(category) {
      const item = data[category][indices[category]];
      document.getElementById(`img-${category}`).src = item.img;
      document.getElementById(`text-${category}`).innerText = item.text;
    }

    // Переключение на следующий слайд
    function nextSlide(category) {
      indices[category] = (indices[category] + 1) % data[category].length;
      renderSlide(category);
    }

    // Создание анимации сердечек
    function createHearts() {
      const container = document.getElementById('hearts-container');
      const heartIcons = ['💖', '💗', '🌸', '✨', '🩷'];
      
      for (let i = 0; i < 15; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart-bg';
        heart.innerText = heartIcons[Math.floor(Math.random() * heartIcons.length)];
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.animationDuration = (Math.random() * 4 + 4) + 's';
        heart.style.animationDelay = (Math.random() * 5) + 's';
        heart.style.fontSize = (Math.random() * 15 + 15) + 'px';
        container.appendChild(heart);
      }
    }

    // Инициализация при загрузке
    window.onload = function() {
      renderSlide('compliments');
      renderSlide('care');
      renderSlide('memories');
      createHearts();
    };
  </script>
</body>
</html>
