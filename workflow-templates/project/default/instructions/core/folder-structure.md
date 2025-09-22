# HiveMind Workflow Structure & Hierarchy

## Three-Tier Hierarchy

HiveMind organizes knowledge and workflows across three levels:

```
Organization (e.g., cloudhippie/)
    ↓
Project (e.g., backend/)
    ↓
Repository (specific codebases)
```

## How Workflows Work

### 1. Organization Level
- Defines company-wide standards and workflows
- Located in `[org]/instructions/`, `[org]/standards/`, `[org]/.claude/commands/`
- Provides default workflows for all projects

### 2. Project Level
- Can override or extend organization workflows
- Located in `[project]/instructions/`, `[project]/standards/`, `[project]/.claude/commands/`
- Inherits from organization if not overridden

### 3. Repository Level
- Inherits from project (or organization if no project override)
- Contains actual code implementation
- Uses workflows from higher levels

## Override Mechanism

Projects can customize any organization workflow:

1. **To Override**: Create a file with the same name in your project
   - Example: Create `[project]/instructions/create-spec.md` to override org version

2. **Inheritance**: If no project-level file exists, organization version is used

3. **Context Priority**:
   - Project CLAUDE.md overrides Organization CLAUDE.md
   - Local standards override inherited standards

## Workflow Resolution

When you run a command like `/create-spec`:

1. Claude checks for project-level instruction first
2. Falls back to organization-level if not found
3. Applies local context and standards
4. Executes with full hierarchy awareness

## File Locations

### Templates (Inactive)
```
[org]/templates/
├── organization/default/  # Org workflow templates
└── project/default/       # Project workflow templates
```

### Active Workflows
```
[location]/
├── instructions/          # Step-by-step workflows
├── standards/            # Code style and practices
└── .claude/commands/     # Quick command shortcuts
```

## Activation

Workflows are distributed as templates and activated via `/init-workflow`:
- Templates remain in `templates/` until explicitly activated
- Activation copies them to active directories
- Projects can then customize as needed

## Best Practices

1. **Organization Level**: Define broad, reusable patterns
2. **Project Level**: Add domain or tech-stack specific customizations
3. **Only Override When Necessary**: Inherit defaults when possible
4. **Document Overrides**: Explain why you're customizing in the file
5. **Propose Improvements**: If useful broadly, suggest for org level