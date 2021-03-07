# GET request 

**GET request pattern using firestore**

We are importing into the file we make the request from:

1. Import firestore: `import { fStore } from '../firebase/config'` We are importing from the firebase folder within the `src` folder on the front end

Within the `try` of the async request function:

2. Make a connection to the firestore collection `posts`, get the collections object and save it to a const:

`const res = await fStore.collection('posts').get()`

3. Get the data and add it to the front end `posts` array:

So far we have grabbed the collection object for `posts`, to get access to the array of documents we use `res.docs` and to grab each docs data (title, body, tags) we use `doc.data()`. The document `id` is not within the document data, it is on the document, so we have to grab that separately with `doc.id`.  We return an object and spread `doc.data()` and `doc.id` into it.  This is the whole getPosts composable but the pattern is within the `try`:

![Screenshot from 2021-03-07 04-37-43](https://user-images.githubusercontent.com/73107656/110229135-27894580-7eff-11eb-9c9d-b2ecff488316.png)


