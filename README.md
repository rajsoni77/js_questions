# Javasript_Essentials

---
**JavaScript Questions (General)**
---

1.  **What are the different data types present in javascript?**
    *   **Primitives:**
        1.  `String`: Textual data (e.g., `"hello"`).
        2.  `Number`: Numeric values (e.g., `100`, `3.14`). Includes `Infinity`, `-Infinity`, and `NaN`.
        3.  `Boolean`: Logical values (e.g., `true`, `false`).
        4.  `Null`: Represents the intentional absence of any object value (e.g., `null`). Its type is `object` (a historical quirk).
        5.  `Undefined`: Represents a variable that has been declared but not yet assigned a value (e.g., `undefined`).
        6.  `Symbol` (ES6): Unique and immutable primitive value, often used as object property keys (e.g., `Symbol('id')`).
        7.  `BigInt` (ES2020): Represents integers with arbitrary precision (e.g., `123n`).
    *   **Non-Primitive (Reference Type):**
        1.  `Object`: Collections of key-value pairs. Includes arrays, functions, dates, etc. (e.g., `{ name: "Alice" }`, `[1, 2]`, `function() {}`).

    ```javascript
    console.log(typeof "hello");     // "string"
    console.log(typeof 100);         // "number"
    console.log(typeof true);        // "boolean"
    console.log(typeof null);        // "object" (historical quirk)
    console.log(typeof undefined);   // "undefined"
    console.log(typeof Symbol('id'));// "symbol"
    console.log(typeof 123n);        // "bigint"
    console.log(typeof {a: 1});      // "object"
    console.log(typeof [1, 2]);      // "object" (arrays are objects)
    console.log(typeof function(){});// "function" (functions are objects)
    ```

2.  **Explain Hoisting in javascript.**
    Hoisting is JavaScript's default behavior of moving declarations to the top of their current scope (function scope for `var`, block scope for `let`/`const`) during the compilation phase. However, only declarations are hoisted, not initializations. `let` and `const` are hoisted but are not initialized and remain in a "Temporal Dead Zone" (TDZ) until their declaration is encountered.

    ```javascript
    // Example with var
    console.log(myVar); // undefined (declaration hoisted, initialization not)
    var myVar = 5;
    console.log(myVar); // 5

    // Example with let (TDZ)
    // console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
    let myLet = 10;
    console.log(myLet); // 10

    // Function hoisting
    greet(); // "Hello!" (function declaration is fully hoisted)
    function greet() {
      console.log("Hello!");
    }
    ```

3.  **Why do we use the word “debugger” in javascript?**
    The `debugger` keyword is used to programmatically invoke any available debugging functionality, such as setting a breakpoint. If a debugger (like browser developer tools) is active, the code execution will pause at the `debugger` statement. If no debugger is active, this statement has no effect.

    ```javascript
    function calculateSum(a, b) {
      let result = a + b;
      debugger; // Execution will pause here if DevTools is open
      console.log("Result is:", result);
      return result;
    }
    calculateSum(5, 10);
    ```

4.  **Difference between “ == “ and “ === “ operators.**
    *   `==` (Abstract Equality Comparison): Compares two values for equality **after performing type coercion** if the types are different.
    *   `===` (Strict Equality Comparison): Compares two values for equality **without performing type coercion**. Both value and type must be the same.

    ```javascript
    console.log(5 == "5");    // true (string "5" is coerced to number 5)
    console.log(5 === "5");   // false (types are different: number vs string)

    console.log(0 == false);  // true (boolean false is coerced to number 0)
    console.log(0 === false); // false (types are different: number vs boolean)

    console.log(null == undefined); // true (special case)
    console.log(null === undefined);// false (types are different)
    ```
    **Recommendation:** Generally, use `===` to avoid unexpected behavior due to type coercion.

5.  **Difference between var and let keyword in javascript.**
    | Feature          | `var`                                    | `let`                                       |
    | :--------------- | :--------------------------------------- | :------------------------------------------ |
    | **Scope**        | Function-scoped or globally-scoped       | Block-scoped (`{}`)                         |
    | **Hoisting**     | Hoisted and initialized with `undefined` | Hoisted but not initialized (Temporal Dead Zone) |
    | **Re-declaration** | Can be re-declared in the same scope   | Cannot be re-declared in the same scope   |
    | **Global Object**| Creates a property on the global object when declared globally | Does not create a property on the global object when declared globally |

    ```javascript
    // Scope
    function scopeTest() {
      if (true) {
        var varVariable = "I am var";
        let letVariable = "I am let";
      }
      console.log(varVariable); // "I am var" (var is function-scoped)
      // console.log(letVariable); // ReferenceError: letVariable is not defined (let is block-scoped)
    }
    scopeTest();

    // Hoisting
    console.log(x); // undefined (var x is hoisted)
    var x = 10;
    // console.log(y); // ReferenceError (let y is in TDZ)
    let y = 20;

    // Re-declaration
    var a = 1;
    var a = 2; // Allowed
    console.log(a); // 2

    let b = 1;
    // let b = 2; // SyntaxError: Identifier 'b' has already been declared
    ```

6.  **Explain Implicit Type Coercion in javascript.**
    Implicit type coercion is the automatic conversion of a value from one data type to another by the JavaScript engine when an operation involves different types. This happens "behind the scenes."

    ```javascript
    console.log(5 + "5");      // "55" (number 5 is coerced to string "5")
    console.log("10" - 5);     // 5 (string "10" is coerced to number 10)
    console.log("5" * "2");    // 10 (both strings coerced to numbers)
    console.log(true + 1);     // 2 (boolean true is coerced to number 1)
    console.log(null + 7);     // 7 (null is coerced to 0)
    if ("hello") {             // "hello" is coerced to true in a boolean context
      console.log("Truthy!");
    }
    ```

7.  **Is javascript a statically typed or a dynamically typed language?**
    JavaScript is a **dynamically typed** language. This means that variable types are checked at runtime, not at compile time. You don't need to declare the type of a variable explicitly; it's determined by the value assigned to it, and it can change during execution.

    ```javascript
    let x;
    console.log(typeof x); // "undefined"
    x = 10;
    console.log(typeof x); // "number"
    x = "hello";
    console.log(typeof x); // "string"
    x = true;
    console.log(typeof x); // "boolean"
    ```

8.  **What is NaN property in JavaScript?**
    `NaN` stands for "Not a Number." It's a special numeric value that represents an unrepresentable or undefined result of an arithmetic operation.
    *   It's a property of the global object.
    *   The type of `NaN` is `number`.
    *   `NaN` is unique because it does not equal itself ( `NaN == NaN` and `NaN === NaN` are both `false`).
    *   To check if a value is `NaN`, use `isNaN()` or `Number.isNaN()`. `Number.isNaN()` is generally preferred as it doesn't coerce the argument.

    ```javascript
    console.log(0 / 0);            // NaN
    console.log(Math.sqrt(-1));    // NaN
    console.log(parseInt("hello"));// NaN
    console.log(typeof NaN);       // "number"

    console.log(NaN == NaN);       // false
    console.log(NaN === NaN);      // false

    console.log(isNaN("hello"));        // true (coerces "hello" to NaN)
    console.log(Number.isNaN("hello")); // false (does not coerce, "hello" is not NaN)
    console.log(Number.isNaN(0/0));     // true
    ```

9.  **Explain passed by value and passed by reference.**
    *   **Pass by Value (Primitives):** When a primitive data type (String, Number, Boolean, Null, Undefined, Symbol, BigInt) is passed to a function, a copy of its value is passed. Changes made to the parameter inside the function do not affect the original variable outside.
    *   **Pass by Reference (Objects - more accurately "Pass by Value of the Reference"):** When an object (including arrays and functions) is passed to a function, a copy of the *reference* (memory address) to that object is passed. This means both the original variable and the function parameter point to the same object in memory. Changes made to the object's properties inside the function *will* affect the original object. However, if you reassign the parameter to a new object inside the function, it won't affect the original variable.

    ```javascript
    // Pass by Value (Primitives)
    let num = 10;
    function changePrimitive(val) {
      val = 20; // Changes a copy
      console.log("Inside function (primitive):", val); // 20
    }
    changePrimitive(num);
    console.log("Outside function (primitive):", num); // 10 (original unchanged)

    // Pass by Reference (Objects)
    let obj = { name: "Alice" };
    function changeObjectProperty(o) {
      o.name = "Bob"; // Modifies the original object
      console.log("Inside function (object property):", o.name); // "Bob"
    }
    changeObjectProperty(obj);
    console.log("Outside function (object property):", obj.name); // "Bob" (original changed)

    function reassignObject(o) {
      o = { name: "Charlie" }; // Parameter 'o' now points to a new object
      console.log("Inside function (reassigned object):", o.name); // "Charlie"
    }
    reassignObject(obj);
    console.log("Outside function (reassigned object):", obj.name); // "Bob" (original not reassigned)
    ```

10. **What is an Immediately Invoked Function in JavaScript? (IIFE)**
    An IIFE is a JavaScript function that is executed as soon as it is defined. It's created by wrapping a function expression in parentheses `()` and then immediately calling it with another pair of parentheses `()`.
    **Purposes:**
    *   Avoid polluting the global scope (variables declared inside an IIFE are not accessible outside).
    *   Create a private scope for modules or specific logic.

    ```javascript
    (function() {
      var message = "Hello from IIFE!";
      console.log(message); // "Hello from IIFE!"
    })();

    // console.log(message); // ReferenceError: message is not defined

    let result = (function(a, b) {
      return a + b;
    })(5, 3);
    console.log(result); // 8
    ```

11. **What do you mean by strict mode in javascript and characteristics of javascript strict-mode?**
    Strict Mode is a way to opt into a restricted variant of JavaScript. It makes several changes to normal JavaScript semantics:
    *   **Enabling:** Add `"use strict";` at the beginning of a script or a function.
    *   **Characteristics:**
        1.  **Converts silent errors into throw errors:** Assigning to a non-writable property, an undeclared variable, or deleting an undeletable property will throw errors.
        2.  **Prevents accidental global variables:** Assigning a value to an undeclared variable throws a `ReferenceError`.
        3.  **Makes `eval` safer:** Variables and functions declared inside `eval` are not created in the surrounding scope.
        4.  **Disallows duplicate parameter names** in functions.
        5.  **Makes `this` undefined** in functions called without an explicit context (in non-strict mode, `this` would be the global object).
        6.  **Simplifies `arguments` and `caller`:** `arguments.callee` and `arguments.caller` are disallowed.
        7.  **Disallows `with` statement.**
        8.  **Forbids deleting plain names** (`delete variableName;`).

    ```javascript
    "use strict";

    function strictTest() {
      // "use strict"; // Can be function-scoped too
      // x = 10; // Throws ReferenceError: x is not defined
      let y = 20;
      console.log(y);

      function showThis() {
        console.log(this); // undefined in strict mode (window/global in non-strict)
      }
      showThis();
    }
    strictTest();
    ```

