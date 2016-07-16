# jQuery tips, tricks and general use cases

We are going to use some examples based on simple DOM manipulation to illustrate some properties and important features of jQuery, so that when we need to use a specific functionality, we can use this file as an aggregated reference for everything jQuery.

jQuery allows you to have _interactive_ and _dynamic_ webpages via **DOM manipulation**. We shall see on later examples how we can have this interactivity. An HTML document is structured according to the Document Object Model, or DOM. It's by interacting with the DOM that jQuery is able to access and modify HTML.

The DOM consists of every element on the page, laid out in a hierarchical way that reflects the way the HTML document is ordered. Remember how we could think of the HTML document as a tree? You can think of the DOM the same way. Just as with an HTML document, elements in the DOM can have parents, children, and siblings.

## How jQuery works

jQuery uses a special syntax to denote that some elements are going to be manipulated and that jQuery is going to be used. It is also important to denote that jQuery **is** a cross-platform JavaScript library designed to simplify the client-side scripting of HTML, which means that, jQuery **is** javascript with some added properties, and its code file needs to be linked to the HTML in the same way a "normal" js file does.

```javascript
$(document).ready(function() {
    //Perform some actions
});
```
This piece of code, states that _some actions_ will be executed **after** the HTML document loads, i.e. when the document is ready. Soon we will see what sort of actions we would like to perform and how they can be executed using the power of jQuery.

### Relationship between jQuery, CSS, HTML (example taken from http://www.codeschool.com/ jQuery track)

As seen above, the ready action applied to our HTML document, can receive a function as input and perform some actions on our DOM inside that specific function. See the folder basic_manipulations for an example on how to both link jQuery with our HTML document and perform a basic action on an HTML element.

#### basic_manipulations folder contents (example [here](https://cdn.rawgit.com/bruno-oliveira/theodinprojectExercises/master/Tips_JS_%26_jQuery/basic_manipulations/index.html))

The key points to remark here are:

* It is necessary to link the js file inside our HTML using ``` <script type="text/javascript" src="script.js"></script>```
* We can use the jQuery 'object' $() to target specific elements, css classes, and more as we will see later. In this example, we target the div whose id is "green" and we apply the jQuery action fadeOut() to it. There are much more actions and they can all be explored at jQuery's official website API reference: http://api.jquery.com/ 

#### intermediate_usages folder contents (example [here](https://cdn.rawgit.com/bruno-oliveira/theodinprojectExercises/master/Tips_JS_%26_jQuery/intermediate_usage/index.html))

This folder serves as a follow-up on the http://www.codeacademy.com/ track, and it is useful to show that jQuery's power is all about functions, and they can come in several types. We can have, as of now:

1. Higher-order functions: these are functions that can receive **other functions** as arguments and execute them after some specific action or condition is met. An example of such a function so far is the $(document).ready() function that receives another function as argument.
2. Built-in functions (or actions), which are functions that are available to us trough the jQuery API, examples are fadeOut(), hide(), mouseover(), etc. These functions can't generally receive others as arguments and are called first order functions.

### Types of jQuery Selectors, their relationship with CSS. The importance of naming variables that hold selectors correctly.

