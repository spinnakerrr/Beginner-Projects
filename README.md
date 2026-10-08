# Hiatus Projects
Aug-09-2026 — Aug-16-2026 Misc Tests/Attempts/Ideas


# CorgiBot 2.1 — 21st Century Romances

CorgiBot is a Telegram bot that shares romantic and literary writing, prompts, haiku, oracle messages, and corgi-themed transmissions. It can also draw from a personal poetry archive stored in a separate text file.

## Features

- Telegram commands for individual writing categories.
- `/random` mixes several categories, including the personal poetry archive.
- `my_poetry.txt` can be edited without changing the Python source. Separate pieces with a line containing `---`.
- Recent-item tracking avoids repeats among the latest 15 items per category while the bot is running.
- Optional daily Telegram posts at 09:00, 19:00, and 23:00 using JobQueue.

## Commands

| Command | Description |
| --- | --- |
| `/start` | Welcome message and command list |
| `/help` | Command descriptions |
| `/random` | Random item from several categories, including personal poetry |
| `/poetry` | Random item from `my_poetry.txt` |
| `/oracle` | Oracle message |
| `/weird` | Unusual writing prompt |
| `/romance` | Romantic fragment |
| `/autism` | Neurodivergent romance writing |
| `/longdistance` | Long-distance writing |
| `/literary` | Literary fragment |
| `/midnight` | Melancholy writing |
| `/prompt` | Writing prompt |
| `/haiku` | Haiku |
| `/manifesto` | 21CR manifesto |
| `/corgi` | Corgi-themed transmission |

Digital intimacy and physical closeness are included in `/random`, but do not have separate commands in the current source.

## Requirements

- Python 3.9 or newer
- `python-telegram-bot` with the JobQueue extra

Install the dependency:

```bash
python -m pip install "python-telegram-bot[job-queue]"
```

## Add personal writing

Create `my_poetry.txt` beside `bot.py`. Put each piece in the file and separate entries with a line containing `---`:

```text
A first piece can span multiple lines.
---
A second piece goes here.
```

If `my_poetry.txt` is missing or empty, `/poetry` returns a notice. The bot reads the archive when the command is used.

## Configure and run

The current `bot.py` contains placeholders for the Telegram bot token and chat ID. Create a bot through BotFather and keep its token private. Before using real credentials or publishing the project, update the code to read the token and chat ID from environment variables. Keep the actual values in a local `.env` file excluded by `.gitignore`.

Run the bot with:

```bash
python bot.py
```

Then open the bot in Telegram and send `/start`.

CorgiBot uses polling, so the Python process must remain running to receive commands and send scheduled posts. Scheduled posts require the JobQueue extra and a valid destination chat where the bot is allowed to post. The source schedules posts at 09:00, 19:00, and 23:00, but does not set a timezone; the effective timezone depends on the runtime and library configuration.

## Before publishing

Never commit a real bot token. If a token has already been shared or committed, revoke it with BotFather and create a new one.

The current source stores its token and chat ID directly in `bot.py`. Its chat ID placeholder is a non-empty string, so the check for `CHAT_ID is None` does not disable scheduled jobs as intended. Configure a real chat ID or fix that logic before running the scheduled jobs.

Decide whether `my_poetry.txt` contains writing you want to make public. The `.gitignore` below leaves it trackable by default; uncomment its optional ignore line if the archive should stay local.

## First GitHub upload

1. Put `bot.py`, `README.md`, `.gitignore`, and any other files you intend to share in one project folder.
2. Check the folder for `.env`, real credentials, virtual environments, and any private writing you don’t want to publish.
3. On GitHub, select **New repository**, choose a name, and choose public or private visibility. Since you already have a README, don’t ask GitHub to add another one.
4. For a beginner-friendly upload, use GitHub Desktop. Choose **Add an Existing Repository** if the folder is already a Git repository, or **Create a New Repository** if it isn’t. Review the files, commit them, then choose **Publish repository**.

You can also create the repository on GitHub and use **Add file → Upload files**. Review the file list before committing.

## License

No license file was present in the inspected project. Add a license after deciding how others may use, modify, and redistribute the code and writing.
