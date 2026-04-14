## Feature 6: Personal Search & Linked References
### 1. Executive Summary
 * **Title:** Scoped Full-Text Search and Wiki-style Cross-Linking
 * **Summary:** This feature transforms a collection of isolated files into a connected knowledge base. It introduces a high-speed search engine that respects directory boundaries and a linking syntax ([[link]]) that allows entries to reference one another regardless of their physical location on the disk.
### 2. Context & Objectives
 * **Background:** As the directory grows, finding specific information via manual navigation becomes impossible. Furthermore, personal events are often related across categories (e.g., a "Learning" log related to a "Project" log).
 * **Goals:** * Provide sub-second search results across all Markdown content.
   * Enable "Bidirectional Linking" so users can see which logs reference the current entry.
 * **Non-Goals:** This will not support web-wide searching; it is strictly limited to the user's local directory.
### 3. Proposed Solution
#### High-Level Architecture
The system utilizes a client-side indexing engine (like FlexSearch) that runs in the browser or local environment. It builds a "Map of Connections" by parsing the Markdown text for specific linking patterns.
#### Detailed Design
 * **Scoped Search Syntax:** Implementation of search modifiers such as in:work (search only within the work directory) or type:aftercare (filter by category metadata).
 * **Wiki-Links ([[ ]]):** A parser that detects double-bracketed text and turns it into a functional internal hyperlink.
 * **Backlink Indexing:** A "References" section at the bottom of each log that lists every other file that links to it.
### 4. Alternatives Considered
 * **Standard OS Search:** Dismissed because it cannot filter by YAML metadata or understand the custom [[ ]] link syntax.
 * **Centralized Link Database:** Dismissed. To keep it local-first, the "links" are discovered by scanning the files, ensuring the file remains the single source of truth.
### 5. Cross-Cutting Concerns
 * **Refactoring:** If a user renames a file, the system should ideally offer to update all [[links]] pointing to that file to prevent broken connections.
 * **Performance:** The search indexer will prioritize the "Title" and "Tags" metadata for instant results, with full-body text indexing happening as a secondary process.
### 6. Execution Plan
 * **Phase 1:** Integrate the full-text search engine and build the initial index from the local directory.
 * **Phase 2:** Implement the Regex-based link parser to enable clickable internal navigation.
 * **Phase 3:** Develop the "Backlink" UI component to show relationships between logs.
 
This completes the integration of all requested features into the Design Proposal. Your system now has a solid blueprint for a **local-first, frictionless, and highly organized personal logging portal.** Since you mentioned you're a software engineer, do you want to dive into the specific implementation of any of these phases, or perhaps look at how to structure the **Git-based sync logic** to keep your logs consistent across your devices?
