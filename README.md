# MyAlexandria Telegram Bot

A Telegram bot that aggregates blog posts from MyAlexandriya.blogspot.com and delivers them to subscribers. The bot includes both interactive subscription management and automatic post notification features.

## Overview

MyAlexandria is a Python-based Telegram bot system designed to:
- Parse blog posts from a Blogspot blog
- Manage user subscriptions via Telegram
- Automatically notify users of new posts
- Provide on-demand access to recent blog content

## Features

- **Interactive Bot** - Users can subscribe/unsubscribe and request recent posts on demand
- **Automatic Notifications** - Background service monitors for new posts and broadcasts them to subscribers
- **User Management** - Persistent user list stored locally
- **Post Retrieval** - Multiple options to view latest 1, 5, or 10 posts
- **HTML Formatting** - Rich Telegram message formatting with clickable post links

## Project Structure

```
MyAlexandria/
├── Parsing.py          # Web scraping module for blog posts
├── Telegram.py         # Interactive Telegram bot for user interactions
├── Telegramsend.py     # Background service for automatic notifications
├── TelegramToken.py    # Configuration (not included - see Setup)
└── Users.txt           # Persistent user list (generated at runtime)
```

## Requirements

- Python 3.x
- `pyTelegramBotAPI` (telebot)
- `beautifulsoup4`
- `urllib` (built-in)

## Setup

1. **Install dependencies:**
   ```bash
   pip install pyTelegramBotAPI beautifulsoup4
   ```

2. **Configure Telegram Token:**
   Create a `TelegramToken.py` file in the project root:
   ```python
   Token = 'YOUR_TELEGRAM_BOT_TOKEN'
   ```
   Get your bot token from [BotFather](https://t.me/botfather) on Telegram.

3. **Create initial Users.txt:**
   ```bash
   echo "0" > Users.txt
   ```

## Usage

### Running the Interactive Bot
```bash
python Telegram.py
```
This starts the interactive bot that responds to user commands.

### Running the Background Notification Service
```bash
python Telegramsend.py
```
This monitors the blog for new posts and sends them to all subscribers (runs indefinitely).

**Note:** For production, run both services simultaneously using separate processes or systemd services.

## Bot Commands

| Command | Description |
|---------|-------------|
| `/start` | Subscribe to news updates |
| `/stop` | Unsubscribe from updates |
| `/last` | Get the latest post |
| `/help` | Show available commands |
| `/status` | Check if server is running |
| `Выдать последние 5` | Get the 5 most recent posts |
| `Выдать последние 10` | Get the 10 most recent posts |
| `Krasava` | Easter egg response |

## Architecture

### Parsing.py
Handles web scraping from the blog:
- Uses BeautifulSoup to parse HTML
- Extracts post title, content, and URL
- Returns structured post data as dictionaries
- Handles errors gracefully

### Telegram.py
Interactive bot that:
- Listens for incoming messages
- Manages user subscriptions
- Responds to commands
- Maintains a persistent user list in `Users.txt`
- Provides on-demand post retrieval

### Telegramsend.py
Background service that:
- Periodically checks the blog for new posts (25-second intervals)
- Detects changes in content
- Broadcasts new posts to all subscribed users
- Logs notification activity

## Configuration Notes

- Blog source: `https://myalexandriya.blogspot.com/`
- Check interval: 25 seconds (in Telegramsend.py)
- User data format: First line is user count, followed by user IDs (one per line)
- Messages use HTML formatting for rich text

## Troubleshooting

- **Module not found errors:** Ensure all dependencies are installed
- **Connection errors:** Check internet connectivity and Telegram API status
- **Token errors:** Verify `TelegramToken.py` contains a valid token
- **No messages sent:** Ensure both `Telegram.py` and `Telegramsend.py` are running

## License

Not specified

## Author

Yaroslav
