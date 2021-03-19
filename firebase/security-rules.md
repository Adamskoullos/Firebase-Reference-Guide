# Rules set-up

Firebase rules can be set within the firebase console or within a `firebase.rules` file within the root of the project.

We will do this within a `firestore.rule` file:

1. create file in the root of the project

2. firebase console > project > cloud firestore > rules: copy the default rules and paste within the `firestore.rules` file as a starting point

- Custom these rules to fit the project

3. Now update the `firebase.json` file to include an object for the `firestore.rules` file.  **Note**: This is automatic when when we initialise firebase from the start of the project

![Screenshot from 2021-03-12 07-26-41](https://user-images.githubusercontent.com/73107656/110906791-5d199e80-8304-11eb-9fe2-3019576fc6de.png)

4. Deploy just the changes and update the back end and live project:

- `firebase deploy --only firestore:rules`


# Requiring Authentication

The below example shows the pattern to only allow read and write access if the user is logged in:

![Screenshot from 2021-03-12 07-37-39](https://user-images.githubusercontent.com/73107656/110907806-d8c81b00-8305-11eb-85f3-8fb16658e510.png)


# Locking the API key to a domain

To do this sign into `console.developers.google.com` select the firebase project > credentials > API key:

Click on the API key and scroll down, click on `HTTP refers (website)` and then add the firebase domain:

![Screenshot from 2021-03-12 07-50-06](https://user-images.githubusercontent.com/73107656/110909094-956eac00-8307-11eb-812a-e29100a4c325.png)

Now only read and write requests made from this domain are accepted by firebase.