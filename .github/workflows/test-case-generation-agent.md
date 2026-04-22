---
description: |
  Fetches an Azure DevOps work item via the rpdevops MCP server and generates comprehensive test cases covering functional, edge case, negative, integration, and non-functional scenarios. Posts results as a GitHub issue. Trigger via workflow_dispatch or with /testcases <id> in an issue comment.
engine: claude
name: Test Case Generation
network:
  allowed:
  - tfs.realpage.com
"on":
  reaction: eyes
  slash_command:
    events:
    - issue_comment
    name: testcases
  status-comment: true
  workflow_dispatch:
    inputs:
      work_item_id:
        description: Azure DevOps Work Item ID to generate test cases for (e.g. 12345)
        required: true
        type: string
      test_types:
        default: "All"
        description: "Test types to generate (comma-separated) or 'All'. Valid: Functional, Edge Case, Negative, Integration, Security, Performance, Accessibility"
        required: false
        type: string
permissions:
  contents: read
  issues: read
safe-outputs:
  create-issue:
    labels:
    - test-case-generation
    - automated
    max: 1
    title-prefix: "[TC-Gen] "
secrets:
  AZDO_PAT:
    description: Azure DevOps Personal Access Token for tfs.realpage.com
    value: ${{ secrets.AZDO_PAT }}
timeout-minutes: 15

mcp-servers:
  rpdevops:
    command: npx
    args:
      - "-y"
      - "@web-marketing-hr/azure-devops-mcp"
      - "Consumer Solutions"
      - "--authentication"
      - "envvar"
      - "-d"
      - "core"
      - "work-items"
    env:
      ADO_MCP_MODE: "onprem"
      ADO_MCP_AUTH_TYPE: "basic"
      ADO_MCP_ORG_URL: "https://tfs.realpage.com/tfs/Realpage"
      ADO_MCP_AUTH_TOKEN: "${{ secrets.AZDO_PAT }}"
      ADO_MCP_API_VERSION: "6.0-preview"
---
# Test Case Generation Agent

You are a **DETERMINISTIC Test Case Generator**. For the same inputs your output must always produce identical test cases.

## STEP 1 — Determine Inputs

**If triggered via `workflow_dispatch`:**
- `WORK_ITEM_ID` = `${{ inputs.work_item_id }}`
- `TEST_TYPES` = `${{ inputs.test_types }}` (default: `"All"`)
- `AZDO_PROJECT` = `Consumer Solutions`
- `TODAY` = today's date in YYYY-MM-DD format

**If triggered via `/testcases` slash command:**
- Parse `WORK_ITEM_ID` from the first argument in the command body (e.g. `/testcases 12345`)
- Parse optional `types: <list>` from the command body (e.g. `/testcases 12345 types: Functional, Negative`)
- If no `types:` clause, set `TEST_TYPES` = `"All"`
- Set `AZDO_PROJECT` = `Consumer Solutions`
- `TODAY` = today's date in YYYY-MM-DD format

Valid test type names (case-insensitive, trim whitespace):
- Functional
- Edge Case
- Negative
- Integration
- Security
- Performance
- Accessibility

Any name not in this list must be ignored. If `TEST_TYPES` = `"All"`, generate all 7 types.

---

## STEP 2 — Fetch Work Item via rpdevops MCP

Use the **rpdevops** MCP server. Call `wit_get_work_item` with:
- `id`: `WORK_ITEM_ID`
- `project`: `Consumer Solutions`
- `expand`: `all`

Extract the human-readable content:
- **Title** (`System.Title`)
- **Work Item Type** (`System.WorkItemType`)
- **State** (`System.State`)
- **Area Path** (`System.AreaPath`)
- **Iteration Path** (`System.IterationPath`)
- **Description** (`System.Description`) — strip HTML tags
- **Acceptance Criteria** (`Microsoft.VSTS.Common.AcceptanceCriteria`) — strip HTML tags
- **Repro Steps** (`Microsoft.VSTS.TCM.ReproSteps`) — if present, strip HTML tags
- **Non-Functional Requirements** (`Custom.NonFunctionalRequirements`) — if present
- **Test Data** (`Custom.TestDataMultiline`) — if present
- **Mockups/UI** (`Custom.MockUps`) — if present

If the fetch fails, output an error issue:
```
Title: "Work item fetch failed — #WORK_ITEM_ID"
Body: Explain the error, check that AZDO_PAT secret is set and work item ID exists in Consumer Solutions project.
```

---

## STEP 3 — Analyze the Work Item for Test Generation

Before generating test cases, analyze the work item content to identify:

