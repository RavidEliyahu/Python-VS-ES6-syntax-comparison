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
 
# Python3.7 VS ES6 syntax comparison (For React)
################################################################################

References:
* A different version https://gist.github.com/revolunet/537a3448cff850231a74
* Javascript: https://developer.mozilla.org/en-US/docs/Web/JavaScript
* Python: https://docs.python.org/3/index.html

Bulit-in Types
########################################

123
========================================

length (JS) len(PY)
========================================

.. code:: python

     len([0, 1, 2])  # 3

.. code:: js

    [0, 1, 2].length  // 3
   
Array (JS) List (PY)
========================================

Add an item
----------------------------------------

.. code:: python

    # two ways
    In [60]: n = [1, 2, 3, 4]
    
    In [61]: n.append(5)
    
    In [62]: n
    Out[62]: [1, 2, 3, 4, 5]
    
    In [63]: n + [6]
    Out[63]: [1, 2, 3, 4, 5, 6]

.. code:: js

    > n = [1, 2, 3, 4]
    [ 1, 2, 3, 4 ]
    > n.push(5)
    5
    > n
    [ 1, 2, 3, 4, 5 ]

   
Dictionary
========================================

    In Javascript, you don't need to put quotation marks around keys.
    
.. code:: python

    In[56]: n = { 'color': 'red'};

    In [57]: n
    Out[57]: {'color': 'red'}
    
    # Or you can do it this way
    
    In [58]: m = dict(color='red')
    
    In [59]: m
    Out[59]: {'color': 'red'}

.. code:: js
    
    n = { 'color': 'red'};  // same as: n = { color: 'red'};
    Object { color: "red" }



Generators
========================================

.. code:: python

    def foo():
        return iter(range(1, 4))
    
    foo_gen = foo()
    print(next(foo_gen))
    print(next(foo_gen))
    print(next(foo_gen))
    print(next(foo_gen))
    # 1
    # 2
    # 3
    # StopIteration
    
    def foo():
        return iter(range(1, 4))
    
    foo_gen = foo()
    print(next(foo_gen))
    print(next(foo_gen))
    print(next(foo_gen))
    # print(next(foo_gen))

    for num in foo():
        print(num)
    # 1
    # 2
    # 3
    # If we continue to use foo_gen, we will get no output.

.. code:: js

    function* foo() {
        yield 1;
        yield 2;
        yield 3;
    }
    
    let foo_gen = foo();
    console.log(oo_gen.next());
    console.log(oo_gen.next());
    console.log(oo_gen.next());
    console.log(oo_gen.next());
    // { value: 1, done: false }
    // { value: 2, done: false }
    // { value: 3, done: false }
    // { value: undefined, done: true }
    
    for (let num of foo()) {
        console.log(num);
    }
    // 1
    // 2
    // 3
    // If we continue to use foo_gen, we will get no output.

next()
----------------------------------------

In Javascript, next() can do two-way communication. No such magic in Python.

Iterators
========================================

.. code:: python

    def fibonacci():
        pre, cur = 0, 1
        while True:
            pre, cur = cur, pre + cur
            yield cur

    for x in fibonacci():
        if (x > 1000):
            break
        print x,

.. code:: js

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

JSON
========================================

Python has built-in JSON support :
    
    import json
    json.loads(data) # import from JSON
    json.dumps(data) # export to JSON
    

Expressions & operators
########################################

Destructuring(JS) Unpacking(PY)
========================================

Flat
----------------------------------------

.. code:: python
    
    >>> a, *b, c = [0, 1, 2, 3, 4]
    >>> a
    0
    >>> c
    4
    >>> b
    [1, 2, 3]
    
    
    >>> [*[1, 2], *[3, 4]]
    [1, 2, 3, 4]
    
    >>> {**{'a': 1}, **{'b': 2}}
    {'a': 1, 'b': 2}

.. code:: js

    const arr = [2, 3, 4, 5];
    let [a, b, c, d] = arr;
    console.log(a, b, c, d);
    // 2 3 4 5
    
    let [a,,,, c] = [0, 1, 2, 3, 4]
    console.log(a, c)
    // 0 4
    // How to get in-between values like in Python??

Nested
----------------------------------------

.. code:: python

    a, b, [c1, c2] = [1, 2, [3, 4]]
    print(a, b, c1+c2)
    # 1 2 7

.. code:: js

    [a, b, [c1, c2]] = [1, 2, [3, 4]];
    console.log(a, b, c1+c2);
    // 1 2 7


Quick Value Swap
========================================

