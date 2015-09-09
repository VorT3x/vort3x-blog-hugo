+++
date = "2015-05-19T00:14:33+03:00"
draft = false
title = "Sails.js on Heroku"
tags = ["Nodejs", "Sailsjs", "Heroku"]
+++

How to deploy your [Sails.js](http://sailsjs.org) application to [Heroku](http://www.heroku.com).

![Sailsjs logo](/images/sailsjs-logo.png)

First of all **What is Sails.js**? Per [sailsjs.org](sailsjs.org):

> Sails makes it easy to build custom, enterprise-grade Node.js apps. It is designed to emulate the familiar MVC pattern of frameworks like Ruby on Rails, but with support for the requirements of modern apps: data-driven APIs with a scalable, service-oriented architecture. It's especially good for building chat, realtime dashboards, or multiplayer games; but you can use it for any web application project - top to bottom.

You can find more detailed information on how to create Sails.js application on their website: http://sailsjs.org/#!/getStarted

![Heroku logo](/images/heroku-logo.jpg)

Heroku is a cloud platform as a service (PaaS). Heroku can build, deploy and run your Ruby, Node.js, Python, Java and PHP applications and it's great platform for production and development environments.

---

Sails.js deployment to Heroku
=============================

We will need to create Heroku application first, then configure Sails.js application and deploy it from command shell using Git.

Prerequisites:
--------------

-	Sails.js application
-	[Git](http://git-scm.com)
-	[Heroku account](https://signup.heroku.com/login)
-	[Heroku Toolbelt](https://toolbelt.heroku.com) installed (CLI tool for creating and managing Heroku apps)

Create Heroku application
-------------------------

First, you need to login into Heroku from your command shell

```
$ heroku login
```

You'll need to enter you email address and password.

```
Enter your Heroku credentials.
Email: user@email.com
Password (typing will be hidden):
```

Create Heroku application:

```
$ heroku create name-of-the-app-on-heroku
```

Next, create Procfile in your Sails.js application's folder.

```bash
$ cd path/to/sailjs-project
$ touch Procfile
```

Now open Procfile with your text editor (or vim/nano) and add `web: npm start`

In your Sails.js application you should have `package.json` file, open it and find scripts block then set start value with `sails lift`:

```javascript
"scripts": {
  "start": "sails lift",
  "debug": "node debug app.js"
},
```

Create a new Git repository in your Sails.js application's directory:

```bash
$ git init
$ heroku git:remote -a name-of-the-app-on-heroku
```

Commit your code to the repository and deploy it:

```bash
$ git add .
$ git commit -m "Added my Sails.js project"
$ git push heroku master
```

You should wait until you get this message:

```bash
remote: -----> Launching... done, v3
remote:        https://name-of-the-app-on-heroku.herokuapp.com/ deployed to Heroku
```

Congratulations! Now you can check your application by this URL: `https://name-of-the-app-on-heroku.herokuapp.com`

To re-deploy your application, you'll need to commit your changes and push to Heroku:

```bash
$ cd path/to/sailjs-project
$ git add .
$ git commit -m "New changes"
$ git push heroku master
```

Feel free to ask me any questions in the comments below.