12. **Explain Higher Order Functions in javascript.**
    A Higher-Order Function (HOF) is a function that does at least one of the following:
    1.  Takes one or more functions as arguments.
    2.  Returns a function as its result.

    Common examples include `map`, `filter`, `reduce`, event listeners, and functions used for currying or composition.

    ```javascript
    // 1. Takes a function as an argument
    function operate(a, b, operationFn) {
      return operationFn(a, b);
    }
    function add(x, y) { return x + y; }
    function multiply(x, y) { return x * y; }

    console.log(operate(5, 3, add));      // 8
    console.log(operate(5, 3, multiply)); // 15

    // Array methods like map, filter, reduce are HOFs
    const numbers = [1, 2, 3, 4];
    const doubled = numbers.map(num => num * 2); // map takes a function
    console.log(doubled); // [2, 4, 6, 8]

    // 2. Returns a function
    function createGreeter(greeting) {
      return function(name) {
        console.log(greeting + ", " + name + "!");
      };
    }
    const sayHello = createGreeter("Hello");
    const sayHi = createGreeter("Hi");

    sayHello("Alice"); // "Hello, Alice!"
    sayHi("Bob");    // "Hi, Bob!"
    ```

13. **Explain “this” keyword.**
    The `this` keyword in JavaScript refers to the **context** in which a function is executed. Its value is determined by *how* a function is called, not where it's defined.
    *   **Global Context:** Outside any function, `this` refers to the global object (`window` in browsers, `global` in Node.js). In strict mode, `this` remains `undefined` in the global scope if not inside a function.
    *   **Function Context (Default Binding):** If a function is called without an explicit context (simple invocation `myFunction()`), `this` refers to the global object in non-strict mode. In strict mode, `this` is `undefined`.
    *   **Method Invocation (Implicit Binding):** When a function is called as a method of an object (`obj.myMethod()`), `this` refers to the object (`obj`) that the method is called on.
    *   **Constructor Invocation (New Binding):** When a function is called with the `new` keyword (`new MyConstructor()`), `this` refers to the newly created instance.
    *   **Explicit Binding (`call`, `apply`, `bind`):** These methods allow you to explicitly set the value of `this` for a function call.
    *   **Arrow Functions:** Arrow functions do not have their own `this` binding. They inherit `this` from their surrounding (lexical) scope.

    ```javascript
    // Global context
    // console.log(this); // window (browser) or global (Node)

    function showThis() {
      console.log(this);
    }
    // showThis(); // window (non-strict) or undefined (strict)

    const myObj = {
      name: "My Object",
      logName: function() {
        console.log(this.name); // "My Object" (this refers to myObj)
      }
    };
    myObj.logName();

    function Person(name) {
      this.name = name; // this refers to the new instance
    }
    const person1 = new Person("Alice");
    console.log(person1.name); // "Alice"

    const obj2 = { name: "Another Object" };
    myObj.logName.call(obj2); // "Another Object" (explicitly set this to obj2)

    const arrowObj = {
      name: "Arrow Example",
      greet: function() {
        setTimeout(() => {
          console.log("Hello, " + this.name); // 'this' is inherited from greet's scope
        }, 100);
      }
    };
    arrowObj.greet(); // "Hello, Arrow Example"
    ```

14. **What do you mean by Self Invoking Functions?**
    Self-Invoking Functions are the same as **Immediately Invoked Function Expressions (IIFEs)**. They are functions that execute immediately after they are defined.
    (See answer for question 10 for definition and example).

15. **Explain call(), apply() and, bind() methods.**
    `call()`, `apply()`, and `bind()` are methods available on all functions in JavaScript. They are used to explicitly set the `this` value for a function's execution and, optionally, pass arguments.

    *   **`call(thisArg, arg1, arg2, ...)`:**
        *   Invokes the function immediately.
        *   The first argument `thisArg` sets the `this` value for the function.
        *   Subsequent arguments are passed individually to the function.

    *   **`apply(thisArg, [argsArray])`:**
        *   Invokes the function immediately.
        *   The first argument `thisArg` sets the `this` value.
        *   The second argument is an **array (or array-like object)** whose elements are passed as arguments to the function.

    *   **`bind(thisArg, arg1, arg2, ...)`:**
        *   **Does not** invoke the function immediately.
        *   It returns a **new function** where `this` is permanently bound to `thisArg`.
        *   Optional arguments `arg1, arg2, ...` are pre-set (partially applied) for the new function.

    ```javascript
    function greet(greeting, punctuation) {
      console.log(greeting + ", " + this.name + punctuation);
    }

    const person = { name: "Alice" };
    const anotherPerson = { name: "Bob" };

    // call()
    greet.call(person, "Hello", "!"); // "Hello, Alice!"
    greet.call(anotherPerson, "Hi", "."); // "Hi, Bob."

    // apply()
    greet.apply(person, ["Good morning", "!!"]); // "Good morning, Alice!!"
    greet.apply(anotherPerson, ["Hey", "..."]);   // "Hey, Bob..."

    // bind()
    const greetAlice = greet.bind(person, "Hola");
    greetAlice("?"); // "Hola, Alice?" (punctuation is passed later)

    const greetBobPolitely = greet.bind(anotherPerson, "Good day", ".");
    greetBobPolitely(); // "Good day, Bob."
    ```
    **Use cases:**
    *   `call`/`apply`: Function borrowing, calling functions with a specific `this` context. `apply` is useful when arguments are already in an array.
    *   `bind`: Creating event handlers, callbacks, or functions with a fixed `this` context, or for partial application.

16. **What is the difference between exec () and test () methods in javascript?**
    Both `exec()` and `test()` are methods of regular expression objects (`RegExp`).

    *   **`test()`:**
        *   Tests for a match in a string.
        *   Returns `true` if a match is found, otherwise `false`.
        *   Simpler and often more performant if you only need to know *if* a match exists.

    *   **`exec()`:**
        *   Executes a search for a match in a string.
        *   Returns an **array** containing information about the match (including the matched substring, captured groups, index, input string) if a match is found.
        *   Returns `null` if no match is found.
        *   If the regex has the global flag (`g`), `exec()` updates the `lastIndex` property of the regex object, so subsequent calls can find further matches.

    ```javascript
    const regex = /hello (\w+)/i; // matches "hello " followed by one or more word characters, case-insensitive
    const str = "Say Hello World, then hello JavaScript.";

    // test()
    console.log(regex.test(str)); // true

    const noMatchStr = "Goodbye";
    console.log(regex.test(noMatchStr)); // false

    // exec()
    let result = regex.exec(str);
    console.log(result);
    /*
    [
      "Hello World", // Full match
      "World",       // First capturing group (\w+)
      index: 4,
      input: "Say Hello World, then hello JavaScript.",
      groups: undefined
    ]
    */

    let noMatchResult = regex.exec(noMatchStr);
    console.log(noMatchResult); // null

    // exec() with global flag
    const globalRegex = /hello (\w+)/ig;
    let match;
    while ((match = globalRegex.exec(str)) !== null) {
      console.log(`Found "${match[0]}" at index ${match.index}. Next search starts at ${globalRegex.lastIndex}. Captured: "${match[1]}"`);
    }
    // Output:
    // Found "Hello World" at index 4. Next search starts at 15. Captured: "World"
    // Found "hello JavaScript" at index 21. Next search starts at 37. Captured: "JavaScript"
    ```

17. **What is currying in JavaScript?**
    Currying is a functional programming technique where a function that takes multiple arguments is transformed into a sequence of functions, each taking a single argument. Each function in the sequence returns another function until all arguments have been supplied, at which point the final result is returned.

    It allows for partial application, creating specialized functions from more general ones.

    ```javascript
    // Non-curried function
    function add(a, b, c) {
      return a + b + c;
    }
    console.log(add(1, 2, 3)); // 6

    // Curried version
    function curryAdd(a) {
      return function(b) {
        return function(c) {
          return a + b + c;
        };
      };
    }
    console.log(curryAdd(1)(2)(3)); // 6

    // Using currying for partial application
    const add5 = curryAdd(5); // Partially apply the first argument
    const add5And3 = add5(3);  // Partially apply the second argument
    console.log(add5And3(2));  // 10 (5 + 3 + 2)
    console.log(add5(10)(1));  // 16 (5 + 10 + 1)

    // A more generic curry function (simplified example)
    function curry(fn) {
      return function curried(...args) {
        if (args.length >= fn.length) {
          return fn.apply(this, args);
        } else {
          return function(...args2) {
            return curried.apply(this, args.concat(args2));
          };
        }
      };
    }

    const curriedSum = curry(add);
    console.log(curriedSum(1)(2)(3)); // 6
    console.log(curriedSum(1, 2)(3)); // 6
    console.log(curriedSum(1)(2, 3)); // 6
    ```

18. **What are some advantages of using External JavaScript?**
    Placing JavaScript code in external `.js` files and linking them to HTML (`<script src="script.js"></script>`) has several advantages:
    1.  **Separation of Concerns:** Keeps HTML structure, CSS presentation, and JavaScript behavior in separate files, making code cleaner and easier to manage.
    2.  **Maintainability:** Easier to update and debug JavaScript logic without touching the HTML.
    3.  **Reusability:** The same JavaScript file can be used across multiple HTML pages.
    4.  **Browser Caching:** Browsers can cache external `.js` files. If the same script is used on multiple pages, it's downloaded only once, speeding up subsequent page loads.
    5.  **Readability:** HTML files become less cluttered and easier to read.
    6.  **Collaboration:** Different developers can work on HTML, CSS, and JavaScript files simultaneously without much conflict.

19. **Explain Scope and Scope Chain in javascript.**
    *   **Scope:** Scope determines the accessibility (visibility) of variables and functions at various parts of your code during runtime. JavaScript has:
        *   **Global Scope:** Variables declared outside any function or block are in the global scope and accessible from anywhere.
        *   **Function Scope:** Variables declared with `var` inside a function are accessible only within that function and any nested functions.
        *   **Block Scope (ES6):** Variables declared with `let` and `const` inside a block (e.g., `if` statement, `for` loop, or just `{}`) are accessible only within that block.

    *   **Scope Chain (Lexical Scoping):** When JavaScript needs to find the value of a variable, it first looks in the current scope. If not found, it looks in the outer (parent) scope, then the parent's parent scope, and so on, up to the global scope. This chain of nested scopes is called the scope chain. Lexical scoping means the scope chain is determined by where functions and blocks are *written* in the code, not where they are called.

    ```javascript
    let globalVar = "I am global"; // Global scope

    function outerFunction() {
      let outerVar = "I am outer"; // Function scope for outerFunction

      function innerFunction() {
        let innerVar = "I am inner"; // Function scope for innerFunction
        console.log(innerVar);    // "I am inner" (found in current scope)
        console.log(outerVar);    // "I am outer" (found in outerFunction's scope)
        console.log(globalVar);   // "I am global" (found in global scope)
        // console.log(anotherVar); // ReferenceError: anotherVar is not defined
      }

      innerFunction();
      // console.log(innerVar); // ReferenceError: innerVar is not defined (not accessible here)
    }

    outerFunction();
    // console.log(outerVar); // ReferenceError: outerVar is not defined (not accessible here)
    ```
    In this example, `innerFunction` forms a scope chain: `innerFunction`'s scope -> `outerFunction`'s scope -> Global scope.

