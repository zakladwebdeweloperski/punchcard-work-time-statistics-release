# Changelog

All notable changes to the "PUNCHCARD - Work Time Statistics" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-30

### Added
- Initial release of PUNCHCARD - Work Time Statistics
- Per-project time tracking with automatic AFK detection
- Global statistics aggregation across all projects
- Metrics tracking:
  - Total active time
  - Lines added/deleted
  - Characters added/deleted
  - Keystrokes count
  - Session history
- Interactive WebView statistics panel with Chart.js visualization
- Daily, weekly, and monthly trend charts
- Status bar integration showing session and daily time
- VS Code Settings Sync support for cross-machine sync
- Export statistics to JSON
- Reset project or all statistics
- Configurable AFK threshold (default: 5 minutes)
- Configurable auto-start tracking on workspace open

### Commands
- `workTimer.showStats` - Open statistics WebView
- `workTimer.resetProject` - Reset current project statistics
- `workTimer.resetAll` - Reset all statistics
- `workTimer.exportData` - Export data to JSON file

### Configuration
- `workTimer.afkThreshold` - AFK detection threshold in milliseconds
- `workTimer.trackOnStartup` - Enable/disable auto-start tracking

## [Unreleased]

### Planned
- Weekly/monthly summary emails
- Pomodoro timer integration
- Team statistics (optional opt-in)
- Customizable charts and dashboard
- Goal setting and achievements
- Integration with external time tracking services
