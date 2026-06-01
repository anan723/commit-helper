# commit-helper

A [Claude Code](https://claude.ai/code) skill that helps generate [Conventional Commits](https://www.conventionalcommits.org/) compliant commit messages with full git workflow support.

## Features

- Analyzes code changes to determine the correct commit type (`feat`, `fix`, `refactor`, etc.)
- Supports scope detection based on changed modules
- Generates well-formatted Conventional Commits messages
- Interactive workflow: preview, confirm, then commit
- Chinese-friendly explanations

## Installation

```bash
npx skills add anan723/commit-helper
```

## Usage

In Claude Code, mention you want to commit changes or type `/commit-helper`. The skill will:

1. Check git status and diff
2. Analyze the change type and scope
3. Generate a Conventional Commits message
4. Let you preview and choose to execute the commit

## Example

```
feat(auth): add user login functionality
fix(ui): correct mobile layout for login page
docs(readme): add installation instructions
```

## License

MIT
