# This

## This and Lexical Scope

To be clear, **this** does not, in any way, refer to a function's lexical scope. It is true that internally, scope is kind of like an object with properties for each of available identifiers. But scope "object" is not accessible to Javascript code. It's inner part of the engine's implementation.

Lexical scope is a compile-time binding, while **this** is a runtime binding. 

When function is invoked, an activation record, otherwise known as an **execution context**. This record contains information about where function was called from, how the function was invoked, what parameters were passed. One of the properties of the record is the **this** reference, which will be used for the duration of that function's execution.

## This is not

This is neither a reference to function itself, nor is it a reference to function's lexcial scope.