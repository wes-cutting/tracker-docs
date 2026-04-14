## Feature 4: Flat-File or "Local-First" Persistence
### 1. Executive Summary
 * **Title:** Markdown-Based File System Storage & Persistence
 * **Summary:** This feature establishes the physical storage layer of the tool. Instead of an opaque database, logs are stored as human-readable .md files within a standard directory structure on the user's local disk. This ensures total data ownership, portability, and long-term durability.
### 2. Context & Objectives
 * **Background:** Personal data stored in proprietary databases is subject to "bit rot" or vendor lock-in. If the app stops working, the data should still be accessible via any text editor.
 * **Goals:** * Enable the "directory" organizational style via actual OS-level folders.
   * Ensure 100% offline functionality.
   * Allow users to use external tools (like Obsidian, VS Code, or Git) alongside this portal.
 * **Non-Goals:** This system will not implement a proprietary encryption layer at the file level (security is deferred to the OS/disk encryption).
### 3. Proposed Solution
#### High-Level Architecture
The application acts as a "window" over a specific local directory. It uses a File System Watcher to sync the UI state with the disk state in real-time.
#### Detailed Design
 * **Storage Schema:** * **Root:** /MyLogs/
   * **Folders:** Represent Categories/Subcategories.
   * **Files:** Each log entry is a file named YYYY-MM-DD-HHmm-Title.md.
 * **Frontmatter Parsing:** Every file starts with a YAML block. The application reads this to populate the UI’s filter and search features without needing a central database.
 * **File System API (FSA):** For the web portal version, use the Browser’s File System Access API to let the user "mount" their local folder directly.
### 4. Alternatives Considered
 * **SQLite Database:** While fast, it makes the data "invisible" to other tools and harder to version control via Git.
 * **JSON Blob Storage:** Dismissed because JSON is harder for humans to read and edit manually compared to Markdown.
### 5. Cross-Cutting Concerns
 * **Data Integrity:** When a user renames a category in the UI, the system must perform a recursive folder rename on the disk.
 * **Conflicts:** If a file is edited in an external editor while the portal is open, the "Last Write Wins" strategy or a simple "File Changed" reload prompt will be used.
### 6. Execution Plan
 * **Phase 1:** Implement the File System "Mounting" logic and directory scanning.
 * **Phase 2:** Build the Markdown/YAML parser to turn flat files into interactive UI objects.
 * **Phase 3:** Establish the "Safe-Write" protocol (writing to a temporary file before replacing the original to prevent data loss).