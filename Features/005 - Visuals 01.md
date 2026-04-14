## Feature 5: Visual Timeline & Heatmaps
### 1. Executive Summary
 * **Title:** Chronological Activity Visualization & Frequency Mapping
 * **Summary:** This feature adds a temporal visualization layer to the file-based system. It aggregates metadata from across the entire directory structure to present a unified "Daily Timeline" view and a GitHub-style "Activity Heatmap," allowing the user to spot patterns in their logging behavior over time.
### 2. Context & Objectives
 * **Background:** In a directory-heavy system, it is easy to lose the "thread" of a day because logs are scattered across different folders (e.g., a "Health" log and a "Work" log).
 * **Goals:** * Provide a unified chronological narrative of the user's day.
   * Visualize consistency and "log density" to encourage regular documentation.
 * **Non-Goals:** This is a read-only visualization; it will not be used for bulk editing of logs.
### 3. Proposed Solution
#### High-Level Architecture
The system will run a lightweight background indexer that scans the event_at frontmatter from all Markdown files. This indexed data is then fed into a time-series visualization component.
#### Detailed Design
 * **The "Daily Stitch":** A view that queries all files where the date matches today (regardless of their directory) and sorts them vertically by time.
 * **Activity Heatmap:** A 12-month grid where each cell represents a day. The "color depth" of the cell is determined by the count of files created on that date.
 * **Filter Layer:** Allows the user to toggle specific categories on/off in the timeline to see, for example, only "Project" logs alongside "Meeting" logs.
### 4. Alternatives Considered
 * **Folder-Specific Timelines:** Dismissed as too narrow. The value of a personal tool is seeing the "whole picture" of a life/day.
 * **External Analytics Integration:** Dismissed to maintain the "Local-First" and privacy-centric nature of the project.
### 5. Execution Plan
 * **Phase 1:** Develop the fast-scan indexing logic to pull timestamps from files without loading full content.
 * **Phase 2:** Implement the Heatmap UI using a lightweight charting library (e.g., D3.js or a simple CSS Grid).
 * **Phase 3:** Build the "Daily Narrative" view with expand/collapse logic for reading log snippets.
### 6. Risks & Mitigations
 * **Risk:** Performance lag when scanning thousands of files.
 * **Mitigation:** Cache the metadata index in a local metadata.json or a small SQLite sidecar to avoid re-scanning every file on every page load.