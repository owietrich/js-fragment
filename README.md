js-fragment
===========

A document fragment is a dom node that is in memory and isn't part of the the main DOM tree. For that reason appending children to it does not cause any page reflow or repaint which can result in possible better performance.


## Out of the flow

Could you tell what is wrong with this example? 

```js
for(var l = 1000; l--;) {
	var a = document.createElement('a');
	a.innerHTML = 'some text';
	a.className = 'link';
	document.body.appendChild(a);
}
```

This loop basically trigger one reflow per anchor appended in the document (i.e 1000). By using document fragment you could optimize your code and only trigger one reflow:

```js
var fragment = document.createDocumentFragment();
for(var l = 1000; l--;) {
	var a = document.createElement('a');
	a.innerHTML = 'some text';
	a.className = 'link';
	fragment.appendChild(a);
}
document.body.appendChild(fragment);
```

When we append the fragment to an element using `appendChild`, all the children inside the fragment are actually appended to the element. How cool is that?

  > moder browsers do an amazing job optimizing node insertions and for the example above, the performance will be slightly similar either you use a naive approach or document fragments. However document fragments do really well for heavy computations.

It is customary to say that dom is expensive but I would argue with people saying that it is slow. I truly think that there is some better ways to interact with dom nodes and using document fragment is one of them.


