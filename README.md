# PUNCHCARD - Work Time Statistics

Track active coding time, keystrokes, and code metrics across projects with automatic AFK detection.

![PUNCHCARD Extension](https://img.shields.io/badge/VS%20Code-Extension-blue)
![Version](https://img.shields.io/badge/version-1.0.0-green)

## Features

### 🕐 Time Tracking
- **Per-Project Tracking**: Track time spent on each workspace/project individually
- **Global Statistics**: View combined statistics across all your projects
- **Automatic AFK Detection**: Pauses tracking when you're away (configurable threshold)
- **Session Management**: Automatically starts new sessions when you return from AFK

### 📊 Metrics Tracked
- Total active coding time
- Lines added and deleted
- Characters added and deleted  
- Total keystrokes
- Number of sessions
- Last active timestamp

### 📈 Visualization
- Interactive charts powered by Chart.js
- Daily, weekly, and monthly trends
- Keystrokes distribution by project
- Lines changed comparison
- Real-time session timer in status bar

### 🔄 Data Sync
- Uses VS Code's built-in Settings Sync
- Your statistics sync automatically across machines
- No external services or accounts required

## Installation

1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X`)
3. Search for "PUNCHCARD - Work Time Statistics"
4. Click Install

Or install from command line:
```bash
code --install-extension punchcard.punchcard-work-time-statistics
```

## Usage

### Status Bar
The extension shows your current session time and today's total time in the status bar. Click it to open the full statistics panel.

![Status Bar](images/statusbar.png)

### Commands
Open the Command Palette (`Ctrl+Shift+P`) and type:

| Command | Description |
|---------|-------------|
| `PUNCHCARD: Show Statistics` | Open the statistics WebView panel |
| `PUNCHCARD: Reset Current Project Statistics` | Reset stats for current workspace |
| `PUNCHCARD: Reset All Statistics` | Reset all tracked statistics |
| `PUNCHCARD: Export Data to JSON` | Export all data to a JSON file |

### Statistics Panel
The statistics panel shows:
- **Summary Cards**: Session time, today's time, total time, keystrokes, lines changed, project count
- **Overview Tab**: Daily coding time chart
- **Projects Tab**: Detailed breakdown by project
- **Trends Tab**: Keystrokes and lines changed charts

## Configuration

Configure the extension in your `settings.json`:

```json
{
  "workTimer.afkThreshold": 300000,
  "workTimer.trackOnStartup": true
}
```

### Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `workTimer.afkThreshold` | number | `300000` | Time in milliseconds before user is considered AFK (default: 5 minutes) |
| `workTimer.trackOnStartup` | boolean | `true` | Start tracking time automatically when VS Code opens |

## How AFK Detection Works

The extension monitors your activity through:
- Text editing (typing)
- Cursor movement
- Scrolling
- File switching

When no activity is detected for the configured threshold (default 5 minutes), tracking pauses automatically. When you resume activity, a new session begins.

## Data Structure

Your statistics are stored in VS Code's globalState and synced via Settings Sync:

```json
{
  "projects": {
    "project-name": {
      "totalTime": 0,
      "linesAdded": 0,
      "linesDeleted": 0,
      "charactersAdded": 0,
      "charactersDeleted": 0,
      "keystrokes": 0,
      "sessions": [],
      "lastActive": 0
    }
  },
  "totalTimeAllProjects": 0,
  "totalKeystrokes": 0
}
```

## Privacy

- **No external services**: All data stays within VS Code
- **No tracking**: We don't collect any personal information
- **Local storage**: Data is stored in VS Code's globalState
- **Settings Sync**: If enabled, data syncs through Microsoft's Settings Sync

## Development

### Building from Source

```bash
# Clone the repository
git clone https://github.com/zakladwebdeweloperski/punchcard-work-time-statistics-release.git
cd punchcard-work-time-statistics

# Install dependencies
npm install

# Compile
npm run compile

# Package extension
npm run vsce:package
```

### Running Tests

```bash
# Compile tests
npm run compile-tests

# Run tests
npm test
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release history.

## Support

If you encounter any issues or have feature requests, please [open an issue](https://github.com/zakladwebdeweloperski/punchcard-work-time-statistics-release/issues) on GitHub.

---

Made with ❤️ for developers who want to track their coding time
