#JavaScript Best Practice Guide

## 1. Use the literal syntax for object creation. eslint: no-new-object

```js     
// bad
const item = new Object();

// good
const item = {};
```

## 2. Use array spreads ... to copy arrays.
      
```js
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

## 3. Use object destructuring when accessing and using multiple properties of an object. eslint: prefer-destructuring
      
   Why? Destructuring saves you from creating temporary references for those properties.
      
```js
// bad
function getFullName(user) {
const firstName = user.firstName;
const lastName = user.lastName;

return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
const { firstName, lastName } = user;
return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
return `${firstName} ${lastName}`;
}
```

## 4. Do not unnecessarily escape characters in strings. eslint: no-useless-escape
      
   Why? Backslashes harm readability, thus they should only be present when necessary.
      
```js
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

## 5. Never use arguments, opt to use rest syntax ... instead. eslint: prefer-rest-params
      
   Why? ... is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like arguments.
      
```js
// bad
function concatenateAll() {
const args = Array.prototype.slice.call(arguments);
return args.join('');
}

// good
function concatenateAll(...args) {
return args.join('');
}
```

## 6. Never use the Function constructor to create a new function. eslint: no-new-func
      
   Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.
      
```js
// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');
```

## 7. When you must use an anonymous function (as when passing an inline callback), use arrow function notation. eslint: prefer-arrow-callback, arrow-spacing
      
   Why? It creates a version of the function that executes in the context of this, which is usually what you want, and is a more concise syntax.
      
   Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.
      
```js
// bad
[1, 2, 3].map(function (x) {
const y = x + 1;
return x * y;
});

// good
[1, 2, 3].map((x) => {
const y = x + 1;
return x * y;
});
```

## 8. Avoid confusing arrow function syntax (=>) with comparison operators (<=, >=). eslint: no-confusing-arrow
      
```js
// bad
const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

// good
const itemHeight = (item) => {
const { height, largeSize, smallSize } = item;
return height <= 256 ? largeSize : smallSize;
};
```

## 9. Always use class. Avoid manipulating prototype directly.
      
   Why? class syntax is more concise and easier to reason about.
      
```js
// bad
function Queue(contents = []) {
this.queue = [...contents];
}
Queue.prototype.pop = function () {
const value = this.queue[0];
this.queue.splice(0, 1);
return value;
};

// good
class Queue {
constructor(contents = []) {
  this.queue = [...contents];
}
pop() {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
}
}
```

## 10. Methods can return this to help with method chaining.
       
```js
// bad
Jedi.prototype.jump = function () {
 this.jumping = true;
 return true;
};

Jedi.prototype.setHeight = function (height) {
 this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
 jump() {
   this.jumping = true;
   return this;
 }

 setHeight(height) {
   this.height = height;
   return this;
 }
}

const luke = new Jedi();

luke.jump()
 .setHeight(20);
```
