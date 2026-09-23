<p align="center">
  <img src="LanLanLu_Profile.webp" alt="LanLanLu Discord Bot Icon" width="128">
</p>

# LanLanLu Discord Bot

[English](README.md) | [臺灣正體中文](README-zh_TW.md)

> **Disclaimer**  
> This project was forged using **Gemini "Vibe Coding"**, fueled by AI magic and excessive amounts of digital fries. **Proceed with caution**! If the UI starts dancing or the code looks like a magical incantation, don't worry—it's just the vibe.

"I want every single word you say!!"

## What is this chaotic masterpiece?

From the LanLanLu universe comes **LanLanLu** — a crazy bot dedicated to kidnapping your conversation logs!

## Crazy Magical Commands

**Note**: Only users with the native **Administrator** permission, or those granted access via `/add_role`, can operate these commands.

* **`/record`**: Records channel conversations. If no end point is specified, it continuously listens for incoming messages until `/stop` is called; if an end time or message ID is provided, it performs a batch export for that range. Supports filtering by time, message ID, or message limit, and allows exporting in `txt` (default), `md`, or `both` formats with optional AI summaries.
* **`/summary`**: Fetches historical messages within a specified range and generates an AI summary without creating a full conversation log. Supports time, message ID, or count limits, and outputs in `txt`, `md`, or `both` formats.
* **`/stop`**: Stops the current recording session and uploads the log and AI summary to the current channel, with an optional `target_channel` parameter to send files to another channel.
* **`/models`**: Displays current Gemini fallback model priority and API key status.
* **`/say`**: Sends a message as the bot while hiding the caller's identity (mass pings like `@everyone` and `@here` are automatically blocked).
* **`/add_role` & `/remove_role`**: Adds or removes a role from the authorized command list (Administrator permission required).

## Gemini AI Summary & Model Configuration

This bot integrates the official Google Gemini SDK (`google-genai`) with automatic multi-tier fallback mechanisms.

### Default Models & Fallback Mechanism

Summaries are generated using `gemini-3.8-flash` by default. If rate limits or API errors occur, the bot automatically degrades to the next fallback model in line:

1. `gemini-3.8-flash` (Primary)
2. `gemini-3.7-flash` (Secondary fallback)
3. `gemini-3.6-flash` (Tertiary fallback)

### Customizing Models

To adjust the models or their priority order, edit the `GEMINI_MODELS` list in [`main.py`](main.py):

```python
GEMINI_MODELS = [
    'gemini-3.8-flash',
    'gemini-3.7-flash',
    'gemini-3.6-flash'
]
```

## Setup & Usage

### Method 1: Deployment via Docker (Recommended)
Ideal for 24/7 server environments with built-in auto-restart functionality.
1. **Environment Variables**: Create a `.env` file with your tokens:
   ```env
   DISCORD_TOKEN=Your_Discord_Token
   GEMINI_API_KEY=Your_Gemini_API_Key
   ```
2. **Initialize Config**: Create an empty file to prevent volume mount issues: `touch config.json`
3. **Start the Bot**: Run `docker compose up -d`

### Method 2: Local Execution
1. **Environment Variables**: Fill in your tokens in the `.env` file.
2. **Install Dependencies**: `pip install -r requirements.txt`
3. **Start the Bot**: `python main.py`

### Role Permissions
Server Administrators have default access. To authorize other roles, an Administrator must use the `/add_role` command in Discord. The configurations will be saved locally in `config.json`.

**License & Copyright**  
Copyright © 2026 flandretw | This project is licensed under the [MIT License](LICENSE).
