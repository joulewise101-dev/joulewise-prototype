# 🚀 Render Deployment Guide - Joule-Wise

## ✅ render.yaml Configuration Created!

I've created a `render.yaml` file that will automatically set up your entire application on Render, including:
- ✅ Web service (Express.js + React)
- ✅ PostgreSQL database
- ✅ Environment variables
- ✅ Auto-deployment from GitHub

---

## 🎯 Quick Deployment (2 Methods)

### Method 1: Using render.yaml (RECOMMENDED) ⭐

This is the easiest method - Render will automatically configure everything!

**Steps:**

1. **Commit and push render.yaml to GitHub:**
   ```bash
   git add render.yaml
   git commit -m "Add Render configuration"
   git push origin main
   ```

2. **Go to Render Dashboard:**
   - Visit https://render.com
   - Sign up or log in with GitHub

3. **Create New Blueprint:**
   - Click "New +" → "Blueprint"
   - Select your repository: `joulewise101-dev/joulewise-prototype`
   - Render will detect `render.yaml` automatically
   - Click "Apply"

4. **Review Configuration:**
   - Render will show you what it will create:
     - ✅ Web Service: `joulewise`
     - ✅ PostgreSQL Database: `joulewise-db`
     - ✅ Environment variables (auto-configured)
   
5. **Deploy:**
   - Click "Create Resources"
   - Wait 5-10 minutes for deployment
   - Done! 🎉

---

### Method 2: Manual Setup (Alternative)

If you prefer to set up manually:

1. **Create PostgreSQL Database:**
   - Go to https://dashboard.render.com
   - Click "New +" → "PostgreSQL"
   - Name: `joulewise-db`
   - Plan: Free
   - Click "Create Database"
   - Copy the "Internal Database URL"

2. **Create Web Service:**
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Configure:
     - **Name:** `joulewise`
     - **Runtime:** Node
     - **Build Command:** `npm install && npm run build`
     - **Start Command:** `npm start`
     - **Plan:** Free

