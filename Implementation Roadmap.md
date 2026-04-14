The **Master Implementation Roadmap** consolidates these six architectural pillars into a logical build order. Instead of building features in isolation, we prioritize the **Core Storage** and **Entry** first to ensure the tool is usable immediately, followed by **Organization** and **Discovery** as the volume of logs grows.
## Phase 1: The Foundation (Week 1–2)
*Focus: Establishing the physical storage and the ability to capture data safely.*
 * [**Feature 4 (Persistence):**](./Features/004%20-%20Persistence%2001.md) Set up the Local-First File System logic. Establish the /root directory and Markdown parser.
 * [**Feature 6 (Audit):**](./Architecture/006%20-%20Persistence%20001.md) Implement "Atomic Saves" and the "Soft Delete" mechanism. Data must be safe before you start logging "real" information.
 * [**Feature 3 (Temporal Engine):**](./Architecture/003%20-%20Temporal%20Engine%2001.md) Implement the recorded_at and event_at logic in the YAML frontmatter.
## Phase 2: The Portal & Capture (Week 3–4)
*Focus: Creating a frictionless UI for manual entries.*
 * [**Feature 4 (Portal):**](./Architecture/004%20-%20Portal%20001.md) Build the actual text editor with Markdown preview and auto-save (Drafts) logic.
 * [**Feature 3 (Time UI):**](./Features/003%20-%20Relative%20Time%20Engine.md) Add the natural-language time picker (e.g., "1 hour ago") to the entry form.
 * [**The "Inbox" logic:**](./Features/001%20-%20Inbox%20Patten.md) (From our previous list) Set the default save location to /Inbox.
## Phase 3: Structural Organization (Week 5–6)
*Focus: Managing the directory tree and data types.*
 * [**Feature 1 (Hierarchy):**](./Architecture/001%20-%20Hierarchical%20Data%20Model.md) Implement the Materialized Path logic. Build the sidebar directory tree and breadcrumb navigation.
 * [**Feature 2 (Dynamic Schema):**](./Architecture/002%20-%20Schema%20001.md) Build the schemas.json engine. Allow the portal to change fields based on whether you are in /Work or /Health.
## Phase 4: Discovery & Intelligence (Week 7–8+)
*Focus: Making the data searchable and visually insightful.*
 * [**Feature 5 (Search):**](./Architecture/005%20-%20Indexing%20001.md) Implement the client-side indexing (FlexSearch). Build the global search overlay with path-based filtering.
 * [**Visualizations:**](./Features/005%20-%Visuals%201.md) Implement the Heatmap and Daily Timeline views to see logs across different directories in a single chronological stream.
## Phase 5: Advanced Navigation & Connectivity (Week 9-10+)
*Focus: Power-user features for rapid navigation and knowledge connectivity.*
 * [**Omnibar Navigation:**](./Features/002%20-%20Omnibar.md) Build the command palette with fuzzy search for instant directory jumping and path creation using Ctrl/Cmd + K.
 * [**Personal Search & Links:**](./Features/006%20-%20Indexing%2001.md) Implement scoped full-text search with wiki-style cross-linking ([[ ]]) and bidirectional reference tracking.
### Implementation Table: Priority vs. Complexity
| Task | Priority | Complexity | Value |
|---|---|---|---|
| **File System/Persistence** | Critical | Low | Data Portability |
| **Atomic Writes/Audit** | Critical | Medium | Data Safety |
| **Markdown Editor** | High | Medium | Entry Speed |
| **Dynamic Schema** | Medium | High | Data Integrity |
| **Full-Text Search** | Medium | High | Retrieval |

