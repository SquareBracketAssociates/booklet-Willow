## Introducing Willow

![Willow logo](figures/willow.png width=30&anchor=fig)


### What does Willow do? / How does it help me?

Imagine you want to create a web application.
No matter your development language of choice for the server, you will need to create HTML files for the frond-end, maybe choose a front-end framework like [https://getbootstrap.com](https://getbootstrap.com) or [https://materializecss.com](https://materializecss.com) to get the foundation of the visual style, add some CSS files to complete the user interface, and most likely write a great deal of Javascript to make it work in the way you expect.

This means at least 3 different languages, plus your server code, each potentially requiring a different way to work with the files. 
But what if you could just express all of it in the same way? 
Maybe try one front-end framework, then another, without changing more than a line of code?
The same vocabulary, used for the web components, for the interaction protocol, and for styling the user interface. *That is what Willow does.*


Now I guess you are an expert developer and have memorized most of the protocol for all of these languages, and never have issues with code completion, finding examples in your own code for some common feature, nor refactoring HTML, CSS and JS components. In my case however, I prefer to have a comfortable development environment, that helps me create and configure the web components, define the interaction (before, during and after the server calls), and also integrate itself with the same tools I use for Test Driven Development, Version Control and Continuous Integration. That is why I use Willow when developing interactive web applications.

### How can I use it in my project?
The first thing you need is to get a Smalltalk environment. Willow is developed using Pharo, so you will always find the latest version there. You can also contact Mercap Software to ask for the VA Smalltalk port.
To get the core components, you would open a workspace and evaluate:

```
Metacello new
  baseline: 'Willow';
  repository: 'github://ba-st/Willow:v14/source';
  load
```

Normally, you will also want to load one of the related Willow projects to add support for a specific front-end framework (instead of just plain HTML5).
To get Bootstrap 3 support, you must load Willow-Bootstrap by evaluating:

```
Metacello new
  baseline: 'WillowBootstrap';
  repository: 'github://ba-st/Willow-Bootstrap:v13/source';
  load
```
To get JQuery UI support, you must load Willow-JQueryUI by evaluating:


```
Metacello new
  baseline: 'WillowJQueryUI';
  repository: 'github://ba-st/Willow-JQueryUI:v12/source';
  load
```
You can also get support for Semantic UI loading Willow-SemanticUI, and also for Materialize loading Willow-Materialize. Be advised however that the protocol for these projects is not yet complete.


### What about some examples?
To get an idea of how to use Willow as part of a web application, we have designed 2 simple (but fully functioning) examples, as part of the Willow-Playground project.
After you load it by evaluating:


```
Metacello new
  baseline: 'WillowPlayground';
  repository: 'github://ba-st/Willow-Playground:v9/source';
  load
```

You will have at your disposal a Live Documentation and a Test Runner application. 
For the first we recommend browsing the WPLiveDocumentation class in your environment. For the second browse `WPTestRunner`.

Both applications, along with an interactive tutorial, can be started by evaluating Smalltalks2017Presentation start. Afterwards go to localhost:8080/willow101, localhost:8080/live-docs, localhost:8080/test-runner-bootstrap3 or localhost:8080/test-runner-bootstrap4 to check them running.
