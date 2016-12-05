# Angular Custom Directives

## Custom directives

##### What are some *standard* directives we've seen so far?

We've seen a lot of attributes: `ng-repeat`, `ng-app`, and so on. But directives
can also be entire elements. Angular lets you create, say, `<grumble>` and
`<comment>`.

##### So what *is* a directive, anyway?

Directives are markers on a DOM element (tags and attributes) that tell AngularJS's HTML compiler to attach a specified behavior to that DOM element.

Directives are Angular's way of letting you add behavior to elements and attributes. DOM elements already have behavior we would want for displaying and linking documents, the original utility of the web. Angular directives add behaviors we would want for building applications.

Basically, a directive is some HTML defined by Angular. A directive can be an
attribute, an element, a class, or even a comment.

All HTML elements have behaviors: anchors take you to a page when you click on
them, textareas let you write stuff inside them, and so on. Angular lets you
create your own HTML elements and give them behaviors you define.

Ever wished there was a `<comment-box>` or a `<random-bill-murray-img>` element?
Now you can make one.

One of Angular's sort-of 'mission statements' is 'to be what HTML would have
been if it was designed from the start with web apps in mind.'

### You can think of directives as 'Angular elements'

Directives are most like helpers in Rails.

##### What are some Rails helpers you remember?

`form_for`, `link_to`, `render partial`, and so on.

##### What do those helpers do?

They all add HTML to a view.

## Let's Make one!

### Define a `directive`

```js
.directive("spineCaseVersion", function(){
  return {}
})
```

```html
<spine-case-version></spine-case-version>
```


### Set a template

```js
.directive("spineCaseVersion", function(){
  return {
    template: 'Hello world'
  }
})
```
One thing to note is that Angular expects you to write the directive's name as camelCase inside the directive JS, but as spine case inside the HTML. .directive('spineCaseVersion') automatically turns into <spine-case-version>.



### Restrict to E,A,C,M

- **E**lement
- **A**ttribute
- **C**lass
- Co**M**ment

```js
.directive("spineCaseVersion", function(){
  return {
    template: 'Hello world',
    restrict: 'E'
  }
})
```
If you only want your directive to be available as an element, you add restrict: 'E' to your directive. This will make angular use the my-custom-directive element and ignore the my-custom-directive attribute. If I add restrict: 'A', it does the opposite.

```html
<spine-case-version></spine-case-version> <!-- element -->
<div spine-case-version></div>            <!-- attribute -->
<div class='spine-case-version'></div>    <!-- class -->
<!-- directive: spine-case-version -->    <!-- comment -->
```

### Initialize some variables
```js
.directive("spineCaseVersion", function(){
  return {
    template: 'Hello {{name}}',
    link: function(scope){
      scope.name = 'Jesse'
    }
  }
})
```

Directives can be given a parameter called link. It'll automatically be run every time an instance of that directive is created

Angular actually passes into this link function an argument called scope. This is an object that's available both in the directive's JS and the directive's HTML. So anything I add to it in the JS will be available in the HTML, and vice-versa.

### Add a method

```js
.directive("spineCaseVersion", function(){
  return {
    template: '<div ng-click="shout(name)"> Hello {{name}}></div>',
    link: function(scope){
      scope.name = 'Jesse'
      scope.shout = function(name){
        alert("HELLO " + name.toUpperCase())
      }
    }
  }
})
```

### Get information into the directive

So far we've seen a bunch of ways of getting things out of the Javascript and into the HTML. But how do we get things out of the HTML and into the Javascript?

We do so using attributes:

```html
<spine-case-version name='Jesse'></spine-case-version>
```

```js
.directive("spineCaseVersion", function(){
  return {
    template: '<div ng-click="shout(name)"> Hello {{name}}></div>',
    scope: {
      name: '@'
    },
    link: function(scope){
      scope.shout = function(name){
        alert("HELLO " + name.toUpperCase())
      }
    }
  }
})
```

## You do: Random Bill Murray Image Directive

https://github.com/ga-wdi-exercises/random-billmurray

### Bonus

Pass the image sizes in from the HTML.

### Double Bonus

Increment the size of the image every time the user clicks on the image.

## Hungry for more?

https://github.com/ga-wdi-lessons/angular-directives
