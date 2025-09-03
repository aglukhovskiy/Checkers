# 🚂 Подробное руководство по деплою на Railway

## Шаг 1: Создание аккаунта и вход

1. **Перейдите на [railway.app](https://railway.app/)**
2. **Нажмите "Get Started"** или "Login"
3. **Выберите вход через GitHub** (рекомендуется)
4. **Авторизуйте приложение** предоставив необходимые permissions

## Шаг 2: Создание проекта

1. **На главной странице Railway нажмите "New Project"**
2. **Выберите "Deploy from GitHub repo"**
   
   ![Deploy from GitHub](https://i.imgur.com/abc123.png)

3. **Если репозиторий не отображается:**
   - Нажмите "Configure GitHub App" или "Install GitHub App"
   - Выберите ваш аккаунт или организацию
   - Разрешите доступ к репозиториям (все или конкретные)
   - Вернитесь в Railway и обновите страницу

## Шаг 3: Настройка деплоя

1. **Выберите ваш репозиторий** из списка
2. **Railway автоматически определит Python проект**
3. **Деплой начнется автоматически** после выбора репозитория

## Шаг 4: Получение URL backend

1. **После успешного деплоя перейдите в Dashboard проекта**
2. **Найдите раздел "Domains" или "Settings"**
3. **Скопируйте URL вашего приложения** (выглядит как `https://your-project-name.up.railway.app`)

## Шаг 5: Настройка GitHub Secrets

1. **Перейдите в ваш GitHub репозиторий**
2. **Settings → Secrets and variables → Actions**
3. **Нажмите "New repository secret"**
4. **Добавьте секрет:**
   - Name: `BACKEND_URL`
   - Value: `https://your-project-name.up.railway.app` (ваш URL из Railway)

## 🔍 Решение проблем

### Репозиторий не отображается в Railway
1. **Проверьте установку GitHub App**: 
   - Перейдите в GitHub → Settings → Applications
   - Убедитесь, что Railway App установлен
   - Проверьте permissions к репозиториям

2. **Переустановите GitHub App**:
   - Удалите Railway из authorized OAuth Apps
   - Повторите процесс подключения

### Ошибки деплоя
1. **Проверьте `requirements.txt`** - все зависимости должны быть указаны
2. **Убедитесь, что `api_v2.py`** находится в корне проекта
3. **Проверьте логи деплоя** в Railway Dashboard

### CORS ошибки
Убедитесь, что в [`api_v2.py`](api_v2.py) правильно настроены CORS:
```python
CORS(app, resources={
    r"/*": {"origins": ["http://localhost:8000", "https://*.github.io"]}
})
```

## 🌐 Альтернативные хостинги

### Render.com
1. **Создайте аккаунт на [render.com](https://render.com/)**
2. **Connect your repository** из GitHub
3. **Создайте Web Service**
4. **Настройки:**
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python api_v2.py`

### Heroku
1. **Установите Heroku CLI**
2. **Создайте `Procfile`:**
   ```
   web: python api_v2.py
   ```
3. **Деплой через Git push**

## 📞 Поддержка

Если все еще возникают проблемы:

1. **Проверьте Railway Status**: [status.railway.app](https://status.railway.app/)
2. **Посмотрите документацию**: [docs.railway.app](https://docs.railway.app/)
3. **Зайдите в Discord**: [Railway Discord](https://discord.gg/railway)

## ✅ Проверка работоспособности

После деплоя проверьте:
1. **Backend доступен**: Откройте `https://your-project.railway.app/get_state` в браузере
2. **Должен вернуться JSON** с состоянием игры
3. **Frontend подключается**: Откройте консоль браузера, не должно быть CORS ошибок

Теперь ваш бот готов к игре на GitHub Pages! 🎉