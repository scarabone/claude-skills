---
name: integration-preflight
description: >
  MANDATORY before building integrations with external platforms, APIs, or services.
  Triggers on: connecting to third-party services, setting up tunnels/proxies,
  implementing auth flows, deploying to cloud platforms, configuring webhooks,
  any work that bridges local code to external systems. CRITICAL FAILURE MODE:
  Assuming feature parity across platforms (desktop ≠ web ≠ mobile ≠ API), or
  starting multi-step implementation without verifying the end goal is achievable.
  Search requirements BEFORE implementation, not after hours of setup.
---

# Integration Preflight Check

## Core Rule

**Verify requirements before implementation.**

If integration work takes >10 minutes, confirm the destination platform actually supports what you're building BEFORE starting.

## Triggers

Run this check when:
- Connecting to third-party APIs or services
- Setting up tunnels, proxies, or public endpoints
- Implementing authentication flows (OAuth, API keys, tokens)
- Deploying to cloud platforms
- Building for a specific client (web, mobile, desktop, CLI)
- Configuring webhooks or callbacks
- Any bridge between local code and external systems

## The Check (Do This First)

### 1. Identify the Target Platform
What specific platform/client will consume this integration?
- Claude.ai web ≠ Claude Desktop ≠ Claude Code ≠ Claude API
- GitHub.com ≠ GitHub Desktop ≠ GitHub CLI
- Be specific. "Claude" is not specific enough.

### 2. Search Official Requirements
Before ANY implementation:
```
Search: "[platform] [integration type] requirements [current year]"
Search: "[platform] [feature] authentication requirements"
Search: "[platform] API documentation [specific endpoint]"
```

Look for:
- **Authentication requirements** (OAuth, API keys, tokens, none)
- **Plan/tier requirements** (free, pro, enterprise)
- **Platform-specific limitations** (web only, desktop only, etc.)
- **Required endpoints or protocols**

### 3. Verify Feature Parity (Don't Assume)

| Assumption | Reality |
|------------|---------|
| "Works on desktop, will work on web" | Often false. Different auth, different capabilities. |
| "API supports it, web UI will too" | Web may have restrictions API doesn't. |
| "Mobile app same as desktop" | Feature sets often differ. |
| "Free tier has this" | May require paid plan. |

### 4. Confirm Before Proceeding

State findings to user:
- "Claude.ai web requires OAuth 2.1 for MCP servers. Authless only works with Claude Desktop."
- "This API requires Enterprise plan for webhook support."
- "Web interface doesn't support custom integrations, only the CLI does."

If requirements aren't met, STOP and discuss alternatives before building.

## Anti-Patterns (What Went Wrong)

### The Tunnel Disaster (2026-01-30)
**Task:** Expose MCP server to internet for Claude.ai web access
**Mistake:** Built entire Cloudflare tunnel infrastructure without checking Claude.ai web requirements
**Discovery:** Claude.ai web requires OAuth 2.1; authless servers only work with Claude Desktop
**Wasted:** ~2 hours of setup, configuration, testing, then rollback
**Fix:** 5-minute search would have revealed OAuth requirement before any implementation

### Pattern: Assumed Feature Parity
"Claude Desktop supports authless MCP, so Claude.ai web must too."

Wrong. Different clients have different security models.

## Quick Reference: Common Gotchas

| Platform | Gotcha |
|----------|--------|
| Claude.ai web | Requires OAuth 2.1 for MCP (authless = Desktop/Code only) |
| GitHub Actions | Different token scopes than personal access tokens |
| Cloudflare | Free tier has request limits, some features Workers-only |
| AWS Lambda | Cold starts, timeout limits, VPC complexity |
| OAuth flows | Callback URLs must be pre-registered |
| Webhooks | Often require HTTPS, public IP, specific response format |

## Decision Point

After the preflight check:

- **Requirements met?** → Proceed with implementation
- **Requirements unclear?** → Search more or ask user before proceeding
- **Requirements NOT met?** → STOP. Discuss alternatives. Don't build something that won't work.

## The 10-Minute Rule

If the integration will take more than 10 minutes to build:
1. Spend 5 minutes on preflight check
2. Confirm requirements with user
3. Then build

Never invert this. Building first and checking later = wasted work.
