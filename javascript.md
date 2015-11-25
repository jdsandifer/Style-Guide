# JavaScript Coding Standards

For almost all of our code style rules, refer to the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript).

When writing ES6 or React code (supported in files with a `.jsx` extension), please also refer to the [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react).

There are a few things that we have customized for our tastes which will take presidence over Airbnb's guide.

## Whitespace
  - Use soft tabs set to 4 spaces.

    ```javascript
    // bad
    function() {
    ∙∙const name;
    }

    // bad
    function() {
    ∙const name;
    }

    // good
    function() {
    ∙∙∙∙const name;
    }
    ```
    
  - Place 1 space before the function keyword and the opening paren for anonymous functions. This does not count for named functions.

    ```javascript
    // bad
    function() {
        ...
    }
    
    // bad
    function getValue (element) {
        ...
    }

    // good
    function∙() {
        ...
    }
    
    // good
    function getValue(element) {
        ...
    }
    ```

## Naming Conventions
  - When saving a reference to `this` use `self`.

    ```javascript
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
