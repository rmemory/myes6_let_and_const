This repo contains some ES6 code examples to demonstrate improvements related to
variable creation, updating, and scoping.

/*** Block Scoping of let and const ***/
var variables are function scoped. Not block scoped. Blocks don't have any effect
on scope of var variables.

function myFunction() {
	var thisVarCanOnlyBeAccessedInThisFunction;
}

if (age > 12) {
	var dogYears = age * 7;
	console.log(`You are ${dogYears} dog years old`);
}

// dogYears is available here too
console.log(`You are ${dogYears} dog years old here too`);

/*** Usage of let, const, and var ***/
var variables can be redefined in code.

var somevar = 5;

...

var somevar = 6;

let and const will not allow redeclaration. 

You can do this because let is used in two different scopes.

let winner = false;

if (points > 40) {
	let winner = true;
}

const of an object means the object instance cannot be reassigned, but the variable 
values in the object can be reassigned ... unless you use Object.freeze();

/*** More examples ***/

Replacing the IIFE, which is used to protect function scoped var variables. Even a 
simple var name = "foobar" is a problem because the global scope (window) has a name
attribute which we would replace.

Here is an IIFE, which protects vars from leaking into the global scope.

( function() {
	var name = "Richard";
}) ();

Meanwhile, if I do this it means name is scoped to that block.

{
	const name = "Richard";

}

Here is a for loop example:

for (var i = 0; i < 10; i++) {
	console.log(i);
}

console.log(i) will echo 10, because i is in global scope.

for (var i = 0; i < 10; i++) {
	setTimeout(function() {
		console.log('The number is ' + i);
	}, 1000);
}

That code will also always print 10, even though the loop increments 0 through 9.
This is because by the time the console.log occurs, the loop has long since
exited, and i is in the global scope, and its value will be 10.

To fix that, use let ...

for (let i = 0; i < 10; i++) {
	setTimeout(function() {
		console.log('The number is ' + i);
	}, 1000);
}

/*** Temporal Dead Zone ***/
console.log(pizza); // undefined, but not an error
var pizza = "Deep Dish";

console.log(someOtherPizza); // results in error
const someOtherPizza = "My Pizza";

Rules: 

* Always declare everything as const, and only change to let when necessary. 
* Never use var, even for global scope vars. Var is dead to me.



