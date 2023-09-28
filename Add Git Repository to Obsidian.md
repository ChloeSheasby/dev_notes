# Add Git Repository to Obsidian

*I found these instructions from https://www.reddit.com/r/ObsidianMD/comments/qbvqft/obsidian_git/.*

1. Navigate to the Obsidian folder. You should see other git folders inside.
2. Create a new git repo.
```
gh repo create <repo name> --private
```

3. Set the remote repository as upstream.
```
git push --set-upstream origin main
```

4. Stage, commit, and push.
```
git add . && git commit -m "initial commit" && git push
```

5. Open Obsidian.
6. Open the Command Palette.
7. Create a backup with Obsidian Git.
8. You should see your repo in GitHub!