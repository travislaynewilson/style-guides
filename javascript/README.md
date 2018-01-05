# Travis' ES5 JavaScript Style Guide

*My approach to writing quality ES5 JavaScript code*

## Table of Contents

  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Numbers](#numbers)
  1. [Functions](#functions)
  1. [Classes](#classes)
  1. [Properties](#properties)
  1. [Variables](#variables)
  1. [Hoisting](#hoisting)
  1. [Comparison Operators & Equality](#comparison-operators--equality)
  1. [Blocks](#blocks)
  1. [Control Statements](#control-statements)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Type Casting & Coercion](#type-casting--coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [Events](#events)
  1. [jQuery](#jquery)



## Objects

  - **Do** use the literal syntax for object creation.

    ```javascript
    /* avoid */
    var item = new Object();

    /* good */
    var item = {};
    ```


  - **Do** use property value shorthand when possible.

    > Why? It is shorter to write, descriptive and DRY.

    ```javascript
    var lukeSkywalker = 'Luke Skywalker';

    /* avoid */
    var obj = {
      lukeSkywalker: lukeSkywalker
    };

    /* good */
    var obj = {
      lukeSkywalker
    };
    ```

  - **Do** group your shorthand properties at the beginning of your object declaration.

    > Why? It’s easier to tell which properties are using the shorthand.

    ```javascript
    var anakinSkywalker = 'Anakin Skywalker',
        lukeSkywalker = 'Luke Skywalker';

    /* avoid */
    var obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker
    };

    /* good */
    var obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4
    };
    ```


  - **Do** define object properties with single quotes only if it has an invalid identifier.

    > Why? In general, we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

    ```javascript
    /* avoid */
    var bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5
    };

    /* good */
    var good = {
      foo: 3,
      bar: 4,
      'data-blah': 5
    };
    ```
    
  - **Consider** including [trailing commas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas) after the last property of an object.

    > Why? Trailing commas can make version-control diffs cleaner and editing code might be less troublesome.

    ```javascript
    /* valid in modern browsers and >IE9 */
    var trailing = {
      foo: 3,
      bar: 4,
    };

    /* valid in all browsers */
    var clean = {
      foo: 3,
      bar: 4
    };
    ```

  
  - **Avoid** calling `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.

    > Why? These methods may be shadowed by properties on the object in question - consider `{ hasOwnProperty: false }` - or, the object may be a null object (`Object.create(null)`).

    ```javascript
    /* avoid */
    console.log(object.hasOwnProperty(key));

    /* better */
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    /* best */
    var hasOwnProperty = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
    console.log(hasOwnProperty.call(object, key));
    ```

**[⬆ back to top](#table-of-contents)**





## Arrays

  - **Do** use the literal syntax for array creation.

    ```javascript
    /* avoid */
    var items = new Array();

    /* good */
    var items = [];
    ```


  - **Do** use [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) instead of direct assignment to add items to an array.

    ```javascript
    var someStack = [];

    /* avoid */
    someStack[someStack.length] = 'abracadabra';

    /* good */
    someStack.push('abracadabra');
    ```


  - **Do** Convert array-like objects to arrays using [Array.from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).
  
    > Note: Ensure that [Array.from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) is polyfilled into your application to support older browsers.

    ```javascript
    var foo = document.querySelectorAll('.foo');

    /* good */
    var nodes = Array.from(foo);
    ```
    
    
    - **Consider** including [trailing commas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas) after the last value in an array.

    > Why? Trailing commas can make version-control diffs cleaner and editing code might be less troublesome.

    ```javascript
    /* valid in modern browsers and >IE9 */
    var trailing = [1, 2, 3,];

    /* valid in all browsers */
    var clean = [1, 2, 3];
    ```


- **Do** use line breaks after open and before close array brackets if an array has multiple lines.
  
  > Why? In general, we consider it subjectively easier to read. 

    ```javascript
    /* avoid */
    var arr = [
      [0, 1], [2, 3], [4, 5]
    ];

    var objectInArray = [{
      id: 1
    }, {
      id: 2
    }];

    var numberInArray = [
      1, 2
    ];


    /* good */
    var arr = [[0, 1], [2, 3], [4, 5]];

    var objectInArray = [
      {
        id: 1
      },
      {
        id: 2
      }
    ];

    var numberInArray = [1, 2];
    ```

**[⬆ back to top](#table-of-contents)**





## Strings

  - **Do** use single quotes `''` for strings.

    ```javascript
    /* avoid */
    var name = "Capt. Janeway";
    
    /* avoid - template literals should contain interpolation or newlines */
    var name = `Capt. Janeway`;
    
    /* good */
    var name = 'Capt. Janeway';
    ```
    
    
  - **Consider** using string concatenation with arrays when writing multiple lines of HTML.

    > Why? String concatenation is painful to work with and make code less searchable. Most JS engines will support tabbed formatting in arrays.

    ```javascript
    /* avoid */
    var html = '<div> \
    Hello world! \
    </div>';

    /* avoid */
    var html = '<div>' +
      'Hello world!' +
      '</div>';

    /* better */
    var html = [
      '<div>',
        'Hello world!',
      '</div>'
    ].join();
    
    /* best - don't write HTML in your JavaScript! */
    ```

  - **Avoid** using string concatenation when writing text strings that cause the line to go over 100 characters.

    > Why? Broken strings are painful to work with and make code less searchable.

    ```javascript
    /* avoid */
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    /* avoid */
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    /* good */
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```


  - **Do** use template strings instead of concatenation when programmatically building up strings and the browser supports it.

    > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

    ```javascript
    /* avoid */
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    /* good */
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    /* best, if available */
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  - **Avoid** using `eval()` on a string.
  
    > Why? It opens too many vulnerabilities.
    
    ```javascript
    /* avoid */
    eval('alert("Hello world!")');
    ```
    

  - **Avoid** unnecessarily escaping characters in strings.

    > Why? Backslashes harm readability, thus they should only be present when necessary.

    ```javascript
    /* avoid */
    var foo = '\'this\' \i\s \"quoted\"';

    /* good */
    var foo = '\'this\' is "quoted"';
    var foo = `my name is '${name}'`;
    ```

**[⬆ back to top](#table-of-contents)**




## Numbers

  - **Avoid** using the global `isNaN`. Use `Number.isNaN` instead.
  
    > Why? The global `isNaN` coerces non-numbers to numbers, returning true for anything that coerces to `NaN`. If this behavior is desired, make it explicit.

    ```javascript
    /* avoid */
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true
    
    /* good */
    Number.isNaN('1.2'); // false
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```
    
    
  - **Avoid** using the global `isFinite`. Use `Number.isFinite` instead.
  
    > Why? The global `isFinite` coerces non-numbers to numbers, returning true for anything that coerces to a finite number. If this behavior is desired, make it explicit.

    ```javascript
    /* avoid */
    isFinite('2e3'); // true
    
    /* good */
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```
    
    
    
**[⬆ back to top](#table-of-contents)**




## Functions

  
  - **Do** wrap immediately invoked function expressions (IIFE) in parentheses.

    > Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.

    ```javascript
    /* avoid - although this works and saves us a character, it's more difficult to read */
    +function () {
      console.log('Welcome to the Internet. Please follow me.');
    }();
    
    /* avoid - does not include the invocation parens in the wrapping parens */
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    
    /* good */
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```


  - **Avoid** declaring functions in a non-function block (`if`, `while`, etc). Assign the function to a variable instead.
  
    > Why?  Browsers will allow you to do it, but they all interpret it differently.
    
    > Note: ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement.

    ```javascript
    /* avoid */
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    /* good */
    var test;
    if (currentUser) {
      test = function() {
        console.log('Yup.');
      };
    }
    ```
    
    
  - **Avoid** saving references to `this`. Use [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    > Why? Binding a function should be an explicit operation that demonstrates the developer's intent. Generally speaking, variables in functions are expected to be used to help the function execute it's purpose. Saving a reference to `this` adds another variable to the function scope that merely serves to reference itself as a context, which isn't generally expected.

    ```javascript
    /* avoid */
    function foo() {
      var self = this;
      
      return function () {
        console.log(self);
      };
    }


    /* avoid */
    function foo() {
      var that = this;
      
      return function () {
        console.log(that);
      };
    }


    /* good */
    function foo() {
      return (function() {
        console.log(this);
      }).bind(this);
    }
    ```


  - **Avoid** naming a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    /* avoid */
    function foo(name, options, arguments) {
      // ...
    }

    /* good */
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - **Consider** using rest syntax `...` instead of slicing `arguments`, if the browser supports it.

    > Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

    ```javascript
    /* ugly, but browser-safe */
    function concatenateAll() {
      var args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    /* better, if allowed */
    function concatenateAll(...args) {
      return args.join('');
    }
    ```


  - **Avoid** using the Function constructor to create a new function. 

    > Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

    ```javascript
    /* avoid */
    var add = new Function('a', 'b', 'return a + b');

    /* avoid */
    var subtract = Function('a', 'b', 'return a - b');
    
    /* good */
    var subtract = function(a, b) {
      return a - b;
    };
    ```


  - **Do** apply a space between the parens and the braces in a function signature.

    > Why? Consistency is nice.

    ```javascript
    /* avoid */
    var f = function(){};
    var g = function (){};

    /* good */
    var x = function() {};
    var y = function a() {};
    ```

  
  - **Avoid** mutating parameters. 

    > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

    ```javascript
    /* avoid */
    function f1(obj) {
      obj.key = 1;
    }

    /* good */
    function f2(obj) {
      var key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  - **Avoid** reassigning parameters.

    > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

    ```javascript
    /* avoid */
    function f1(a) {
      a = 1;
      // ...
    }

    /* avoid */
    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    /* good */
    function f3(a) {
      var b = a || 1;
      // ...
    }

    /* best, if supported */
    function f4(a = 1) {
      // ...
    }
    ```

  
  - **Do** indent functions with multiline signatures, or invocations, just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item.

    ```javascript
    /* avoid */
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    /* good */
    function foo(
      bar,
      baz,
      quux
    ) {
      // ...
    }

    /* avoid */
    console.log(foo,
      bar,
      baz);

    /* good */
    console.log(
      foo,
      bar,
      baz
    );
    ```

**[⬆ back to top](#table-of-contents)**



## Classes

  
  - **Do** create reusable classes whenever possible using prototype.

    > Why? Working with object-oriented code is wonderful.

    ```javascript
    /* avoid - does not support `new` keyword, private methods or static methods. */
    var AuthService = {
      someStaticMethod: function() {},
      somePrivateHelper: function() {},
      login: function(username, password) {},
      logout: function() {}
    };
 
 
    /* good */
    var AuthService = (function () {    
      // CTOR
      function AuthService() {}
      
      // Private helpers
      function somePrivateHelper() {}
      
      // Static methods
      AuthService.someStaticMethod = function() {};
            
      // Public methods
      AuthService.prototype.login = function(username, password) {};
      AuthService.prototype.logout = function() {};
      
      return AuthService;
    }());
    ```
    
    
  - **Do** extend classes and write base classes to be extended.

    > Why? Working with object-oriented code is so wonderful.

    ```javascript
    /**
     * Extends a class by applying a base class.
     * @param {class} d - The class to extend
     * @param {class} b - The base class
     */
    var extend = (function () {
        var extendStatics = Object.setPrototypeOf ||
            ({ __proto__: [] } instanceof Array && function (d, b) { d.__proto__ = b; }) ||
            function (d, b) { for (var p in b) if (b.hasOwnProperty(p)) d[p] = b[p]; };
        return function (d, b) {
            extendStatics(d, b);
            function __() { this.constructor = d; }
            d.prototype = b === null ? Object.create(b) : (__.prototype = b.prototype, new __());
        };
    })();
    ```
    ```javascript
    // Base class
    var Animal = (function () {
      function Animal(name) {
          this.name = name;
      }
      
      Animal.prototype.move = function (distanceInMeters) {
        if (distanceInMeters === void 0) { distanceInMeters = 0; }
        console.log(this.name + " moved " + distanceInMeters + "m.");
      };
      
      return Animal;
    }());
    
    
    // An implementation of `Animal`
    var Snake = (function (super) {
      extends(Snake, super);
      
      function Snake(name) {
        return super.call(this, name) || this;
      }
      
      Snake.prototype.move = function (distanceInMeters) {
        if (distanceInMeters === void 0) { distanceInMeters = 5; }
        console.log("Slithering...");
        super.prototype.move.call(this, distanceInMeters);
      };
      
      return Snake;
    }(Animal));
    
    
    // Try it out!
    var chupa = new Animal("A chupacabra");
    chupa.move();
    // > A chupacabra moved 0m.
    
    var sam = new Snake("Sammy the Python");
    sam.move(5);
    // > Slithering...
    // > Sammy the Python moved 5m.  
    ```
    
    
**[⬆ back to top](#table-of-contents)**



## Properties

  - **Do** use dot notation when accessing properties.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    /* avoid when possible */
    var isJedi = luke['jedi'];

    /* good */
    var isJedi = luke.jedi;
    ```

  
  - **Do** use bracket notation `[]` when accessing properties with a variable.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```
    

**[⬆ back to top](#table-of-contents)**




## Variables

  - **Do** use `var` to declare variables.
  
    > Why? Not doing so will result in global variables. We want to avoid polluting the global namespace.

    ```javascript
    /* avoid */
    superPower = new SuperPower();

    /* good */
    var superPower = new SuperPower();
    ```


  - **Do** use one `var` declaration for multiple variables.

    > Why? It’s easier to add new variable declarations this way, and you reduce the risk of leaving off a `var` and creating a global variable.

    ```javascript
    /* avoid */
    var foo;
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';

    /* good */
    var foo,
        items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
    ```


  - **Avoid** chaining variable assignments.

    > Why? Chaining variable assignments creates implicit global variables.

    ```javascript
    /* avoid */
    (function example() {
      // JavaScript interprets this as:
      // let a = ( b = ( c = 1 ) );
      // The `var` keyword only applies to variable a; variables b and c become global variables.
      var a = b = c = 1;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // 1
    console.log(c); // 1

    /* good */
    (function example() {
      var a = 1;
      var b = a;
      var c = a;
    }());

    console.log(a); // throws ReferenceError
    console.log(b); // throws ReferenceError
    console.log(c); // throws ReferenceError
    ```

  
  - **Avoid** using unary increments and decrements (++, --).

    > Why? Unary increment and decrement statements are subject to automatic semicolon insertion and can cause silent errors with incrementing or decrementing values within an application. It is also more expressive to mutate your values with statements like `num += 1` instead of `num++` or `num ++`. Disallowing unary increment and decrement statements also prevents you from pre-incrementing/pre-decrementing values unintentionally which can also cause unexpected behavior in your programs.

    ```javascript
    /* avoid */
    var array = [1, 2, 3],
        num = 1;
    num++;
    --num;

    /* good */
    var array = [1, 2, 3],
        num = 1;
    num += 1;
    num -= 1;
    ```

**[⬆ back to top](#table-of-contents)**




## Hoisting

  - **Do** declare your `var` declarations before you reference it.  

**[⬆ back to top](#table-of-contents)**




## Comparison Operators & Equality

  - **Do** use `===` and `!==` over `==` and `!=`. 

  - **Understand** that conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    - **Objects** evaluate to **true**
    - **Undefined** evaluates to **false**
    - **Null** evaluates to **false**
    - **Booleans** evaluate to **the value of the boolean**
    - **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    - **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0] && []) {
      // true
      // an array (even an empty one) is an object, objects will evaluate to true
    }
    ```

  
  - **Do** use shortcuts for booleans when possible. Prefer explicit comparisons for strings.

    ```javascript
    /* avoid - too verbose */
    if (isValid === true) {
      // ...
    }

    /* good */
    if (isValid) {
      // ...
    }

    /* avoid - not enough info to accurately evaluate this string as a boolean
    if (name) {
      // ...
    }

    /* good */
    if (name !== '') {
      // ...
    }

    /* good, but verbose because 0 is falsey
    if (collection.length > 0) {
      // ...
    }

    /* good */
    if (collection.length) {
      // ...
    }

    ```


  - **Avoid** checking for `undefined` using the keyword `undefined`. Use `void 0` instead.
  
    > Why? `undefined` is actually a global property, not a keyword. `undefined` can be changed, where as `void` is an operator which cannot be overridden in JavaScript and is used to obtain the `undefined` primitive value.
      
    ```javascript
    var x = undefined;
    console.log(x);
    // > undefined

    var undefined = 1;
    var y = undefined;
    console.log(y);
    // > 1
    
    console.log(void 0);
    // > undefined
    ```
    

  - **Avoid** nesting ternary expressions. Try to format them as single line expressions if readability doesn't suffer.

    ```javascript
    /* avoid - nesting */
    var foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;      
      
    /* avoid - poor readability */
    var foo = originalValue > newValue ? 'The value has changed' : 'The value has not changed at all. Better luck next time!';

    /* good */
    var foo = originalValue > newValue
      ? 'The value has changed'
      : 'The value has not changed at all. Better luck next time!';

    /* good */
    var foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  - **Avoid** unneeded ternary statements.

    ```javascript
    /* avoid */
    var foo = a ? a : b;
    var bar = c ? true : false;
    var baz = c ? false : true;

    /* good */
    var foo = a || b;
    var bar = !!c;
    var baz = !c;
    ```

  - **Do** enclose operators in parentheses when they are mixed in a statement. When mixing arithmetic operators, do not mix `**` and `%` with themselves or with `+`, `-`, `*`, & `/`.

    > Why? This improves readability and clarifies the developer’s intention.

    ```javascript
    /* avoid */
    var foo = a && b < 0 || c > 0 || d + 1 === 0;

    /* avoid */
    var bar = a ** b - 5 % d;

    /* avoid - one may be confused into thinking (a || b) && c */
    if (a || b && c) {
      return d;
    }

    /* good */
    var foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    /* good */
    var bar = (a ** b) - (5 % d);

    /* good */
    if (a || (b && c)) {
      return d;
    }

    /* good */
    var bar = a + b / c * d;
    ```

**[⬆ back to top](#table-of-contents)**




## Blocks

  - **Do** use braces with all multi-line blocks.

    ```javascript
    /* avoid */
    if (test)
      return false;

    /* avoid */
    if (test) return false;

    /* good */
    if (test) {
      return false;
    }

    /* avoid */
    function foo() { return false; }

    /* good */
    function bar() {
      return false;
    }
    ```

  
  - **Do** put `else` on the same line as your `if` block’s closing brace if you're using multi-line blocks with `if` and `else`.
  
    ```javascript
    /* avoid */
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    /* good */
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  
  - **Avoid** providing an `else` block if it's `if` block always executes a `return` statement. A `return` in an `else if` block following an `if` block that contains a `return` can be separated into multiple `if` blocks.

    ```javascript
    /* avoid */
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    /* avoid */
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    /* avoid */
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    /* good */
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    /* good */
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    /* good */
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ back to top](#table-of-contents)**




## Control Statements


  - **Do** put each (grouped) condition onto a new line when your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length. The logical operator should begin the line.

    > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

    ```javascript
    /* avoid */
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    /* avoid */
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    /* avoid */
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    /* avoid */
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    /* good */
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    /* good */
    if (
      (foo === 123 || bar === "abc")
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    /* good */
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

**[⬆ back to top](#table-of-contents)**





## Comments

  - **Do** use `/** ... */` for multi-line comments.

    ```javascript
    /* avoid */
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {
      // ...
      return element;
    }

    /* good */
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {
      // ...
      return element;
    }
    ```


  - **Do** use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

    ```javascript
    /* avoid */
    var active = true;  // is current tab

    /* good */
    // is current tab
    var active = true;

    /* avoid - no line above the comment */
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this.type || 'no type';

      return type;
    }

    /* good */
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this.type || 'no type';

      return type;
    }

    /* good */
    function getType() {
      // set the default type to 'no type'
      var type = this.type || 'no type';

      return type;
    }
    ```


  - **Do** start all comments with a space to make it easier to read.

    ```javascript
    /* avoid */
    //is current tab
    var active = true;

    /* good */
    // is current tab
    var active = true;

    /* avoid */
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {
      // ...
      return element;
    }

    /* good */
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {
      // ...
      return element;
    }
    ```


  - **Do** prefix your actionable comments with `TODO[Name]` to help other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. 

    ```javascript
    function make(tag) {
      // TODO[Travis]: We should probably do something here.
      return element;
    }
    ```
    
    
  - **Do** document your classes, functions, properties using [JSDoc](http://usejsdoc.org/) syntax.

    ```javascript
    /* avoid */
    // Adds two numbers together
    function add(a, b) {
      return a + b;
    }
    
    /* good */
    /**
     * Adds two numbers together
     * @param {number} a - The first value
     * @param {number} b - The second value
     * @return {number} The result of both values added together
     */
    function add(a, b) {
      return a + b;
    }
    ```
    
    
  - **Avoid** committing commented-out code into version control.
  
    > Why? Old, unused code in source control leads to polluted source code.

    ```javascript
    /* avoid */
    /* function make(tag) {
      return element;
    }*/
    ```

**[⬆ back to top](#table-of-contents)**




## Whitespace

  
  - **Do** place 1 space before the leading brace.
    ```javascript
    /* avoid */
    function test(){
      console.log('test');
    }

    /* good */
    function test() {
      console.log('test');
    }

    /* avoid */
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    /* good */
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  
  - **Do** place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space between the argument list and the function name in function calls and declarations.

    ```javascript
    /* avoid */
    if(isJedi) {
      fight ();
    }

    /* good */
    if (isJedi) {
      fight();
    }

    /* avoid */
    function fight () {
      console.log ('Swooosh!');
    }

    /* good */
    function fight() {
      console.log('Swooosh!');
    }
    ```


  - **Do** set off operators with spaces.

    ```javascript
    /* avoid */
    var x=y+5;

    /* good */
    var x = y + 5;
    ```

  
  - **Do** end files with a single newline character.

    ```javascript
    /* avoid */
    require(['es6'], function(es6) {
      // ...
    });
    ```

    ```javascript
    /* avoid */
    require(['es6'], function(es6) {
      // ...
    });↵
    ↵
    ```

    ```javascript
    /* good */
    require(['es6'], function(es6) {
      // ...
    });↵
    ```


  - **Do** use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
    emphasizes that the line is a method call, not a new statement. 

    ```javascript
    /* avoid */
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    /* avoid */
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    /* good */
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    /* avoid */
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    /* good */
    var leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    /* good */
    var leds = stage.selectAll('.led').data(data);
    ```


  - **Do** leave a blank line after blocks and before the next statement.

    ```javascript
    /* avoid */
    if (foo) {
      return bar;
    }
    return baz;


    /* good */
    if (foo) {
      return bar;
    }

    return baz;
    ```



  - **Avoid** padding your blocks with blank lines.

    ```javascript
    /* avoid */
    function bar() {

      console.log(foo);

    }

    /* avoid */
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    /* good */
    function bar() {
      console.log(foo);
    }

    /* good */
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  - **Avoid** adding spaces inside parentheses.

    ```javascript
    /* avoid */
    function bar( foo ) {
      return foo;
    }

    /* good */
    function bar(foo) {
      return foo;
    }

    /* avoid */
    if ( foo ) {
      console.log(foo);
    }

    /* good */
    if (foo) {
      console.log(foo);
    }
    ```


  - **Avoid** adding spaces inside brackets.

    ```javascript
    /* avoid */
    var foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    /* good */
    var foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  
  - **Do** add spaces inside curly braces.

    ```javascript
    /* avoid */
    var foo = {clark: 'kent'};

    /* good */
    var foo = { clark: 'kent' };
    ```


  - **Avoid** having lines of code that are longer than 100 characters (including whitespace). 
  
    > Why? This ensures readability and maintainability.
    
    > Note: Per [above](#strings--line-length), long strings are exempt from this rule and should not be broken up.

    ```javascript
    /* avoid */
    var foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    /* avoid */
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    /* good */
    var foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    /* good */
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' }
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

**[⬆ back to top](#table-of-contents)**




## Commas

  - **Avoid** leading commas: 

    ```javascript
    /* avoid */
    var story = [
        once
      , upon
      , aTime
    ];

    /* good */
    var story = [
      once,
      upon,
      aTime
    ];

    /* avoid */
    var hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    /* good */
    var hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers'
    };
    ```

  
  - **Consider** adding additional trailing commas.

    > Why? This can lead to cleaner version diffs. Also, transpilers like Babel and TypeScript will remove the additional trailing comma in the transpiled code, which means you don’t have to worry about the trailing comma problem in legacy browsers (if you're using a transpiler).

    ```diff
    /* ugly - git diff without trailing comma */
    var hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    /* good - git diff with trailing comma */
    var hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    /* clean */
    var hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    var heroes = [
      'Batman',
      'Superman'
    ];

    /* trailing */
    var hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    var heroes = [
      'Batman',
      'Superman',
    ];

    /* clean */
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    /* trailing */
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }
    ```

**[⬆ back to top](#table-of-contents)**




## Semicolons


  - **Do** include semicolors after each statement and expression.

    > Why? When JavaScript encounters a line break without a semicolon, it uses a set of rules called [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether or not it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. These rules will become more complicated as new features become a part of JavaScript. Explicitly terminating your statements and configuring your linter to catch missing semicolons will help prevent you from encountering issues.

    ```javascript
    /* avoid - raises exception */
    var luke = {}
    var leia = {}
    [luke, leia].forEach(jedi => jedi.father = 'vader')

    /* avoid - raises exception */
    var reaction = "No! That's impossible!"
    (function meanwhileOnTheFalcon(){
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    /* avoid - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI! */
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    /* good */
    var luke = {},
    var leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    /* good */
    var reaction = "No! That's impossible!";
    (function meanwhileOnTheFalcon(){
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    /* good */
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

**[⬆ back to top](#table-of-contents)**




## Type Casting & Coercion

  
  - **Do** perform type coercion at the beginning of the statement.

  
  - **Do** coerce strings using the `String` global object

    ```javascript
    this.reviewScore = 9;

    /* avoid - typeof totalScore is "object", not "string" */
    var totalScore = new String(this.reviewScore);

    /* avoid - invokes this.reviewScore.valueOf()*/
    var totalScore = this.reviewScore + '';

    /* avoid - isn’t guaranteed to return a string */
    var totalScore = this.reviewScore.toString();

    /* good */
    var totalScore = String(this.reviewScore);
    ```

  
  - **Do** coerce numbers using the `Number` global object and `parseInt`. When using `parseInt`, provide a radix to clarify the base in the intended mathematical numeral system (usually 10 for the decimal numeral system commonly used by humans).

    > Why? Defining the radix when using `parseInt` eliminates reader confusion and guarantees predictable behavior. Different implementations produce different results when a radix is not specified.
    
    ```javascript
    var inputValue = '4';

    /* avoid - typeof val is "object", not "number" */
    var val = new Number(inputValue);

    /* avoid - coercion is far less performant than `parseInt` in Chrome */
    var val = +inputValue;

    /* avoid - bitshifting is far less performant than `parseInt` in Firefox in most cases */
    var val = inputValue >> 0;

    /* avoid - no radix defined */
    var val = parseInt(inputValue);

    /* good */
    var val = Number(inputValue);

    /* good */
    var val = parseInt(inputValue, 10);
    ```

  
  - **Consider** using bitshift to coerce a number if, for whatever reason, you are doing something wild and `parseInt` is a  bottleneck for [performance reasons](https://jsperf.com/coercion-vs-casting/3). Leave a comment explaining why and what you're doing.

    > Note:  Be careful when using bitshift operations. Numbers are represented as 64-bit values, but bitshift operations always return a 32-bit integer ([source](https://es5.github.io/#x11.7)). Bitshifting can lead to unexpected behavior for integer values larger than 32 bits. Largest signed 32-bit integer is 2,147,483,647.
    
    ```javascript
    /* good */
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```


  - **Understand** that bitshift operations always return a 32-bit integer ([source](https://es5.github.io/#x11.7)). Numbers are natively represented as 64-bit values. Bitshifting can lead to unexpected behavior for integer values larger than 32 bits. Largest signed 32-bit integer is 2,147,483,647.

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  
  - **Do** coerce booleans using coercion. The `Boolean` global object can also be used, but is more verbose.

    ```javascript
    var age = 0;

    /* avoid - typeof hasAge is "object", not "boolean" */
    var hasAge = new Boolean(age);

    /* good */
    var hasAge = Boolean(age);

    /* best */
    var hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**




## Naming Conventions

  
  - **Avoid** single letter names. Be descriptive with your naming.

    ```javascript
    /* avoid */
    function q() {
      // ...
    }

    /* good */
    function query() {
      // ...
    }
    ```

  
  - **Do** use camelCase when naming objects, functions, and instances.

    ```javascript
    /* avoid */
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {}

    /* good */
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  
  - **Do** use PascalCase only when naming constructors or classes. 

    ```javascript
    /* avoid */
    function user(options) {
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    /* good */
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    var good = new User({
      name: 'yup'
    });
    ```

  
  - **Avoid** using trailing or leading underscores.

    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won’t count as breaking, or that tests aren’t needed. tl;dr: if you want something to be “private”, it must not be observably present.

    ```javascript
    /* avoid */
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';
    var _firstName = 'Panda';
    function _add() {}

    /* good */
    this.firstName = 'Panda';
    var firstName = 'Panda';
    function add() {}
    ```


  - **Do** name acronyms and initialisms as all capitalized, or all lowercased.

    > Why? Names are for readability, not to appease a computer algorithm.

    ```javascript

    /* avoid */
    var HttpRequests = [
      // ...
    ];

    /* good */
    var HTTPRequests = [
      // ...
    ];

    /* good */
    var httpRequests = [
      // ...
    ];
    ```
    
    
  - **Do** name a boolean property/method with a verb prefix to represent the value as a state, such as `isVal` or `hasVal` instead of `val`.

    ```javascript
    /* avoid */
    var old = false;
    if (!dragon.age()) {
      return false;
    }

    /* good */
    var isOld = false;
    if (!dragon.hasAge()) {
      return false;
    }
    ```
    
    
  - **Do** use consistent file names for all assets named after what they represent. Use only lowercase file names. Use dashes to separate words, acronyms and initialisms in the file name.

    ```javascript
    export function SessionContext() {
      // ...
    }

    /* avoid */
    SessionContext.js
    sessionContext.js
    Session-Context.js    
    
    /* good */
    session-context.js
    ```
    
      
  - **Do** use conventional type names when applicable, including a suffix like `.service`, `.store`, `.module` and `.util`. Avoid using appreviated type names, such as `.svc`. Invent additional type names if you feel it's appropriate, but take care not to create too many.

    > Why? Type names provide a consistent way to quickly identify what is in the file, and make searching for a specific file type easy using many IDE's search techniques.

    ```javascript
    export function UserAuthService() {
      // ...
    }

    /* avoid */
    user-auth.js
    user-auth-service.js
    user-auth.service.js
    user-auth.svc.js    
    
    /* good */
    user-auth.service.js
    ```
    
    
    
  - **Do** name test specification files the same as the file they test, followed with the suffix `.spec`.

    > Why? The suffix `.spec` provides a consistent way to quickly identify tests and provides pattern matching for [Karma](http://karma-runner.github.io/) and other test runners. It also helps the file and it's tests stay together in IDE file trees.

    ```javascript
    user-auth.service.js

    /* avoid */
    spec.user-auth.service.js
    user-auth-service.spec.js
    user-auth.spec.js

    /* good */
    user-auth.service.spec.js
    ```
    

**[⬆ back to top](#table-of-contents)**




## Accessors


  - **Avoid** using JavaScript getters/setters. Instead, if you do make accessor functions, use getVal() and setVal('hello').
  
    > Why? They cause unexpected side effects and are harder to test, maintain and reason about. 
  
    ```javascript
    /* avoid */
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }
    
    /* avoid */
    class Dragon {
      Object.defineProperty(this, 'age', {
        get: function() {
            // ...
        },
        set: function(value) {
            // ...
        }
      });
    }

    /* good */
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```


  - **Do** create get() and set() functions in objects when appropriate, but be consistent.

    ```javascript
    var Jedi = (function() {
      function Jedi(options) {
        var lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      Jedi.prototype.set = function(key, val) {
        this[key] = val;
      };

      Jedi.prototype.set = function(key) {
        return this[key];
      };
      
      return Jedi;
    });
    ```
    
    
**[⬆ back to top](#table-of-contents)**




## Events

  
  - **Do** pass an object literal instead of a raw value when attaching data payloads to events.
  
    > Why? This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event.

    ```javascript
    /* avoid */
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingId) => {
      // do something with listingId
    });
    ```

    ```javascript
    /* good */
    $(this).trigger('listingUpdated', { listingId: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingId
    });
    ```


  - **Do** use namespace suffixes when creating and triggering custom events. Choose namespaces that represent the feature that the event is related to.
  
    > Why? Namespace suffixes allow developers to determine if an event belongs to a specific feature, and allows for more convenient unbinding and management by following a consistent naming convention.

    ```javascript
    /* avoid - no namespace for this custom event */
    $(this).trigger('updated');
    
    /* avoid - namespace words not separated by dashes */
    $(this).trigger('updated.mycache');
    
    /* avoid - namespace in prefix */
    $(this).trigger('mycache.updated');
    
    /* avoid - click fired in custom feature not namespaced */
    $(this).trigger('click');
    
    /* good */
    $(this).trigger('updated.my-cache');
    $(this).trigger('click.my-feature');
    ```

  **[⬆ back to top](#table-of-contents)**



## jQuery

  - **Consider** not using jQuery in your application.
  
    > Why? The best quality web JavaScript code separates the model from the view, and is written to be testable and object-oriented. Direct access to the DOM results in your JavaScript being tightly-coupled to your view. It also encourages the view to contain state, which makes testing very difficult. jQuery's ease of use and low barrier-to-entry makes it tempting to query the DOM frequently, and with modern browsers becoming more performant each year, it's easy to miss performance concerns on weaker computers and mobile devices. Lastly, there are far superior techniques and patterns for working with the DOM that have become popular since jQuery, such as [VueJS](https://vuejs.org/). jQuery is now despised by most modern web developers, who consider it antiquated, slow (relative to other solutions), unscalable and responsible for many poorly-trained developers, anti-patterns and poorly-written websites present on the web today.

  
  - **Do** prefix jQuery object variables with a `$`.

    ```javascript
    /* avoid */
    var sidebar = $('.sidebar');

    /* good */
    var $sidebar = $('.sidebar');

    /* good */
    var $sidebarBtn = $('.sidebar-btn');
    ```

  
  - **Do** cache jQuery lookups.

    ```javascript
    /* avoid */
    function setSidebar() {
      $('.sidebar').hide();
    }

    /* good */
    function setSidebar() {
      var $sidebar = $('.sidebar');
      
      $sidebar.hide();
    }
    ```
    
    
  - **Do** chain jQuery operations when two or more operations are used.

    ```javascript
    /* avoid */
    function setSidebar() {
      var $sidebar = $('.sidebar');
    
      $sidebar.hide();
      $sidebar.css({
        'background-color': 'pink'
      });
    }

    /* good */
    function setSidebar() {
      var $sidebar = $('.sidebar');
      
      $sidebar
        .hide()
        .css({
          'background-color': 'pink'
        });
    }
    ```
    
    
  - **Do** modify parent and child selectors in a chain using traversal methods like `.find()`, `.children()`, `.siblings()`, `.parent()` and `.end()`.
  
    > Why? Traversing and reverse-traversing in a chain is very performant and reduces the number of DOM cycles that need to be made.

    ```javascript
    /* avoid - too many DOM queries */
    function setSidebar() {
      $('ul.first').find('.foo').css('background-color', 'red');
      $('ul.first').find('.bar').css('background-color', 'green');
    }

    /* good */
    function setSidebar() {
      $('ul.first')
        .find('.foo')
          .css('background-color', 'red')
        .end()
        .find('.bar')
          .css('background-color', 'green');
    }
    ```
    
    
  - **Do** contextualize your DOM queries when working in elements that may appear somewhere else on the page.
  
    > Why? Without contextualization, your DOM queries could affect unintended elements.

    ```html
    <div id="mywidget">
      <section class="card">
        <header class="card-header">
          <h4 class="card-title">Weather</h4>
        </header>
        <article class="card-body">
          <p>Sunny!</p>
        </article>
      </section>
    </div>
    ```
    ```javascript
    /* avoid */
    $('.card').hide();

    /* good */
    var $context = $('#mywidget');
    $('.card', $context).hide();
    ```
    
    
    
  - **Do** start all DOM queries from an ID when an ID is available and reasonably-positioned near your desired element(s), and traverse from there.
  
    > Why? Querying DOM elements by ID is much faster and more performant than querying by class names or `[data]` attributes.

    ```html
    <section class="card" id="mycard">
      <header class="card-header">
        <h4 class="card-title">Weather</h4>
      </header>
      <article class="card-body">
        <p>Sunny!</p>
      </article>
    </section>
    ```
    ```javascript
    /* avoid */
    var title = $('.card .card-title').text();
    var title = $('.card').find('.card-title').text();

    /* good */
    var title = $('#mycard').find('.card-title').text();
    ```
    
    
  - **Avoid** unnecessarily-precise selectors when possible. Opt for the loosest query possible.
  
    > Why? The more precise a selector is, the more tightly-coupled the jQuery call is to the current DOM structure. This makes future style changes more difficult.

    ```html
    <section class="card" id="mycard">
      <header class="card-header">
        <h4 class="card-title">Weather</h4>
      </header>
      <article class="card-body">
        <p>Sunny!</p>
      </article>
    </section>
    ```
    ```javascript
    /* avoid - expects certain DOM elements to be used, which might not be necessary */
    var title = $('section#mycard h4.card-title').text();    
    
    /* avoid - rigid nesting structure is overkill */
    var title = $('.card .card-header .card-title').text();

    /* good - starts with an ID and it's lean */
    var title = $('#mycard .card-title').text();
    ```
    
    
  - **Avoid** creating CSS classes solely to query DOM elements in jQuery. Use existing IDs and classes to query DOM elements, and create `[data-attributes]` when none exist.
  
    > Why? CSS classes are expected to have styles defined. A CSS class with no styles is confusing and messy to anyone not working on the JavaScript at that time, and is likely to be removed without knowing how it's used in jQuery. This is made more dangerous considering that there would likely be no tests to check for this.

    ```css
    <style>
      #site-nav {  }
    </style>
    ```
    ```javascript    
    /* avoid */
    <nav id="site-nav" class="mynav"></nav>
    
    var $nav = $('.mynav');
    

    /* good */
    <nav id="site-nav"></nav>
    
    var $nav = $('#site-nav');
    
    
    /* best */
    <nav id="site-nav" [data-nav]="site"></nav>
    
    var $nav = $('[data-nav="site"]');
    ```
    
    
  - **Do** use object literal syntax when creating new DOM elements in memory.

    ```javascript
    /* avoid */
    var $div = $('<div class="foo"></div>');
    
    /* avoid */
    var $div = $('<div></div>');
    $div.addClass('foo');

    /* good */
    var $div = $('<div />', {
      class: 'foo'
    });
    ```

  
  - **Do** cascading `$('parent descendant')`, parent > child `$('parent > child')` or `.find()`/`.children()` for DOM queries. Use context selectors only if your context is stored in an object reference.

    ```javascript
    /* avoid */
    $('ul', '.sidebar').hide();
    $('.sidebar').find('ul').hide();

    /* good */
    $('ul', $sidebar).hide();
    $('.sidebar > ul').hide();
    $sidebar.find('ul').hide();
    $sidebar.children('ul').hide();
    ```
    
    
  - **Do** use shorthand for `$(document).ready()`.

    ```javascript
    /* avoid */
    $(document).ready(function() {});
    $(window).on('load', function() {});

    /* good */
    $(function() {});
    ```
    
    
  - **Do** use delegated event handlers.
  
    > Why? Delegated event handlers are only registered to a single element, work for any decendents in the DOM, work for static- and dynamically-injected DOM elements and result in a more performant experience, thanks to [JavaScript event bubbling](https://en.wikipedia.org/wiki/Event_bubbling).

    ```javascript
    /* avoid */
    $('.form .submit').on('click', function() {});

    /* good */
    $('.form').on('click', '.submit', function() {});
    ```
    
    
  - **Consider** throttling or debouncing certain event handlers, like window resizing, to maximize performance.
