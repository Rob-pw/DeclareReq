# DeclareReq
Annotate JS functions with required properties, retrieved from this. Super simple dependency injection without compilation.

Example:
module.js
```javascript
  // the $ prefix indicates a symbol reference.
  import { $required } from 'declarereq';
  import { $dependency1, $dependency2 } = './constants'; 
  
  myFunction[$required] = [$dependency1, $dependency2]; //multiple named dependencies
  export function myFunction(param1) {
    const { $dependency1, $dependency2 } = this;
    
    console.log($dependency1, $dependency2);
  }
  
  myFunction1[$req] = $dependency1; //single dependency; $req is an alias for $required
  export function myFunction1() {
    console.log(this); //this is the value associated with $dependency1 in the context;
  }
```

use.js
```javascript
  import { prepare } from 'declarereq';
  import { $dependency1, $dependency2 } = './constants'; 
  import * as functions from './module';
  
  const context = { 
    [$dependency1]: "ichi", 
    [$dependency2]: "ni"
  };
  
  (() => {
    const myFunction = prepare.call(context, functions.myFunction);
    myFunction('param1');
  
    const myFunction1 = prepare.call(context, functions.myFunction1);
    myFunction1();
  }());
  
  (() => {
    const { myFunction, myFunction1 } = prepare.call(context, functions);
    myFunction('param1'); 
    myFunction1();
  }());
  
  const boundPrepare = prepare.bind(context);
  const { myFunction, myFunction1 } = boundPrepare(functions);
```
