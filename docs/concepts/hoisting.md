# JavaScript Hoisting

### Hoisting is JavaScript's default behavior of moving declarations to the top.

In JavaScript, Hoisting is the default behavior of moving all the declarations at the top of the scope before code execution.Basically, it gives us an advantage that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

It allows us to call functions before even writing them in our code. 


> Note: JavaScript only hoists declarations, not the initializations.


JavaScript allocates memory for all variables and functions defined in the program before execution.

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

