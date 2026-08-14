# What Not to Commit

These are the rules for keeping the repository safe and clean.  
- Restrict creations: Only people with bypass permission can create branches.  
- Restrict updates: Only people with bypass permission can push changes.  
- Restrict deletions: Only people with bypass permission can delete branches.  
- Require linear history: No merge commits; only fast-forward merges.  
- Require signed commits: All commits must be verified.  
- Require pull requests: Changes must be made through a PR instead of direct pushes.  
- Require status checks: CI checks must pass before merging.  
- Block force pushes: Prevent rewriting history.  
- Require code scanning and quality checks: Security and quality tools must approve changes.  
- Restrict code coverage: Pull requests must meet minimum test coverage.  
- Copilot code review: Copilot automatically reviews new PRs when available.
