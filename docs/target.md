# Target API
The Target API is a set of native APIs written in C that encapsulate javascript features to work with statically typed programming.

## Example
Take the following example JavaScript.
```js
function main() {
    let plusOne = plusOneFunc(12)

    console.log(plusOne())
    return 0;
}

function plusOneFunc(count) {
    return () => {
        return count++;
    }
}
```

Using the Target API, the following code can also be written in C using all the tools the API provides, like dynamic variables, lambda's, contexts, etc.

```cpp
var* plusOneFunc__lmbd_01(ctx* context) {
    return var_arithm_add(ctx_get(context,0),var_int(1));
}

var* plusOneFunc(var* count) {
    ctx* context = decl_context(count);
    return lambda(&plusOneFunc__lmbd_01, context);
}

int main() {

    var* plusOne = plusOneFunc(var_int(12));

    console_log( lambda_exec(plusOne) );

    return 0;
}
```

## Table of contents
1. [Variables](#variables)
    1. [var](#11-var)
    2. [declvar](#12-declvarvoid-val-short-t)

## 1. Variables
### 1.1 var
The [var](#11-var) struct represents a JavaScript variable. It can be changed both in value and type. The struct itself contains a pointer to an address in memory and a identifier for the type. Use [declvar]() to declare a variable, [modvar]() to modify a variable and [frvar]() to free it from memory.

### 1.2 declvar(void* val, short t) 
The [declvar](#12-declvarvoid-val-short-t) method creates a 