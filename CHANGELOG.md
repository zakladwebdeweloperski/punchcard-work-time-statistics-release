# Changelog

All notable changes to the "PUNCHCARD - Work Time Statistics" extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.3.0] - 2026-02-17

### Added
- **Period-based statistics**: All metrics (time, keystrokes, lines, characters) are now aggregated by day and can be viewed by period
- **Period selector tabs**: Switch between Today, This Week, This Month, and All Time in the statistics panel
- Summary cards and project stats update dynamically when switching periods
- Daily metrics tracking (`dailyMetrics` map per project) for accurate period breakdowns
- **Sync & Debug Log panel**: Collapsible log viewer built into the statistics panel
  - Machine ID, save count, sync events, merge count, sessions by machine
  - Log filtering by category (sync, storage, tracker, session, merge, init) and level (error, warn, info, debug)
  - Force Sync Check and Clear Logs buttons
- New commands: `PUNCHCARD: Force Sync Check` and `PUNCHCARD: Clear Sync Log`

### Changed
- Statistics panel now defaults to All Time view with instant client-side period switching
- Period badge on Projects section header shows currently selected time range
- Daily metrics are merged across machines using per-field Math.max strategy

### Fixed
- Period tab switching no longer causes visual jerk (transparent borders, no font-weight reflow)

## [1.2.1] - 2026-02-12

### Fixed
- **CRITICAL**: Fixed cross-machine synchronization losing time data
  - `checkForSyncedData` now properly detects new sessions even when local totalTime is higher
  - `totalTime` is now derived from merged sessions instead of using Math.max, preventing data loss
  - `mergeSessions` now keeps the session with longer duration on conflict (more up-to-date)
  - `importData` now properly deduplicates sessions instead of concatenating them
- Sessions are now the source of truth for time tracking accuracy
- Added 7 comprehensive tests for cross-machine sync scenarios

## [1.2.0] - 2026-02-08

### Changed
- **DEVELOPMENT**: Migrated test suite from Mocha to Vitest for improved performance and developer experience
- All 72 unit tests now run 3-5x faster with Vitest's optimized test runner
- Improved test command with watch mode: `npm run test:watch`

### Improved
- Test infrastructure is now more maintainable with Vitest's modern tooling
- Better test output formatting and error reporting
- Faster test feedback during development

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
