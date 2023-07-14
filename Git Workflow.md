
## When you are ready to make a PR:

##### If you are worried about accidentally messing up your branch or if you are about to do something risky, you can always back it up with `git branch backup`.

### 1. Fetch from remote.
Command Line
```
git fetch --all 
```
VS Code: Source Control ... &rarr; Pull, Push &rarr; Fetch From All Remotes &rarr; origin/main

### 2. Count your commits on your branch.
Option 1: Use the [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) VS Code extension to manually count the number of commits on your branch.
Option 2: I haven't figured out the command line version lol.

### 3. Squash commits.
`git reset --soft HEAD~<number of commits to squash>`

### 4. Do a local commit with a message.
This is to save the squash locally.
Command Line:
```
git add .
git commit -m "squashed commits into one"
```

VS Code:
- Stage changes.
- Commit message.
- Push.


Git flow: fetch from remote, squash commits (+ do a local commit w/ message), force push to remote, rebase onto dev branch, force push, open a PR.  
Note: backup before doing anything risky.