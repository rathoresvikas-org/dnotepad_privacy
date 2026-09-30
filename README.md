# Privacy Policy for DNotepad

**Effective Date:** September 14, 2026 &nbsp;|&nbsp; **Last Updated:** September 30, 2026 &nbsp;|&nbsp; **Version:** 2.8.5 &nbsp;|&nbsp; **Developer:** RathoreSVikas &nbsp;|&nbsp; **Package:** `com.dnotepad.app`

---

DNotepad is an advanced, privacy-first, **100% offline** Text Editor, Source Code IDE, Notes Workspace, and Local AI Productivity Suite for Android, developed by RathoreSVikas.

We believe that your personal notes, documents, source code, and data belong **exclusively to you**. DNotepad is engineered from the ground up to operate completely without internet access, ensuring absolute confidentiality, privacy, and zero data collection.

---

## Google Play Data Safety — Quick Reference

The table below summarises the declarations made in the Google Play Data Safety section. Full explanations are in the sections that follow.

| Category | Collected? | Shared? | Notes |
|---|---|---|---|
| Personal info (name, email, phone, etc.) | ❌ No | ❌ No | Never requested or stored |
| Financial info | ❌ No | ❌ No | App is free, no payments |
| Health & fitness data | ❌ No | ❌ No | Not applicable |
| Messages | ❌ No | ❌ No | Not applicable |
| Photos & videos | ❌ No | ❌ No | Images stay on-device only |
| Audio files | ❌ No | ❌ No | Not applicable |
| Files & documents | ❌ No | ❌ No | Opened/saved locally via SAF only |
| Calendar events | ❌ No | ❌ No | Not applicable |
| Contacts | ❌ No | ❌ No | Not applicable |
| App activity (usage, search history) | ❌ No | ❌ No | No telemetry or analytics |
| Web browsing history | ❌ No | ❌ No | Not applicable |
| App info & performance (crash logs) | ❌ No | ❌ No | No remote crash reporting |
| Device or other identifiers | ❌ No | ❌ No | No device ID collection |
| Location | ❌ No | ❌ No | Not requested or used |
| **Data encrypted in transit** | N/A — no data ever leaves the device | | |
| **User can request data deletion** | ✅ Yes — via in-app deletion or app uninstall | | |

> **Data Safety Compliance Note:** Because DNotepad holds no `INTERNET` or `ACCESS_NETWORK_STATE` permissions at the Android OS level, no data — from our code or any bundled third-party library — can be transmitted off-device. This is enforced at the Linux kernel socket layer, not merely as a software policy.

---

## 1. 100% Offline Architecture & Zero Data Collection

**No Internet Permissions at the OS Level:**
DNotepad does not possess, request, or use the Android `INTERNET` or `ACCESS_NETWORK_STATE` permissions. Both are explicitly removed from the final merged manifest using `tools:node="remove"` to strip any permissions that transitive library dependencies might attempt to inject. At the Android operating system and Linux kernel level, DNotepad is physically blocked from opening network sockets or transmitting data over the internet.

**No Remote Servers or Cloud Sync:**
We do not own, operate, or connect to any cloud server, backend service, or third-party API endpoint. No user documents, source code, notes, images, AI-generated summaries, or any metadata are ever transmitted, synced, or uploaded to any external server.

**Zero Tracking, Telemetry, or Analytics:**
DNotepad contains no advertising SDKs, no crash reporting libraries (such as Firebase Crashlytics or Sentry), no analytics services (such as Google Analytics or Mixpanel), and no remote monitoring frameworks. We do not track what you type, compile, view, scan, or organise.

**No Personal Data Harvesting:**
We do not collect, store on any server, buy, sell, broker, share, or monetise personal information of any kind — including but not limited to your name, email address, phone number, location data, IP address, device identifiers, or advertising IDs.

---

## 2. Feature-Specific Local Data Handling

All data processing, execution, and storage within DNotepad occur strictly inside the secure, sandboxed private storage of your local device.

### A. Text Editor & Source Code IDE

All text files, source code scripts, and documents that you open, edit, or create in DNotepad are read directly from and written directly to your device's local file system or external SD card via the Android Storage Access Framework (SAF). SAF provides file access without bypassing Android's sandboxing model.

- No file contents are intercepted, logged, cached remotely, or exported.
- No document metadata (filenames, paths, modification timestamps) is transmitted anywhere.

### B. Offline Multi-Language Code Compilation & Execution

DNotepad includes embedded, fully on-device execution runtimes supporting:

**Interpreted / JIT-executed languages:** Python 3 (via Chaquopy/CPython JNI), JavaScript & TypeScript (transpiled/executed locally), Java (interpreted locally), Kotlin (interpreted locally), Lua, PHP, Ruby, Shell scripts.

**Rendered / previewed languages:** HTML, CSS, Markdown, SVG, SQL.

