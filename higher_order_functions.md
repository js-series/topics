# JavaScript
## Higher Order Functions

<!-- toc -->

- [SWBAT...](#swbat)
- [What is a HoF?](#what-is-a-hof)
- [HoF's We Know](#hofs-we-know)
  * [Sorting!](#sorting)
  * [addEventListener](#addeventlistener)
  * [Questions](#questions)
  * [Quick Exercise](#quick-exercise)
- [Closure/Scoping](#closurescoping)
  * [Simple Nested Function](#simple-nested-function)
  * [Quick Review In Chrome](#quick-review-in-chrome)
  * [Closure](#closure)
  * [Quick Exercises](#quick-exercises)
- [Conclusion](#conclusion)
- [Next](#next)

<!-- tocstop -->

## SWBAT...

| Objectives |
| :--- |
| Define what a Higher Order Function. |
| Identify HoFs they have seen. |
| Write two different examples of a HoF. |
| Examine and debug closures in Chrome. |


## What is a HoF?

A **higher order function** is a function that either takes a function argument or returns a function.

## HoF's We Know

We've probably seen quite a few instances of Higher Order Functions already. Remember any time you pass a function as an **argument** to another function you are using a Higher Order Function.

### Sorting!

Recall sorting numbers? If we didn't pass in an argument it wouldn't properly sort anything. It's a trash lexicographical sort.

```javascript
var ascending = function ascending(a, b) {
  return a - b;
};

var descending = function (a, b) {
  return b - a;
};

[1, 11, 23, 2].sort(ascending);

[1, 11, 23, 2].sort(descending);
```

### addEventListener

Our usual task of adding an event listener for an event is an example of a higher order function.

`index.html`

```HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Clicky Thing</title>
  </head>
  <body>
    <div id="box">
      Click Me
    </div>

    <script src="app.js" charset="utf-8"></script>
  </body>
</html>
```

`app.js`

```JavaScript
// Select some element from the DOM
var clickBox = document.querySelector('#box');


// Define some handler for clicking the box
var clickHandler = function clickHandler(event) {
  console.log('The box was clicked!');
};

// Add a click handler for click events
clickBox.addEventListener('click', clickHandler);
```

[LIVE EXAMPLE](https://jsbin.com/kupewes/edit?html,js,console,output)

### Questions

* Where else have you provided functions as an argument?

### Quick Exercise

* Write a function called `times` that takes two parameters, a number and a function. It should call the function the specified number of times.

## Closure/Scoping

**WARNING/DISCLAIMER**: You may still be unfamiliar with scope and this isn't the time dive into all the questions you might have. Here the focus will be on giving you the tools you need to explore those concepts on your own.

A function that returns a function is also considered a higher order function. Let's recall what we know about function scoping.

* GLOBAL SCOPE is the default environment where one can define named values: globals vars, named functions, etc.
* LOCAL SCOPE is the environment created inside for an executing function.

We also have certain scoping behavior avaiable for functions.

* LEXICAL SCOPING allows a function to look up a variable that's not defined in it's local scope (so called **non-local variables**).

### Simple Nested Function

Here our `addSeed` value function used inside our `createArray` function has lexical access to the `newArr` value.

```javascript
function createArray(size, seedVal) {
  var newArr = [];

  times(size, function addSeed() {
    newArr.push(seedVal);
  });

  return newArr;
}
```

### Quick Review In Chrome

* Go to **Chrome Dev Tools** > **Sources** and select **Snippets** in the left hand tabs.
* Select **+ New Snippet**
* Paste your code for `times` into the the editor area.

  ```javascript
  function times(number, action) {
     while(number--) {
         action();
     }
  }
  ```

* Paste the above code for `createArray` into the editor.
* Click the line number on the left that has the line. This sets a break point.

  ```javascript
    newArr.push(seedVal);
  ```

* Paste in some lines of code to use `createArray`.

  ```javascript
    createArray(2, 'hello world!');
    createArray(3, 'I am seed value');
  ```

* Hit `CMD + Enter` to run the script. Check out the **Scope** and **Call Stack** dropdowns on the right.
  * What do we see?
* Hit the button at upper left of the right menu to **Resume Script Execution** or hit `CMD + \`. Then observe the changes in the **Scope**.


### Closure

If you return a nested function from a function it will retain values to which it had lexical access. This is called a closure.


```javascript
function createCounter() {
  var count = 0;

  return function counter() {
    count += 1;
    return count;
  };
}
```

The real benefit here of a closure it gives hidden state to your function, and brings your procedural abstractions one step closer to a data-abstraction.

Beware of making closure's your next hammer because you do pay the processing price of **non-local** variable lookup and memory creation of the closure to carry that state.

### Quick Exercises

* Modify `createCounter` to take an optional initial count value.
* Modify `createCounter` to take an optional increment as an argument.
* Use your `createCounter` function to count backward by 2's from 100.


## Conclusion

This is a first introduction to Higher Order Functions and you'll need to see and play with closures quite a few times before they become familiar. Now you've seen it and define and demonstrate how functions execute and use scope. You've also seen that you've been using higher order callback style functions already: event handlers, ajax, promises, etc!

## Next

Going forward we will use callback style function arguments to iterate through lists and accumulate results. You should take some time to look at `forEach` for arrays and try it out a bit. Then try to implement it on your own!