
When you are ready to make a PR:
1. Fetch from remote.
	1. Command Line: `git fetch --all 
	2. VS Code: Source Control ... &rarr; Pull, Push &rarr; Fetch From All Remotes &rarr; origin/main
2. Count your commits on your branch.
	1. 
3. Squash commits.
	1. `git reset --soft HEAD~<number of commits to squash>`
Git flow: fetch from remote, squash commits (+ do a local commit w/ message), force push to remote, rebase onto dev branch, force push, open a PR.  
Note: backup before doing anything risky.