# PUNCHCARD - Work Time Statistics: Developer & User Instructions

## Overview

PUNCHCARD is a VS Code extension that tracks your active coding time, keystrokes, and code metrics across projects with automatic AFK (Away From Keyboard) detection. All data syncs automatically across machines when VS Code Settings Sync is enabled.

---

## Features

### Time Tracking
- Tracks active time per project (workspace)
- Tracks global time across all projects
- Automatic AFK detection with configurable threshold (default: 5 minutes)
- Activities monitored: text editing, cursor movement, scrolling, file switching

### Metrics Tracked
- **Total active time** (in milliseconds, displayed as HH:MM:SS)
- **Lines added/deleted**
- **Characters added/deleted**
- **Total keystrokes**
- **Sessions** (start time, end time, duration)
- **Last active timestamp**

### Data Visualization
- WebView panel with Chart.js charts
- Daily, weekly, and monthly trends
- Per-project breakdown
- Doughnut chart showing time distribution by project

### Data Sync
- Uses VS Code's built-in Settings Sync via `globalState.setKeysForSync()`
- No external CDN or cloud services required
- Data syncs automatically between machines when Settings Sync is enabled

---

## Commands

| Command | Shortcut | Description |
|---------|----------|-------------|
| `PUNCHCARD: Show Statistics` | Click status bar | Opens the statistics WebView panel |
| `PUNCHCARD: Reset Current Project Statistics` | - | Resets statistics for the current workspace |
| `PUNCHCARD: Reset All Statistics` | - | Resets ALL tracked statistics |
| `PUNCHCARD: Export Data to JSON` | - | Exports all data to a JSON file |

---

## Configuration

Add to your `settings.json`:

```json
{
  "workTimer.afkThreshold": 300000,
  "workTimer.trackOnStartup": true
}
```

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `workTimer.afkThreshold` | number | 300000 | AFK threshold in milliseconds (5 min = 300000) |
| `workTimer.trackOnStartup` | boolean | true | Auto-start tracking when VS Code opens |

---

## How It Works

### Activity Detection
The extension listens to these VS Code events:
- `onDidChangeTextDocument` - Text editing
- `onDidChangeTextEditorSelection` - Cursor movement
- `onDidChangeTextEditorVisibleRanges` - Scrolling
- `onDidChangeActiveTextEditor` - File switching

### AFK Detection
- A timer checks every second
- If no activity detected for `afkThreshold` milliseconds, user is marked as AFK
- Current session is finalized when going AFK
- New session starts when activity resumes

### Session Management
- Each period of activity is recorded as a session
- Sessions include: start time, end time, duration
- Sessions allow accurate time-of-day and trend analysis

---

## Status Bar

The status bar item shows:
- **Session time**: Current session duration (HH:MM:SS)
- **Today's time**: Total time tracked today
- **AFK indicator**: Shows "AFK" when no activity detected

Click the status bar to open the statistics panel.

---

## Data Storage

Data is stored in VS Code's `globalState`:
- Storage key: `punchcard-work-stats`
- Automatically synced when Settings Sync is enabled

### Data Structure
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
      "sessions": [
        {
          "startTime": 1234567890,
          "endTime": 1234567899,
          "duration": 9000
        }
      ],
      "lastActive": 1234567899
    }
  },
  "totalTimeAllProjects": 0,
  "totalKeystrokes": 0
}
```

---

## Tips

1. **Let it run**: The extension tracks automatically - just code!

2. **Use Settings Sync**: Enable VS Code Settings Sync to keep statistics across machines.

3. **Export regularly**: Use "Export Data to JSON" for backups.

4. **Adjust AFK threshold**: If you take frequent short breaks, increase the threshold.

5. **Check trends**: Use the weekly/monthly charts to identify your most productive times.

6. **Status bar click**: Fastest way to check your stats is clicking the status bar.

---

## Troubleshooting

### Statistics not syncing
- Ensure VS Code Settings Sync is enabled
- Check Settings Sync settings to include extensions

### Time not tracking
- Make sure `workTimer.trackOnStartup` is `true`
- Check if you have a workspace/folder open
- Activity must occur within a text editor

### WebView not loading charts
- Check your internet connection (Chart.js is loaded from CDN)
- Try closing and reopening the statistics panel

---

## Development

### Building
```bash
npm install
npm run compile   # Build once
npm run watch     # Watch mode
npm run package   # Production build
```

### Testing
```bash
npm test          # Run integration tests
npm run test:unit # Run unit tests
```

### Packaging
```bash
npm run vscode:prepublish
npm run vsce:package  # Creates .vsix file
npm run vsce:publish  # Publish to marketplace
```

---

## Updating These Instructions

When making changes to the extension:

1. **New features**: Add to Features section and Commands table if applicable
2. **New settings**: Add to Configuration table
3. **Changed behavior**: Update relevant sections
4. **Bug fixes**: Add to Troubleshooting if user-facing
5. **API changes**: Update Data Structure section

Keep instructions concise and actionable. Include examples where helpful.

---

## License

MIT License - See LICENSE file for details.
