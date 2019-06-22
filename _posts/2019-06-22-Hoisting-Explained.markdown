---
layout: post
title:  "Hosting in JavaScript"
date:   2019-06-22 15:23:36 +0100
description: In this blog we will explore what hoisting is in JavaScript
---

Have you ever noticed in JavaScript that sometimes you might use a variable before it's been used? Let's look at an example:

```javascript
var x = 'Hello';
y = 'World';

console.log(x + " " + y);

var y;
```

This will give the same result as the following example:

```javascript
var x = 'Hello';
var y = 'World';

console.log(x + " " + y);
```

This is because in JavaScript the parser will look through the script or function and 'hoist' the var declarations to the top. 

```javascript
// Example a                  | Example B
var x = 'Hello';              | var x = 'Hello';
y = 'World';                  | var y;
                              | y = 'World';
console.log(x + " " + y);     | console.log(x + " " y);
                              |
var y;                        |
```

Although this seems quite simple, it can sometimes create bugs that you might find difficult to sort out. Consider the following:

```javascript
var car = 'ford';

(function (){
 console.log(car); //outputs 'ford'
 console.log(car); //outputs 'ford'
})()
```

This makes sense, right? We initialised car with 'ford' and then logged the output within a function. What happens if we then re-initialise car?

```javascript
var car = 'ford';

(function (){
 console.log(car); //outputs 'undefined'
 var car = 'skoda';
 console.log(car); //outputs 'skoda'
})()
```

The first 'car' is now undefined. This is because JavaScript has hoisted the declaration of the variable to the top but not the initialisation of the variable. 

_Note: When using let or const, you will receive a ```ReferenceError``` rather than have an undefined variable. Although let or const are both hoisted, they do not get initialised. With var we see that it has the value of undefined, meaning that it is intialised as ```undefined``` when it is hoisted._

[Some people][hackernoon] argue that you should stop using var completely,but if you want reduce the likelihood of introducing a bug via hoisting, some people suggest that you declare variables just above where they are going to be used. This does not mean that you should declare all your variables within a function at the top of the function however. Take a look at the following example:

```javascript
function hoist() {
    var a;
    var b;

    // couple of lines which use a and b

    var c;
    var d;

    // couple of lines that use c and d
}
```


[hackernoon]:[https://hackernoon.com/why-you-shouldnt-use-var-anymore-f109a58b9b70]