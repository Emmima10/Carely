# Streamlit Secrets Configuration for CarelyAI

## Setting Up Secrets in Streamlit Cloud

When deploying to Streamlit Cloud, you need to configure your secrets in the Streamlit Cloud dashboard instead of using a `.env` file.

### Steps:

1. **Go to your app's settings** in Streamlit Cloud
2. **Navigate to the "Secrets" section**
3. **Add the following content** (in TOML format):

```toml
# Required for AI chat
GROQ_API_KEY = "your_groq_api_key_here"

# Optional for Telegram caregiver alerts
TELEGRAM_BOT_TOKEN = "your_telegram_bot_token_here"
TELEGRAM_CHAT_ID = "your_telegram_chat_id_here"
```

### Getting Your API Keys:

#### GROQ API Key (Required)
1. Visit [https://console.groq.com/](https://console.groq.com/)
2. Sign up for a free account
3. Go to API Keys section
4. Create a new API key
5. Copy the key and paste it in the secrets

#### Telegram Bot (Optional)
1. Open Telegram and search for `@BotFather`
2. Send `/newbot` and follow the instructions
3. Copy the bot token you receive
4. To get your chat ID:
   - Start a chat with your new bot
   - Visit `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
   - Find your chat ID in the response

### Local Development

For local development, use the `.env` file:
1. Copy `.env.example` to `.env`
2. Fill in your actual API keys
3. The `.env` file is already in `.gitignore` to prevent accidental commits

### Important Notes:
- **Never commit** your `.env` file or actual API keys to Git
- The `.env.example` file serves as a template only
- Streamlit Cloud will automatically use secrets from the dashboard
- The app will work locally with `.env` and on cloud with Streamlit secrets
