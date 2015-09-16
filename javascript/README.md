# function stepframeJsStyleGuide() {

## Table of Contents

1. [Types](#types)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Properties](#properties)
1. [Variables](#variables)
1. [Hoisting](#hoisting)
1. [Comparison Operators & Equality](#comparison-operators--equality)
1. [Blocks](#blocks)
1. [Comments](#comments)
1. [Whitespace](#whitespace)
1. [Commas](#commas)
1. [Semicolons](#semicolons)
1. [Type Casting & Coercion](#type-casting--coercion)
1. [Naming Conventions](#naming-conventions)
1. [Controlling Scope](#controlling-scope)
1. [Accessors](#accessors)
1. [Constructors](#constructors)
1. [Events](#events)
1. [jQuery](#jquery)
	1. [jQuery Variables](#jquery-variables)
	1. [jQuery Events](#jquery-events)
1. [Code Organization for micro sites](#microsites)
1. [Tools](#tools)

<a name="types"></a>
## Types

- **Primitives**: When you access a primitive type you work directly on its value.

	+ `string`
	+ `number`
	+ `boolean`
	+ `null`
	+ `undefined`

```javascript
	var foo = 1;
	var bar = foo;

	bar = 9;

	console.log(foo, bar); // => 1, 9
```
- **Complex**: When you access a complex type you work on a reference to its value.

	+ `object`
	+ `array`
	+ `function`

```javascript
	var foo = [1, 2];
	var bar = foo;

	bar[0] = 9;

	console.log(foo[0], bar[0]); // => 9, 9
```

**[⬆ back to top](#table-of-contents)**

<a name="objects"></a>
## Objects

- Use the literal syntax for object creation.

```javascript
	// bad
	var item = new Object();

	// good
	var item = {};
```

- Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys. It won't work in IE8. [More info](https://github.com/airbnb/javascript/issues/61).

```javascript
	// bad
	var superman = {
		default: { clark: 'kent' },
		private: true
	};

	// good
	var superman = {
		defaults: { clark: 'kent' },
		hidden: true
	};
```

- Use readable synonyms in place of reserved words.

```javascript
	// bad
	var superman = {
		class: 'alien'
	};

	// bad
	var superman = {
		klass: 'alien'
	};

	// good
	var superman = {
		type: 'alien'
	};
```

- Place the colon immediately after the key, and add a space after the colon:
```javascript
	// bad
	var superman = {
		type : 'alien'
	}

	// bad
	var superman = {
		type:'alien'
	}

	// good
	var superman = {
		type: 'alien'
	}
```

**[⬆ back to top](#table-of-contents)**

<a name="arrays"></a>
## Arrays

- Use the literal syntax for array creation.

```javascript
	// bad
	var items = new Array();

	// good
	var items = [];
```

- Use Array#push instead of direct assignment to add items to an array.

```javascript
	var someStack = [];

	// bad
	someStack[someStack.length] = 'abracadabra';

	// good
	someStack.push('abracadabra');
```

- When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

```javascript
	var len = items.length;
	var itemsCopy = [];
	var i;

	// bad
	for (i = 0; i < len; i++) {
		itemsCopy[i] = items[i];
	}

	// good
	itemsCopy = items.slice();
```

- When looping, favor forEach over a standard for loop because of readability. Use the naming convention of el, i, arr for the arguments (element, index, array). For IE8 and below, use polyfill from [mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach).

```javascript
	// okay
	function() {

		var i;
		var someArr = [0, 1, 2, 3, 4, 5, 6];

		for(i = 0; i < someArr.length; i++) {
			console.log(someArr[i]);
		}
	}

	// this is better
	function() {

		var someArr = [0, 1, 2, 3, 4, 5, 6];

		someArr.forEach(function(el, i, arr) {

			console.log(el);
		});
	}
```

**[⬆ back to top](#table-of-contents)**


<a name="strings"></a>
## Strings

- Use single quotes `''` for strings.

```javascript
	// bad
	var name = "Bob Parr";

	// good
	var name = 'Bob Parr';

	// bad
	var fullName = "Bob " + this.lastName;

	// good
	var fullName = 'Bob ' + this.lastName;
```

**[⬆ back to top](#table-of-contents)**


<a name="functions"></a>
## Functions

- Function expressions:

```javascript
	// anonymous function expression
	var anonymous = function() {

		return true;
	};

	// immediately-invoked function expression (IIFE)
	(function(window, $, nancy, undefined) {

		console.log('Welcome to the Internet. Please follow me.');
	})(window, jQuery, 'awesome');
```

- Function declarations:

```javascript
	function someFunc() {

		return true;
	}
```

- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.
- **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

```javascript
	// bad
	if (currentUser) {
		function test() {

			console.log('Nope.');
		}
	}

	// good
	var test;
	if (currentUser) {
		test = function() {

			console.log('Yup.');
		};
	}
```

- Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

```javascript
	// bad
	function nope(name, options, arguments) {

		// ...stuff...
	}

	// good
	function yup(name, options, args) {

		// ...stuff...
	}
```

**[⬆ back to top](#table-of-contents)**


<a name="properties"></a>
## Properties

- Use dot notation when accessing properties.

```javascript
	var luke = {
		jedi: true,
		age: 28
	};

	// bad
	var isJedi = luke['jedi'];

	// good
	var isJedi = luke.jedi;
```

- Use subscript notation `[]` when accessing properties with a variable.

```javascript
	var luke = {
		jedi: true,
		age: 28
	};

	function getProp(prop) {

		return luke[prop];
	}

	var isJedi = getProp('jedi');
```

**[⬆ back to top](#table-of-contents)**

<a name="variables"></a>
## Variables

- Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

```javascript
	// bad
	superPower = new SuperPower();

	// good
	var superPower = new SuperPower();
```

- Declare variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues. JavaScript is function scoped, not block scoped, so the top of a variable's scope is the top of the function.

```javascript
	// bad
	function() {

		test();
		console.log('doing stuff..');

		//..other stuff..

		var name = getName();

		if (name === 'test') {
			return false;
		}

		return name;
	}

	// good
	function() {

		var name = getName();

		test();
		console.log('doing stuff..');

		//..other stuff..

		if (name === 'test') {
			return false;
		}

		return name;
	}

	// bad
	function() {

		var someArr = [0, 1, 2, 3, 4];

		for(var i = 0; i < someArr.length; i++) {
			console.log('first: ', i);
		}

		// at this point, i has been declared twice
		for(var i = 0; i < someArray.length; i++) {
			console.log('second: ', i);
		}
	}

	// good
	function() {

		var i;
		var someArr = [0, 1, 2, 3, 4],

		for(i = 0; i < someArr.length; i++) {
			console.log('first: ', i);
		}

		for(i = 0; i < someArray.length; i++) {
			console.log('second: ', i);
		}
	}

```

- When performing error checking before continuing in a function, avoid unnecessary logic prior to the error check.

```javascript
	// bad - unnecessary call to getName()
	function() {

		var name = getName();

		if (!arguments.length) {
			return false;
		}

		this.setFirstName(name);

		return true;
	}

	// good
	function() {

		var name;

		if (!arguments.length) {
			return false;
		}

		name = getName();
		this.setFirstName(name);

		return true;
	}
```

- Use one `var` declaration per variable. It's easier to add new variable declarations this way, and you never have
	to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. **The only exception to this rule is in the case of counters**.

```javascript
	// bad
	var items = getItems(),
		goSportsTeam = true,
		dragonball = 'z';

	// bad
	// (compare to above, and try to spot the mistake)
	var items = getItems(),
		goSportsTeam = true;
		dragonball = 'z';

	// good
	var i, j, k;
	var items = getItems();
	var goSportsTeam = true;
	var dragonball = 'z';
```

**[⬆ back to top](#table-of-contents)**

<a name="hoisting"></a>
## Hoisting

- Variable declarations get hoisted to the top of their scope, but their assignment does not.

```javascript
	// we know this wouldn't work (assuming there
	// is no notDefined global variable)
	function example() {

		console.log(notDefined); // => throws a ReferenceError
	}

	// creating a variable declaration after you
	// reference the variable will work due to
	// variable hoisting. Note: the assignment
	// value of `true` is not hoisted.
	function example() {

		console.log(declaredButNotAssigned); // => undefined
		var declaredButNotAssigned = true;
	}

	// The interpreter is hoisting the variable
	// declaration to the top of the scope,
	// which means our example could be rewritten as:
	function example() {

		var declaredButNotAssigned;
		console.log(declaredButNotAssigned); // => undefined
		declaredButNotAssigned = true;
	}
```

- Anonymous function expressions hoist their variable name, but not the function assignment.

```javascript
	function example() {

		console.log(anonymous); // => undefined

		anonymous(); // => TypeError anonymous is not a function

		var anonymous = function() {

			console.log('anonymous function expression');
		};
	}
```

- Named function expressions hoist the variable name, not the function name or the function body.

```javascript
	function example() {

		console.log(named); // => undefined

		named(); // => TypeError named is not a function

		superPower(); // => ReferenceError superPower is not defined

		var named = function superPower() {

			console.log('Flying');
		};
	}

	// the same is true when the function name
	// is the same as the variable name.
	function example() {

		console.log(named); // => undefined

		named(); // => TypeError named is not a function

		var named = function() {

			console.log('named');
		}
	}
```

- Function declarations hoist their name and the function body.

```javascript
	function example() {

		superPower(); // => Flying

		function superPower() {

			console.log('Flying');
		}
	}
```

- For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#table-of-contents)**


<a name="comparison-operators--equality"></a>
## Comparison Operators & Equality

- Use `===` and `!==` over `==` and `!=`. The only exception to this is when checking for null or undefined.
```javascript
	var sponge = 'bob';

	// bad
	if (sponge == 'bob') {
		...
	}

	// good
	if (sponge === 'bob') {
		...
	}

	sponge = undefined;

	// good (checks for null or undefined)
	if (sponge == null) {
		...
	}
```

- Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

	+ **Objects** evaluate to **true**
	+ **Undefined** evaluates to **false**
	+ **Null** evaluates to **false**
	+ **Booleans** evaluate to **the value of the boolean**
	+ **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
	+ **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

```javascript
	if ([0]) {
		// true
		// An array is an object, objects evaluate to true
	}
```

- Use shortcuts.

```javascript
	// bad
	if (name !== '') {
		// ...stuff...
	}

	// good
	if (name) {
		// ...stuff...
	}

	// bad
	if (collection.length > 0) {
		// ...stuff...
	}

	// good
	if (collection.length) {
		// ...stuff...
	}
```

- For more information see [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

**[⬆ back to top](#table-of-contents)**

<a name="blocks"></a>
## Blocks

- Use braces with all blocks.

```javascript
	// bad
	if (test)
		return false;

	// bad
	if (test) return false;

	// good
	if (test) {
		return false;
	}

	// bad
	function() { return false; }

	// good
	function() {

		return false;
	}
```

- If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your
	`if` block's closing brace.

```javascript
	// bad
	if (test) {
		thing1();
		thing2();
	}
	else {
		thing3();
	}

	// good
	if (test) {
		thing1();
		thing2();
	} else {
		thing3();
	}
```

- Always put a single space after conditionals
```javascript
	// bad
	if(test) {
	...
	}

	// good
	if (test) {

	}
```


**[⬆ back to top](#table-of-contents)**

<a name="comments"></a>
## Comments

- Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.
	Make use of this convention when writing plugins or larger modules, but this is not required for smaller functions in microsites.
	Use discretion on when this is needed.

```javascript
	// good
	/**
	 * make() returns a new element
	 * based on the passed in tag name
	 *
	 * @param {String} tag
	 * @return {Element} element
	 */
	function make(tag) {

		// ...stuff...

		return element;
	}
```

- Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

```javascript
	// bad
	var active = true;  // is current tab

	// good
	// is current tab
	var active = true;

	// bad
	function getType() {

		console.log('fetching type...');
		// set the default type to 'no type'
		var type = this._type || 'no type';

		return type;
	}

	// good
	function getType() {

		console.log('fetching type...');

		// set the default type to 'no type'
		var type = this._type || 'no type';

		return type;
	}
```

- Use `// TODO:` to annotate solutions to problems or to point out something that needs fixing. These are different than regular comments because they are actionable.

```javascript
	function Calculator() {

		// TODO: total should be configurable by an options param
		this.total = 0;

		return this;
	}
```

**[⬆ back to top](#table-of-contents)**

<a name="whitespace"></a>
## Whitespace

- Use hard tabs.

```javascript
	// bad
	function() {

	∙∙∙∙var name;
	}

	// good
	function() {

	→	var name;
	}
```

- Place 1 space before the leading brace.

```javascript
	// bad
	function test(){

		console.log('test');
	}

	// good
	function test() {

		console.log('test');
	}

	// bad
	dog.set('attr',{
		age: '1 year',
		breed: 'Bernese Mountain Dog'
	});

	// good
	dog.set('attr', {
		age: '1 year',
		breed: 'Bernese Mountain Dog'
	});
```

- Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space before the argument list in function calls and declarations.

```javascript
	// bad
	if(isJedi) {
		fight ();
	}

	// good
	if (isJedi) {
		fight();
	}

	// bad
	function fight () {

		console.log ('Swooosh!');
	}

	// good
	function fight() {

		console.log('Swooosh!');
	}
```

- Leave space on either side of all operators.

```javascript
	// bad
	var x=y+5;

	// good
	var x = y + 5;
```

- End files with a single newline character.

```javascript
	// bad
	(function(global) {

		// ...stuff...
	})(this);
```

```javascript
	// bad
	(function(global) {

		// ...stuff...
	})(this);↵
	↵
```

```javascript
	// good
	(function(global) {

		// ...stuff...
	})(this);↵
```

- Avoid trailing whitespace with editor settings

```javascript
	// In Sublime Text User Settings
	{
		"trim_trailing_white_space_on_save": true
	}

	// Visual Studio Code User Settings
	{
		"files.trimTrailingWhitespace": true
	}
```

- Use indentation when making long method chains. Use a leading dot, which
	emphasizes that the line is a method call, not a new statement. Up to 3
	items may be chained before switching to the indented method.

```javascript
	// bad
	$('#items').find('.selected').highlight().end().find('.open').updateCount();

	// bad
	$('#items').
		find('.selected').
			highlight().
			end().
		find('.open').
			updateCount();

	// good
	$('#items')
		.find('.selected')
			.highlight()
			.end()
		.find('.open')
			.updateCount();

	// bad
	var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
			.attr('width', (radius + margin) * 2).append('svg:g')
			.attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
			.call(tron.led);

	// good
	var leds = stage.selectAll('.led')
			.data(data)
		.enter().append('svg:svg')
			.classed('led', true)
			.attr('width', (radius + margin) * 2)
		.append('svg:g')
			.attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
			.call(tron.led);
```

- Leave a blank line after blocks that are not properties of an object and before the next statement

```javascript
	// bad
	if (foo) {
		return bar;
	}
	return baz;

	// good
	if (foo) {
		return bar;
	}

	return baz;

	// bad
	var obj = {
		foo: function() {
		},
		bar: function() {
		}
	};
	return obj;

	// good
	var obj = {
		foo: function() {
		},
		bar: function() {
		}
	};

	return obj;
```


**[⬆ back to top](#table-of-contents)**

<a name="commas"></a>
## Commas

- Leading commas: **Nope.**

```javascript
	// bad
	var story = [
			once
		, upon
		, aTime
	];

	// good
	var story = [
		once,
		upon,
		aTime
	];

	// bad
	var hero = {
			firstName: 'Bob'
		, lastName: 'Parr'
		, heroName: 'Mr. Incredible'
		, superPower: 'strength'
	};

	// good
	var hero = {
		firstName: 'Bob',
		lastName: 'Parr',
		heroName: 'Mr. Incredible',
		superPower: 'strength'
	};
```

- Additional trailing comma: **Nope.** This can cause problems with IE6/7 and IE9 if it's in quirksmode. Also, in some implementations of ES3 would add length to an array if it had an additional trailing comma. This was clarified in ES5 ([source](http://es5.github.io/#D)):

> Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array. This is not a semantic change from Edition 3 but some implementations may have previously misinterpreted this.

```javascript
	// bad
	var hero = {
		firstName: 'Kevin',
		lastName: 'Flynn',
	};

	var heroes = [
		'Batman',
		'Superman',
	];

	// good
	var hero = {
		firstName: 'Kevin',
		lastName: 'Flynn'
	};

	var heroes = [
		'Batman',
		'Superman'
	];
```

**[⬆ back to top](#table-of-contents)**

<a name="semicolons"></a>
## Semicolons

- **Yup.**

```javascript
	// bad
	(function() {

		var name = 'Skywalker'
		return name
	})()

	// good
	(function() {

		var name = 'Skywalker';
		return name;
	})();

	// good (guards against the function becoming an argument when two files with IIFEs are concatenated)
	;(function() {

		var name = 'Skywalker';
		return name;
	})();
```

	[Read more](http://stackoverflow.com/a/7365214/1712802).

**[⬆ back to top](#table-of-contents)**

<a name="type-casting--coercion"></a>
## Type Casting & Coercion

- Perform type coercion at the end of the statement or use `toString`.
- Strings:

```javascript
	//  => this.reviewScore = 9;

	// bad
	var totalScore = '' + this.reviewScore;

	// good
	var totalScore = this.reviewScore + '';

	// good
	var totalScore = this.reviewScore.toString();

	// good
	var totalScore = this.reviewScore + ' total score';
```

- Use `parseInt` for Numbers and always with a radix for type casting.

```javascript
	var inputValue = '4';

	// bad
	var val = new Number(inputValue);

	// bad
	var val = +inputValue;

	// bad
	var val = inputValue >> 0;

	// good
	var val = parseInt(inputValue);

	// good
	var val = Number(inputValue);

	// gooder
	var val = parseInt(inputValue, 10);
```

**[⬆ back to top](#table-of-contents)**

<a name="naming-conventions"></a>
## Naming Conventions

- Avoid single letter names. Be descriptive with your naming. An exception is for i as an iterator (and j, k, for nested loops).

```javascript
	// bad
	function q() {

		// ...stuff...
	}

	// good
	function query() {

		// ..stuff..
	}

	// i & j are okay
	function query() {

			var someArr1 = [
					[1,2,3],
					[4,5,6],
					[7,8,9,10]
			],
					i,
					j;

			for (i = 0; i < someArr1.length; i++) {
					for (j = 0; j < someArr1[i].length; j++) {
							console.log(someArr1[i][j]);
					}
			}
	}
```

- Use camelCase when naming objects, functions, and instances.

```javascript
	// bad
	var OBJEcttsssss = {};
	var this_is_my_object = {};
	var o = {};
	function c() {}

	// good
	var thisIsMyObject = {};
	function thisIsMyFunction() {}
```

- Use PascalCase when naming constructors or classes.

```javascript
	// bad
	function user(options) {

		this.name = options.name;
	}

	var bad = new user({
		name: 'nope'
	});

	// good
	function User(options) {

		this.name = options.name;
	}

	var good = new User({
		name: 'yup'
	});
```

- Use a leading underscore `_` when naming private properties.

```javascript
	// bad
	this.__firstName__ = 'Panda';
	this.firstName_ = 'Panda';

	// good
	this._firstName = 'Panda';
```

<a name="controlling-scope"></a>
## Controlling Scope

- Controlling scope can be a confusing topic in JavaScript. Here are a few techniques to be sure `this` is what you expect it to be:

- **Capture `this` in a variable in an outer closure and use that variable in place of `this`**. When saving a reference to `this` use a meaningful name.
	If the context does is not conducive to a meaningful name, use `instance`.

```javascript
	// bad
	function() {

		var self = this;
		return function() {

			console.log(self);
		};
	}

	// bad
	function() {

		var that = this;
		return function() {

			console.log(that);
		};
	}

	// good - using instance
	function() {

		var instance = this;
		return function() {

			console.log(instance);
		};
	}

	// gooder - using a meaningful name (`sponge` in this case)
	var spongebob = new SeaSponge('Spongebob');
	spongebob.logger() {

		var sponge = this;
		return function() {

			console.log(sponge);
		}
	}
```

- **If you have browser support (>IE9), `bind` is a nice tool**. A great description of `bind` is [here](http://stackoverflow.com/a/10115970/1647608). "Bind creates a new function that will have `this` set to the first parameter passed to `bind()`." One great use is click handlers:

```javascript
	var Button = function(content) {

		this.content = content;
	};
	Button.prototype.click = function() {

		console.log(this.content + ' clicked');
	}

	var myButton = new Button('OK');
	myButton.click();

	// not bound, 'this' is not myButton
	var looseClick = myButton.click;
	looseClick();

	// bound, 'this' is myButton
	var boundClick = myButton.click.bind(myButton);
	boundClick();
```

- **If using jQuery, another option is the `$.proxy`**. Similar to `bind`, `$.proxy` takes a function and returns a new one that will always have a particular context. Example taken from [jquery site](https://api.jquery.com/jQuery.proxy/).

```javascript
	var you = {
		type: "person",
		test: function( event ) {

			$( "#log" ).append( this.type + " " );
		}
	};

	// Execute you.test() in the context of the `you` object
	// no matter where it is called
	// i.e. the `this` keyword will refer to `you`
	var youClick = $.proxy( you.test, you );

	// attach click handlers to #test
	$( "#test" )
		// this === "zombie"; handler unbound after first click
		.on( "click", $.proxy( me.test, me ) )

		// this === "person"
		.on( "click", youClick )

		// this === "zombie"
		.on( "click", $.proxy( you.test, me ) )

		// this === "<button> element"
		.on( "click", you.test );
```

- **The JavaScript functions `call` and `apply` are other options**. The `call` method calls a function with a given this value and arguments provides individually. The `apply` method calls a function with a given this value and arguments provided as an array. A useful way to remember which is which... apply uses an array, both start with 'a'. Call/apply call the function immediately, whereas `bind` returns a function that will have the specified context when executed later.  Details on MDN for [call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) and [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply).

```javascript
	// One use is chaining constructors
	function Animal(name, weight) {

		this._name = name;
		return this;
	}

	// call
	function SeaSponge(name) {

		Animal.call(this, name);
		this._species = 'seasponge';
	}

	// apply
	function SeaSponge(name) {

		Animal.apply(this, [name]);
		this._species = 'seasponge';
	}

	// Another use is to invoke an anonymous function
	var animals = [
		{ species: 'Sea Sponge', name: 'Spongebob Squarepants' },
		{ species: 'Squirrel', name: 'Sandy Cheeks' }
	];

	// call
	for (var i = 0; i < animals.length; i++) {
		(function(i) {

			console.log('#' + i + ' ' + this.species + ': ' + this.name);
		}).call(animals[i], i);
	}

	// apply
	for (var i = 0; i < animals.length; i++) {
		(function(i) {

			console.log('#' + i + ' ' + this.species + ': ' + this.name);
		}).apply(animals[i], [i]);
	}
```

<a name="accessors"></a>
## Accessors

- Accessor functions for properties are not required.
- If you do make accessor functions use getVal() and setVal('hello').

```javascript
	// bad
	dragon.age();

	// good
	dragon.getAge();

	// bad
	dragon.age(25);

	// good
	dragon.setAge(25);
```

- If the property is a boolean, use isVal() or hasVal().

```javascript
	// bad
	if (!dragon.age()) {
		return false;
	}

	// good
	if (!dragon.hasAge()) {
		return false;
	}
```

**[⬆ back to top](#table-of-contents)**

<a name="constructors"></a>
## Constructors

- Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

```javascript
	function Jedi() {

		console.log('new jedi');
	}

	// bad
	Jedi.prototype = {
		fight: function() {

			console.log('fighting');
		},

		block: function() {

			console.log('blocking');
		}
	};

	// good
	Jedi.prototype.fight = function() {

		console.log('fighting');
	};

	Jedi.prototype.block = function() {

		console.log('blocking');
	};
```

- Methods can return `this` to help with method chaining.

```javascript
	// bad
	Jedi.prototype.jump = function() {

		this.jumping = true;
		return true;
	};

	Jedi.prototype.setHeight = function(height) {

		this.height = height;
	};

	var luke = new Jedi();
	luke.jump(); // => true
	luke.setHeight(20); // => undefined

	// good
	Jedi.prototype.jump = function() {

		this.jumping = true;
		return this;
	};

	Jedi.prototype.setHeight = function(height) {

		this.height = height;
		return this;
	};

	var luke = new Jedi();

	luke.jump()
		.setHeight(20);
```


- It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

```javascript
	function Jedi(options) {

		options || (options = {});
		this.name = options.name || 'no name';
	}

	Jedi.prototype.getName = function() {

		return this.name;
	};

	Jedi.prototype.toString = function() {

		return 'Jedi - ' + this.getName();
	};
```

**[⬆ back to top](#table-of-contents)**

<a name="events"></a>
## Events

- When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. Name the hash `data`. For example, instead of:

```js
	// bad
	$(this).trigger('listingUpdated', listing.id);

	...

	$(this).on('listingUpdated', function(e, listingId) {

		// do something with listingId
	});
```

	prefer:

```js
	// good
	$(this).trigger('listingUpdated', { listingId : listing.id });

	...

	$(this).on('listingUpdated', function(e, data) {

		// do something with data.listingId
	});
```

**[⬆ back to top](#table-of-contents)**

<a name="jquery"></a>
## jQuery

<a name="jquery-variables"></a>
### jQuery Variables

- Prefix jQuery object variables with a `$`.

```javascript
	// bad
	var sidebar = $('.sidebar');

	// good
	var $sidebar = $('.sidebar');
```

- Cache jQuery lookups.

```javascript
	// bad
	function setSidebar() {

		$('.sidebar').hide();

		// ...stuff...

		$('.sidebar').css({
			'background-color': 'pink'
		});
	}

	// good
	function setSidebar() {

		var $sidebar = $('.sidebar');
		$sidebar.hide();

		// ...stuff...

		$sidebar.css({
			'background-color': 'pink'
		});
	}
```

<a name="jquery-events"></a>
### jQuery Events

- DO NOT use anonymous functions to attach events. [They're difficult to debug, maintain, test, or reuse](https://learn.jquery.com/code-organization/beware-anonymous-functions/). Use a function declaration instead. Take advantage of the fact that function declarations get hoisted to allow for events to be grouped higher up in the function, and handlers to be grouped below. This allows for quickly scanning through the events without weeding through their implementation.

```javascript
	// bad
	$(document).ready(function() {

		$('#myLink1').on('click', function() {...});
		$('#myLink2').on('click', function() {...});
		$('#myLink3').on('click', function() {...});
	});

	// good
	$(document).ready(init);

	function init() {

		//Events
		$('#myLink1').on('click', myLink1ClickHandler);
		$('#myLink2').on('click', myLink2ClickHandler);
		$('#myLink3').on('click', myLink3ClickHandler);
	}

	//Handlers (these are hoisted to the top of the scope)
	function myLink1ClickHandler() {...}
	function myLink2ClickHandler() {...}
	function myLink3ClickHandler() {...}
```

- Don't mix JavaScript inline events with jQuery events. Favor jQuery events.

```javascript
	// bad
	<a id="myLink" href="#" onclick="myEventHandler();">my link</a>

	// good
	$("#myLink").on("click", myEventHandler);
```

- When unbinding events, use custom namespaces to avoid inadvertently detaching all events from an object.

```javascript
	$("#myLink").on("click.mySpecialClick", myEventHandler);

	// Later on, it's easier to unbind just your click event
	$("#myLink").unbind("click.mySpecialClick");
```
- Use event delegation when attaching the same event to multiple elements. As stated [here](https://learn.jquery.com/events/event-delegation/), "Event delegation allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future."

```javascript
	// bad, you are attaching an event to all the links under the list.
	$("#list a").on("click", myClickHandler);

	// good, only one event handler is attached to the parent.
	$("#list").on("click", "a", myClickHandler);
```

<a name="microsites"></a>
##Code Organization for micro sites

- Put document ready inside a script tag at the bottom of the page. The app object is in a `app.js` code file that was included above the document ready script tag.
- Put code for all plugins and polyfills into a plugins.js file. Paste in the minified version of the source with a comment that clearly states what plugin and
	version it is.

```javascript
	// On the page
	<script src="js/jquery.js"></script>
	<script src="js/plugins.js"></script>
	<script src="js/app.js"></script>
	<script>
			$(document).ready(app.init);
	</script>

	// Then in the app.js, we use the revealing module pattern or an object literal.
	// This way, there is no logic in the document ready and no temptation to put everything
	// in one big document ready function.
	var app = (function() {

		var privateVar = 'I am private';
		var alsoPrivate = 'I am also private';

		function someFunc() {

				...
		}

		function init() {

				// initialize the app here
		}

		return {
				init: init,
				someFunc: someFunc
		};

	}())
	```
**[⬆ back to top](#table-of-contents)**

<a name="tools"></a>
##Tools

###ESLint
- Use ESLint to lint your code and ensure that you are using the prescribed style and syntax choices laid out in this guide.
	- Follow instructions on [ESLint site](http://eslint.org/docs/user-guide/getting-started) to install.
- ESLint has a Sublime plugin as well. Details [here](https://github.com/roadhump/SublimeLinter-eslint).
- ESLint makes use of a config file that can be placed at the root of your project. Once installed, use the [.eslintrc file](.eslintrc) in the javascript folder of this guide as the config file.
	- NOTE: A config file in the project directory is required in order to lint according to our rules. There is no global config for eslint.
- ESLint rules are [here](http://eslint.org/docs/rules/).

####Note
If you ever find yourself needing to have eslint ignore a specific line (for a really good reason!),
[this post](https://stackoverflow.com/questions/27732209/turning-off-eslint-rule-for-a-specific-line) can help.
#####To ignore a specific rule on a single line (in this case, the "indent" rule):

```javascript
		function someLineWithErrors() { // eslint-disable-line indent
		...
	}
```

#####To disable eslint for a block of code

```javascript
	/*eslint-disable */
	function someLinesWithErrors() {
			var doubleIndent;
		var singleIndent;
	}
	/*eslint-enable */
```

Just don't go disabling eslint for all your stuff. That would be _**#losing**_.

###JSBeautify
- A nice tool to format code using a given set of rules. It's a great starting point when updating legacy code to match the conventions laid out in the style guide. Site is here http://jsbeautifier.org/
- Sublime plugin is [here](https://github.com/enginespot/js-beautify-sublime).
	- After installation, the following config should be used under `Preferences -> Package Settings -> JavaScript Beautify -> Settings - User`

```json
	{
		"indent_size": 4,
		"indent_char": "	",
		"indent_level": 0,
		"indent_with_tabs": true,
		"preserve_newlines": true,
		"max_preserve_newlines": 10,
		"jslint_happy": false,
		"brace_style": "collapse",
		"keep_array_indentation": false,
		"keep_function_indentation": false,
		"space_before_conditional": true,
		"break_chained_methods": false,
		"eval_code": false,
		"unescape_strings": false,
		"wrap_line_length": 0,

		// jsbeautify options
		"format_on_save": false,
		"use_original_indentation": false
	}
```
# };
