# 🚀 Quick Deployment Checklist

Use this checklist before pushing to Git and deploying to Streamlit Cloud.

## ✅ Pre-Deployment Checklist

### 1. Security Check
- [ ] `.env` file is in `.gitignore` (already done ✓)
- [ ] `carely.db` is in `.gitignore` (already done ✓)
- [ ] No API keys are hardcoded in any `.py` files
- [ ] All sensitive data uses environment variables

### 2. Files Check
- [ ] `.env.example` exists with placeholder values (✓)
- [ ] `requirements.txt` is up to date (✓)
- [ ] `.gitignore` is complete (✓)
- [ ] `DEPLOYMENT.md` guide is ready (✓)
- [ ] `SECRETS_SETUP.md` is available (✓)

### 3. Test Locally
```powershell
# Test that your app runs
streamlit run main.py
```
- [ ] App starts without errors
- [ ] Chat functionality works
- [ ] Database initializes correctly
- [ ] No errors in console

### 4. Prepare Git Repository
```powershell
# Check what will be committed
git status

# You should NOT see:
# - .env
# - carely.db
# - data/vectors/
# - attached_assets/Pasted*
```
- [ ] No sensitive files in `git status`

### 5. Commit and Push
```powershell
git add .
git commit -m "Initial commit: CarelyAI application"
git remote add origin https://github.com/YOUR_USERNAME/carelyai.git
git branch -M main
git push -u origin main
```
- [ ] Code pushed to GitHub successfully
- [ ] Repository is visible on GitHub

### 6. Streamlit Cloud Setup
- [ ] Signed up at [share.streamlit.io](https://share.streamlit.io)
- [ ] Connected GitHub account
- [ ] Created new app deployment
- [ ] Selected correct repository and branch
- [ ] Set main file path to `main.py`

### 7. Configure Secrets
In Streamlit Cloud secrets (TOML format):
```toml
GROQ_API_KEY = "your_actual_key_here"
TELEGRAM_BOT_TOKEN = "your_bot_token_here"  # Optional
TELEGRAM_CHAT_ID = "your_chat_id_here"      # Optional
```
- [ ] GROQ_API_KEY added to secrets
- [ ] Telegram credentials added (if using)
- [ ] Secrets saved

### 8. Deploy!
- [ ] Clicked "Deploy" button
- [ ] Waited for build to complete (2-5 minutes)
- [ ] App is running successfully
- [ ] No errors in logs

### 9. Post-Deployment Testing
- [ ] App URL is accessible
- [ ] Homepage loads correctly
- [ ] Can send chat messages
- [ ] AI responses work
- [ ] No console errors

## 🎉 Success!

Your app is now live at: `https://YOUR_APP_URL.streamlit.app`

---

## 📝 Quick Commands Reference

### Local Development
```powershell
# Run app locally
streamlit run main.py

# Check environment variables
cat .env
```

### Git Commands
```powershell
# Check status
git status

# See what changed
git diff

# Commit changes
git add .
git commit -m "Your message here"

# Push updates
git push
```

### Update Deployed App
```powershell
# After making changes:
git add .
git commit -m "Description of changes"
git push
# Streamlit Cloud auto-deploys!
```

---

## ⚠️ Common Issues

### Issue: App won't start
**Solution:** Check Streamlit Cloud logs for errors

### Issue: "GROQ_API_KEY not found"
**Solution:** Verify secrets are set in Streamlit Cloud dashboard

### Issue: Database resets on redeploy
**Solution:** This is expected behavior with SQLite on Streamlit Cloud (ephemeral storage)

### Issue: Import errors
**Solution:** Add missing packages to `requirements.txt` and push

---

## 📚 Resources

- Full deployment guide: `DEPLOYMENT.md`
- Secrets setup guide: `SECRETS_SETUP.md`
- Streamlit docs: [docs.streamlit.io](https://docs.streamlit.io/)
- Get Groq API key: [console.groq.com](https://console.groq.com/)

---

**Ready to deploy? Let's go! 🚀**
