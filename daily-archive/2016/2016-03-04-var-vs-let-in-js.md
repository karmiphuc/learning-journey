---
layout: post
summary: "The difference between `var` and `let`"
tags: javascript
---
#### `let`-scoped variables in for loops

Source: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let

![Demo](https://pbs.twimg.com/media/CbiYLKOUMAAblbw.png)

> You can use the let keyword to bind variables locally in the scope of for loops. This is different from the var keyword in the head of a for loop, which makes the variables visible in the whole function containing the loop.

```js

var i=0;
for (let i=5; i < 10 ; i++ ) {
  console.log(i);
}
console.log(i);

// Prints: 5 6 7 8 9 0

for (var i=5; i < 10 ; i++ ) {
  console.log(i);
}
console.log(i);

// Prints: 5 6 7 8 9 10

```

> You can use the let keyword to bind variables locally in the scope of loops instead of using a global variable (defined using var) for that.

```js

for (var i = 0; i < 10; ++i) {
  setTimeout(_ => {
    console.log(i)
  }, 100 * i)
}

// Prints:
// 10
// 10
// ... (7 more times here)
// 10

for (let i = 0; i < 10; ++i) {
  setTimeout(_ => {
    console.log(i)
  }, 100 * i)
}

// Prints:
// 0
// 1
// ... 
// 9

```
