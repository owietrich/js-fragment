js-fragment
===========

A document fragment is a dom node that is in memory and isn't part of the the main DOM tree. For that reason appending children to it does not cause any page reflow or repaint which can result in possible better performance.


## Overview

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

  > modern browsers do an amazing job optimizing node insertions and for the example above, the performance will be slightly similar either you use a naive approach or document fragments. However document fragments do really well for heavy computations.

It is customary to say that dom is expensive but I would argue with people saying that it is slow. It is actually faster than some alternatives such as virtual dom. I truly think that there is some better ways to interact with dom nodes and using document fragment is one of them.


If you have any questions or comments, please feel free to post an [issue](https://github.com/owietrich/js-fragment/issues).

## License

The MIT License (MIT)

Copyright (c) 2014 Olivier Wietrich <olivier.wietrich@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
