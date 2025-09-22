---
description: Initialize workflows for organization or project from templates
argument-hint: [project-name | "for this project"]
allowed-tools: Bash(ls:*), Bash(cp:*), Bash(mkdir:*), Read, Write, Edit
---
# Initialize Workflow

Initialize workflows for organization or project from templates.

## Usage

Natural language patterns:
- `/init-workflow` - Initialize for current directory
- `/init-workflow $1` - Initialize specific project (e.g., `/init-workflow backend`)
- `/init-workflow for this project` - Initialize current project

## Process

1. **Detect Context**
   - Parse argument: $ARGUMENTS
   - If empty: Check current directory (org or project)
   - If contains project name: Navigate to that project
   - If "for this project": Use current directory as project

2. **Copy Templates**
   - Organization: Copy from `workflow-templates/organization/default/`
   - Project: Copy from `../[org-folder]/workflow-templates/project/default/`

3. **Place Files**
   ```bash
   ! cp -r workflow-templates/[level]/default/instructions ./instructions
   ! cp -r workflow-templates/[level]/default/standards ./standards
   ! mkdir -p .claude/commands
   ! cp workflow-templates/[level]/default/commands/* .claude/commands/
   ```

4. **Update CLAUDE.md**
   - Add section explaining workflow structure
   - Document available commands
   - Explain org→project→repo hierarchy

5. **Commit Changes**
   ```bash
   ! git add instructions/ standards/ .claude/commands/ CLAUDE.md
   ! git commit -m "feat: initialize $1 workflows"
   ```

## Implementation Notes

- Commands reference `@../instructions/` and `@../standards/`
- No path updates needed during copy (relative paths work)
- Check for existing files and prompt before overwriting
- Ensure `.claude/` directory exists before copying commands