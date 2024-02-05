Here I am going to create a simple Node.js application.

In your local file system, create a new directory (folder). For example: node-tutorial

From your Visual Studio Code, open the node-tutorial folder.

In this folder, create a file manifest.yml with the following content:

<h1>YAMLCopy</h1>
---
applications:
- name: myapp
  random-route: true
  path: myapp
  memory: 128M
  buildpacks:
  - nodejs_buildpack
The manifest.yml file represents the configuration describing your application and how it will be deployed to Cloud Foundry.

IMPORTANT: Make sure you don’t have another application with the name myapp in your space! If you do, use a different name and adjust the whole tutorial according to it.

Inside node-tutorial, create a subfolder myapp.

In the myapp directory, execute:

Bash/ShellCopy
npm init
Press Enter on every step. This process will walk you through creating a package.json file in the myapp folder.

Then, still in the myapp directory, execute:

Bash/ShellCopy
npm install express --save
This operation adds the express package as a dependency in the package.json file.

After the installation is completed, the content of package.json should look like this:

JSONCopy
{
  "name": "myapp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2"
  }
}
Add engines to the package.json file and update the scripts section. Your package.json file should look like this:

JSONCopy
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
Inside the myapp folder, create a file start.js with the following content:

<h1>JavaScriptCopy</h1>

const express = require('express');
const app = express();
app.get('/', function (req, res) {
  res.send('Hello World!');
});
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('myapp listening on port ' + port);
});
This creates a simple web application returning a Hello World! message when requested. The express module represents the web server part of this application. Once these steps are completed, you can see that the express package has been installed in the node_modules folder.

Deploy the application on Cloud Foundry. To do that, in the node-tutorial directory, execute:

Bash/ShellCopy
cf push
Make sure you always execute cf push in the directory where the manifest.yml file is located! In this case, that’s node-tutorial.

