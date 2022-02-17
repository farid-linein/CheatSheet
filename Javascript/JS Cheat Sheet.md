# JS Cheat Sheet

## Script inside HTML

**On Page Script**

```javascript
<script type="text/javascript"> 
...
</script>
```

**Include external JS file**

```javascript
<script src="filename.js"></script>Import and Export
```

## 

## Export & Import

**Exprot**

```javascript
//file name functions.js
export const sayHello = (name, surname) => {
  console.log('Hello, ' + name + ' ' + surname + '!');
};
```

**Import**

```javascript
//filename solution.js
import { sayHello } from './functions.js'
sayHello('Jack', 'Jackson'); // Hello, Jack Jackson!
```

```javas
## Object

> curly braces to create an object { }
> 
> square brackets to create an array [ ]

**empty object**

```javascript
const user = {};

user.name = 'Jack';
user.age = 25;
```

## 

## Alternative Function Format

> - Parentheses, in which we can specify the parameters of the function `(name, surname)`.
> 
> - Arrow `=>` to separate the parameters of the function and the list of commands (body) of the function.
> 
> - Curly braces `{}`, inside of which we will place the body of the function.
> 
> - The keyword `return`, followed by the return value.

**Function 1**

```javascript
const sayHello = (name, surname) => {
  console.log('Hello, ' + name + ' ' + surname + '!');
};
```

**Function 2**

```javascripts
const add = (x, y) => {
  return x + y;
}
```

## 

## Object

**Object**

```javascript
const user = {
  name: 'Jack',
  age: 25
}
```

**complex object**

```javascript
''

const user = {
  name: 'Jack',
  age: 25,
  address: {
    country: 'US',
    state: 'NY',
    postcode: '10005',
    street: '11 Wall St '
  }
}
 user.address.state = 'LA';
```

## Array

**Array 1**

```javascript
const animals = ['Cow', 'Horse', 'Dog', 'Cat'];
console.log(animals[0], animals[3]); // Cow Cat
```

**Mixing Array & Object**

>  To add a new element into the array, you can use the `push` function. It is built into any JS array and adds an element to the end of it.

```javascript
const animals = [{
  type: 'Dog',
  name: 'Rex',
}, {
  type: 'Horse',
}];


console.log (animals.length);
animals.push ({type: 'Cat', name: 'Murka'});
console.log (animals.length);
```

**Array 2**

```java
//filename helper.js
const firstRow = [ 1, 2, 3 ];
const secondRow = [ 4, 5, 6 ];
const thirdRow = [ 7, 8, 9 ];

export const twoDime = [firstRow,secondRow];

//filename solution.js
import { twoDime } from './helper.js';

console.log(twoDime);
```

**Array 3**

```javascript
//filename helper.js
export const objects = [
    {angka:1},
    {nomer:2},
    {banyak:3}
];

//filename solution.js

import { objects } from './helper.js';

console.log(objects);
console.log(objects.length); // 3
```

## Conditional Statement

**If structure 1**

```javascript
if (/* condition */) {
  // do something useful if the condition is true
}
```

**If Struture 2**

```javascript
if (isRaining) {   // condition
  useUmbrella();   // execute if the condition is true
} else {
  hideUmbrella();  // execute if condition is false
}
```

>  In order to combine several conditions, the operators `&&` (logical "AND") and `||` (logical "OR") are useful.
> 
> ```javascript
> true && true;   // true
> true && false;  // false
> false && true;  // false
> false && false; // false
> 
> true || true;   // true
> true || false;  // true
> false || true;  // true
> false || false; // false
> ```

**If Structure 3**

```javascript
if (isRaining || isHeavySunshine) {  // if it rains OR the sun is hot
  useUmbrella ();                    // get the umbrella
} else {
  hideUmbrella ();                   // hide the umbrella
}
```
