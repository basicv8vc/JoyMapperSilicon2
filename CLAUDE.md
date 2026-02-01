# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

JoyMapperSilicon is a native macOS app (Swift 5.0) that maps Nintendo Joy-Con and Pro Controller inputs to keyboard/mouse events. It supports Apple Silicon and Intel Macs running macOS 11.0+. The app runs as a menu bar utility (LSUIElement) with per-application key mapping configurations.

## Build Commands

```bash
# Install dependencies (first time or after Podfile changes)
pod install

# Build via command line
xcodebuild -workspace JoyKeyMapper.xcworkspace -scheme "JoyMapperSilicon" -configuration Release

# Open in Xcode (recommended for development)
open JoyKeyMapper.xcworkspace
# Cmd+B to build, Cmd+R to run
```

**Important:** Always use the `.xcworkspace` file (not `.xcodeproj`) because of CocoaPods integration.

## Creating Distribution DMG

```bash
./scripts/build_dmg.sh /path/to/built/JoyMapperSilicon.app
```

Requires Apple Developer ID credentials and notarization API keys.

## Architecture

### Two Targets

1. **JoyMapperSilicon** - Main application with controller mapping UI and logic
2. **JoyKeyMapperLauncher** - Helper app for auto-launch at login functionality

### Key Source Directories (JoyKeyMapper/)

- **Views/** - UI components organized by feature (AppList, ControllerList, KeyConfigView, KeyMapList, AppSettings)
- **DataModels/** - Core Data entities and managers for persisting controller/key configurations
- **Misc/** - Utilities including key conversion helpers (Utils.swift)

### Core Components

- `AppDelegate.swift` - App lifecycle, status bar setup, controller connection handling
- `ViewController.swift` - Main window controller managing feature views
- `DataManager.swift` - Core Data container and fetch operations
- `GameController.swift` - Wrapper for JoyCon/Pro Controller communication

### Dependencies

- **JoyConSwift** (v0.2.1 via CocoaPods) - JoyCon/Pro Controller communication library
- **Core Data** - Persistent storage for controller and mapping configurations
- **InputMethodKit** - Keyboard/mouse event generation

### Localization

Supports English and Japanese via `.lproj` directories in Views/ and Misc/.
