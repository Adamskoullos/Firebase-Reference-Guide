# Firebase Reference Guide

Toc:

[Setting Up](#Setting-Up)<br>
[Firestore](#https://github.com/Adamskoullos/Firebase-Reference-Guide/blob/master/firestore/firestore.md)<br>
[Cloud Functions]()<br>
[Authentication]()<br>
[Rules](#)<br>
[Hosting](#)<br>

----------------------------------------

# Setting Up

Each project requires the firebase package for the frontend, and a firebase `web app` for the backend.  We join the two using the firebase api key:   

## Install Firebase package for the front end

`npm install firebase`

The firebase package is installed within the node_modules folder and gives us access to import any of the firebase services

## Configuration Object

1. Create a firebase `web app` for the project.  This is done from the firebase project overview page

2. Go to the new `we app` settings and copy the firebase SDK snippet `config` to add to the front end

3. Create new folder inside `src` called firebase, and then create a `config.js` file to copy the SDK snippet to

4. Import the core firebase package at the top of the `config.js` file: `import firebase from 'firebase/app'` 

5. Then underneath, Import any specific services: `import 'firebase/firestore'`

6. Initialise firebase below the config snippet, passing in the config object: `firebase.initializeApp(firebaseConfig)`

7. Initialise any services: `const projFirestore = firebase.firestore()`

8. Export any firebase services so we can connect to them and connect to the firebase backend from within the front end: `export { projFirestore }` 