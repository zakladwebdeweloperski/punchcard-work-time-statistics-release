# Changelog

All notable changes to the "PUNCHCARD - Work Time Statistics" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-02-04

### Added
- Individual stat reset buttons for fine-grained control
- Global summary stat reset buttons (hover to reveal)
- Import data from JSON command for manual data restoration
- Sync status checking command with detailed requirements
- Intelligent sync merge handling to prevent data loss
- Bulk operation detection (paste, format, git operations) vs typed input
- Separate tracking of typed lines vs bulk/pasted lines

### Fixed
- **CRITICAL**: Keystroke counting now tracks actual key presses, not character count
- **CRITICAL**: Pasted content no longer inflates keystroke count
- **CRITICAL**: Fixed sync race condition where local data could overwrite synced data
- Line counting now distinguishes between typed input and bulk operations
- Sync now properly merges data from multiple devices without loss
- Configuration keys changed from `workTimer.*` to `punchcardWorkTimer.*`

### Changed
- Enhanced statistics display with separate "Typed" vs "Bulk/Paste" metrics
- Improved sync reliability with delayed merge checks
- Added comprehensive logging for sync debugging
- Session deduplication to prevent counting same sessions twice

### Commands Added
- `workTimer.importData` - Import and merge data from JSON file
- `workTimer.checkSync` - Check sync status and requirements

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
