---
name: terminal-command-formatter
description: Formats terminal commands without comments for copy/paste safety. Comments in command blocks break copy/paste functionality.
---

# Terminal Command Formatter

## CRITICAL RULE: No Comments in Terminal Command Blocks

Terminal command blocks must NEVER contain comments. Comments break copy/paste functionality.

## Command Block Formatting Rules

### For Terminal Commands (bash, zsh, sh):

**Correct Pattern:**
1. Explain in prose BEFORE the command
2. Provide clean command block with NO comments
3. Explain results or next steps AFTER if needed

### For Saved Script Files:
Comments ARE allowed in saved script files using proper syntax:
- Shell scripts: `#` for comments
- Python scripts: `#` for comments
- AppleScript: `--` for comments

### Multi-Step Commands:
Break into sequential, discrete blocks - one action per block.

## Examples

### ❌ WRONG:
```bash
# Install HACS
wget -O - https://get.hacs.xyz | bash -

# Restart Home Assistant
ha core restart  # This will take a minute
```

### ✅ RIGHT:
Install HACS:
```bash
wget -O - https://get.hacs.xyz | bash -
```

Restart Home Assistant (this will take about a minute):
```bash
ha core restart
```

## Code File Exceptions

When creating saved files (not direct terminal commands), comments ARE appropriate:

**Shell script file (saved as script.sh):**
```bash
#!/bin/bash
# This script backs up Home Assistant
# Usage: ./backup-ha.sh

BACKUP_DIR="/backup"
DATE=$(date +%Y%m%d)

# Create backup
ha backups new --name "backup-${DATE}"
```

## Summary

- **Terminal command blocks**: NO comments, explain in prose
- **Saved script files**: Comments OK with proper syntax
- **Multi-step processes**: Separate blocks with prose between
- **Copy/paste safety**: Top priority for terminal commands
