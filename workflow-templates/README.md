# Workflow Templates - Development Guide

This directory contains the source templates for HiveMind's workflow distribution system.

## Development Structure

```
workflow-templates/
├── organization/           # Organization-level templates
│   └── default/           # Default variant
│       ├── instructions/
│       │   ├── core/     # Agent-OS core workflows (DO NOT ADD NEW)
│       │   └── meta/     # Agent-OS meta workflows (DO NOT ADD NEW)
│       ├── standards/     # Agent-OS standards (DO NOT ADD NEW)
│       └── commands/      # Agent-OS commands + init-workflow
└── project/
    └── default/
        └── commands/      # Project-level command overrides
```

## Critical Development Rules

1. **DO NOT add new Agent-OS style components** - Only update references
2. **All Agent-OS references** must be changed from `@.agent-os/` to `@../`
3. **HiveMind additions** must be clearly separated and documented
4. **See [workflow-design.md](../docs/workflow-design.md)** for component origins and rules

## Component Sources

### Agent-OS Components (Maintain Parity)
- All files in `instructions/core/` except `folder-structure.md`
- All files in `instructions/meta/`
- All files in `standards/`
- Commands: analyze-product, create-spec, create-tasks, execute-tasks, plan-product

### HiveMind Components (Our Additions)
- `instructions/core/folder-structure.md` - Three-tier hierarchy explanation
- `commands/init-workflow.md` - Template initialization command

## Template Distribution Flow

```
1. Source Templates (hivemind/workflow-templates/)
       ↓
2. HiveMind init-org copies to [org]/workflow-templates/
       ↓
3. User runs /init-workflow to activate
       ↓
4. Templates copied to active locations
```

## Making Changes

### Updating Agent-OS Components
1. Pull latest from Agent-OS source
2. Update only the content, preserving our reference changes
3. Test that all `@../` references work
4. Document the sync date in workflow-design.md

### Adding HiveMind Features
1. Verify it doesn't overlap with Agent-OS patterns
2. Place in appropriate location
3. Document in workflow-design.md with clear origin marking
4. Update this README if structural changes

### Testing Changes
```bash
# Test template copying
hivemind init-org test-org

# Verify structure
ls test-org/workflow-templates/

# Test activation (in Claude)
/init-workflow
```

## Variant Planning

Future variants will follow pattern:
- `organization/startup/` - Fast iteration focus
- `organization/enterprise/` - Compliance heavy
- `project/scrum/` /  `project/kanban/`
- `project/frontend/` /  `project/backend/`

Each variant must maintain the same component separation rules.

## References

- Design spec: [../docs/workflow-design.md](../docs/workflow-design.md)
- Agent-OS source: [github.com/buildermethods/agent-os](https://github.com/buildermethods/agent-os)
- Integration spec: [../../specs/03_agent-os-hivemind-integration.md](../../specs/03_agent-os-hivemind-integration.md)