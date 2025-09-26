from telegram import Update
from telegrak import.ext import ApplicationBuilder,CommandHealder,MessageHealder,filters import openai
openai.api_key=8128848449:AAFwP_39VkWG1FTPiuWVyprE-E7_-Js43E4
async def handle_message(update: Update, context):
    user_input = update.message.text
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": user_input}]
)
    reply = response.choices[0].message.content
    await update.message.reply_text(reply)

app = ApplicationBuilder().token("TOKEN_BOT_KAMU").build()
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
app.run_polling()
