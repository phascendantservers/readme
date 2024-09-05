# Backup Automation Tool

This suite includes `watch_dog.exe` and `go-bot-discord.exe` for managing and automating backups for ARK: Survival Ascended maps. `watch_dog.exe` is responsible for starting and monitoring `go-bot-discord.exe`, which handles the actual backup operations.

## Prerequisites

- Windows operating system
- `watch_dog.exe` and `go-bot-discord.exe` executables
- A Discord bot token
- MySQL database credentials
- Relevant ARK: Survival Ascended backup directories

## Setup Instructions

### 1. Configure Environment Variables

1. **Edit the `.env` File**: Provide your Discord bot token and MySQL database credentials.

   Example `.env` file:

   ```plaintext
   DISCORD_TOKEN=your_discord_bot_token
   ALLOWED_CHANNEL_ID=your_discord_channel_id

   MYSQL_USER=your_mysql_user
   MYSQL_PASSWORD=your_mysql_password
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_DATABASE=ark
   ```

   - Replace `your_discord_bot_token` with your actual Discord bot token.
   - Replace `your_discord_channel_id` with the ID of the Discord channel where the bot will send messages.
   - Update MySQL credentials (`MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_HOST`, `MYSQL_PORT`, `MYSQL_DATABASE`) with your actual database information.

### 2. Configure Backup Settings

1. **Edit the `config.json` File**: Define the backup paths, file types, and intervals for each ARK map. This file is used by `go-bot-discord.exe` to manage backups.

   Example `config.json` file:

   ```json
   [
       {
           "map": "TheIsland",
           "zip_dir": "C:/Users/YourUsername/Desktop/ark_backups/TheIsland",
           "extract_dir": "C:/Users/YourUsername/Desktop/ark_saves/TheIsland",
           "overwrite": true,
           "extensions": [".arktributetribe", ".arkprofile", ".profilebak", ".arktribe", ".tribebak"],
           "filenames": ["TheIsland_WP.ark"],
           "backup_interval": 30,
           "retention_days": 30
       },
       {
           "map": "ScourchedEarth",
           "zip_dir": "C:/Users/YourUsername/Desktop/ark_backups/ScourchedEarth",
           "extract_dir": "C:/Users/YourUsername/Desktop/ark_saves/ScorchedEarth",
           "overwrite": true,
           "extensions": [".arktributetribe", ".arkprofile", ".profilebak", ".arktribe", ".tribebak"],
           "filenames": ["ScorchedEarth_WP.ark"],
           "backup_interval": 30,
           "retention_days": 30
       },
       {
           "map": "TheCenter",
           "zip_dir": "C:/Users/YourUsername/Desktop/ark_backups/TheCenter",
           "extract_dir": "C:/Users/YourUsername/Desktop/ark_saves/TheCenter",
           "overwrite": true,
           "extensions": [".arktributetribe", ".arkprofile", ".profilebak", ".arktribe", ".tribebak"],
           "filenames": ["TheCenter_WP.ark"],
           "backup_interval": 30,
           "retention_days": 30
       },
       {
           "map": "TheIslandNew",
           "zip_dir": "C:/Users/YourUsername/Desktop/ark_backups/TheIslandNew",
           "extract_dir": "C:/Users/YourUsername/Desktop/ark_saves/TheIslandNew",
           "overwrite": true,
           "extensions": [".arktributetribe", ".arkprofile", ".profilebak", ".arktribe", ".tribebak"],
           "filenames": ["TheIslandNew_WP.ark"],
           "backup_interval": 30,
           "retention_days": 30
       }
   ]
   ```

   - Replace the dummy paths with the actual paths on your system where backups and saves are stored.
   - Adjust the `backup_interval` (in minutes) and `retention_days` according to your needs.

### 3. Running the Application

1. **Start `watch_dog.exe`**: This utility handles starting and monitoring `go-bot-discord.exe`. Running `watch_dog.exe` will automatically launch `go-bot-discord.exe` and manage its operation.

## Discord Bot Commands

Once the bot is running, you can use the following commands in the Discord channel where the bot is active:

- **`/search playername`**: Searches for the specified player and shows their EOS ID.
  
  Example:
  ```
  /search player123
  ```

- **`/list mapname eos.arkprofile`**: Lists the backup files (`.zip`) that contain the specified `eos.arkprofile` for the given map.

  Example:
  ```
  /list TheIsland eos.arkprofile
  ```

- **`/restore mapname back.zip eos.arkprofile`**: Restores the `eos.arkprofile` from the specified backup zip file for the given map.

  Example:
  ```
  /restore TheIsland backup_2024-09-05.zip eos.arkprofile
  ```

## Notes

- **File Extensions**: The `extensions` field in `config.json` specifies which file types to include in the backup.
- **Backup Interval**: The `backup_interval` defines how often backups are performed, in minutes.
- **Retention Days**: The `retention_days` specifies how long backups are kept before being deleted.

## Troubleshooting

- **`go-bot-discord.exe` Not Starting**: Ensure that `watch_dog.exe` is running and has the correct configuration in `.env` and `config.json`.
- **`watch_dog.exe` Issues**: Verify that `watch_dog.exe` is correctly set up and has necessary permissions to run `go-bot-discord.exe`.
- **Discord Bot Issues**: Confirm the bot token and channel ID are correct, and that the bot has the necessary permissions.

