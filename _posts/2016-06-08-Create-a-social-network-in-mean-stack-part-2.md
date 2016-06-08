---
layout: posts
category: socialnetwork
title: "Create a social network using MEAN stack - Part 2"
comments: true
excerpt: "In part 2 of the series I will start by creating a repository and the basic file structure for the application"
date: 2016-06-08
---

Hey guys , this is second part of my tutorial series . In this part I will start by creating a repository for my app followed by the file structure.By the way I decided to do a [Youtube](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) video series for this set of tutorials , so if you have doubts or something is not clear after reading the blog , you can head over to my [Youtube Channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) and watch the videos related to this blog . So without further delay , lets get started.

Head over to [Github](https://github.com/) or [Bitbucket](https://bitbucket.org/)  and create a new repository.Once the repository is created clone it to your local machine.If you have doubts regarding creating repos , take a look at my video or google some nice set of git tutorials.

Once cloned , open the project folder in your favorite ide , and start creating this file structure in your root directory of the project.

```
project
|---Readme.md
|---License
|
|------app/
|       |---controllers/
|       |---routes/
|       |---models/
|       |---services/
|
|-----config/
|
|-----public/
|       |---img/
|       |---css/
|       |---templates/
|       |---lib/
|       |---js/
|           |---controllers/
|           |---routes/
|           |---factory/
|
|-----uploads/
```

Now the directories are created , notice I have only created directories , `/` at end of all directories , I will start creating the files in next tutorials. Now let me explain what all these directories will contain.

Starting from top the `app` directory will contain all server side stuff, where all the logic of our backend will be stored in `controllers` , while all the database models will be stored in `models` . The `routes` folder will contain all our **rest api** and server side routing and `services` will contain different services. The `config` folder will hold our configuration files , for example :- api keys of different external services , token secrets , (It will start making sense once we start coding). The `uploads` folder will contain all media files which user uploads , for example the profile picture .

The `public` folder will contain all our frontend side of code including html, css, and JavaScript. `img` will contain images , `css` will contain css , `templates` will contain all html files . `lib` will contain all external libraries which we will use for our app , like angular or bootstrap or some material design libraries. As I said in last post , I will be using angular , which uses controllers, routes and factory , that explains the presence of `controllers` , `routes` and `factory` folders.

```js
var express = require('express'); var path = require('path'); var logger = require('morgan'); var cookieParser = require('cookie-parser'); var bodyParser = require('body-parser');

var app = express();

app.set('port', process.env.PORT || 3000); app.use(logger('dev')); app.use(bodyParser.json()); app.use(bodyParser.urlencoded()); app.use(cookieParser()); app.use(express.static(path.join(dirname, 'public')));

app.listen(app.get('port'), function() { console.log('Express server listening on port ' + app.get('port')); });

```

Thats it for this post , in the next post i will start the app by writing a simple Hello World!!! program. Check out my [Youtube Channel](https://www.youtube.com/channel/UC5qMKRZgKizuz9JtztFijHQ) , where I will be posting videos related to every posts I publish here.For comments , questions , and feedback send me an [email](mailto:me@rishabh1403.com) or leave a comment below . Thanks, Happy Coding !!!
