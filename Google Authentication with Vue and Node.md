- The first instructions about setting up a Google client come from https://medium.com/@jebasuthan/signup-with-google-using-vuejs-11c9d4428250.
- The example code come from the Tutorial Application:
	- [Tutorial Frontend Vue2](https://github.com/OC-ComputerScience/tutorial-frontend-vue2)
	- [Tutorial Backend](https://github.com/OC-ComputerScience/tutorial-backend

## Overview

1. Setup a project with Google Developer Console.
	1. Get some codes to link your project to Google.
2. Add a Google button on the frontend on some login page.
3. Add a login service on the backend.
4. Add authorization to routes on the backend.

## Google OAuth Flow

*This is adapted from the flow chart in the [article](https://medium.com/@jebasuthan/signup-with-google-using-vuejs-11c9d4428250) mentioned above.*

![[attachments/google-oauth-flow.png]]

## Configure Google OAuth

1. Log into the [Google Developer Console](https://console.developers.google.com/).
2. Click the Select a Project dropdown and select New Project.
3. Once the project has been created, use the project selector to pick your new project.
4. Now we need to add available APIs. Select and open Library in the left menu.
5. Open and Enable Google+ API and Google Analytics API.
6. Next, we need to enable an OAuth consent screen. Select OAuth consent screen on the left side bar menu.
7. After clicking create, you will be taken to a screen where you must provide:
	1. An app name—whatever you want
	2. A user support email—preferably the email you are using to host the application
	3. Authorized domains—name of the server hosting your application
8. Click Save and Continue.
9. Don’t add anything on the next couple of pages.
10. Click Save and Continue until the app registration is complete. 
11. Now we must create an OAuth client ID. Go to the Credentials tab, click on the Create Credentials popup, and select OAuth client ID.
12. Select Web application for the Application type and provide:
	1. A name
	2. Authorized JavaScript origins:
		1. This depends on the name of the site on the AWS server. 
		2. Make sure that yours says https at the beginning. Google with not allow authentication on remote servers that are not secure.
		3. You’ll also need localhost to be an allowed origin—this is the only URL that is allowed to be http.
	3. Authorized redirect URIs: http://localhost:8081/callback
	4. Nothing needed for the server URL
13. Click Create.
14. This will generate a Client ID and Client Secret.
15. You should download the JSON file for later reference as you will need these variables in your frontend and backend.

## Add Google Authentication to the Frontend

1. Set up your frontend repository. 
2. Make an .env file.
	1. This should be in the main folder of your project where package.json is.
	2. Name it just .env.
	3. Add this to your .env file

```
VUE_APP_CLIENT_ID = 'your-google-client-id'  
VUE_APP_CLIENT_URL = 'http://localhost:8081'  
VUE_APP_API_URL = 'https://accounts.google.com/gsi/client'
```

4. You can find your Google Client ID by opening the .json file you downloaded earlier when setting up your client or by going to the [Google Developer Console](https://console.developers.google.com/)

5. Make sure that your [.gitignore](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/.gitignore) file includes .env so that the .env file will never be pushed to your GitHub repository
	1. We don’t want sensitive information like this in a public online repository.
	2. We will instead make secrets on GitHub so that this information is secure.
    

3. Make secrets in your GitHub repository.
    

1. You will need four secrets in your frontend repository
    

1. SERVER_SSH_KEY
    

1. Like you did for the last project
    

3. VUE_APP_API_URL
    
4. VUE_APP_CLIENT_ID
    

1. Make sure you don’t put this in quotes in GitHub – Google doesn’t like that for some reason.
    

6. VUE_APP_CLIENT_URL
    

  

![Graphical user interface, application
Description automatically generated](https://lh6.googleusercontent.com/9cPtJKk5pvNnpzrHsGnWWAP8EfjxKlVERsVZIIuZ8Gg_kuM6QfmCE13TGper9KYUv-E9p3H1KiFc5O3Cm5gDJ6aNf6By7J-F8QdrSBP9LUGkTP014G0ZrSFCdDwWjkeqe44iJYSzVrXFuKMU6QqDGA)

  

4. Add the Google API script to [public/index.html](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/public/index.html).
    

  

<script src="https://accounts.google.com/gsi/client" ></script>

  

5. Add login button and function to login screen.
    

1. See example in the [SocialLogin.vue](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/components/SocialLogin.vue) component.
    
2. You will need to add a div with an id to the html section of your code so that Google can render the button in the location you want it to be.
    
3. You will need a login function that gives information to Google.
    
4. You will need a handleCredentialResponse function that allows the Google object to access your code globally. 
    
5. This component is imported into the actual [Login](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/views/Login.vue) screen. You can do that or just have everything in your own login screen.
    

7. Make a Utils object that will handle your store.
    

1. See example in the [config/utils.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/config/utils.js) file.
    
2. You can import this object across different files in your project to get the store.
    
3. We will set the store as soon as a user is authenticated and logged in.
    

9. Make a store so that you can access user data locally.
    

1. See example in the [store/store.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/store/store.js) file.
    
2. This will allow you to have a store to access globally across your project.
    

11. Add the store to your [main.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/main.js) file.
    

1. Again, this will help you to access your store globally.
    

13. Send your token whenever you make a request in your [services.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/services/services.js) file.
    

1. Your services.js file may be called http-common.js.
    
2. This will allow for us to do extra authorization in our backend, which means we can restrict users on which requests they are allowed to send, etc.
    
3. You can also have this file check the response to see if you need to automatically log out a user.
    

1. Be sure that when you log out a user, you clear out the store.
    
2. An example of logging out is also in the [MenuBar.vue](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/components/MenuBar.vue) component.
    

15. Add routes for authentication requests. 
    

1. Create a  [services/authServices.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/services/authServices.js) file.
    
2.  You will need routes to go from the frontend to your backend login and logout services.
    

17. Set up your [vue-deploy.yml](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/.github/workflows/vue-deploy.yml) file so that the AWS server gets the secrets from GitHub.
    
18. Fix your [package.json](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/package.json) file.
    

1. We want to make sure that the bundle command in the script section says 
    

“mv .env dist”

**

## Add Google Authentication to the Backend

