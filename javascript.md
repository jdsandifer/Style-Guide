# JavaScript Coding Standards

For almost all of our code style rules, refer to the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript).

When writing ES6 or React code (supported in files with a `.jsx` extension), please also refer to the [Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react).

There are a few things that we have customized for our tastes which will take presidence over Airbnb's guide.

## Functions
  - Always wrap the function expression for immediately-invoked function expressions (IIFE) in parens:

    ```javascript
    // bad
    (function () {
        console.log('Welcome to the Internet. Please follow me.');
    }());

    // good
    (function () {
        console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

## Whitespace
  - Use soft tabs set to 4 spaces.

    ```javascript
    // bad
    function () {
    ∙∙const name;
    }

    // bad
    function () {
    ∙const name;
    }

    // good
    function () {
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

  - Do not add spaces inside curly braces.

    ```javascript
    // bad
    const foo = { clark: 'kent' };

    // good
    const foo = {clark: 'kent'};
    ```

## Naming Conventions
  - When saving a reference to `this` use `self`.

    ```javascript
    // bad
    function () {
        var _this = this;
        return function () {
            console.log(_this);
        };
    }

    // bad
    function () {
        var that = this;
        return function () {
            console.log(that);
        };
    }

    // good
    function () {
        var self = this;
        return function () {
            console.log(self);
        };
    }
    ```
    
## React Specific Styles

* Do not use underscores when naming private methods. Most methods will be private, so just be sure to mark the public methods with `@public` in their method documentation.
* Do not add method documentation for the built-in [lifecycle methods](https://facebook.github.io/react/docs/component-specs.html) of a component.
* Do not add methods to your view that return pieces of things to render. Build those as [stateless components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) instead.
* Add descriptions to all propTypes using inline comments. No need to document the types, but add some context for each property so that other developers understand the intended use.

```javascript
// bad
{
  propTypes: {
    currency: React.PropTypes.string.isRequired,
    amount: React.PropTypes.number.isRequired,
    isIgnored: React.PropTypes.bool.isRequired
  }
}

// bad
{
  propTypes: {
    /**
     * The currency that the reward is in
     */
    currency: React.PropTypes.string.isRequired,
    /**
     * The amount of reward
     */
    amount: React.PropTypes.number.isRequired,
    /**
     * If the reward has been ignored or not
     */
    isIgnored: React.PropTypes.bool.isRequired
  }
}

// good
{
  propTypes: {
    // The currency that the reward is in
    currency: React.PropTypes.string.isRequired,
    // The amount of reward
    amount: React.PropTypes.number.isRequired,
    // If the reward has been ignored or not
    isIgnored: React.PropTypes.bool.isRequired
  }
}
```

* Use inline ternary statements when rendering optional pieces of templates. Notice the white space and formatting of the ternary.

```javascript
// bad
{
  render() {
    const optionalTitle = this.props.title ? <div className="title">{this.props.title}</div> : null;
    return (
      <div>
        {optionalTitle}
        <div className="body">This is the body</div>
      </div>
    );
  }
}

// good
{
  render() {
    return (
      <div>
        {this.props.title ?
          <div className="title">{this.props.title}</div>
        : null}
        <div className="body">This is the body</div>
      </div>
    );
  }
}

// good
{
  render() {
    return (
      <div>
        {this.props.title ?
          <div className="title">{this.props.title}</div>
        :
          <div className="title">Default Title</div>
        }
        <div className="body">This is the body</body>
      </div>
    );
  }
}
```

# JavaScript bits of no-ledge

## Module Pattern

When you hear "module pattern" in the context of javascript think singleton pattern. The way singletons or modules are usually implemented in js is by using a plain js object. Typically

We set variables and functions as properties of the object so you won't see prototype anywhere in a module.
Variables are prefixed with `_` since they're usually "private" to the module and if they're made available to the outside world it's usually through getters and setters
The [PubSub](https://github.com/Expensify/Mobile-Expensify/blob/c778eba328ea7de0f323bd1db99695576b9925aa/app/libs/pubSub.js) library is a perfect example of this pattern in use.

## Immediately Invoked Function Expression (IIFE)

The name is confusing and the syntax may feel strange if you've never seen it before but this is a very simple concept and what it allows you to do is declare a function and immediately call it, as the name suggests.

In Expensify this looks like this

```js
(function () {
    // function body
}());
```

and a perfect example of this is [setTimeout (on mobile)](https://github.com/Expensify/Mobile-Expensify/blob/18781e7c7115355a24fadcf04c6326f934ce4f7d/JavaScript/yapl.js#L218-L232).

```js
this.setTimeout = (function () {
    var id = 0;
    return function (fun, milliseconds) {
        yaplCall('yaplSetTimeout', fun, milliseconds);
        return ++id;
    };
}());
```

We only know of one **good reason** to use IIFEs and that is to **take advantage of closures**.

What the code above does is define a function that returns a closure and immediately invoke the function. You can think of a closure like a box with two things in it: a function and a context where the context is just a collection of variables that are available to the function. In the case above the IIFE defines (and invokes) a function that returns a closure: the inner function + the variable `id`.

Closures are used in js to emulate private variables. In js there's no such thing as private variables (surprise!) but by leveraging closures you can emulate private variables and this is illustrated in the `setTimeout` example above where the variable id is inaccessible from outside of that function.

Note that we **do not recommend using IIFEs to emulate private variables** in Expensify's code bases because the convention of prefixing private variables with an underscore serves the same purpose and allows you to access the variables from outside the function **for debugging purposes**: think about accessing these from the Safari / Chrome console while debugging our iOS or web app.

For the specific case of `setTimeout`, creating a module seemed like overkill for this and we need `setTimeout` to return a number but we don't think we're ever gonna need to inspect the value of `id`.

Also note that IIFEs make no sense in a modular JS environment since you export only what you want to expose and everything else remains private to the module.

Last, we'd advise against using it for dependency injection unless you're trying not to pollute scope since you can accomplish the same thing with clearer syntax. Consider the following example

```js
// Nothing exciting here, just defining two different app renderers
var ConsoleRenderer = {
    render: function (app) {
        console.log(app.name);
    }
};

var GrowlRenderer = {
    render: function (app) {
        yaplShowGrowl(app.name);
    }
};

// This illustrates the benefits of dependency injection
// as this is the only thing you'd need to change to use a different renderer
var appRenderer = ConsoleRenderer;
// var appRenderer = GrowlRenderer;

// The IIFE way
(function (renderer) {
    var app = {
        name: 'Carlos'
    };

    renderer.render(app);
}(appRenderer));

// The alternative with clearer syntax
// Note that in this case renderApplication is added to the current scope
// (which may well be the global scope)
function renderApplication(renderer) {
    var app = {
        name: 'Carlos'
    };

    renderer.render(app);
}

renderApplication(appRenderer);
```

## Publisher / Subscriber

This one isn't specific to js but we think it's worth mentioning because

1.- We use it heavily on web and mobile

2.- We should be using it more on mobile

3.- For new hires?

The publisher / subscriber pattern helps decouple objects from one another by changing the paradigm a bit from having objects directly call one another (thus coupling one to the public API of the other) to having objects publish (send / emit) events or messages while others subscribe (react) to them and using an event bus to send and receive these messages, which in our case is the `PubSub` library.

This is very useful when you have and event or action that is of interest to different parts of the application that are logically split and in different areas of the code. An example of this would be an event that causes different parts of the UI owned by different parts of the code to be updated.

On mobile for instance we publish the event `Event.REPORT_LIST_FETCHED` when we load reports from the servers to which both the expenses page and the reports page subscribe to and redraw the cells in the expenses list (we show the report name on the expenses list for reported expenses) and reports lists.

Note that if an object is publishing an event to which only that object is subcribed to, it's better to remove the event entirely and just call the handler directly. Said another way, there's no benefit to having an object adopt the publisher/subscriber pattern to communicate only with itself.

## Functions as first class citizens

Probably one of the most important concepts (and features!) **to understand** of JS is that functions are first-class citizens, which is a fancy way of saying that functions can be assigned to variables, passed as function parameters and returned from functions.

Something we see often is people creating unnecessary anonymous functions and passing them as parameters. Here's an example of what we mean

```js
API.BankAccount_Create({...})
  .done(function () {
    return deferred.resolve();
  }).unhandled(function () {
    return deferred.reject();
  });
```

Notice that `deferred.resolve` is a function and the `()` is just an operator to invoke that function but the important part here is that **`deferred.resolve` is a function**.

So what happens in the example above when the API request succeeds is

```
invoke done callbacks
invoke anonymous function
invoke deferred.resolve
```

Now a similar way of doing this is

```js
API.BankAccount_Create({...})
  .done(deferred.resolve)
  .unhandled(deferred.reject);
```

And the call stack for the successful case would be

```
invoke done callbacks
invoke deferred.resolve
```

While the two solutions are semantically equivalent (given that the wrapping anonymous functions have the same _contract_ than the ones that aren't wrapped)
they are logically different as one introduces a new anonymous function that in this particular case is unnecessary. This is unlikely to improve performance or affect the code in any way but we think it's important to understand the difference between the two implementations.

This isn't limited to functions that take no parameters, for example, imagine `API.GetReportSummary` returns a promise that resolves with a report name and status as two separate strings, that means that the function passed to the done callback takes two parameters (name, status), so

```js
// This
API.GetReportSummary({reportID: 123})
    .done(function (name, status) {
        logReportSummary(name, status);
    });

// Is (semantically) equivalent to
API.GetReportSummary({reportID: 123})
    .done(logReportSummary);

function logReportSummary(name, status) {
    console.log('Report Name:', name, 'Report Status:', status);
}
```

There are times however where a function that is passed as a parameter to another function depends on its context (ie, what `this` is bound to), and in that case it's important that `this` is set to the right thing. In the following example, the last two implementations are (semantically) equivalent since `.bind` returns a function and in the second example we're just creating an anonymous function on the fly.

```js
// Wrong
deletingExpense.done(this.fetchItems);

// Right
deletingExpense.done(this.fetchItems.bind(this));

// Right and more performant (keep reading)
var self = this;
deletingExpense.done(function () {
    self.fetchItems();
});
```


Note that using Function's `bind` to set the scope of `this` is extremely non-performant since it iterates through every single property of the object being bound to, which takes a lot of processing especially with large objects. Thus, using `self` has a very good performance benefit and thus is our preferred convention. A side tangent here is that with ES6, you can use arrow functions which removes the need for either of these, since arrow functions have a scope dead-zone with no `this` (using `this` will always reference `this` in the parent scope). With web, you can use any ES6 code if you give the file a **.jsx** extension in the **/site** directory.

## Anything else?

See [promises](https://github.com/Expensify/Mobile-Expensify/pull/4892#issue-108909111) and [queues](https://github.com/Expensify/Web-Expensify/blob/97a79e3d4fb6bd552edbfb2c580c3bb4f1cf9222/site/README.md#queue)!
