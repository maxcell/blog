---
layout:     post
title:      Learn Ember!
date:       2016-07-09
summary:    After spending my summer learning how to use Ember, I wanted to share the basics with those who are interested! Here is a brief tutorial that will get you started with installing Ember, generating a project, and creating a few routes & components.
categories: ember js tutorial
excerpt: <p>Welcome to our first segment to learning Ember.js (or for the time being, we will refer to as just Ember)! I have been spending the entire summer working on a project using Ember from the bottom up.
comments: true

---

### Table of contents
{:.no_toc}
* Table of contents placeholder
{:toc}


## Preface

Welcome to our first segment to learning Ember.js (or for the time being, we will refer to as just Ember)! For part of my internship, I have had to use Ember as part of our solution to the front-end. **Now note**, I did not know Ember going into the summer, but here I am giving you a tutorial from __my__ learning path and understanding. This will have been through many reviews and revisions from the community and friends for accuracy.

There are two main reasons why I decided on writing this piece. The first was for myself. I wanted to practice my writing chops. It's valuable as I continue to write pieces people want to see and implement the feedback I am given! Second reason is a good tutorial is hard to come by. When I was finding out how to really use Ember, I had to sift through content that was back from 1.X and noticed their API actually changed quite a bit since the now 2.X (specifically, 2.6.2 at the time of writing this). For people like myself, the official tutorial did seem a bit more complicated and I needed a bit better explanation of what was going on.

So enough chatter, let's get you all setup!

