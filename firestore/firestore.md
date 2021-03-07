# Fetch request (Grabbing a whole collection) 

**Fetch request pattern using firestore**

We are importing into the file we make the request from:

1. Import firestore: `import { fStore } from '../firebase/config'` We are importing from the firebase folder within the `src` folder on the front end

Within the `try` of the async request function:

2. Make a connection to the firestore collection `posts`, get the collections object and save it to a const:

`const res = await fStore.collection('posts').get()`

3. Get the data and add it to the front end `posts` array:

So far we have grabbed the collection object for `posts`, to get access to the array of documents we use `res.docs` and to grab each docs data (title, body, tags) we use `doc.data()`. The document `id` is not within the document data, it is on the document, so we have to grab that separately with `doc.id`.  We return an object and spread `doc.data()` and assign `doc.id` to id.  This is the whole getPosts composable but the pattern is within the `try`:

![Screenshot from 2021-03-07 04-37-43](https://user-images.githubusercontent.com/73107656/110229135-27894580-7eff-11eb-9c9d-b2ecff488316.png)

# Fetch request (Grabbing a single document)

Similar to grabbing the whole collection, the pattern for grabbing a single post also sits within the `try` block.

We have access to the post id as it is passed into the `getPost` function, we add `.doc(id)` before `.get()` in the `const res`.  This allows us to connect to the posts collection, grab the post document that matches the id. We do not need to use map as we are not cycling through an array, we just need to assign an object to `post.value` and spread in the data `res.data()` and add `id: res.id`. This time we also utilise the `exists` property on the document object which returns a boolean to throw an error if the post does not exist. Here is the pattern:

![Screenshot from 2021-03-07 05-56-08](https://user-images.githubusercontent.com/73107656/110230571-d6328380-7f09-11eb-88d7-5e6a0dfedf48.png)

