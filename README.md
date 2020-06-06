# JavaScript Summary
Brief JS basics

## 1. Event delegation
[js.info]: https://javascript.info/event-delegation
[js.info]

The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them – we put a single handler on their common ancestor.

## 2. Bubbling and capturing
[js.info]: https://javascript.info/bubbling-and-capturing
[js.info]

The bubbling principle - when an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

The process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.


## 3. Differences between .call and .apply?
[js.info]: https://javascript.info/call-apply-decorators
[js.info]

They both invoke the function they are called on, and take a ‘this’ keyword as their first argument. 
The difference is that .call passes all arguments after the first one on to the invoked function, while .apply takes an array as its second argument and passes the members of that array as arguments.

## 4. Let, Const, Var
There are two main differences of var compared to let/const:

- var variables have no block scope, they are visible minimum at the function level.
- var declarations are processed at function start (script start for globals).

These differences make var worse than let most of the time. Block-level variables is much easier to understand.

To declare a constant (unchanging) variable, use const instead of let.

## 5. Мар and WeakMap objects
Map is a collection of keyed data items, just like an Object. But the main difference is that Map allows keys of any type. Unlike objects, keys are not converted to strings.

WeakMap is Map-like collection that allows only objects as keys and removes them together with associated value once they become inaccessible by other means.
WeakMap doesn’t prevent garbage-collection of key objects.
WeakMap keys must be objects, not primitive values.
If we’re working with an object that “belongs” to another code, maybe even a third-party library, and would like to store some data associated with it, that should only exist while the object is alive – then WeakMap is exactly what’s needed.
We put the data to a WeakMap, using the object as the key, and when the object is garbage collected, that data will automatically disappear as well.

## 6. Set and WeakSet objects
[MDN-Set]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set
[MDN-Set]

The **Set** object stores unique values of any type, whether primitive values or object references.

WeakSet is Set-like collection that stores only objects and removes them once they become inaccessible by other means.

It is analogous to Set, but we may only add objects to WeakSet (not primitives).
An object exists in the set while it is reachable from somewhere else.
Like Set, it supports add, has and delete, but not size, keys and no iterations.

The most notable limitation of WeakMap/WeakSet is the absence of iterations, and inability to get all current content. That may appear inconvenient, but does not prevent WeakMap/WeakSet from doing their main job – be an “additional” storage of data for objects which are stored/managed at another place.
WeakMap/WeakSet are used as “secondary” data structures in addition to the “main” object storage. Once the object is removed from the main storage, if it is only found as the key of WeakMap/WeakSet, it will be cleaned up automatically.

## 7. Symbol
[js.info]: https://javascript.info/symbol
[js.info]

Is a primitive type for unique identifiers. They are created with **Symbol()** call with an optional description (name).


## 8. Data and Structure types
[MDN]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Data_and_Structure_types
[MDN]

The latest ECMAScript standard defines nine types:

Six primitive Data Types that are:
- Undefined
- Boolean
- String
- Number
- BigInt
- Symbol

Special primitive **Null** (typeof 'object').

**Object** is a special structural type for any constructed object instance also used as data structures: new Object, new Array, new Map, new Set, new WeakMap, new WeakSet, new Date and almost everything made with new keyword.

**Function** (every Function constructor is derived from Object constructor).

## 9. Pure and Impure functions
Pure functions:
- must take arguments
- the same input (arguments) will always produce the same output (return)
- rely only on local state and do not mutate external state (note: console.log changes global state)
- do not produce side effects
- cannot call impure functions

An impure function mutates state outside its scope. Any function that has side effects is impure.

## 9. What is a Function?
A function is a process which takes some input, called arguments, and produces some output called a return value.
Functions may serve the following purposes:
 - mapping: produce some output based on given inputs. A function maps input values to output values.
 - procedures: a function may be called to perform a sequence of steps.
 - I/O: some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network.

## 10. Higher-order Functions
A higher-order function is a function that:
 - accepts another function as an argument, or
 - returns a function as a result.

 In JavaScript, functions are first-class objects. They can be stored and passed around as values: we can assign a function to a variable or pass a function to another function.

## 11. One-Way Data Flow and Two-Way Data Binding
An application or framework with **one-way data flow** uses the model as the single source of truth.
Messages, sent from a UI in the form of events, are signaling the model to update.
Data is only flowing in one direction: from the model down. The UI input does not have direct access to the model. If we want to update state in response to changes from the UI, the input must send a message carrying the payload. The only way the UI can influence the model is through event that triggers some **setState()** method. The UI will never automagically update the model.