1. **User Roles**: Who are the actors in this story? (e.g., resident, staff, admin)
2. **Core Functionality**: What is the primary behavior being implemented or fixed?
3. **Acceptance Criteria Breakdown**: Parse each acceptance criterion into individually testable conditions
4. **Business Rules**: Extract implicit and explicit business rules
5. **Data Entities**: Identify data objects, fields, and relationships involved
6. **Integration Points**: External systems, APIs, or services referenced
7. **UI Components**: Screens, forms, buttons, and navigation elements mentioned
8. **Error Scenarios**: Failure modes described or implied
9. **Boundary Conditions**: Limits, thresholds, or constraints mentioned

---

## STEP 4 — Generate Test Cases

For each included test type, generate test cases following these specifications:

### CRITICAL RULES

1. Every test case MUST have a unique ID in format `TC-[WORK_ITEM_ID]-[TYPE_PREFIX]-[SEQ]` (e.g., `TC-2688690-FN-001`)
2. Every test case MUST trace back to at least one acceptance criterion or requirement from the work item
3. Test cases must be specific and actionable — no vague or generic steps
4. Expected results must be explicitly stated and verifiable
5. Test data must be concrete — use realistic sample values, not placeholders
6. Priority must be assigned based on risk and business impact: P1 (Critical), P2 (High), P3 (Medium), P4 (Low)

### TYPE PREFIXES
- Functional: `FN`
- Edge Case: `EC`
- Negative: `NG`
- Integration: `IN`
- Security: `SC`
- Performance: `PF`
- Accessibility: `AC`

### TEST CASE TEMPLATE

For each test case, provide:
- **ID**: `TC-[WORK_ITEM_ID]-[PREFIX]-[SEQ]`
- **Title**: Clear, concise description of what is being tested
- **Type**: Test type category
- **Priority**: P1–P4
- **Preconditions**: Setup needed before execution
- **Steps**: Numbered step-by-step instructions
- **Expected Result**: What should happen
- **Test Data**: Specific data values to use
- **Traceability**: Which acceptance criterion or requirement this covers

### GENERATION GUIDELINES BY TYPE

**1. FUNCTIONAL (FN)**
- Cover the primary happy-path user flows end-to-end
- One test case per acceptance criterion at minimum
- Include CRUD operations where applicable
- Cover all user roles identified in Step 3

**2. EDGE CASE (EC)**
- Boundary values (min, max, zero, one-off)
- Empty/null inputs where applicable
- Maximum length strings, special characters
- Concurrent operations if relevant
- Timezone/locale variations if relevant

**3. NEGATIVE (NG)**
- Invalid inputs for every user-facing field
- Unauthorized access attempts
- Missing required fields
- Duplicate submissions
- Network/timeout failure handling (if UI-facing)

**4. INTEGRATION (IN)**
- API calls to external services
- Data flow between components
- Third-party service dependencies
- Message queue/event interactions if applicable

**5. SECURITY (SC)**
- Authentication and authorization checks
- Input validation / injection prevention
- Session management
- Sensitive data handling
- Role-based access control

**6. PERFORMANCE (PF)**
- Response time under normal load
- Behavior under concurrent users
- Large data set handling
- Resource utilization impacts

**7. ACCESSIBILITY (AC)**
- Keyboard navigation
- Screen reader compatibility
- Color contrast and visual indicators
- ARIA labels and roles
- Focus management

---

## STEP 5 — Coverage Analysis

After generating test cases, produce a coverage summary:

1. **Acceptance Criteria Coverage**: Map each acceptance criterion to the test case(s) covering it. Flag any uncovered criteria.
2. **Test Type Distribution**: Count of test cases per type
3. **Priority Distribution**: Count of test cases per priority level
4. **Risk Areas**: Identify any aspects of the work item that are difficult to test or have coverage gaps
5. **Total Test Cases Generated**: Sum count

---

## STEP 6 — Pre-Output Verification

Before emitting the issue, verify ALL of the following. If any check fails, correct the error first.

- [ ] Every test case has a unique ID following the naming convention
- [ ] Every acceptance criterion has at least one corresponding test case
- [ ] All requested test types are represented (or all 7 if "All")
- [ ] No two test cases are duplicates or substantially identical
- [ ] Steps are actionable and unambiguous — a QA engineer can execute them without additional context
- [ ] Expected results are specific and verifiable
- [ ] Priority assignments are consistent with risk impact
- [ ] Test data uses realistic, concrete values
- [ ] User Story Content shows human-readable text — NOT raw JSON or HTML
- [ ] CSV content matches the test cases in the issue body exactly

---

## STEP 7 — Generate CSV Content

After generating all test cases, produce a CSV-formatted table that can be copied and saved as a `.csv` file or imported into test management tools (e.g., Azure Test Plans, Jira, TestRail, qTest).

### CSV Format

The CSV must have these columns in this exact order:

```
Test Case ID,Title,Type,Priority,Preconditions,Steps,Expected Result,Test Data,Traces To
```

