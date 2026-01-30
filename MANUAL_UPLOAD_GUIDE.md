# 📤 Manual Upload Guide (No Command Line Needed)

Yes, you can upload files manually! This works perfectly with Render.

## Step 1: Prepare Your Files
1. Open File Explorer on your computer.
2. Navigate to: `Downloads` -> `Joule-Wise` -> `Joule-Wise`
3. Make sure you see these files:
   - `package.json`
   - `render.yaml`
   - `client` (folder)
   - `server` (folder)

## Step 2: Create GitHub Repository
1. Log in to [GitHub.com](https://github.com).
2. Click the **+** icon (top right) -> **New repository**.
3. Repository name: `joulewise-prototype`
4. **Uncheck** "Initialize this repository with a README".
5. Click **Create repository**.

## Step 3: Upload Files
1. In your new repository screen, click the link: **"uploading an existing file"**.
2. **Select all files** inside your local `Joule-Wise` folder.
   - Tip: Press `Ctrl+A` in your folder to select everything.
3. **Drag and drop** them into the GitHub page.
4. Wait for them to upload.
5. In the "Commit changes" box at the bottom, type "Initial upload".
6. Click **Commit changes**.

## Step 4: Deploy to Render
1. Go to [Render.com](https://render.com).
2. Click **New +** -> **Blueprint**.
3. Select your `joulewise-prototype` repo.
4. Click **Apply**.
5. Click **Create Resources**.

Render will now check out your code and deploy it!
