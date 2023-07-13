# Rebase vs Pull Best Practices

_I learned this from Isaac Hildebrandt._

## Why Pulling From Main Is Bad

If main has been updated, my inclination has always been to pull from main into my feature branch. However, this is not best practice:
- Pulling from main lines all commits in history order.
- Your 'source of truth' will remain at an older main instead of the new one.
- If you happen to need to revert main, it's almost impossible--there isn't a clean line of where main is.

## Why Rebasing To Main Is Good
The thing to remember is the whatever main has is waayyyy more important than your branch.
Here is why rebasing is much better:
- Rebasing takes your branch, scoops up your commits, and makes the newest main the foundation of your branch.
- Then it asks if you want to apply your commits.
- Then you resolve merge conflicts.
- Thus your branch always stay based on the latest main instead of some pieced together main.

## How To Rebase To Main
Here is how to do that:
1. (Optional) If you are worried about accidentally messing up your branch, you can always back it up with `git branch backup`.
2. (Optional) You can squash all of your commits together so that you only have to resolve merge conflicts on one commit instead of going through the same (or almost the same) files for a million commits: `git reset --soft HEAD~<number of commits to squash>`
3. Rebase to main.
	1. Command Line: `git rebase origin/main` 
	2. VS Code: Source Control ... &rarr; Branch &rarr; Rebase Branch... &rarr; origin/main
4. Pick if you want to keep all of your commits or merge them, etc.
5. Resolve merge conflicts for each commit you keep.
	1. "Incoming" changes will be from your feature branch.
	2. "Current" changes will be from the latest **main** branch.
6. Force push back to your remote branch. (It's safer to do this command line only.)
	1. `git push -f origin <your-branch-name>`

## Visuals of Rebasing vs Merging/Pulling

![[images/image-5.png]]
[Differences Between Git Merge and Rebase — and Why You Should Care](https://blog.git-init.com/differences-between-git-merge-and-rebase-and-why-you-should-care/)

<br/>


![[images/git-merge-vs-rebase 1.png|300]]
[Git Merge vs Rebase](https://www.softwaremeadows.com/posts/graphic_-_git_merge_vs_rebase/)