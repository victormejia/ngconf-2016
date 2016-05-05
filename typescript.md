# TypeScript and ES6 Workshop

[Slides](http://tinyurl.com/TS-ES6-In60)

## Key ES6 Features
   * Maps/Sets
   * Modules/Classes
   * Block Scope
   * Destructuring
   * Arrow Functions

[http://kangax.github.io/compat-table/es6](http://kangax.github.io/compat-table/es6)

TypeScript ---> compiler ---> JavaScript (ES5)

How do we control what gets compiled down?

`tsconfig.json`

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "sourceMap": true,ypesp
    "emitDecoratorMetadata": true, // decorators for ng2
    "experimentalDecorators"
    "noImplicitAny": true, // enforce types
  }
}
```

`"module"` options

```
commonjs
system
es6
```

## Types

Built-in types:

  * string
  * number
  * Array
  * any
  * Boolean

```
function add(x:number ,y:number) {
	return x + y;
}

add('2', 2);
```

## Classes

```
class Customer {
  name: string;
  isPrime: boolean;

  constructor(name: string, isPrime: boolean) {
    this.name = name;
    this.isPrime = isPrime;
  }

  placeOrder(productId: number, price: number) {
    return 'Order placed';
  }
}

var customer = new Customer('Victor', true);
```

this is what it generates
```
var Customer = (function () {
    function Customer(name, isPrime) {
        this.name = name;
        this.isPrime = isPrime;
    }
    Customer.prototype.placeOrder = function (productId, price) {
        return 'Order placed';
    };
    return Customer;
}());
var customer = new Customer('Victor', true);
```

## Interfaces

```javascript
interface CustomerInfo {
	name: string;
	isPrime: boolean;
}

class Customer {

  constructor(info: CustomerInfo) {
  }

  placeOrder(productId: number, price: number) {
    return 'Order placed';
  }
}

var customer = new Customer({
	name: 'Victor',
	isPrime: true
});
```

Automatically adding `public`, assigns it as property
```javascript
constructor(public info: CustomerInfo) {

}
```

```javascript
var Customer = (function () {
    function Customer(info) {
        this.info = info;
    }
    Customer.prototype.placeOrder = function (productId, price) {
        return 'Order placed';
    };
    return Customer;
}());
var customer = new Customer({
    name: 'Victor',
    isPrime: true
});
```


## Modules

  * Will appeal to CommonJS (Node) and AMD (require.js) developers
  * Compact syntax that relies on `import` and `export`

``` javascript
// customer.js
export var name = 'Victor';
export var city = 'Mejia';

// app.js
import {name, city} from 'customer';
console.log(name); // Victor

// app.js
import * as customer from 'customer';
console.log(customer.name);
console.log(customer.city);
```

## Modules and SystemJS

SystemJS can load modules:

You give it the starting point (`main.js`)

```html
<script src="/node_modules/systemjs/dist/system.src.js"></script>
<script>
  System.config({
      packages: {
        scripts: {
          format: 'register',
          defaultExtension: 'js'
        }
      }
    });
  System.import('scripts/main')
        .then(null, console.error.bind(console));
</script>
```

## Sets

```javascript
var set = new Set();
set.add('HR');
set.add('Finance');
set.add('Finance'); // duplicate ignored

set.has('Finance'); // true
set.delete('Finance');
set.size; // 2
```

## Maps

duplicates also ignored

```javascript
var map = new Map();
map.set('Finance', 'Process Bills');
map.set('HR', 'HR and Healthcare');
```

## Arrow Functions

```javascript
class Timer {
  foo() {

  }

  startTimer() {
    setInterval(function() {
      this.foo(); // this here isn't Timer, its the window
    }, 1000);
  }
}
```

change to

```javascript
class Timer {
  foo() {

  }

  startTimer() {
    setInterval(() => {
      this.foo(); // "this" is Timer object
    }, 1000);
  }
}
```
and this is what it generates

```javascript
var Timer = (function () {
    function Timer() {
    }
    Timer.prototype.foo = function () {
    };
    Timer.prototype.startTimer = function () {
        var _this = this;
        setInterval(function () {
            _this.foo(); // "this" is Timer object
        }, 1000);
    };
    return Timer;
}());
```

## Template Strings

No more string concatenation!

```javascript
  return `<h1>${title}</h1>`
```


## Destructuring
```
var {total, tax} = {total: 9.99, tax: 0.50};
```


## Default and Rest parameters
```javascript
  setDetails(make = 'None', model = 'None', year = this.currentYear()) {
    console.log(make + ' ' + model + ' ' + year);
  }
```

Allow a variable number of parameters to be passed to a function:

```
class Car {
  //accessories is a "rest parameter"
  setDetails(make = 'No Make', ...accessories) {
    console.log(make);

    if (accessories) {
      for (var i = 0; i < accessories.length; i++) {
        console.log('\n' + accessories[i]);
      }
    }
  }
}
```
