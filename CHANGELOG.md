# Changelog

All notable changes to **SG EV Charging (Android)** are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this
project uses Android versioning: each release lists its `versionName (versionCode)`. The
**Added/Changed/Fixed** notes for the latest release are mirrored into the Google Play
**release notes** at submission time.

## [Unreleased]

- _Nothing yet._

## [1.1] — 2026-06-21 · versionCode 2

### Added
- Bottom navigation with **Map**, **Feedback**, and **About** tabs.
- **Feedback** tab: a Title field, a Message field, and a "Send via WhatsApp" button that
  opens a chat to +65 8866 6375 with the composed message.
- **About** tab: app description, Developer card (Tertiary Infotech Academy Pte. Ltd. +
  tertiaryinfotech.com), a Data-source card, app Version, and a tappable link to the official
  **LTA DataMall** source.
- Visible "Data source: LTA DataMall" attribution link on the main search panel.

### Fixed
- **Google Play rejection (Misleading Claims — Missing Source Link for Government
  Information):** added a clear, accessible link to the official LTA DataMall source both in
  the store listing full description and inside the app, with an independence disclaimer.

### Play submission
- Closed testing track **Alpha**, testers: **All Testers** list, country: **Singapore**.
- Submitted for review on 2026-06-21.

## [1.0] — 2026-06-21 · versionCode 1

### Added
- Initial native Android port of the SwiftUI iOS app (Kotlin + Jetpack Compose + Material 3).
- Find nearby EV charging points in Singapore: search by postal code or place, detect current
  location and rank by distance, live available/occupied/unavailable connector states,
  operator/plug/power/last-updated metadata, Google Maps directions, and a map-first UI with
  nearby station chips.
- Data from LTA DataMall (`EVChargingPoints` + `EVCBatch`); Google Maps Compose; Fused
  Location Provider; platform Geocoder.

### Play submission
- First closed testing submission. **Rejected** under the Misleading Claims policy for a
  missing government-data source link (fixed in 1.1).

[Unreleased]: https://github.com/alfredang/sgevchargingapp_android/compare/v1.1...HEAD
[1.1]: https://github.com/alfredang/sgevchargingapp_android/releases/tag/v1.1
[1.0]: https://github.com/alfredang/sgevchargingapp_android/releases/tag/v1.0
