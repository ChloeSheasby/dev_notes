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
	1. If you are using Vue 3 with Vite, you'll have to name this with VITE instead of VUE i.e. `VITE_APP_API_URL`.
```
VUE_APP_CLIENT_ID = 'your-google-client-id'  
VUE_APP_CLIENT_URL = 'http://localhost:8081'  
VUE_APP_API_URL = 'https://accounts.google.com/gsi/client'
```

3. You can find your Google Client ID by opening the .json file you downloaded earlier when setting up your client or by going to the [Google Developer Console](https://console.developers.google.com/)

4. Make sure that your [.gitignore](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/.gitignore) file includes .env so that the .env file will never be pushed to your GitHub repository
	1. We don’t want sensitive information like this in a public online repository.
	2. We will instead make secrets on GitHub so that this information is secure.
5. Make secrets in your GitHub repository.
	1. You will need four secrets in your frontend repository
```
SERVER_SSH_KEY
VUE_APP_API_URL
VUE_APP_CLIENT_ID
VUE_APP_CLIENT_URL
```

6. Add the Google API script to [public/index.html](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/public/index.html).
```
<script src="https://accounts.google.com/gsi/client" ></script>
```

7. Add login button and function to login screen.
	1. See example in the [SocialLogin.vue](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/components/SocialLogin.vue) component.
	2. You will need to add a div with an id to the html section of your code so that Google can render the button in the location you want it to be.
	3. You will need a login function that gives information to Google.
	4. You will need a handleCredentialResponse function that allows the Google object to access your code globally. 
	5. This component is imported into the actual [Login](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/views/Login.vue) screen. You can do that or just have everything in your own login screen.
8. Make a Utils object that will handle your store.
	1. See example in the [config/utils.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/config/utils.js) file.
	2. You can import this object across different files in your project to get the store.
	3. We will set the store as soon as a user is authenticated and logged in.
9. Make a store so that you can access user data locally.
	1. See example in the [store/store.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/store/store.js) file.
	2. This will allow you to have a store to access globally across your project.
	3. Think about using [Pinia](https://pinia.vuejs.org/) as a store instead.
10. Add the store to your [main.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/main.js) file.
	1. Again, this will help you to access your store globally.
11. Send your token whenever you make a request in your [services.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/services/services.js) file.
	1. This will allow for us to do extra authorization in our backend, which means we can restrict users on which requests they are allowed to send, etc.
	2. You can also have this file check the response to see if you need to automatically log out a user.
		1. Be sure that when you log out a user, you clear out the store.
		2. An example of logging out is also in the [MenuBar.vue](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/components/MenuBar.vue) component.
12. Add routes for authentication requests. 
	1. Create a  [services/authServices.js](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/src/services/authServices.js) file.
	2.  You will need routes to go from the frontend to your backend login and logout services.
13. Set up your [vue-deploy.yml](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/.github/workflows/vue-deploy.yml) file so that the AWS server gets the secrets from GitHub.
14. Fix your [package.json](https://github.com/OC-ComputerScience/tutorial-frontend-vue2/blob/dev/package.json) file.
	1. We want to make sure that the bundle command in the script section says `mv .env dist`

## Add Google Authentication to the Backend


1. Set up your backend repository.
2. Make an .env file.

```
CLIENT_ID = "your-google-client-id"  
CLIENT_SECRET = "your-google-client-secret"  
DB_HOST = "localhost"  
DB_PW = ""  
DB_USER = "root"  
DB_NAME = "your-database-name"
```

3. You can find your Google Client ID and Google Client Secret by opening the .json file you downloaded earlier when setting up your client or by going to the [Google Developer Console](https://console.developers.google.com/).
4. Make sure that your [.gitignore](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/.gitignore) file includes .env so that the .env file will never be pushed to your GitHub repository.
    

1. We don’t want sensitive information like this in a public online repository
    
2. We will instead make secrets on GitHub so that this information is secure
    

3. Make secrets in your GitHub repository.
    

1. You will need seven secrets in your frontend repository
    

1. SERVER_SSH_KEY
    

1. Like you did for the last project
    

3. AWS_DB_HOST
    
4. AWS_DB_NAME
    
5. AWS_DB_PW
    
6. AWS_DB_USER
    
7. CLIENT_ID
    
8. CLIENT_SECRET
    

3. The four AWS variables will be the host, name, password, and user for the database information on your AWS server.
    

  

![Graphical user interface, application, Teams
Description automatically generated](https://lh3.googleusercontent.com/ScjZDwF-2VUH1vrNg_vkGeXuC1zgJIE1Hf-5lx6Ks4Svbgg8vSphgtAH2a6pTv9s9azj3eJpGaq4D0dy9xYL7qK1VO7csViimzK-_3fh1XLi0LS4cBgXDOuuMtlyygNtWao2QxlkzZ1GqnIAT2Y9cw)

  

4. Fix your db.config.js file.
    

1. See example in the [config/db.config.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/config/db.config.js) file.
    
2. We want this config file to now get data from the .env file instead of hardcoding it.
    

6. Create a user table.
    

1. See examples in the [user.model.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/models/user.model.js), [user.controller.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/controllers/user.controller.js), and [user.routes.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/routes/user.routes.js) files.
    

8. Create a session table.
    

1. See example in the [session.model.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/models/session.model.js) file.
    
2. You don’t need a routes or controller file for the session table.
    

10. Create an auth.config.js file.
    

1. See example in the [config/auth.config.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/config/auth.config.js) file.
    
2. This will help us create a JSON web token later.
    

12. Create login and logout functions.
    

1. See example in the [auth.controller.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/controllers/auth.controller.js) file.
    
2. This is where a user will be authenticated through Google and where we will add users to the user table.
    
3. This is also where we will add sessions to the sessions table and create a JSON web token for each session.
    
4. After a user has been created or found, and a session has been created, we will send whatever information we want to be saved to the frontend.
    
5. When the frontend receives that information, it saves it to the store.
    

14. Create routes to the login and logout functions.
    

1. See example in the [auth.routes.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/routes/auth.routes.js) file.
    
2. You do not need any of the authorization code. That only applies if you are integrating something like the Google calendar API.
    

16. Create an authorization.js file.
    

1. See example in the [authorization/authorization.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/authorization/authorization.js) file.
    
2. This will help us limit users to not be able to send requests if their session has timed out.
    
3. You can use this same idea to limit different roles from accessing different requests.
    

18. Add authorization to all routes.
    

1. See example in the [tutorial.routes.js](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/app/routes/tutorial.routes.js) file.
    
2. We want all our routes, besides login and logout, to require the session to be authorized before we send the request.
    

20. Add a service file.
    

1. See example in the [tutorial-backend.service](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/tutorial-backend.service) file.
    

22. Set up your [node-deploy.yml](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/.github/workflows/node-deploy.yml) so that the AWS server gets the secrets from GitHub, including the different variables for the AWS database.
    
23. Fix your [package.json](https://github.com/OC-ComputerScience/tutorial-backend/blob/dev/package.json) file.
    

1. We want to make sure that the bundle command in the script section makes sure that all parts of the backend are pushed to AWS, including our service file and our .env file.
    
2. Yes, we want our .env file on the AWS server.
    



**