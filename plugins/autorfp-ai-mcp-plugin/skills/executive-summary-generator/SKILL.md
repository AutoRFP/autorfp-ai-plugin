---
name: executive-summary-generator
description: Generates compelling executive summaries for RFP and bid responses that lead with win themes, address prospect priorities, and set the narrative for the entire proposal. Use this skill when a user has a completed or near-complete RFP response and needs an executive summary written. Also trigger when users say "write the exec summary", "executive summary for this bid", "proposal overview", "management summary", "opening section for my RFP", or have win themes and a completed response and need to tie it all together. The executive summary is the most-read section of any proposal and this skill treats it accordingly.
---

# Executive Summary Generator for RFP

Generates executive summaries for RFP and bid responses that are persuasive, prospect-focused, and strategically structured to set the evaluation narrative from page one.

## Works Well With

- **win-theme-generator** - Develop your win themes first; this skill structures the exec summary around them
- **conversational-intelligence-analyzer** - Prospect quotes and "why now" triggers from conversation analysis make the opening section significantly stronger
- **rfp-contradiction-checker** - Run after generating the exec summary to ensure it does not contradict the body of the response

## Why the Executive Summary Matters More Than Any Other Section

The executive summary is the only section of your proposal that every evaluator reads. Technical evaluators skim your architecture section. Legal reviewers focus on T&Cs. But the executive summary is read by everyone, from the procurement lead to the C-suite sponsor. It sets the frame through which every subsequent answer is interpreted.

Most executive summaries fail because they are about the vendor, not the prospect. They open with "Founded in 2005, we are the leading provider of..." Nobody cares. The evaluator wants to know: "Do these people understand our problem, and can they solve it?"

## What the AutoRFP.ai MCP Server Can and Cannot See

This plugin ships with the AutoRFP.ai MCP server. The MCP is read-only and can access:
- Project requirements and answers (if the proposal is being built in AutoRFP.ai)
- Tags
- The approved Content Library (useful for sourcing boilerplate, case studies, capability descriptions)

**The MCP cannot read the original RFP document.** Evaluation criteria, weightings, the prospect's narrative description of their challenge, and submission instructions all live in the source PDF/DOCX/XLSX, not the structured Q&A.

**If the user wants an exec summary anchored on the prospect's stated priorities, ask them to upload the original RFP document.** Pulling Q&A from an AutoRFP.ai project gives you the proposed solution, but it does not give you the prospect's framing of the problem. Both are needed to write a strong exec summary.

## Input Requirements

### Required (at least one):
- A completed or near-complete RFP response to summarize (uploaded file, or pulled via the AutoRFP.ai MCP if the project lives in AutoRFP.ai)
- OR a set of win themes and key proposal points to structure around

### Strongly Recommended:
- The original RFP document (to reference evaluation criteria and stated priorities) - **ask user to upload, MCP cannot see this**
- Win themes (if developed using the win-theme-generator or otherwise)
- Prospect intelligence (from the conversational-intelligence-analyzer or user knowledge)

### Optional:
- Company boilerplate or "about us" content (often available in the AutoRFP.ai Content Library via the MCP)
- Relevant case studies or references (search the Content Library by tag)
- Evaluation criteria and weightings (only available from the original RFP - ask user to upload)

## Workflow

### Step 1: Gather Context

Ask the user for:
1. The RFP response or key proposal content (file upload or AutoRFP.ai project ID)
2. The original RFP document if available (explicitly explain the MCP cannot see this)
3. Win themes (if they have them)
4. What they know about the prospect's priorities beyond what is in the RFP
5. Any specific evaluation criteria or weightings
6. Word count or page limit for the executive summary (if specified by the RFP)

If the user does not have formal win themes, ask:
- "In one sentence each, what are the 2-3 strongest reasons you should win this?"
- Use their answers as informal win themes