.. code:: python

    a = 1
    b = 2
    c = 3
    d = 4
    a, b, c, d = d, c, b, a
    print(a, b, c, d)
    # 4 3 2 1
    
    dog = {name:'lucky', age: 5, toys: ['bone', 'ball']}
    # no javascript style unpack, use to get or [] to access items
    dog.get('name')
    dog['name']


.. code:: js

    a = 1;
    b = 2;
    c = 3;
    d = 4;
    [a, b, c, d] = [d, c, b, a];
    console.log(a, b, c, d);
    // 4 3 2 1
    
    let dog = {name:'lucky', age: 5, toys: ['bone', 'ball']};
    let {name:dog_name, age: dog_age, toys: dog_toys} = dog;
    console.log(dog_name, dog_age, dog_toys);
    // lucky 5 [ 'bone', 'ball' ]
    let {name, age, toys} = dog
    console.log(dog_name, dog_age, dog_toys);
    // lucky 5 [ 'bone', 'ball' ]
    
    dog.name;  // lucky




Comprehensions
========================================

.. code:: python

    names = [c.name for c in customers if c.admin]  # List

    names = {c.id: c.name for c in customers}  # Dictionary

    names = {c.name for c in customers}  # Set

(Experimental in Babel)

.. code:: js

    var names = [for (c of customers) if (c.admin) c.name];

async and await
========================================

.. code:: python

    import asyncio, json, aiohttp
    
    async def fetch(session, url):
        async with session.get(url) as response:
            return await response.text()
    
    async def main(user, index):
        async with aiohttp.ClientSession() as session:
            response = await fetch(session, f"https://api.github.com/users/{user}")
            data = json.loads(response)
            repo_response = await fetch(session, data["repos_url"])
            repo_data = json.loads(repo_response)
            print(repo_data[25]["name"])
    
    if __name__ == "__main__":
        loop = asyncio.get_event_loop()
        loop.run_until_complete(main("jeremy886", 25))

.. code:: js

    require('isomorphic-fetch');
    async function get_repo(user, index) {
        let response = await fetch(`https://api.github.com/users/${user}`);
        let data = await response.json();
        let repo_response = await fetch(data.repos_url);
        let repo_data = await repo_response.json();
        console.log(repo_data[index].name);
    }
    
    get_repo('jeremy886', 25);
    // django-rest-framework

Statements and Declarations
########################################

Imports / Modules
========================================

.. code:: python

    import math
    print math.log(42)

    from math import log
    print log(42)

    # not a good practice (pollutes local scope) :
    from math import *
    print log(42)


Curly braces are used if you would like to import a non-default export.

.. code:: js

    import math from 'math';
    console.log(math.log(42));

    import { log } from 'math';
    console.log(log(42));

    import * from 'math';
    console.log(log(42));

    
Flow Control
========================================

for (each) loop
----------------------------------------


.. code:: python

    In [7]: names = ['John', 'Jame', 'Jim', 'Josh']
    
    In [8]: for name in names:
       ...:     print(name)
       ...:
    John
    Jame
    Jim
    Josh

.. code:: js

    > names = ['John', 'Jame', 'Jim', 'Josh']
    [ 'John', 'Jame', 'Jim', 'Josh' ]
    > for (let i=0; i<4; i++) { console.log(names[i]); }
    John
    Jame
    Jim
    Josh
    
    
index (JS) v enumerate (PY)
----------------------------------------

.. code:: python

    In [10]: for i, number in enumerate([1, 2, 3]):
        ...:     print(number*i)
        ...:
    0
    2
    6

.. code:: js

    > [1, 2, 3].forEach(function(number, i) {
    ... console.log(number * i);
    ... })
    0
    2
    6
    undefined
    


OOP
########################################

Classes (syntax sugar for prototype in JS)
==========================================

.. code:: python

        class Person:
            def __init__(self, name):
                self.name = name
        
            def say_name(self):
                print(f'My name is {self.name}.')
        
        p1 = Person('Jennifer')
        p1.say_name()
        # My name is Jennifer.

.. code:: js

    class Person {
        constructor(name) {
            this.name = name;
        }
        say_name() {  // no need to use "function" key word
            console.log(`My name is ${this.name}.`);
        }
    }
    let p1 = new Person('Jennifer');
    p1.say_name();
    // My name is Jennifer.
    console.log(p1.__proto__ === Person.prototype)
    // true
    console.log(p1.say_name === Person.prototype.say_name)
    // true

Inheritance
========================================
(Python has builtin support for multiple inheritance)

