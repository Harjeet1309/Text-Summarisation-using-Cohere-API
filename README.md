# 🧠 Telegram Text Summarizer Bot using Cohere API

This bot listens to your messages on Telegram and sends back a concise summary using the Cohere AI API.

---

## 🔧 Features

- Summarizes any text you send it.
- Uses Cohere’s `summarize-xlarge` model.
- Built using Python with `telebot` and `cohere` packages.
- Can be deployed anywhere Python is supported.

---

## 🛠 Requirements

Install these using pip:

```bash
pip install pyTelegramBotAPI cohere
```

---

## 🔑 Setup

1. **Telegram Bot Token**  
   - Get it from [@BotFather](https://t.me/BotFather) on Telegram.
   - Replace it in the `TELEGRAM_BOT_TOKEN` variable.

2. **Cohere API Key**  
   - Get it from [https://dashboard.cohere.com](https://dashboard.cohere.com).
   - Replace it in the `COHERE_API_KEY` variable.

---

## 🚀 Running the Bot

Just run:

```bash
python bot.py
```

Now message your bot and it will reply with a summary.

---

## 🧪 Test It

Send this long paragraph:

> Climate change refers to long-term alterations in temperature, precipitation, wind patterns, and other elements of the Earth's climate system. While climate change can occur naturally, scientific evidence overwhelmingly shows that human activities...

And get a neat, accurate summary in reply.

---

## 📂 `bot.py` — Full Python Code

```python
# bot.py

# ===== Dependencies =====
# pip install pyTelegramBotAPI cohere

import telebot
import cohere

# ===== API KEYS =====
TELEGRAM_BOT_TOKEN = "YOUR_TELEGRAM_BOT_TOKEN_HERE"
COHERE_API_KEY = "YOUR_COHERE_API_KEY_HERE"

# ===== Initialize Clients =====
bot = telebot.TeleBot(TELEGRAM_BOT_TOKEN)
co = cohere.Client(COHERE_API_KEY)

# ===== Handle Messages =====
@bot.message_handler(func=lambda message: True)
def handle_message(message):
    user_text = message.text.strip()

    if not user_text:
        bot.reply_to(message, "Please send some text to summarize.")
        return

    try:
        response = co.summarize(
            text=user_text,
            length='auto',
            format='auto',
            model='summarize-xlarge',
            additional_command='',
            temperature=0.3,
        )

        summary = response.summary
        bot.reply_to(message, f"📝 Summary:\n{summary}")

    except Exception as e:
        print(f"[ERROR] {str(e)}")
        bot.reply_to(message, "⚠️ Error: Could not summarize the message.")

# ===== Start Bot =====
print("🤖 Bot is polling...")
bot.polling()
```

---

## 🛡️ Important Notes

- Do **not** share your API keys publicly.
- This bot is suitable for basic summarization tasks.
- For more advanced control, you can tweak Cohere’s parameters or add logging and monitoring.

---

## 👨‍💻 Author

Engineered by Harjeet Gudde, for humans and machines alike.

