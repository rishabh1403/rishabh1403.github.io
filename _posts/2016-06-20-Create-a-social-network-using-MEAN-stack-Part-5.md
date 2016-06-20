---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 5"
comments: true
excerpt: "In this post we will create routes for our authentication pages and create a simple register and login page"
date: 2016-06-20
---

Hello everyone , in this post we will start adding routes to our app , create authentication pages and create simple login form. From this post onward we will be writing a lot more code than we used to , so i will just write all the codes and explain them. Lets get started .

First of all what is *routing* ? In basic terms routes are different states of our website . Like if we go to our homepage then it is a state and its route is **/** . If we go to **homepage/login** , it means we want to go to login page , so login view will be rendered in the browser.In our post we will be using **ui-router library** , which is an awesome library for routing in angularjs . Routing can be done either via server or client . If it is done via server , the browser request an url , server sends the response i.e. the html or view and it gets rendered on the browser . In the client side routing , only the part of a page which need to change is requested and it is rendered . For example , say you are on your homepage and you have a top navigation and your info . Now you want to go to messages page , in that page navigation bar does not change , so your browser will request server for the data which is changing and is rendered.In this case page refresh does not take place and we can save a lot of bandwidth and give user a nice experience. Enough talk now time to code!!!. First go to [this link](http://angular-ui.github.io/ui-router/release/angular-ui-router.min.js) and get the file for ui-router. Copy everything , create a file called ```uirouter.min.js``` in your lib folder paste everything and close the file .

- [ ] Done ? Move forward  :wink: .

You can also look at their [documentation](https://github.com/angular-ui/ui-router) , it is pretty self explaining but i will be explaining things as we go along . Second thing , we need to add this as dependency . This is an external library and our angular app is depending on it , so add this in our main ```app.js``` located in ```public/js/ folder```

```js

(function () {
    angular.module('socialNetwork',['ui.router']);
}());

```


- [ ] Added ui-router as dependency ? Move Forward :wink:

Now that we have our library set up , lets start writing our routes i.e. when user requests homepage what should we show them , when user requests login , what should be show them .
Go ahead and create a file named ```homeRoutes.js``` in your ```public/js/routes/``` folder.
Add this set of code to your file and save .

```js

(function () {
    angular.module('socialNetwork').config(['$stateProvider','$urlRouterProvider',function ($stateProvider, $urlRouterProvider) {

        $stateProvider
            .state('home',{
                url:'',
                templateUrl:'templates/home.html',
                controller:'homeCtrl'
            })
            .state('login',{
                url:'/login',
                templateUrl:'templates/login.html',
                controller:'loginCtrl'
            })
            .state('register',{
                url:'/register',
                templateUrl:'templates/register.html',
                controller:'registerCtrl'
            })

        $urlRouterProvider.otherwise('/');
    }])
}());

```


- [ ] Code included ? Move Forward :wink:

**Explanation** :- there is an opening anonymous function like we used in controller , to prevent pollution of global name space . Next is our angular module , it defines that this configuration is of our socialNetwork module, then there is an array just controllers , to prevent code from breaking during minification  . The config method takes 2 arguments *$stateProvider* and *$urlRouterProvider* . Next we start writing our routes . *$stateProvider.state* is just the syntax to specify our state , it takes a name i.e. state name and a JSON object with 3 properties , *url* , *templateUrl* , *controller* . Url is the address on which this state is activated , templateUrl is the path to view which has to be rendered and controller is the name of controller which is to be attached to that view . Simple enough .

- [ ] Understood a little ? Good, move forward :wink:

There are other ways you can pass this properties , but i like this one , so yeah , lets go ahead with it .Now there are three states as you can see are used in the code , First one has url **''** , i.e. when user requests the homepage , templateUrl says render the file named ```home.html``` which is in **templates** folder under **public** . Controller just says that attach *homeCtrl* to that view.
Rest of the two works same way.The last part is providing an otherwise link i.e. when user requests a link which is not in any of the states , so in that case go to the the link in otherwise , in our app it is the root home url.

- [ ] Understood everything ? Move Forward :wink:

Now you may notice that we do not have these three html files mentioned in our routes , neither are the controllers , so how will the browser render the page ? It will not , so what do we do ? Simple ... We create those files , so go ahead create three html files in **templates** folder and three controllers in **js/controllers** folder.

**home.html**

```html

{{home}}

<a ui-sref="login">login</a>
<a ui-sref="register">register</a>

```

**login.html**

```html

<div>
    Email:-
    <input type="email" ng-model="loginForm.email">
    Username :-
    <input type="text" ng-model="loginForm.username">
    Password:-
    <input type="text" ng-model="loginForm.password">
    <button type="button" name="button" ng-click="login(loginForm)">login</button>

    <a ui-sref="register">register</a>

</div>

```

**register.html**

```html

<div>
    Email:-
    <input type="email" ng-model="registerForm.email">
    Username :-
    <input type="text" ng-model="registerForm.username">
    Password:-
    <input type="text" ng-model="registerForm.password">
    <button type="button" name="button" ng-click="register(registerForm)">register</button>

    <a ui-sref="login">login</a>

</div>

```

**homeController.js**

```js

(function () {
    angular.module('socialNetwork').controller('homeCtrl',['$scope',function($scope){
        $scope.home = "hello home";


    }]);
}());

```

**loginController.js**

```js

(function () {
    angular.module('socialNetwork').controller('loginCtrl',['$scope',function($scope){
        $scope.loginForm = {
            "email" : "",
            "username" : "",
            "password" :""
        }
        $scope.login = function (data) {
            console.log(data);
        }
    }]);
}());

```

**registerController.js**

```js

(function () {
    angular.module('socialNetwork').controller('registerCtrl',['$scope',function($scope){

        $scope.registerForm = {
            "email" : "",
            "username" : "",
            "password" :""
        }
        $scope.register = function (data) {
            console.log(data);
        }
    }]);
}());

```


- [ ] Created files ? Well March ahead :zap:   

Now Just one more thing , we need to add the routes file and other controller in our ```index.html``` . Go ahead and add the controllers and routes to the file , notice the change in body in the file

```html

<!DOCTYPE html>
<html ng-app="socialNetwork" ng-controller="appCtrl">
    <head>
        <meta charset="utf-8">
        <title>hello world</title>
    </head>
    <body>
        {{hello}}
        <div ui-view>

        </div>

        <script type="text/javascript" src="lib/angular.min.js"></script>
        <script src="lib/uirouter.min.js" charset="utf-8"></script>
        <script src="js/app.js" charset="utf-8"></script>
        <script src="js/routes/homeRoutes.js" charset="utf-8"></script>
        <script src="js/controllers/appController.js" charset="utf-8"></script>
        <script src="js/controllers/homeController.js" charset="utf-8"></script>
        <script src="js/controllers/loginController.js" charset="utf-8"></script>
        <script src="js/controllers/registerController.js" charset="utf-8"></script>
    </body>
</html>

```


- [ ] Made all the changes ? You are halfway ... keep reading :relaxed:

The div with **ui-view** directive is where the routes render the views , the files home,login,register will be rendered there.
Moving forward to home.html , it is pretty simple , a simple home variable , just to check if our controller is properly attached to view , it has two links , notice in the links we are not using *href* , instead we are using **ui-sref** , this allows us to just pass in the state name and it will work same as an href . How this helps ? Lets take an example , lets say you have a long link ```a/b/c/d/e.html``` and the state name is **stateE** , so instead of using that long name , you can just use the state name in **ui-sref** . Makes Sense ? . *homeController* is also straight forward , just a simple controller with a scope variable .
Next is login and register pages and controllers . I will explain Just one , because both are almost same .

- [ ] Easy till now ? No? Give it a shot again ... Yes ? Move ahead :relieved:

There are three input fields , *email* , *username* and *password* , ( i will change password field from text to password later ).
All of then has **ng-model** directive with some value , ng-model basically binds whatever we write in the input field to the variable which is the value , for example , email we type will be stored in **loginForm.email** . Why using the long variable name instead of just email ? well we can use any name and access that in our controller by $scope , but it is better to store form data in a *JSON* , it is easier to just send one variable instead of ten , if we have ten input fields in our form . If you don't know what a JSON is , please google a bit , next in the submit button , we have a **ng-click** directive which specifies what should be done if the button is clicked . In our case call login Method and pass *loginForm* as an argument . Since loginForm has all the values ,our forms complete data is passed. In The Controller we created a login method , notice it is attached with $scope which is  the reason we can access it in our view, any general method is not accessible in the view , the method is simple right now , just logs the value of the received data in our browser.

- [ ] Understood the code ? Move ahead

Before checking the code please install **nodemon** on your system , you have to restart node server every time you change some file , this will be handled automatically by nodemon .
type ``` sudo npm install -g nodemon ``` in your terminal window , and start server by ```nodemon server.js``` instead of ```node server.js```
Go ahead start the server , open the webpage and you should see your homepage with **hello angular** and **hello home**. Click the links ,notice there is no page refresh , fill the forms check browser console, If you get any error or have doubts watch my video of this post below , or on my [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) .

- [ ] Every Thing works as expected ? Subscribe to my Blog and [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) :wink:

<div class="ytVidContainer">
<iframe class="ytVid" src="https://www.youtube.com/embed/6_2m4aqV_qg" frameborder="0" allowfullscreen></iframe>
</div>
<br />

That is it for this tutorial folks !!!. In the next part I will start with mongoDB,mongoose, create user model and if time permits register and login our user . Subscribe to my blog and [Youtube  channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) to find out when new posts come out. Again if you have any doubts , you can see video regarding to this post .For comments , questions , and feedback send me an [email](mailto:me@rishabh1403.com) or leave a comment below . Thanks, Happy Coding !!!
