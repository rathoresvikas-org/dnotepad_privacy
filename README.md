# Privacy Policy for DNotepad

**Effective Date:** September 14, 2026  
**Last Updated:** September 14, 2026

**DNotepad** app, developed by **RathoreSVikas**, is an advanced, privacy-first, 100% offline Text Editor, Source Code IDE, and Notes Workspace for Android. 

We believe that your personal notes, documents, source code, and data belong exclusively to you. DNotepad is engineered from the ground up to operate completely without internet access, ensuring absolute confidentiality, privacy, and zero data collection.

---

### 1. 100% Offline Architecture & Zero Data Collection

* **No Internet Permissions at the OS Level:** DNotepad does not possess, request, or use the Android `INTERNET` or `ACCESS_NETWORK_STATE` permissions. At the Android operating system and Linux kernel level, DNotepad is physically blocked from opening network sockets or transmitting data over the internet.
* **No Remote Servers or Cloud Sync:** We do not own, operate, or connect to cloud servers. No user documents, source code, notes, images, or metadata are ever transmitted, synced, or uploaded to any external server.
* **Zero Tracking, Telemetry, or Analytics:** DNotepad contains no advertising frameworks, no tracking SDKs, no analytics services, and no remote crash reporting libraries. We do not track what you type, compile, view, or organize.
* **No Personal Data Harvesting:** We do not collect, buy, sell, share, or monetize personal information (such as your name, email address, phone number, location data, or device identifiers).

---

### 2. Feature-Specific Local Data Handling

All data processing, execution, and storage within DNotepad occur strictly inside the secure sandbox of your local device:

#### A. Text & Source Code Editor
* All text files, source code scripts, and documents opened, edited, or created in DNotepad are read directly from and written directly to your device's local file system or SD card via Android Storage Access Framework.
* No telemetry or document contents are intercepted, logged, or exported.

#### B. Offline Multi-Language Code Compilation & Execution
* DNotepad includes an embedded multi-language execution engine (supporting Python via on-device Chaquopy CPython, Java via on-device BeanShell on ART, Kotlin via local AST transpilation, C/C++ via local WebAssembly, and HTML/CSS/JavaScript/SVG via sandboxed local WebView).
* All code execution, script interpretation, and visual document previews run 100% locally within on-device sandboxed execution environments. 
* No source code or execution output is dispatched to external compilation servers.

#### C. Notes & Workspace Management
* Text notes, checklists, category tags, and embedded image attachments are stored exclusively in a sandboxed local SQLite/Room database located within the application's private internal storage, protected by Android's operating system isolation and device-level hardware encryption.
* Quick capture widgets, sticky memos, and action bars interact strictly with your local device database.

#### D. AI Quota Tracker & Countdown Timers
* The AI Quota Tracker and accompanying home screen widgets are 100% manual, on-device calculation and countdown tools designed to help you track your own subscription cycles (e.g., Claude, ChatGPT, Grok).
* DNotepad does not connect to, authenticate with, or communicate with OpenAI, Anthropic, Google, xAI, or any third-party AI APIs. All quota numbers and reset schedules are stored purely in local device preferences.

#### E. On-Device Optical Character Recognition (OCR) & Local ML
* DNotepad provides local text recognition (OCR) and document summarization.
* Image scanning, character extraction, and text summarization are executed entirely on-device using bundled offline machine learning models (bundled Google ML Kit and LiteRT / TensorFlow Lite). 
* Your photos, scanned documents, and extracted text never leave your physical device.

---

### 3. Device Permissions & Transparency

DNotepad requests only the minimal permissions necessary to function as a powerful offline file editor and productivity workspace:

* **All Files Access / Storage (`MANAGE_EXTERNAL_STORAGE`, `READ_EXTERNAL_STORAGE`, `WRITE_EXTERNAL_STORAGE`):**
  * *Purpose:* Required strictly to provide core editor functionality—enabling you to browse, open, view, edit, compile, and save text documents, code files, and projects across your device’s internal storage and external SD cards.
* **Exact Alarms, Notifications & Foreground Services (`SCHEDULE_EXACT_ALARM`, `POST_NOTIFICATIONS`, `FOREGROUND_SERVICE`):**
  * *Purpose:* Required solely to trigger local task, checklist, and note reminders that you explicitly schedule within the app, and to execute background maintenance tasks (such as autosave cleanup).
  * *Why This Is Safe:* DNotepad does not request or use `USE_EXACT_ALARM`. Note reminders operate via standard `SCHEDULE_EXACT_ALARM` with a 3-tier defensive fallback:
    * If `canScheduleExactAlarms()` → uses `setExactAndAllowWhileIdle()` ✅
    * If not → falls back to `setAndAllowWhileIdle()` (slightly inexact but works) ✅
    * If `SecurityException` → falls back to `set()` ✅
* **Boot & Hardware Triggers (`RECEIVE_BOOT_COMPLETED`, `VIBRATE`, `WAKE_LOCK`):**
  * *Purpose:* Required to restore your scheduled local reminders if your device reboots, and to provide haptic feedback and alarm alerts when reminders fire.

---

### 4. Third-Party Libraries and Runtimes

To provide offline compilation, syntax highlighting, and local text recognition, DNotepad bundles select open-source libraries (such as bundled offline ML Kit text recognition, AndroidX components, Chaquopy, and embedded script engines). 

* All bundled libraries and runtimes execute strictly within the local device environment.
* Because DNotepad strips all network permissions (`INTERNET` and `ACCESS_NETWORK_STATE`) from its manifest, no third-party library has the technical capability to transmit data from your device.

---

### 5. Data Retention, Security, and User Deletion Rights

Because all data resides strictly on your physical hardware:
* **Total User Control:** You maintain absolute ownership and authority over all files and notes.
* **Immediate Deletion:** Deleting a note, task, or file inside DNotepad permanently deletes it from the local database or storage immediately.
* **Full App Erasure:** Clearing DNotepad's storage in Android Settings or uninstalling the application permanently erases all internal application databases, preferences, and temporary caches from your device.
* **Device Backup:** DNotepad operates no cloud backup services. Any backup of your app data is strictly governed by your device's operating system settings (such as your personal Android Google Drive backup).

---

### 6. Children's Privacy (COPPA Compliance)

DNotepad is an offline productivity tool that does not collect, solicit, or store personal information from anyone, including children under the age of 13. The application is completely offline, non-commercial, and safe for all audiences.

---

### 7. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect future on-device features or platform requirements. Any revisions will be published with an updated "Last Updated" date.

---

### 8. Contact Information

If you have any questions, suggestions, or concerns regarding this Privacy Policy or DNotepad's offline architecture, please contact:

* **Developer:** RathoreSVikas
* **GitHub Repository:** [https://github.com/rathoresvikas-org/dnotepad_privacy]
* **Support Email:** [rathoresvikas@outlook.com]
