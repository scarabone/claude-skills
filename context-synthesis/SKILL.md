---
name: context-synthesis
description: MANDATORY synthesis of Brett's established context BEFORE answering technical questions. Triggers IMMEDIATELY when Brett mentions ANY of these - Homelab (Home Assistant, Frigate, Proxmox, Docker, Portainer, Dockge), networking (Tailscale, AdGuard), self-hosted software (Grocy, Paperless, Immich, any self-hosted tool), cameras/surveillance, automations, MCP servers, code projects, development environment, or uses phrases like "my setup", "my server", "my cameras", "the container", "my automation". Apply proactively to avoid re-asking for information already established in conversation history or memory. Does NOT trigger for pure theoretical questions with no implementation component.
---

# Context Synthesis Skill

Before responding to technical questions, synthesize relevant context from the user's established setup, preferences, and ongoing projects.

## Core Context Areas

**Infrastructure**
- Proxmox host: Dell XPS server
- Home Assistant: Docker container, managed via Portainer/Dockge
- Networking: Tailscale for remote access, AdGuard DNS integration
- Surveillance: Frigate with 4 cameras (front yard, doorbell, driveway, + 1 more)
- Self-hosted services: Running various Docker containers for home automation and media
- Development: Apple ecosystem (MBP M4 Pro 24GB, iPhone 16 Pro, MBA M2)

**Active Projects**
- MCP server development (authenticated browser, search proxy, Proxmox management)
- Frigate camera troubleshooting (configuration not connecting)
- Home Assistant voice optimization
- Claude skills development
- Warp terminal evaluation for development workflow

**Established Preferences**
- Backup before changes, test incrementally
- Simple reliable solutions over complex cutting-edge
- Professional/personal AI use kept separate (no AI at work)
- Apple ecosystem exclusive
- Atlanta timezone, hospital schedule constraints

## Application Pattern

**Before responding, check:**
1. Does this touch their homelab? → Reference Proxmox/Docker/HA setup
2. Is this about automation? → Consider existing HA integrations and voice work
3. Involves code/development? → Note Apple ecosystem, backup-first approach
4. References "the setup" or "my system"? → Apply full infrastructure context
5. Builds on previous work? → Connect to MCP servers, skills, or automations
6. Mentions self-hosted software? → Consider Docker stack and existing services

**When NOT to apply:**
- Theoretical questions with no implementation component
- Questions explicitly about different setups/environments
- Initial exploration of completely new topics

## Response Adjustments

**Skip redundant questions:**
- ✗ "Are you running Home Assistant in Docker or as an OS?"
- ✓ Apply knowledge: Docker container on Proxmox

**Suggest consistent approaches:**
- ✗ "You could try X, Y, or Z"
- ✓ "Following your backup-first approach, let's snapshot the container first"

**Build on previous work:**
- ✗ Provide generic solution
- ✓ "We can extend your existing search proxy MCP server to handle this"

**Respect constraints:**
- ✗ Ignore timing considerations
- ✓ "Since you're on the hospital schedule, this backup can run during your admin day"

## Context Loading Efficiency

Keep context application lightweight - reference only what's directly relevant. Don't recite the user's entire setup unless they're asking for an overview.

**Good:** "I'll add this to your Docker stack on Proxmox"
**Bad:** "Since you're running a Dell XPS with Proxmox hosting Docker containers managed by Portainer..."