All code execution, script interpretation, and document previews run 100% locally within sandboxed on-device environments. No source code, input data, or execution output is dispatched to external compilation servers.

**Bundled Python Library Disclosure (`requests`):**
The embedded Python 3 runtime includes the `requests` HTTP library as part of the pip package ecosystem available for user-written Python scripts. Because DNotepad holds no `INTERNET` permission, the `requests` library — or any other code running inside DNotepad — is physically prevented from opening network connections by the Android OS and the Linux kernel's socket permission enforcement. This is not a software-only restriction; it is enforced at the operating system level.

### C. Notes & Workspace Management

Text notes, checklists, category tags, and image attachments are stored exclusively in a sandboxed local SQLite/Room database located within the application's private internal storage (`/data/data/com.dnotepad.app/databases/`). This directory is:

- Protected by Android's per-application OS-level isolation.
- Protected by device-level hardware encryption when the device has a screen lock enabled.
- Never backed up to Google Drive or any cloud service (explicitly excluded — see Section 5).

Quick-capture widgets, sticky memo widgets, checklist widgets, the AI Quota tracker widget, and the Quick Settings tile all interact exclusively with this local device database and local SharedPreferences.

### D. AI Quota Tracker & Countdown Timers

The AI Quota Tracker and all associated home screen and Quick Settings widgets are **100% manual, on-device** calculation and countdown tools designed to help you track your own AI subscription usage cycles (e.g., Claude, ChatGPT, Grok, Gemini).

DNotepad does **not** connect to, authenticate with, or communicate with OpenAI, Anthropic, Google, xAI, or any third-party AI service API. All quota numbers, account labels, reset schedules, and countdown states are stored purely in local device SharedPreferences. No data from the AI Quota Tracker leaves your device.

### E. On-Device Optical Character Recognition (OCR)

DNotepad provides local text recognition (OCR) via the bundled Google ML Kit Text Recognition library (`com.google.mlkit:text-recognition`). This is the **bundled offline variant** of ML Kit that operates entirely on-device without any Play Services dependency or network connectivity.

- Image scanning and character extraction are executed entirely on-device.
- Your photos and scanned documents are processed in memory and immediately discarded after text extraction.
- Extracted text never leaves your physical device.

### F. On-Device AI Note Summarization, Task Extraction & Smart Tagging (Local LLM/SLM)

DNotepad includes an embedded on-device Small Language Model (SLM) inference engine powered by Google LiteRT (TensorFlow Lite). This engine is used for:

- **Executive Summarization:** Generating structured summaries of your notes.
- **Task Extraction:** Automatically identifying action items from note content.
- **Document Classification & Auto-Tagging:** Categorising notes with relevant tags.

**How it works:**
The engine loads a bundled `.tflite` model file stored in the app's private `filesDir`. If the model binary is not present, the engine falls back to an entirely deterministic, rule-based linguistic analysis pipeline that requires no model file at all.

In both modes:
- All inference runs entirely on your physical device using on-device CPU/NPU compute.
- No note content, prompts, inferred outputs, or intermediate tensors are transmitted anywhere.
- The model cannot phone home — DNotepad holds no `INTERNET` permission.

> **AI Disclosure (Google Play 2026 Requirement):** DNotepad uses on-device AI to generate note summaries and extract tasks from your notes. This AI processing is performed locally on your device. No AI-generated outputs are sent to external services. The app does not integrate with any third-party AI cloud API.

---

## 3. Device Permissions & Transparency

DNotepad requests only the minimal permissions necessary to function as a powerful offline file editor and local AI productivity workspace. Every permission requested has a single, specific, user-facing purpose.

### Storage

**`READ_EXTERNAL_STORAGE`** *(Android 12 and below, `maxSdkVersion="32"`)*
**`WRITE_EXTERNAL_STORAGE`** *(Android 9 and below, `maxSdkVersion="28"`)*

> **Purpose:** Required on older Android versions to allow you to browse, open, view, edit, compile, and save text documents, source code files, and projects on your device's internal storage and external SD cards. On Android 10+, DNotepad uses the Scoped Storage model and Android Storage Access Framework (SAF) exclusively — no legacy storage permission is needed or used.

### Notifications & Alarms

**`POST_NOTIFICATIONS`** *(Android 13+)*

> **Purpose:** Required on Android 13 and above to deliver local note and task reminder notifications that you explicitly schedule within the app. DNotepad never sends unsolicited, marketing, or server-pushed notifications of any kind.

**`SCHEDULE_EXACT_ALARM`**

