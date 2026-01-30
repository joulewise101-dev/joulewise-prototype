# 🔐 GitHub Authentication Fix

## ❌ Error: Permission Denied (403)

You got this error:
```
remote: Permission to joulewise101-dev/joulewise-prototype.git denied
fatal: unable to access 'https://github.com/...': The requested URL returned error: 403
```

**This means:** You need to authenticate with GitHub to push code.

---

## ✅ SOLUTION: Use GitHub Personal Access Token

### Step 1: Create a Personal Access Token

1. **Go to GitHub Settings:**
   - Visit: https://github.com/settings/tokens
   - Or: GitHub → Click your profile → Settings → Developer settings → Personal access tokens → Tokens (classic)

2. **Generate New Token:**
   - Click "Generate new token" → "Generate new token (classic)"
   - **Note:** `Joule-Wise Deployment`
   - **Expiration:** 90 days (or your preference)
   - **Select scopes:**
     - ✅ `repo` (Full control of private repositories)
     - ✅ `workflow` (Update GitHub Action workflows)

3. **Generate and Copy:**
   - Click "Generate token" at the bottom
   - **IMPORTANT:** Copy the token immediately (you won't see it again!)
   - It looks like: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

---

### Step 2: Configure Git to Use Token

**Option A: Use Git Credential Manager (Recommended)**

Run this command and it will prompt you to log in:

```bash
cd "c:/Users/Aakansha Jagga/Downloads/Joule-Wise/Joule-Wise"
git push -u origin main
```

When prompted:
- **Username:** `joulewise101-dev` (or your GitHub username)
- **Password:** Paste your Personal Access Token (not your GitHub password!)

Git will remember your credentials for future pushes.

---

**Option B: Update Remote URL with Token**

```bash
cd "c:/Users/Aakansha Jagga/Downloads/Joule-Wise/Joule-Wise"

# Remove old origin
git remote remove origin

# Add new origin with token embedded
git remote add origin https://YOUR_TOKEN@github.com/joulewise101-dev/joulewise-prototype.git

# Push
git push -u origin main
```

Replace `YOUR_TOKEN` with your actual token.

**⚠️ Warning:** This stores your token in plain text in `.git/config`. Only use if you're the only user of this computer.

---

**Option C: Use GitHub CLI (Easiest)**

1. **Install GitHub CLI:**
   - Download from: https://cli.github.com/
   - Or use: `winget install --id GitHub.cli`

2. **Authenticate:**
   ```bash
   gh auth login
   ```
   - Choose: GitHub.com
   - Choose: HTTPS
   - Authenticate with browser

3. **Push:**
   ```bash
   cd "c:/Users/Aakansha Jagga/Downloads/Joule-Wise/Joule-Wise"
   git push -u origin main
   ```

---

## 🚀 Quick Fix (Recommended)

**Just run this and follow the prompts:**

```bash
cd "c:/Users/Aakansha Jagga/Downloads/Joule-Wise/Joule-Wise"
git push -u origin main
```

When prompted:
- **Username:** Your GitHub username
- **Password:** Your Personal Access Token (create one at https://github.com/settings/tokens)

---

## 📋 Step-by-Step Summary

1. ✅ Create Personal Access Token at https://github.com/settings/tokens
2. ✅ Copy the token (starts with `ghp_`)
3. ✅ Run: `cd "c:/Users/Aakansha Jagga/Downloads/Joule-Wise/Joule-Wise"`
4. ✅ Run: `git push -u origin main`
5. ✅ Enter your GitHub username
6. ✅ Paste your token as password
7. ✅ Done! Code pushed to GitHub

---

## ⚠️ Important Notes

- **Don't use your GitHub password** - It won't work for HTTPS push
- **Use Personal Access Token** - This is the new authentication method
- **Token is like a password** - Keep it secret, don't share it
- **Git will remember it** - You only need to enter it once

---

## 🔍 Troubleshooting

### "Token doesn't work"
- Make sure you selected `repo` scope when creating the token
- Make sure you copied the entire token
- Try creating a new token

### "Still getting 403"
- Make sure you're using the token as password, not your GitHub password
- Check that the repository exists: https://github.com/joulewise101-dev/joulewise-prototype
- Make sure you have write access to the repository

### "Repository doesn't exist"
1. Go to https://github.com/new
2. Create repository: `joulewise-prototype`
3. Don't initialize with README
4. Try pushing again

---

## ✅ After Successful Push

Once you successfully push, you can:

1. **Verify on GitHub:**
   - Visit: https://github.com/joulewise101-dev/joulewise-prototype
   - You should see your code and `render.yaml`

2. **Deploy to Render:**
   - Go to https://render.com
   - Click "New +" → "Blueprint"
   - Select your repository
   - Click "Apply"
   - Done! 🎉

---

## 🎯 Next Steps

1. Create Personal Access Token
2. Push to GitHub with token
3. Deploy to Render
4. Your app goes live!

**See `RENDER_DEPLOYMENT.md` for deployment instructions after you push to GitHub.**
