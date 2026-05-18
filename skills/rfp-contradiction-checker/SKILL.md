---
name: rfp-contradiction-checker
description: Scans a completed or draft RFP response for internal contradictions, inconsistencies between answers, and conflicts with the source content library or technical documentation. Use this skill whenever a user has a draft or completed RFP response and wants a quality check before submission. Also trigger on phrases like "check my RFP for contradictions", "find inconsistencies in my response", "QA my bid", "does my proposal contradict itself", "consistency check", "review my answers against our documentation", or "pre-submission review". This is a pre-submission quality gate and should be the last step before sending.
---

# RFP Contradiction Checker

Performs a systematic review of a completed RFP response to find internal contradictions between answers, inconsistencies with source documentation, and factual conflicts that could undermine credibility with evaluators.

## Works Well With

- **compliance-matrix-builder** - Build the matrix first so every requirement is catalogued; use this skill as the final quality gate
- **executive-summary-generator** - Run contradiction checking before writing the exec summary so it does not inherit inconsistencies from the body
- **conversational-intelligence-analyzer** - After incorporating conversation insights into your RFP, check the new content does not contradict existing answers

## Why This Matters

Nothing kills an RFP score faster than contradicting yourself. When one answer says "we support on-premise deployment" and another says "our solution is cloud-only", evaluators lose confidence in every answer. This is especially common when multiple SMEs contribute sections independently, when content is pulled from a library without checking context, or when responses are reused from previous bids without full adaptation.

Evaluators are trained to cross-reference answers. This skill does the same thing before they do.

## What the AutoRFP.ai MCP Server Can and Cannot See

This plugin ships with the AutoRFP.ai MCP server. Be explicit with the user about what is available:

**The MCP CAN access (read-only):**
- Projects and their requirements / answers (question-answer pairs)
- Tags and tag-based filtering of requirements and content
- The approved Content Library (semantic and keyword search)
- Project metadata (status, due date, tags)

**The MCP CANNOT access:**
- The original RFP document (PDF, DOCX, XLSX) as published by the prospect
- Files attached to a project that are not the structured Q&A
- Anything outside the user's AutoRFP.ai workspace

**If the user wants to check answers against the original RFP narrative, evaluation criteria, or specific clauses, ask them to upload the original document.** The MCP can pull the structured requirements that have been imported into a project, but it cannot read the source PDF/DOCX/XLSX itself.

## Input Requirements

### Required: The RFP Response
The completed or near-complete RFP response to check. Accepted sources:
- An AutoRFP.ai project pulled via the MCP (Q&A pairs)
- `.docx` - Word document with questions and answers
- `.xlsx` / `.csv` - Spreadsheet with question-answer pairs (common for compliance questionnaires)
- `.pdf` - PDF export of the response
- Copy-pasted text of specific sections

### Optional but Recommended: Source Content
One or more sources of truth to check the RFP response against:
- **AutoRFP.ai Content Library** - Via the MCP, the approved response content
- **Technical documentation** - Product docs, architecture docs, API docs (ask user to upload)
- **Company website** - URL to check claims against published information
- **Previous RFP responses** - To check for inconsistencies across bids (ask user to upload if not in AutoRFP.ai)
- **Capabilities document** - A reference file describing what you can and cannot do

The more source material provided, the more thorough the contradiction check.

## Workflow

### Step 1: Ingest the RFP Response

If pulling from AutoRFP.ai: ask the user for the project name or ID, then use the MCP to list the requirements and answers in that project.

If a file is uploaded: read the full RFP response. Build an index of every question-answer pair, noting:
- Question number or identifier
- Section or category
- Core claims made in each answer
- Specific numbers, dates, timelines, or commitments stated

If the response is very large, work through it section by section, but always cross-reference across sections at the end.

### Step 2: Internal Contradiction Scan

Compare every answer against every other answer looking for:

**Direct contradictions:**
- Answer A says X, Answer B says not-X
- Example: Q12 says "implementation takes 6-8 weeks" but Q45 says "typical deployment is 4-6 months"