20. **Explain Closures in JavaScript.**
    A closure is the combination of a function and the lexical environment (scope) within which that function was declared. This means a closure gives you access to an outer function's scope (its variables and parameters) from an inner function, even after the outer function has finished executing and returned.

    **Key Characteristics:**
    1.  An inner function "remembers" the environment (variables, parameters) of its outer enclosing function.
    2.  This "memory" persists even if the outer function has returned.

    ```javascript
    function outerFunction(outerArg) {
      let outerVar = "I am from outer";

      function innerFunction(innerArg) {
        console.log("Outer Arg:", outerArg);
        console.log("Outer Var:", outerVar);
        console.log("Inner Arg:", innerArg);
      }
      return innerFunction; // Return the inner function
    }

    const myClosure = outerFunction("Hello"); // outerFunction executes and returns innerFunction
    // At this point, outerFunction's execution context is gone,
    // but myClosure (which is innerFunction) still has access to outerArg and outerVar.

    myClosure("World");
    // Output:
    // Outer Arg: Hello
    // Outer Var: I am from outer
    // Inner Arg: World

    // Another example: Counter
    function createCounter() {
      let count = 0;
      return function() {
        count++;
        console.log(count);
        return count;
      };
    }

    const counter1 = createCounter();
    counter1(); // 1
    counter1(); // 2

    const counter2 = createCounter(); // Creates a new, independent closure
    counter2(); // 1
    ```
    Closures are powerful for data privacy (creating private variables), partial application, and in callbacks.

21. **Mention some advantages of javascript.**
    1.  **Ubiquity & Client-Side Interactivity:** Runs in all modern web browsers, enabling dynamic and interactive user experiences without page reloads.
    2.  **Large Ecosystem & Community:** Extensive libraries (React, Angular, Vue, jQuery), frameworks (Node.js, Express), and a vast, active developer community providing ample resources and support.
    3.  **Full-Stack Development:** With Node.js, JavaScript can be used for both front-end and back-end development, simplifying the tech stack ("JavaScript everywhere").
    4.  **Relatively Easy to Learn:** Compared to some other languages, JavaScript has a relatively gentle learning curve for beginners.
    5.  **Asynchronous Processing:** Supports non-blocking operations (callbacks, Promises, async/await), crucial for efficient I/O tasks and responsive applications.
    6.  **Speed and Performance:** Modern JavaScript engines (like V8) are highly optimized, making JavaScript execution fast.
    7.  **Versatility:** Used for web development, mobile apps (React Native, Ionic), desktop apps (Electron), server-side applications, game development, and IoT.
    8.  **Dynamic Typing:** Offers flexibility, though it can also be a source of bugs if not managed carefully.

22. **What are object prototypes?**
    Object prototypes are the mechanism through which JavaScript objects inherit features (properties and methods) from one another. Every object in JavaScript has a hidden internal property, often referred to as `[[Prototype]]` (accessible via `__proto__` or `Object.getPrototypeOf()`), which is either `null` or a reference to another object, called its "prototype."
    When you try to access a property or method on an object, if it's not found directly on the object itself, JavaScript looks up the prototype chain (the object's prototype, then that prototype's prototype, and so on) until the property is found or the chain ends with `null`.

    ```javascript
    let animal = {
      eats: true,
      walk() {
        console.log("Animal walks");
      }
    };

    let rabbit = {
      jumps: true,
      __proto__: animal // Sets 'animal' as the prototype of 'rabbit' (older way)
    };

    // Modern way to set prototype
    let dog = Object.create(animal);
    dog.barks = true;

    console.log(rabbit.eats);   // true (inherited from animal)
    rabbit.walk();              // "Animal walks" (inherited from animal)
    console.log(rabbit.jumps);  // true (own property)

    console.log(dog.eats);      // true
    dog.walk();                 // "Animal walks"
    console.log(dog.barks);     // true

    // Check prototype
    console.log(Object.getPrototypeOf(rabbit) === animal); // true
    console.log(Object.getPrototypeOf(dog) === animal);    // true
    ```
    Constructor functions' `prototype` property is what becomes the `[[Prototype]]` for objects created with `new`.

23. **What are callbacks?**
    A callback is a function that is passed as an argument to another function and is intended to be executed at a later point in time, often after an operation (like an asynchronous task or an event) has completed. The function that receives the callback is responsible for "calling it back."

    **Common Uses:**
    *   Asynchronous operations (e.g., fetching data, timers).
    *   Event handling (e.g., click events, key presses).
    *   Higher-order functions (e.g., `map`, `filter`, `forEach`).

    ```javascript
    // Example 1: Synchronous callback (Array.forEach)
    const numbers = [1, 2, 3];
    numbers.forEach(function(number) { // This function is a callback
      console.log(number * 2);
    });
    // Output: 2, 4, 6

    // Example 2: Asynchronous callback (setTimeout)
    function greet(name, callback) {
      console.log("Preparing greeting...");
      setTimeout(function() {
        const message = "Hello, " + name + "!";
        callback(message); // Execute the callback after 2 seconds
      }, 2000);
    }

    function displayGreeting(greetingMessage) {
      console.log(greetingMessage);
    }

    greet("Alice", displayGreeting);
    // Output:
    // Preparing greeting...
    // (after 2 seconds)
    // Hello, Alice!

    // Example 3: Event Handling (conceptual, browser environment)
    /*
    const button = document.getElementById('myButton');
    button.addEventListener('click', function() { // This anonymous function is a callback
        console.log('Button clicked!');
    });
    */
    ```

24. **What are the types of errors in javascript?**
    JavaScript has several built-in error types that can be thrown when something goes wrong:
    1.  **`Error`:** The base object for all errors.
    2.  **`SyntaxError`:** An error in parsing code that doesn't conform to JavaScript syntax (e.g., missing parenthesis, invalid keyword usage). These usually prevent the script from running.
    3.  **`ReferenceError`:** Thrown when trying to access a variable that has not been declared or is out of scope.
    4.  **`TypeError`:** Thrown when an operation is performed on a value of an inappropriate type (e.g., calling a non-function, accessing properties of `null` or `undefined`).
    5.  **`RangeError`:** Thrown when a numeric variable or parameter is outside of its valid range (e.g., invalid array length, illegal number for `Number.prototype.toFixed()`).
    6.  **`URIError`:** Thrown when global URI handling functions (like `encodeURIComponent()`, `decodeURIComponent()`) are used incorrectly.
    7.  **`EvalError`:** (Rarely used) Represents an error regarding the global `eval()` function. Modern JS engines mostly don't throw this.
    8.  **`InternalError`:** (Non-standard, specific to some engines like Firefox) Indicates an internal error in the JavaScript engine, often due to too much recursion ("too much recursion").

    ```javascript
    // SyntaxError (would prevent script from running if not commented)
    // let x = ;

    // ReferenceError
    try {
      console.log(nonExistentVar);
    } catch (e) {
      console.error(e.name + ": " + e.message); // ReferenceError: nonExistentVar is not defined
    }

    // TypeError
    try {
      let num = 123;
      num.toUpperCase(); // Numbers don't have toUpperCase
    } catch (e) {
      console.error(e.name + ": " + e.message); // TypeError: num.toUpperCase is not a function
    }

    // RangeError
    try {
      const arr = new Array(-1); // Invalid array length
    } catch (e) {
      console.error(e.name + ": " + e.message); // RangeError: Invalid array length
    }
    ```

25. **What is memoization?**
    Memoization is an optimization technique used to speed up function execution by caching the results of expensive function calls and returning the cached result when the same inputs occur again. It's particularly useful for pure functions (functions that always return the same output for the same input and have no side effects).

    ```javascript
    function memoize(fn) {
      const cache = {}; // Store results
      return function(...args) {
        const key = JSON.stringify(args); // Create a unique key for the arguments
        if (cache[key]) {
          console.log("Fetching from cache for args:", args);
          return cache[key];
        } else {
          console.log("Calculating result for args:", args);
          const result = fn(...args);
          cache[key] = result;
          return result;
        }
      };
    }

    function slowFactorial(n) {
      if (n <= 1) return 1;
      // Simulate expensive calculation
      for(let i=0; i < 1e7; i++) {}
      return n * slowFactorial(n - 1);
    }

    const memoizedFactorial = memoize(function factorial(n) { // Pure function for factorial
        if (n <= 1) return 1;
        return n * memoizedFactorial(n - 1); // Recursive call to memoized version
    });


    console.time("factorial 5 first call");
    console.log(memoizedFactorial(5));
    console.timeEnd("factorial 5 first call");
    // Output:
    // Calculating result for args: [ 5 ]
    // Calculating result for args: [ 4 ]
    // Calculating result for args: [ 3 ]
    // Calculating result for args: [ 2 ]
    // Calculating result for args: [ 1 ]
    // 120
    // factorial 5 first call: ...ms

    console.time("factorial 5 second call");
    console.log(memoizedFactorial(5));
    console.timeEnd("factorial 5 second call");
    // Output:
    // Fetching from cache for args: [ 5 ]
    // 120
    // factorial 5 second call: ...ms (much faster)

    console.time("factorial 6 call");
    console.log(memoizedFactorial(6)); // Will use cached value for factorial(5)
    console.timeEnd("factorial 6 call");
    // Output:
    // Calculating result for args: [ 6 ]
    // Fetching from cache for args: [ 5 ]
    // 720
    // factorial 6 call: ...ms
    ```

26. **What is recursion in a programming language?**
    Recursion is a programming technique where a function calls itself directly or indirectly to solve a problem. A recursive function breaks a problem down into smaller, self-similar subproblems until it reaches a **base case**—a condition that stops the recursion. Without a base case, a recursive function would call itself indefinitely, leading to a stack overflow error.

    ```javascript
    // Example: Factorial
    function factorial(n) {
      // Base case: if n is 0 or 1, factorial is 1
      if (n <= 1) {
        return 1;
      }
      // Recursive step: n * factorial of (n-1)
      else {
        return n * factorial(n - 1);
      }
    }

    console.log(factorial(5)); // 120 (5 * 4 * 3 * 2 * 1)
    console.log(factorial(0)); // 1

    // Example: Countdown
    function countdown(num) {
      if (num < 0) { // Base case
        console.log("Done!");
        return;
      }
      console.log(num);
      countdown(num - 1); // Recursive call
    }
    countdown(3);
    // Output:
    // 3
    // 2
    // 1
    // 0
    // Done!
    ```