.. code:: python

    class Human:
        def __init__(self, age):
            self.age = age
    
    class Spider:
        pass
    
    class SpiderMan(Human, Spider):
        def __init__(self, age, powers):
            super().__init__(age)
            self.powers = powers
        def attack(self):
            print('launch web')
    
    p1 = SpiderMan(15, ['crawl', 'swing'])
    print(p1)
    # <__main__.SpiderMan object at 0x000001E78BA6D470>
    
.. code:: js

    class SuperHero {
        constructo(age) {
            this.age = age;
        }
    }
    class SpiderMan extends SuperHero {
        constructor(age, powers) {
            super(age);
            this.powers = powers;
        }
        attack() {
            console.log('launch web');
        }
    }
    p1 = new SpiderMan(15, ['crawl', 'swing']);
    console.log(p1);
    // SpiderMan { powers: [ 'crawl', 'swing' ] }


this (JS) self(PY)
========================================

Hard to compare


Functions
########################################

Range
========================================

.. code:: python

    print(range(5))
    # 0, 1, 2, 3, 4

.. code:: js

    console.log(Array.from(new Array(5), (x,i) => i));
    // 0, 1, 2, 3, 4


Lambdas
========================================

.. code:: python

    lambda a: a * 2

.. code:: js

    a => a * 2;  // for one expression function, omit () { return ... }
    const persons = (props) => {
        if (props.lenght >= 1) do_something();
    }; 
    // () is optional for single paramter.

In Javascript => also allows a function to use a lexical scope.

Overloading
========================================

Both don't have function overloading. Python has "singledispatch" to support it indirectly.

.. code:: python

    from functools import singledispatch
    @singledispatch
    def div(a, b=1):
        print(a, b)
    
    @div.register(int)
    def _(a: int, b=1):
        print(a/b)
    
    @div.register(str)
    def _(a: str, b=1):
        print(a[:len(a)//b])
    
    div(25 , 2)
    div('single dispatch practice', 2)
    

Default parameters (same)
========================================

.. code:: python

    def add(a, b=5):
        return a + b

.. code:: js

    function add(a, b=5) {
        return a+b;
    }

recursive
========================================

Functional Trio: Map, Filter, Reduce
========================================



Filter
----------------------------------------

.. code:: python

    numbers = [3, 4, 6, 8, 7];
    evens = filter(lambda x: x%2 == 0, numbers)
    print(list(evens))
    # [4, 6, 8]
    
.. code:: js

    let numbers = [3, 4, 6, 8, 7];
    let evens = numbers.filter(
        function(number) {return number % 2 === 0;})
    console.log(evens)
    // [4, 6, 8]

Map (Continued from Filter)
----------------------------------------

.. code:: python

    doubled = map(lambda x: x*2, evens)
    print(list(doubled))
    # [8, 12, 16]
    # OR use list comprehension


.. code:: js

    let doubled = evens.map(function(number){ return number * 2;})
    console.log(doubled)
    // [8, 12, 16]

Reduce (Continued from Map)
----------------------------------------
.. code:: python

    from functools import reduce
    reduced = reduce(lambda x, y: x+y, doubled)
    print(reduced)
    # 36
    
.. code:: js

    let reduced = doubled.reduce(function(num1, num2){return num1+num2;});
    console.log(reduced)
    // 36
    
Chaining
----------------------------------------

.. code:: python

    # needs external library

.. code:: js
    
    let result = [3, 4, 6, 8, 7]
        .filter(function(number) {return number % 2 === 0;})
        .map(function(number){ return number * 2;})
        .reduce(function(num1, num2){return num1+num2;});
    console.log(result);
    // 36


Spread(JS) Unpacking(PY)
========================================

.. code:: python

    def add(*args):
        print(sum(args))

    nums = [1, 2, 3]
    add(*nums, 4)
    # 10

.. code:: js
    
    function arg_info(...values) {
        console.log(values.reduce((a, b)=> a+b, 0));
    }
    nums = [1, 2, 3];
    arg_info(...nums, 4)
    // 10
    
    function arg_info() {
        console.log(arguments)
    }
    arg_info(1, 2, 3, 4)
    // { '0': 1, '1': 2, '2': 3, '3': 4 }

String Manipulation
########################################

Template String (JS) v F-string (PY)
========================================

.. code:: python

     name = 'James'
     print(f'My name is {name}.')  # use normal quotation marks

.. code:: js

    const name = 'James';
    console.log(`My name is ${name}.`);  // use back tick 
    


Errors (JS) Exceptions (PY)
########################################

evoke
========================================

.. code:: python

    raise Exception("error occurs")

.. code:: js

    throw new Error('Error occurs');
    
HTML
########################################

    
    
Type-Hinting
########################################
