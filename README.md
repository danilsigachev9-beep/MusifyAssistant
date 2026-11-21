<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Musify Assistant Pro — Скажите, компьютер сделает</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    
    <style>
        /* --- CSS (Стили) --- */
        :root {
            --bg-color: #08050C;
            --sidebar-color: #0F0A17;
            --card-color: #161021;
            --accent-color: #8B5CF6;
            --accent-hover: #7C3AED;
            --text-color: #FFFFFF;
            --text-dim: #9E96AB;
            --border-color: #2A1F3D;
            --font-main: 'Inter', sans-serif;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        body { font-family: var(--font-main); background-color: var(--bg-color); color: var(--text-color); line-height: 1.6; }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }

        /* Кнопки */
        .btn { display: inline-block; padding: 12px 28px; border-radius: 8px; font-weight: 600; text-decoration: none; transition: background 0.3s; cursor: pointer; border: none; font-size: 16px; }
        .btn-primary { background-color: var(--accent-color); color: #fff; }
        .btn-primary:hover { background-color: var(--accent-hover); }
        .btn-secondary { background-color: transparent; color: var(--text-color); border: 1px solid var(--border-color); }
        .btn-secondary:hover { border-color: var(--accent-color); }

        /* Шапка */
        header { background-color: rgba(8, 5, 12, 0.8); backdrop-filter: blur(10px); position: fixed; width: 100%; top: 0; z-index: 1000; border-bottom: 1px solid var(--border-color); }
        .header-content { display: flex; justify-content: space-between; align-items: center; height: 70px; }
        .logo { font-size: 24px; font-weight: 800; display: flex; align-items: center; gap: 8px; color: white; text-decoration: none;}
        .logo-icon { color: var(--accent-color); }
        .logo-pro { font-size: 12px; background: var(--accent-color); padding: 2px 6px; border-radius: 4px; vertical-align: super; }
        nav a { color: var(--text-dim); text-decoration: none; margin-left: 24px; font-weight: 600; transition: color 0.3s; }
        nav a:hover { color: var(--text-color); }

        /* Главный экран */
        .hero { padding: 150px 0 100px; }
        .hero-content { display: flex; align-items: center; justify-content: space-between; gap: 50px; }
        .hero-text { flex: 1; }
        .hero-text h1 { font-size: 56px; line-height: 1.1; margin-bottom: 24px; }
        .gradient-text { background: linear-gradient(90deg, #A78BFA, #8B5CF6); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hero-text p { font-size: 18px; color: var(--text-dim); margin-bottom: 32px; max-width: 500px; }
        .hero-buttons { display: flex; gap: 16px; margin-bottom: 40px; }
        .hero-stats { display: flex; gap: 40px; }
        .stat { font-size: 14px; color: var(--text-dim); }
        .stat-num { font-size: 28px; font-weight: 800; color: var(--text-color); }
        .hero-visual { flex: 1; display: flex; flex-direction: column; gap: 16px; align-items: flex-end; }
        .chat-bubble { padding: 16px 24px; border-radius: 20px; font-weight: 600; max-width: 80%; }
        .chat-bubble.user { background-color: var(--card-color); border: 1px solid var(--border-color); border-bottom-right-radius: 4px; }
        .chat-bubble.bot { background-color: var(--accent-color); border-bottom-left-radius: 4px; }

        /* Секции */
        section { padding: 80px 0; }
        .section-title { font-size: 36px; text-align: center; margin-bottom: 12px; }
		.section-subtitle { text-align: center; color: var(--text-dim); font-size: 18px; margin-bottom: 48px; }

        /* Демонстрация */
        .demo-grid { display: flex; justify-content: center; gap: 16px; margin-bottom: 24px; flex-wrap: wrap; }
        .demo-btn { background-color: var(--card-color); border: 1px solid var(--border-color); color: var(--text-color); padding: 12px 24px; border-radius: 8px; cursor: pointer; font-size: 16px; transition: all 0.3s; }
        .demo-btn:hover { border-color: var(--accent-color); background-color: rgba(139, 92, 246, 0.1); }
        .demo-result { background-color: var(--card-color); border: 1px solid var(--border-color); border-radius: 12px; padding: 32px; text-align: center; max-width: 600px; margin: 0 auto; min-height: 100px; display: flex; align-items: center; justify-content: center; font-size: 18px; color: var(--text-dim); }

        /* Сценарии */
        .scenario-cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 24px; }
        .scenario-card { background-color: var(--card-color); border: 1px solid var(--border-color); border-radius: 12px; padding: 32px; }
        .scenario-card h3 { margin-bottom: 16px; color: var(--accent-color); }
        .scenario-card ul { list-style: none; }
        .scenario-card li { padding: 8px 0; color: var(--text-dim); border-bottom: 1px solid rgba(255,255,255,0.05); }
        .scenario-card li:last-child { border-bottom: none; }

        /* Персонажи */
        .character-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 24px; }
        .character-card { background-color: var(--card-color); border: 1px solid var(--border-color); border-radius: 12px; padding: 32px; text-align: center; transition: border-color 0.3s; }
        .character-card.active { border-color: var(--accent-color); }
        .char-icon { font-size: 48px; margin-bottom: 16px; }

        /* Редактор */
        .editor-content { display: flex; gap: 50px; align-items: center; }
        .editor-text { flex: 1; }
        .editor-list { list-style: none; margin-top: 24px; }
        .editor-list li { padding: 8px 0; color: var(--text-dim); display: flex; align-items: center; gap: 12px; }
        .editor-list li::before { content: "✓"; color: var(--accent-color); font-weight: bold; }
        .editor-visual { flex: 1; }
        .code-block { background-color: var(--card-color); border: 1px solid var(--border-color); border-radius: 12px; padding: 32px; font-family: 'Courier New', monospace; }
        .code-line { margin-bottom: 12px; color: var(--text-dim); }
        .code-keyword { color: var(--accent-color); }

        /* FAQ */
        .faq-item { background-color: var(--card-color); border: 1px solid var(--border-color); border-radius: 12px; margin-bottom: 16px; overflow: hidden; }
        .faq-question { width: 100%; text-align: left; padding: 24px; background: none; border: none; color: var(--text-color); font-size: 18px; font-weight: 600; cursor: pointer; display: flex; justify-content: space-between; align-items: center; }
        .faq-question::after { content: "+"; color: var(--accent-color); font-size: 24px; }
        .faq-answer { padding: 0 24px 24px; color: var(--text-dim); display: none; }
        .faq-item.active .faq-answer { display: block; }

        /* Подвал */
        footer { background-color: var(--sidebar-color); padding: 60px 0 20px; border-top: 1px solid var(--border-color); }
        .footer-content { display: flex; justify-content: space-between; margin-bottom: 40px; }
        .footer-info p { color: var(--text-dim); margin-top: 8px; }
        .footer-links a { display: block; color: var(--text-dim); text-decoration: none; margin-bottom: 12px; transition: color 0.3s; }
        .footer-links a:hover { color: var(--accent-color); }
        .footer-bottom { text-align: center; color: var(--text-dim); font-size: 14px; border-top: 1px solid var(--border-color); padding-top: 20px; }
		/* Адаптивность (для телефонов) */
        @media (max-width: 768px) {
            .hero-content, .editor-content { flex-direction: column; text-align: center; }
            .hero-text h1 { font-size: 36px; }
            .hero-stats { justify-content: center; flex-wrap: wrap; gap: 20px; }
            .header-content nav { display: none; }
            .hero-visual { align-items: center; margin-top: 30px; }
            .chat-bubble { max-width: 100%; }
        }
    </style>
</head>
<body>
    <!-- ШАПКА -->
    <header>
        <div class="container header-content">
            <a href="#" class="logo">
                <span class="logo-icon">🌀</span> Musify <span class="logo-pro">PRO</span>
            </a>
            <nav>
                <a href="#features">Возможности</a>
                <a href="#characters">Персонажи</a>
                <a href="#editor">Редактор</a>
                <a href="#faq">FAQ</a>
            </nav>
            <a href="https://t.me/musify_assistant_bot" class="btn btn-primary">Купить</a>
        </div>
    </header>

    <!-- ГЛАВНЫЙ ЭКРАН -->
    <section class="hero">
        <div class="container hero-content">
            <div class="hero-text">
                <h1>Скажите — <br><span class="gradient-text">компьютер сделает</span></h1>
                <p>Одна фраза — и программы открыты, музыка играет, окна на местах. А нейросеть и ИИ-агент в образе <strong>Рика Санчеза</strong> возьмут на себя остальное.</p>
                <div class="hero-buttons">
                    <a href="https://t.me/musify_assistant_bot" class="btn btn-primary">Попробовать</a>
                    <a href="#features" class="btn btn-secondary">Узнать больше</a>
                </div>
                <div class="hero-stats">
                    <div class="stat"><span class="stat-num">100+</span><br>Готовых команд</div>
                    <div class="stat"><span class="stat-num">6</span><br>Персонажей</div>
                    <div class="stat"><span class="stat-num">∞</span><br>Своих сценариев</div>
                </div>
            </div>
            <div class="hero-visual">
                <div class="chat-bubble user">Открой Steam и запусти CS2</div>
                <div class="chat-bubble bot">Секунду, гений. Уже запускаю.</div>
            </div>
        </div>
    </section>

    <!-- ДЕМОНСТРАЦИЯ -->
    <section class="demo" id="features">
        <div class="container">
            <h2 class="section-title">Сказали — <span class="gradient-text">сделано</span></h2>
            <p class="section-subtitle">Нажмите на пример и посмотрите, что сделает Musify.</p>
            <div class="demo-grid">
                <button class="demo-btn" data-command="Открой браузер">Открой браузер</button>
                <button class="demo-btn" data-command="Громкость на 50">Громкость на 50</button>
                <button class="demo-btn" data-command="Запусти игру">Запусти игру</button>
            </div>
            <div class="demo-result">
                <p id="demo-text">Выберите команду выше...</p>
            </div>
        </div>
    </section>

    <!-- СЦЕНАРИИ -->
    <section class="scenarios">
        <div class="container">
            <h2 class="section-title">Одна фраза — <span class="gradient-text">десяток действий</span></h2>
            <p class="section-subtitle">Утро, работа, игра, вечер — каждый в одну команду.</p>
            <div class="scenario-cards">
                <div class="scenario-card">
                    <h3>«Начать работу»</h3>
                    <ul>
                        <li>Открыть браузер</li>
                        <li>Запустить Telegram</li>
                        <li>Включить музыку</li>
                        <li>Громкость на 30%</li>
                    </ul>
                </div>
                <div class="scenario-card">
                    <h3>«Игровой режим»</h3>
                    <ul>
                        <li>Запустить Steam</li>
						<li>Открыть Discord</li>
                        <li>Закрыть лишние окна</li>
                        <li>Громкость на 80%</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- ПЕРСОНАЖИ -->
    <section class="characters" id="characters">
        <div class="container">
            <h2 class="section-title">Выбери <span class="gradient-text">свой голос</span></h2>
            <p class="section-subtitle">В Musify Assistant Pro ты не привязан к одному голосу.</p>
            <div class="character-grid">
                <div class="character-card active">
                    <div class="char-icon">🔬</div>
                    <h3>Рик Санчез</h3>
                    <p>Гениальный, циничный, с матами.</p>
                </div>
                <div class="character-card">
                    <div class="char-icon">🤵</div>
                    <h3>Джарвис</h3>
                    <p>Идеальный британский дворецкий.</p>
                </div>
                <div class="character-card">
                    <div class="char-icon">🤖</div>
                    <h3>GLaDOS</h3>
                    <p>Холодная и пассивно-агрессивная.</p>
                </div>
                <div class="character-card">
                    <div class="char-icon">🌸</div>
                    <h3>Мита</h3>
                    <p>Милая аниме-девушка с подтекстом.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- РЕДАКТОР КОМАНД -->
    <section class="editor" id="editor">
        <div class="container editor-content">
            <div class="editor-text">
                <h2 class="section-title">Свои команды — <br><span class="gradient-text">без строчки кода</span></h2>
                <p>Придумайте фразу, добавьте шаги — готово. Визуальный редактор позволяет создавать сценарии любой сложности.</p>
                <ul class="editor-list">
                    <li>Своя фраза и слова-триггеры</li>
                    <li>Запись действий (повторите клики один раз)</li>
                    <li>Создание с AI (опишите словами)</li>
                    <li>Импорт и экспорт команд</li>
                </ul>
            </div>
            <div class="editor-visual">
                <div class="code-block">
                    <div class="code-line"><span class="code-keyword">Команда:</span> "Начать стрим"</div>
                    <div class="code-line"><span class="code-keyword">Действие 1:</span> Открыть OBS</div>
                    <div class="code-line"><span class="code-keyword">Действие 2:</span> Запустить Discord</div>
                    <div class="code-line"><span class="code-keyword">Действие 3:</span> Включить микрофон</div>
                </div>
            </div>
        </div>
    </section>

    <!-- FAQ -->
    <section class="faq" id="faq">
        <div class="container">
            <h2 class="section-title">Частые <span class="gradient-text">вопросы</span></h2>
            <div class="faq-item">
                <button class="faq-question">Нужен ли мощный компьютер?</button>
                <div class="faq-answer"><p>Нет. Программа оптимизирована под Windows 10/11 и работает даже на слабых ПК. Основная нагрузка идет только при общении с нейросетью.</p></div>
            </div>
            <div class="faq-item">
                <button class="faq-question">Это подписка?</button>
                <div class="faq-answer"><p>Нет, вы покупаете лицензию навсегда. Все будущие обновления бесплатны.</p></div>
            </div>
            <div class="faq-item">
                <button class="faq-question">Нужен ли интернет?</button>
                <div class="faq-answer"><p>Для базовых команд — нет. Для генерации голоса и общения с ИИ — да.</p></div>
            </div>
        </div>
    </section>

    <!-- ПОДВАЛ -->
    <footer>
        <div class="container footer-content">
            <div class="footer-info">
			<div class="logo">🌀 Musify <span class="logo-pro">PRO</span></div>
                <p>Голосовой ассистент с характером.</p>
            </div>
            <div class="footer-links">
                <a href="https://t.me/musify_assistant_bot">Бот-магазин</a>
                <a href="https://t.me/musify_support_bot">Поддержка</a>
            </div>
        </div>
        <div class="footer-bottom">
            <p>© 2026 Musify Assistant Pro. Все права защищены.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Демонстрация команд
            const demoButtons = document.querySelectorAll('.demo-btn');
            const demoText = document.getElementById('demo-text');

            const responses = {
                'Открой браузер': '🌐 Открываю браузер... Готово!',
                'Громкость на 50': '🔊 Устанавливаю громкость на 50%... Готово!',
                'Запусти игру': '🎮 Запускаю Steam и CS2... Удачной игры!'
            };

            demoButtons.forEach(btn => {
                btn.addEventListener('click', () => {
                    const command = btn.dataset.command;
                    demoText.textContent = `Выполняю: "${command}"...`;
                    setTimeout(() => {
                        demoText.textContent = responses[command] || 'Команда выполнена!';
                    }, 800);
                });
            });

            // Аккордеон FAQ
            const faqQuestions = document.querySelectorAll('.faq-question');
            faqQuestions.forEach(question => {
                question.addEventListener('click', () => {
                    const item = question.parentElement;
                    item.classList.toggle('active');
                });
            });
        });
    </script>
</body>
</html>