27. **What is the use of a constructor function in javascript?**
    A constructor function is a special function used to create and initialize objects. It acts as a blueprint for creating multiple objects of the same type.
    **Key features and uses:**
    1.  **Object Creation:** Used with the `new` keyword to create new object instances.
    2.  **`this` Keyword:** Inside a constructor function, `this` refers to the newly created object instance.
    3.  **Initialization:** Used to set initial properties and values for the created objects.
    4.  **Prototype:** Constructor functions have a `prototype` property. This property is an object that becomes the prototype (`[[Prototype]]`) for all objects created by that constructor. Methods and properties defined on the constructor's `prototype` are shared among all instances, promoting code reuse and efficiency.
    5.  **Naming Convention:** By convention, constructor function names start with an uppercase letter (e.g., `Person`, `Car`).

    ```javascript
    function Person(name, age) {
      // 'this' refers to the new object being created
      this.name = name;
      this.age = age;

      // Methods can be defined directly, but it's often better on the prototype
      // this.greet = function() {
      //   console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
      // };
    }

    // Methods are typically added to the prototype for efficiency (shared by all instances)
    Person.prototype.greet = function() {
      console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    };

    Person.prototype.species = "Homo Sapiens"; // Shared property

    // Create instances using the 'new' keyword
    const person1 = new Person("Alice", 30);
    const person2 = new Person("Bob", 25);

    person1.greet(); // "Hello, my name is Alice and I am 30 years old."
    person2.greet(); // "Hello, my name is Bob and I am 25 years old."

    console.log(person1.species); // "Homo Sapiens"
    console.log(person2.species); // "Homo Sapiens"

    console.log(person1 instanceof Person); // true
    console.log(person1.constructor === Person); // true
    ```

28. **What is DOM?**
    DOM stands for **Document Object Model**. It's a programming interface (API) for web documents (HTML, XML). It represents the page structure as a tree of objects, where each node in the tree represents a part of the document (e.g., an element, an attribute, text).
    **Key Aspects:**
    1.  **Tree Structure:** The DOM represents the HTML document as a hierarchical tree of nodes. The `document` object is the root.
    2.  **Objects:** Each HTML element, attribute, and piece of text is an object (node) in this tree.
    3.  **Manipulation:** JavaScript can use the DOM to access, create, modify, or delete elements and their content dynamically. This allows for interactive web pages.
    4.  **Standard:** The DOM is a W3C (World Wide Web Consortium) standard, ensuring cross-browser compatibility.

    ```javascript
    // Assume this HTML:
    // <div id="container">
    //   <h1>Hello DOM</h1>
    //   <p>This is a paragraph.</p>
    // </div>

    // Accessing an element
    const container = document.getElementById('container');

    // Modifying content
    const heading = container.querySelector('h1');
    if (heading) {
      heading.textContent = 'Hello World, via DOM!';
    }

    // Creating and appending a new element
    const newParagraph = document.createElement('p');
    newParagraph.textContent = 'This is a new paragraph added by JavaScript.';
    if (container) {
      container.appendChild(newParagraph);
    }
    ```

29. **Which method is used to retrieve a character from a certain index?**
    There are two common ways to retrieve a character from a string at a certain index:
    1.  **`charAt(index)` method:** Returns a new string containing the single character at the specified `index`.
    2.  **Bracket notation `[]` (Property Accessor):** Treats the string like an array-like object and returns the character at the `index`. This is generally preferred for its conciseness and consistency with array access.

    Both return an empty string if `index` is out of bounds for `charAt()`, while bracket notation returns `undefined`.

    ```javascript
    const str = "Hello";

    // Using charAt()
    console.log(str.charAt(0)); // "H"
    console.log(str.charAt(1)); // "e"
    console.log(str.charAt(10)); // "" (empty string for out-of-bounds)

    // Using bracket notation []
    console.log(str[0]);      // "H"
    console.log(str[1]);      // "e"
    console.log(str[10]);     // undefined (for out-of-bounds)

    // Performance is generally similar for both.
    // Bracket notation is often preferred for its conciseness.
    ```

30. **What do you mean by BOM?**
    BOM stands for **Browser Object Model**. It's a browser-specific API that allows JavaScript to interact with the browser itself, outside the content of the web page (which is handled by the DOM). The BOM is not standardized and can vary between browsers, though some common objects are widely supported.
    **Key objects within the BOM include:**
    *   **`window`:** The global object in client-side JavaScript. It represents the browser window or tab. All global variables and functions become properties and methods of the `window` object. It also provides methods like `alert()`, `prompt()`, `confirm()`, `setTimeout()`, `setInterval()`, `open()`, `close()`.
    *   **`navigator`:** Contains information about the browser (e.g., name, version, user agent, geolocation).
    *   **`screen`:** Contains information about the user's screen (e.g., width, height, color depth).
    *   **`location`:** Represents the current URL of the document. Can be used to get URL details or navigate to a new page (`location.href`, `location.reload()`).
    *   **`history`:** Allows interaction with the browser's session history (e.g., `history.back()`, `history.forward()`, `history.go()`).
    *   `document`: While technically part of the DOM, the `document` object is also accessible via `window.document` and is often considered part of the BOM's entry point to the page content.

    ```javascript
    // Examples of BOM usage (run in a browser console)

    // window object
    // window.alert("Hello from BOM!");
    console.log(window.innerWidth); // Width of the browser window's viewport
    // setTimeout(() => console.log("Delayed message"), 1000);

    // navigator object
    console.log(navigator.userAgent);
    // navigator.geolocation.getCurrentPosition(pos => console.log(pos.coords));

    // screen object
    console.log(screen.width + "x" + screen.height);

    // location object
    console.log(location.href);
    // location.href = "https://www.example.com"; // Navigates to a new page

    // history object
    // history.back(); // Goes to the previous page
    ```

31. **What is the distinction between client-side and server-side JavaScript?**

    | Feature             | Client-Side JavaScript                       | Server-Side JavaScript (e.g., Node.js)       |
    | :------------------ | :------------------------------------------- | :------------------------------------------- |
    | **Environment**     | Runs in the user's web browser.              | Runs on a server.                            |
    | **Primary Purpose** | Enhance user interface, interactivity, DOM manipulation, make API calls. | Build web servers, APIs, interact with databases, file systems, perform computations. |
    | **Core Objects**    | Access to `window`, `document` (DOM), BOM.   | Access to file system (`fs`), HTTP module (`http`), OS information (`os`), process handling. No direct DOM/BOM access. |
    | **Execution**       | Triggered by user actions, page load, scripts embedded in HTML. | Triggered by HTTP requests from clients or other server processes. |
    | **Security**        | Runs in a sandboxed environment with limited access to user's system for security. | Can have full access to the server's resources (file system, databases, network). |
    | **Use Cases**       | Form validation, animations, dynamic content updates, single-page applications (SPAs). | Web application backends, REST APIs, microservices, real-time applications (chat), command-line tools. |
    | **Example Context** | `<script>alert('Hello');</script>` in HTML.   | `const http = require('http');` in a `.js` file run by Node.js. |

---
**JavaScript Interview Questions for Experienced**
---

1.  **What are arrow functions?**
    Arrow functions (introduced in ES6) provide a concise syntax for writing function expressions.
    **Key Differences & Features:**
    1.  **Concise Syntax:** Shorter than traditional function expressions.
    2.  **Lexical `this`:** Arrow functions do not have their own `this` binding. `this` is inherited from the surrounding (lexical) scope. This is a major advantage, especially for callbacks and methods.
    3.  **No `arguments` Object:** Arrow functions do not have their own `arguments` object. You can use rest parameters (`...args`) instead.
    4.  **Cannot be used as Constructors:** Arrow functions cannot be called with `new`. They don't have a `prototype` property.
    5.  **No `prototype` property.**
    6.  **Implicit Return:** If the function body is a single expression, the `return` keyword and curly braces `{}` can be omitted, and the expression's value is implicitly returned.
    7.  **Cannot use `yield`:** Arrow functions cannot be used as generator functions.

    ```javascript
    // Traditional function expression
    const add_trad = function(a, b) {
      return a + b;
    };

    // Arrow function
    const add_arrow = (a, b) => a + b; // Implicit return
    const greet = name => `Hello, ${name}!`; // Single parameter, implicit return

    console.log(add_arrow(2, 3)); // 5
    console.log(greet("Alice"));   // "Hello, Alice!"

    // Lexical 'this' example
    function Person(name) {
      this.name = name;
      this.age = 0;

      // Traditional function in setTimeout - 'this' would be global/window or undefined (strict)
      // setTimeout(function() {
      //   console.log(this.name); // undefined or error
      // }, 100);

      // Arrow function in setTimeout - 'this' is lexically bound to Person instance
      setTimeout(() => {
        console.log(`From arrow function, this.name: ${this.name}`); // "Bob"
      }, 100);
    }
    const p = new Person("Bob");

    // No arguments object
    const sumAll = (...args) => {
      let sum = 0;
      for (let arg of args) {
        sum += arg;
      }
      return sum;
    };
    console.log(sumAll(1, 2, 3, 4)); // 10
    ```

2.  **What do mean by prototype design pattern?**
    The Prototype design pattern is a **creational** design pattern that focuses on creating new objects by cloning (copying) an existing object, called a "prototype." Instead of creating objects from scratch using a class or constructor, you create a prototypical instance, and then new objects are created by copying this prototype.
    **Key Ideas:**
    1.  **Cloning:** New objects are created by copying an existing object.
    2.  **Reduced Subclassing:** It can reduce the need for numerous subclasses if object creation involves complex configurations.
    3.  **Performance:** Cloning can sometimes be more efficient than creating new objects if initialization is resource-intensive.
    JavaScript's prototypal inheritance is inherently related to this pattern. `Object.create()` is a direct way to implement the prototype pattern.

    ```javascript
    // Prototypical object
    const carPrototype = {
      wheels: 4,
      fuel: "petrol",
      startEngine: function() {
        console.log("Engine started!");
      },
      clone: function() {
        // A simple shallow clone, could be more complex for deep cloning
        let cloned = Object.create(Object.getPrototypeOf(this));
        for (let key in this) {
          if (this.hasOwnProperty(key)) {
            cloned[key] = this[key];
          }
        }
        return cloned;
      }
    };

    // Create new objects by cloning the prototype
    const myCar = Object.create(carPrototype); // Using Object.create directly
    myCar.color = "red";
    myCar.model = "Sedan";

    const anotherCar = carPrototype.clone(); // Using a custom clone method
    anotherCar.color = "blue";
    anotherCar.model = "SUV";

    myCar.startEngine();       // "Engine started!"
    console.log(myCar.color);  // "red"

    anotherCar.startEngine();    // "Engine started!"
    console.log(anotherCar.model); // "SUV"

    console.log(Object.getPrototypeOf(myCar) === carPrototype); // true (if carPrototype was the direct prototype)
                                                              // false if myCar.clone made a copy with carPrototype as ITS prototype
    // Corrected clone if we want carPrototype itself to be the prototype of the cloned object
    const carPrototypeCorrected = {
        wheels: 4,
        fuel: "petrol",
        startEngine: function() { console.log("Engine started!"); },
        init: function(color, model) {
            this.color = color;
            this.model = model;
        }
    };

    // Client code
    const redSedan = Object.create(carPrototypeCorrected);
    redSedan.init("red", "Sedan");

    const blueSUV = Object.create(carPrototypeCorrected);
    blueSUV.init("blue", "SUV");

    redSedan.startEngine();
    console.log(redSedan.color); // "red"
    ```
    The core idea is that you have a template object (the prototype), and you create new objects that are either instances of this prototype or copies of it, possibly customized afterward.

