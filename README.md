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

* `/record`: **Record Logs**. Listens in real-time until `/stop`, or performs an immediate batch export if an end time or message ID is provided. Supports time/count filters, format switching (`txt`, `md`, `both`), and optional summary generation.
* `/summary`: **Instant Summary**. Fetches historical messages and generates key takeaways without exporting full conversation logs.
* `/stop`: **Stop Session**. Wraps up the current recording and delivers logs to the channel, with optional `target_channel` redirection.
* `/models`: **Model Hierarchy**. Inspects the current Gemini fallback chain and API status.
* `/say`: **Echo Message**. Speaks as the bot while concealing the caller, featuring built-in `@everyone` and `@here` mass-ping protection.
* `/add_role` / `/remove_role`: **Role Management**. Dynamically authorizes or revokes roles allowed to operate the bot (Administrator only).

## Gemini Summary Fallback Architecture

We never allow summary tasks to crash halfway. The bot features a built-in multi-tier fallback chain: `gemini-3.8-flash` is our primary powerhouse to digest massive amounts of server chatter rapidly. If API rate limits tighten or connection hiccups occur, the system seamlessly hands the baton over to 3.7 and 3.6 to keep summarizing without missing a single beat.

### Fallback Hierarchy

1. `gemini-3.8-flash` (Primary)
2. `gemini-3.7-flash` (Secondary fallback)
3. `gemini-3.6-flash` (Tertiary fallback)

### Customizing Models

To adjust the fallback lineup or reorder priorities, modify `GEMINI_MODELS` in [`main.py`](main.py):

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
1. **Environment Variables**: Fill in your tokens in `.env`.
2. **Install Dependencies**: `pip install -r requirements.txt`
3. **Start the Bot**: `python main.py`

### Role Permissions
Server Administrators have default access. To authorize other roles, an Administrator can run `/add_role` in Discord. Configuration changes persist in `config.json`.

**License & Copyright**  
Copyright © 2026 flandretw | This project is licensed under the [MIT License](LICENSE).
