# Git

## Commit messages
- Commit messages should be clear and concise in describing the content of the commit
- Commit messages may not include emojis

### JIRA ID
Prefix commit message with a [JIRA](https://www.atlassian.com/software/jira) ID surrounded by square brackets when available. Always use the ID of the main task and ignore sub task ID's.

**Right:**
- [JIRA-123] Add Git conventions

**Wrong:**
- Add Git conventions
- JIRA-123 Add Git conventions
- Add Git conventions (JIRA-123)

## Branch names
Prefix branches with a [JIRA](https://www.atlassian.com/software/jira) ID followed by a descriptive name. Always use dashes to split words. When you have multiple ID's for one feature you can combine them with a dash.

**Right:**
- JIRA-123-update-conventions
- JIRA-123-456-update-conventions

**Wrong:**
- update-conventions
- JIRA-123_update_conventions

## Branches
Learn more about our different [branches](branches.md).

## Remove branches directly after merging
Remove your branch directly after merging a hotfix, feature, iteration or staging branch.