# User Story Evaluation

**Work Item:** [#1727233](https://tfs.realpage.com/tfs/Realpage/AOS/_workitems/edit/1727233)
**Date:** 2026-04-16

---

## User Story Content

**Title:** Settings - Floor Plan - List View - Auto Pilot (2 of 2) - Columns Filter Data and Interaction of Colum filter With Horizontal filter

**Description:**
As an RM user on Settings > New Floor Plan Parameters > List View > Column Filter, I want each section of the 'Column Filter' aside to display the parameters that I have selected via the dropdown, so that I may have visibility on my selection and a way to deselect using the 'x'.

Furthermore I want that the horizontal filter option and Column filter option be independent of each other and not work in conjunction (on top of) with each other for a smooth user experience.

> **Note:** This enhancement is for US, UK and Canadian sites and for all property types.
> AC001, 002 for Column Filter Functionality covered on [#1708534](https://tfs.realpage.com/tfs/Realpage/AOS/_workitems/edit/1708534).
> Figma: https://www.figma.com/proto/hls5z78A4AL5MzKqd3IwbS/Setting-Updates?node-id=1009-169195

**Acceptance Criteria:**

**AC001** — Given an RM user on Settings > Floor Plan Parameters > List View, when I click the 'Column Filters' button, then an aside opens with:
- Header: "Column Filters"
- Parameter labels displayed section-wise under each corresponding section
- Three buttons: Clear Filters (only when ≥1 parameter selected), Close, Apply Filters (disabled when no selections)

**AC002** — Given the Column Filters Aside is open, when I select one or more parameters across same or different sections, then my selected parameter labels are displayed:
- Under each corresponding section
- In alphabetical order per section (post selection)
- In blue highlight with an 'x' to cancel/remove
- Apply Filters button is enabled

**AC003a** — When I click 'Clear Filters', then selections clear out and uncheck, aside remains open, no filters are set.

**AC003b** — When I click 'Apply Filters', then aside closes and the list view grid only reflects the selected column filter parameters; grid width adjusts based on grid content.

**AC004** — Given column filters are selected, when I make changes (add/remove) to property or FP dropdown selections, then column filter selections are retained and grid displays correct data; grid width adjusts based on grid content.

**AC005** — Given one or more column filters are applied, when I navigate to a different Settings tab, different workflow, hit back in browser, or refresh, then the page resets to default view (no filters selected, 'All' defaults).

**AC006** — (Mutual exclusivity) When I have applied horizontal filters and then apply column filters, then horizontal filters are cleared and only column filters remain active.

**AC007** — (Mutual exclusivity) When I have applied column filters and then apply horizontal filters, then column filters are cleared and only horizontal filters remain active.

---

## Weight Percentage Matrix

**Selected Framework Row:** Row 1
**Excluded Categories:** None

| Core Structure | Functional Req. | Validation Specs | Non-Functional | UI/UX | API | DB | Total % |
|----------------|-----------------|------------------|----------------|-------|-----|----|---------|
| 30%            | 15%             | 15%              | 10%            | 10%   | 10% | 10%| 100%    |

---

## Evaluation Matrix

| Category                    | Weight | Score (1–10) | Weighted Score | Comments                                                         |
|-----------------------------|--------|--------------|----------------|------------------------------------------------------------------|
| Core Structure              | 30%    | 8.0          | 2.4            | Strong "As a / I want / So that" format; 7 detailed ACs; missing negative/error ACs |
| Functional Requirements     | 15%    | 8.0          | 1.2            | All interactions, outcomes, and paths well-covered; Save/Cancel noted as not yet developed |
| Validation Specifications   | 15%    | 4.0          | 0.6            | Independently testable with clear success criteria; no test data or sample scenarios |
| Non-Functional Requirements | 10%    | 1.0          | 0.1            | None specified; performance, scalability, security all absent |
| UI/UX Requirements          | 10%    | 4.0          | 0.4            | Visual appearance, layout, and Figma link present; missing responsiveness, browser support, localization |
| API Requirements            | 10%    | 1.0          | 0.1            | No API endpoints, methods, or response formats defined |
| DB Requirements             | 10%    | 1.0          | 0.1            | No data storage, tables, or constraints defined |
| **TOTAL**                   | **100%**| **3.9**     | **4.9**        | **Adequate — Basic details but gaps exist** |

---

## Detailed Evaluation

### 1. Core Structure

✓ Uses "As a [user], I want..., So that..." format
✓ Identifies user role (RM user)
✓ Specifies user goal (display column filter selections; independent filter behavior)
✓ States user value (visibility on selections and ability to deselect)
✓ Title is clear (descriptive, though long)
✓ Description provides context (navigation path, scope note for US/UK/CA, Figma link, reference to prior US #1708534)
✓ Acceptance Criteria: specific and testable (7 ACs in Given/When/Then format)
✓ Acceptance Criteria: clear language (structured and unambiguous)
✗ Acceptance Criteria: includes positive AND negative cases (all ACs cover positive behavior; no error scenarios, e.g., failed API call, empty parameter list, or boundary conditions)

**Score: 8.0 / 10**

---

### 2. Functional Requirements

✓ Feature behavior defined (column filter aside display and mutual exclusivity with horizontal filters)
✓ All user interactions listed (open aside, select parameter, remove via 'x', clear all, apply, close, navigate away)
✓ Expected outcomes clear (each AC has explicit "Then" clauses)
✓ Step-by-step user journey present (ACs 001–007 form a complete journey)
✓ Integration with workflow described (interaction with horizontal filters in 006/007; property/FP dropdown in 004)
✓ Entry/exit points defined (button click opens aside; Apply Filters closes aside; navigation resets in 005)
✓ All possible user paths covered (select/apply/clear/retain/reset/mutual-exclusivity paths all present; note: Save and Cancel are flagged as "not developed yet" in AC004)

**Score: 8.0 / 10**

---

### 3. Validation Specifications

✗ Test data requirements specified ("Not a Previously Required Field" — no sample data for parameters, property types, or grid content)
✗ Sample scenarios provided (ACs describe behavior but no concrete data examples, e.g., "select 'Rent' and 'Occupancy' parameters")
✓ Story is independently testable (each AC is self-contained with Given/When/Then)
✓ Success/failure criteria defined (explicit acceptance outcomes in each AC)
✗ Measurable outcomes present (no quantitative metrics; e.g., no threshold for grid render time, no parameter count limits)

**Score: 4.0 / 10**

---

### 4. Non-Functional Requirements

✗ Response time specified
✗ Throughput specified
✗ Resource utilization specified
✗ Scalability addressed (US/UK/CA scope is market coverage, not a scalability requirement)
✗ Access control defined (RM user role mentioned but no permissions or role-based access detail)
✗ Data protection addressed
✗ Compliance requirements stated
✗ Logging/auditing covered

**Score: 1.0 / 10**

---

### 5. UI/UX Requirements

✓ Visual appearance described (blue highlight for selected items, 'x' deselect option, disabled state for Apply Filters button, section-wise layout with labels)
✓ Layout/positioning specified (aside panel structure, "Column Filters" header, parameters grouped under corresponding section headers, alphabetical ordering within sections)
✗ Responsiveness addressed (no mention of behavior on different screen sizes or breakpoints)
✓ Design guidelines referenced (Figma prototype link present in description)
✗ Browser/device support specified (not mentioned)
✗ Backward compatibility addressed (grid width adjustment is a layout behavior, not a backward-compat requirement)
✗ Platform requirements stated (US/UK/CA refers to market scope, not platform or OS)
✗ Localization covered (multi-market scope noted but no localization detail: currency, date formats, language, etc.)

**Score: 4.0 / 10**

---

### 6. API Requirements

✗ Clear definition of endpoints
✗ HTTP methods specified (GET, POST, PUT, DELETE)
✗ Clear response format
✗ Clear request parameters
✗ Clear body format
✗ Status codes and error messages specified

**Score: 1.0 / 10**

---

### 7. DB Requirements

✗ Data that needs to be stored is identified (column filter selections are session-state per AC005; no explicit DB storage requirement)
✗ Tables/collections specified
✗ Data type or format checks defined
✗ Constraints defined (NOT NULL, UNIQUE, etc.)
✗ Relationships defined (foreign keys, one-to-many, etc.)

**Score: 1.0 / 10**

---

## Improvement Recommendations

### 1. Core Structure Improvements
- Add at least one negative/error AC: what happens when parameter data fails to load, or when the filter API returns an error? e.g., *"Given the Column Filter aside is open, when the parameter list API fails, then a friendly error message is shown and the aside remains open"*

### 2. Functional Requirements Improvements
- Clarify behavior when Save and Cancel actions are developed (AC004 flags them as "not developed yet" — add follow-up stories or defer AC004's save/cancel scope explicitly)
- Define whether column filter state persists in browser session storage or local storage

### 3. Validation Specifications Improvements
- Add test data examples: specify sample parameter names (e.g., "Rent", "Occupancy", "Unit Type") and expected grid column output
- Add boundary scenarios: what happens when 0 parameters exist in the aside? What is the max number of selectable parameters?
- Add measurable outcome: e.g., "aside should open within X milliseconds", or "grid should re-render within X seconds after Apply Filters"

### 4. Non-Functional Requirements Improvements
- Specify response time target for aside open/close and grid re-render after applying filters
- Define access control: is this feature available to all RM user roles, or specific sub-roles (e.g., admin vs. read-only)?
- Address scalability: behavior when a property has hundreds of floor plan parameters
- Specify logging: should filter apply/clear events be logged for usage analytics?

### 5. UI/UX Requirement Improvements
- Add responsiveness requirement: behavior on tablet, small screen, or narrow browser window
- Specify browser support: Chrome, Edge, Firefox minimum versions
- Address localization: for UK/Canadian sites, confirm whether parameter labels and UI text require translation or locale-specific formatting
- Clarify backward compatibility: does this aside replace or augment an existing filter mechanism?

### 6. API Requirement Improvements
- Define the API endpoint(s) for fetching available column filter parameters (e.g., `GET /api/floorplan/parameters?propertyId=X`)
- Define the API endpoint for applying/persisting filter state if server-side
- Specify response schema: parameter object structure, section grouping field, display name
- Document error response format (HTTP status codes + error body)

### 7. DB Requirement Improvements
- Clarify whether column filter selections are persisted server-side (DB) or client-side (session/local storage)
- If server-side: identify the table/entity, user-filter association, and TTL or reset conditions
- If client-side: document storage key names and data structure

---

## Document Information

- **Version:** 1.0
- **Work Item State:** Closed
- **Project:** AOS — Revenue Management Program > RM-Shalom
- **Iteration:** AOS\\PI 23.Q4\\Sprint 23.26
- **Generated By:** Manual User Story Evaluation
- **Date:** 2026-04-16
