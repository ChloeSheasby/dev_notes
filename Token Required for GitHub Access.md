*Here are instructions for what to do if you receive an error from Git requiring you to have a **personal access token** set up instead of using **password authentication**.*

## The Error

- Password-based authentication for Git has been removed in favor of more secure authentication methods. 
	- [https://docs.github.com/en/get-started/getting-started-with-git/why-is-git-always-asking-for-my-password](https://docs.github.com/en/get-started/getting-started-with-git/why-is-git-always-asking-for-my-password)
    
- You may have encountered an error on VS Code or in a terminal window when trying to access a repository on GitHub.
    
- All you need to do is create a personal access token to use as your authentication instead of your password.
    
- This means that when you login to GitHub, it will be expecting the token, not your password.
    

// picture here

## Create a Personal Access Token

[https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1. On GitHub, click your profile photo, then click Settings.
2. On the left, click Developer settings.
3. On the left, click Personal access tokens.
4. Click Tokens (classic).
	1. I'm not sure about Fine-grained tokens yet.
5. . Click Generate new token.
    
5. Name your token and select an expiration date.
    
6. To use your token to access repositories from the command line, select repo.
    
7. Click Generate token.
    
8. Copy the personal access token because you won’t be able to see it again!
    
9. Treat the personal access token like a password and put it in a safe place.
    

