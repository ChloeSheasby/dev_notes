# Git Workflow

## When you are ready to make a PR:

##### If you are worried about accidentally messing up your branch or if you are about to do something risky, you can always back it up by making a backup branch.

### 1. Fetch from remote.
**Command Line**
```
git fetch --all 
```

**VS Code**
Source Control ... &rarr; Pull, Push &rarr; Fetch From All Remotes &rarr; origin/main

### 2. Count your commits on your branch.
**Command Line**
```
git rev-list --count --first-parent <parent>..<branch_name>
```

**VS Code**
Use the [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) VS Code extension to manually count the number of commits on your branch.

### 3. Squash commits.
```
git reset --soft HEAD~<number of commits to squash>
```

### 4. Do a local commit with a message.
This is to save the squash locally.
**Command Line**
```
git add .
git commit -m "squashed commits into one"
```

**VS Code**
- Stage changes.
- Commit message.
- Push.

### 5. Force push to remote.
```
git push -f origin <name of branch>
```

### 6. Rebase onto the dev branch.
**Command Line**
```
git rebase origin/dev
``` 

**VS Code** 
Source Control ... &rarr; Branch &rarr; Rebase Branch... &rarr; origin/dev

### 7. Force push to remote.
```
git push -f origin <name of branch>
```

### 8. Open a PR.

### 9. Enjoy your clean Git history :)