---
layout: post
title:  "ES6 - Array Slice"
date:   2019-12-12 21:53:23 +0400
categories: javascript interview questions
---
Arrays are list-like objects whose prototype has methods to perform traversal and mutations. Neither the length of JavaScript array nor their elements are fixed. Array are widely used in web applications, below will explain most widely used prototype method **Slice.** Most of the tricky questions or algorithims asked will make use of Slice methods. They plays important roles in Functional Programming.

`Important things about Slice Method:`

- It returns the shallow copy of a portation of an Array into a new array object. Original array will not be modified.
- Object references are copied into the new array. Both the original and new array refer to the same object.
- For strings, numbers and booleans (not [String][string], [Number][number], [Boolean][boolean] objects), it copies the values. So changes in one array do not affect the other array.

*Caution:*
The `slice` method is not to be confused with the `splice` method, which modifies an array in place.

`Syntax Slice`

{% highlight javascript %}
 arr.slice(begin[, end]])
{% endhighlight %}

- Both arguments are optional
- When provided negative indices, counts back from the end of array.

For more details about how it works refer [MDN Documentations][mdn-document]

`Interview Tips`

- Write a function which will rotate the characters of given string, left and then right sequentially,<br/>
for example<br/>
<mark>getShiftedString(string, shiftLeft, shiftRight)<br/></mark>
*Input:* getShiftedString("UnitedWeStand", 2, 1)<br/>
*OutPut:* nitedWeStandU

{% highlight javascript %}
function getShiftedString(s, leftShifts, rightShifts) {
  const arr = [...s]
  const netLeftShifts = (leftShifts - rightShifts) % arr.length; 
  return [...arr.slice(netLeftShifts), ...arr.slice(0, netLeftShifts)]
        .join('');
}
console.log(getShiftedString("UnitedWeStand", 2, 1));
{% endhighlight %}

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[mdn-document]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array