# JavaScript Hoisting

### Hoisting is JavaScript's default behavior of moving declarations to the top.

In JavaScript, Hoisting is the default behavior of moving all the declarations at the top of the scope before code execution.Basically, it gives us an advantage that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.
It allows us to call functions before even writing them in our code. 
JavaScript allocates memory for all variables and functions defined in the program before execution.


> Note: JavaScript only hoists declarations, not the initializations.


**Let us understand what exactly this is:**
The following is the sequence in which variable declaration and initialization occur. 

### **Declaration –> Initialisation/Assignment –> Usage** 

```
// Variable lifecycle
let a;        // Declaration
a = 100;      // Assignment
console.log(a);  // Usage
```

However, since JavaScript allows us to both declare and initialize our variables simultaneously, this is the most used pattern:  

```
let a = 100;
```

> **Note**: Always remember that in the background the Javascript is first declaring the variable and then initializing them. It is also good to know that variable declarations are processed before any code is executed. 

However, in javascript, undeclared variables do not exist until code assigning them is executed. Therefore, assigning a value to an undeclared variable implicitly creates it as a global variable when the assignment is executed. This means that all undeclared variables are global variables.

```
// hoisting
function codeHoist(){
    a = 10;
    let b = 50;
}
codeHoist();
 
console.log(a); // 10
console.log(b); // ReferenceError : b is not defined
```

```
Output: 10
```

> **Explanation**: In the above code sample we created a function called codeHoist() and in there we have a variable which we didn’t declare using let/var/const and a let variable b. The undeclared variable is assigned the global scope by javascript hence we are able to print it outside the function, but in case of the variable b the scope is confined and it is not available outside and we get a ReferenceError.

> **Note**: There’s a difference between ReferenceError and undefined error. An undefined error occurs when we have a variable that is either not defined or explicitly defined as type undefined. ReferenceError is thrown when trying to access a previously undeclared variable.

### **ES5**
When we talk about ES5, the variable that comes into our minds is var. Hoisting with var is somewhat different as when compared to let/const. Let’s make use of var and see how hoisting works:  

```
// var code (global)
console.log(name); // undefined
var name = 'Mukul Latiyan';
```

```
Output: undefined
```

> **Explanation**: In the above code we tried to console the variable name which was declared and assigned later than using it, the compiler gives us undefined which we didn’t expect as we should have got ReferenceError as we were trying to use name variable even before declaring it. 
But the interpreter sees this differently, the above code is seen like this:  

```
//how interpreter sees the above code
var name;
console.log(name); // undefined
name = 'Mukul Latiyan';
```

```
Output: undefined
```

Function scoped variable
Let’s look at how function scoped variables are hoisted.  
```
//function scoped
function fun(){
    console.log(name);
    var name = 'Mukul Latiyan';
}
fun(); // undefined
```

```
Output: undefined
```

There is no difference here as when compared to the code where we declared the variable globally, we get undefined as the code seen by the interpreter is: 

```
//function scoped
function fun(){
    var name;
    console.log(name);
    name = 'Mukul Latiyan';
}
fun(); // undefined
```

```
Output: undefined
```

In order to avoid this pitfall, we can make sure to **declare and assign the variable at the same time, before using it**. 
Something like this:  

```
//in order to avoid it
function fun(){
    var name = 'Mukul Latiyan';
    console.log(name); // Mukul Latiyan
}
fun();
```

```
Output: Mukul Latiyan
```

## ES6
### The let and const Keywords
Variables defined with let and const are hoisted to the top of the block, but not initialized.

Meaning: The block of code is aware of the variable, but it cannot be used until it has been declared.

Using a let variable before it is declared will result in a ReferenceError.

The variable is in a "temporal dead zone" from the start of the block until it is declared:


**Let** :
We know that variables declared with let keywords are block scoped not function scoped and hence it is not any kind of problem when it comes to hoisting. 

Example:
```
//let example(global)
console.log(name);
let name='Mukul Latiyan'; // ReferencError: name is not defined
```  

```
Output
ReferenceError : can't access lexical declaration 'name' before initialization
```

Like before, for the var keyword, we expect the output of the log to be undefined. However, since the es6 let doesn’t take kindly on us using undeclared variables, the interpreter explicitly spits out a Reference error. This ensures that we always declare our variable first. 

