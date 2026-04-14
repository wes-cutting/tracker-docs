## Feature 3: Metadata & Contextual Awareness (The "Relative Time" Engine)
### 1. Executive Summary
 * **Title:** Temporal Metadata Enrichment and Relative Time Parsing
 * **Summary:** This feature automates the capture of situational context (time, device, and timezone) for every entry. It includes a "Natural Language" parser that allows the user to log events using relative terms (e.g., "30 mins ago") while ensuring the underlying data remains anchored to an absolute UTC timestamp.
### 2. Context & Objectives
 * **Background:** Manual time entry is often accurate but tedious. Users often remember events relative to the "now" (e.g., "I started this an hour ago"). Forgetting to change the default timestamp leads to "dirty data" in personal history.
 * **Goals:** * Eliminate manual date/time picking for 90% of entries.
   * Provide "Passive Context" (device type) to aid future memory recall.
 * **Non-Goals:** This will not use GPS/Location tracking to preserve privacy and minimize battery/resource drain on mobile devices.
### 3. Proposed Solution
#### High-Level Architecture
The entry portal will utilize a "Context Collector" service that intercepts the save action to inject metadata into the file’s YAML frontmatter.
#### Detailed Design
 * **Relative Time Parser:** A logic layer that transforms strings like "Yesterday 10am" or "5m ago" into ISO 8601 timestamps before the file hits the disk.
 * **Dual-Clock Logic:**
   * **event_at:** The parsed/user-intended time.
   * **captured_at:** The immutable system time when the "Save" button was pressed.
 * **Device Fingerprinting:** A simple key-value pair stored in the metadata (e.g., source: iPad-Pro or source: Desktop-Chrome) based on the User-Agent or a local configuration file.
### 4. Alternatives Considered
 * **Strict Manual Selection:** Dismissed as it creates friction and leads to users "lying" to the system by just accepting whatever the default time is.
 * **Third-Party Calendar Sync:** Considered for context, but dismissed to keep the tool "Local-First" and independent of external APIs.
### 5. Execution Plan
 * **Phase 1:** Update the frontmatter schema to support the new metadata fields.
 * **Phase 2:** Integrate a natural language date library (e.g., Chrono or date-fns) into the entry portal.
 * **Phase 3:** Create a "Metadata Preview" in the UI so the user can see what passive data is being recorded.
### 6. Risks & Mitigations
 * **Risk:** Timezone confusion when traveling.
 * **Mitigation:** Always store the offset (e.g., UTC-5) alongside the timestamp so the log remains geographically anchored.