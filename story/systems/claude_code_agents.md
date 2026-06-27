# Claude Code Agent Routing

Cost-optimized agent routing for Claude Code development on the Ashborne project. Agents are automatically dispatched based on task type.

## Agent Configuration

### Installed Plugin
- **Location**: `~/.claude/plugins/cache/user/model-router/1.0.0/`
- **Status**: Enabled in `~/.claude/settings.json`

### Available Agents

| Agent | Model | Purpose | Cost |
|-------|-------|---------|------|
| `shell-runner` | Haiku (delegates to Ollama gemma4:e2b) | File ops, shell commands, git, diagnostics | Free (local) |
| `code-writer` | Sonnet 4.6 | Write code, debug, refactor, architecture | Balanced |
| `code-reviewer` | Sonnet 4.6 | Code review, design critique, alternatives | Balanced |
| `story-writer` | Haiku | Narrative, dialogue, worldbuilding, lore | Cheap |

### Dispatch Rules

Claude Code automatically selects the appropriate agent based on your request:

- **shell-runner**: "run X", "check status", "list files", "git X", "install Y"
- **code-writer**: "write function", "debug this", "refactor", "implement feature", "design X"
- **code-reviewer**: "review", "check this code", "critique", "alternative approaches"
- **story-writer**: "write scene", "dialogue for", "character voice", "worldbuilding", "narrative"

## Local Model Integration

### Ollama Setup
- **Service**: Running at `http://localhost:11434`
- **Configuration**: `OLLAMA_HOME=/var/home/napalm/.ollama` in `/etc/systemd/system/ollama.service`
- **Models available**:
  - `gemma4:e2b` (5.1B, free for shell-runner delegation)
  - `gemma4:e4b` (8.0B)
  - `gemma4:31b` (31.3B)
  - `qwen3.5:latest` (9.7B)
  - `qwen3-coder:latest` (30.5B)

### MCP Integration
- **Service**: Ollama MCP server via `ollama-mcp` npm package
- **Configured in**: `~/.claude/settings.json` → `mcpServers.ollama`
- **Endpoint**: `http://localhost:11434`
- **Usage**: `shell-runner` agent can delegate to local Ollama for free execution

## Development Workflow

### Starting a Session
1. Ensure Ollama is running: `sudo systemctl status ollama`
2. Open Claude Code
3. Ask your question — the right agent will be selected automatically

### Examples

**Run a shell command** (uses shell-runner + local Ollama):
```
list all TypeScript files in src/
```

**Write code** (uses code-writer):
```
implement a crafting system manager class that handles recipe tracking and component inventory
```

**Review a change** (uses code-reviewer):
```
review the changes I just made to the dialogue system and suggest improvements
```

**Write narrative** (uses story-writer):
```
write the opening monologue for Maddox discovering the anomalous partition
```

## Cost Optimization

- **shell-runner**: Free (local Ollama gemma4:e2b)
- **story-writer**: ~0.3¢ per task (Haiku)
- **code-writer**: ~2¢ per task (Sonnet 4.6)
- **code-reviewer**: ~2¢ per task (Sonnet 4.6)

Typical workflow: 70% shell-runner (free) + 20% story-writer (cheap) + 10% code (balanced).

## Customization

To modify agent behavior, edit the agent files at:
```
~/.claude/plugins/cache/user/model-router/1.0.0/agents/
```

Changes take effect immediately in the next Claude Code session.

## Troubleshooting

**Ollama not responding**: Check service status and restart if needed:
```bash
sudo systemctl restart ollama
curl http://localhost:11434/api/tags
```

**Agents not appearing**: Verify plugin is enabled in `~/.claude/settings.json`:
```json
"enabledPlugins": {
  "model-router@user": true
}
```

**MCP tool not available**: Ensure `ollama` is configured in `mcpServers` and the npm package is installed on first use (auto-installs via `npx -y ollama-mcp`).
