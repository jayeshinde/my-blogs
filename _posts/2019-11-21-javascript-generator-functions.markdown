---
layout: post
title:  "ES6 - Generator Functions"
date:   2019-11-21 21:53:23 +0400
categories: javascript interview questions
---
One of the most powerful feature of ECMA6 is Generator Functions, which is the most favourite topics for interviewers. Generator functions are nothing but, can be exited and later re-entered, where their context will be saved across re-entrances. ie. <mark>Can be stopped in Midway and continued from where it is Stopped.</mark>

`Some of the tricky question asked:`

- What is the generator function return type?
- Can generator function support "return" apart from "yield"?
- How we can pass arguments or new value to generator function?
- Generators are construct-able?
- How the generator function works?

`Below section of the post describe all the answers.`

Generator object, which confirms to Iterable and Iterator protocol. Used in conjunction with Promises they resolve the problem with [Callback Hell][callback-hell] and [Inversion of Control][inversion-control].

Calling a generator function does not execute its body immediately; an iterator object for the function is returned instead. 

When the iterator's next() method is called, the generator function's body is executed until the first [yield][yield-1] expression, which specifies the value to be returned from the iterator or, with [yield*][yield-2], delegates to another generator function. 

The next() method returns an object with a value property containing the yielded value and a done property which indicates whether the generator has yielded its last value, as a boolean. 
<mark>{ value: Any, done: false | true }</mark>

Calling the next() method with an argument will resume the generator function execution, replacing the yield expression where execution was paused with the argument from next().

A return statement in a generator, when executed, will make the generator finish <mark>({ value: Any, done: true }).</mark>

If an error thrown inside the generator will make the generator finished -- unless caught within the generator's body.

When a generator is finished, subsequent next calls will not execute any of that generator's code, they will just return an object of this form: <mark>{value: undefined, done: true}.</mark>

`Interview Tips`

- Write a function which will print all the letters of a given sentences sequentially, "United We Stand".
{% highlight javascript %}
function* charGenerator(str) {
  for(var i=0; i < str.length; i++) {
  	yield str[i];
  }
}

var str = "United We Stand";
var gen = charGenerator([...str]);

console.log(gen.next()); // Object { value: "U", done: false }
console.log(gen.next()); // Object { value: "i", done: false }
console.log(gen.next()); // Object { value: "n", done: false }
console.log(gen.next()); // Object { value: "t", done: false }
console.log(gen.next()); // Object { value: "e", done: false }
console.log(gen.next()); // Object { value: "d", done: false }
console.log(gen.next()); // Object { value: " ", done: false }
console.log(gen.next()); // Object { value: "W", done: false }
console.log(gen.next()); // Object { value: "e", done: false }
console.log(gen.next()); // Object { value: " ", done: false }
console.log(gen.next()); // Object { value: "S", done: false }
console.log(gen.next()); // Object { value: "t", done: false }
console.log(gen.next()); // Object { value: "a", done: false }
console.log(gen.next()); // Object { value: "n", done: false }
console.log(gen.next()); // Object { value: "d", done: false }
console.log(gen.next()); // Object { value: undefined, done: true }
{% endhighlight %}

`Some of the True Statements about Generators:`
- Generators can be used to create infinite data-series, that never ends.
- Generators can be used as observers which receives the new value using next(val)
- Generators are Memory Efficient as they generate the value which is needed.
- Generator Objects are one time access only. Once you exhausted all value, you can not iterate over.
- Generators are defined in an expressions.
- Generators are not constructable.
- Generators can be used as Computed Property or Object Method.
- Generators support "return" statement post which it's executions gets stopped.
- Generators are commonly used in Redux-Saga based middleware, which construct most of the Actions part.

[callback-hell]: http://callbackhell.com/
[inversion-control]: https://frontendmasters.com/courses/rethinking-async-js/callback-problems-inversion-of-control/
[yield-1]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield*
[yield-2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield