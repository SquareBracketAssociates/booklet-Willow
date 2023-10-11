## Rendering 

Here we should have a little intro. 

### What can be rendered?

We mentioned in the previous post that `TodoApplication>>#contentView` should declare the content to render.
We will use to the concept of a renderable object as provided by Seaside.

- Rendering a string means just drawing it on the screen, like we saw in the previous chapter. (SD it was unclear to me)
- Rendering a block with no arguments means rendering the result of evaluating it.
- Rendering a block with one argument considers the argument to be a canvas on which you can write html using Seaside syntax. For example, to add a span with class ``‘sample’``, that contains the text ``“hello world”``, you write:

```
[ :canvas | canvas span
                     class: 'sample';
                     with: 'hello world' ]
```	 

Rendering a Seaside component (normally a subclass of `WAPainter`), requires implementing the method `renderContentOn:` on it, with the argument being a canvas as was the case for blocks:

```
TodoApplication>>renderContentOn: aCanvas
    aCanvas span
       class: 'sample';
       with: 'hello world'
```
If your method `contentView` returns an object that does not match any of the previous cases, the message `printString` will be sent to the object and the result will be rendered.

### What was that about a Painter?

We just mentioned that one of the possible contents is a subclass of `WAPainter`. 
You are encouraged to reify the components of your application in that way. 
You can build the instances as you like, implement whatever methods you require, and the only requirement is that you implement the method `renderContentOn:` to determine how it will be rendered on the browser.

Now, the interesting trick is that `aCanvas` understands the message `render:` which receives a renderable object, just as before (string, block, subclass of `WAPAinter`). So you could have something like this:

```
WAPainter subclass: #PendingTask
	...
```

```
PendingTask >> renderContentOn: aCanvas
 aCanvas strong: 'Do it'.
 aCanvas paragraph: 'Only you can improve the code!'
TodoApplication >> #contentView
 ^ [ :canvas | canvas unorderedList
                   add: PendingTask new ]
```
So, in the end, the components that represent the visual interface of your model will be defined using these web views that inherit from WAPainter. In most cases, only the innermost object will use the Seaside messages to write directly on the canvas, the rest will do stuff like aCanvas render: aWebView.
To polish this implementation, let’s extract the rendering of the task to its own method:

```
PendingTask >> contentView
 ^ [ :canvas | self renderTasksOn: canvas ]
```

```
PendingTask >> renderTasksOn: aCanvas
  aCanvas unorderedList add: PendingTask new
``

Now we will learn how to access commonly used web views.

