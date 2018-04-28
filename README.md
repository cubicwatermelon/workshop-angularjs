# ES6

## Block scoping (let e const)

```javascript
// let = pertence ao bloco, não ao escopo da função
function fn () {
  let x = 0
  if (true) {
    let x = 1 // only inside this `if`
  }
}
 
 
// const = não pode ser reatribuido
const a = 1
```

## Backtick strings

```javascript
const message = `Hello ${name}`;
```

## Destructuring

### Destructuring assignment

```javascript
// Arrays
const [first, last] = ['Nikola', 'Tesla']
 
// Objects
let {title, author} = {
  title: 'The Silkworm',
  author: 'R. Galbraith'
}
```

### Default values

```javascript
const scores = [22, 33];

const [math = 50, sci = 50, arts = 50] = scores;

// Result: math === 22, sci === 33, arts === 50
```

### Loops

```javascript
const songs = [
  {title: 'Everlong', artist: 'Foo Fighters'},
  {title: 'Immigrant song', artist: 'Led Zepellin'},
];

for (let {title, artist} of songs) {
  ···
}
```

### Reassigning keys

```javascript
function printCoordinates({ left: x, top: y }) {
  console.log(`x: ${x}, y: ${y}`)
}
```

### Function arguments

```javascript
function greet({ name, greeting }) {
  console.log(`${greeting}, ${name}!`)
}

greet({ name: 'Larry', greeting: 'Ahoy' })
```

### Default Function values

```javascript
function greet({ name = 'Rauno' } = {}) {
  console.log(`Hi ${name}!`);
}

greet() // Hi Rauno!
greet({ name: 'Larry' }) // Hi Larry!
```

## Spread

### Object spread

```javascript
const user = {name: 'John Smith'};

const options = {
  ...defaults,
  visible: true
}

// returns {name: 'John Smith', visible: true}
```

### Array spread

```javascript
const admins = ['John', 'Peter'];

const editors = ['Rita', 'Carlos'];

const users = [
  ...admins,
  ...editors,
  'rstacruz'
]

// returns ['John', 'Peter', 'Rita', 'Carlos', 'rstacruz']
```

## Functions

### Function arguments

```javascript
function greet (name = 'Jerry') {
  return `Hello ${name}`
}
 
/// est arguments
function fn(x, ...y) {
  // y is an Array
  return x * y.length
}
 
// Spread
fn(...[1, 2, 3])
// same as fn(1, 2, 3)
```

### Fat arrows

```javascript
setTimeout(() => {
  ···
})
 
// With arguments
readFile('text.txt', (err, data) => {
  ...
})
 
// Implicit return
numbers.map(n => n * 2)

// No curly braces = implicit return
// Same as: numbers.map(function (n) { return n * 2 })
```

## Objects

### Properties

```javascript
const name = 'myApp';

const App = {
  name
}

// Same as: App = { name: name }
```

### Methods

```javascript
const App = {
  start () {
    console.log('running')
  }
}

// Same as: App = { start: function () {···} }
```

### Computed property names

```javascript
let event = 'click'
let handlers = {
  [`on${event}`]: true
}
// Same as: handlers = { 'onclick': true }
```


## AngularJS

#### IIFE

```javascript
(function (angular) {
  'use strict';
  
  // ...
}(angular));
```

### Módulos

### Controllers e Views

### Directives

#### Nativas

##### ng-if

##### ng-show

##### ng-hide

##### ng-repeat

##### ng-model

##### Eventos

#### Customizadas

```javascript
angular.module('docsIsolateScopeDirective', [])
  .directive('myCustomer', function() {
    return {
      // 'A' - only matches attribute name
      // 'E' - only matches element name
      // 'C' - only matches class name
      // 'M' - only matches comment
      restrict: 'E',
      scope: {
        customerInfo: '=info'
      },
      template: '<p>{{ info.name }}</p>'
    };
  });
```

##### Shared Scope

```javascript
angular.module('docsScopeProblemExample', [])
  .controller('NaomiController', ['$scope', function($scope) {
    $scope.customer = {
      name: 'Naomi'
    };
  }])
  .controller('IgorController', ['$scope', function($scope) {
    $scope.customer = {
      name: 'Igor'
    };
  }])
  .directive('myCustomer', function() {
    return {
      restrict: 'E',
      template: '<p>{{ info.name }}</p>'
    };
  });
```

Gera 

```html
<div ng-controller="NaomiController">
  <p>Naomi</p>
</div>

<div ng-controller="NaomiController">
  <p>Igor</p>
</div>
```

##### One-way Scope

##### Isolated Scope

### Filters

### Services

#### Store

#### Http

### Components
