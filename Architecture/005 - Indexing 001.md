## Feature 5: Search & Discovery Architecture
### 1. Executive Summary
 * **Title:** Full-Text Indexing and Multi-Dimensional Discovery
 * **Summary:** This feature provides the "retrieval" engine for the system. It enables the user to query their entire personal history through full-text search, metadata filtering, and structural browsing, ensuring that information remains accessible even as the directory grows to thousands of entries.
### 2. Context & Objectives
 * **Background:** A directory structure is excellent for organization but poor for discovery when the specific location of a log is forgotten. A robust search layer turns a "storage system" into a "knowledge base."
 * **Goals:** * Provide sub-second search results across all log content and metadata.
   * Enable "Discovery Filters" to slice data by time, category, or tags.
 * **Non-Goals:** This engine will not search external cloud drives or emails; it is scoped strictly to the local logging directory.
### 3. Proposed Solution
#### High-Level Architecture
The system utilizes a **Client-Side Indexing** approach. Since the tool is "Local-First," an index is built in the background using a library like **FlexSearch** or **MiniSearch**, which resides in the user's local memory/cache.
#### Detailed Design
 * **Inverted Indexing:** The system scans all Markdown files and creates an inverted index of every word, mapped back to the file path.
 * **Scoped Queries:** Support for advanced search syntax:
   * path:"work/projects": Limits search to a specific directory.
   * after:2026-01-01: Limits search by date.
   * category:technical: Filters by metadata schema.
 * **Fuzzy Matching:** Implementation of Levenshtein distance logic to account for typos or partial word recalls during manual entry retrieval.
### 4. Alternatives Considered
 * **Grep/Standard OS Search:** Dismissed because it cannot parse YAML metadata or offer the speed of a pre-built index within the portal UI.
 * **Server-Side Search (Elasticsearch):** Dismissed for a personal tool as it requires heavy infrastructure and compromises the "local-only" privacy model.
### 5. Execution Plan
 * **Phase 1:** Build the background worker that crawls the directory and indexes files.
 * **Phase 2:** Create the "Search Results" UI with keyword highlighting and breadcrumb paths.
 * **Phase 3:** Implement "Saved Searches" or "Smart Folders" (e.g., a folder that automatically shows all logs with the tag #todo).
### 6. Risks & Mitigations
 * **Risk:** High memory usage for very large log collections.
 * **Mitigation:** Use a "Lazy Loading" indexer that only loads full-text into memory for recently accessed or high-priority directories.