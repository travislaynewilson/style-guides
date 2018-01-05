# Travis' JavaScript Style Guide

*A reasonable approach to writing quality ES5 JavaScript code*

## Table of Contents

  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Functions](#functions)
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
  1. [ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  1. [Standard Library](#standard-library)
  1. [Testing](#testing)
  1. [Performance](#performance)
  1. [Resources](#resources)
  1. [In the Wild](#in-the-wild)
  1. [Translation](#translation)
  1. [The JavaScript Style Guide Guide](#the-javascript-style-guide-guide)
  1. [Chat With Us About JavaScript](#chat-with-us-about-javascript)
  1. [Contributors](#contributors)
  1. [License](#license)
  1. [Amendments](#amendments)



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

    // bad
    var obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker
    };

    // good
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
    const name = `Capt. Janeway`;
    
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
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

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



