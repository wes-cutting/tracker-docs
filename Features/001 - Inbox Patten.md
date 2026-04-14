Understood. We will take it one feature at a time, integrating them into the **Design Proposal** structure we established.
Since this is a personal tool focused on a local-first, file-based architecture, we’ll start with the foundation: the **Inbox Pattern**.
## Feature 1: The "Inbox" Pattern (Frictionless Entry)
### 1. Executive Summary
 * **Title:** Implementing the "Inbox" Entry & Processing Workflow
 * **Summary:** This feature introduces a low-friction landing zone for all new manual logs. By decoupling "capture" from "categorization," the user can record data instantly without navigating the directory tree, ensuring no information is lost due to cognitive overhead during the entry process.
### 2. Context & Objectives
 * **Background:** Personal logging often fails when the user has to decide exactly where a log belongs (e.g., "Is this a 'Project' log or a 'Meeting' log?") while in the middle of a task.
 * **Goals:** * Reduce "Time-to-Capture" to under 5 seconds.
   * Provide a dedicated view for "Unfiled" items that need organization.
 * **Non-Goals:** This will not handle automatic AI-categorization (sorting remains a manual, intentional act).
### 3. Proposed Solution
#### High-Level Architecture
The system will maintain a special directory at the root level labeled /Inbox. All entry points (Mobile Widget, Quick-Hotkey, or the Portal) will default to this path if no other directory is specified.
#### Detailed Design
 * **Data Models:** * A boolean flag is_filed: false will be added to the file metadata (YAML frontmatter).
   * Any file located in the /Inbox folder is treated as "pending."
 * **Logic:**
   * **The "Processing" UI:** A split-screen view where the user sees the Inbox log on the left and the directory tree on the right to facilitate quick "drag-and-drop" filing.
### 4. Alternatives Considered
 * **Forcing Categorization on Entry:** Dismissed because it creates "entry friction," leading to fewer logs being recorded.
 * **Auto-filing based on Keywords:** Dismissed to keep the system predictable and give the user total control over their personal directory structure.
### 5. Execution Plan
 * **Phase 1:** Create the global /Inbox directory and the default "Quick Add" button in the portal.
 * **Phase 2:** Implement the "Move" logic to update the file path and frontmatter when an item is filed.