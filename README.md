Setting Up a Simple Node.js Application for Cloud Foundry
1.Create a new directory (folder) on your local file system:
mkdir node-tutorial

2.Open the node-tutorial folder in Visual Studio Code.

3.Create a manifest.yml file with the following content:
yaml
---
applications:
- name: myapp
  
  random-route: true

  path: myapp

  memory: 128M

  buildpacks:

  - nodejs_buildpack

4.Create a subfolder myapp inside the node-tutorial folder.

5.Navigate to the myapp directory and initialize npm:

cd myapp

npm init

6.Install Express as a dependency:

    
    npm install express --save

7.Update the package.json file:

json

{

  "name": "myapp",
  
  "version": "1.0.0",
  
  "description": "My simple Node.js app",
  
  "main": "index.js",
  
  "engines": {
  
    "node": "16.x.x"
  
  },
  
  "scripts": {
  
    "start": "node start.js"
  
  },
  
  "author": "",
  
  "license": "ISC",
  
  "dependencies": {
  
    "express": "^4.18.2"
  
  }

}


8.Create a file start.js inside the myapp folder with the following content:

javascript code

const express = require('express');

const app = express();

app.get('/', function (req, res) {

  res.send('Hello World!');

});

const port = process.env.PORT || 3000;

app.listen(port, function () {

  console.log('myapp listening on port ' + port);

});


9.Deploy the application on Cloud Foundry:


perl

cf push


Make sure to execute cf push in the node-tutorial directory where the manifest.yml file is located.

