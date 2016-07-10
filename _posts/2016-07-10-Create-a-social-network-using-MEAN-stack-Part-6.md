---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 6"
comments: true
excerpt: "In this post we will start with mongoDB . We will create a database and establish connection to the db ."
date: 2016-07-10
---

Hello everyone , in this post we will start with mongoDB . We will create a database and establish connection to the db . Before getting started just make sure you have mongoDB installed and running on your system. Lets get started .

First of all we will need some libraries on the server side so lets install those first.Head over to the project root directory in your terminal and type ``` npm install --save mongoose body-parser serve-favicon ``` . You already know what this command does from our previous post . Here we are installing 3 libraries . Mongoose is a helper library , it helps us to establish connection to our db. Body-parser is used to parse data that we send from our client to our server , it may be form data or other json data. Serve-favicon is used to serve the favicon for our website , the tiny little icon in our website title . Once the installation is complete , we are ready to move forward.

Now we have to specify which database or url to the db which we will be using in our app, so create a file ```db.js``` in config folder and add the following code to it.

```js

module.exports={
    url : "mongodb://localhost/socialnetwork"
}

```
This is a simple file which specifies the url of our db which we will make connection to , what ```module.exports``` does is , it allows us to access its properties ( here 'url') anywhere in our app after requiring this file. I will just clear this up in a minute.Now we will connect our app to db at this url , so open your ```server.js``` and replace everything with the following code below

```js

var express = require('express');
var app = express();
var bodyParser = require('body-parser');
var mongoose = require('mongoose');
var serveFavicon = require('serve-favicon');

var db = require('./config/db');
mongoose.connect(db.url);
mongoose.connection.on('connected',function () {
    console.log("connnection established");
})

app.use(bodyParser.urlencoded({ extended: true }))

app.use(bodyParser.json())

app.use(express.static('public'));

require('./app/routes/auth')(app);
app.listen(3000,function (err) {
    console.log("server is running at http://localhost:3000");
});

```

There are some additions and changes from its previous versions , we required all three libraries that we installed , pretty simple till there :wink: , then we are requiring the ```db.js``` that we just created and assigning it to a variable **db** now all the properties that are **exported** in ```db.js``` can be accessed in this file by using **dot** operator. In the next line we are calling connect function of mongoose and passing our db url which it has to connect to. In the next line we are listening for events ( there are some pre-defined events ) . Here we are listening for connection event , i.e. as the connection is established log a message in terminal . Next two lines are for body-parser configuration. In one we are allowing to parse url parameters and in other we are allowing to parse json data. There is a change in app.listen function , here we are providing a callback function which show a nice message when starts successfully . Skip the ```require ``` thing just before the listen function , I will explain that after I create api routes for the authentication. So create a file called ```auth.js``` in your ```ap/routes directory ``` and paste the following code .

```js

var authCtrl = require('../controllers/authController');

module.exports=function (app) {
    app.post('/api/auth/register',authCtrl.register);
    app.post('/api/auth/login',authCtrl.login);
}

```

In the first line we are requiring a controller , but we don't have that yet , so what do we do ? , create one :wink: . Go to your ```app/controllers``` directory and create a file named ```authController.js``` and paste the following code.

```js

module.exports.register=function (req,res) {
    console.log("register data" , req.body);
    res.send("data received");
}
module.exports.login = function (req,res) {
    console.log("login data" , req.body);
    res.send("data received");
}

```
Now all the server side files we needed are created , lets put the pieces together and try to understand how all this works.

In the ```authController``` we are exposing two functions **register** and **login** , so any file which requires this file can access these functions . Now what do they do ? . Both function takes two parameters , **req** and **res** i.e. request and response. The request is the original user request that the client creates and response is the answer the server will send for that request. In both function we are printing the contents of our request body to the console. and then we are sending a response that the data is received . It is important that every request should send a response . You can send HTTP status codes , a html file , simple strings , or json data as response.

Now we are requiring this file in our routes , so we can use the two functions in that file. There we are again exposing a function which takes a parameter ```app``` the same instance of our express. Next we are creating two routes , post is a http verb , there are many http verbs , example post , get , put , delete , we are passing in two things , first is the route at which the request has to be made , second is the function which will handle the request , the same function which we created in our controllers .

And at last we are requiring this file in ```server.js``` and passing the ```app``` instance so that it can access the pre-defined methods. To summarize , a user requests login api , request comes to server , server searches for that route , it is found in the ```auth.js``` route file , request goes there , it looks for the function that will handle this request the request goes to the ```authController.js``` , there the body of request is logged in console and a response is sent . Now we have to call these rest apis from our frontend and check that everything is working.

Head over to our client login and register controllers and replace everything with following code respectively .

```js

(function () {
    angular.module('socialNetwork').controller('loginCtrl',['$scope','$http',function($scope,$http){
        $scope.loginForm = {
            "email" : "",
            "username" : "",
            "password" :""
        }
        $scope.login = function (data) {
            console.log(data);
            $http.post('/api/auth/login',data).success(function (response) {
                console.log(response);
            }).error(function (err) {
                console.log(err);
            })
        }
    }]);
}());

```

And

```js

(function () {
    angular.module('socialNetwork').controller('registerCtrl',['$scope','$http',function($scope,$http){

        $scope.registerForm = {
            "email" : "",
            "username" : "",
            "password" :""
        }
        $scope.register = function (data) {
            console.log(data);
            $http.post('/api/auth/register',data).success(function (response) {
                console.log(response);
            }).error(function (err) {
                console.log(err);
            })
        }
    }]);
}());

```


The ```register``` and ```login``` function has changed in both the controllers , they are similar so I will explain just one of them . Lets look into register controller . We are injecting a new dependency ```$http``` like we injected ```$scope``` . It is used to make requests to the server . Here we are requesting the register api that we created in our server file , the **post** here should be same as declared in our server , and we are passing the data we recieved from our form to the server . This data will be sent as ```req.body``` and then there are two callbacks **success** and **error** as name suggests , they will run if the server request was successful or not respectively . In both the functions we are logging the response to the console. everything is set up , now start your server by ```nodemon server.js``` and fill login or register forms and hit submit , you should see the entered values in your terminal i.e. just printing out the request body and in browser console you should be seeing a message ***data received*** .
If you get any error or have doubts watch my video of this post below , or on my [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) .

<input type="checkbox"> Every Thing works as expected ? Subscribe to my Blog and [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) :wink: <br />

<div class="ytVidContainer">
<iframe class="ytVid" src="https://www.youtube.com/embed/Hw2nN78SBkc" frameborder="0" allowfullscreen></iframe>
</div>
<br />

That is it for this tutorial folks !!!. In the next part I will start with create user model and register our user into the database . Subscribe to my blog and [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) to find out when new posts come out. Again if you have any doubts , you can see video regarding to this post .For comments , questions , and feedback send me an [email](mailto:me@rishabh1403.com) or leave a comment below . Thanks, Happy Coding !!!
