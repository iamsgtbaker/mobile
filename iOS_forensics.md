# iOS Forensic Collection Method Comparison

> **Internal Reference | Mobile Threat Operations | iOS 16+**

This document compares the forensic data available from iOS 16+ devices across four acquisition methods: Full File System (FFS), Advanced Logical Image (ALI), Encrypted Backup, and Unencrypted Backup. It is intended for mobile threat hunters and forensic analysts when scoping collections, identifying evidence gaps, and determining which artifacts are actionable for detection or investigation.

---

## Table of Contents

- [Collection Methods](#collection-methods)
  - [Full File System (FFS)](#full-file-system-ffs)
  - [Advanced Logical Image (ALI)](#advanced-logical-image-ali)
  - [Encrypted Backup](#encrypted-backup)
  - [Unencrypted Backup](#unencrypted-backup)
- [Collection Tools](#collection-tools)
  - [Full File System Tools](#full-file-system-tools)
  - [Advanced Logical Image Tools](#advanced-logical-image-tools)
  - [Encrypted Backup Tools](#encrypted-backup-tools)
  - [Unencrypted Backup Tools](#unencrypted-backup-tools)
  - [Operational Notes](#operational-notes)
- [Key Artifact Deep Dives](#key-artifact-deep-dives)
  - [The iOS Keychain & Keychain Extraction Module](#the-ios-keychain--keychain-extraction-module)
  - [KnowledgeC — The iOS Behavioral Activity Log](#knowledgec--the-ios-behavioral-activity-log)
- [Availability Legend](#availability-legend)
- [Comparative Data Availability Table](#comparative-data-availability-table)
  - [Communications — SMS & iMessage](#communications--sms--imessage)
  - [Communications — Phone & FaceTime](#communications--phone--facetime)
  - [Communications — Third-Party Messaging](#communications--third-party-messaging)
  - [Contacts & Relationships](#contacts--relationships)
  - [Location & Movement](#location--movement)
  - [Photos, Media & Files](#photos-media--files)
  - [Internet & Browser Activity](#internet--browser-activity)
  - [App Usage & Device Activity](#app-usage--device-activity)
  - [Device & System Information](#device--system-information)
  - [Security, Credentials & Keychain](#security-credentials--keychain)
  - [Health, Fitness & Sensors](#health-fitness--sensors)
  - [Calendar, Reminders & Notes](#calendar-reminders--notes)
  - [Financial & Transactions](#financial--transactions)
  - [Siri & On-Device Intelligence](#siri--on-device-intelligence)
  - [Network & System Forensic Artifacts](#network--system-forensic-artifacts)

---

## Collection Methods

### Full File System (FFS)

A Full File System acquisition provides the deepest level of access available without hardware-level intervention. It requires either a jailbroken device, a specialized agent installed on the device (as used by Cellebrite UFED, Magnet Verakey, and Oxygen Forensics), or exploitation of a documented vulnerability to achieve elevated filesystem privileges. An FFS image captures the entire `/private/var` partition, providing access to all app sandbox containers, the Keychain (when combined with a Keychain extraction module), system databases, the unified OS event log, Biome behavioral data streams, crash logs, and artifacts from deleted or previously uninstalled apps.

FFS is the gold standard for mobile forensic investigations and the only method capable of recovering deleted content, accessing encrypted app databases in plaintext, and retrieving system-level artifacts such as the KnowledgeC activity database, Biome data streams, sysdiagnose archives, the unified log, application crash reports, and AMFI trust cache records. These artifacts are essential for detecting and attributing sophisticated mobile threats such as Pegasus and Predator spyware.

### Advanced Logical Image (ALI)

An Advanced Logical Image — also referred to as an Advanced Logical Acquisition or File System acquisition in some tooling — extracts a curated set of files and databases through the iOS backup protocol augmented by additional file transfer mechanisms that do not require elevated privileges, such as the Apple File Conduit (AFC) protocol. An ALI typically includes most of what an encrypted backup provides, plus additional media files, some crash reporter content, data usage records, and select system preference files.

The exact scope of an ALI varies significantly between tools and iOS versions. ALI does not provide access to the Keychain, protected system databases such as the full KnowledgeC database or Biome streams, process-level artifacts, or deleted data. It represents a useful middle ground when FFS access is not achievable but more data than a standard backup is required.

### Encrypted Backup

An iTunes or Finder backup created with an encryption password enabled unlocks a significantly broader data set compared to an unencrypted backup. When backup encryption is enabled, iOS includes Keychain items marked as backup-eligible by app developers (excluding hardware-bound and non-migratable items), HealthKit data, Wi-Fi network credentials, and full email account authentication tokens.

The backup is structured as a flat directory of files named by SHA-1 hash of their domain and relative path, paired with a `Manifest.db` SQLite index. Encrypted backups are an excellent non-invasive collection method when device access is cooperative, requiring only an established trust pairing relationship and the backup encryption password.

### Unencrypted Backup

An unencrypted backup represents the minimum dataset that iOS exposes through the standard iTunes or Finder backup mechanism. iOS explicitly withholds Keychain data, HealthKit records, Wi-Fi passwords, and several other categories unless backup encryption is enabled. While unencrypted backups remain useful for gathering communications history, contact records, call logs, calendar data, and media content, they are the most limited of the four methods.

For mobile threat hunting purposes, unencrypted backups provide insufficient forensic depth to detect sophisticated implants. The most forensically significant system-level artifacts — unified logs, Biome streams, crash reports, KnowledgeC records, and AMFI logs — reside entirely outside the backup scope.

---

## Collection Tools

### Full File System Tools

FFS is the most tool-dependent category because it requires elevated access. The key caveat for all FFS tools: coverage depends entirely on the iOS version and chip generation. A tool that supports FFS on iOS 16.3 may not support iOS 16.5 because Apple patches the vulnerabilities these agents exploit. Cellebrite and Verakey both publish support matrices; staying current on those is part of the operational workflow.

| Tool | Type | Notes |
|------|------|-------|
| **Cellebrite UFED** | Commercial | Most widely deployed; uses a proprietary agent for supported devices |
| **Magnet Verakey** | Commercial | Purpose-built for iOS FFS; generally best iOS coverage; tends to pull more KnowledgeC data than competitors |
| **Oxygen Forensic Detective** | Commercial | Full FFS support on compatible devices |
| **checkra1n** | Open Source / Jailbreak | Works on A5–A11 chips (iPhone X and older); enables FFS access via AFC2/ifuse |
| **palera1n** | Open Source / Jailbreak | Extends coverage to A12–A16 on iOS 16+; requires tethered jailbreak which complicates field use |
| **iproxy / AFC2 / ifuse** | Open Source | Used post-jailbreak to mount the filesystem over USB |

### Advanced Logical Image Tools

| Tool | Type | Notes |
|------|------|-------|
| **Cellebrite UFED** | Commercial | Explicit "Advanced Logical" collection mode |
| **Magnet Verakey / AXIOM** | Commercial | Most thorough ALI scope; pulls beyond standard backup via AFC protocol |
| **Oxygen Forensic Detective** | Commercial | Full ALI support |
| **libimobiledevice** (`idevicebackup2`, `ifuse`) | Open Source | Foundational library implementing AFC and backup protocols; useful for scripted or automated collection |

### Encrypted Backup Tools

| Tool | Type | Notes |
|------|------|-------|
| **Cellebrite UFED** | Commercial | Native encrypted backup support with hash verification |
| **Magnet Verakey / AXIOM** | Commercial | Native support; chain-of-custody controls |
| **Oxygen Forensic Detective** | Commercial | Native support |
| **idevicebackup2** (libimobiledevice) | Open Source | Reliable encrypted backup via command line |
| **iTunes / Finder** | Apple Native | Works but lacks chain-of-custody controls and hash verification |

> **Operational note:** You need either the existing backup password or the ability to reset it (which requires the device passcode). If the device already has an encrypted backup password set by the user and you don't know it, collection is blocked.

### Unencrypted Backup Tools

| Tool | Type | Notes |
|------|------|-------|
| **Cellebrite UFED** | Commercial | Standard backup mode |
| **Magnet Verakey / AXIOM** | Commercial | Standard backup mode |
| **Oxygen Forensic Detective** | Commercial | Standard backup mode |
| **idevicebackup2** (libimobiledevice) | Open Source | Command-line unencrypted backup |
| **iTunes / Finder** | Apple Native | Standard backup without password |
| **iMazing** | Commercial | Commonly used for non-forensic collection scenarios |

> **Operational note:** If the device has an existing encrypted backup password configured, you cannot create an unencrypted backup without first clearing the password using the device passcode.

### Operational Notes

**Trust pairing** — The lockdown pairing record stored in `/private/var/root/Library/Lockdown/` is the prerequisite for ALI and backup collections. Without a paired record or the ability to establish one on a cooperating device, data collection is not possible. Preserving existing pairing records from a suspect computer can be valuable for enabling collection.

**GrayKey (Grayshift)** — Primarily a passcode extraction tool rather than a collection tool. Unlocking a device with GrayKey then enables FFS collection with a tool of choice. It is not a standalone collection platform.

**Verakey lab coverage** — Maintain a test device running each major iOS version in your lab. Verakey's FFS coverage tends to lag slightly behind iOS releases. Knowing your current coverage ceiling before being in front of a live device matters.

---

## Key Artifact Deep Dives

Several artifacts referenced in the comparison table warrant additional explanation. The following sections cover the iOS Keychain and its extraction mechanics, and the KnowledgeC database — both of which appear frequently in collection scoping discussions and are directly relevant to detecting sophisticated mobile threats.

### The iOS Keychain & Keychain Extraction Module

The iOS Keychain is Apple's hardware-backed encrypted credential store. It is the authoritative location for secrets that applications and the OS cannot afford to leave in plaintext: passwords, API tokens, OAuth refresh tokens, private keys, TLS certificates, Wi-Fi pre-shared keys, and VPN credentials. The raw database resides at `/private/var/Keychains/keychain-2.db`, but its contents are encrypted using keys derived from two sources: the device's hardware UID (a unique key fused into the SoC at manufacture and never exposed to software) and the user's passcode. This means that even a byte-perfect FFS image of a locked device yields an encrypted blob that is computationally infeasible to brute-force without the passcode.

A Keychain extraction module resolves this by operating on an unlocked, trusted device rather than against the raw encrypted file. Forensic agents deployed by tools such as Cellebrite UFED, Magnet Verakey, and Oxygen Forensics call the same Keychain APIs that an authorized application would use, but with the elevated entitlements their agents have been granted. The OS performs the decryption transparently and returns plaintext item values, which the module captures and structures into a readable output: the secret value, item class (generic password, internet password, certificate, or cryptographic key), the owning app's bundle ID, creation and modification timestamps, and the item's access control attributes.

#### Keychain Accessibility Constants

Each Keychain item is tagged with an accessibility constant that defines when iOS will permit access:

| Constant | Accessibility | Extractable? |
|----------|--------------|--------------|
| `kSecAttrAccessibleAfterFirstUnlock` | Accessible after the device has been unlocked at least once since boot. The most common setting for app tokens and credentials. Survives device sleep. | ✅ Yes (FFS + module) |
| `kSecAttrAccessibleWhenUnlocked` | Accessible only while the device is actively unlocked. More restrictive; used for highly sensitive secrets. | ✅ Yes (FFS + module, device must be unlocked) |
| `kSecAttrAccessibleAlways` | Accessible even when locked. Deprecated in iOS 12. Legacy apps may still use this. | ✅ Yes (FFS + module) |
| `kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly` | Bound to the Secure Enclave and the current passcode. Cannot be extracted by any software method, cannot migrate to a new device, and is destroyed if the passcode is removed. | ❌ Never extractable |

The `ThisDeviceOnly` suffix on any accessibility constant indicates the item is hardware-bound and non-migratable. It will never appear in a backup and cannot be extracted by a Keychain module regardless of agent privilege level, because the decryption key never leaves the Secure Enclave.

#### Backup vs. Full Extraction

Encrypted backups expose a separate, filtered subset of Keychain data. When a user creates an encrypted backup, iOS includes items that developers have explicitly permitted for backup by omitting the `ThisDeviceOnly` constraint. The result is the `keychain-backup.plist` file inside the backup archive — a useful but incomplete view of the Keychain that excludes all hardware-bound items, which in practice means it omits most system-level and security-critical entries.

#### Threat Hunting Relevance

Implants and stalkerware frequently store their configuration and C2 credentials in the Keychain. A process that writes an unexpected Keychain entry — particularly one with a bundle ID that does not match any installed app, or using a generic password class with an unusual service name — warrants investigation. Correlating Keychain entries against the installed app list from the `MobileInstallation` plist can surface orphaned entries left by deleted malicious apps.

---

### KnowledgeC — The iOS Behavioral Activity Log

KnowledgeC is the SQLite database that functions as iOS's unified behavioral activity journal. It is maintained by the CoreDuet daemon, which is Apple's on-device machine learning prediction engine. CoreDuet's stated purpose is to model user behavior in order to power Siri Suggestions, app pre-warming, battery optimization, and adaptive display management. The incidental forensic value of this work is an extraordinarily detailed, continuously written, timestamped log of almost everything that happens on the device — by the user or otherwise.

**Location:** `/private/var/mobile/Library/CoreDuet/Knowledge/knowledgeC.db`

#### Key Event Streams

The database is organized into event streams, each corresponding to a different behavioral domain:

| Event Stream | Description |
|---|---|
| `com.apple.knowledge.app.install` / `uninstall` | Records when apps are installed or removed, including timestamps and bundle IDs |
| `com.apple.knowledge.app.inForeground` / `inBackground` | Every transition of every app between foreground and background states with sub-second timestamps. The backbone of behavioral timeline analysis |
| `com.apple.knowledge.device.isLocked` / `isUnlocked` | Device lock and unlock events; allows reconstruction of exactly when the screen was active |
| `com.apple.knowledge.call.inCall` | Active phone call state — when the device entered and exited a call |
| `com.apple.knowledge.audio.route` | Audio route changes: headphones connected/disconnected, speakerphone enabled, AirPods paired |
| `com.apple.knowledge.device.isCharging` / `batteryLevel` | Charging state transitions and battery percentage over time |
| `com.apple.knowledge.safari.domainVisit` | Web domains visited in Safari correlated with the exact foreground session |
| `com.apple.knowledge.media.nowPlaying` | What media was playing, which app was playing it, and for how long |
| `com.apple.knowledge.device.backlight` | Screen backlight on/off events at granular level; useful for determining whether a user was actively looking at the device |

#### Threat Hunting Relevance

What makes KnowledgeC distinctively useful for threat hunting — as opposed to routine investigations — is its function as a behavioral baseline record. Because it logs every app foreground event without exception, it will record the presence of a malicious process if that process ever runs in a context that CoreDuet observes. Sophisticated implants like Pegasus are designed to minimize their observable footprint, but any process that becomes foreground, triggers a system call that CoreDuet monitors, or interacts with a framework that feeds into the knowledge store will leave a trace.

In practice, KnowledgeC analysis for threat detection involves:

- Querying the `inForeground` and `inBackground` streams for process bundle IDs that do not correspond to any installed application in the `MobileInstallation` plist
- Identifying app activity during time windows when the device was locked (indicating background process execution rather than user-initiated foreground use)
- Correlating timestamps against known IOCs such as exploitation windows identified in Citizen Lab or Amnesty Tech reports

KnowledgeC data is accessible via FFS and, to a limited extent, via Advanced Logical Image depending on the tool. It is not available in any backup format.

#### Recommended Tool: APOLLO

The most widely used open-source parser for KnowledgeC is **APOLLO** (Apple Pattern of Life Lazy Output'er), developed by Sarah Edwards. APOLLO maps event streams to human-readable timelines and supports queries across multiple databases simultaneously. It is the recommended starting point for KnowledgeC-based analysis.

#### KnowledgeC vs. Biome

In iOS 16+, Apple has been progressively migrating higher-fidelity behavioral telemetry to the **Biome** framework (`/private/var/mobile/Library/Biome/streams/`), which captures more granular per-interaction data than KnowledgeC — including specific UI interactions within apps, individual attachment opens, and contact lookup events. KnowledgeC and Biome are complementary: KnowledgeC provides the macro timeline of device activity while Biome provides the micro-level interaction record. Both are FFS-only artifacts.

---

## Availability Legend

| Symbol | Meaning |
|--------|---------|
| ✅ Yes | Artifact is fully available through this collection method |
| ⚠️ Partial | Artifact is partially available; scope, fidelity, or completeness is reduced compared to FFS |
| ❌ No | Artifact is not accessible through this collection method |

---

## Comparative Data Availability Table

### Communications — SMS & iMessage

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Message Content | Full text body of SMS and iMessage conversations. FFS also recovers soft-deleted messages from SQLite WAL and free pages. | `/private/var/mobile/Library/SMS/sms.db` | ✅ | ✅ | ✅ | ✅ |
| Message Attachments | Images, video, audio, and document files exchanged in messages. Full files via FFS; backup methods may return thumbnails only. | `/private/var/mobile/Library/SMS/Attachments/` | ✅ | ⚠️ | ✅ | ⚠️ |
| Deleted Messages | Soft-deleted messages retained in SQLite free-list pages and WAL journal. Recoverable only with raw database access from FFS. | `/private/var/mobile/Library/SMS/sms.db` (WAL / free pages) | ✅ | ❌ | ❌ | ❌ |
| Tapback / Reaction Records | Emoji reactions stored as associated message records linked by GUID. | `/private/var/mobile/Library/SMS/sms.db` (message_attachment_join) | ✅ | ✅ | ✅ | ✅ |
| Group Chat Metadata | Group name, participant list, and thread identifier for multi-party conversations. | `/private/var/mobile/Library/SMS/sms.db` (chat, chat_handle_join tables) | ✅ | ✅ | ✅ | ✅ |
| Cross-Device Delete Sync Records | Records of messages deleted on other Apple devices and synced; useful for identifying silenced or cleared threads. | `/private/var/mobile/Library/SMS/sms.db` (sync_deleted_messages) | ✅ | ❌ | ❌ | ❌ |

### Communications — Phone & FaceTime

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Call History | Incoming, outgoing, missed, and blocked calls with timestamps, duration, and contact identifiers. Includes cellular, FaceTime, and CallKit VoIP calls. | `/private/var/mobile/Library/CallHistoryDB/CallHistory.storedata` | ✅ | ✅ | ✅ | ✅ |
| FaceTime Call Logs | Audio and video FaceTime calls logged alongside PSTN calls in the unified call history store. | `/private/var/mobile/Library/CallHistoryDB/CallHistory.storedata` | ✅ | ✅ | ✅ | ✅ |
| CallKit VoIP Records | Third-party VoIP calls from WhatsApp, Signal, Teams, and Zoom when they use the CallKit integration. | `/private/var/mobile/Library/CallHistoryDB/CallHistory.storedata` | ✅ | ✅ | ✅ | ✅ |
| Voicemail Recordings | Visual voicemail audio files and metadata. Voicemail audio excluded from unencrypted backups. | `/private/var/mobile/Library/Voicemail/` | ✅ | ⚠️ | ✅ | ❌ |

### Communications — Third-Party Messaging

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| WhatsApp Messages | Chat messages, media references, group metadata, and call logs. Database encrypted at rest in recent versions; FFS provides plaintext via agent. | `/private/var/mobile/Containers/Shared/AppGroup/<UUID>/ChatStorage.sqlite` | ✅ | ⚠️ | ✅ | ⚠️ |
| Signal Messages | End-to-end encrypted messages. Local SQLite database accessible only via FFS with an agent or jailbreak. Not available via any backup method. | `/private/var/mobile/Containers/Shared/AppGroup/<UUID>/grdb/signal.sqlite` | ✅ | ❌ | ❌ | ❌ |
| Telegram Messages | Cloud-synced messages with a local device cache. Partial content available via FFS app container. | `/private/var/mobile/Containers/Shared/AppGroup/<UUID>/` | ✅ | ⚠️ | ❌ | ❌ |
| Apple Mail (Mail.app) | Email headers, body text, and attachments cached locally in EMLX flat files and SQLite envelope index. | `/private/var/mobile/Library/Mail/` | ✅ | ✅ | ✅ | ✅ |
| Third-Party Email (Outlook, Gmail) | Locally cached email within the app sandbox. Scope depends on each app's caching policy and sync window. | `/private/var/mobile/Containers/Data/Application/<UUID>/Library/` | ✅ | ⚠️ | ⚠️ | ❌ |

### Contacts & Relationships

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Address Book Entries | Full contact records: name, phone numbers, email addresses, postal addresses, organization, birthday, and notes. | `/private/var/mobile/Library/AddressBook/AddressBook.sqlitedb` | ✅ | ✅ | ✅ | ✅ |
| Contact Photos | Profile images associated with address book contacts. | `/private/var/mobile/Library/AddressBook/AddressBookImages.sqlitedb` | ✅ | ✅ | ✅ | ✅ |
| Recent Interaction Metadata | Interaction frequency data used by Siri and Spotlight for contact surfacing and suggestion ranking. | `/private/var/mobile/Library/AddressBook/AddressBook.sqlitedb` (ABRecent) | ✅ | ⚠️ | ⚠️ | ❌ |
| Account Configurations | Synced contact account settings for iCloud, Google, Exchange, and CardDAV sources. | `/private/var/mobile/Library/Accounts/Accounts3.sqlite` | ✅ | ⚠️ | ⚠️ | ❌ |

### Location & Movement

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Core Location Cache | Cached GPS fix coordinates from Location Services with timestamps, accuracy radius, and altitude. | `/private/var/root/Library/Caches/locationd/consolidated.db` | ✅ | ❌ | ❌ | ❌ |
| Significant Locations | Machine-learned frequently visited places with visit frequency and dwell time. Stored encrypted in iOS 13+ within the routined cache. | `/private/var/mobile/Library/Caches/com.apple.routined/` | ✅ | ❌ | ❌ | ❌ |
| Maps Search History | Apple Maps search queries and navigation route history. | `/private/var/mobile/Containers/Data/Application/<UUID>/Library/` (Maps) | ✅ | ✅ | ✅ | ❌ |
| Maps Favorites & Recents | Saved place bookmarks and recently viewed locations from Apple Maps. | `/private/var/mobile/Library/Maps/GeoServices.sqlite` | ✅ | ✅ | ✅ | ⚠️ |
| Photo EXIF GPS Coordinates | Latitude and longitude embedded in photo EXIF metadata at the moment of capture. | `/private/var/mobile/Media/DCIM/` (EXIF metadata in image files) | ✅ | ✅ | ✅ | ✅ |
| Wi-Fi Geolocation Data | Wi-Fi network scan results (SSID, BSSID, signal strength) used by Location Services for triangulation. | `/private/var/root/Library/Caches/locationd/` | ✅ | ❌ | ❌ | ❌ |
| Navigation Routing Logs | Turn-by-turn navigation session data cached by Maps app during active route guidance. | `/private/var/mobile/Containers/Data/Application/<UUID>/tmp/` (Maps) | ✅ | ❌ | ❌ | ❌ |
| Geofence Records | App-registered geographic boundaries and associated trigger event logs from Location Services. | `/private/var/mobile/Library/Caches/locationd/` | ✅ | ❌ | ❌ | ❌ |

### Photos, Media & Files

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Camera Roll Photos | JPEG and HEIC photos captured with the device camera. | `/private/var/mobile/Media/DCIM/` | ✅ | ✅ | ✅ | ✅ |
| Video Recordings | MOV and MP4 video files recorded on device. | `/private/var/mobile/Media/DCIM/` | ✅ | ✅ | ✅ | ✅ |
| Photos Library Database | Metadata for all media assets: albums, faces, keywords, smart album rules, creation and modification timestamps, and iCloud sync state. | `/private/var/mobile/Media/PhotoData/Photos.sqlite` | ✅ | ✅ | ✅ | ✅ |
| Recently Deleted Photos | Photos and videos held in the Recently Deleted album for up to 30 days before permanent removal. | `/private/var/mobile/Media/PhotoData/CPLAssets/` | ✅ | ⚠️ | ⚠️ | ❌ |
| Voice Memos | Audio recordings created with the Voice Memos app, stored as M4A files with metadata. | `/private/var/mobile/Media/Recordings/` | ✅ | ✅ | ✅ | ✅ |
| iCloud Drive Files (cached) | Locally cached copies of iCloud Drive documents and folders. | `/private/var/mobile/Library/Mobile Documents/` | ✅ | ✅ | ✅ | ⚠️ |
| Files App Downloads | Files downloaded via Safari or the Files app to the local Downloads folder. | `/private/var/mobile/Library/Mobile Documents/com~apple~CloudDocs/Downloads/` | ✅ | ✅ | ✅ | ⚠️ |

### Internet & Browser Activity

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Safari Browse History | Visited URLs, page titles, visit counts, and timestamps. | `/private/var/mobile/Library/Safari/History.db` | ✅ | ✅ | ✅ | ✅ |
| Safari Bookmarks & Reading List | Saved bookmarks and Reading List items with URLs, titles, and archive content. | `/private/var/mobile/Library/Safari/Bookmarks.db` | ✅ | ✅ | ✅ | ✅ |
| Safari Open Tabs | Currently open tabs including URL and page title at time of collection. | `/private/var/mobile/Library/Safari/BrowserState.db` | ✅ | ✅ | ✅ | ❌ |
| Safari Cookies | HTTP cookies including session tokens and persistent tracking cookies. | `/private/var/mobile/Library/Cookies/Cookies.binarycookies` | ✅ | ✅ | ✅ | ❌ |
| Safari Web Cache | Cached HTML, images, and JavaScript stored by WebKit. Not included in any backup method. | `/private/var/mobile/Library/Caches/com.apple.WebKit/` | ✅ | ❌ | ❌ | ❌ |
| Safari AutoFill Form Data | Saved form field entries including names, email addresses, and shipping addresses. | `/private/var/mobile/Library/Safari/AutoFill.db` | ✅ | ✅ | ✅ | ❌ |
| Saved Website Passwords | iCloud Keychain credential entries for websites. Accessible only via FFS with Keychain extraction module. | Keychain (com.apple.password-manager entries) | ✅ | ❌ | ❌ | ❌ |
| Safari Download History | Record of files downloaded through Safari with source URLs and destination paths. | `/private/var/mobile/Library/Safari/Downloads.plist` | ✅ | ✅ | ✅ | ⚠️ |
| Third-Party Browser Data | Chrome, Firefox, Brave, and other browser history cached within app sandbox containers. | `/private/var/mobile/Containers/Data/Application/<UUID>/Library/` | ✅ | ⚠️ | ⚠️ | ❌ |

### App Usage & Device Activity

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Installed Application List | Bundle IDs, display names, install dates, version numbers, and sandbox UUIDs for all installed apps. | `/private/var/mobile/Library/MobileInstallation/LastLaunchServicesMap.plist` | ✅ | ✅ | ✅ | ❌ |
| Screen Time Records | Per-app usage duration by day, pickup counts, notification counts, and downtime schedules. | `/private/var/mobile/Library/Application Support/com.apple.ScreenTime/RMAdminStore-Local.sqlite` | ✅ | ✅ | ✅ | ❌ |
| KnowledgeC Activity Database | System-level activity log recording app foreground/background transitions, device lock state, audio routes, and call state with sub-second timestamps. Critical for behavioral timeline analysis. | `/private/var/mobile/Library/CoreDuet/Knowledge/knowledgeC.db` | ✅ | ⚠️ | ❌ | ❌ |
| Biome Data Streams | High-fidelity behavioral telemetry: per-app UI interactions, attachments opened, contact lookups, Siri queries, device orientation. Primary artifact for detecting spyware behavioral anomalies. | `/private/var/mobile/Library/Biome/streams/` | ✅ | ❌ | ❌ | ❌ |
| Notification Delivery History | Record of notifications delivered per app. iOS 16+ retains approximately 7 days in KnowledgeC. | `/private/var/mobile/Library/CoreDuet/Knowledge/knowledgeC.db` | ✅ | ⚠️ | ❌ | ❌ |
| Spotlight Search History | On-device Spotlight and Siri search queries typed by the user. | `/private/var/mobile/Library/Suggestions/` | ✅ | ❌ | ❌ | ❌ |
| App Clips Invocation Records | Invocation events and temporary container data for App Clips experiences. | `/private/var/mobile/Containers/Data/AppClips/` | ✅ | ❌ | ❌ | ❌ |

### Device & System Information

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Device Identifiers | UDID, serial number, IMEI, MEID, hardware model identifier, Wi-Fi MAC address, and Bluetooth MAC address. | `/private/var/root/Library/Lockdown/data_ark.plist` | ✅ | ✅ | ✅ | ✅ |
| iOS Version & Build | Installed iOS version string, build number, and OTA software update history. | `/private/var/mobile/Library/Preferences/com.apple.springboard.plist` | ✅ | ✅ | ✅ | ✅ |
| Wi-Fi Network History | SSIDs, BSSIDs, and first/last connection timestamps for all previously joined Wi-Fi networks. | `/private/var/preferences/SystemConfiguration/com.apple.wifi.plist` | ✅ | ✅ | ⚠️ | ❌ |
| Bluetooth Paired Devices | MAC addresses, device names, and pairing timestamps for previously paired Bluetooth accessories. | `/private/var/mobile/Library/Preferences/com.apple.MobileBluetooth.plist` | ✅ | ✅ | ✅ | ❌ |
| MDM & Configuration Profiles | MDM enrollment details, applied configuration profiles, and managed policy restrictions. | `/private/var/mobile/Library/ConfigurationProfiles/` | ✅ | ⚠️ | ⚠️ | ❌ |
| Installed Certificates | TLS certificates, MDM trust anchors, and custom root certificate authority additions. | `/private/var/mobile/Library/Keychains/` & `/private/var/Managed Preferences/` | ✅ | ⚠️ | ⚠️ | ❌ |
| SIM & Carrier Information | SIM card ICCID, IMSI, and carrier provisioning configuration data. | `/private/var/root/Library/Lockdown/data_ark.plist` | ✅ | ✅ | ✅ | ✅ |
| Signed-In Apple ID | Apple ID email address and associated account identifiers for all signed-in iCloud services. | `/private/var/mobile/Library/Accounts/Accounts3.sqlite` | ✅ | ✅ | ✅ | ✅ |
| Shutdown & Reboot Log | System shutdown and reboot event records. Useful for detecting unexpected reboots caused by forensic tools or spyware processes. | `/private/var/mobile/Library/Logs/CrashReporter/` | ✅ | ❌ | ❌ | ❌ |

### Security, Credentials & Keychain

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Keychain — Full Database | Complete Keychain including all passwords, API tokens, private keys, and certificates. Requires FFS with a dedicated Keychain extraction module. | `/private/var/Keychains/keychain-2.db` | ✅ | ❌ | ❌ | ❌ |
| Keychain — Backup-Eligible Subset | Subset of Keychain items marked as backup-eligible by app developers. Excludes hardware-bound and Secure Enclave-bound items. | `keychain-backup.plist` (inside backup archive) | ❌ | ❌ | ✅ | ❌ |
| Stored Wi-Fi Passwords | Pre-shared keys (PSK) for saved Wi-Fi networks, stored as Keychain entries. | Keychain (com.apple.network.eap.user.item) | ✅ | ❌ | ❌ | ❌ |
| VPN Credentials & Profiles | VPN profile configurations and associated authentication credentials stored in Keychain. | Keychain + `/private/var/mobile/Library/Preferences/com.apple.networkextension.plist` | ✅ | ❌ | ❌ | ❌ |
| Biometric Enrollment State | Whether Touch ID or Face ID is enrolled. Biometric templates reside only in the Secure Enclave and cannot be extracted by any software method. | `/private/var/mobile/Library/Biometric/BiometricKit.plist` | ✅ | ❌ | ❌ | ❌ |
| Application Crash Logs | Per-app crash reports with process name, exception type, thread backtraces, and binary memory maps. Critical for identifying exploitation attempts. | `/private/var/mobile/Library/Logs/CrashReporter/` | ✅ | ❌ | ❌ | ❌ |
| Sysdiagnose Archives | Comprehensive system diagnostic bundles. Contains process listing, network state, kernel logs. Essential in Pegasus and Predator spyware investigations. | `/private/var/mobile/Library/Logs/CrashReporter/DiagnosticLogs/` | ✅ | ❌ | ❌ | ❌ |
| AMFI / TrustCache Records | Apple Mobile File Integrity code-signing validation logs. Can reveal execution of unsigned or tampered binaries. | `/private/var/db/AMFI/` | ✅ | ❌ | ❌ | ❌ |

### Health, Fitness & Sensors

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| HealthKit Database | All health metrics: step counts, heart rate, blood oxygen, respiratory rate, ECG, sleep analysis, workouts, and nutrition. | `/private/var/mobile/Library/Health/healthdb_secure.sqlite` | ✅ | ✅ | ✅ | ❌ |
| Sleep Tracking Records | Sleep stage analysis records from Apple Watch or third-party apps submitted to HealthKit. | `/private/var/mobile/Library/Health/healthdb_secure.sqlite` | ✅ | ✅ | ✅ | ❌ |
| Medical ID | Emergency medical information: conditions, medications, blood type, and emergency contacts. | `/private/var/mobile/Library/Health/healthdb_secure.sqlite` | ✅ | ✅ | ✅ | ❌ |
| CoreMotion Sensor Cache | Raw accelerometer and pedometer data cached by the CoreMotion framework between sync cycles. | `/private/var/mobile/Library/Caches/com.apple.CMHeadphoneMotionData/` | ✅ | ❌ | ❌ | ❌ |

### Calendar, Reminders & Notes

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Calendar Events | All calendar events: title, start/end time, location, attendees, recurrence rules, alarms, and organizer. | `/private/var/mobile/Library/Calendar/Calendar.sqlitedb` | ✅ | ✅ | ✅ | ✅ |
| Reminders & Tasks | Task and reminder records including title, due date, priority, completion status, and list membership. | `/private/var/mobile/Library/Reminders/` | ✅ | ✅ | ✅ | ✅ |
| Notes Content | Notes including plain text, rich text, embedded images, tables, checklists, and sketches. | `/private/var/mobile/Library/Notes/NoteStore.sqlite` | ✅ | ✅ | ✅ | ✅ |
| Recently Deleted Notes | Notes in the Recently Deleted folder retained before permanent removal. | `/private/var/mobile/Library/Notes/NoteStore.sqlite` | ✅ | ⚠️ | ⚠️ | ❌ |
| Shared Notes Metadata | iCloud collaboration metadata for shared notes including participant list and edit history. | `/private/var/mobile/Library/Notes/NoteStore.sqlite` | ✅ | ✅ | ✅ | ❌ |

### Financial & Transactions

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Apple Pay Transaction History | Transaction records and provisioned card metadata. Full card numbers are not stored on device; only last four digits and token data. | `/private/var/mobile/Library/Passes/Cards/` | ✅ | ⚠️ | ❌ | ❌ |
| Wallet Passes | Boarding passes, loyalty cards, event tickets, and gift cards stored in Wallet. | `/private/var/mobile/Library/Passes/` | ✅ | ✅ | ✅ | ✅ |
| App Store Purchase Records | Metadata for purchased and downloaded apps. Billing details are not stored locally. | `/private/var/mobile/Library/Caches/com.apple.appstored/` | ✅ | ⚠️ | ❌ | ❌ |

### Siri & On-Device Intelligence

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Siri Interaction Logs | Siri query text and response metadata. May include sensitive spoken queries reflecting user intent. | `/private/var/mobile/Library/Assistant/` | ✅ | ⚠️ | ❌ | ❌ |
| Siri Shortcuts & Automations | User-defined Siri Shortcuts, personal automations, and shortcut action sequences. | `/private/var/mobile/Library/Shortcuts/` | ✅ | ✅ | ✅ | ❌ |
| On-Device ML Personalization | Personalization model data used to train Siri suggestions and on-device intelligence features. | `/private/var/mobile/Library/Siri/` | ✅ | ❌ | ❌ | ❌ |

### Network & System Forensic Artifacts

| Data Point | Description | iOS Path | FFS | ALI | Enc. Backup | Unenc. Backup |
|---|---|---|:---:|:---:|:---:|:---:|
| Data Usage Per App | Cellular and Wi-Fi data consumption per app with timestamps. Useful for detecting anomalous background exfiltration patterns. | `/private/var/wireless/Library/Databases/DataUsage.sqlite` | ✅ | ✅ | ⚠️ | ❌ |
| Unified System Logs | Complete OS-level event log stream in logarchive format. Enables precise timeline reconstruction of process activity, network connections, and system events. Highest-value artifact for advanced threat detection. | `/private/var/db/diagnostics/` (logarchive) | ✅ | ❌ | ❌ | ❌ |
| Powerlog | Device power consumption correlated with process and app activity. Reveals background process execution patterns; useful for identifying persistent implant activity. | `/private/var/mobile/Library/Logs/CrashReporter/DiagnosticLogs/Powerlog/` | ✅ | ❌ | ❌ | ❌ |
| URLSession Cache (Cache.db) | HTTP request and response pairs cached per app by the URLSession framework. May contain network IOCs such as C2 domain names and URI patterns. | `/private/var/mobile/Containers/Data/Application/<UUID>/Library/Caches/` | ✅ | ⚠️ | ❌ | ❌ |
| Network Interface Config | Network interface history, DHCP lease records, and assigned IP address history. | `/private/var/preferences/SystemConfiguration/` | ✅ | ❌ | ❌ | ❌ |
| VPN & Network Extension Logs | Connection attempts, session durations, and configuration for VPN and Network Extension profiles. | `/private/var/mobile/Library/Preferences/com.apple.networkextension.plist` | ✅ | ❌ | ❌ | ❌ |
| Aggregate Dictionary | Privacy-preserving aggregate statistics about app network activity maintained by the OS. | `/private/var/mobile/Library/Caches/com.apple.aggregated/` | ✅ | ❌ | ❌ | ❌ |

---

*Internal Reference | Mobile Threat Operations | iOS 16+ | Hunt*
