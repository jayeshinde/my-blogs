---
layout: post
title:  "Need for Virtual Dom"
date:   2020-11-23 21:53:23 +0400
categories: react web development
---

We are hearing the term `Virtual Dom` from past couple of years, as most of the javascript libraries like React, Vue, Next, Gastby, etc are using it. From the concept wise it is simple thing to understand but many of us still not aware or sure why to use Virtual DOM. 
In this article, we will see the the What is Virtual DOM, its Role and Need in modern web application development.

### WHAT is Virtual DOM 
- According to [React] docs virtual DOM is

`The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM.`

- Basically The Document Object Model (DOM) is an application programming interface (API) for valid HTML and well-formed XML documents.

- Virtual DOM is a representation of the real DOM, whose creation / manipulation is handled by browsers. Advance frameworks/libraries like React, Vue will create a tree of elements similar to Real DOM in memory which forms the Virtual DOM.

For example:
```javascript

<ul class="fruits">
  <li>Apple</li>
  <li>Banana</li>
  <li>Guva</li>
</ul>

```
Virtual DOM Representation
```javascript
{
    type: "ul",
    props: {
        "class": "fruits" 
    },
    children: [
        {
            type: "li",
            props: null,
            children: [
                "Apple"
            ]
        },
        {
            type: "li",
            props: null,
            children: [
                "Banana"
            ]
        },
        {
            type: "li",
            props: null,
            children: [
                "Guva"
            ]
        }
    ]
}
```

### Need for Virtual DOM
In last 5-6 years server side rendering of website gone, and browser based rendering increased. Single Page Applications, motivated based on the single DOM manipulation, where un-optimized way killing the UI rendering, making it harder to use. Thus need of Virtual DOM arises and many frameworks/libraries come up with their own way of managing the same. Like Angular, React, Vue have their own way to managing the DOM.

For example, lets see below piece of code which is much inspired from Backbone js to render the list of array in html.

```javascript
function generateList(fruits) {
    let ul = document.createElement('ul');
    document.getElementByClassName('.fruits').appendChild(ul);
    fruits.forEach(function (item) {
        let li = document.createElement('li');
        ul.appendChild(li);
        li.innerHTML += item;
    });
    return ul
}
let fruits = ['Apple', 'Banana', 'Guva']
 document.getElementById('#list').innerHtml =  generateList(fruits)

```

To change the list, we need to call the function `generateList` again.
```javascript

 fruits = ['Apple', 'Banana', 'Orange']
 document.getElementById('#list').innerHtml = generateList(fruits)

```

The problem with this approach is only the text of single fruit is changed but a new list is generated and updated to DOM. This operation become costlier when elements list is massive, causing serious issues in performance. We can change the unoptimised code like below. This will reduce the number of operations in DOM.

```javascript
document.querySelector('li').innerText = fruits[0]
```

If the size of list large then you can see the difference. This was the problem we had in older frameworks like backbone js.

`To solve above problem we need Virtual DOM.`

What modern frameworks like React does is whenever something is changed in the state/props, a new virtual DOM representation will be created and it will be compared with the previous one, known as Diffing Algorithm. 
In our example, the only change will be "Guva" to "Orange". Since only text is changed instead of replacing whole list react will update the DOM by the following code.

```javascript
document.querySelector('li').innerText = "Orange"
```

### Is Virtual DOM is faster then Real DOM

No, virtual DOM is not faster than the real DOM. Under the hood virtual DOM also uses real DOM to render the page or content. So there is no way that virtual DOM is faster than real dom.

For more details about Diffing Algorithms one can find on react official document under [Reconcilation]

[React]: https://reactjs.org/docs/faq-internals.html#:~:text=The%20virtual%20DOM%20(VDOM)%20is,This%20process%20is%20called%20reconciliation.&text=They%20may%20also%20be%20considered,virtual%20DOM%E2%80%9D%20implementation%20in%20React.
[Reconcilation]: https://reactjs.org/docs/reconciliation.html