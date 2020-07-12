---
layout: post
title:      "JavaScript Variables and Hoisting"
date:       2020-07-12 01:28:19 +0000
permalink:  javascript_variables_and_hoisting
---


Understanding variable declarations and their scope is essential to building quality code and debugging. That being said, let's discuss the differences between `const`, `let`, and `var`. Let's start with `const`.

`const` is a variable declaration that can't be re-declared or updated. `const` must be declared and initialized because of this. For example:

```
const pi = 3.1415;
console.log(pi); // 3.1415
```

But if you don't initialize the variable:

```
const pi; // Uncaught SyntaxError: Missing initializer in const declaration
```

Or try to change it after initializing:

```
const pi = 3.1415;
const pi = 3.14; // Uncaught TypeError: Assignment to constant variable.
```

`const` is also a block-scoped declaration. This means it can only be used within the block it's declared in. Any variables defined outside of the block are considered a completely separate variable:

```
const it = "pronoun"

if (true) {
    const it = "Deadly Clown"
		console.log(it); // "Deadly Clown"
}
console.log(it); // "pronoun"
```

This is useful because whenever you use `const`, it's a signifier that the variable isn't meant to be changed. If you don't need to change the variable, it's best to use `const`.

`let` is another variable declaration slightly different from `const`. `let` can't be re-declared, but it can be updated. This also allows it to be declared without being initialized:

```
let work; // undefined
work = "In the Office";
let coronavirus = true;
work = "From Home";
console.log(work); // "From Home"
```

You won't return any errors for trying to update the variable. You'll only get an error when you try to re-declare the variable:

```
let house = "Rented"
let house = "Owned" // Uncaught SyntaxError: Identifier 'house' has already been declared
```

`let` is also block-scoped like `const`. It's perfect to use when you know you need to change the variable. For instance loops would use `let`.

`var` is the original variable declaration. When `var` is used, the variable is either globally-scoped or function-scoped. This means unlike `const` and `let`, it's **NOT block-scoped**. It can be re-declared and updated:

```
var store = "full";
var coronavirus = true;

if (coronavirus) {
   var store = "empty"
}

console.log(store); // "empty"
```

`var` is normally not used in newer code now that `const` and `let` exist. Generally, you won't need to use `var`. This could potentially cause unintended bugs. There's also the scenario when the declaration is forgotten. If this happens the variable will always be globally scoped, even if it's in a function:

```
function topSecret () {
  secret = "Don't tell anybody!"
}

topSecret();
console.log(secret); // "Don't tell anybody!"
```

Now that we understand the variable declarations, let's talk about hoisting. To understand hoisting, let's talk about how JavaScript runs code. JavaScript executes in two parts: Compilation and Execution. During the compilation phase, variables and functions are declared and stored. During the execution phase, the functions are run.

```
//newFunction() will  be executed during the execution phase (Which happens after initialization)

newFunction(); // "Will this work?"

//newFunction() will be initialized during the compilation phase

function newFunction() {	
	return "Will this work?";
}
```

The reason you can write code to invoke a function before declaring the function is because of hoisting. The declaration of the variables happens during the compilation phase before the code is executed. It seems like the code is 'hoisting' some of the code when you look at how it's sequenced.

```
function anotherFunction() {
  console.log(number)
  var number = 5
}

anotherFunction(); // undefined
```

This will seem to execute like below:

```
function anotherFunction() {
  var number;
  console.log(number) // undefined
  number = 5;
}

anotherFunction(); // undefined
```

This is why it logs undefined instead of an error. Although, `const` and `let` are still technically hoisted, it won't work for those declarations. This is because `var` is initialized as undefined and `const` and `let` aren't initialized and can't be referenced.

```
function anotherFunction() {
  console.log(number)
  let number = 5
}

anotherFunction(); // Uncaught ReferenceError: Cannot access 'number' before initialization
```

As a standard, variables should always be declared at the top of the scope. This should prevent some of the issues with `var`. With the new capability of `let` and `const` though, `var` shouldn't be used. It can cause more problems than it can fix. With the new declarations, hoisting doesn't cause as much confusion and makes debugging easier. If there's code that still uses `var`, just make sure to pay some extra attention to detail.
