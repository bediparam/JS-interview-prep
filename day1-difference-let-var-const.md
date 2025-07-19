# Day 1 - Difference between let, var and const

## Scoping

It is worth noting how the variables are scoped. When declaring variables, if its done with var, its in global/functional scope where as if the variables are declared with let/const, its always block scoped. Lets take an example -

```javascript
function varScope() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 - accessible due to function scope
}

function letScope() {
  if (true) {
    let y = 20;
  }
  console.log(y); // ReferenceError - y is block scoped
}

{
  const a = 10;
}
console.log(a); // ReferenceError - a is block scoped
```

## Shadowing

A variable declared in inner scope of a block with the same name as in outer scope shadows (overlaps) the outer one. lets take an example -

In case of let and const, shadowing happens...

```javascript
let a = 100;
{
  let a = 200;
  console.log(a); // 200 - inner 'a' shadows the outer one
}

console.log(a); // 100 - outer scope unchanged
```

but if you use var in block scope with a let in outer, it will give error as var is global scope which means there will be 2 declarations in global scope at the same time.

```javascript
let b = 10;
{
  var b = 20; // SyntaxError: Identifier 'b' has already been declared
}
```

## Redeclaration

var allows redeclaration where as let, const doesn't allow redeclaration in the same scope.

```javascript
var name = "Alice";
var name = "Bob"; // Allowed

let city = "Paris";
let city = "London"; // SyntaxError - cannot redeclare block-scope variable

const PI = 3.14;
const PI = 3.14159; // SyntaxError - cannot redeclare block-scope variable
```

##Declaration without initialization and Reassigning
var and let variables can be declared without initialization and reassigned where as const needs to be initialized at the time of declaration and cannot be reassigned.

```javascript
var a; // Correct
let b;  // Correct
const c; // SyntaxError: Missing initializer in const declaration
```

```javascript
var x = 10;
x = 15; // correct

let y = 20;
y = 25; // correct

const z = 30;
z = 35; // TypeError: Assignment to constant variable
```

## Hoisting

A JS program consists of 2 phases - creation phase and execution phase.

During Creation phase, JS engine creates global/window object and allocates heap memory for declaration of variables.

During this phase, all variables and functions are moved to top of the code and declared. variables are initialized \_undefined \_whereas whole function is declared. This is called hoisting.

Remember, var is hoisted but let, const are not (they are hoisted technically but in temporal deadzone which means they are in the scope but not declared yet).

```javascript
console.log(price); // undefined (hoisted)
var price = 100;
```

```javascript
console.log(message); // ReferenceError (not initialized)
let message = "Hello";
```

**Note:** The temporal dead zone is the time between entering scope and the variable's actual declaration where let and const exist, but accessing them throws an error.

**Final Notes:**

- Avoid using var in modern JS code unless absolutely necessary.
- Prefer let for variables that need reassignment.
- Use const by default for immutable references.
