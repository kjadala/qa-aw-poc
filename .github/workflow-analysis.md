---
# Workflow Analysis Configuration
# Changes here are automatically picked up by workitem-analysis.yml at runtime.
# No need to edit the workflow YAML — just update this file.

name: TFS Work Item Analysis with Claude

model: claude-sonnet-4-20250514
max_tokens: 800
anthropic_version: "2023-06-01"

tfs:
  api_version: "6.0"
  fields:
    - System.Title
    - System.Description

html_cleanup:
  strip_tags: true
  decode_entities: true

---

# Analysis Prompt Template

Analyze this user story and provide:

## Story Points
- Estimate story points on a Fibonacci scale (1, 2, 3, 5, 8, 13)
- Provide rationale for the estimate

## Complexity
- Rate complexity as Low, Medium, Medium-High, or High
- List technical complexity factors

## Risks

### High Risk
- Items that could block or derail the story

### Medium Risk
- Items that need attention but are manageable

### Low Risk
- Minor concerns

## Suggestions

### Technical Recommendations
- Architecture, state management, performance optimizations

### UX Improvements
- User guidance, visual indicators, accessibility

### Implementation Strategy
- Recommended phased approach

### Definition of Done Additions
- Additional acceptance criteria to consider

### Questions for Clarification
- Open questions for the product owner or team
