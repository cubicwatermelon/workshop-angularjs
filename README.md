# ES6

## Block scoping

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

#### Básico

```javascript
  angular.module('MyBasicApp', [])
```

#### Composto

```javascript
  angular.module('MyApp.Controllers', [])
```

```javascript
  angular.module('MyApp.Services', [])
```

```javascript
  angular.module('MyComposedApp', ['MyApp.Controllers', 'MyApp.Services'])
```

### Controllers e Views

#### Dependency Injection

```javascript
someModule.controller('MyController', ['$scope', 'greeter', function($scope, greeter) {
  // ...
}]);

// --------------------------------------------------------------------------------------

var MyController = function($scope, greeter) {
  // ...
}

MyController.$inject = ['$scope', 'greeter'];

someModule.controller('MyController', MyController);
```

### Directives

#### Nativas

##### ng-if

```html
<p ng-if="user.active">{{ user.name }}</p>
```

##### ng-show

```html
<p ng-show="user.active">{{ user.name }}</p>
```

##### ng-hide

```html
<p ng-hide="!user.active">{{ user.name }}</p>
```

##### ng-repeat

```html
<p ng-repeat="user in users">{{ user.name }}</p>
```

##### ng-model

```html
<input type="text" ng-model="user.name" />
```

##### Eventos

```html
<input type="text" ng-click="showAlert()" />
```

```html
<input type="text" ng-change="showAlert()" />
```

```html
<form ng-submit="saveUser()">
  <button type="submit">Send</button>
</form>
```

#### Customizadas

```javascript
someModule.directive('myCustomer', function() {
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
someModule.controller('NaomiController', ['$scope', function($scope) {
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

```html
<div ng-controller="NaomiController">
  <my-customer></my-customer>
</div>

<div ng-controller="IgorController">
  <my-customer></my-customer>
</div>
```

Gera 

```html
<div>
  <p>Naomi</p>
</div>

<div>
  <p>Igor</p>
</div>
```

##### Isolated Scope

```javascript
someModule.directive('myCustomer', function() {
    return {
      restrict: 'E',
      scope: {
        // = : two-way databinding
        // @ : plain-text databinding
        // & : callback function databinding
        customerInfo: '=info'
      },
      template: '<p>{{ customerInfo.name }}</p>'
    };
  });
```

```html
<my-customer customer-info="{name: 'John'}"></my-customer>
```

Gera 


```html
<p>John</p>
```

### Filters

```html
{{ expression | filter }}

{{ expression | filter1 | filter2 | ... }}

{{ expression | filter:argument1:argument2:... }}

{{ 1234 | number:2 }} // 12.34
```

#### Nativos

- currency
- date
- filter
- json
- limitTo
- lowercase
- number
- orderBy
- uppercase

#### Customizado

```javascript
someModule.filter('decorate', function(decoration) {

    function decorateFilter(input) {
      return `*${input}*`;
    }

    decorateFilter.$stateful = true;

    return decorateFilter;
  })
```

```html
{{ 'esse ai dibra muito!' | decorate }}
```

Gera

```html
*esse ai dibra muito!*
```

### Services

```javascript
myModule.factory('serviceId', function() {
  let shinyNewServiceInstance;
  
  // ...

  return shinyNewServiceInstance;
});
```

### Components

```javascript
angular.module('heroApp').component('heroDetail', {
  template: '<p>{{ $ctrl.hero.name }}</p>',
  bindings: {
    // < : one-way databinding
    // = : two-way databinding
    // @ : plain-text databinding
    hero: '='
  }
});
```

```html
<hero-detail hero="{name: 'Batman'}"><hero-detail>
```

Gera

```html
<p>Batman</p>
```

### Routes

#### ng-router: só aceita templates e controllers
```html
<body ng-app="myApp">

  <p><a href="#/!">Main</a></p>

  <a href="#!red">Red</a>
  <a href="#!green">Green</a>
  <a href="#!blue">Blue</a>

  <div ng-view></div>

  <script>
    var app = angular.module("myApp", ["ngRoute"]);
    app.config(function($routeProvider) {
      $routeProvider
        .when("/", {
          template : "<h3>main<h3>"
        })
        .when("/red", {
          template: '<h3 style="color: red;">red</h3>'
        })
        .when("/green", {
          template: '<h3 style="color: green;">green</h3>'
        })
        .when("/blue", {
          template: '<h3 style="color: blue;">blue</h3>'
        });
    });
  </script>
</body>
```

#### ui-router: aceita componetes, controllers, templates e estados sem url

```html
<body ng-app="myApp">

  <p><a ui-sref="">Main</a></p>

  <a ui-sref="red">Red</a>
  <a ui-sref="green">Green</a>
  <a ui-sref="blue">Blue</a>

  <div ui-view></div>

  <script>
    var app = angular.module("myApp", ["ui.router"]);
    app.config(function($routeProvider) {
      const red = {
        name: 'main',
        url: '/',
        template: '<h3>main</h3>'
      };

      const red = {
        name: 'red',
        url: '/red',
        template: '<h3 style="color: red;">red</h3>'
      };

      const green = {
        name: 'green',
        url: '/green',
        template: '<h3 style="color: green;">green</h3>'
      };

      const blue = {
        name: 'green',
        url: '/blue',
        template: '<h3 style="color: blue;">blue</h3>'
      };

      $stateProvider.state(red);
      $stateProvider.state(green);
      $stateProvider.state(blue);
    });
  </script>
</body>
```

# Templates Javascript: 
```javascript
(function() {
    'use strict';

    angular
        .module('module')
        .controller('Controller', Controller);

    Controller.$inject = ['dependencies'];

    /* @ngInject */
    function Controller(dependencies) {
        var vm = this;
        vm.title = 'Controller';

        activate();

        ////////////////

        function activate() {
        }
    }
})();

====================================

(function() {
    'use strict';

    angular
        .module('module')
        .filter('filter', filter);

    function filter() {
        return filterFilter;

        ////////////////

        function filterFilter(params) {
            return params;
        }
    }

})();

======================================

(function() {
    'use strict';

    angular
        .module('module')
        .directive('directive', directive);

    directive.$inject = ['dependencies'];

    /* @ngInject */
    function directive(dependencies) {
        // Usage:
        //
        // Creates:
        //
        var directive = {
            bindToController: true,
            controller: Controller,
            controllerAs: 'vm',
            link: link,
            restrict: 'A',
            scope: {
            }
        };
        return directive;

        function link(scope, element, attrs) {
        }
    }

    /* @ngInject */
    function Controller() {

    }
})();

=================================

(function() {
    'use strict';

    angular
        .module('module')
        .factory('factory', factory);

    factory.$inject = ['dependencies'];

    /* @ngInject */
    function factory(dependencies) {
        var service = {
            func: func
        };
        return service;

        ////////////////

        function func() {
        }
    }
})();
===============================

(function() {
    'use strict';

    angular
        .module('module')
        .component('component', {
            bindings: {

            },
            controller: Controller

        });

    Controller.$inject = ['dependencies'];

    /* @ngInject */
    function Controller(dependencies) {

    }
})();

====================================

(function() {
    'use strict';

    angular
        .module('AppTesteServices')
        .config(RouterApp);

    RouterApp.$inject = ['$routeProvider'];

    function RouterApp($routeProvider) {

		}

})();
```
# Template HTML: 
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title></title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
</head>
<body>
  <div class="container">
  </div>
  <script src="../../../node_modules/angular/angular.min.js"></script>
</body>
</html>
```
