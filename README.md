# Python VS ES6 syntax comparison

Python syntax here : 2.7 - [online REPL](https://repl.it/languages/Python)

Javascript ES6 via [Babel](http://babeljs.org) transpilation - [online REPL](https://babeljs.io/repl)

## Imports

```python
import math
print math.log(42)

from math import log
print log(42)

# not a good practice (pollutes local scope) :
from math import *
print log(42)
```

```js
import math from 'math';
console.log(math.log(42));

import { log } from 'math';
console.log(log(42));

import * from 'math';
console.log(log(42));
```

## Range

```python
print range(5)
# 0, 1, 2, 3, 4
```

```js
console.log(Array.from(new Array(5), (x,i) => i));
// 0, 1, 2, 3, 4
```

## Generators

```python
def foo():
    yield 1
    yield 2
    yield 3
```


```js
function *foo() {
    yield 1;
    yield 2;
    yield 3;
}
```

### Lambdas

```python
lambda a: a * 2
```

```js
a => a * 2
```

### Destructuring

```python
status, data = getResult()
```

```js
var [status, data] = getResult();
```

### Spread

```python
search_db(**parameters)
```

```js
searchDb(...parameters);
```

### Iterators

```python
def fibonacci():
    pre, cur = 0, 1
    while True:
        pre, cur = cur, pre + cur
        yield cur

for x in fibonacci():
    if (x > 1000):
        break
    print x,
```

```js
var fibonacci = {
  [Symbol.iterator]: function*() {
    var pre = 0, cur = 1;
    for (;;) {
      var temp = pre;
      pre = cur;
      cur += temp;
      yield cur;
    }
  }
}
for (var n of fibonacci) {
  if (n > 1000)
    break;
  console.log(n);
}
```

### Classes

(Python has builtin support for multiple inheritance)

```python
class SpiderMan(Human, SuperHero):
    def __init__(self, age):
        super(SpiderMan, self).__init__(age)
        self.age = age
    def attack(self):
        print 'launch web'
```

```js
class SpiderMan extends SuperHero {
    constructor(age) {
        super();
        this.age = age;
    }
    attack() {
        console.log('launch web')
    }
}
```



### Comprehensions

```python
names = [c.name for c in customers if c.admin]
```
(Experimental in Babel)

```js
var names = [for (c of customers) if (c.admin) c.name];
```

### Map

```python
map(lambda: x*2, [1,2,3,4])
```

```js
[1,2,3,4].map(x => x*2)
```

### length

```python
 len([])
```

```js
[].length
```

## What's better in Python

 - `help(anything)` : get docstring for any module/method/function
 - list comprehensions, class magic methods !
 - very powerful OOP
 - huge and coherent standard library, ex : string has 38 useful methods
 - built-in [strings and array slicing](http://stackoverflow.com/a/509295/174027).



## What's better in Javascript

 - Builtin JSON support
 - NPM packaging is a killer-feature : simple and fast, light-years ahead pip+virtualenv.
 - Works in the browser :)
