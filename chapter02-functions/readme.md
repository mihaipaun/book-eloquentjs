## Notes on Chapter 2: Functions

### Definition order

The computer looks up all function definitions, and stores the assocciated functions, _before_ it starts executing the rest of the program. Thus, we do not have to think about the order in which we define and use our functions - they are all allowed to call each other, regardless of which one is defined first:

    print("The future says: ", future());
    function future() {
      return "We STILL have no flying cars.";
    }

### Nested scope

Functions defined inside other functions can refer to the local variables in their parent functions, functions defined inside those inner functions can refer to variables in both their parent and their grandparent functions, and so on.

All variables that were defined "above" a function's definition are visible, which means both those in function bodies that enclose it and those at the top level of the program. This approach to variable visibility is called __lexical scoping__:

    function multiplyAbsolute(number ,factor) {
      function multiply(number) {
        return number * factor;
      }
      if(number < 0)
        return multiply(-number);
      else
        return multiply(number);
    }
    /* When the body of the function *multiply* runs, it uses the same _factor_ variable as the outer function but has its own _number_ variable. */

### Function values

The _first-class_ nature of functions is the term used for "functions are values" concept.

### Closure

    function createFunction() {    
      var local = 100;  
      return function() { return local; };
    }

When _createFunction_ is called, it creates a local variable and then returns a function that returns that local variable. This is also known as "upwards Funarg problem".
Doing createFunction()() (creating the function and then calling it) results in the value 100 being returned, as hoped.
This feature is called **closure**, and a function that "closes over" some local variables is called _a closure_.

The following function makes it possible to dynamically create function values that add a certain number to their argument:

    function makeAdder(amount) {
      return function(number) {
        return number + amount;
      };
    }
    var addTwo = makeAdder(2);
    addTwo(3) -> 5

### Optional arguments

JavaScript is notoriously nonstrict about the amount of arguments you pass to a function. If you pass too many, the extra ones are ignored. If you pass too few, the missing ones get the value undefined.

### Recursion

In most JavaScript implementations, recursion is about 10 times slower than running through a simple loop. That being said, the basic rule, which has been repeated by many programmers, is **to not worry about efficiency until your program is provably too slow**. When it is, find out which parts are taking up the most time, and start exchanging elegance for efficiency in those parts.

How would you write a function that, given a number, tries to find a sequence of additions and multiplications that produce that number?
    function findSequence(goal) {
      function find(start, history) {
        if (start == goal)
          return history;
        else if (start > goal)
          return null;
        else
          return find(start + 5, "(" + history + " + 5)") || find(start * 3, "(" + history + " * 3)");
        /* equivalent (but more wordy) code would look like this:
        else {
          var found = find(start + 5, "(" + history + " + 5)");
          if (found == null)
            found = find(start * 3, "(" + history + " * 3)");
          return found;
        }
        */
      }
      return find(1, "1");
    }
    /* findSequence(24) -> (((1 * 3) + 5) * 3) */
The inner _find_ function, by calling itself in two different ways, explores both the possibility of adding 5 to the current number and of multiplying it by 3. When it finds the number, it returns the history string, which is used to record all the operators that were performed to get to this number. The use of the || operator in the example can be read as "return the solution found by adding 5 to start, and if that fails, return the solution found by multiplying start by 3".