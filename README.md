# Universal AI Governance MCP

One MCP server that assesses AI projects against AI laws, ISO standards, risk frameworks, and technical compliance checks, behind a single interface. It returns a YES / NO / NEEDS REVIEW verdict in milliseconds, with traceable evidence, and a full internal audit report on request.

**Live MCP endpoint:** https://ai-governance-mcp.ravi-antone.workers.dev/mcp
**Transport:** MCP Streamable HTTP (JSON-RPC over POST /mcp)
**Landing page:** https://ai-governance-mcp.ravi-antone.workers.dev
**Version:** 1.1.0-audit

## Install

No API key is needed in this preview. Do not submit private repositories, production personal data, or real secrets.

### Claude Code

```
claude mcp add --transport http ai-governance https://ai-governance-mcp.ravi-antone.workers.dev/mcp
```

Then inside Claude Code run `/mcp` to confirm it connected, or run `claude mcp list`.

### Cursor

Edit `.cursor/mcp.json` in your project, or `~/.cursor/mcp.json` for every project, then restart Cursor:

```json
{
  "mcpServers": {
    "ai-governance": {
      "url": "https://ai-governance-mcp.ravi-antone.workers.dev/mcp"
    }
  }
}
```

### VS Code

Create `.vscode/mcp.json` in your workspace, or use Command Palette, MCP: Add Server, HTTP:

```json
{
  "servers": {
    "ai-governance": {
      "type": "http",
      "url": "https://ai-governance-mcp.ravi-antone.workers.dev/mcp"
    }
  },
  "inputs": []
}
```

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json`. Windsurf uses `serverUrl`, not `url`:

```json
{
  "mcpServers": {
    "ai-governance": {
      "serverUrl": "https://ai-governance-mcp.ravi-antone.workers.dev/mcp"
    }
  }
}
```

### Claude Desktop

Settings, Connectors, Add custom connector. Name it `ai-governance` and paste the MCP URL above.

### MCP Inspector and other clients

Run `npx @modelcontextprotocol/inspector`, choose Transport Streamable HTTP, paste the MCP URL, and Connect. Any other Streamable HTTP client uses the same URL.

## First prompts to try

1. Discover the frameworks available, then assess this project.
2. Review these files against the governance checks and show evidence.
3. Generate an ISO/IEC 42001 audit report for this project, with nonconformities and corrective actions.
4. Fix a failed check, then review the changes and tell me what is fixed.

## Tools (22)

discover_frameworks, assess_ai_system, review_codebase, map_requirements, assess_ai_risks, check_controls, generate_tests, generate_evidence, review_changes, explain_requirement, register_watch, get_watch_report, generate_audit_report, get_audit_report, get_about, health_check, assess_prompt, review_agent_action, check_agent_config, generate_agent_policy, get_example_prompts, plan_next_steps.

Full tool schemas are in `examples/tools.json`, live from `/api/tools`.

## Agent-first tools

This MCP is mainly used by an AI agent. An agent should start with `get_about` (product, owner, contact, install, limitations) and `health_check` (self-test), then use `assess_prompt` before executing a prompt, `review_agent_action` before a destructive, financial, or external action, and `check_agent_config` for risky permissions. `generate_agent_policy` produces a governance system-prompt snippet, `get_example_prompts` gives the full tool workflow, and `plan_next_steps` turns an assessment into an ordered task list: fix failed checks first, then human review, re-check, audit, and watch.

## Framework maturity

- ISO/IEC 42001: **Implemented**. 50 checks, ISO42001-01 to ISO42001-50, covering clauses 4 to 10 and Annex A controls, based on the structure of BS ISO/IEC 42001:2023. Full ISO text is NOT reproduced in this product. Use your own licensed copy to read the standard.
- EU AI Act, GDPR, ISO/IEC 23894, NIST AI RMF, ISO/IEC 27001, 27701, 42005, 38507: **Work in Progress**. All are exposed in tools and catalogue, not hidden, and not claimed as full modules yet.

## Audit reporting

`generate_audit_report` returns an internal audit report: scope and criteria, audit opinion, summary by clause, major and minor nonconformities with corrective actions, observations needing human review, evidence trace with file and line, limitations, and next audit. Reports are stored and retrievable by audit ID with `get_audit_report`.

Reproducible samples are in `examples/sample-audit.json`. Risky sample: 0 Verified, 20 Failed (19 major, 1 minor), 23 observations, 7 not applicable. AIMS documentation sample: 50/50 Verified.

## Fire-and-Forget Watch

`register_watch` stores a project snapshot with a weekly or monthly schedule. The hosted worker re-assesses due watches on Mondays at 06:00 UTC and stores reports, retrievable with `get_watch_report`.

## Limitations, read before use

- Developer preview, unauthenticated. Do not submit private repositories or secrets.
- Automated checks are not legal compliance, not a conformity assessment, and not ISO certification.
- Audit reports are internal audit only, not a certification decision.
- ISO material is referenced by structure and clause identifier only, not reproduced.
- Deterministic checks only in this preview. Model-assisted reasoning is not yet in the assessment engine.
- The $49/developer/month price on the landing page is a pricing hypothesis, not a validated price.

## Contact

ravi.antone@gmail.com, +46733115830

The same contact details are returned by the `get_about` tool and by `GET /api/about`.
