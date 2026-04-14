## Feature 6: Audit & Persistence
### 1. Executive Summary
 * **Title:** Version Control, Data Integrity, and Recovery Protocols
 * **Summary:** This feature ensures the long-term reliability of the system. It focuses on how data is written, backed up, and versioned. By implementing "Soft Deletes" and a "Write-Ahead" strategy, the system protects the user from accidental data loss and provides a historical trail of changes to manual entries.
### 2. Context & Objectives
 * **Background:** In a personal system, the user is the primary admin. Accidental deletions or corrupted saves can lead to devastating data loss. Traditional file systems don't always provide an easy "undo" for file-level changes made over long periods.
 * **Goals:** * Prevent permanent data loss from accidental deletion.
   * Ensure file integrity during the save process.
   * Provide a mechanism to "Time Travel" through previous versions of a log.
 * **Non-Goals:** This will not replace a full Git implementation; it is a high-level safety layer within the app itself.
### 3. Proposed Solution
#### High-Level Architecture
The system adopts a **"Safe-Write"** pattern. When a user saves an entry, the application writes to a temporary hidden file first, verifies the write, and then swaps it with the original.
#### Detailed Design
 * **Soft Deletes (The Trash Directory):** Instead of calling a delete command on the OS, the system moves the file to a hidden .trash directory at the root. Files remain here for 30 days before permanent purging.
 * **Snapshotting (Local Versioning):** Before an edit is committed, the system can optionally save a copy of the current file to a .versions subfolder. This allows the UI to offer a "Compare Versions" view.
 * **Integrity Checks:** Upon startup, the system runs a checksum scan to ensure that Markdown files haven't been corrupted or truncated.
### 4. Alternatives Considered
 * **Relying on Cloud Sync (Dropbox/Drive) Versioning:** Dismissed as the primary solution because it's inconsistent across providers and requires the user to leave the app to recover data.
 * **Database Transactions:** Dismissed to maintain the "Flat-File" architecture. Instead, we mimic transactions through file-swapping logic.
### 5. Execution Plan
 * **Phase 1:** Implement the "Atomic Save" logic (Temp File -> Verify -> Swap).
 * **Phase 2:** Build the Trash/Recovery UI to allow users to restore moved files.
 * **Phase 3:** Develop a "Snapshot Manager" to allow for basic version comparison in the entry portal.
### 6. Risks & Mitigations
 * **Risk:** The .trash and .versions folders taking up significant disk space over time.
 * **Mitigation:** Implement a configurable "Cleanup Policy" that limits the size of the version history or the age of deleted files (e.g., "Keep only the last 5 versions").