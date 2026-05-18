---
name: rfp-shredder
description: Analyzes RFP, tender, and bid documents to produce a structured Go/No-Go qualification assessment. Use this skill whenever a user uploads an RFP document (PDF, XLSX, DOCX, CSV) and asks for analysis, shredding, qualification, or a Go/No-Go decision. Also trigger when users want mandatory requirements extracted, capability mapping against an RFP, or a structured bid/no-bid recommendation. Even if the user just says "look at this RFP" or "should we bid on this", use this skill.
---

# RFP Shredder & Go/No-Go Qualification

Analyzes uploaded RFP documents, extracts mandatory requirements, maps them against company capabilities, answers standard qualification questions, and produces a scored Go/No-Go recommendation.

## Reference Files

Before starting any analysis, read both reference files:

- `references/questions.md` - Scored Go/No-Go qualification questions grouped by category with weights. Users customize this to match their qualification criteria.
- `references/capabilities.md` - Company capabilities, certifications, constraints, and known limitations. Requirements are mapped against this file.

**If `capabilities.md` is still the empty template that ships with this plugin, stop and tell the user to fill it in (or paste their company capabilities into the chat) before running the analysis. Without capabilities the skill cannot map requirements and cannot produce a meaningful Go/No-Go score.**

## What the AutoRFP.ai MCP Server Can and Cannot See

This plugin ships with the AutoRFP.ai MCP server. The MCP server is read-only and can pull:
- Projects and requirements (if the RFP has already been imported into AutoRFP.ai as a project)
- Tags
- The approved Content Library (for capability coverage estimates)

**The MCP cannot read the original RFP document (PDF, DOCX, XLSX) as published by the prospect.** Mandatory requirement extraction, evaluation criteria, weightings, submission instructions and deadlines all live in the original document, not the structured Q&A.

**Always ask the user to upload the original RFP document before running this skill.** If they tell you "it's in AutoRFP.ai project X", the MCP can pull requirements but will miss the narrative sections (scope of work, evaluation methodology, contract terms, submission instructions). For a real Go/No-Go assessment you need the source document.

## Supported Input Formats

- `.pdf` - Extract text, tables, and structure
- `.xlsx` / `.csv` - Parse sheets, paying attention to requirement tables, compliance matrices, and evaluation criteria tabs
- `.docx` - Extract text content and table structures

If the document is very large, prioritize extracting: scope of work, mandatory requirements, technical requirements, commercial expectations, evaluation criteria and weightings, timeline and key dates, legal/security/compliance requirements, and submission deadlines.

## Workflow

### Step 0: Confirm Source Material

Ask the user to upload the original RFP document if they have not already. If they only have an AutoRFP.ai project ID, explain that the MCP can pull structured requirements but cannot read the source document, and request the original PDF/DOCX/XLSX. Optionally pull existing AutoRFP.ai project data via the MCP to cross-reference.

### Step 1: Ingest and Summarize

Accept the uploaded document and produce a brief RFP overview covering: issuing organization, opportunity name, submission deadline, estimated contract value, contract duration, sector, and any stated evaluation methodology.

### Step 2: Extract Mandatory Requirements

Scan the full document for mandatory requirements. Look for:

- Language signals: "must", "shall", "mandatory", "required", "minimum", "essential", "pass/fail"
- Formatting signals: rows or sections explicitly labeled mandatory vs desirable/optional
- Compliance tables: columns asking for "Compliant / Non-Compliant / Partial"
- Evaluation criteria: items with pass/fail scoring rather than weighted scoring

Produce a numbered list of every mandatory requirement found.

### Step 3: Map Requirements to Capabilities

Read `references/capabilities.md`. For each mandatory requirement, assign a status:

| Status | Meaning |
|---|---|
| **COMPLIANT** | Company fully meets this requirement per capabilities.md |
| **PARTIAL** | Company can partially meet this, or could with reasonable effort |
| **NON-COMPLIANT** | Company cannot meet this, or it directly conflicts with a stated constraint |
| **UNCLEAR** | Requirement is ambiguous or capabilities.md lacks sufficient information |

If the user has the AutoRFP.ai MCP connected and the prospect's requirements have been imported into a project, optionally use the MCP to estimate Content Library coverage. Phrase it as: "Approximately X% of these requirements can be answered from your existing approved content."

Flag every NON-COMPLIANT item as a potential deal-breaker. If the RFP states all mandatory requirements must be met, even one NON-COMPLIANT is a strong No-Go signal. Call this out explicitly.

### Step 4: Answer Qualification Questions

Read `references/questions.md`. Work through every question using the RFP content as primary source.

For each question:
1. State the question
2. Answer based on what the RFP reveals (or "Not found in RFP" if absent)
3. Assign a score from 1-5 per the scoring guidance
4. Provide brief rationale

Some questions need information only the user has (relationship strength, team bandwidth, competitive intel). Flag these as **REQUIRES USER INPUT** and note what information is needed. Do not guess or assume - surface the gap.

### Step 5: Calculate Go/No-Go Score

1. Calculate weighted score per category using weights from questions.md
2. Calculate overall weighted percentage
3. Apply decision thresholds:
   - **80%+ = Strong Go** - Pursue with confidence
   - **65-79% = Conditional Go** - Pursue, but address flagged risks
   - **50-64% = Executive Review** - Escalate; significant risks present
   - **Below 50% = No-Go** - Do not pursue unless strategic override justified
4. List all NON-COMPLIANT mandatory items separately as deal-breaker flags
5. List all REQUIRES USER INPUT items that could materially shift the score

### Step 6: Output the Report

Present using this structure:

```
## RFP Shredder Report

### 1. RFP Overview
Issuing org, opportunity name, deadline, value, duration, sector

### 2. Mandatory Requirements Assessment
Table: # | Requirement | Status | Notes

### 3. Go/No-Go Scorecard
Table: Category | Weight | Score (1-5) | Weighted Score | Key Rationale

### 4. Overall Recommendation
- Total weighted score: X%
- Decision: [Strong Go / Conditional Go / Executive Review / No-Go]
- Deal-breaker flags
- Items requiring user input

### 5. Key Risks and Considerations
Top 3-5 risks as narrative

### 6. Win Theme Opportunities
If Go or Conditional Go: 2-3 potential win themes based on strong capability fit

### 7. Content Library Coverage (if MCP connected)
Rough estimate of how much of this RFP can be answered from existing approved content in AutoRFP.ai
```

## Output Format

- Quick assessments: structured markdown directly in conversation
- Formal reports: create as `.md` file and present to user
- If user requests DOCX or PDF, use the appropriate creation skill

## Important Principles

- This skill does not make the final bid decision. It provides a structured, evidence-based recommendation.
- Always surface uncertainty. If the RFP is vague, say so instead of assuming.
- If the RFP contains evaluation criteria with explicit weightings, include them in the report since they should influence where the team invests writing effort.
- Encourage users to customize `references/questions.md` and `references/capabilities.md` to match their business. `capabilities.md` ships as an empty template; the skill cannot produce a meaningful Go/No-Go without it.