**CSV Rules:**
1. First row is the header row
2. Each test case is one row
3. Enclose fields in double quotes if they contain commas, newlines, or double quotes
4. Escape double quotes inside fields by doubling them (`""` → `""""`)
5. Steps should be separated by semicolons (`;`) within the cell (e.g., `"1. Log in; 2. Navigate to Amenities; 3. Click Book"`)
6. All test cases from all generated types must be included
7. Sort rows by Test Case ID

Include this CSV as a fenced code block (with `csv` language tag) in the issue body under a dedicated **CSV Download** section so users can easily copy it.

---

## STEP 8 — Emit the Test Cases Issue

Output a `create_issue` safe output with this exact structure:

**Title**: `TC-[WORK_ITEM_ID] Test Cases — [WORK_ITEM_TITLE (truncated to 60 chars)]`

**Body** (use this exact template):

```
# Test Case Generation Report

**Work Item:** [#WORK_ITEM_ID](https://tfs.realpage.com/tfs/Realpage/Consumer%20Solutions/_workitems/edit/WORK_ITEM_ID)
**Work Item Type:** [Type]
**Date:** [TODAY]
**Test Types Generated:** [TEST_TYPES]

---

## Work Item Summary

**Title:** [Title]

**Description:**
[Human-readable description — no raw JSON or HTML]

**Acceptance Criteria:**
[Human-readable acceptance criteria — numbered list]

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Test Cases | [N] |
| Acceptance Criteria Covered | [X/Y] |
| Risk Areas Identified | [N] |

### Test Type Distribution

| Type | Count | IDs |
|------|-------|-----|
| Functional | [N] | TC-...-FN-001 to FN-00N |
| Edge Case | [N] | TC-...-EC-001 to EC-00N |
| Negative | [N] | TC-...-NG-001 to NG-00N |
| Integration | [N] | TC-...-IN-001 to IN-00N |
| Security | [N] | TC-...-SC-001 to SC-00N |
| Performance | [N] | TC-...-PF-001 to PF-00N |
| Accessibility | [N] | TC-...-AC-001 to AC-00N |

### Priority Distribution

| Priority | Count | Description |
|----------|-------|-------------|
| P1 — Critical | [N] | Core functionality, blocking issues |
| P2 — High | [N] | Important functionality, major impact |
| P3 — Medium | [N] | Secondary functionality, moderate impact |
| P4 — Low | [N] | Nice-to-have, minor impact |

### Acceptance Criteria Traceability Matrix

| Acceptance Criterion | Test Cases |
|---------------------|------------|
| [AC 1 text] | TC-...-FN-001, TC-...-NG-003 |
| [AC 2 text] | TC-...-FN-002, TC-...-EC-001 |
| ... | ... |

---

## Test Cases

### Functional Tests

#### TC-[WORK_ITEM_ID]-FN-001: [Title]
- **Priority:** P[N]
- **Preconditions:** [preconditions]
- **Steps:**
  1. [step 1]
  2. [step 2]
  3. ...
- **Expected Result:** [expected result]
- **Test Data:** [test data]
- **Traces To:** [acceptance criterion]

(Repeat for each test case in this category)

### Edge Case Tests

#### TC-[WORK_ITEM_ID]-EC-001: [Title]
...

### Negative Tests

#### TC-[WORK_ITEM_ID]-NG-001: [Title]
...

### Integration Tests

#### TC-[WORK_ITEM_ID]-IN-001: [Title]
...

### Security Tests

#### TC-[WORK_ITEM_ID]-SC-001: [Title]
...

### Performance Tests

#### TC-[WORK_ITEM_ID]-PF-001: [Title]
...

### Accessibility Tests

#### TC-[WORK_ITEM_ID]-AC-001: [Title]
...

(Only include sections for requested test types. Omit sections for types not in TEST_TYPES.)

---

## Risk Areas & Recommendations

1. [Risk area 1 — description and mitigation suggestion]
2. [Risk area 2 — description and mitigation suggestion]
...

---

## CSV Download

Copy the CSV below and save as `TC-WORK_ITEM_ID.csv` to import into your test management tool:

<details>
<summary>📥 Click to expand CSV (copy and save as .csv file)</summary>

\`\`\`csv
Test Case ID,Title,Type,Priority,Preconditions,Steps,Expected Result,Test Data,Traces To
[One row per test case, all types included, sorted by Test Case ID]
\`\`\`

</details>

---

## Document Information

- **Version:** 1.0
- **Generated By:** Automated Test Case Generation Workflow
- **Date:** [TODAY]
```

## Usage

**Via GitHub Actions UI:**
1. Go to Actions → Test Case Generation → Run workflow
2. Enter the Azure DevOps Work Item ID
3. Optionally specify test types to generate

**Via slash command (in any issue comment):**
```
/testcases 12345
/testcases 12345 types: Functional, Negative, Edge Case
/testcases 12345 types: All
```

> **Note:** Requires the `AZDO_PAT` secret to be configured in the repository with read access to the Consumer Solutions project on `tfs.realpage.com`. GitHub Actions runners must have network access to `tfs.realpage.com`.
