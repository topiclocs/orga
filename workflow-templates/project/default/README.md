# Project-Level Workflows

This directory contains project-specific workflow templates that can override or extend organization-level workflows.

## Hierarchy and Override System

Projects inherit from the organization but can customize:

1. **Instructions**: Projects can override any organization instruction by creating a file with the same name
2. **Standards**: Projects can define additional standards or override organization standards
3. **Commands**: Projects get their own commands that can reference either project or organization workflows

## How Overrides Work

When Claude executes a command:
1. First checks for project-level instruction/standard
2. Falls back to organization-level if not found locally
3. Project CLAUDE.md context always takes precedence

## Example Override

To override organization's `create-spec.md`:
1. Create `instructions/create-spec.md` in your project
2. Define project-specific spec creation process
3. The command automatically uses your version

## Common Project Customizations

- **Tech Stack Specific**: Override `execute-task.md` for framework-specific patterns
- **Domain Specific**: Custom `create-spec.md` for industry requirements
- **Team Preferences**: Project-specific code standards in `standards/`

## Best Practices

1. Only override when necessary - inherit organization defaults when possible
2. Document why you're overriding in the customized file
3. Keep overrides minimal and focused on project-specific needs
4. Consider proposing improvements back to organization level if broadly useful