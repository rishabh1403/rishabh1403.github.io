---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 3"
comments: true
excerpt: "In this part we will write a simple hello world program"
date: 2016-06-09
---

Hey guys this is part 3 of the tutorial series . In this part we will write a simple hello world program . Lets get started.

Head over to project root directory in terminal and run ```npm init``` command . This will ask you a series of questions , you can just keep pressing enter and leave the fields default or empty , at last it will confirm if the contents are correct , just press enter. As this command runs completely , you will see a ```package.json``` file in your root directory .

A ```package.json``` file contains meta data of the app or project . Most importantly it stores the dependencies of the app , that is , the external libraries on which the app depends. All libraries we use must be mentioned here. Next step is to install ```ExpressJs``` , which is a framework for nodejs . It is very useful in creating apis very quickly.
Run ```npm install express --save``` in your project root directory. This will create a folder named ```node_modules``` , where the libraries will be stored . The ```--save``` here allows us to mention the dependency in our ```package.json``` without manually mentioning it. Its very important that we use ```--save``` when installing dependencies for our application.

Now we have everything installed for now , lets code !!!. Create a file named ```server.js``` in project root directory and a file named ```index.html``` in public directory.Write the following code in your ```server.js```

```js
var express = require('express');
var app = express();
app.use(express.static('public'));
app.listen(3000);
```
and following in ```index.html```

```html 

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Hello World app</title>
    </head>
    <body>

        Hello World!!!

    </body>
</html>
```

Now make sure you are in your project root directory , run ```node server.js``` in your terminal window , and head over to ```http://localhost:3000/``` . Did you see the hello world in your browser ? If yes , then go ahead and read the description below about how this works , if not , then read the post again and try to find the fault . If you are unable to find the fault , please post your issue in comments , and I will reply ASAP .

Now how does this code works ? Looking at the server code , first we are requiring the installed library , it is basically telling the system that we will be using that library in this file , in next line we are creating an instance of express , so that we can use its predefined methods. In the third line we are using a **middleware** , recognized by  ```app.use()``` .**Middleware** is basically a set of actions from which program control flow , ```express.static('public')``` refers that express should look for static files in public directory . ```app.listen(3000)``` starts a simple web server at port 3000 . So now if anyone visits the link ```http://localhost:3000/``` , the server actually tries to find ```index.html``` , since it is a static file and , its declared that static files will reside in public folder , so server tries to find ```index.html``` in public folder and serves that file to the web browser . Thus our Hello World is rendered on the screen.

Thats it for this post folks!!!.You can also refer to my video on my [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ),it will have the same name as blog .  In the next post I will add angular to our code , explain little bit about controllers ,and how to make a http get request from frontend , and send response for that request from our server. For comments , questions , and feedback send me an [email](mailto:me@rishabh1403.com) or leave a comment below . Thanks, Happy Coding !!!