## Prerequisites
So, before we continue, there are a few pre-requisite pieces of software we are going to need. First, you MUST have [Git](https://git-scm.com/downloads) installed. Git is a popular distributed version control software which if you are not familiar with, definitely read up on it!

You are going to need to have two package managers installed: [Node Package Manager (or better known as npm)](https://nodejs.org/en/download/) and [Bower](https://bower.io/#install-bower) (in that order). [NodeJS](https://nodejs.org/en/download/) makes life a lot less hectic to install npm if you do not understand how to use a Terminal. Once installed, you get [npm](https://www.npmjs.com/) alongside it. Now, you will be able to actually go into a Terminal window and download [Bower](https://bower.io/#install-bower) through a small command like so:

```bash
$ npm install -g bower
```

Ember is a solution to the front-end and with it, additional software is needed to get the appropriate results. We will be using packages that Open Source Community has developed to make our lives easier rather than having to reinvent the wheel. These package managers help us greatly with developing, testing, and sharing our projects. For instance, if we want to add [Bootstrap](http://getbootstrap.com/) to our project, it is easier to go through a package manager than to figure out where to store the file. The package manager knows where it should install it and how to reference it within the project. Whenever we finally want to Open Source our project, others can actually copy down the project, install what packages they need without having to ever ask us. It is all recorded with the help of special files that the package managers understand.

Now that we have the tools, time for us to do the magic installation of Ember!

## Installation
The installation is a small command like installing Bower was, but instead it looks something like this:

```bash
npm install -g ember-cli
npm install -g phantomjs
```

Now, you might be wondering, "Prince, you said we were learning Ember! What the heck is `ember-cli`?" Well, I will tell you inquisitive reader! Ember is a front-end framework that exists, while [ember-cli](https://ember-cli.com/) is a command line utility that makes writing Ember apps quicker as it generates the necessary files for you through different commands. So rather than having to build each file out from hand, we have `ember-cli` to ease out that process. We are still going to be writing Ember code no matter what, this just helps predefine a project structure that you will see with all Ember apps. Check out what [Discourse](https://github.com/discourse/discourse/tree/master/app/assets/javascripts/discourse) used to look like before it made some changes into its Rails code. This is just one of the many platforms that utilizes Ember.

The second thing we are installing is called [PhantomJS](http://phantomjs.org/) which is a tool that is recommended for our testing purposes. We won't be writing any tests in this tutorial, but in future ones we will go all over why [TDD](http://agiledata.org/essays/tdd.html) is the bees knees.

With all the prerequisites and installation requirements met, we are finally ready to truly dive into writing some Ember!

## Starting the Project

### Getting a new Project
Whenever we want to start a new Ember project, we will open up a Terminal window and navigate to where we want to start our project. The command for starting a new Ember app is: `ember new <app_name>`. So if we want to call our project `trevor`, we can do this:

(Name inspired by [Kevin Lewis](https://twitter.com/_phzn))

```bash
$ ember new trevor
```

There is no real significance to the name `trevor`. This app will just be our playground to do cool things with.

We will see our project build and several things being created & installed through npm:

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
  ...         # Trimmed down all created files but there are more
  create vendor/.gitkeep
Successfully initialized git.
⠙ Installing packages for tooling via npm
```

This may or may not take a bit depending on your system so just be slightly patient for the initial configuration.

Once it is all complete, you will see it now change from installing to:

```bash
Installed packages for tooling via npm.
Installed browser packages via Bower.
```

Ta-da! We made it through! *Wasn't that painless?*

<br>

Let's change into our new project and talk a bit about what has happened and what we are looking at.

```bash
$ cd trevor
```

Once inside of the project, we actually can go ahead and start up a server and have it already working out of the box!

To run an Ember Server all you have to do is:

```bash
$ ember server
```

And then it will begin our local server. When you head over to [localhost:4200/](localhost:4200/), you will see this amazing screen:
![Ember Initial Server without any routes]({{ site.baseurl }}/assets/img/new_build.png)

### Directory Structure

**Aside**: When I was learning Ember, things were a bit of a challenge for me because I came in and didn't quite understand everything that was going on. Instead of overwhelming you with a bunch of technical jargon, we are going to do most of our talk simply on the `app/` for the time being as that is the main piece we will be interacting with. We will get to the other stuff in other tutorials but I want you to be able to say, "Hey, I built an Ember project today and understand how Ember flows! Someone give me a high five!" You go excited reader \***high five**\*!

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

Now no need to fear, each of these lovely folders/files are going to be our navigators through the ways of Ember. With `ember-cli`, whenever we generate a new item into our project, they will find their way into its appropriate folder.

So let's generate our first feature, a route!

## Routes
Routes are our little pathways throughout our application. You all use them daily but you might not realize what they are. So let's start off with generating three, just to see what I am talking about.

```bash
$ ember generate route application
installing route
  create app/routes/application.js
  create app/templates/application.hbs
installing route-test
  create tests/unit/routes/application-test.js

$ ember g route index # g is shorthand for generate
installing route
  create app/routes/index.js
  create app/templates/index.hbs
installing route-test
  create tests/unit/routes/index-test.js

$ ember g route about
installing route
  create app/routes/about.js
  create app/templates/about.hbs
installing route-test
  create tests/unit/routes/about-test.js
```

To understand what is going, we are going to deconstruct our commands. With all of them, we are saying, "`ember-cli` can you generate me a route named **\<route-name\>**?" And `ember-cli` will respond with, "Sure homeslice, here are some files you are going to need and I hope you use them well!" `ember-cli` knows we are going to need our `<route-name>.hbs` (our main files for writing what will appear to the user) for our templates, so it adds that within our `templates/`. It also knows we might need to do some logic behind the scenes, that's what we will see in our `routes/` folder. Even though you would think *all* your files would be found there, these files handle behind-the-scenes logic, such as actions and models (we will speak more about models later in this tutorial) and puts them as `<route-name>.js`. And finally, `ember-cli` wants you to be able to write your tests because **tests are important**. Tests allow for you to determine if your code works as you *believe* it does versus just making an assumption.

### Application Route

A quick second to explain the significance of the application route. The application route is the largest influencing route you can generate. If you take a look inside of the `app/templates/application.hbs` file, you will notice all it has is:

{% highlight html %}
{% raw %}
{{outlet}}
{% endraw %}
{% endhighlight %}

Even though all routes generate like this, the `application.hbs` file shows markup that will be found on every page within our application. The `{%raw%}{{outlet}}{%endraw%}` is content that is deferred to our router. So in layman's terms it means that depending on what page we are on, that page's content will render in place of the `{%raw%}{{outlet}}{%endraw%}`.

Let's learn by example, go ahead and add the name of your app as a part of the navigation on the `application.hbs` file like so:
{% highlight html %}
{% raw %}
<nav>Trevor</nav>
{{outlet}}
{% endraw %}
{% endhighlight %}

And you should be seeing something like this so far:
![Content on the Application route]({{site.baseurl}}/assets/img/nav_trevor.png)

### Index Route
You won't quite see what has happened yet till we add some content within `index.hbs` and `about.hs`. So let's do some more changes in these files!

Inside of our `index.hbs` replace everything with:

```html
<div style="text-align:center">
  <h3>Welcome to Trevor</h3>
  <p>The cool and hip new application written by this amazing developer.</p>
</div>
```

When we head over to [localhost:4200/](localhost:4200/) again, we will see:
![Content on the index route]({{site.baseurl}}/assets/img/index_adding_content.png)

### About Route

For this route, tell your user something about yourself in `about.hbs`. For instance:

```html
<div style="text-align:center">
  <h3>About the Developer</h3>
  <p>Name: Prince Wilson</p>
  <p>GitHub: maxcell</p>
  <p>Twitter: maxcellw</p>
  <p>Favorite Animal: Corgi</p>
</div>
```

Now, this will not be in the same location as the other two files we have seen. We actually head over to [localhost:4200/about](localhost:4200/about) to see our changes which brings up:
![Content on the About Route]({{site.baseurl}}/assets/img/about_adding_content.png)


Congratulations you made your first set of routes in Ember! When we switch between [localhost:4200/](localhost:4200/) and [localhost:4200/about](localhost:4200/about), we can see how the `application.hbs` continues to follow us around even though we are rendering different routes.

This is great. Now let's also take a small look into what the model hook is and how we can leverage components!

## Model Hook

Inside of any of our `<route-name.js>`, we can add a function called `model`. This is understood in Ember as [the model hook](https://guides.emberjs.com/v2.6.0/tutorial/model-hook/). It acts as **hook** which really means Ember can call upon it at different times within our app. The model hook is typically used for us to return data from our backend or database. But we will just hardcode JSON inside of it for this tutorial.

Let's say we want to have our `index` page to have a list of all the projects we have done. Now we can manually put all of our content of that into our `index.hbs` making it static, or we can leverage the power of our model hook and make it a bit more dynamic so that way we don't have to change the contents each time in `index.hbs` or any other files that will need to display the same information.

Taking a look inside of `routes/index.js`, we are going add some code to change:

```js
import Ember from 'ember';

export default Ember.Route.extend({
});
```

To:

```js
import Ember from 'ember';

let projects = [{
    id: 1,
    name: "Foo",
    date: "January",
    software: ["JavaScript", "Ruby on Rails"],
    about: "An amazing application that is totally used by everyone for everything."
}, {
    id: 2,
    name: "Bar",
    date: "February",
    software: ["JavaScript", "Swift", "Java"],
    about: "The application that makes other applications wish they were better."
}, {
    id: 3,
    name: "FizzBuzz",
    date: "March",
    software: ["Haskell"],
    about: "The classic problem in the best functional language there is around."
}];

export default Ember.Route.extend({
  model() {
    return projects;
  }
});
```

Now this will not show any physical changes yet. However, if we do some changes within our `index.hbs`, you can see the effect that the model has:

{% highlight html %}
{% raw %}
<div style="text-align:center">
  <h3>Welcome to Trevor</h3>
  <p>The cool and hip new application written by this amazing developer.</p>
</div>

<h4>Projects</h4>
{{#each model as |project|}}
  <p>{{project.name}} - {{project.date}}</p>
  {{#each project.software as |tool| }}
    <li>
      {{tool}}
    </li>
  {{/each}}
  <p>{{project.about}}</p>
{{/each}}

{% endraw %}
{% endhighlight %}

Look at this amazing thing of ours!

![Add Project content to Index Route]({{site.baseurl}}/assets/img/index_adding_projects.png)

This will cause our page to load with a list of projects. `{%raw%}{{#each model as |project|}}{%endraw%}` allows for us to take the data that is passed within our model hook and iterate through each object or record. We also don't want to just call everything `model`, especially since each route could have a different model coming in, so we try to describe it with something meaningful to developers such as `|project|`. The `{%raw%}{{}}{%endraw%}` (moustache braces or curly braces) are part of the [Handlebars templating library](http://handlebarsjs.com/) and allow us to do the Ember portions of our code within our `.hbs` files.

To expand on this slightly, we can even begin to make a component out of our logic from above!

## Components
Components have been becoming more and more popular across the many web front-end frameworks and Ember is no exception. When we see we are doing things over and over, we realize we need to utilize the [DRY principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), a.k.a. Don't Repeat Yourself. In the case of our project list, it would make more sense to turn this into a component so that way we declutter our `index.hbs` and have a bit more meaningful piece of code.

### Adding a New Component

By strict convention, `ember-cli` requires all components to have a hyphenated name, this is due to avoiding any future HTML tags being overwritten (isn't that smart?). So let's call our first component `project-item`. Remember how before we generated our routes? Can you guess how we generate components?

```bash
$ ember g component project-item
installing component
  create app/components/project-item.js
  create app/templates/components/project-item.hbs
installing component-test
  create tests/integration/components/project-item-test.js
```

We want to take all the stuff we are already doing for each project and push that content withLet's take a look at what our component will look like in the `templates/components/project-item.hbs` file:

{% highlight html %}
{%raw%}
<li>{{project.name}} - {{project.date}}</li>
<ul>
  {{#each project.software as |tool| }}
    <li>{{tool}}</li>
  {{/each}}
</ul>
<p>{{project.about}}</p>
{%endraw%}
{% endhighlight %}

Because of us making a component, we want to change some behind-the-scenes logic too. Going over to `components/project-item.js`, we want to add in a `tagName`.

```js
import Ember from 'ember';

export default Ember.Component.extend({
  tagName: 'ul'
});
```

### Rewriting your Route

By default, each component is covered with the `<div>` tags. Since we want to be using `<li>`, it makes sense for us to surround them with the `<ul>` tags and `tagName: 'ul'` allows for us to change it. We are also going to change our `index.hbs` to look more like this:

{% highlight html %}
{% raw %}
<div style="text-align:center">
  <h3>Welcome to Trevor</h3>
  <p>The cool and hip new application written by this amazing developer.</p>
</div>

<h4>Projects</h4>
{{#each model as |curr-project|}}
  {{project-item project=curr-project}}
{{/each}}

{% endraw %}
{% endhighlight %}

When we want to refer to our component we will use our {%raw%}{{component-name}}{%endraw%}. Along with that, you may have noticed now we have this `project=curr-project`. `project` is a property of our component and whenever we feed anything into it, it will take in that data and refer to its template (`templates/component/project-item.hbs`) and figure out if and where it needs to be rendered.

So what's happened? We moved out all of our code from within the `{%raw%}{{#each}}{%endraw%}` block and put in its place `{%raw%}{{project-item project=curr-project}}{%endraw%}`. Notice we changed `project` to `curr-project` and when we use our component we feed it into the `project` property. Once we have done that, we have this amazing look now!

![New Index route]({{site.baseurl}}/assets/img/index_add_component.png)

## Congratulations

You really did make your first Ember app! It uses `ember-cli`, has a few routes and has its very own component involved with it! You learned a bit on how the model hook works and you learned on how to feed that into a component. You are
official a [Tomster](http://emberjs.com/tomster/)! Go forth and show the world your powerful abilities. I hope you learned a bunch and you found this a good stepping stone into the world of Ember!
