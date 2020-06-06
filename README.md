# js-summary
Brief basic JavaScript information

## 1. Event delegation

The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them – we put a single handler on their common ancestor.
javascript.info/event-delegation

## 2. Bubbling and capturing
The bubbling principle - when an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

The process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.
https://javascript.info/bubbling-and-capturing

## 3. Differences between .call and .apply?

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

## 6. WeakSet

WeakSet is Set-like collection that stores only objects and removes them once they become inaccessible by other means.

It is analogous to Set, but we may only add objects to WeakSet (not primitives).
An object exists in the set while it is reachable from somewhere else.
Like Set, it supports add, has and delete, but not size, keys and no iterations.

The most notable limitation of WeakMap/WeakSet is the absence of iterations, and inability to get all current content. That may appear inconvenient, but does not prevent WeakMap/WeakSet from doing their main job – be an “additional” storage of data for objects which are stored/managed at another place.
WeakMap/WeakSet are used as “secondary” data structures in addition to the “main” object storage. Once the object is removed from the main storage, if it is only found as the key of WeakMap/WeakSet, it will be cleaned up automatically.

## 7. Symbol
[Symbol]: https://javascript.info/symbol "javascript.info"
[Symbol] is a primitive type for unique identifiers. They are created with **Symbol()** call with an optional description (name).


## 8. Data and Structure types
The latest ECMAScript standard defines nine types:

Six primitive Data Types that are:
- undefined
- boolean
- number
- string
- bigint
- symbol

Special primitive **null** (typeof 'object').

**Object** is a special structural type for any constructed object instance also used as data structures: new Object, new Array, new Map, new Set, new WeakMap, new WeakSet, new Date and almost everything made with new keyword.

**Function** (every Function constructor is derived from Object constructor).

## 9. Pure functions
They must take arguments.
The same input (arguments) will always produce the same output (return).
Pure functions rely only on local state and do not mutate external state (note: console.log changes global state).
Pure functions do not produce side effects.
Pure functions cannot call impure functions.
