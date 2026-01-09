# Contributing to ClaudePM

Thanks for your interest in contributing to ClaudePM.

## Development Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Dammyjay93/claudepm.git
   cd claudepm
   ```

2. Install in Claude Code for testing:
   ```
   /plugin marketplace add Dammyjay93/claudepm
   /plugin install claudepm
   ```

## Project Structure

```
claudepm-marketplace/
├── .claude-plugin/
│   └── marketplace.json      # Marketplace configuration
├── plugins/
│   └── claudepm/
│       ├── .claude-plugin/
│       │   └── plugin.json   # Plugin metadata
│       └── commands/         # Slash commands
│           ├── claudepm.md   # Main dispatcher
│           └── claudepm/     # Subcommands
│               ├── plan.md
│               ├── start.md
│               ├── done.md
│               ├── save.md
│               ├── status.md
│               ├── switch.md
│               └── setup.md
├── docs/                     # Documentation
├── CHANGELOG.md
└── README.md
```

## Making Changes

### Commands

Commands are markdown files that Claude interprets. Each command file should:

- Have a clear purpose
- Include explicit file paths (never relative)
- Reference the File Structure in main claudepm.md

### Testing

1. Make your changes
2. Update the marketplace: `/plugin marketplace update claudepm-marketplace`
3. Reinstall the plugin: `/plugin install claudepm`
4. Test the affected commands

### Versioning

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR**: Breaking changes (command renames, behavior changes)
- **MINOR**: New features (new commands, new options)
- **PATCH**: Bug fixes

Update `CHANGELOG.md` with your changes.

## Pull Requests

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Update CHANGELOG.md
5. Submit a pull request

### PR Guidelines

- Keep changes focused and atomic
- Update documentation if needed
- Add changelog entry under `[Unreleased]`

## Reporting Bugs

Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:

- Steps to reproduce
- Expected vs actual behavior
- Your environment (Claude Code version, OS)

## Feature Requests

Use the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md) and describe:

- The problem you're solving
- Your proposed solution
- Alternative approaches considered

## Questions?

Open a [discussion](https://github.com/Dammyjay93/claudepm/discussions) or reach out to [@Dammyjay93](https://github.com/Dammyjay93).
