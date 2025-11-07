# CarelyAI - Deployment Guide

## 🚀 Deploying to Streamlit Cloud

This guide will help you deploy CarelyAI to Streamlit Cloud from GitHub.

---

## 📋 Prerequisites

Before you begin, make sure you have:
- ✅ A GitHub account
- ✅ A Groq API key (free at [console.groq.com](https://console.groq.com/))
- ✅ (Optional) Telegram bot token for caregiver alerts

---

## 🔧 Step 1: Prepare Your Repository

### 1.1 Initialize Git (if not already done)

```powershell
cd d:\Streamlitcloud\CarelyAI
git init
```

### 1.2 Check What Will Be Committed

**IMPORTANT:** Before committing, verify that sensitive files are NOT being tracked:

```powershell
git status
```

**You should NOT see:**
- `.env` file
- `carely.db` file
- Any files in `data/vectors/` directory
- Any files in `attached_assets/Pasted*`

If you see any of these, they're already in `.gitignore` and won't be committed.

### 1.3 Add Files to Git

```powershell
git add .
```

### 1.4 Commit Your Changes

```powershell
git commit -m "Initial commit: CarelyAI application"
```

---

## 🌐 Step 2: Push to GitHub

### 2.1 Create a New Repository on GitHub

1. Go to [github.com](https://github.com)
2. Click the **"+"** icon in the top right
3. Select **"New repository"**
4. Name it: `carelyai` (or any name you prefer)
5. Choose **Public** or **Private** (both work with Streamlit Cloud)
6. **DO NOT** initialize with README, .gitignore, or license
7. Click **"Create repository"**

### 2.2 Connect Local Repository to GitHub

GitHub will show you commands. Use these:

```powershell
git remote add origin https://github.com/YOUR_USERNAME/carelyai.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

---

## ☁️ Step 3: Deploy to Streamlit Cloud

### 3.1 Sign Up for Streamlit Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io/)
2. Click **"Sign up"** or **"Continue with GitHub"**
3. Authorize Streamlit to access your GitHub repositories

### 3.2 Deploy Your App

1. Click **"New app"** button
2. Fill in the deployment form:
   - **Repository:** Select `YOUR_USERNAME/carelyai`
   - **Branch:** `main`
   - **Main file path:** `main.py`
   - **App URL:** Choose a custom URL (e.g., `carelyai-yourname`)

3. Click **"Advanced settings"** (optional)
   - **Python version:** 3.11 (recommended)

### 3.3 Configure Secrets

**CRITICAL STEP:** Before deploying, add your secrets:

1. In the deployment settings, find **"Secrets"** section
2. Click **"Edit Secrets"**
3. Add the following in TOML format:

```toml
# Required for AI chat
GROQ_API_KEY = "your_actual_groq_api_key_here"

# Optional for Telegram alerts
TELEGRAM_BOT_TOKEN = "your_telegram_bot_token_here"
TELEGRAM_CHAT_ID = "your_telegram_chat_id_here"
```

4. Click **"Save"**

### 3.4 Deploy!

Click **"Deploy!"** button and wait 2-5 minutes for your app to build and launch.

---

## 🔑 Getting Your API Keys

### GROQ API Key (Required)

1. Visit [console.groq.com](https://console.groq.com/)
2. Sign up for a free account
3. Navigate to **"API Keys"**
4. Click **"Create API Key"**
5. Copy the key immediately (you won't see it again!)

### Telegram Bot (Optional)

1. Open Telegram
2. Search for `@BotFather`
3. Send `/newbot` command
4. Follow the prompts to create your bot
5. Copy the **bot token** you receive
6. To get your **chat ID**:
   - Send a message to your new bot
   - Visit: `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
   - Find `"chat":{"id":123456789}` in the response

---

## 🔄 Updating Your Deployed App

When you make changes to your code:

```powershell
# Make your changes, then:
git add .
git commit -m "Description of your changes"
git push
```

Streamlit Cloud will automatically detect the changes and redeploy your app!

---

## ⚠️ Important Notes

### Database Persistence
- **Streamlit Cloud uses ephemeral storage** - the SQLite database will reset when:
  - The app redeploys
  - The container restarts
  - You push new code

- **For production use**, consider:
  - Using a cloud database (PostgreSQL on Heroku, Supabase, etc.)
  - Or accepting that data is temporary for demo purposes

### File Structure on Cloud
- The app runs in a temporary container
- Only files in your Git repository are available
- The `.env` file is NOT uploaded (it's in `.gitignore`)
- Secrets come from Streamlit Cloud's secrets management

### Security Best Practices
- ✅ Never commit `.env` files
- ✅ Never commit API keys or passwords
- ✅ Use Streamlit Cloud secrets for sensitive data
- ✅ Regularly rotate your API keys
- ✅ Use `.env.example` as a template only

---

## 🐛 Troubleshooting

### App won't start
1. Check the **Logs** in Streamlit Cloud dashboard
2. Verify all secrets are correctly set
3. Make sure `requirements.txt` includes all dependencies

### "Module not found" errors
- Add the missing module to `requirements.txt`
- Push the change to GitHub
- Streamlit Cloud will automatically redeploy

### Database errors on startup
- This is normal! The database is created on first run
- The app initializes sample data automatically

### API key errors
- Verify secrets are in TOML format (not `.env` format)
- Check for typos in variable names
- Ensure no quotes or special characters are escaped incorrectly

---

## 📞 Support

For detailed secrets setup, see: `SECRETS_SETUP.md`

For Streamlit Cloud support: [docs.streamlit.io](https://docs.streamlit.io/)

---

## 🎉 Success!

Once deployed, your app will be available at:
```
https://YOUR_CUSTOM_URL.streamlit.app
```

Share this URL with anyone to let them use CarelyAI! 

---

**Made with ❤️ for elderly care**
