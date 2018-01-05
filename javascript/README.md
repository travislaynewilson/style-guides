# Travis' JavaScript Style Guide

*A reasonable approach to writing quality ES5 JavaScript code*

## Table of Contents

  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Arrow Functions](#arrow-functions)
  1. [Classes & Constructors](#classes--constructors)
  1. [Modules](#modules)
  1. [Iterators and Generators](#iterators-and-generators)
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
  1. [ECMAScript 6+ (ES 2015+) Styles](#ecmascript-6-es-2015-styles)
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
    
  - **Avoid** trailing commas after the last property of an oject.

    > Why? Although most JS engines will gracefully ignore them, trailing commas are unnecessary and lazy.

    ```javascript
    /* avoid */
    var bad = {
      foo: 3,
      bar: 4,
    };

    /* good */
    var good = {
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
