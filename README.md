# Firebase NodeJS starter project commands 

Simple file listing the commands to quickly set up a Firebase starter project. 

## Creating a new firebase project:
`mkdir project-name`

`cd project-name`

`npm i -g firebase-tools`

`firebase init hosting`

`firebase init functions`

`cd functions`

`npm install express --save`

`cd ..`

`code .`

## Project structure:
  - "functions" folder is the backend.
  - "public" folder is the frontend.
  - "firebase.json" is the firebase config file.

## Testing a GET request:
- Go to functions/index.js.
- Replace with GET request handler.

```
const functions = require('firebase-functions');
const express = require('express');

const app = express();

app.get('/timestamp', (request, response) => {
  response.send(`${Date.now()}`);
});

exports.app = functions.https.onRequest(app);
```

- Go to firebase.json file in root of project.
- Add a rewrite to handle URL requests (**note:** the **app** export in the above code `exports.app` has to match the **app** in the snippet below `"function": "app"`).

```
"rewrites": [{
  "source": "/timestamp",
  "function": "app"
}]
```

- Launch projet locally with the following command:

`firebase serve --only functions,hosting`

- Go to http://localhost:5000/timestamp.


## Adding advanced features:
### Caching
To add caching with ExpressJS, simply add this line of code in an API request:

`response.set('Cache-Control', 'public, max-age=300, s-maxage=600');`

**Parameter 1 - Cache-Control:** Activates cache with header of response

**Parameter 2 - Cache-Control values:** 
- **public:** Enables cache content on server. If it was private, we could only cache in user's browser. 
- **max-age=300:** How long we can store this content in the user's browser in seconds (300 seconds in this example). 
- **s-maxage=600:** How long we can store this on the CDN in seconds (600 seconds in this example). 