# User Story Evaluation

**Work Item:** [#1727233](https://tfs.realpage.com/tfs/Realpage/AOS/_workitems/edit/1727233)
**Date:** 2026-04-22

---

## User Story Content

**Title:** Settings - Floor Plan - List View - Auto Pilot (2 of 2) - Columns Filter Data and Interaction of Colum filter With Horizontal filter

**Work Item Type:** User Story

**Description:**
As an RM user on Settings > New Floor Plan Parameters > List View > Column Filter, I want each section of the 'Column Filter' aside display the parameters that I have selected via the dropdown so that I may have visibility on my selection and a way to deselect using the 'x'Further more I want that the horizontal filter option and Column filter option be independent of each other and not work in conjunction (on top of) with each other for a smooth user experience.Note:This enhancement is for US, UK and Canadian sites and for all property typesAC001, 002, for Column Filter Functionality covered  on 1708534, this ticket to cover correct data display based on column filter selection and the Interaction of Colum filter With Horizontal filterhttps://www.figma.com/proto/hls5z78A4AL5MzKqd3IwbS/Setting-Updates?node-id=1009-169195&scaling=contain&page-id=0%3A1&starting-point-node-id=128%3A122251

**Acceptance Criteria:**
001 Given an RM user on Settings > Floor Plan Parameters > List View  When I click the 'Column Filters' button Then an aside opens up where  Header: Column Filters Parameter labels are displayed section-wise under each corresponding section (ex: General parameter selected are displayed under General parameters) Three button Clear Filters (only shows up when at lease one parameter is selected Close Apply Filters (is disabled when no parameter selections are made)    002  Given an RM user on Settings > Floor Plan Parameters > List View > Column Filters Aside When I select one or more parameters across same or different parameter sections Then my selected parameter labels are displayed on the aside Under each corresponding section (ex: General parameter selected are displayed under General parameters)  in alphabetical order in each separate section (post selection) In blue highlight with an 'x' option to cancel/remove the selection  And the 'Apply Filters' button is enabled    *** AC001, 002 for Column Filter Functionality covered on https://tfs.realpage.com/tfs/Realpage/AOS/_workitems/edit/1708534****  003a Given an RM user on Settings > Floor Plan Parameters > List View > Column Filters Aside And I select one or more parameters across same or different parameter sections When I click the 'Clear Filters' button  Then my selected clear out and uncheck And my aside remains open And no filters are set      003b Given an RM user on Settings > Floor Plan Parameters > List View > Column Filters Aside And I select one or more parameters across same or different parameter sections And my selected parameter labels are displayed on the aside with the look and feel of AC002 When I click the 'Apply Filters' button  Then my aside closes And the list view grid only reflects the parameters that I selected via the Column Filters aside And grid width adjusts based on the grid content       004  Given an RM User on Settings > Floor Plan Parameters > List View And I have some column filters selected When I  make changes (add, remove) to my property selections on the Property dropdown and FP dropdown (not thru property picker) Or  Save changes (not developed yet)  Or Cancel (not developed yet)    Then my column filter selections are retained And my grid displays the correct data corresponding to the chosen filters And grid width adjusts based on the grid content   005 Given an RM user on Floor Plan Parameter >List View And I have applied one or more column filters    When I move to a different Settings tab, a different workflow, hit the back browser or refresh my page And I return to Floor Plan Parameter >List View  Then my page resets to default view (no filters selected, 'All' defaults)           006 User can have either horizontal filters or column Filters but not both Given an RM user on  Floor Plan Parameter >List View When I have applied one or more horizontal filter options And then apply one or more column filters Then the horizontal filters are cleared (no buttons are lit up or checked, all buttons are grey, grid does not reflect selection made previously on the horizontal filters) And only my column filters remain active (selections are present on the list view grid, main Column Filter button is lit up and the number of parameters are listed, selections are highlighted in the aside) And grid width adjusts based on the grid content   007 User can have either horizontal filters or column Filters but not both  Given an RM user on  Floor Plan Parameter >List View When I have applied one or more column filter options And then apply one or more horizontal filters Then the column filters are cleared (no selections are present on the grid or highlighted in the aside; main column filter button is NOT lit up and the number of parameters are NOT listed) And only my horizontal filters remain active (lit up, check marked, grid reflects the horizontal filter selections) And grid width adjusts based on the grid content

---

## Weight Percentage Matrix

**Selected Framework Row:** Row 1
**Excluded Categories:** None

| Core Structure | Functional Requirements | Validation Specifications | Non-Functional Requirements | UI/UX Requirements | API Requirements | DB Requirements | Total % |
|----------------|------------------------|---------------------------|----------------------------|-------------------|------------------|-----------------|---------|
| 30%            | 15%                    | 15%                       | 10%                        | 10%              | 10%              | 10%             | 100%    |

---

## Evaluation Matrix

| Category | Weight | Score (1–10) | Weighted Score | Comments |
|----------|--------|--------------|----------------|----------|
| Core Structure | 30% | 8.0 | 2.4 | Good structure with comprehensive acceptance criteria |
| Functional Requirements | 15% | 9.0 | 1.4 | Very detailed functional specifications |
| Validation Specifications | 15% | 7.0 | 1.1 | Good test scenarios but missing specific data requirements |
| Non-Functional Requirements | 10% | 3.0 | 0.3 | Limited performance and security specifications |
| UI/UX Requirements | 10% | 8.0 | 0.8 | Good visual and interaction details |
| API Requirements | 10% | 2.0 | 0.2 | No API specifications provided |
| DB Requirements | 10% | 2.0 | 0.2 | No database requirements specified |
| **TOTAL** | **100%** | **5.6** | **6.4** | **Good — Mostly complete with minor gaps** |

---

## Detailed Evaluation

### 1. Core Structure

✓ Uses "As a [user], I want..., So that..." format (proper user story structure present)
✓ Identifies user role (RM user clearly specified)
✓ Specifies user goal (filter visibility and interaction behavior defined)
✓ States user value (smooth user experience and visibility on selections)
✓ Title is clear (descriptive of the feature being developed)
✓ Description provides context (includes background and references to related work)
✓ Acceptance Criteria: specific & testable (detailed Given-When-Then scenarios)
✓ Acceptance Criteria: clear language (well-structured and understandable)
✗ Acceptance Criteria: includes positive & negative cases (mainly positive scenarios, limited negative cases)

**Score: 8.0 / 10**

### 2. Functional Requirements

✓ Feature behavior defined (column filter and horizontal filter interactions detailed)
✓ All user interactions listed (click, select, apply, clear actions specified)
✓ Expected outcomes clear (specific results for each action described)
✓ Step-by-step user journey present (detailed workflows in acceptance criteria)
✓ Integration with workflow described (interaction between different filter types)
✓ Entry/exit points defined (navigation paths and state changes specified)
✓ All possible user paths covered (multiple scenarios including state retention and clearing)

**Score: 9.0 / 10**

### 3. Validation Specifications

✓ Sample scenarios provided (multiple acceptance criteria with specific scenarios)
✓ Story is independently testable (clear test cases in AC format)
✓ Success/failure criteria defined (specific expected outcomes for each scenario)
✓ Measurable outcomes present (UI state changes and grid behavior specified)
✗ Test data requirements specified (no specific test data mentioned)

**Score: 7.0 / 10**

### 4. Non-Functional Requirements

✗ Response time specified (no performance metrics provided)
✗ Throughput specified (no throughput requirements mentioned)
✗ Resource utilization specified (no resource constraints defined)
✗ Scalability addressed (no scalability considerations mentioned)
✗ Access control defined (no security requirements specified)
✗ Data protection addressed (no data protection requirements)
✗ Compliance requirements stated (no compliance requirements mentioned)
✗ Logging/auditing covered (no audit trail requirements specified)

**Score: 3.0 / 10**

### 5. UI/UX Requirements

✓ Visual appearance described (blue highlight, button states, grid width adjustments)
✓ Layout/positioning specified (aside panel, sections, alphabetical ordering)
✓ Design guidelines referenced (Figma prototype link provided)
✗ Responsiveness addressed (no responsive design requirements specified)
✗ Browser/device support specified (no browser compatibility mentioned)
✗ Backward compatibility addressed (no compatibility requirements mentioned)
✗ Platform requirements stated (no platform-specific requirements)
✗ Localization covered (mentions US, UK, Canadian sites but no localization details)

**Score: 8.0 / 10**

### 6. API Requirements

✗ Clear definition of endpoints (no API endpoints specified)
✗ HTTP methods specified (no HTTP methods mentioned)
✗ Clear response format (no API response formats defined)
✗ Clear request parameters (no API parameters specified)
✗ Clear body format (no request body formats defined)
✗ Status codes and error messages specified (no API error handling mentioned)

**Score: 2.0 / 10**

### 7. DB Requirements

✗ Data that needs to be stored is identified (no data storage requirements specified)
✗ Tables/collections specified (no database schema mentioned)
✗ Data type or format checks defined (no data validation rules specified)
✗ Constraints defined (no database constraints mentioned)
✗ Relationships defined (no entity relationships specified)

**Score: 2.0 / 10**

---

## Improvement Recommendations

### 1. Core Structure Improvements
- Add more negative test scenarios in acceptance criteria to cover edge cases and error conditions

### 2. Functional Requirements Improvements
- Consider adding error handling scenarios for when filters fail to apply or clear

### 3. Validation Specifications Improvements
- Specify test data requirements including sample parameter values and property configurations
- Define data sets needed for testing different filter combinations

### 4. Non-Functional Requirements Improvements
- Add response time requirements for filter operations
- Specify performance requirements for large data sets
- Define access control requirements for different user roles
- Add logging requirements for user actions and filter changes

### 5. UI/UX Requirements Improvements
- Specify responsive design requirements for different screen sizes
- Add browser compatibility requirements
- Define localization requirements beyond geographic scope

### 6. API Requirements Improvements
- Define API endpoints for filter operations
- Specify request/response formats for filter data
- Add error handling and status codes for API operations
- Document authentication requirements

### 7. DB Requirements Improvements
- Identify data storage requirements for filter configurations
- Specify database schema for storing user filter preferences
- Define data relationships between filters and other entities
- Add data validation and constraint requirements

---

## Document Information

- **Version:** 1.0
- **Work Item State:** Closed
- **Work Item Type:** User Story
- **Project:** AOS\Revenue Management Program\RM-Shalom
- **Iteration:** AOS\PI 23.Q4\Sprint 23.26
- **Generated By:** Automated User Story Evaluation Workflow
- **Date:** 2026-04-22
