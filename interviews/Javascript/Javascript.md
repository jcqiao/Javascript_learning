## What's the apply, call, bind and differences

Apply, call, and bind are all methods that let you explicitly set the this keyword for a function. The main difference between apply and call is how they handle arguments.

Call takes arguments one by one.
Apply takes them as an array.
Both of these execute the function immediately. But in a callback it will lose this binding.

The bind method is different, it doesn’t call the function right away. Instead, it returns a new function with this already set. This is useful when you want to pass a function as a reference without losing its original this context. It can also handle partial application, or 'currying,' by pre-setting some arguments.

## What's the arrow function

Arrow functions are a shortway to write funtions in javascript, introduced in ES6. They use the arrow syntax and provide seveal benefits over traditional function expressions:
1. Concise syntax
2. Solve the problem of missing this in seveal scenario, such as as a callback function in setTimeout or in a object function.
3. No arguments object, use the rest operator to handle multiple arguments.
4. Not suitable as methods or constructors: Because they don't have their own this and they lack the prototype property.