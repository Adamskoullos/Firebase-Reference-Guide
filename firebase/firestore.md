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

# Creating a new document

## Adding a document to the database from the front end

First within the async function we create an object for the new document and save it to a const. We then create a resolve const and assign it the returned value of the await request. The request starts by targeting the firestore collection, then adding `.add(obj)` to the end passing in the object to create the new database document from.  Make sure to hit enter when typing the firestore service `fStore` so Vue adds the import to the file:

![Screenshot from 2021-03-08 02-02-15](https://user-images.githubusercontent.com/73107656/110264928-5280a180-7fb2-11eb-9be5-472e9ea5492c.png)

![Screenshot from 2021-03-08 01-46-24](https://user-images.githubusercontent.com/73107656/110263979-1c422280-7fb0-11eb-8837-2bfde2fcdfd8.png)

# Deleting a document

1. Add a button with a click event listener on the view we want to make the delete from, in this instance it will be the individual post view for a blog post

![Screenshot from 2021-03-08 02-27-21](https://user-images.githubusercontent.com/73107656/110266494-d38d6800-7fb5-11eb-9e56-614aa97687b2.png)

2. Define the function within the `setup()` function

- Make the function `async`
- target the firestore collection, then the post by `id` within the firestore collection using `await` and add `delete()` to the end
    - Note here that we can target the id by either `props.id` as we have it or as we have imported and saved `useRoute` to `route` we can use `route.params.id` which i have done here
- Re-route the user back to the home view in this case the main blog page. We use the vue-router for this so we need to:
    - Save the router to a const `const router = useRouter()`
    - auto import `useRouter` as we do this
    - Use the `router.push()` method to redirect the user

4. Add the function to the `setup()` function returned object so the template has access to it

![Screenshot from 2021-03-08 02-41-25](https://user-images.githubusercontent.com/73107656/110267475-cb362c80-7fb7-11eb-9cd2-92ea91b71a52.png)

# TimeStamp - Adding a 'created at' timestamp to each document

Firebase has a timestamp data type that can be used as a field value within a document, just like booleans, strings etc.  To get access to the data type we have to set it up within the `config.js` file, run the firebase timestamp method and save the returned function so we can use it as a `field value` to grab the timestamp for each document when they are created:

1. `config.js` - Initialise the firebase timestamp data type and save it to a const:

![Screenshot from 2021-03-08 04-05-59](https://user-images.githubusercontent.com/73107656/110273051-9e881200-7fc3-11eb-82ae-167ce423aac7.png)

Above, the `serverTimestamp` returns a function that is used as the field value

2. Add the `timestamp()` function as the value to the `createdAt` document property within the function that creates new documents and sends them to the db:

![Screenshot from 2021-03-08 04-14-37](https://user-images.githubusercontent.com/73107656/110273583-d04da880-7fc4-11eb-903b-4e5fba9b1903.png)

![Screenshot from 2021-03-08 04-15-14](https://user-images.githubusercontent.com/73107656/110273640-e8252c80-7fc4-11eb-8543-2bc8b8252a96.png)

Now we have a timestamp for each document, we can organise them in date order (ascending or descending)

