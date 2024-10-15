# Use aliases

## .bashrc aliases

```bash
alias git_config_view='git config --list'
alias git_repo-remote-url='git remote get-url origin 2> /dev/null'

alias git_log-oneline='git log --graph --decorate --pretty=oneline --abbrev-commit'

alias git_clean-local-branches='git fetch --prune 2> /dev/null'
alias git_clean-untracked='git clean -fd -f 2> /dev/null'
alias git_clean-all='git-clean-local-branches && git-clean-untracked'

alias git_delete-merged-branches-locally='git branch --merged 2> /dev/null | egrep -v "(^\*|master|main|develop|dev|stag|staging)" | xargs git branch -d'
```
