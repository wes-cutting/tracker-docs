## Feature 3: Precision Temporal Engine
### 1. Executive Summary
 * **Title:** Immutable Audit-Trail and Flexible Event-Time Mapping
 * **Summary:** This feature manages the "When" of every log entry. It distinguishes between the moment an event actually happened and the moment it was recorded, ensuring that personal history remains accurate even when logs are entered after the fact.
### 2. Context & Objectives
 * **Background:** In manual logging, there is often a gap between an event and the record-keeping (e.g., logging a morning workout in the evening). Relying on a single "Created At" timestamp leads to an inaccurate personal timeline.
 * **Goals:** * Implement **Dual-Timestamping** for every entry.
   * Maintain an immutable record of entry creation for audit purposes.
   * Support manual override for "Event Time" with a precision-focused UI.
 * **Non-Goals:** This engine will not automatically sync with external calendars, as it focuses strictly on the internal log integrity.
### 3. Proposed Solution
#### High-Level Architecture
The system utilizes a "Temporal Service" that generates a multi-point time object for every file. This object is stored in the YAML frontmatter to ensure the data stays with the file.
#### Detailed Design
 * **The Timestamp Duo:**
   * event_at: The user-defined time of the occurrence.
   * recorded_at: The system-generated, immutable UTC timestamp of when the file was saved.
 * **Normalization Layer:** All times are stored in ISO 8601 UTC format. The UI translates these to the user's local timezone on-the-fly to ensure the directory remains readable regardless of travel or DST changes.
 * **Time-Picker UI:** A specialized entry component that defaults to "Now" but allows for quick-select offsets (e.g., "-15m", "-1h", "Yesterday").
### 4. Alternatives Considered
 * **Single Timestamp (System Time Only):** Dismissed. It makes it impossible to retroactively log events accurately.
 * **Storing Local Time Only:** Dismissed. This creates "gaps" or "overlaps" in the timeline if the user changes timezones or if Daylight Savings occurs.
### 5. Execution Plan
 * **Phase 1:** Standardize the YAML frontmatter to include event_at, recorded_at, and timezone_offset.
 * **Phase 2:** Develop the UI component for precision time selection.
 * **Phase 3:** Create a "Chronology Guard" that warns the user if they are attempting to log an event_at date that is in the future.
### 6. Risks & Mitigations
 * **Risk:** Users might accidentally back-date entries and lose track of the true creation date.
 * **Mitigation:** The recorded_at field is hidden from the standard entry form and is only accessible via "Advanced Info" to act as a permanent source of truth.