Understood. We will reset the focus to the **Architectural Features** list we generated earlier, applying each one to the formal **Design Proposal** structure.
We’ll start with the first architectural pillar: **The Hierarchical Data Model**.
## Feature 1: Hierarchical Data Model (Directory-Style)
### 1. Executive Summary
 * **Title:** Recursive Directory & Hierarchical Log Organization
 * **Summary:** This feature establishes the core organizational logic of the system. It moves away from flat tagging by implementing a nested path structure, allowing the user to group logs into logical parents and sub-categories (e.g., /Project/Coding/Bug-Fixes).
### 2. Context & Objectives
 * **Background:** Personal data often follows a natural hierarchy. A flat list becomes unmanageable as the volume of logs grows, making it difficult to find related context.
 * **Goals:** * Support infinite nesting of categories and subcategories.
   * Enable "inheritance" where sub-folders can inherit the properties of their parents.
 * **Non-Goals:** This feature is strictly about the logical grouping of files; it does not handle the search or visual timeline (which are separate modules).
### 3. Proposed Solution
#### High-Level Architecture
The system will use a **Materialized Path** approach. Each log entry is not just a standalone entity but is defined by its location within a string-based path.
#### Detailed Design
 * **Path Resolution:** Each log will store a path attribute (e.g., health/fitness/workouts).
 * **Virtual Directory Nodes:** The UI will dynamically generate "folder" views by grouping all entries that share a common path prefix.
 * **Move Logic:** When a category is renamed or moved, the system will perform a recursive update on all child logs to maintain the path integrity.
### 4. Alternatives Considered
 * **Adjacency List (Parent-ID):** Dismissed because querying deep trees in a flat-file/local environment is more computationally expensive than parsing a Materialized Path string.
 * **Tag-Only System:** Dismissed because it lacks the "spatial" mental model that directories provide, making it harder to browse by "area of life."
### 5. Execution Plan
 * **Phase 1:** Define the path parsing utility that converts strings into UI tree nodes.
 * **Phase 2:** Build the "Breadcrumb" navigation component.
 * **Phase 3:** Implement the "Directory Browser" sidebar to allow for folder-based exploration.
### 6. Risks & Mitigations
 * **Risk:** Deeply nested paths leading to extremely long file URLs or path names.
 * **Mitigation:** Enforce a maximum character limit for directory names and provide a "slugification" utility to keep paths URL-friendly.