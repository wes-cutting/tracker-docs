## Feature 2: Path-Based Navigation (The "Omnibar")
### 1. Executive Summary
 * **Title:** Command Palette & URI-style Path Navigation
 * **Summary:** This feature replaces deep-tree clicking with a keyboard-centric "Omnibar." It allows for rapid jumping between directories and creation of new subcategories using a familiar file-path syntax (e.g., work/research/api-docs).
### 2. Context & Objectives
 * **Background:** As a personal log grows, the directory structure becomes deep. Manual clicking through folders is slow and discourages deep organization.
 * **Goals:** * Enable navigation to any subfolder in under 3 keystrokes using fuzzy search.
   * Allow users to "teleport" between disparate categories (e.g., from Finance to Hobbies) instantly.
 * **Non-Goals:** This is not a global content search (which is a separate feature); it is specifically for **structural navigation**.
### 3. Proposed Solution
#### High-Level Architecture
The UI will feature a persistent command palette (Ctrl/Cmd + K). This component listens to the local file system's directory structure and indexes folder names into a client-side fuzzy search provider.
#### Detailed Design
 * **The "Breadcrumb" Parser:** A utility that converts the current active path into a clickable UI element, allowing for easy upward navigation.
 * **Path-Creation Logic:** If a user types a path in the Omnibar that doesn't exist (e.g., travel/2026/italy), the system will offer a "Create and Go" shortcut, automatically generating the nested folders.
 * **Fuzzy Matching:** Implementation of a scoring algorithm (like Smith-Waterman) to prioritize exact matches and recently visited directories.
### 4. Alternatives Considered
 * **Permanent Sidebar Tree:** While useful, it consumes screen real estate and is inefficient for deep hierarchies. The Omnibar will complement the sidebar, not replace it.
 * **Tag-Only Navigation:** Dismissed because it lacks the physical organizational mental model of a "directory" that the user requested.
### 5. Execution Plan
 * **Phase 1:** Build the fuzzy search index for the existing directory structure.
 * **Phase 2:** Develop the Ctrl + K overlay and the "Jump to Path" logic.
 * **Phase 3:** Integrate "Quick Folder Creation" directly from the bar.
### 6. Risks & Mitigations
 * **Risk:** Overlapping shortcut keys with the browser or OS.
 * **Mitigation:** Provide a customizable shortcut setting and a visible "Search" icon in the UI as a fallback.
