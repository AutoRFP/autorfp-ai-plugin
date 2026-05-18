# autorfp-ai-plugin

The Claude plugin that powers AutoRFP.ai inside Claude. See the [repository README](../../README.md) for installation and usage.

## Skills

- `/autorfp-ai-mcp-plugin:rfp-shredder` - Go/No-Go qualification on a new RFP
- `/autorfp-ai-mcp-plugin:executive-summary-generator` - persuasive exec summary for a near-complete proposal
- `/autorfp-ai-mcp-plugin:rfp-contradiction-checker` - pre-submission QA gate

Plus the AutoRFP.ai MCP server, auto-loaded via `.mcp.json` and authenticated on first use.

## What the MCP can read

- Projects and requirements (Q&A)
- Tags
- Approved Content Library

## What the MCP cannot read

The original RFP document (PDF/DOCX/XLSX). Upload it when prompted.

## Customize before running rfp-shredder

`skills/rfp-shredder/references/capabilities.md` ships as an empty template. Fill it in with your company's actual capabilities, certifications, deployment model, and constraints. The skill maps mandatory RFP requirements against this file.

`skills/rfp-shredder/references/questions.md` ships with a default 7-category Go/No-Go scoring framework. Customize weights to your business.
