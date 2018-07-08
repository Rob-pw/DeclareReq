# DeclareReq
Annotate JS functions with required properties, retrieved from this.

Example:
module.js
`javascript
  import { $required } from 'declarereq';
  import { $dependency1, $dependency2 } = './constants'; 
  
  myFunction[$required] = [$dependency1, $dependency2];
  export myFunction(param1) {
    const { $dependency1, $dependency2 } = this;
    
    console.log($dependency1, $dependency2);
  }
`
use.js
`javascript
  import { $dependency1, $dependency2 } = './constants'; 
  import { myFunction } from './module';
  
  const context = { 
    $dependency1: "ichi", 
    $dependency2: "ni"
  };
    
  const _myFunction = prepare.call(context, myFunction);
  _myFunction('param1');
`