3. **Add Environment Variables:**
   - In the web service settings, add:
     - `NODE_ENV` = `production`
     - `DATABASE_URL` = (paste the Internal Database URL from step 1)
     - `SESSION_SECRET` = (generate a random string, e.g., use https://randomkeygen.com/)

4. **Deploy:**
   - Click "Create Web Service"
   - Wait for deployment

---

## 📋 What's in render.yaml?

```yaml
services:
  - type: web
    name: joulewise
    runtime: node
    plan: free                    # Free tier
    buildCommand: npm install && npm run build
    startCommand: npm start
    envVars:
      - DATABASE_URL              # Auto-linked to database
      - SESSION_SECRET            # Auto-generated
      - NODE_ENV=production

databases:
  - name: joulewise-db
    plan: free                    # Free PostgreSQL
    databaseName: joulewise
```

**Benefits:**
- ✅ Everything configured automatically
- ✅ Database URL auto-linked to web service
- ✅ SESSION_SECRET auto-generated
- ✅ Free tier for both web service and database
- ✅ Auto-deploys on every git push

---

## 🔧 Configuration Details

### Web Service Settings:
- **Name:** `joulewise`
- **Runtime:** Node.js (auto-detected)
- **Plan:** Free (750 hours/month)
- **Region:** Oregon (us-west)
- **Build:** `npm install && npm run build`
- **Start:** `npm start`
- **Health Check:** `/` (root path)

### Database Settings:
- **Name:** `joulewise-db`
- **Type:** PostgreSQL 16
- **Plan:** Free (90 days, then $7/month)
- **Region:** Oregon (same as web service)
- **Database Name:** `joulewise`
- **User:** `joulewise`

### Environment Variables (Auto-configured):
- `NODE_ENV` → `production`
- `SESSION_SECRET` → Auto-generated secure random string
- `DATABASE_URL` → Auto-linked from `joulewise-db`

---

## 🎯 After Deployment

### 1. Initialize Database Schema

Once deployed, you need to push your database schema:

**Option A: Using Render Shell**
1. Go to your web service in Render dashboard
2. Click "Shell" tab
3. Run:
   ```bash
   npm run db:push
   ```

**Option B: Using Local Environment**
1. Copy the External Database URL from Render
2. In your local `.env` file, temporarily set:
   ```env
   DATABASE_URL=<paste-external-database-url>
   ```
3. Run locally:
   ```bash
   npm run db:push
   ```
4. Revert `.env` to your local database

### 2. Verify Deployment

Visit your deployed app:
- Your app will be at: `https://joulewise.onrender.com`
- Check the logs in Render dashboard
- Test the main features

### 3. Set Up Custom Domain (Optional)

1. In Render dashboard, go to your web service
2. Click "Settings" → "Custom Domain"
3. Add your domain (e.g., `joulewise.com`)
4. Follow DNS configuration instructions

---

## 🔄 Automatic Deployments

With `render.yaml` in your repository:

- ✅ **Auto-deploy on push:** Every push to `main` branch triggers deployment
- ✅ **Preview deployments:** Pull requests get preview URLs
- ✅ **Rollback support:** Easy rollback to previous versions
- ✅ **Build logs:** Full visibility into build process

---

## 💰 Cost Breakdown

### Free Tier:
- **Web Service:** FREE (750 hours/month)
  - Spins down after 15 minutes of inactivity
  - Spins up automatically on request (takes ~30 seconds)
  
- **PostgreSQL:** FREE for 90 days
  - After 90 days: $7/month
  - 1GB storage
  - Shared CPU

### To Stay Free Forever:
- Use Render for web service (free)
- Use external free database:
  - **Neon** (https://neon.tech) - Free forever, 0.5GB
  - **Supabase** (https://supabase.com) - Free forever, 500MB
  - **ElephantSQL** (https://elephantsql.com) - Free tier available

**To use external database:**
1. Create database on Neon/Supabase
2. Copy connection string
3. In Render, set `DATABASE_URL` manually instead of using `fromDatabase`

---

## 🐛 Troubleshooting

### "No render.yaml found on main branch"
**Solution:**
```bash
git add render.yaml
git commit -m "Add Render configuration"
git push origin main
```

### "Build failed"
**Check:**
- Are all dependencies in `package.json`?
- Does `npm run build` work locally?
- Check build logs in Render dashboard

### "Application error / 503"
**Check:**
- Is `npm start` command correct?
- Are environment variables set?
- Check application logs in Render dashboard

### "Database connection failed"
**Check:**
- Is DATABASE_URL set correctly?
- Is database running? (check database dashboard)
- Did you run `npm run db:push`?

### "App spins down / slow to start"
**This is normal on free tier:**
- Free tier spins down after 15 minutes of inactivity
- First request after spin-down takes ~30 seconds
- Upgrade to paid tier ($7/month) for always-on

---

## 📊 Monitoring Your App

### In Render Dashboard:

1. **Logs:**
   - Click on your service → "Logs" tab
   - See real-time application logs
   - Filter by time period

2. **Metrics:**
   - Click "Metrics" tab
   - See CPU, memory, request count
   - Monitor performance

3. **Events:**
   - See deployment history
   - Track builds and deploys
   - View rollback options

---

## 🔐 Security Best Practices

### Environment Variables:
- ✅ Never commit `.env` to Git
- ✅ Use Render's environment variable management
- ✅ Rotate SESSION_SECRET periodically
- ✅ Use strong database passwords

### Database:
- ✅ Use Internal Database URL for web service (faster, more secure)
- ✅ Only use External Database URL for local development
- ✅ Enable SSL for database connections (enabled by default)

---

## 🚀 Advanced Configuration

### Custom Build Command:
```yaml
buildCommand: npm ci && npm run build && npm run db:push
```
This will also run database migrations during build.

### Health Check:
```yaml
healthCheckPath: /api/health
```
Create a health check endpoint in your app.

### Custom Region:
```yaml
region: singapore  # or frankfurt, oregon, ohio
```
Choose region closest to your users.

### Environment-Specific Variables:
```yaml
envVars:
  - key: OPENAI_API_KEY
    sync: false  # Won't be synced from render.yaml
```

---

## ✅ Deployment Checklist

**Before Deploying:**
- [x] ✅ `render.yaml` created
- [ ] ⏳ Code pushed to GitHub
- [ ] ⏳ Render account created
- [ ] ⏳ Repository connected to Render

**During Deployment:**
- [ ] ⏳ Blueprint applied
- [ ] ⏳ Resources created
- [ ] ⏳ Build completed
- [ ] ⏳ Service started

**After Deployment:**
- [ ] ⏳ Database schema pushed (`npm run db:push`)
- [ ] ⏳ App tested and working
- [ ] ⏳ Custom domain configured (optional)
- [ ] ⏳ Monitoring set up

---

## 🎉 Next Steps

1. **Commit render.yaml:**
   ```bash
   git add render.yaml
   git commit -m "Add Render deployment configuration"
   git push origin main
   ```

2. **Deploy to Render:**
   - Go to https://render.com
   - Click "New +" → "Blueprint"
   - Select your repository
   - Click "Apply"

3. **Initialize Database:**
   - Use Render Shell to run `npm run db:push`

4. **Test Your App:**
   - Visit `https://joulewise.onrender.com`
   - Test all features

5. **Share Your App:**
   - Your app is now live! 🎊

---

## 📞 Need Help?

- **Render Docs:** https://render.com/docs
- **Render Community:** https://community.render.com
- **Your Guides:** Check `README_DEPLOYMENT.md` and `QUICKSTART.md`

---

**Your app is ready to deploy! 🚀**

Just commit `render.yaml` and push to GitHub, then create a Blueprint on Render!
