Angular [Udemy Class](https://www.udemy.com/ultimate-angularjs-course/learn/v4/overview) Notes.

###Set-up

* Make folders css, scripts
* Make file `index.html`
* run npm commands:

```
$ npm init
$ npm install angular angular-material mdi angular-animate angular-aria angular-messages
$ npm install http-server -g
$ mkdir css scripts
$ touch index.html

```

###Files

* Set up a basic html file in `index.html`
* Link to the angular.js file in the angular folder in node_modules
* Create `app.js` file in scripts folder. This will be your first module


###Module - Basic Set-up

This sets up the module and the array is for any dependent modules

In `app.js`:

```
angular.module("ngClassified", [])

```
In `index.html`:

```
<body ng-app="ngClassifieds">

```
This will say: "Hey, within this tag make the ngClassifieds module available"

Within the body tag add a template message inside an h1 tag, curly braces are for templates

```
{{ message }}

```
Just to test if it's working you can add the following to to body tag as well.

```
ng-init="message='hello world'"

```

Now it's time to run the server to see if the app is working

```
$ http-server

```


###MVC - Model View Controller

Breaks code into different responsibilities 

* Separation of Concerns
* Smaller Units are Easier to Reason About
* Helpful when you're working with teams
* Keeps Code DRY (Don't Repeat Yourself)
* Saves Time

####Model

Communicating with the database

####View

The code that makes up what the user actually sees

####Controller

Takes the data from the Model and delivers it to the View and vis versa

### Controllers

Create a new folder `components` with a file `classifieds.ctr.js`

```
$ mkdir components
$ touch classifieds.ctr.js

```

In this file we will be using immediately evoked functions and "use strict". We also call angular.module again like in the `app.js` file, but we don't pass it an array. This will make it a reference not a declaration of a new module

`/components/classifieds.ctr.js`

```
(function(){
  "use strict"
  angular
    .module("ngClassifieds")
    .controller("classifiedsCtrl")
})()

```

Add `ng-controller="classifiedsCtrl"` to the body tag, body tag will read as follows

`index.html`

```
<body ng-app="ngClassifieds" ng-controller="classifiedsCtrl">

```

### $scope object

`$scope` is the glue between the controller and the view. You must inject the $scope as a parameter in an anonymous function within the `.controller` method in the `classifieds.ctr.js` file. Then you can set variables like the example below

`classifieds.ctr.js`

```
...

.controller("classifiedsCtrl", function($scope){
  $scope.name = "Tiffany"
})

```

`index.html` - You can add this code to the file to get the name variable

```
{{ name }}

```

Also add a reference to the `classifieds.ctr.js` file in the `index.html` using a script tag

###Two Way Data Binding

Two way data binding allows you to have live updates to your app

In the index file add an input box above h1 name tag. `ng-model` allows you to reference a certain `$scope` element

```
<input type="text" placeholder="Enter Your Name" ng-model="name">

```

The above will now be directly tied to the `{{name}}` when you type

###More about Templating

You can also do math in the temples:

```
  <p>{{ 5+6 }}</p>

```
You can concatenate strings with variables

```
  <h1>{{name + ", how are you today"}}</h1>

```

You can do it this way too:

```
  <h1>{{name}}, How are you today</h1>

```

####Scope and Objects

You can also make the scope be an object

In the `index.html` file you can change the name variable to be an object with first and last name:

`index.html`

```
$scope.name = {
  first: "Tiffany",
  last: "Poss"
}

```

You must also change the `ng-model` property of the input box to be `name.first` since it is now an object

```
<input type="text" placeholder="Enter Your Name" ng-model="name.first">

```

###Dependency Injection

Allows us to easily being in code to various parts of our application

###Providers

Add ngMaterial to the `app.js` file in the array

```
angular.module("ngClassifieds", ["ngMaterial"])

```

You can also add the below to set the defaults for ngMaterial

```
angular
  .module("ngClassifieds", ["ngMaterial"])
  .config(function($mdThemingProvider){
    $mdThemingProvider.theme("default")
      .primaryPalette('teal')
      .accentPalette('orange')
  });
```


###Directives

Examples of things you might see.

```
<md-toolbar></md-toolbar>
<md-button></md-button>

```
You can use them as an html element (only recognized by Angular), or as an attribute of an element.

Add the following dependencies to your app for angular-material

```
  <script type="text/javascript" src="node_modules/angular-animate/angular-animate.js"></script>
  < script type="text/javascript" src="node_modules/angular-aria/angular-aria.js"></script>
  <script type="text/javascript" src="node_modules/angular-material/angular-material.js"></script>

```

####Adding a Directive

Normally you would have separate files for your directive, but here we will just add it to your `app.js` file

Here we will be making a "hello world" directive

Within your `index.html` files add the following code:

```
  <hello-world></hello-world>

```

Within your `app.js` file add the following snippet below the other code, chaining the method on the angular object. This will return an object known as the "directive definition object"

```
  .directive("helloWorld", function(){
    return {
      template: "<h1>Hello, World!</h1>"
    }
  })

```

The reason why you have `hello-world` in "kebab case" in the `index.html` file and `helloWorld` in "camel case" in the `app.js` file is because Angular will automatically convert the camel case in the directive into kabab case.

#####Using Templating in your directive

You could also use templating in this system with the curly braces.

In `app.js` change the `<h1></h1>` message to contain `{{ message }}`

```
  .directive("helloWorld", function(){
    return {
      template: "<h1>{{ message }}</h1>"
    }
  })

```

In `classifieds.ctr.js` add message to the scope:

```
  $scope.message = "Hello, world!"

```


###Angular Material

Angular Material is a library based on Google's Material Design which gives you many ready to go elements

In `index.html` add the Angular Material css files from the node_modules folder

```
  <link rel="stylesheet" href="node_modules/angular-material/angular-material.css">
  <link rel="stylesheet" type="text/css" media="all" href="node_modules/mdi/css/materialdesignicons.min.css">

```

Once you added that you can start adding directives from Material design

####Toolbar

In `index.html` you can add:

```
  <md-toolbar>
    <div class="md-toolbar-tools">
      <p><strong>ngClassifieds</strong></p>
      <md-button>
        <md-icon class="mdi mdi-plus-circle"></md-icon>
          New Classifieds
      </md-button>
    </div>
  </md-toolbar>

```

The above is a bunch of pre-made derivatives made in Material Design. There are some pre-made classes and tags, and also icons using mdi. 

You can create a `style.css` file within the `css` folder and add a link to the `index.html` file

####Content

For the content part you can add the below snippet to the `index.html` file. This is using the `md-content` derivative and is utilizing the md-padding class, and layout features. Material design uses flex-box.

```
<md-content class="md-padding" layout="row" layout-wrap>
    <md-card flex="33">
      <img src="http://i01.i.aliimg.com/wsphoto/v0/32276661925/diy-full-diamond-painting-sets-butterfly-kitten-diy-square-resinstone-diamond-painting-patchwork-unfinish.jpg">
      <md-card-content>
        <div class="classified-info">
          <h2 class="md-title">First Kitten</h2>
          <h3>$1,000,000</h3>
          <p>Attack dog, run away and pretend to be victim cat is love, cat is life. Hiss at vacuum cleaner bathe private parts with tongue then lick owner's face refuse to drink water except out of someone's glass. Run outside as soon as door open need to chase tail. Make muffins damn that dog so chase red laser dot for all of a sudden cat goes crazy favor packaging over toy. Eat from dog's food chase the pig around the house and walk on car leaving trail of paw prints on hood and windshield play time.</p>
        </div>
      </md-card-content>
    </md-card>
  </md-content>

```

* `md-content` tag is material design's content, it also has pre-made padding class and flex-box styling attributes
* `md-card` is a pre-made card derivative
* `flex=33` is saying flex-box 33% width of the page for this element
* `md-card-content` is the card's content


#####Bringing content to the controller

The above is hard coded, but what if you want to have the content from a database (or here we will just be using a json object)

The markup from the previous section now looks like this in `index.html`

```
  <md-content class="md-padding" layout="row" layout-wrap>
    <md-card flex="33">
      <img src="http://i01.i.aliimg.com/wsphoto/v0/32276661925/diy-full-diamond-painting-sets-butterfly-kitten-diy-square-resinstone-diamond-painting-patchwork-unfinish.jpg">
      <md-card-content>
        <div class="classified-info">
          <h2 class="md-title">{{classified.title}}</h2>
          <h3>{{classified.price}}</h3>
          <p>{{classified.description}}</p>
        </div>
      </md-card-content>
    </md-card>
  </md-content>

```


Add the following snippet to the `classifieds.ctr.js` file:

```
  $scope.classified = {
      	title: "First Kitten",
      	price: "$1,000,000",
      	description: "Attack dog, run away and pretend to be victim cat is love, cat is life. Hiss at vacuum cleaner bathe private parts with tongue then lick owner's face refuse to drink water except out of someone's glass. Run outside as soon as door open need to chase tail. Make muffins damn that dog so chase red laser dot for all of a sudden cat goes crazy favor packaging over toy. Eat from dog's food chase the pig around the house and walk on car leaving trail of paw prints on hood and windshield play time."
      }

```


###Looping through content

`ng-repeat` takes a collection (from an array) and iterates over it.

You add the `ng-repeat` derivative to whatever element you would like repeated, in the above case it is `<md-card` tag.

Update the html `md-card` to be the below, this will loop through the classifieds array from `$scope` in the controller (must also be updated). We also updated `flex` to equal 30 to make more room so 3 listings fit per row

```
  <md-card flex="30" ng-repeat="classified in classifieds">
    <!--whatever-->
  </md-card>

```

`classifieds.ctr.js` now has a $scope like the below, an array of objects (now updated to classifieds, with an s on the end):

```
$scope.classifieds = [
  {stuff: "stuff"},
  {stuff: "moreStuff"},
  {stuff: "evenMoreStuff"}
]

```

Now within the `md-card` in `index.html` you can update it to template

* image src is now `{{ classified.image }}`, and `src` will be replaced with `ng-src`

```
<img ng-src="{{ classified.image }}">

```

The rest can remain the same



###Angular's Built-in Filters

You can access built-in filters by using the pipe character `|` after the variable name within the template

####Currency Filter

```
  <h3>{{ classified.price | currency }}</h3>

```
####Date

You can have dates formatted automatically and pass them attributes of the way you want it formatted

```
  <h3>{{ classified.posted | date:'longDate' }}</h3>

```

####Other Filters

* uppercase
* lowercase
* json (if you wanted to format markup)

###Hiding and Showing Parts of the UI

`ng-show` is an attribute in Angular that will take a value of true or false in order to show or hide something.

Below if `showName` is a truthy value it will show it, if not it will hide it

```
  <p ng-show="showName">Tiffany</p>

```
####ng-show and ng-click

You can also add the `ng-click` to a button to easily set this value. Consider the below will toggle between displaying the first name and last name.

On page load the last name is shown and the first name is hidden, but it can be toggled with the buttons

```
  <button ng-click="showName = true">Show Name</button>
  <button ng-click="showName = false">Hide Name</button>
  <p ng-show="showName">Tiffany</p>
  <p ng-show="!showName">Poss</p>

```

####ng-if

`ng-if` removes elements from the dom completely. A good example for use would be a user is admin to show it, but if they are not don't serve that content

```
  <div class="classified-admin" ng-if="showAdmin"></div>

```

####Example

Consider the following

```

  <div class="classified-contact" ng-show="showContact">
          <p><md-icon class="mdi mdi-account"></md-icon>{{ classified.contact.name}}</p>
          <p><md-icon class="mdi mdi-phone"></md-icon>{{ classified.contact.phone}}</p>
          <p><md-icon class="mdi mdi-email"></md-icon>{{ classified.contact.email}}</p>
   </div>
   
   <div layout="row">
   
          <md-button 
            ng-click="showContact = true"
            ng-show="!showContact">
            Contact
          </md-button>
          
          <md-button 
            ng-click="showContact = false"
            ng-show="showContact">
            Details
          </md-button>
          
          <md-button 
            ng-click="showAdmin = true"
            ng-show="!showAdmin">
            Admin
          </md-button>
          
          <md-button 
            ng-click="showAdmin = false"
            ng-show="showAdmin">
            Close
          </md-button>
          
        </div>
        
        <div class="classified-admin" ng-if="showAdmin">
          <h3>Admin</h3>
          <div layout="row">
          	<md-button class="md-primary">Edit</md-button>
          	<md-button class="md-warn">Delete</md-button>
        </div> 
        
    </div>
        
```


##$http & Data

####Round Trip Apps

* Resources Returned for Individual Pages
* Data Returned with Requests


####Single Trip Apps

* All Page Resources Load on Initial Page Load
* Data is sent and receive by a Data API
* Backend is Self-contained
* Front-end is Self-contained


####RESTful API

An api that allows you to dig deeper into the api in order to get additional information

```
api.github.com/users
api.github.com/users/mojombo
api.github.com/users/mojombo/followers

```

Each one of the urls above digs deeper into the api to get additional information



###Remote Data Sources

Create a new folder on the top level titled `data` and create a `classifieds.json` inside of it

Move the array of data from the `classifieds.ctr.js` file into the new `classifieds.json` file

Within the `classifieds.ctr.js` file you now want to inject `$http` into the .controller function so it looks something like this:

```
  angular
    .module("ngClassifieds")
    .controller("classifiedsCtrl", function($scope, $http){
      $http.get('data/classifieds.json').then(function(classifieds){
      	$scope.classifieds = classifieds.data;
      });
  });

```

* `$http` is for ajax requests
* `$http.get` allows you to make a get request to an api, in this case we are just using a local file
* `.then` is used because angulars $http uses promises
* `classifieds` represents the data that it receives (in this case the json data from `classifieds.json`)
* `$scope` makes the received data accessible to the html file
* `classifieds` sets it to the data object that it defaults to

###Services

What happens if you want to use the same data in multiple pages in the same app. Instead of copying and updating code, you can use services.

There are many ways to make a `Service`. One way is to make a factory. 

In the `components` folder create a file named `classifieds.fac.js`. This will be our factory

`classifieds.fac.js`

```
  (function(){
	"use strict";
	 angular
	  .module("ngClassifieds")
	  .factory("classifiedsFactory", function($http){
	    function getClassifieds(){
	    	return $http.get('data/classifieds.json')
	    }
	    return {
	    	getClassifieds: getClassifieds
	    }
	  })
  })()

```

* calls the `ngClassifieds` module
* creates a factory named `classifiedsFactory` with param of `$http`
* returns an object with getClassifieds and returns the method that is defined above that
* `getClassifieds` function returns a get request to the same data file


Now you must add the `classifieds.fac.js` file to your `index.html` file

In the controller, the `classifieds.ctr.js` file, you can swap out the old code make a get request to:

```
  angular
    .module("ngClassifieds")
    .controller("classifiedsCtrl", function($scope, $http, classifiedsFactory){
      classifiedsFactory.getClassifieds().then(function(classifieds){
      	$scope.classifieds = classifieds.data
      });
  });
  
```

* passes `classifiedsFactory` into the controller
* runs the `getClassifieds()` method we created in the factory
* `then` evokes a promise and the data is set to `$scope`



###Creating Data

####Side Nav

Angular Material has a side nav function you can add to your angular sites.

Below is some AM premade things to create a pre-made sidebar

```
   <md-sidenav class="md-sidnav-left md-whiteframe-z2" 
    md-component-id="left"
    md-is-locked-open="true">
    <md-toolbar>
      <h1 class="md-toolbar-tools">Add a Classified</h1>
    </md-toolbar>
  </md-sidenav>

```

* `md-sidenav` is a sidenav component
* `md-sidenav-left` makes it on the left side
* `md-whiteframe-z2` controls some styling
* `md-component-id` is giving the complenet an identifying name
* `md-is-locked-open` mades it default open
* `md-toolbar` because it's a toolbar


####The form

Add a form inside of the `md-sidenav` section at the bottom.

```
<form>
        <md-input-container>
          <label for="title">Title</label>
          <input type="text" id="title" 
                md-autofocus>
        </md-input-container>
        <md-input-container>
          <label for="price">Price</label>
          <input type="text" id="price">
        </md-input-container>
        <md-input-container>
          <label for="description">Description</label>
          <textarea type="text" id="description"></textarea>
        </md-input-container>
        <md-input-container>
          <label for="image">Image Link</label>
          <input type="text" id="image">
        </md-input-container>
        <md-button class="md-primary">
          Save
        </md-button>
        <md-button class="md-primary">
          Save Edit
        </md-button>
        <md-button class="md-warn">
          Cancel
        </md-button>
      </form>

```


Now find the `New Classfieds` button made earlier. We are going to add a click handler in there to control the side nav

```
  <md-button ng-click="openSidebar()">
    <md-icon class="mdi mdi-plus-circle"></md-icon>
      New Classifieds
  </md-button>

```

In the `classifieds.ctr.js` add this to control the `openSidebar` method we just added to the above button. We must pass in $mdSidenav as a param in the controller, then we can references it in scope

```
  $scope.openSidebar = function(){
    $mdSidenav('left').open()
  }

```

That will control the open and close of the sidebar

#####Closing the sideNav on click of button

Add an `ng-click` to the cancel button from the form with a new function `closeSidebar`

```
  <md-button ng-click="closeSidebar()" class="md-warn">
      Cancel
  </md-button>
```

within the controller add the below

```
  $scope.closeSidebar = function(){
    $mdSidenav('left').close();
  };

```


###Adding data

> Note that since we arn't using a real backend database, even though we will be able to add data, once we refresh it will not persist.

In our form we need to add `ng-model` to all of our input/textarea boxes. For example `ng-model="classified.title"` for the title one etc.


once we do that, we can temporaryly see if its working by writing this `classifed` object the screen.

You can add the below text within the form to see if what you type will appear as a json object on the screen

```
  <pre>{{ classified | json }}</pre>

```

####How to send data through


In `classifieds.ctr.js`, the basic setup is as follows:

```
  $scope.saveClassified = function(classified){
    $scope.classifieds.push(classified);
  }


```

In `index.html` you can add a `ng-click` method for the saveClassified one from the controller. Notice that we are passing in classified, the object we previously made linked to the input boxes

```
  <md-button ng-click="saveClassified(classified)" class="md-primary">
    Save
  </md-button>
```

Now you will be able to click save and the content will be added to the data and it will append to the page automatically

####Make sure required data is filled in.

Add an if statement `if(classified)` around the if push statement in the controller, this will make sure at least one of the properties are filled in.

####Clearing the input boxes after they are submitted

In the controller you can set `$scope.classified = {}` to an empty object

####Closing side nav after saving

In the controller, add `$scope.closeSidebar()` to close it after saving


The controller for the `saveClassified` section looks something like the below:

```
  $scope.saveClassified = function(classified){
    if(classified){
      $scope.classifieds.push(classified);
      $scope.classified = {};
      $scope.closeSidebar();
    }
  }
    
```


###Adding User info to classifieds

>We are not going to add a login, but we are going to fake being able to add your contact info. Normally on one of these sites you might create a profile and log in, then you would be able to post ads that would auto populate your info. We are going to fake that here.

To the controller you might add something like this to make a fake contact

```
  var contact = {
    name: "Tiffany Poss",
    phone: "(555) 555-5555",
    email: "tiffanyposs@gmail.com"
   };
    
```

then you can add it to your saveClassified by doing:

```
  classified.contact = contact

```

###Adding a completed popup

The `toast` feature the Angular Material allows you to make a popup message when an action is completed

Add `$mdToast` as an injections on the controller (param). Then you can add `$mdToast` to the if statement within the `.saveClassified` area of your controller.

```
  $mdToast.show(
    $mdToast.simple()
      .content("Classified Saved")
      .position("top, right")
      .hideDelay(3000)
  );

```

* `.show` shows it
* `simple` makes it simple
* `.content` says whats inside
* `.position` tells you were to put it
* `.hideDelay(3000)` will hide it once it's shown for 3 seconds



###Editing

In the `index.html` you want to add `ng-click="editClassified(classified)"` to the `md-button` within the cards, making sure to pass it classified. This classified is the current iteration of the card, so it will attach it one to the one that is clicked on by the user to edit

In the `classified.crt.js` file, add the `editClassified` method to `$scope`

```
  $scope.editClassified = function(classified){
  	//do stuff
  }

```

Then you're going to need a way to tell the window if something is currently being edited. You can set a editing variable like this:

```
  $scope.editing = true;

```

The logic is that if the person is editing, show the Edit Save button and if they person is creating a new one, show the Save button. So within those two buttons within the `index.html` file you can use `ng-if` to toggle which one shows and hides:

```
  <md-button ng-if="!editing" ng-click="saveClassified(classified)" class="md-primary">
    Save
  </md-button>
  <md-button ng-if="editing" class="md-primary">
    Save Edit
  </md-button>

```

Then, whenever we are editing, we want to sidebar to open, so you can simply add the below to your `.editClassified` section of you controller

```
$scope.openSidebar()

```

Now that the nav bar will open when you click on Edit, you want the content of that card to auto-populate into the form. Below you are taking the param that you are passing in and passing it to the form on `$scope`. Now the form will have the data from the one you are editing and it will live update on the screen as you edit it.

```
$scope.classified = classified;

```

Now you will see that the update will remain the same if you x out of the sidebar, but we have not added functionality to the Save Edit button yet.

```
  $scope.saveEdit = function(){
    $scope.editing = false;
    $scope.classified = {};
    $scope.closeSidebar();
  }

```

* You create a `saveEdit` function on $scope
* `$scope.editing` You set editing to false so the appropriate buttons will disappear
* `$scope.classified` sets the form to nothing
* `$scope.closeSidebar` closes the sidebar


Now we want to create a popup again like when we create a new classified, but it seems like we would have to re-write a bunch of code. Lets take the old code and make it reusable.

Take all the showToast method from the `saveClassified` and move it into a new independed function. This we will pass in the message instead of hard coding it in.

```
  function showToast(message) {
    $mdToast.show(
	  $mdToast.simple()
	  	.content(message)
	  	.position("top, right")
	  	.hideDelay(3000)
      );
    };

```

Now we have a reusable function we can add to any completed task with on line of code. Add `showToast("Classified Saved!")` to where the `$mdToast` used to be in the `.saveClassified` section. Add `showToast("Edit Saved");` to the `.saveEdit` section.

Lastly we can add `ng-click` to the Save Edit button:

```
  <md-button ng-click="saveEdit()" ng-if="editing" class="md-primary">
     Save Edit
  </md-button>

```

Now you controller looks like this for the new added sections:

```
  $scope.editClassified = function(classified){
    $scope.editing = true;
    $scope.openSidebar();
    $scope.classified = classified;
  }

  $scope.saveEdit = function(){
	$scope.editing = false;
	$scope.classified = {};
	$scope.closeSidebar();
	showToast("Edit Saved");
  }

```


###Deleting

In the `index.html` find the delete button from the 