In the previous examples, we have seen the basic relationship between CSS, jQuery and HTML, by including our js file inside our HTML (with the jQuery library being served by Google's CDN) and by running the examples, it was possible to see that indeed our jQuery worked as expected affecting the elements we intended. Let's take a more in-depth look as to why and how we affected those elements and show a more wider range of actions that we can accomplish with these selectors. **_Anything we can affect via CSS, we can affect via jQuery._**

#### It's all about CSS. How IDs, classes and elements can be manipulated by jQuery.

It is known that we can apply some CSS style to our HTML elements via classes, IDs or simply groups of elements.

Examples of these include:

```css
div {
    height: 100px;
    width: 100px;
    display: inline-block;
    background-color: #F38630;
    border-radius: 5px;
}

#blue {
    background-color: #A7DBD8;
}
```

This applies a certain style to all div elements that have no specific ID and changes the background color of the div element whose id is "blue".

The HTML would look like:

```html
<!DOCTYPE html>
<html>
    <head>
		<title>Vanishing Act</title>
        <link rel='stylesheet' type='text/css' href='stylesheet.css'/>
        <script type='text/javascript' src='script.js'></script>
	</head>
	<body>
        <div id="blue"></div>
        <div></div>
        <div></div>
        <div></div>
        <br/><button>Click Me!</button>
	</body>
</html>
```
Our goal now, is to show how we can use the jQuery selectors (that shall map to the corresponding CSS selectors) to manipulate a specific div element (in this example we want to specifically manipulate the div with id="blue") and we can achieve it with:

```javascript
$(document).ready(function() {
    $('button').click(function() {
        $('#blue').fadeOut('slow');
    });
});
```
The code for this particular example is located in the folder simple_selector and you can run it [here](https://cdn.rawgit.com/bruno-oliveira/theodinprojectExercises/master/Tips_JS_%26_jQuery/simple_selector/index.html).

#### Quick overview regarding Simple Selectors. Compound Selectors explained and an example.

The main idea of simple selectors is that we can use the jQuery object $(), usually coupled with some function to select specific HTML elements:

'div', 'p', 'li', etc, all select the corresponding HTML elements.

However, a much better and fine-grained usage is when we want to select elements with a specific ID or class:

* $('#blue')... -> Allows manipulation of all DOM objects whose id="blue"
* $('.test')... -> Allows manipulation of all DOM objects whose class="test"

#### What are compound selectors?

Imagine that we would extend the usage of selectors in a way that we would select multiple elements at once, for example, elements styled with different classes.

This is exactly the purpose that compound selectors serve, as they allow to select multiple elements that belong to different classes, for an example, check [here](https://cdn.rawgit.com/bruno-oliveira/theodinprojectExercises/master/Tips_JS_%26_jQuery/compound_selector/index.html).

### Using _this_ and its role

As useful as selectors, both simple and compound, are, you might have realized that there's a potential problem with them: they are from what we have seen, very limited, as they allow either for the indescriminated selection of ALL elements of a same type (say, select ALL div or select ALL p) or they allow for selections based on attributes like the ID or the class of a particular element. This is limiting when we want to reference a specific element or affect a specific element from a given group with a particular action. For that purpose, we can use the **this** object.

The this keyword refers to the jQuery object you're currently doing something with. Its complete rules are a little tricky, but the important thing to understand is if you use an event handler on an element, you can call the actual event that occurs (for eg, fadeOut()) on $(this), and the event will only affect the element you're currently doing something with (for example, clicking on or mousing over).

Inside the folder using_this, you can see a working example, which you can run [here](https://cdn.rawgit.com/bruno-oliveira/theodinprojectExercises/master/Tips_JS_%26_jQuery/using_this/index.html), that illustrates the desired functionality.

#### Short explanation of the example

The most important functionality of the example is the usage of the **this** jQuery object inside the script.js file, which allows, as the example shows, for the individual manipulation of objects, i.e., objects that are affected by the desired jQuery actions individually, without being dependent of belonging to a specific css class or having a specific id, which allows for much better interactivity as well as for a fine-grained application of actions to DOM elements, which is usually desired.

### A full example: animating a slider with jQuery

The main goal of jQuery is to allow and add, interactivity to our web applications trough easier DOM manipulation. As an illustrating example, we shall animate a slider using jQuery to put all of these concepts to use, as well as to see the capabilities of this js library.

#### Part 1: The necessary (static) HTML and CSS design

As this is a jQuery tutorial and not a UX/UI design tutorial, the majority of the static code will be given and the main focus will be on using jQuery to anime the elements, as such, the code below can be assumed to be given (a bit like editing an existing codebase):

##### HTML code:
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Slide Panel</title>
        <link rel="stylesheet" type="text/css" href="stylesheet.css"></link>
    </head>
    <body>
        <div class="panel">
        <br />
        <br />
        <p>Now you see me!</p>
        </div>
        <p class="slide"><div class="pull-me">Slide Up/Down</div></p>
    </body>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script type="text/javascript" src="script.js"></script>
</html>
```
##### CSS code:
```css
body {
    margin:0 auto;
    padding:0;
	width:200px;
    text-align:center;
}
.pull-me{
    -webkit-box-shadow: 0 0 8px #FFD700;
    -moz-box-shadow: 0 0 8px #FFD700;
    box-shadow: 0 0 8px #FFD700;
    cursor:pointer;
}
.panel {
	background: #ffffbd;
    background-size:90% 90%;
    height:300px;
	display:none;
    font-family:garamond,times-new-roman,serif;
}
.panel p{
    text-align:center;
}
.slide {
	margin:0;
	padding:0;
	border-top:solid 2px #cc0000;
}
.pull-me {
	display:block;
    position:relative;
    right:-25px;
    width:150px;
    height:20px;
	font-family:arial,sans-serif;
    font-size:14px;
	color:#ffffff;
    background:#cc0000;
	text-decoration:none;
    -moz-border-bottom-left-radius:5px;
    -moz-border-bottom-right-radius:5px;
    border-bottom-left-radius:5px;
    border-bottom-right-radius:5px;
}
.pull-me p {
    text-align:center;
}
```

We can see immediately, that we have defined several classes that are affecting our HTML elements, and it will be by using those classes that we will be able to apply styling and the desired effect to create a slider. Remember that it's easy to manipulate elements that belong to a specific class or have a specific id, using the jQuery selectors.

#### Part 2: Understanding what we need to do and where to apply jQuery

Now that we have the static parts of the code, as well as the styling, done, we can now proceed to what matters, the application of jQuery to animate the our slider.

Let's firstly review the process on applying jQuery:

| Code written                                 | Effect                                                    |
|----------------------------------------------|------------------------------------------------------------|
|  $(document).ready(**function(){}**)         | States that there jQuery will be used to manipulate our html	|
|  **function(){ $('.pull-me').click()};**          | Div with class 'pull-me' will react to the click() event        |
|  $('.pull-me').click(_function(){}_);          | When the div is clicked, some function will be executed              |
|  .click(_function(){ $('.panel').slideToggle('slow')}_) | Triggers the slide action to display our panel 	|

As the special formatting denotes, the most important thing in the application of jQuery to anime a specific HTML element is **function composition**. Function composition is what binds actions together, that when coupled with some of jQuery's built-in actions allows for an element to be animated. 

In the case of our example, the aforementioned function composition coupled with built-in jQuery actions, works as follows:

When our document is ready, a function will be executed. That function will "tell" the div with class 'pull-me' to react to the click built-in action and, following that, the click built-in function, when executed will call yet another function, i.e., the built-in slideToggle action, that will animate our element.

The final code is available inside the folder jquery_slider and it can be run [here].
