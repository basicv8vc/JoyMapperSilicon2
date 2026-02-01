# Repository Guidelines

## Project Structure & Module Organization
- `JoyKeyMapper/` is the main macOS app (Swift, AppKit). UI is in storyboards under `JoyKeyMapper/Views/*` and assets in `JoyKeyMapper/Assets.xcassets`.
- `JoyKeyMapperLauncher/` is the helper/login item app with its own assets and storyboards.
- `JoyMapperSilicon.xcodeproj` and `JoyKeyMapper.xcworkspace` are the Xcode project/workspace; use the workspace when CocoaPods is involved.
- `resources/` holds design assets (icons, background). `lang/` contains localized screenshots.
- `scripts/` includes packaging helpers (DMG build, build number).

## Build, Test, and Development Commands
- `pod install` — installs CocoaPods dependencies (JoyConSwift) and generates the workspace.
- `open JoyKeyMapper.xcworkspace` — open in Xcode and run the `JoyKeyMapper` scheme.
- `xcodebuild -workspace JoyKeyMapper.xcworkspace -scheme JoyKeyMapper -configuration Debug` — command-line build (adjust configuration as needed).
- `scripts/build_dmg.sh /path/to/JoyKeyMapper.app` — codesign + notarize + DMG packaging (requires `dmgbuild` and Apple API credentials via `APP_API_*` or prompts).

## Coding Style & Naming Conventions
- Swift uses 4-space indentation; match existing formatting in nearby files.
- Types and protocols use `PascalCase`; methods, properties, and locals use `camelCase`.
- Storyboard identifiers and assets follow existing names (e.g., `Main.storyboard`, `menu_icon`); keep additions consistent.
- No enforced linter/formatter is checked in; prefer minimal, surgical changes.

## Testing Guidelines
- No automated tests or XCTest targets are present in this repo.
- Validate changes manually in Xcode: launch the app, connect a controller, and verify key mapping, mouse movement, and multi-display behavior.
- Document any manual test steps in your PR.

## Commit & Pull Request Guidelines
- Commit history uses short, imperative subjects (e.g., “Fix mouse moving events”, “Update README”).
- PRs should include: a concise description, testing notes, and screenshots for UI or UX changes.
- Link related issues or upstream references when applicable.

## Configuration & Release Notes
- Entitlements live in `JoyKeyMapper/JoyKeyMapper.entitlements` and `JoyKeyMapperLauncher/JoyKeyMapperLauncher.entitlements`; review changes carefully.
- Build numbers and marketing versions are derived from Git tags and commit counts via `scripts/set_build_number.sh`.