3.  **Differences between declaring variables using var, let and const.**

    | Feature           | `var`                                     | `let`                                       | `const`                                                   |
    | :---------------- | :---------------------------------------- | :------------------------------------------ | :-------------------------------------------------------- |
    | **Scope**         | Function-scoped or globally-scoped        | Block-scoped (`{}`)                          | Block-scoped (`{}`)                                       |
    | **Hoisting**      | Hoisted and initialized with `undefined`  | Hoisted but not initialized (Temporal Dead Zone - TDZ) | Hoisted but not initialized (Temporal Dead Zone - TDZ)    |
    | **Re-assignment** | Can be re-assigned                        | Can be re-assigned                        | Cannot be re-assigned (immutable binding, not value for objects) |
    | **Re-declaration**| Can be re-declared in the same scope    | Cannot be re-declared in the same scope   | Cannot be re-declared in the same scope                 |
    | **Initialization**| Optional at declaration                   | Optional at declaration                   | **Must be initialized** at declaration                    |
    | **Global Object Property** | Creates property on global object if declared globally | Does not create property on global object | Does not create property on global object                |

    ```javascript
    // Scope
    function scopeTest() {
      if (true) {
        var v = "var";
        let l = "let";
        const c = "const";
      }
      console.log(v); // "var"
      // console.log(l); // ReferenceError
      // console.log(c); // ReferenceError
    }
    scopeTest();

    // Re-assignment & Re-declaration
    var x = 1;
    x = 2; // OK
    var x = 3; // OK

    let y = 1;
    y = 2; // OK
    // let y = 3; // SyntaxError

    const z = 1;
    // z = 2; // TypeError: Assignment to constant variable.
    // const z = 3; // SyntaxError

    // Const with objects/arrays (value is immutable, binding is not)
    const obj = { a: 1 };
    obj.a = 2; // OK, modifying the object's property
    // obj = { b: 3 }; // TypeError, cannot re-assign obj

    const arr = [1, 2];
    arr.push(3); // OK
    // arr = [4, 5]; // TypeError
    ```

4.  **What is the rest parameter and spread operator?**
    Both use the three-dot (`...`) syntax but have opposite functionalities.

    *   **Rest Parameter (`...`):**
        *   Used in **function parameter lists**.
        *   Collects all remaining arguments passed to a function into a **single array**.
        *   It must be the **last parameter** in the function definition.
        *   Allows functions to accept a variable number of arguments.

        ```javascript
        function sumAll(...numbers) { // 'numbers' will be an array
          let total = 0;
          for (const num of numbers) {
            total += num;
          }
          return total;
        }
        console.log(sumAll(1, 2, 3));       // 6
        console.log(sumAll(10, 20, 30, 40)); // 100
        console.log(sumAll());              // 0

        function logArgs(firstArg, ...restOfArgs) {
            console.log("First:", firstArg);
            console.log("Rest:", restOfArgs);
        }
        logArgs("a", "b", "c", "d");
        // First: a
        // Rest: [ 'b', 'c', 'd' ]
        ```

    *   **Spread Operator (`...`):**
        *   Used where **multiple elements/values are expected** (e.g., in array literals, function calls, object literals).
        *   **Expands** an iterable (like an array or string) or an object into individual elements or key-value pairs.

        ```javascript
        // Expanding arrays
        const arr1 = [1, 2, 3];
        const arr2 = [4, 5, 6];
        const combinedArray = [...arr1, ...arr2, 7]; // [1, 2, 3, 4, 5, 6, 7]
        console.log(combinedArray);

        const arrCopy = [...arr1]; // Creates a shallow copy
        console.log(arrCopy);      // [1, 2, 3]

        // Expanding strings
        const str = "hello";
        const chars = [...str]; // ['h', 'e', 'l', 'l', 'o']
        console.log(chars);

        // In function calls
        function multiply(x, y, z) {
          return x * y * z;
        }
        const nums = [2, 3, 4];
        console.log(multiply(...nums)); // Equivalent to multiply(2, 3, 4) -> 24

        // Expanding objects (ES2018+)
        const obj1 = { a: 1, b: 2 };
        const obj2 = { b: 3, c: 4 };
        const mergedObj = { ...obj1, ...obj2, d: 5 }; // { a: 1, b: 3, c: 4, d: 5 } (obj2.b overwrites obj1.b)
        console.log(mergedObj);

        const objCopy = { ...obj1 }; // Shallow copy
        console.log(objCopy); // {a: 1, b: 2}
        ```

