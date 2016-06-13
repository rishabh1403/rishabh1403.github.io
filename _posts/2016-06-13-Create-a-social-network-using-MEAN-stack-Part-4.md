---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 4"
comments: true
excerpt: "In this post we will start with adding angular to our app"
date: 2016-06-13
---

Hello everyone , in this post we will start adding angular to frontend of our app . Please try to grasp as much you can from this post , I will be explaining concepts of controller and two-way data binding in this post , which are very important concepts . So lets get started .

First of all you will need to include angularjs script to your html , so go ahead to this link , copy everything . create a new file in public/lib named angular.min.js and paste everything in it . Save and close the file.
Next thing we need to do is include this in our index.html , so open your index.html and write this code just above the ending body tag.
Now create two files , first in public/js named app.js and second in public/js/controllers named appController.js .
Description :- app.js is the main angular file , here we will define that the app is an angular app and give it a name .
appController.js is the main controller for our app , which means that this file will contain codes which will control the flow of data in our app . There can be many controllers in an app , we will be creating a lot of them as we go along , controllers can also be nested , for more information visit angularjs documentation on controllers.
In our app.js write the following code

```js

(function () {
    angular.module('socialnetwork',[]);
}());
```

Line 2 creates an angular app with name socialnetwork.
POST in progress.
