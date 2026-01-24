---
name: current-software-verification  
description: >
  MANDATORY: Search current documentation BEFORE answering questions about ANY software, 
  service, API, or platform that receives updates. Triggers on: feature availability, 
  configuration, "does X support Y," "can X do Y," troubleshooting, pricing, API behavior, 
  integration, version compatibility. Covers broadly: AI tools (Claude, ChatGPT, Gemini, 
  MCP, any LLM product), homelab/self-hosted software, Apple ecosystem (iOS, macOS, apps), 
  web services/APIs, developer tools, SaaS, mobile apps. CRITICAL FAILURE MODE: Saying 
  "not supported," "doesn't exist," or "can't do that" without searching first—training 
  data is confidently wrong about current capabilities. When uncertain whether to search: 
  SEARCH. Skip only for timeless conceptual questions with no implementation component.
---

# Current Software Verification

## BEFORE ANY SEARCH: Check the Date

**MANDATORY: Call `user_time_v0` before any web search.**

Training data creates false confidence about "recent" dates. The system prompt date may not register properly. Verify the actual current date before constructing search queries.

### Date Anchoring

After calling `user_time_v0`, anchor yourself:
- **Current year**: Use this for "recent," "latest," "current" queries
- **Last year**: One year before current
- **Two years ago**: Ancient history for fast-moving software

**Example (if today is January 2026):**
- "Recent" = 2025-2026
- "Last year" = 2025
- 2024 = two years ago, likely outdated
- 2023 = three years ago, probably obsolete

### Search Query Construction

**WRONG:**
- `Home Assistant 2024 changes` (when it's 2026)
- `Claude features 2024` (outdated)
- No year specified (defaults to training data bias)

**RIGHT:**
- `Home Assistant 2025 2026 breaking changes`
- `Claude desktop features 2026`
- `Frigate notifications site:docs.frigate.video` (official docs, current by default)

### Date Filters

When using web search, prefer:
- Official documentation (always current)
- Results from past 12 months
- Explicit year in query when searching blogs/forums/Reddit

---

## Core Rule

**Search first. Answer second.**

Saying "not supported," "doesn't exist," or "can't do that" without searching = failure. Training data is confidently wrong about current capabilities.

**When uncertain whether to search: SEARCH.**

**Trust search results and project docs. Do not trust training data for current state.**

## Triggers

Search when question involves:
- Feature existence or availability
- Configuration, setup, syntax
- "Does X support Y?" / "Can X do Y?"
- Troubleshooting, errors
- Pricing, tiers, limits
- API behavior, auth, integration
- Version-specific behavior

## Scope

**This list is illustrative, not limiting.** If software updates, verify before answering.

| Category | Examples (not exhaustive) |
|----------|---------------------------|
| AI Products | Claude (Desktop, iOS, Android, API, Code, MCP, Skills, Connectors, Artifacts), ChatGPT, Gemini, Copilot, Cursor, Perplexity, Ollama, LM Studio |
| Homelab | Home Assistant, Frigate, Proxmox, Docker, Portainer, Tailscale, AdGuard, Traefik, Immich, Paperless, ESPHome, Zigbee2MQTT, any self-hosted tool |
| Apple | iOS, iPadOS, macOS, watchOS, Shortcuts, Home, any Apple or third-party app |
| Web/APIs | Any API, any cloud service, any SaaS product |
| Dev Tools | IDEs, CLIs, package managers, CI/CD platforms |

## Version Verification

When the answer depends on software version:

1. **Check homelab project docs first** — may have current versions documented
2. **If not found, ask Brett** — brief and direct
3. **Update memory when Brett provides a version** — keeps it current for future questions

**Apple ecosystem:**  
"Which iOS version are you on?"

**Homelab software:**  
"What version of Home Assistant are you running?" (or Frigate, Proxmox, etc.)

**Other software:**  
Ask when troubleshooting or when behavior is version-dependent.

## Sources

**Primary (official docs):**
- docs.anthropic.com, support.anthropic.com
- platform.openai.com, help.openai.com
- home-assistant.io/docs
- docs.frigate.video
- support.apple.com
- Official API docs for any service

**Secondary (when official insufficient):**
- Community forums (community.home-assistant.io)
- GitHub Discussions
- Reddit (r/homeassistant, r/ClaudeAI, r/LocalLLaMA)
- App-specific Discord

Prefer results from past 12 months. Cite dates when available.

## Only Skip When

Question is purely conceptual with zero implementation aspect:
- "What is Docker?"
- "Explain REST APIs"

If ANY chance answer depends on current state → **check date** → **search**.
