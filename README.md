# DeclareReq
Annotate JS functions with required properties, retrieved from this. Super simple dependency injection.

Example:
module.js
```javascript
  import { $required } from 'declarereq';
  import { $dependency1, $dependency2 } = './constants'; 
  
  myFunction[$required] = [$dependency1, $dependency2];
  export function myFunction(param1) {
    const { $dependency1, $dependency2 } = this;
    
    console.log($dependency1, $dependency2);
  }
```

use.js
```javascript
  import { prepare } from 'declarereq';
  import { $dependency1, $dependency2 } = './constants'; 
  import { myFunction } from './module';
  
  const context = { 
    $dependency1: "ichi", 
    $dependency2: "ni"
  };
    
  const _myFunction = prepare.call(context, myFunction);
  _myFunction('param1');
```