**const** behaves similar to let when it comes to hoisting.


## JavaScript Initializations are Not Hoisted
JavaScript only hoists declarations, not initializations.

#### Example 1 does not give the same result as Example 2:


Example 1
```
var x = 5; // Initialize x
var y = 7; // Initialize y
console.log(x); // x
console.log(y); // y
```

Example 2
```
var x = 5; // Initialize x
console.log(x); // x
console.log(y); // undefined
var y = 7; // Initialize y
```

Does it make sense that y is undefined in the last example?
This is because only the declaration (var y), not the initialization (=7) is hoisted to the top.
Because of hoisting, y has been declared before it is used, but because initializations are not hoisted, the value of y is undefined.

## Variable hoisting
Variable hoisting means the JavaScript engine moves the variable declarations to the top of the script. For example, the following example declares the counter variable and initialize its value to 1:

```
console.log(counter); // undefined
var counter = 1;
```

In this example, we reference the counter variable before the declaration.
However, the first line of code doesn’t cause an error. The reason is that the JavaScript engine moves the variable declaration to the top of the script.
Technically, the code looks like the following in the execution phase:

```
var counter;
console.log(counter); // undefined
counter = 1;

```

During the creation phase of the global execution context, the JavaScript engine places the variable ```counter``` in the memory and initializes its value to ```undefined```.

### The let keyword
The following declares the variable counter with the let keyword:
```
console.log(counter);
let counter = 1;
```

The JavaScript issues the following error:
```
"ReferenceError: Cannot access 'counter' before initialization
```
The error message explains that the counter variable is already in the heap memory. However, it hasn’t been initialized.
Behind the scenes, the JavaScript engine hoists the variable declarations that use the let keyword. However, it doesn’t initialize the let variables.
Notice that if you access a variable that doesn’t exist, the JavaScript will throw a different error:

```
console.log(alien);
let counter = 1;
```

Here is the error:
``` "ReferenceError: alien is not defined ```

## Function hoisting
Like variables, the JavaScript engine also hoists the function declarations. This means that the JavaScript engine also moves the function declarations to the top of the script.

For example:
```
let x = 20,
  y = 10;

let result = add(x, y);
console.log(result);

function add(a, b) {
  return a + b;
}
```

In this example, we called the add() function before defining it. The above code is equivalent to the following:
```
function add(a, b){
    return a + b;
}

let x = 20,
    y = 10;

let result = add(x,y);
console.log(result);
```
During the creation phase of the execution context, the JavaScript engine places the add() function declaration in the heap memory. To be precise, the JavaScript engine creates an object of the Function type and a function reference called add that refers to the function object.

### Function expressions
The following example changes the add from a regular function to a function expression:
```
let x = 20,
    y = 10;

let result = add(x,y);
console.log(result);

var add = function(x, y) {
return x + y;
}
```
If you execute the code, the following error will occur:
``` 
TypeError: add is not a function
```
During the creation phase of the global execution context, the JavaScript engine creates the add variable in the memory and initializes its value to undefined.

When executing the following code, the add is undefined, hence, it isn’t a function:
``` let result = add(x,y); ```
The add variable is assigned to an anonymous function only during the execution phase of the global execution context.

### Arrow functions
The following example changes the add function expression to the arrow function:
```
let x = 20,
    y = 10;

let result = add(x,y);
console.log(result);

var add = (x, y) => x + y;
```
The code also issues the same error as the function expression example because arrow functions are syntactic sugar for defining function expressions.
``` 
TypeError: add is not a function 
```
Similar to the functions expressions, the arrow functions aren’t hoisted.


## Summary
- JavaScript hoisting occurs during the creation phase of the execution context that moves the variable and function declarations to the top of the script.
- The JavaScript engine hoists the variables declared using the let keyword, but it doesn’t initialize them as the variables declared with the var keyword.
- The JavaScript engine doesn’t hoist the function expressions and arrow functions.


### References
- [w3cSchools](https://www.w3schools.com/js/js_hoisting.asp)
- [javascript tutorial](https://www.javascripttutorial.net/javascript-hoisting/)
- [geeksforgeeks](https://www.geeksforgeeks.org/javascript-hoisting/)
