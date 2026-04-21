# User Story Evaluation

**Work Item:** [#2688690](https://tfs.realpage.com/tfs/Realpage/Consumer%20Solutions/_workitems/edit/2688690)
**Date:** 2026-04-16

---

## User Story Content

**Title:** PME-488877 - LOFT Living: Unable to Make an Amenity Reservation Error - Request failed with status code 500

**Work Item Type:** Bug

**Description:**
PME-488877 Due Date: 3/19/2026
The client has been trying to create a reservation for the guest suite at Fernwood Manor, but when they do, they get the error 500.

Error: Request failed with status code 500

The same error is showing if a resident will submit a reservation, if a staff on behalf of a resident and for office use.

Before they contacted LOFT Support:
1. They made sure that they had accepted the cookies of the page
2. They have tried to clear all their cookies and cache. Then also remove all cookies associated with all websites.
3. They and other colleagues are getting the same error
4. At this time, it looks like only this building is having issues with the reservations

Property: Fernwood Manor Apartments
Site ID: 4565392
PMC: Devon Properties

**Acceptance Criteria:**
Clients should be able to book an amenity without any error.

---

## Weight Percentage Matrix

**Selected Framework Row:** Row 1
**Excluded Categories:** None

| Core Structure | Functional Req. | Validation Specs | Non-Functional | UI/UX | API | DB | Total % |
|----------------|-----------------|------------------|----------------|-------|-----|----|---------|
| 30%            | 15%             | 15%              | 10%            | 10%   | 10% | 10%| 100%    |

---

## Evaluation Matrix

| Category                    | Weight | Score (1–10) | Weighted Score | Comments                                                                                          |
|-----------------------------|--------|--------------|----------------|---------------------------------------------------------------------------------------------------|
| Core Structure              | 30%    | 5.0          | 1.5            | Title and description are clear; user role/goal implied; missing user story format, explicit value statement, specific/testable ACs, and negative cases |
| Functional Requirements     | 15%    | 3.0          | 0.5            | Error scenario and 3 affected user types identified; no expected success state, step-by-step journey, integration context, or alternative paths |
| Validation Specifications   | 15%    | 2.0          | 0.3            | Independently testable (property/site ID known); no test credentials, step-by-step scenarios, or measurable success criteria |
| Non-Functional Requirements | 10%    | 1.0          | 0.1            | None specified; no response time, access control, data protection, or logging requirements |
| UI/UX Requirements          | 10%    | 1.0          | 0.1            | External screenshot link in description but no UI/UX specifications defined within the work item |
| API Requirements            | 10%    | 1.0          | 0.1            | HTTP 500 symptom noted but no endpoint, method, request/response schema, or error contract defined |
| DB Requirements             | 10%    | 1.0          | 0.1            | No data storage, tables, constraints, or relationships defined                                    |
| **TOTAL**                   | **100%**| **2.0**     | **2.7**        | **Poor — Missing critical information**                                                           |

---

## Detailed Evaluation

### 1. Core Structure

✗ Uses "As a [user], I want..., So that..." format (Bug report format used, not user story format)
✓ Identifies user role (client/resident, staff, office staff mentioned)
✓ Specifies user goal (book an amenity / guest suite reservation)
✗ States user value (no explicit statement of business or user value)
✓ Title is clear (includes PME ID, property context, and error type)
✓ Description provides context (property name, site ID, PMC, reproduction context, troubleshooting steps already taken)
✗ Acceptance Criteria: specific & testable (single vague line — "book without any error" — no steps, scenarios, or scope)
✓ Acceptance Criteria: clear language (simple and unambiguous)
✗ Acceptance Criteria: includes positive AND negative cases (only one positive outcome; no edge cases, partial booking, or error recovery scenarios)

**Score: 5.0 / 10**

---

### 2. Functional Requirements

✓ Feature behavior defined (amenity booking returns HTTP 500 for all user types at this property)
✓ All user interactions listed (resident self-service, staff on behalf of resident, office use — 3 paths all broken)
✗ Expected outcomes clear (AC only states "no error"; no specific expected state — booking confirmation, record, notification)
✗ Step-by-step user journey present (no navigation path or step sequence for the amenity booking flow)
✗ Integration with workflow described (no mention of calendar availability, payment, email notifications, or admin approval)
✗ Entry/exit points defined (no entry point into the reservation flow; no exit state on success or failure)
✗ All possible user paths covered (only the error path; no success path, cancellation path, or waitlist scenario)

**Score: 3.0 / 10**

---

### 3. Validation Specifications

✗ Test data requirements specified (Site ID 4565392 and property name provided but no test user credentials, reservation type, date/time, or amenity name)
✗ Sample scenarios provided (no step-by-step test scenarios, e.g., "Log in as resident → Navigate to Amenities → Select Guest Suite → Submit → Expect 500")
✓ Story is independently testable (known property and site ID make the issue reproducible)
✗ Success/failure criteria defined (vague acceptance criterion — no specific success state defined, e.g., booking confirmation screen, record in calendar)
✗ Measurable outcomes present (no performance targets, no booking record assertion, no notification verification)

**Score: 2.0 / 10**

---

### 4. Non-Functional Requirements

✗ Response time specified
✗ Throughput specified
✗ Resource utilization specified
✗ Scalability addressed (scope limited to one property; no mention of impact assessment)
✗ Access control defined (RM/staff role mentioned descriptively but no permission or role-based access detail)
✗ Data protection addressed
✗ Compliance requirements stated
✗ Logging/auditing covered (no mention of error logging, monitoring, or alerting requirements)

**Score: 1.0 / 10**

---

### 5. UI/UX Requirements

✗ Visual appearance described (Salesforce screenshot link referenced in description, but no UI behavior documented in the work item)
✗ Layout/positioning specified
✗ Responsiveness addressed
✗ Design guidelines referenced (no Figma, mockup, or design spec link)
✗ Browser/device support specified (client troubleshooting mentions cookies/cache but no browser specifics)
✗ Backward compatibility addressed
✗ Platform requirements stated
✗ Localization covered

**Score: 1.0 / 10**

---

### 6. API Requirements

✗ Clear definition of endpoints (no API endpoint identified for amenity reservation)
✗ HTTP methods specified (GET, POST, PUT, DELETE)
✗ Clear response format (HTTP 500 error is a symptom reported by the client, not an API specification)
✗ Clear request parameters
✗ Clear body format
✗ Status codes and error messages specified (error "500" mentioned descriptively only, not as an API contract item)

**Score: 1.0 / 10**

---

### 7. DB Requirements

✗ Data that needs to be stored is identified (no mention of what reservation data must be persisted or updated)
✗ Tables/collections specified
✗ Data type or format checks defined
✗ Constraints defined (NOT NULL, UNIQUE, etc.)
✗ Relationships defined (foreign keys, one-to-many, etc.)

**Score: 1.0 / 10**

---

## Improvement Recommendations

### 1. Core Structure Improvements
- Reframe as a user story or at minimum add a "So that..." clause to the AC: e.g., *"Clients should be able to book an amenity without any error so that they can reserve shared spaces as expected"*
- Add at least one negative AC: *"Given the amenity is fully booked, when a resident attempts to reserve it, then an appropriate availability message is shown — not an unhandled 500 error"*
- Make the AC specific and testable: include the reservation type (Guest Suite), user type(s), and expected confirmation behavior

### 2. Functional Requirements Improvements
- Define the expected success outcome: what does a successful booking look like? (confirmation screen, email, record in calendar, admin notification)
- Document the step-by-step booking flow: Navigate to Amenities → Select amenity → Choose date/time → Submit → Receive confirmation
- Describe the integration points: Is there a calendar API? A payment gateway? An admin approval step?
- Cover alternative paths: What if the date is unavailable? What if the resident is not eligible?

### 3. Validation Specifications Improvements
- Provide test credentials: a test resident account and staff account for Site ID 4565392 (Fernwood Manor Apartments)
- Add structured test scenarios:
  - Scenario 1: Resident self-service booking → Expected: booking confirmation
  - Scenario 2: Staff booking on behalf of resident → Expected: booking confirmation
  - Scenario 3: Office use booking → Expected: booking confirmation
- Define measurable success: e.g., booking record appears in the amenity calendar within 5 seconds of submission; confirmation email sent within 1 minute

### 4. Non-Functional Requirements Improvements
- Specify error recovery: if the reservation API fails, the client should see a user-friendly error message, not a raw 500
- Define logging requirement: the 500 error event should be logged with request payload, timestamp, site ID, and user role for debugging
- Add access control detail: confirm which roles (resident, staff, admin) can book which amenity types
- Address impact scope: confirm whether the issue is isolated to this property or a potential latent bug across all sites

### 5. UI/UX Requirement Improvements
- Embed or describe the error screenshot rather than linking to a Salesforce case URL (external link may expire or require login)
- Specify the expected UI on booking success: confirmation modal, page redirect, or inline message
- Specify the expected UI on booking failure: user-friendly error message instead of a raw HTTP 500 display
- Confirm browser support requirements: client used cookies/cache troubleshooting — specify supported browsers/versions

### 6. API Requirement Improvements
- Identify the amenity reservation API endpoint (e.g., `POST /api/amenities/reservations`) and HTTP method
- Document the request payload: reservation date/time, amenity ID, user ID, booking type
- Document the expected response schema on success (201 Created with booking ID) and expected error format (400/500 with error code and message)
- Investigate and document the root-cause 500 response: log the actual error from the server-side to determine if it is a data issue, missing config, or service dependency failure

### 7. DB Requirement Improvements
- Identify the reservation entity/table that the POST call writes to and confirm it exists and is accessible for Site ID 4565392
- Check for missing FK constraints or null references (e.g., amenity ID or property config not found for this site) that may be triggering the 500
- Confirm whether Devon Properties / Fernwood Manor has the amenity feature properly configured in the database (amenity record, availability schedule, booking rules)

---

## Document Information

- **Version:** 1.0
- **Work Item State:** Closed
- **Work Item Type:** Bug
- **Project:** Consumer%20Solutions — Resident Portals Program > ActiveBuilding > Pod E
- **Iteration:** Consumer%20Solutions\PI 26.Q2\Sprint 26.07
- **Generated By:** Manual User Story Evaluation
- **Date:** 2026-04-16