> **Purpose:** Required to trigger your scheduled note reminders and AI Quota reset countdowns at the precise times you set. DNotepad implements a 3-tier defensive fallback:
> 1. If `canScheduleExactAlarms()` → uses `setExactAndAllowWhileIdle()` ✅
> 2. If not granted → falls back to `setAndAllowWhileIdle()` (slightly inexact but functional) ✅
> 3. If `SecurityException` occurs → falls back to `set()` ✅
>
> *Note: DNotepad does **NOT** request or use `USE_EXACT_ALARM`.*

### Full-Screen Reminder Alerts

**`USE_FULL_SCREEN_INTENT`** *(Android 14+, Special App Access Permission)*

> **Purpose:** Required on Android 14 (API 34) and above to display scheduled note and task reminder notifications as full-screen, alarm-style alerts when your device screen is locked. This permission is used exclusively for high-priority local reminder notifications that you explicitly schedule yourself inside the app (e.g., "Remind me at 9:00 AM").
>
> DNotepad uses this permission strictly for locally-triggered, user-initiated alarms — never for server-pushed, marketing, or unsolicited notifications. On Android 14+, DNotepad checks `NotificationManager.canUseFullScreenIntent()` before attempting to display a full-screen alert, and gracefully degrades to a standard heads-up notification if the permission has not been granted.
>
> You can manage this permission at any time in: **Android Settings → Apps → DNotepad → Special app access → Use full-screen intents.**

### Boot, Hardware & Background

**`RECEIVE_BOOT_COMPLETED`** and **`MY_PACKAGE_REPLACED`**

> **Purpose:** Required to automatically restore your scheduled local reminders and AI Quota reset countdowns after your device reboots or after the app is updated. Without this, all scheduled alarms would be lost on every device restart.

**`VIBRATE`**

> **Purpose:** Required to provide haptic vibration feedback when a reminder notification fires.

**`WAKE_LOCK`**

> **Purpose:** Required to temporarily wake the device processor to deliver a scheduled alarm notification at the precise time it is due, even if the device is in sleep mode.

### Permissions Explicitly NOT Requested

DNotepad does **not** request and never uses:

`INTERNET` · `ACCESS_NETWORK_STATE` · `ACCESS_FINE_LOCATION` · `ACCESS_COARSE_LOCATION` · `CAMERA` · `READ_CONTACTS` · `READ_CALL_LOG` · `RECORD_AUDIO` · `READ_MEDIA_IMAGES` · `READ_MEDIA_VIDEO` · `READ_MEDIA_AUDIO` · `MANAGE_EXTERNAL_STORAGE` · `USE_EXACT_ALARM` · `REQUEST_INSTALL_PACKAGES` · `SYSTEM_ALERT_WINDOW`

---

## 4. Third-Party Libraries, SDKs, and Runtimes

To provide offline compilation, syntax highlighting, OCR, and local AI inference, DNotepad bundles selected open-source libraries and embedded runtimes. All bundled components operate strictly within the local device environment.

| Library / Runtime | Purpose | Network Access Possible? |
|---|---|---|
| Chaquopy (CPython 3 JNI/NDK) | Python 3 code execution | ❌ No — blocked at OS level |
| `requests` (Python pip package) | Available to user Python scripts | ❌ No — blocked at OS level |
| `numpy` (Python pip package) | Available to user Python scripts | ❌ No — blocked at OS level |
| Google ML Kit Text Recognition (bundled) | On-device OCR | ❌ No — bundled offline variant |
| Google LiteRT / TensorFlow Lite | On-device SLM/AI inference | ❌ No — no network calls made |
| Markwon | Markdown rendering | ❌ No — pure local rendering |
| JUniversalChardet | Character encoding detection | ❌ No — local only |
| AndroidX Room | Local SQLite database ORM | ❌ No — local only |
| AndroidX DataStore | Local preferences storage | ❌ No — local only |
| Hilt (Dagger) | Dependency injection | ❌ No — compile-time only |

> **Important:** Because DNotepad strips all network permissions (`INTERNET` and `ACCESS_NETWORK_STATE`) from its final compiled manifest using `tools:node="remove"`, no third-party library — regardless of its own capabilities — has any technical ability to transmit data from your device. This is enforced by the Android OS at the Linux kernel socket layer.

---

## 5. Data Storage, Retention, Security & Deletion Rights

### Where Your Data Lives

All data created within DNotepad resides exclusively on your physical device:

| Data Type | Storage Location | Encrypted? |
|---|---|---|
| Notes, checklists, tags, reminders | App private Room database (`/data/data/com.dnotepad.app/databases/`) | ✅ Yes, device-level |
| AI Quota tracker settings | App private SharedPreferences | ✅ Yes, device-level |
| Temporary exports / cached previews | App private cache (`/data/data/com.dnotepad.app/cache/`) | ✅ Yes, device-level |
| Your text files / code projects | Your device's external storage / SD card (via SAF) | Per your device settings |

### Total User Control

You maintain absolute ownership and authority over all your files, notes, and application data.

### Immediate Deletion

