_I learned this from Isaac H._

If main has been updated, my inclination has always been to pull from main into my feature branch. However, this is not best practice:
- Pulling from main lines all commits in history order.
- Your 'source of truth' will remain at an older main instead of the new one.
- If you happen to need to revert main, it's almost impossible--there isn't a clean line of where main is.

The thing to remember is the whatever main has is waayyyy more important than your branch.
Here is why rebasing is much better:
- Rebasing takes your branch, scoops up your commits, and makes the newest main the foundation of your branch.
- Then it asks if you want to apply your commits.
- Then you resolve merge conflicts.
- Thus your branch always stay based on the latest main instead of some pieced together main.

Here is how to do that:
1. Rebase to main.
	1. Command Line: `git rebase origin/main` 
	2. VS Code: Source Control ... &rarr; Branch &rarr; Rebase Branch... &rarr; origin/main
2. Pick if you want to keep all of your commits or merge them, etc.
3. Resolve merge conflicts.
	1. "Incoming" changes will be from your feature branch.
	2. "Current" changes will be from the latest **main** branch.
4. Force push back to your remote branch. (It's safer to do this command line only.)
	1. `git push -f origin <your-branch-name>`
