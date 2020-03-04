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
  - "functions" folder is the backend
  - "public" folder is the frontend
  - "firebase.json" is the firebase config file

## Testing a GET request:
- Go to functions/index.js
- Replace with GET request handler

```
const functions = require('firebase-functions');
const express = require('express');

const app = express();

app.get('/timestamp', (request, response) => {
  response.send(`${Date.now()}`);
});

exports.app = functions.https.onRequest(app);
```

- Go to firebase.json file in root of project
- Add a rewrite to handle URL requests (note the `exports.`**`app`** above matches the `"function": "`**`app`**`"`)

```
"rewrites": [{
  "source": "/timestamp",
  "function": "app"
}]
```
