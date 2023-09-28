# Token Required for GitHub Access

*Here are instructions for what to do if you receive an error from Git requiring you to have a **personal access token** set up instead of using **password authentication**.*

## The Error

- Password-based authentication for Git has been removed in favor of more secure authentication methods. 
	- [https://docs.github.com/en/get-started/getting-started-with-git/why-is-git-always-asking-for-my-password](https://docs.github.com/en/get-started/getting-started-with-git/why-is-git-always-asking-for-my-password)
- You may have encountered an error on VS Code or in a terminal window when trying to access a repository on GitHub.
- All you need to do is create a personal access token to use as your authentication instead of your password.
- This means that when you login to GitHub, it will be expecting the token, not your password.

![[attachments/git-requires-pat.png]]

## Create a Personal Access Token

[https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1. On GitHub, click your profile photo, then click **Settings**.
2. On the left, click **Developer settings**.
3. On the left, click **Personal access tokens**.
4. Click **Tokens (classic)**.
	1. I'm not sure about Fine-grained tokens yet.
5. Click **Generate new token**.
6. Name your token and select an expiration date.
7. To use your token to access repositories from the command line, select **repo**.
8. Click Generate token.
9. Copy the personal access token because you won’t be able to see it again!
10. Treat the personal access token like a password and put it in a safe place.

## Set Token for Personal Machine Use

*This will save your personal access token on your machine’s list of credentials so that if you are logging in online, etc., you will be authenticated with your token instead of your GitHub password.*

[https://stackoverflow.com/questions/68779331/use-token-to-push-some-code-to-github-support-for-password-authentication-was](https://stackoverflow.com/questions/68779331/use-token-to-push-some-code-to-github-support-for-password-authentication-was)

#### Mac
1. Go to the **Keychain Access** application.
2. Press the **Login** tab.
3. Find the **GitHub key**.
4. Double click on it.
5. Check **Show Password**.
6. Change the password to your **personal access token**.

#### Windows
1. Go to Control Panel &rarr; User Accounts &rarr; Credential Manager.
2. Edit the Generic Credential of GitHub.
3. Change the password to the personal access token.

## Set Token for Remote Access

*This will save your personal access token for direct access to GitHub through command line or on applications like VS Code.*

[https://stackoverflow.com/questions/66231282/how-to-add-a-github-personal-access-token-to-visual-studio-code](https://stackoverflow.com/questions/66231282/how-to-add-a-github-personal-access-token-to-visual-studio-code)

1. Open a command line window, like in VS Code.
2. Set the current directory to your project folder.
3. Run the following command to set remote access through your personal access token:
   
```
git remote set-url origin https://<user>:<token>@github.com/<user>/<repo>.git
```

4. Now try and push your code to GitHub again.