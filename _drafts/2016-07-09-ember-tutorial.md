---
layout:     post
title:      Learn Ember!
date:       2016-07-09
summary:    After a spending my summer learning how to do Ember, I would love to share this knowledge with everyone else!
categories: Ember js tutorial
---

### Table of contents
{:.no_toc}
* Table of contents placeholder
{:toc}

## Preface

Welcome to our first segment to learning Ember.js (or for the time being, we will refer to as just Ember)! I have been spending the entire summer working on a project using Ember from the bottom up. **Now note**, I did not know Ember going into the summer, but here I am giving you a tutorial from __my__ learning path and understanding. This will have been through many reviews and revisions from the community and friends to make sure it is accurate as possible!

There are two main reasons why I decided on writing this piece for everyone. The first was for myself. I wanted to practice my writing chops and it is important as I continue to bring out content that people wish to see and implement feedback I am given! Second reason is a good tutorial is hard to come by. When I was finding out how to really use Ember, I had to sift through content that was back from 1.X and how their API actually changed quite a bit to the now 2.X (specifically, 2.6.2 at the time of writing this). Also, for a newbie like myself, the official tutorial did seem a bit more complicated and I needed a bit better explanation of what is going on.

So enough chatter, let's get you all setup!

## Prerequisites
So, before we continue, there are a few pre-requisite pieces of software we are going to need. You are going to need to have two package managers installed: [NodeJS](https://nodejs.org/en/download/) and [Bower](https://bower.io/#install-bower) (in that order).

With [NodeJS](https://nodejs.org/en/download/), it makes life a lot easier to get your appropriate installer if you do not understand how to do it yourself. Once installed, you get an additional software built on top called, [Node Package Manager](https://www.npmjs.com/) or better known as [npm](https://www.npmjs.com/). With that, you will be able to actually go into a Terminal window and simply download [Bower](https://bower.io/#install-bower) through a simple run like so:

```bash
$ npm install -g bower
```

Ember is a solution to the front-end and with it, additional software is needed to get the appropriate results. In order for us to develop, test and share, we will be using packages that Open Source Community has developed to make our lives easier rather than having to reinvent the wheel. For instance, if we want to add [Bootstrap](http://getbootstrap.com/) to our project, it is easier to go through the package manager than to figure out where to store the file. Along with that, if we are trying to share our project with others, it allows for us to enforce what packages are needed along with their versions.

Now that we have the tools, time for us to do the magic installation of Ember!

## Installation
Now that we have the two things we need, the installation is a small command like Bower, instead it is:

```bash
$ npm install -g ember-cli
$ npm install -g phantomjs
```

Now, you might be wondering, "Prince, you said we were learning Ember! What the heck is `ember-cli`?" Well, I will tell you inquisitive reader! Ember is a framework that exists, while [ember-cli](https://ember-cli.com/) is a command line utility that makes writing Ember apps quicker as it generates the necessary files for you through different commands.

And the second thing we are installing is called [PhantomJS](http://phantomjs.org/) which is a tool that may be required or recommended for our testing purposes.

With all the prerequisites and installation requirements, we are finally ready to truly dive into writing some Ember!

## Starting the Project

### Getting a new Project
Whenever we want to start a new Ember project, we can just navigate to a location in which we want to build our app. The command for starting a new Ember app is: `ember new <app_name>`. So if we want to call our project `trevor`, we can do this:

(Name inspired by [Kevin Lewis](https://twitter.com/_phzn))

```bash
$ ember new trevor
```

We will see our project build and several things being created and installed through npm:

```bash
$ ember new trevor
installing app
  create .bowerrc
  create .editorconfig
  create .ember-cli
  create .jshintrc
  create .travis.yml
  create .watchmanconfig
  create README.md
  create app/app.js
  create app/components/.gitkeep
  create app/controllers/.gitkeep
  create app/helpers/.gitkeep
  create app/index.html
  create app/models/.gitkeep
  create app/resolver.js
  create app/router.js
  create app/routes/.gitkeep
  create app/styles/app.css
  create app/templates/components/.gitkeep
  create bower.json
  create config/environment.js
  create ember-cli-build.js
  create .gitignore
  create package.json
  create public/crossdomain.xml
  create public/robots.txt
  create testem.js
  create tests/.jshintrc
  create tests/helpers/destroy-app.js
  create tests/helpers/module-for-acceptance.js
  create tests/helpers/resolver.js
  create tests/helpers/start-app.js
  create tests/index.html
  create tests/integration/.gitkeep
  create tests/test-helper.js
  create tests/unit/.gitkeep
  create vendor/.gitkeep
Successfully initialized git.
⠙ Installing packages for tooling via npm
```

This may or may not take a bit depending on your system so just be slightly patient for the initial configuration.

And then eventually it will change the installing to:

```bash
Installed packages for tooling via npm.
Installed browser packages via Bower.
```

Ta-da! We made it through! *Wasn't that painless?*

<br>

Let's change into that directory and talk a bit about what has happened and what we are looking at.

```bash
$ cd trevor
```

Once inside of the directory, we actually can go ahead and start up a server and have it already working out of the box!

To run an Ember Server all you have to do is:

```bash
$ ember server
```

And then it will launch up and you will see this [amazing screen]()

### Directory Structure

**Aside**: Now like I said, when I was learning Ember, things were a bit of a challenge for me because I came in and didn't quite understand everything that was going on. Instead of overwhelming you with a bunch of technical jargon, we are going to do most of our talk simply on the `app/` for the time being as that is the main piece we will be interacting with. We will get to the other stuff in other tutorials but I want you to be able to say, "Hey, I built an Ember project today and understand how Ember flows! Someone give me a high five!" You go excited reader \***high five**\*!

When looking inside of that folder, we can see these:

```bash
├── app.js
├── components
├── controllers
├── helpers
├── index.html
├── models
├── resolver.js
├── router.js
├── routes
├── styles
│   └── app.css
└── templates
    └── components
```

Now no need to fear, each of these lovely folders/files are going to be our navigators through the ways of Ember. With the ember-cli solution, whenever we generate a new item into our project, they will find their way into its appropriate folder. So let's generate our first feature, a component!
