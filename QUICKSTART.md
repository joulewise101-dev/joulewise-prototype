# 🚀 QUICK START - Joule-Wise

## ⚡ TL;DR - Get Running in 5 Minutes

### 1️⃣ Install Dependencies
```bash
npm install
```

### 2️⃣ Set Up Environment
```bash
# Copy the example environment file
copy .env.example .env
```

Then edit `.env` and add your database URL:
```env
DATABASE_URL=postgresql://user:password@localhost:5432/joulewise
```

### 3️⃣ Set Up Database
```bash
npm run db:push
```

### 4️⃣ Run the App
```bash
npm run dev
```

Visit: http://localhost:5000

---

## 🗄️ Need a Database?

### Option A: Free Cloud Database (Easiest)
1. Go to https://neon.tech
2. Sign up (free)
3. Create a project
4. Copy the connection string
5. Paste it in `.env` as `DATABASE_URL`

### Option B: Local PostgreSQL
1. Download: https://www.postgresql.org/download/windows/
2. Install and remember your password
3. Use this in `.env`:
   ```env
   DATABASE_URL=postgresql://postgres:YOUR_PASSWORD@localhost:5432/joulewise
   ```

---

## 🌐 Deploy to Production

**⚠️ IMPORTANT: DO NOT use Netlify!** 

This is a full Express.js server. Use one of these instead:

### Render (Recommended)
1. Go to https://render.com
2. Connect GitHub repo
3. Create Web Service
4. Add PostgreSQL database
5. Deploy!

See `README_DEPLOYMENT.md` for detailed instructions.

---

## ✅ All Errors Fixed

- ✅ Windows compatibility (cross-env added)
- ✅ Environment setup (.env.example created)
- ✅ Deployment guide (use Render, not Netlify)

---

## 📚 More Info

- **Full Deployment Guide:** `README_DEPLOYMENT.md`
- **Environment Variables:** `.env.example`
- **Netlify Config:** `netlify.toml` (reference only, won't work for deployment)