In **two-way data binding**, the data flows in both directions. This means that the JS can update the model and the UI can do so as well.

## 12. Destructuring assignment
[js.info]: https://javascript.info/destructuring-assignment
[js.info]

Destructuring assignment is a special syntax that allows us to “unpack” arrays or objects into a bunch of variables. Destructuring also works great with complex functions that have a lot of parameters, default values, and so on.

Examples:
 - let [firstName, lastName] = ['John', 'Doe']; // assigns 'John' to firstName variable and 'Doe' to lastName variable
 - let [firstName, surname] = 'John Doe'.split(' '); // same result
 - let [firstName, , title] = ["Julius", "Caesar", "Consul"] // ignore elements using commas
 - let [one, two, three] = new Set([1, 2, 3]) // works with any iterable
 - let [a, b, c] = "123"; // assumes string as array ["1", "2", "3"]
 - [guest, admin] = [admin, guest] // swap previously assigned values

## 13. Prototypal inheritance
If we have a **user** object with its properties and methods, we can make **admin** and **guest** as slightly modified variants of **user**. We’d like to reuse what we have in **user**, not copy/reimplement its methods, just build a new object on top of it. Prototypal inheritance is a language feature that helps in that.

In JavaScript, objects have a special hidden property **[[Prototype]]**, that is either null or references another object. That object is called “a prototype”.

When we want to read a property from object, and it’s missing, JavaScript automatically takes it from the prototype.

The property **[[Prototype]]** is internal and hidden, but there are many ways to set it. One of them is to use the special name **__proto__**, like this:
let animal = { eats: true }; let rabbit = { jumps: true };
rabbit.__proto__ = animal;

Note: **__proto__** is an old-fashoned getter/setter for **[[Prototype]]**. Modern language standard suggests using functions **Object.getPrototypeOf/Object.setPrototypeOf**.

## 14. Class Inheritance
[js.info]: https://javascript.info/class-inheritance
[js.info]

Class inheritance is a way for one class to extend another class.
So new functionality can be created on top of the existing.

 - To extend a class: **class Child extends Parent** - means Child.prototype.__proto__ = Parent.prototype, so methods are inherited.
 - When overriding a constructor, we must call parent constructor as **super()** in Child constructor before using **this**.
 - when method is overriden we still can use **super.methodName()** in a Child method to call Parent method.
 - methods remember their class/object in the internal **[[HomeObject]]** property. That’s how **super** resolves parent methods. So it’s not safe to copy a method with **super** from one object to another.
 - arrow functions don’t have their own **this** or **super**, so they transparently fit into the surrounding context.

## 15. Promise
[js.info]: https://learn.javascript.ru/promise-basics
[js.info]
[MDN]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[MDN]

The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
Instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

A Promise has three possible states:
 - pending: initial state, neither fulfilled nor rejected
 - fulfilled: meaning that the operation completed successfully
 - rejected: meaning that the operation failed

 When pending **Promise** becomes **fulfilled** or **rejected** the associated handlers queued up by a promise's **then** method are called.
 If the promise has already been fulfilled or rejected when a corresponding handler is attached, the handler will be called, so there is no race condition between an asynchronous operation completing and its handlers being attached.

## 16. Equality operators
[MDN]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality
[MDN]

The **equality** operator (==) compare operands with implicit type coercion, while **strict equality** operator (===) requires that both operands be of the same type before comparing.

**Set of rules**
 - comparison of **Objects** will return true only if both operands reference the same object.
 - comparison of **Null** and **Undefined** returns **true**.
 - when comparing a **Number** and a **String**, the String is converted to a Number value. JavaScript attempts to convert the string numeric literal to a Number type value. First, a mathematical value is derived from the string numeric literal. Next, this value is rounded to nearest Number type value.
 - if one of the operands is **Boolean**, the Boolean operand is converted to 1 if it is true and +0 if it is false.
 - if an **Object** is compared with a **Number** or **String**, JavaScript attempts to return the default value for the object. Operators attempt to convert the object to a primitive value, a String or Number value, using the valueOf and toString methods of the objects. If this attempt to convert the object fails, a runtime error is generated.
 - comparison of two **Number** returns true only if both operands have the same value. +0 and -0 are treated as the same value. If either operand is NaN, return false.
 - comparison of two **Boolean** returns true only if operands are both true or both false.