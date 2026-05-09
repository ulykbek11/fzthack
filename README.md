# Hackathon Project

## Как запустить

### Backend
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Конфигурация
1. Скопируй `.env.example` в `.env.local`
2. Добавь данные Supabase (URL и anon key)

### Настройка Google OAuth
1. Перейди в [Supabase Dashboard](https://supabase.com/dashboard/project/etaieuwclbqbwoapwkgp)
2. **Authentication → Providers → Google**
3. Включи Google provider
4. Добавь Google Client ID и Client Secret (получи в [Google Cloud Console](https://console.cloud.google.com/))
5. В **Redirect URLs** добавь: `http://localhost:3000/auth/callback`
6. Сохрани изменения

Теперь пользователи смогут входить через email/password или Google аккаунт!
