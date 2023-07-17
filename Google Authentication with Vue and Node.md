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
15. You should download the JSON file for later reference You will need these variables in your frontend and backend.
    

  

![Graphical user interface, application, Teams
Description automatically generated](https://lh3.googleusercontent.com/mHFbjZE7fN650rTvJYweqLL1FOQXUt0qGcedGEPHDC135F-gqP06O0RpOR-i_rzmyBt82J0S-Do9qNhWaNZpVCLi6v6ex1-2uT7DzA-fhdRojoIgBfUhGY7wzBn99Gi5hjT0nlou3Cb6Sr7m_kBYlQ)

  
**

## Add Google Authentication to the Frontend

## Add Google Authentication to the Backend

