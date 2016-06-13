---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 4"
comments: true
excerpt: "In this post we will start with adding angular to our app"
date: 2016-06-13
---

Hello everyone , in this post we will start adding angular to frontend of our app . Please try to grasp as much as you can from this post , I will be explaining concepts of controller and two-way data binding in this post , which are very important concepts . So lets get started .

First of all you will need to include angularjs script to your html , so go ahead to this [link](https://code.angularjs.org/1.5.6/angular.min.js) , copy everything . create a new file in public/lib named ```angular.min.js``` and paste everything in it . Save and close the file.
Next thing we need to do is include this in our **index.html** , so open your **index.html** and write this code just above the ending body tag.


```html

<script type="text/javascript" src="lib/angular.min.js"></script>

```
Now create two files , first in ```public/js``` named ```app.js``` and second in ```public/js/controllers``` named ```appController.js``` .
Description :- ```app.js``` is the main angular file , here we will define that the app is an angular app and give it a name.

Next ```appController.js```  is the main controller for our app , which means that this file will contain codes which will control the flow of data in our app . There can be many controllers in an app , we will be creating a lot of them as we go along , controllers can also be nested , for more information visit [angularjs documentation on controllers](https://docs.angularjs.org/guide/controller).
In our ```app.js``` write the following code

```js

(function () {
    angular.module('socialnetwork',[]);
}());

```

Line 2 creates an angular app with name **socialnetwork**.The function wrapping it just makes sure that we leave no global variables , that is , we don't pollute the global name space. The function calls it self . The empty array states the list of dependencies of our angluar app.
In ```appController.js``` add the following code.


```js

(function(){
    angular.module('socialnetwork').controller('appCtrl',['$scope',function($scope){

    }]);
}());

```
The wrapping function serves same purpose here , the code in between defines a *controller* for the app . The array here states dependency for this controller , here I have listed a dependency **$scope** , which is basically used to bind the view (html) to the controller . There is a function in the array , all our controller logic will go inside this function , we are listing the dependency here too , because when we minify our file the variables in function arguments gets  converted to some other  shorter variables , which will break our program.That is the reason we are supplying our dependencies in the array before the function .
Now we will add these file to our **index.html** , and attach the angular module and the controller to our app.
So go ahead and add scripts to index.html.

```html

<script src="js/app.js"></script>
<script src="js/controllers/appController.js"></script>

```

**Make sure these scripts are below angular.js and in the order , first app.js then appController.js.**
Now in the html tag of the html file add

```html

<html ng-app="socialNetwork" ng-controller="appCtrl">

```
This binds the angular module to our view and assigns the controller to everything inside html tags.
Now to make sure that everything is setup correctly , in place of hello world in html file replce it with {{hello}} and in appController.js in the function add
```js

$scope.hello = "hello angular";

```
All done , now start the server , go to the link in web browser , you must see Hello Angular instead of Hello world . If You got it right go ahead and read the description on how it works , if not , please post your doubts in comments section below.
Description :- $scope binds a variable with a value and we can access this in our view using {{ }} . We just have to use the same name here.

That is it for this tutorial folks !!!. Next tutorial is going to be a long one , I Will start with client side routing and create pages for Authentication . Subscribe to my blog and [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) to find out when new posts come out. Again if you have any doubts , you can see video regarding to this post .For comments , questions , and feedback send me an [email](mailto:me@rishabh1403.com) or leave a comment below . Thanks, Happy Coding !!!
