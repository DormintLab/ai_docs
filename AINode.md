
AI Node is 
- UI configurator
- Handles (inputs / outputs)
- Code template

## UI configuration
```
SequenceCard([
  TextCard("bot_token",
           help="Bot token from BotFather bot"),
  TextCard("message_filter",
           help="Describe what messages to process",
           is_area=True),
])
```

## Handles
```
Inputs: $OUTPUT_MESSAGE
Outputs: $MESSAGE
```

## Code template

```
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes


async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    user_message = update.message.text
    $EMIT($MESSAGE, user_message)
    await update.message.reply_text($OUTPUT_MESSAGE)


def main() -> None:
    bot_token = $BOT_TOKEN
    application = Application.builder().token(bot_token).build()
    application.add_handler(MessageHandler($MESSAGE_FILTER, handle_message))

    # Запускаем бота
    application.run_polling()

if __name__ == "__main__":
    main()
```