**Numerical inconsistencies:**
- Different numbers for the same metric in different answers
- Example: Q8 says "99.99% uptime SLA" but Q33 says "99.9% availability guarantee"

**Capability conflicts:**
- One answer claims a capability, another answer limits or denies it
- Example: Q15 says "full API access for all modules" but Q28 says "API access available for core modules only"

**Timeline mismatches:**
- Different answers give different timelines for the same activity
- Example: Q20 says "data migration typically takes 2 weeks" but Q35 says "migration is a 6-week workstream"

**Scope inconsistencies:**
- Answers that imply different scope of what is included vs excluded
- Example: Q10 says "training is included" but Q50 says "training packages are available as an add-on"

**Terminology drift:**
- The same thing described with different (potentially confusing) names
- Example: Sometimes called "Dashboard", sometimes "Analytics Console", sometimes "Reporting Hub". Evaluators may think these are different things.

**Tone/confidence inconsistencies:**
- One answer is definitive ("we do X") while another hedges on the same topic ("we can potentially support X")

### Step 3: Source Content Comparison (if provided)

If the user provided source documentation, compare every claim in the RFP response against the source material:

**Factual accuracy:**
- Do stated capabilities match the technical documentation?
- Do quoted statistics match published data?
- Do described processes match documented workflows?

**Overpromises:**
- Does the RFP response claim more than the source documentation supports?
- Are there commitments that go beyond standard offerings?

**Outdated information:**
- Does the response reference features, certifications, or capabilities that are no longer current?
- Are version numbers, dates, or statistics outdated?

**Missing caveats:**
- Does the source documentation include limitations or conditions that the RFP response omits?
- Example: Technical docs say "supports up to 10,000 concurrent users" but the RFP answer just says "highly scalable"

### Step 4: Generate the Contradiction Report

Present findings organised by severity:

```
## RFP Contradiction Report

### Summary
- Total answers reviewed: [X]
- Contradictions found: [X]
- Critical (must fix): [X]
- Moderate (should fix): [X]
- Minor (consider fixing): [X]

### Critical Contradictions
Issues that an evaluator would likely catch and that could result in disqualification or significant score reduction.

For each:
| # | Type | Answer A | Answer B | The Contradiction | Suggested Resolution |
With full quotes from both answers showing the conflict.

### Moderate Contradictions
Inconsistencies that undermine confidence but are unlikely to disqualify.

[Same format]

### Minor Inconsistencies
Terminology drift, tone mismatches, or minor numerical rounding differences.

[Same format]

### Source Content Conflicts (if applicable)
Claims in the RFP response that conflict with provided documentation.

For each:
| # | RFP Answer | Source Document | The Conflict | Suggested Resolution |

### Consistency Recommendations
General observations about patterns. For example: "Implementation timelines are described differently in 4 separate answers; standardise on a single range and reference it consistently."
```

### Step 5: Resolution Assistance

After presenting the report, offer to help resolve contradictions:
- For each critical contradiction, suggest which answer is likely correct (based on source docs if available) and provide corrected language
- For terminology drift, suggest a standardised glossary
- If patterns emerge (e.g., all security answers have inconsistencies), flag that a specific SME should review their entire section

## Output Format

- Quick check (fewer than 30 questions): results directly in conversation
- Full review: create as `.md` file
- If user requests DOCX or PDF: use the appropriate creation skill

## Important Principles

- Every contradiction flagged must include the exact text from both conflicting answers so the user can see the problem immediately. Do not summarise. Quote.
- Severity classification matters. Not every inconsistency is critical. An evaluator will not disqualify you for calling the same feature two different names, but they will disqualify you for contradicting a mandatory requirement.
- Suggested resolutions should favour accuracy over optimism. If two answers conflict and one is more conservative, the conservative answer is usually the correct one to keep.
- This is a quality gate, not a rewrite tool. Flag the problems clearly and help resolve them, but the SMEs who wrote the answers should confirm which version is correct.
- Be thorough. Check every answer against every other answer. The contradictions evaluators find are often between answers 50 pages apart.
