
When you are ready to make a PR:
### Fetch from remote.
Command Line: `git fetch --all 
VS Code: Source Control ... &rarr; Pull, Push &rarr; Fetch From All Remotes &rarr; origin/main

### Count your commits on your branch.
Option 1: Use the [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) VS Code extension to manually count the number of commits on your branch.

### Squash commits.
`git reset --soft HEAD~<number of commits to squash>`
Git flow: fetch from remote, squash commits (+ do a local commit w/ message), force push to remote, rebase onto dev branch, force push, open a PR.  
Note: backup before doing anything risky.