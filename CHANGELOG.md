# Changelog

## [1.1.0] - 2025-12-16

### Added
- **Offline Mode**: 
  - Implemented a dedicated "No internet connection" screen with a refresh button.
  - Gracefully intercepts network errors (`ClientException`, `SocketException`) instead of showing generic error text.
- **OS Recognition**: 
  - Added visual detection for **Windows** (`assets/windows.png`) and **Linux** (`assets/linux.png`) servers.
  - Automatically identifies the OS from system info and displays the appropriate icon on the dashboard card.
- **Notification Center**:
  - Added a **Notification Bell** with a **Red Badge** to the Dashboard AppBar to indicate unread alerts.
  - Implemented **Smart Suppression**: Prevents duplicate alerts for the same issue until the user acknowledges (clears) them.
  - Added `POST_NOTIFICATIONS` permission support for Android 13+.

### Changed
- **User Interface**:
  - Removed the redundant "Alerts" option from the user popup menu (now accessible via the AppBar bell).
  - Improved `System` model parsing to extract kernel/OS information.
- **Alert Logic**:
  - `AlertManager` now tracks state (unread/read) to coordinate with the UI badge.
  - Notifications are now requested properly on app startup.

### Fixed
- **Permission Issues**: Resolved `Permission denied` for notifications on newer Android versions.
- **UI Bugs**: Fixed the "question mark" icon issue for Linux systems by updating fallback logic.

---

## [1.0.0] - 2025-12-15

### Added
- **Custom Pull-to-Refresh**: Implemented a custom refresh indicator on the Dashboard that spins the app icon (`assets/icon.png`) during refresh.
- **Startup Alert Checks**: The app now immediately checks system health upon Dashboard load. If a system is *already* overloaded (>80%) when the app starts, an alert is triggered instantly.
- **Safe Initialization**: Added `postFrameCallback` to Dashboard initialization to ensure the UI renders immediately before starting heavy background services.

### Changed
- **Alert Thresholds**: Updated CPU, RAM, and Disk alert thresholds to a uniform **> 80%**.
- **PIN Security Flow**: Restored PIN Code functionality with automatic cleanup on Logout.
- **Alert History**: Capped local alert history to **50 items**.

### Fixed
- **Startup Crash**: Resolved `Unhandled Exception: Widget has been unmounted`.
- **Emulator Freeze**: Mitigated initialization performance issues.
