Most of us started developing Angular apps with one of these many tutorials out in the internet.

All the authors - which I belong to as well - have done a great job showing the basics and these "how-to-get-started"-articles. But these are very small example projects that are far away from a real world app. The real challenge comes mostly if the code grows starting with a certain size of the codebase.

Luckily I had the possibility to participate in several large Angular applications until now. And I realized that all teams are facing the same problems at the beginning of their project:

<blockquote>Btw these are the questions that I usually hear in my workshops.</blockquote>

In this blogpost I'll try to skim on some examples of what I have come up with as good solutions for myself.

<blockquote>Please keep in mind: these are my solutions. If you disagree let's discuss this here or on twitter @webdave_de.</blockquote>

Here are the questions and problems:
<ol>
	<li>Which folder structure should I build to stay scalable?</li>
	<li>How do I cut modules?</li>
	<li>Is it possible to have too much modules?</li>
	<li>Which components are there?</li>
	<li>What belongs in a component, what in a service?</li>
	<li>Where should I provide services?</li>
	<li>The imports are too long!</li>
	<li>How to keep my code maintainable even for colleagues?</li>
</ol>

<h2>Folder structure</h2>

Since Angular CLI stepped in most of the Angular projects are scaffold with it. Hence we often have a well known poject structure.

<img src="https://www.webdave.de/wp-content/uploads/2018/03/architecture_1-150x150.png" alt="" width="150" height="150" class="alignnone size-thumbnail wp-image-446" />

In the project root folder we see some files and three folders: "e2e", "node_modules" and "src"
We want to focus on the <code>src</code> folder for now. Here our application code is located.
Inside the "src" folder we'll see the <code>app</code> folder where our application logic is located.

So we have a nice starting point. Kudos to the cli team btw.!

But that's not enough: The next step should be the structure of our application in the <code>app</code> folder.

In there we can split the application in some sub folders to organize our code better. It’s very common to do it like that.

First of all we want to create a <code>feature</code> folder for our features we want to implement in our app.
We also want to have a <code>framework</code> folder and a <code>shared</code> folder.

<blockquote> They seem to be very similar but if we take a look at the functionalities we can see the differences.</blockquote>

<ul>
	<li><strong>shared</strong>: is used at multiple places</li>
	<li><strong>framework</strong>: is used generaly</li>
</ul>

That’s the outline of our architecture.

Now let's have a look at a very common user interface (UI).

Most of the apps have a navigation, a header and something very often called "container" or "view".

# IMG_2

Those parts together are known as the <strong>app shell</strong>.
The app shell is a very important part of your app. It's visible almost everywher  and an important piece of code when you start thinking about Progressive Web Applications (PWAs).

So where would we expect the app shell to be located?
Right: in <code>framework</code> folder because it's a generaly used functionality.

<h2>Cut your code into modules</h2>

Next let's talk about the <code>features</code>.
To get the idea of the features of an app it's always a good strategy to look at the menu/navigation.

# IMG_3

All this entries are features.

<blockquote>very important principle:
	<ul>
		<li>split your application into features.</li>
		<li>every feature should have it’s own module.</li>
	</ul>
	that’s called <strong>single responsibility</strong> or <strong>seperation of concerns</strong>
</blockquote>

// Achtung: SRP !== SOC! Am besten sagst du nur "Soc" :)

in fact that means:
<ul>
	<li><h3>no amme <small>(sorry sheldon)</small></h3></li>
<li><h3>no asme</h3></li>
<li><h3>no acme <small>(sorry bugs bunny)</small></h3></li>
<li><h3>no adme</h3></li>
</ul>

// Was bedeuten diese Abkürzungen?

<h2>FAQ</h2>

<i>Q: But if I split everything into modules it is possible to have too many modules?</i>

A: No! The maintainability grows by the number of modules. Split your app into modules and your modules into sub modules

# IMG_4

<h2>Type of components</h2>

So what about Components? Components represent the UI stuff of our app. We can break them up into two categories:

container components and presentational (or dumb) components.
<ol>
<li>Container Components can host other components and logic. They are connected to services to get data maybe from an api and provide this data to their child components</li>
<li>Dump Components have no dependencies, they only have logic which is directly used for their view. They get all the data they need through the @Input decorators, communicate with their parents through @Output decorators
and they are reusable.</li>
</ol>

# IMG_4

Just a small explanation of the connection and the data flow here

We have a container component with some logic and it holds some presentational components.
All the data the presentational components need are passed through the @Input decorators. If they want to talk to their parents they would make use of an @Output decorator. If we use a service for some stuff we only use it in the container component.

# IMG_6

To identify these kind of components take a look at the mockups. Sections which can be splitted into smaller parts are container components.

# IMG_7

Those small parts can be presentational components

# IMG_8

<h2>Reuse code</h2>

Components can be reused but logic can be reused, too. We can relocate logic into services.

Almost all logic in am app should fit to one of the following categories:
<ol>
<li>View logic</li>
<li>Reusable logic (the logic we copy ‘n paste in a bunch of components)</li>
<li>Logic to call the api and manage the data</li>
<li>All the other logic ;)</li>
</ol>

<blockquote>Dont mess arround with the dependency tree. Provide the logic at the top most point where it is needed. It might be a component or a module or even another service.</blockquote>

<h2>Stay maintainable</h2>

Maybe your structure is very deep.
And this means you have looooong imports.

# IMG_9

That's no problem if your IDE is able to manage the imports automatically but if you move modules to another place, it’s can get hard to refactor and maintain. Yes it is a pain but there is a solution.

<code>pathmap</code>. 
The pathmap is an awesome typescript feature. You can define a mapping table in your tsconfig.json

# IMG_10

which can maybe change your developer live

# IMG_11

<h2>Follow the style guide</h2>

that’s the structure of our companies feature

# IMG_12

The naming conventions is very important.

<ul>
<li>Modules should be named as <code>.modules</code></li>
<li>componnet should be named as <code>.components</code></li> 
<li>etc</li>
</ul>
find meaningful names for your classes, methods and attributes.
<blockquote>I once was fighting with a project where every method and every file had a variable called tmp!
that was not helpful at all</blockquote>