5.  **In JavaScript, how many different methods can you make an object?**
    There are several ways to create objects in JavaScript:
    1.  **Object Literal:** Simplest way.
        ```javascript
        const obj1 = {
          name: "Alice",
          age: 30,
          greet: function() { console.log("Hello!"); }
        };
        ```
    2.  **Constructor Function (with `new` keyword):**
        ```javascript
        function Person(name, age) {
          this.name = name;
          this.age = age;
        }
        Person.prototype.greet = function() { console.log(`Hi, I'm ${this.name}`); };
        const obj2 = new Person("Bob", 25);
        ```
    3.  **`Object.create()` method:** Creates a new object with a specified prototype object and optional properties.
        ```javascript
        const animalPrototype = {
          makeSound: function() { console.log("Generic sound"); }
        };
        const obj3 = Object.create(animalPrototype);
        obj3.type = "Dog";
        obj3.makeSound(); // "Generic sound" (if not overridden)
        console.log(obj3.type); // "Dog"

        const obj3b = Object.create(null); // Creates an object with no prototype
        ```
    4.  **ES6 Classes (Syntactic Sugar over Prototypal Inheritance):**
        ```javascript
        class Car {
          constructor(make, model) {
            this.make = make;
            this.model = model;
          }
          displayInfo() {
            console.log(`${this.make} ${this.model}`);
          }
        }
        const obj4 = new Car("Toyota", "Camry");
        obj4.displayInfo();
        ```
    5.  **Using `Object.assign()` to create a new object or clone/merge:**
        ```javascript
        const source = { a: 1, b: 2 };
        const obj5 = Object.assign({}, source, { c: 3 }); // Creates a new object by merging
        console.log(obj5); // { a: 1, b: 2, c: 3 }
        ```
    6.  **Factory Functions:** Functions that return an object, without using `new` or `this` in the traditional constructor sense.
        ```javascript
        function createCircle(radius) {
          return {
            radius, // shorthand for radius: radius
            draw: function() {
              console.log(`Drawing a circle with radius ${this.radius}`);
            }
          };
        }
        const obj6 = createCircle(5);
        obj6.draw();
        ```

6.  **What is the use of promises in javascript?**
    Promises are objects representing the eventual completion (or failure) of an asynchronous operation and its resulting value. They provide a cleaner and more manageable way to handle asynchronous code compared to traditional callback-based approaches ("callback hell").
    **Key Uses and Benefits:**
    1.  **Managing Asynchronous Operations:** Ideal for tasks like API calls, file reading, database queries, or any operation that takes time and doesn't block the main thread.
    2.  **Avoiding Callback Hell:** Promises allow chaining asynchronous operations sequentially using `.then()` and handling errors centrally with `.catch()`, making code more readable and maintainable.
    3.  **States:** A Promise can be in one of three states:
        *   `pending`: Initial state, neither fulfilled nor rejected.
        *   `fulfilled` (or `resolved`): The operation completed successfully, and the promise has a resulting value.
        *   `rejected`: The operation failed, and the promise has a reason (error).
    4.  **Chaining:** `.then()` methods can be chained to perform sequential asynchronous operations. Each `.then()` receives the result of the previous promise.
    5.  **Error Handling:** `.catch()` provides a centralized way to handle errors from any preceding promise in the chain. `.finally()` can be used for cleanup code that runs regardless of success or failure.
    6.  **Composition:** `Promise.all()`, `Promise.race()`, `Promise.allSettled()`, `Promise.any()` allow for combining multiple promises.

    ```javascript
    function fetchData(url) {
      return new Promise((resolve, reject) => {
        // Simulate an API call
        setTimeout(() => {
          if (url === "success") {
            resolve({ data: "Some data from server" });
          } else {
            reject(new Error("Failed to fetch data"));
          }
        }, 1000);
      });
    }

    fetchData("success")
      .then(response => {
        console.log("First then:", response.data);
        return response.data.toUpperCase(); // Pass data to the next .then()
      })
      .then(processedData => {
        console.log("Second then:", processedData);
      })
      .catch(error => {
        console.error("Error:", error.message);
      })
      .finally(() => {
        console.log("Operation finished (either success or failure).");
      });

    // Example with failure
    fetchData("failure")
      .then(response => console.log(response.data)) // This won't run
      .catch(error => console.error("Error from failure case:", error.message))
      .finally(() => console.log("Failure operation finished."));
    ```

7.  **What are classes in javascript?**
    ES6 classes are primarily **syntactic sugar** over JavaScript's existing prototype-based inheritance. They provide a more familiar, class-like syntax for creating objects and implementing inheritance, similar to what's found in other object-oriented languages like Java or C++.
    **Key Features:**
    1.  **`class` Keyword:** Used to declare a class.
    2.  **`constructor` Method:** A special method for creating and initializing an object created with a class. There can be only one `constructor` method in a class.
    3.  **Methods:** Defined within the class body. These methods are added to the class's `prototype`.
    4.  **`static` Methods/Properties:** Belong to the class itself, not to instances of the class. Called on the class directly (e.g., `MyClass.staticMethod()`).
    5.  **`extends` Keyword:** Used for class inheritance. A subclass inherits from a superclass.
    6.  **`super` Keyword:** Used to call the constructor of the parent class (`super()`) or access methods of the parent class (`super.parentMethod()`).
    7.  **Getters and Setters:** Special methods for defining computed properties.
    8.  **Strict Mode:** Class declarations and expressions are executed in strict mode by default.

    ```javascript
    class Animal {
      constructor(name) {
        this.name = name;
      }

      speak() {
        console.log(`${this.name} makes a sound.`);
      }

      static info() {
        console.log("This is an Animal class.");
      }
    }

    class Dog extends Animal {
      constructor(name, breed) {
        super(name); // Call the parent class constructor
        this.breed = breed;
      }

      speak() { // Override parent method
        super.speak(); // Call parent method if needed
        console.log(`${this.name} barks.`);
      }

      get fullDescription() {
        return `${this.name} is a ${this.breed}.`;
      }

      set nickName(nick) {
        this._nickName = nick; // Use a backing property
      }
      get nickName() {
        return this._nickName || this.name;
      }
    }

    Animal.info(); // "This is an Animal class."

    const myDog = new Dog("Buddy", "Golden Retriever");
    myDog.speak();
    // Output:
    // Buddy makes a sound.
    // Buddy barks.

    console.log(myDog.fullDescription); // "Buddy is a Golden Retriever."
    myDog.nickName = "Bud";
    console.log(myDog.nickName); // "Bud"

    console.log(typeof Animal); // "function" (classes are special functions)
    console.log(myDog instanceof Dog);    // true
    console.log(myDog instanceof Animal); // true
    ```

8.  **What are generator functions?**
    Generator functions (introduced in ES6) are a special type of function that can be **paused and resumed**, allowing them to produce a sequence of values over time, rather than computing them all at once and returning them in, say, an array. They are defined using the `function*` syntax (or `*generatorMethod()` in classes).
    **Key Features:**
    1.  **`function*` syntax:** Defines a generator function.
    2.  **`yield` keyword:** Pauses the generator function's execution and returns the value of the expression following `yield`. When resumed, execution continues from that point.
    3.  **Iterator Protocol:** When a generator function is called, it doesn't execute its body immediately. Instead, it returns a special **iterator object** (Generator object).
    4.  **`next()` method:** The iterator object has a `next()` method. Calling `next()` resumes the generator's execution until the next `yield` statement or until the function terminates. `next()` returns an object with two properties: `value` (the yielded value) and `done` (a boolean indicating if the generator has finished).
    5.  **Lazy Evaluation:** Values are produced on demand, which can be memory efficient for large sequences.
    6.  **Stateful:** Generators maintain their internal state between pauses.

    ```javascript
    function* numberGenerator() {
      console.log("Generator started");
      yield 1;
      console.log("After first yield");
      yield 2;
      console.log("After second yield");
      yield 3;
      console.log("Generator finished");
      return "Done"; // The value for the last next() call when done is true
    }

    const gen = numberGenerator(); // Doesn't execute the function body yet

    console.log(gen.next()); // { value: 1, done: false } (Executes until first yield)
    console.log(gen.next()); // { value: 2, done: false } (Resumes, executes until second yield)
    console.log(gen.next()); // { value: 3, done: false } (Resumes, executes until third yield)
    console.log(gen.next()); // { value: "Done", done: true } (Resumes, finishes, returns value)
    console.log(gen.next()); // { value: undefined, done: true } (Already finished)

    // Using a generator for an infinite sequence (e.g., IDs)
    function* idGenerator() {
      let id = 1;
      while (true) {
        yield id++;
      }
    }

    const ids = idGenerator();
    console.log(ids.next().value); // 1
    console.log(ids.next().value); // 2
    console.log(ids.next().value); // 3

    // Generators are iterable, so they can be used with for...of loops
    function* fruitGenerator() {
      yield "Apple";
      yield "Banana";
      yield "Orange";
    }

    for (const fruit of fruitGenerator()) {
      console.log(fruit);
    }
    // Output:
    // Apple
    // Banana
    // Orange
    ```
    Generators are foundational for implementing iterators and are also used under the hood by `async/await` (though `async/await` is built on Promises).

9.  **Explain WeakSet in javascript.**
    A `WeakSet` (introduced in ES6) is a collection of **objects only**. It's "weak" because references to objects in a `WeakSet` are weakly held. This means if an object stored in a `WeakSet` has no other strong references elsewhere in the program, it can be garbage collected, and it will be automatically removed from the `WeakSet`.
    **Key Characteristics:**
    1.  **Stores Objects Only:** Cannot store primitive values (strings, numbers, etc.). Attempting to add a primitive will throw a `TypeError`.
    2.  **Weak References:** Does not prevent garbage collection of its items if they are not referenced elsewhere. This is its primary use case: associating metadata with objects without preventing their cleanup.
    3.  **Not Iterable:** You cannot iterate over the items in a `WeakSet` (e.g., using `forEach` or a `for...of` loop). This is because the items can be removed by the garbage collector at any time, making iteration unreliable.
    4.  **No `size` Property:** For the same reason (unpredictable collection size due to GC), `WeakSet` does not have a `size` property.
    5.  **Methods:**
        *   `add(value)`: Adds an object to the `WeakSet`.
        *   `has(value)`: Returns `true` if the object is in the `WeakSet`, `false` otherwise.
        *   `delete(value)`: Removes the object from the `WeakSet`.

    ```javascript
    let ws = new WeakSet();

    let obj1 = { name: "Alice" };
    let obj2 = { name: "Bob" };

    ws.add(obj1);
    ws.add(obj2);

    console.log(ws.has(obj1)); // true
    console.log(ws.has(obj2)); // true

    // ws.add(123); // TypeError: Invalid value used in WeakSet

    // Demonstrating weak reference (conceptual, GC behavior is not directly controllable)
    obj1 = null; // Remove the strong reference to obj1

    // At some point, if obj1 is garbage collected (and had no other strong refs),
    // it will be automatically removed from ws.
    // console.log(ws.has(obj1)); // Eventually might become false after GC,
    // but difficult to demonstrate deterministically. The original obj1 reference is lost.

    // Use case: Tracking objects that should not prevent GC
    let activeObjects = new WeakSet();
    class SomeComponent {
      constructor() {
        activeObjects.add(this);
      }
      destroy() {
        activeObjects.delete(this);
        console.log("Component destroyed. Is it in active set?", activeObjects.has(this));
      }
    }

    let comp1 = new SomeComponent();
    let comp2 = new SomeComponent();
    console.log("comp1 active?", activeObjects.has(comp1)); // true

    comp1.destroy(); // Component destroyed. Is it in active set? false
    comp1 = null; // Allow comp1 to be garbage collected
    // If comp1 is GC'd, it's removed from activeObjects.
    ```

10. **Why do we use callbacks?**
    (This question is similar to question 23 from the general list, but might be asked for deeper understanding in an experienced context).
    Callbacks are functions passed as arguments to other functions, to be executed later. We use them primarily for:
    1.  **Asynchronous Operations:** JavaScript is single-threaded. To prevent blocking the main thread during long operations (like I/O: network requests, file system access, timers), these operations are performed asynchronously. Callbacks provide a way to specify what code should run *after* the asynchronous operation completes (either successfully or with an error).
        *   *Example:* `setTimeout`, `fetch` (older XHR used them more directly), Node.js file system operations.
    2.  **Event Handling:** In UIs (both browser and other environments), callbacks are used as event listeners/handlers. When an event occurs (e.g., a button click, mouse move, key press), the registered callback function is executed.
        *   *Example:* `element.addEventListener('click', function() { /* I am a callback */ });`
    3.  **Higher-Order Functions & Code Reusability:** Callbacks enable more generic and reusable functions. Functions like `Array.prototype.map`, `filter`, `reduce`, and `sort` accept callback functions to define the specific operation to be performed on each element or for comparison. This allows the core logic of iteration or sorting to be separated from the specific action.
        *   *Example:* `numbers.map(num => num * 2);` (the arrow function is a callback)
    4.  **Modularity and Separation of Concerns:** Callbacks can help decouple parts of your code. A function can perform a general task and then delegate specific subsequent actions to a callback provided by the caller.
    5.  **Continuation-Passing Style (CPS):** A programming style where control is passed explicitly via functions (continuations/callbacks) rather than direct return values. While not always explicit, callbacks are a form of this.

    ```javascript
    // Asynchronous example (setTimeout)
    console.log("Start");
    setTimeout(() => {
      console.log("Callback executed after 2 seconds"); // This is the callback
    }, 2000);
    console.log("End"); // This logs before the callback

    // Higher-Order Function example (Array.filter)
    const numbers = [1, 2, 3, 4, 5, 6];
    const isEven = (num) => num % 2 === 0; // Callback function
    const evenNumbers = numbers.filter(isEven);
    console.log(evenNumbers); // [2, 4, 6]
    ```
    While powerful, deeply nested callbacks can lead to "callback hell," which is why Promises and async/await were introduced as more manageable alternatives for asynchronous programming.

11. **Explain WeakMap in javascript.**
    A `WeakMap` (introduced in ES6) is a collection of **key-value pairs** where the **keys must be objects**, and the values can be arbitrary. Similar to `WeakSet`, `WeakMap` holds its keys "weakly."
    **Key Characteristics:**
    1.  **Keys Must Be Objects:** Primitive values cannot be used as keys. Attempting to use a primitive key will throw a `TypeError`.
    2.  **Weak References to Keys:** If an object used as a key in a `WeakMap` has no other strong references, it can be garbage collected. When a key is garbage collected, its corresponding key-value pair is automatically removed from the `WeakMap`.
    3.  **Use Case: Associating Data with Objects Privately/Without Memory Leaks:** `WeakMap` is excellent for attaching additional data to an object without modifying the object directly and without preventing the object from being garbage collected if it's no longer needed.
    4.  **Not Iterable:** You cannot iterate over the keys, values, or entries of a `WeakMap` (e.g., no `forEach`, `keys()`, `values()`, `entries()` methods that return iterators). This is because the set of keys can change at any time due to garbage collection.
    5.  **No `size` Property:** For the same reason, `WeakMap` does not have a `size` property.
    6.  **Methods:**
        *   `set(key, value)`: Adds or updates a key-value pair. `key` must be an object.
        *   `get(key)`: Returns the value associated with the `key`, or `undefined` if the key is not found.
        *   `has(key)`: Returns `true` if a value is associated with the `key`, `false` otherwise.
        *   `delete(key)`: Removes the key-value pair associated with the `key`.

    ```javascript
    let wm = new WeakMap();

    let user1 = { id: 1 };
    let user2 = { id: 2 };

    let userData = {
      [user1.id]: { preferences: "dark mode" }, // Not how WeakMap works, just for illustration
      [user2.id]: { lastLogin: "2023-10-26" }
    };

    // Correct usage of WeakMap: keys are objects
    wm.set(user1, { preferences: "dark mode" });
    wm.set(user2, { lastLogin: "2023-10-26" });

    console.log(wm.get(user1)); // { preferences: "dark mode" }
    console.log(wm.has(user2)); // true

    // wm.set("key1", "value"); // TypeError: Invalid value used as weak map key

    // Demonstrating weak reference (conceptual)
    user1 = null; // Remove the strong reference to user1

    // If user1 is garbage collected, the entry in wm associated with the original user1 object
    // will be automatically removed.
    // console.log(wm.has(user1)); // This would be false if GC ran and user1 had no other refs.
    // The original object that user1 pointed to is what the WeakMap holds weakly.

    // Use Case: Caching computed results for objects
    const cache = new WeakMap();
    function process(obj) {
      if (cache.has(obj)) {
        console.log("Returning cached result for object:", obj);
        return cache.get(obj);
      }
      console.log("Computing result for object:", obj);
      const result = /* some expensive computation based on obj properties */;
      result = obj.data * 2; // Example computation
      cache.set(obj, result);
      return result;
    }

    let dataObj1 = { data: 10 };
    let dataObj2 = { data: 20 };

    console.log(process(dataObj1)); // Computing result for object: { data: 10 } -> 20
    console.log(process(dataObj1)); // Returning cached result for object: { data: 10 } -> 20
    console.log(process(dataObj2)); // Computing result for object: { data: 20 } -> 40

    dataObj1 = null; // If dataObj1 is now GC'd, its entry in 'cache' is also removed.
    ```

12. **What is Object Destructuring?**
    Object destructuring (introduced in ES6) is a JavaScript expression that makes it possible to unpack values from object properties into distinct variables. It provides a concise syntax to extract data from objects.
    **Key Features & Syntax:**
    1.  **Basic Destructuring:**
        ```javascript
        const person = { name: "Alice", age: 30, city: "New York" };
        const { name, age } = person;
        console.log(name); // "Alice"
        console.log(age);  // 30
        // 'city' is not destructured here
        ```
    2.  **Assigning to New Variable Names:** If you want the destructured variable to have a different name than the property name:
        ```javascript
        const { name: personName, age: personAge } = person;
        console.log(personName); // "Alice"
        console.log(personAge);  // 30
        ```
    3.  **Default Values:** Provide default values for properties that might not exist on the object:
        ```javascript
        const { country = "USA" } = person;
        console.log(country); // "USA" (since 'country' property doesn't exist on 'person')

        const { city = "Unknown" } = person;
        console.log(city); // "New York" (default not used as property exists)
        ```
    4.  **Nested Destructuring:** Destructure properties from nested objects:
        ```javascript
        const user = {
          id: 123,
          info: {
            firstName: "John",
            lastName: "Doe",
            address: { street: "123 Main St", city: "Anytown" }
          }
        };
        const { id, info: { firstName, address: { city: userCity } } } = user;
        console.log(id);        // 123
        console.log(firstName); // "John"
        console.log(userCity);  // "Anytown"
        ```
    5.  **Rest in Object Destructuring:** Collect remaining properties into a new object:
        ```javascript
        const options = { title: "Menu", width: 100, height: 200, color: "red" };
        const { title, ...rest } = options;
        console.log(title); // "Menu"
        console.log(rest);  // { width: 100, height: 200, color: "red" }
        ```
    6.  **Function Parameters:** Can be used to unpack object arguments directly in function parameters:
        ```javascript
        function displayUser({ name, age, city = "Unknown" }) {
          console.log(`Name: ${name}, Age: ${age}, City: ${city}`);
        }
        displayUser({ name: "Bob", age: 25 }); // Name: Bob, Age: 25, City: Unknown
        displayUser({ name: "Charlie", age: 35, city: "London" }); // Name: Charlie, Age: 35, City: London
        ```
    Object destructuring makes code more readable and concise when working with object properties.

13. **Difference between prototypal and classical inheritance**

    | Feature                 | Prototypal Inheritance (JavaScript)                                  | Classical Inheritance (e.g., Java, C++)                      |
    | :---------------------- | :------------------------------------------------------------------- | :----------------------------------------------------------- |
    | **Core Concept**        | Objects inherit directly from other objects (prototypes).            | Objects are instances of classes, which inherit from other classes. |
    | **Mechanism**           | An object has a prototype link (`[[Prototype]]`) to another object. Property lookup follows this chain. | Classes define blueprints. Subclasses extend superclasses, inheriting members. |
    | **"Blueprint"**         | The "blueprint" is an existing object (the prototype).             | The "blueprint" is a class definition.                       |
    | **Object Creation**     | New objects are often created by cloning/extending a prototype object (e.g., `Object.create()`) or via constructor functions whose `prototype` property is used. | New objects are instantiated from classes using `new ClassName()`. |
    | **Flexibility**         | Generally more flexible; objects can acquire new properties/methods at runtime. Prototypes can be modified, affecting all objects that inherit from them. | More rigid; class structure is defined at compile-time (or definition time). |
    | **Multiple Inheritance**| Not directly supported, but can be simulated via mixins or composition. | Some languages support it directly (e.g., C++), others don't (e.g., Java uses interfaces). |
    | **`this` behavior**     | `this` is dynamic, based on how a function is called.                | `this` (or `self`) typically refers to the instance of the class. |
    | **"Is-a" Relationship** | An object "behaves like" or "delegates to" its prototype.          | An instance "is an" instance of its class and superclasses.   |
    | **ES6 Classes**         | JavaScript ES6 classes provide syntactic sugar over prototypal inheritance, making it look more like classical. Underneath, it's still prototypal. | Fundamental to the language's OO model.                      |

    **Example (Prototypal):**
    ```javascript
    const animal = {
      eat: function() { console.log("Eating..."); }
    };
    const dog = Object.create(animal); // dog's prototype is animal
    dog.bark = function() { console.log("Woof!"); };
    dog.eat(); // "Eating..." (delegates to animal)
    dog.bark(); // "Woof!"
    ```

    **Conceptual Example (Classical - Pseudocode-like):**
    ```
    // class Animal {
    //   public void eat() { System.out.println("Eating..."); }
    // }
    // class Dog extends Animal {
    //   public void bark() { System.out.println("Woof!"); }
    // }
    // Dog myDog = new Dog();
    // myDog.eat();
    // myDog.bark();
    ```
    In essence, prototypal inheritance is about objects inheriting from objects, while classical inheritance is about classes inheriting from classes, and objects being instances of those classes.

14. **What is a Temporal Dead Zone?**
    The Temporal Dead Zone (TDZ) is a behavior in JavaScript associated with variables declared using `let` and `const` (and also `class` declarations).
    *   Variables declared with `let` and `const` *are* hoisted to the top of their block scope, but they are **not initialized**.
    *   The TDZ is the period between the start of the block and the actual declaration of the `let` or `const` variable.
    *   Accessing (reading or writing) a `let` or `const` variable within its TDZ (i.e., before its declaration line is executed) will result in a `ReferenceError`.
    *   This behavior helps prevent bugs by ensuring variables are not used before they are properly declared and (optionally for `let`, mandatorily for `const`) initialized.

    ```javascript
    function tdzExample() {
      // Start of TDZ for myLet and myConst

      // console.log(myLet);   // ReferenceError: Cannot access 'myLet' before initialization
      // console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization

      // Even typeof throws an error in TDZ for let/const
      // console.log(typeof myLet); // ReferenceError

      let myLet = "Hello";   // End of TDZ for myLet. myLet is initialized.
      const myConst = "World"; // End of TDZ for myConst. myConst is initialized.

      console.log(myLet);   // "Hello"
      console.log(myConst); // "World"
    }
    tdzExample();

    // Compare with var (no TDZ, hoisted and initialized to undefined)
    function varExample() {
      console.log(myVar); // undefined (hoisted, initialized to undefined)
      var myVar = "I am var";
      console.log(myVar); // "I am var"
    }
    varExample();
    ```
    The TDZ exists from the moment the scope is entered until the variable's declaration is processed.

15. **What do you mean by JavaScript Design Patterns?**
    JavaScript Design Patterns are reusable, well-tested solutions to commonly occurring problems within a given context in JavaScript software design. They are not specific algorithms or pieces of code, but rather general concepts or templates for structuring code to solve particular challenges in an elegant and efficient way.
    Using design patterns leads to:
    *   **Maintainability:** Code becomes easier to understand and modify.
    *   **Reusability:** Patterns provide proven solutions that can be adapted.
    *   **Communication:** Developers can use pattern names as a common vocabulary.
    *   **Robustness:** Patterns often address subtle issues and edge cases.

    **Categories and Examples:**
    1.  **Creational Patterns:** Deal with object creation mechanisms.
        *   **Constructor Pattern:** Using constructor functions or classes to create objects (e.g., `new Person()`).
        *   **Factory Pattern:** A function or method that creates objects without exposing the instantiation logic to the client.
            ```javascript
            function createUser(type, name) {
              if (type === 'admin') return { name, isAdmin: true, greet: () => console.log(`Admin ${name}`) };
              return { name, isAdmin: false, greet: () => console.log(`User ${name}`) };
            }
            const admin = createUser('admin', 'Alice');
            ```
        *   **Singleton Pattern:** Ensures a class has only one instance and provides a global point of access to it.
        *   **Prototype Pattern:** Creating new objects by cloning an existing prototype object (see question B2).
        *   **Module Pattern (often uses IIFEs and closures):** Encapsulates "private" and "public" members.

    2.  **Structural Patterns:** Deal with object composition and relationships.
        *   **Adapter Pattern:** Allows objects with incompatible interfaces to collaborate.
        *   **Decorator Pattern:** Adds new functionality to an object dynamically without altering its class.
        *   **Facade Pattern:** Provides a simplified interface to a complex subsystem.
        *   **Proxy Pattern:** Provides a surrogate or placeholder for another object to control access to it.

    3.  **Behavioral Patterns:** Deal with algorithms and assignment of responsibilities between objects.
        *   **Observer Pattern (Pub/Sub):** Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. (Used in event handling).
        *   **Command Pattern:** Encapsulates a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
        *   **Iterator Pattern:** Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
        *   **Strategy Pattern:** Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

    Understanding design patterns helps in writing more organized, scalable, and maintainable JavaScript applications.

16. **Is JavaScript a pass-by-reference or pass-by-value language?**
    JavaScript is often described as **"pass-by-value,"** but this can be confusing when it comes to objects. A more accurate description is:
    *   **For Primitive Types (String, Number, Boolean, Null, Undefined, Symbol, BigInt):** JavaScript passes them **by value**. This means when you pass a primitive to a function, a *copy* of the value is created and passed to the function. Any modifications to the parameter inside the function do not affect the original variable outside.
    *   **For Object Types (Object, Array, Function, etc.):** JavaScript passes them by **"pass-by-value of the reference"** or **"pass-by-sharing."**
        *   When an object is passed to a function, a *copy of the reference* (the memory address) to that object is passed.
        *   Both the original variable and the function parameter now point to the *same object* in memory.
        *   Therefore, if you modify a *property* of the object through the function parameter, the original object will be affected because they both refer to the same underlying data.
        *   However, if you *reassign* the function parameter to a completely new object, it will not affect the original variable. The parameter will now point to a new memory location, while the original variable still points to the old one.

    ```javascript
    // Primitive (Pass by Value)
    let myNumber = 10;
    function changePrimitive(num) {
      num = 20; // num is a copy of myNumber's value
      console.log("Inside function (primitive):", num); // 20
    }
    changePrimitive(myNumber);
    console.log("Outside function (primitive):", myNumber); // 10 (original unchanged)

    // Object (Pass by Value of the Reference)
    let myObject = { value: "original" };
    function changeObject(objParam) {
      // Modifying a property of the object objParam refers to
      objParam.value = "modified"; // This affects the original myObject
      console.log("Inside function (property modified):", objParam.value); // "modified"

      // Reassigning the parameter objParam to a new object
      objParam = { value: "new object" }; // objParam now points to a different object
      console.log("Inside function (parameter reassigned):", objParam.value); // "new object"
    }

    changeObject(myObject);
    console.log("Outside function:", myObject.value); // "modified" (original object's property was changed)
                                                    // The reassignment inside the function did not affect myObject
    ```
    So, the "value" that is passed for objects is the memory address (the reference).

17. **Difference between Async/Await and Generators usage to achieve the same functionality.**
    Both `async/await` and Generators (with a runner/co-routine) can be used to manage asynchronous operations and write asynchronous code in a more synchronous-looking style. However, `async/await` is generally preferred for its simplicity and direct integration with Promises.

    | Feature              | `async/await`                                                                | Generators (with a runner)                                                  |
    | :------------------- | :--------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
    | **Primary Purpose**  | Specifically designed to simplify working with Promises for asynchronous operations. | General-purpose for creating iterators and pausable functions; can be adapted for async control flow. |
    | **Underlying Mechanism** | Syntactic sugar built on top of Promises. An `async` function implicitly returns a Promise. `await` pauses execution until a Promise settles. | Uses `function*` and `yield`. `yield` pauses execution. Requires a "runner" function to manage the generator and handle yielded values (often Promises). |
    | **Return Value**     | An `async` function always returns a Promise. The resolved value of the Promise is what the `async` function `return`s (or `undefined` if no explicit return). | A generator function returns an iterator object. The runner orchestrates its execution. |
    | **Error Handling**   | Standard `try...catch` blocks can be used around `await` expressions, just like synchronous code. Rejected Promises are caught. | Error handling is more complex. The runner needs to call `iterator.throw()` or propagate errors from yielded Promises. `try...catch` can be used inside the generator. |
    | **Readability**      | Generally considered more readable and closer to synchronous code style for async tasks. | Can be more verbose and less intuitive for typical async operations due to the need for a runner. |
    | **Complexity**       | Simpler to use for common asynchronous patterns.                              | More powerful and flexible for complex control flows (e.g., custom iteration, advanced coroutines), but more complex to set up for basic async. |
    | **Use Case Focus**   | Best for Promise-based asynchronous workflows.                               | Broader applications including lazy evaluation, infinite sequences, custom iteration protocols, and complex state machines. |

    **Achieving similar async flow:**

    **Using `async/await` (Preferred for async operations):**
    ```javascript
    function fetchData(id) {
      return new Promise(resolve => setTimeout(() => resolve(`Data for ${id}`), 500));
    }

    async function processData() {
      try {
        console.log("Starting async/await process...");
        const data1 = await fetchData(1);
        console.log(data1);
        const data2 = await fetchData(2);
        console.log(data2);
        console.log("Async/await process finished.");
        return "All data processed";
      } catch (error) {
        console.error("Async/await Error:", error);
      }
    }
    processData().then(result => console.log(result));
    ```

    **Using Generators (with a simple runner):**
    ```javascript
    function fetchDataGen(id) { // Same fetchData as above
      return new Promise(resolve => setTimeout(() => resolve(`Data for ${id} (gen)`), 500));
    }

    function* generatorProcess() {
      try {
        console.log("Starting generator process...");
        const data1 = yield fetchDataGen(1); // yield a Promise
        console.log(data1);
        const data2 = yield fetchDataGen(2); // yield another Promise
        console.log(data2);
        console.log("Generator process finished.");
        return "All data processed (gen)";
      } catch (error) {
        console.error("Generator Error:", error);
      }
    }

    // Simple generator runner (co-routine)
    function runGenerator(genFunc) {
      const iterator = genFunc();

      function step(nextF) {
        let iteratorResult;
        try {
            iteratorResult = nextF();
        } catch (e) {
            return Promise.reject(e); // Catch errors from sync part of generator
        }

        const { value, done } = iteratorResult;

        if (done) {
          return Promise.resolve(value); // Generator finished
        }

        // Assuming the yielded value is a Promise
        return Promise.resolve(value).then(
          res => step(() => iterator.next(res)), // Feed resolved value back
          err => step(() => iterator.throw(err)) // Propagate error back
        );
      }
      return step(() => iterator.next(undefined)); // Start the generator
    }

    runGenerator(generatorProcess).then(result => console.log(result));
    ```
    `async/await` is essentially a more refined and standardized version of the generator + runner pattern specifically for Promises.

18. **What are the primitive data types in JavaScript?**
    (This is a repeat of question 1 from the general list, often asked to ensure foundational knowledge is solid.)
    JavaScript has seven primitive data types:
    1.  **String:** Represents textual data. (e.g., `"hello"`, `'world'`)
    2.  **Number:** Represents numeric values, including integers, floating-point numbers, `Infinity`, `-Infinity`, and `NaN`. (e.g., `42`, `3.14`, `NaN`)
    3.  **Boolean:** Represents logical values: `true` or `false`.
    4.  **Null:** Represents the intentional absence of any object value. It is a primitive value, though `typeof null` returns `"object"` (a historical quirk).
    5.  **Undefined:** Represents a variable that has been declared but not yet assigned a value, or a function argument not provided.
    6.  **Symbol (ES6):** Represents a unique and immutable identifier, often used as keys for object properties to avoid name collisions. (e.g., `Symbol('description')`)
    7.  **BigInt (ES2020):** Represents integers with arbitrary precision, larger than what `Number` can safely represent. (e.g., `12345678901234567890n`)

    Primitives are immutable (their values cannot be changed directly) and are compared by value.

19. **What is the role of deferred scripts in JavaScript?**
    Deferred scripts, specified using the `defer` attribute in a `<script>` tag (`<script src="script.js" defer></script>`), affect how external JavaScript files are downloaded and executed by the browser.
    **Role and Behavior:**
    1.  **Asynchronous Download:** The browser downloads the script file asynchronously, in parallel with HTML parsing. This means the HTML parsing is **not blocked** by the script download.
    2.  **Execution After HTML Parsing:** The deferred script is guaranteed to execute only **after** the HTML document has been fully parsed and the DOM is ready (specifically, before the `DOMContentLoaded` event fires).
    3.  **Execution Order:** If multiple deferred scripts are present, they are executed in the **order they appear** in the HTML document. This is a key difference from scripts with the `async` attribute.
    4.  **External Scripts Only:** The `defer` attribute only works for external scripts (those with a `src` attribute). It has no effect on inline scripts.

    **Benefits:**
    *   **Non-Blocking Parsing:** Improves page load performance as HTML parsing can continue while the script downloads.
    *   **DOM Ready:** Scripts can safely access and manipulate the DOM because they run after the DOM is built.
    *   **Preserved Order:** Useful when scripts depend on each other or need to execute in a specific sequence.

    **Compared to `async`:**
    *   `async` scripts also download asynchronously but execute as soon as they are downloaded, potentially interrupting HTML parsing. Their execution order is not guaranteed.
    *   `defer` scripts wait for HTML parsing and execute in order.

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Deferred Scripts</title>
        <!-- These scripts download in parallel with HTML parsing -->
        <!-- They execute in order AFTER HTML is parsed, before DOMContentLoaded -->
        <script src="lib.js" defer></script>
        <script src="main.js" defer></script>
        <script>
            // This inline script might execute before or after DOM parsing starts,
            // but deferred scripts will execute after the whole document is parsed.
            console.log("Inline script in head.");
        </script>
    </head>
    <body>
        <p>Page content.</p>
        <script>
            document.addEventListener('DOMContentLoaded', () => {
                console.log("DOMContentLoaded event fired."); // Deferred scripts run before this
            });
            console.log("Inline script in body.");
        </script>
    </body>
    </html>
    ```
    **Use Case:** `defer` is generally recommended for most scripts, especially those that need to interact with the DOM and whose execution order matters, as it provides a good balance of performance and predictability.

