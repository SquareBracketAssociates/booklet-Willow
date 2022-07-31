## Your first Willow application

Now you want to create your own interactive application. How do you proceed? That is what you'll learn here.
Throughout this chapter, we'll assume the goal is to create a simple ToDo list, because we are original like that.


### Defining an application

The first object you will need is a subclass of WillowApplication, in our case:

```
WillowApplication subclass: #ToDoApplication
 instanceVariableNames: ''
 classVariableNames: ''
 package: 'ToDoWeb'
``` 
The simplest thing to do is just complete the methods defined as abstract (`subclassResponsibility`) in `WillowApplication`.

On the class side, the class method `applicationTitle` determines the name shown on your browser tab.

```
ToDoApplication class >> applicationTitle
	 ^ 'To Do'
```
The class method `handlerName` determines the url of your application. For example `http://localhost:8080/to-do`

ToDoApplication class>> handlerName
 ^ 'to-do'

Let’s move now to the instance side.

The method `componentSupplierForApplication` determines the front-end framework of your application. 
We'll start by using the simplest option, plain HTML5, included with the core Willow package.


```
ToDoApplication >> componentSupplierForApplication
 ^ Html5ComponentSupplier new
 ```
 
To add more component suppliers, you need to install additional projects like Willow-Bootstrap for Bootstrap 3 and Bootstrap 4, or Willow-JQueryUI for JQuery UI.

The method `contentView` is where the stuff happens. 
This method should eventually point to the content of your application. 

This means you must return a renderable object (as defined by Seaside). Let's leave that for later, and return only a string:

```
ToDoApplication >> contentView
 ^ 'This is the To Do application'
```

The method `jQueryLibrary` is the last mandatory message to implement. 
It defines the basic jQuery library from Seaside that your application will use. The most common implementation will indicate JQuery 3:

```
ToDoApplication >> jQueryLibrary
  ^ JQuery3OnlineLibrary default
```  

That will be enough to continue.

### Starting your application

With the previous methods implemented, we can already check our application at work.

To start a web server for our applications, we will use Zinc, which comes included with the Seaside installation in Pharo. 
Assuming we choose to use port 8080, the script to start it is:

```
(ZnZincServerAdaptor port: 8080) start
```

Now we need to register our application, so that it can be accessed from a browser:

```
ToDoApplication registerAsDevelopmentApplication
```
With that our little example is ready, go to [localhost:8080/to-do](localhost:8080/to-do) and check for yourself.

