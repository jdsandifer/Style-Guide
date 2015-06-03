# Overview

For almost all of our styles, refer to the [ES5 AirBnB styleguide ](https://github.com/airbnb/javascript/tree/master/es5).

There are a few things that we have customized for our tastes which will take presidence over AirBnB.

# Whitespace
* Use soft tabs set to 4 spaces

```js
// bad
function() {
∙∙var name;
}

// bad
function() {
∙var name;
}

// good
function() {
∙∙∙∙var name;
}
```

# Naming Conventions
* When saving a reference to `this` use `self`

```js
// bad
function() {
  var _this = this;
  return function() {
    console.log(_this);
  };
}

// bad
function() {
  var that = this;
  return function() {
    console.log(that);
  };
}

// good
function() {
  var self = this;
  return function() {
    console.log(self);
  };
}
```
