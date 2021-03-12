# Build and Deploy

Go to firebase console > project > hosting:

1. Grab the firebase cli install snippet: `npm install -g firebase-tools` and install globally on machine

2. To access and use the cli we need to login to firebase from the project directory `firebase login`

3. Initialise the project `firebase init` 

4. Build the project ready to deploy. This process bundles the build and puts it in the public `dist` folder ready for deployment. `npm run build`

5. Deploy the project `firebase deploy`

Once deployed all the information including live links to the app are in the firebase console and the app can also be given a custom domain. 

**Note**: Any time we make changes to the project we need to `re-build` and `re-deploy` 