20. **What has to be done in order to put Lexical Scoping into practice?**
    Lexical scoping (also known as static scoping) is a fundamental characteristic of how JavaScript (and many other programming languages) resolves variable names. It's not something you "put into practice" by enabling a feature; rather, it's **how the language inherently works.**
    **Lexical scoping means that the scope of a variable is determined by its position within the source code at the time the code is written (lexed/parsed), not by where the function is called (dynamic scope).**

    **Understanding and working *with* lexical scoping involves:**
    1.  **Writing Code:** Simply by writing JavaScript code, you are using lexical scoping. The JavaScript engine automatically determines scopes based on where functions and blocks (`{}`) are defined.
    2.  **Understanding Nesting:** When you nest functions or blocks, you create nested lexical scopes. Inner scopes have access to variables in their outer scopes, forming a scope chain.
        ```javascript
        let globalVar = "global";
        function outer() {
          let outerVar = "outer"; // outer's lexical scope starts here
          function inner() {
            let innerVar = "inner"; // inner's lexical scope
            console.log(innerVar, outerVar, globalVar); // Accesses variables from all parent lexical scopes
          }
          inner(); // inner's scope is determined by where it's written inside outer
        }
        outer();
        ```
    3.  **Closures:** Closures are a direct consequence of lexical scoping. An inner function "remembers" its lexical environment (the variables from its outer scopes) even after the outer function has returned.
        ```javascript
        function makeGreeter(greeting) {
          // greeting is in makeGreeter's lexical scope
          return function(name) {
            // This inner function forms a closure, "remembering" greeting
            console.log(greeting + ", " + name);
          };
        }
        const sayHello = makeGreeter("Hello"); // sayHello is a closure
        sayHello("World"); // "Hello, World" - 'greeting' is accessed via the closure
        ```
    4.  **`let` and `const`:** These ES6 keywords introduce block scoping, which is also lexical. The scope of a `let` or `const` variable is the block (`{...}`) in which it is defined.
    5.  **Avoiding Global Pollution:** Understanding lexical scope helps in writing modular code and avoiding unintended modification of global variables by properly encapsulating variables within function or block scopes.

    **In summary, you don't "do" anything special to enable lexical scoping; it's the default and only scoping mechanism for variable resolution in JavaScript (for user-defined variables). Your task as a developer is to understand how it works to write predictable and maintainable code.** The JavaScript engine handles the "practice" of lexical scoping during parsing and execution.

  ```javascript
**Most asked questions with Short answers**
Explain the differences between var, let, and const:
var has function scope and can be reassigned and redeclared within its scope.
let has block scope and can be reassigned but not redeclared within its scope.
const has block scope and cannot be reassigned or redeclared once initialized.

What is a closure in JavaScript?
A closure is a function that has access to variables from an outer function even after the outer function has finished executing. Closures "remember" the environment in which they were created.

Explain scope and scope chain in JavaScript.
Scope determines the accessibility of variables and functions at various parts of the code. There are three types of scopes: global scope, function scope, and block scope.
The scope chain is used by the JavaScript engine to find variables. If a variable is not found in the local scope, it checks the outer scope, and finally the global scope.

What is hoisting in JavaScript?
Hoisting is a JavaScript concept where variable and function declarations are moved to the top of their scope before code execution. This allows variables and functions to be used before they are declared, as long as they are declared before they are used in a function.

What is the purpose of async and await in JavaScript?
async and await are used for asynchronous programming in JavaScript. The async keyword is used to declare an asynchronous function, which automatically returns a promise. The await keyword is used to wait for a promise to resolve before continuing the execution of the function.

Explain the difference between == and === operators.
The == operator compares values after performing type coercion if necessary. The === operator compares both values and types without type coercion.

What is the difference between passed by value and passed by reference?
Primitive data types (like numbers, strings, and booleans) are passed by value, meaning a copy of the value is passed to the function. Non-primitive data types (like objects and arrays) are passed by reference, meaning a reference to the original object is passed.

What is a higher-order function in JavaScript?
A higher-order function is a function that can accept other functions as arguments or return functions as their results. Examples include map, filter, and reduce.

What is the purpose of the setTimeout() function in JavaScript?
The setTimeout() function is used to execute a function or a piece of code after a specified delay (in milliseconds).

How can you check if an array includes a certain value?
The includes() method is used to check if an array includes a certain value. It returns true if the value is found, and false otherwise.
```
---

Good luck to all aspiring developers!
