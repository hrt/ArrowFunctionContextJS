A method of accessing 'this' inside of an arrow function.
It can be useful to access `this` inside of functions where the context is defined by `bind` / `apply` calls.
Arrow functions do not work well with `this` - it is unbindable.

However, we can access the binded `this` using some magic:

```js
var fn = _=>{
	Error.prepareStackTrace = function(error, structuredStackTrace) {
		return structuredStackTrace[0].getThis();
	}
	try {
		null.test;
	} catch(e) {
		_this = e.stack;
	}
	delete Error.prepareStackTrace;
	console.log('_this: ' + _this)
};
fn.apply("you_can't_access_me", []);```
