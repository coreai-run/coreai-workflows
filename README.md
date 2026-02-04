# COREAI Workflows

Official workflow registry for COREAI.

## What are Workflows?

Workflows are multi-step automation sequences that combine multiple skills and actions to accomplish complex tasks. Unlike skills (which are single-purpose tools), workflows orchestrate a series of operations to achieve a broader goal.

## Installation

Install a workflow using the COREAI CLI:

```bash
coreai workflow install <name>
```

For example:

```bash
coreai workflow install code-review
```

## Workflow Structure

Each workflow is a directory containing:

```
workflow-name/
├── WORKFLOW.md      # Workflow definition and instructions (required)
└── defaults.yaml    # Default configuration values (optional)
```

### WORKFLOW.md

The main workflow definition file that describes:
- What the workflow does
- The steps involved
- Required inputs and outputs
- Any dependencies on skills

### defaults.yaml

Optional configuration file with default values for the workflow.

## Creating a Workflow

1. Create a new directory under `workflows/` with your workflow name
2. Add a `WORKFLOW.md` file with your workflow definition
3. Optionally add a `defaults.yaml` for default configuration
4. Submit a pull request

## License

MIT