Deleting a note, task, checklist item, image attachment, or file inside DNotepad permanently removes it from the local database or file system immediately. There is no server-side copy, recycle bin, or cloud backup to purge.

**How to delete your data:**
1. **Individual notes/files:** Delete from within the DNotepad app.
2. **All app data:** Go to **Android Settings → Apps → DNotepad → Storage → Clear Data**. This permanently erases all databases, preferences, and caches from your device.
3. **Complete removal:** Uninstalling DNotepad permanently erases all internal application databases, preferences, and caches.

*Because DNotepad collects no server-side data, no external data deletion request process exists — there is nothing stored on our end to delete.*

### Cloud Backup — Explicitly Disabled

DNotepad's `backup_rules.xml` and `data_extraction_rules.xml` explicitly exclude all app data domains (root, file, database, sharedpref, external) from Google Drive Auto-Backup. DNotepad will never appear in your Google Drive backup storage.

### Device-to-Device Transfer

When you set up a new Android device from your old one (via Android's device migration wizard), Android's `device-transfer` mechanism may transfer DNotepad's local database and settings directly between your own physical devices over a local, encrypted connection (such as Wi-Fi Direct or a cable). It does not route through any cloud server or DNotepad infrastructure. You can exclude DNotepad from device transfers via your device manufacturer's setup settings.

### Security Practices

- All app data is protected by Android's per-application sandboxing.
- On devices with a screen lock enabled, all app data is protected by device-level hardware encryption (AES-256 on most modern Android devices).
- DNotepad does not transmit any data in transit — there is no transmission of any kind.
- The app uses the `FileProvider` API (not direct file URIs) when sharing files with other apps, ensuring no unintended file exposure.

---

## 6. Your Privacy Rights

Even though DNotepad collects no personal data on any server, we recognise and respect the privacy rights granted to users under applicable laws.

### Under GDPR (European Economic Area & UK Residents)

Under the General Data Protection Regulation (GDPR), you have the right to:

| Right | What it means for DNotepad |
|---|---|
| **Access** | DNotepad holds no personal data on any server. |
| **Rectification** | All your data is local; you have full control. |
| **Erasure ("Right to be Forgotten")** | Clear app data or uninstall — no server copy exists. |
| **Restriction of Processing** | Not applicable — we process nothing remotely. |
| **Data Portability** | Your files are standard file-system files; export at any time. |
| **Object** | Not applicable — no personal data is processed remotely. |

DNotepad operates on the legal basis of **legitimate interest** for local data processing (displaying your own notes back to you on your own device) and **user consent** for permissions such as notifications.

### Under CCPA (California Residents)

Under the California Consumer Privacy Act (CCPA), you have the right to:

- **Know** what personal information is collected, used, shared, or sold. *(We collect, use, share, and sell nothing.)*
- **Delete** personal information. *(Clear app data or uninstall.)*
- **Opt-out of sale.** *(We do not sell personal information.)*
- **Non-discrimination** for exercising your rights.

### Exercising Your Rights

The most direct and complete way to exercise any of the above rights is to:
1. Delete specific items within the DNotepad app.
2. Use **Android Settings → Apps → DNotepad → Clear Data** to erase all app data.
3. Uninstall the app to erase all data entirely.

For any questions about your rights, contact us at the address in Section 9.

---

## 7. Children's Privacy (COPPA Compliance)

DNotepad is an offline productivity tool that does not collect, solicit, transmit, or store personal information from any user, including children under the age of 13. The application is completely offline, non-commercial, and imposes no registration or account requirement. DNotepad is safe for all audiences and fully complies with the Children's Online Privacy Protection Act (COPPA).

---

## 8. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect new on-device features, changes to Android platform requirements, or to maintain Google Play compliance. Any revisions will be published at the GitHub repository listed in Section 9 with an updated "Last Updated" date.

We will not make changes that retroactively reduce your privacy protections without clear notice. Continued use of DNotepad after a policy update constitutes acceptance of the revised policy. If you disagree with any update, you may uninstall the application.

---

## 9. Contact Information

If you have any questions, suggestions, or concerns regarding this Privacy Policy, DNotepad's offline architecture, or your privacy rights, please contact:

**Developer:** RathoreSVikas  
**GitHub Repository & Privacy Policy Source:** [https://github.com/rathoresvikas-org/dnotepad_privacy](https://github.com/rathoresvikas-org/dnotepad_privacy)  
**Support Email:** [rathoresvikas@outlook.com](mailto:rathoresvikas@outlook.com)

We aim to respond to all privacy-related enquiries within **30 days**.

---

## 10. In-App Accessibility

This Privacy Policy is accessible from within DNotepad via the app's Help / About section. It is also linked on the Google Play Store listing page for DNotepad.

---

*This Privacy Policy was last reviewed for Google Play compliance on **September 30, 2026**.*