If the user has an AutoRFP.ai project, use the MCP to pull the requirements and answers. Then ask for the original document to anchor on evaluation criteria.

### Step 2: Analyze the Proposal

Review the RFP response (or key points) to understand:
- What capabilities are being proposed
- What implementation approach is described
- What differentiators are emphasized in the technical sections
- What case studies or references are cited
- What commitments are made (timelines, SLAs, pricing approach)

Also review the original RFP (uploaded by user) to understand:
- What the prospect asked for and why
- How the evaluation will be scored
- What language and terminology the prospect uses

### Step 3: Structure the Executive Summary

Use this framework. The exact section headings should be adapted to the RFP context, but the flow should follow this pattern:

**Opening (1-2 paragraphs):**
Start with the prospect's challenge or opportunity, in their language. Demonstrate that you understand their situation before you talk about yourself. Reference specific details from the RFP or prospect intelligence.

Do NOT open with your company history, founding date, or market position.

**Your understanding (1-2 paragraphs):**
Articulate your understanding of what the prospect needs, why they need it now, and what success looks like from their perspective. This is where conversational intelligence is invaluable. If you know the "why now" trigger, reference it.

**Your approach (2-3 paragraphs):**
Describe your proposed solution at a high level, structured around win themes rather than features. Each paragraph should connect a capability to a prospect priority.

Pattern: "[Prospect priority] requires [approach]. Our [capability] delivers this through [brief how], as demonstrated by [proof point]."

**Why us (1-2 paragraphs):**
This is where win themes are stated most directly. Each differentiator should be specific, evidence-backed, and tied to a prospect priority. Avoid generic claims.

**Proof points (1 paragraph):**
Reference the most relevant case study or customer reference. Ideally in the same sector, with quantifiable outcomes. The AutoRFP.ai Content Library (via MCP) often has approved case study content you can pull.

**Commitment (1 paragraph):**
Close with a forward-looking statement about partnership, implementation approach, and the team's commitment. Include any specific commitments (named team members, implementation timeline, support model) that demonstrate seriousness.

### Step 4: Write the Executive Summary

Draft the executive summary following the structure above. Key writing principles:

- **Prospect-first language**: "Your organization's need for..." not "Our platform provides..."
- **Specific over general**: "Reducing your regulatory reporting cycle from 15 days to 3" not "Improving efficiency"
- **Evidence over assertion**: "Based on our deployment at [similar client]" not "We are industry-leading"
- **Active voice**: "We will deploy" not "The solution will be deployed"
- **Mirror the prospect's terminology**: If they call it a "platform," do not call it a "solution." If they say "colleagues," do not say "employees."
- **Respect the word count**: If the RFP specifies a limit, stay within it. If no limit is specified, aim for 1-2 pages (500-800 words). Shorter is almost always better.

### Step 5: Review and Refine

Present the draft to the user. Ask specifically:
- Does this accurately represent your proposal?
- Does the opening resonate? Would the prospect feel understood?
- Are the win themes stated strongly enough?
- Is there anything you want to emphasize more or less?
- Does the tone match your company's voice?

Refine based on feedback. The executive summary often takes 2-3 iterations to get right.

## Output Format

- Draft: presented in conversation for discussion and iteration
- Final version: delivered in the format that matches the rest of the RFP response (`.md`, `.docx`, or copy-paste ready)

## Important Principles

- The executive summary is not a table of contents or a summary of your company. It is a persuasive argument for why you should win, structured around the prospect's priorities.
- Resist the urge to cover everything. The executive summary should focus on 2-4 key themes that differentiate you. Details belong in the technical sections.
- If the prospect stated evaluation criteria with weightings, the executive summary should spend proportional attention on the highest-weighted criteria.
- Every claim in the executive summary should be substantiated somewhere in the full proposal. The exec summary makes promises; the rest of the proposal delivers proof.
- The last impression matters as much as the first. Close with something specific and forward-looking, not a generic "we look forward to working with you."
