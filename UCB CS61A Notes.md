### Lecture 1 Welcome
- Types of expressions
	- An expression describes a computation and evaluates to a value
	- function call notation: generalization 
		- All expressions can use function call notation
		- *Python examples*
- Anatomy of a Call Expression
	- **Operator** and **operand** are also expressions
	- Evaluation procedure for call expressions
		- Evaluate the **operator** and then the **operand** subexpressions
		- Apply the function (which is the value of the operator subexpression) to the arguments (which are the values of the operand subexpression)
- Evaluating Nested Expressions
	- example `mul(add(2, mul(4, 6)), add(3, 5))`
### Lecture 2 Functions
- Names, Assignment, and User-Defined Functions *demo*
```Python
# Assignment for variables
from math import pi
radius = 10

# Notice: assignment don't keep variables synced! 
area, circ = pi * radius * radius, 2 * pi * radius


# Assignment for functions
calcMax = max
max = 7
# now the name 'max' refers to a integar variable whose value is 7
calcMax(1, 2, max) # result: 7
max = calcMax
# now the name 'max' refers to a function whose value is the 'built-in function max'
max(1, 2, 3) #result: 3

# User defined functions
def square(x):
	'''calculate the square of the given argument'''
	return mul(x, x)

def sumSquares(x, y):
	'''calculate the sum of the squares of the given arguments'''
	return square(x) + square(y)


def calcArea(radius):
	'''calculate the area of a circle whose radius is given as an argument'''
	return pi * radius * radius
	# the return expression re-evaluates every time the function is called

# Notice: function keep variables synced! 
calcArea(10)
calcArea(20)
```
- Types of Expressions
	- Primitive expressions
	- Call expressions
- Defining Functions
	- Assignment *simple means of abstraction*: binds names to **values**
	- Function definition *more powerful of abstraction*: binds name to **expressions**
	- Function composition
		- Function **signature** indicates arguments
		- Function **body** defines the computational process
	- Execution procedure for def statements
		- Create a function with signature
		- Set the body of the function
		- Bind name to the new function
- Calling User-Defined Functions
	- Procedure version 1
		- Add a local frame, forming a new environment
		- Bind the function's formal parameters to its arguments in that frame
		- Execute the body of the function in that new environment
- Looking Up Names In Environments
	- Every expression is evaluated in the context of an environment.
		- An environment is a sequence of frames
		- A name evaluates to the value bound to that name in the **earliest** frame of the current environment in which that name is found
```Python
def square(square):
	return mul(square, square)
```
- Environment Diagrams *visualize the interpreter's process*
- Assignment Statements
	- Evaluate all expressions to the right of `=` from left to right
	- Bind all names to the left of `=` to the resulting values in the current frame
- None
	- The special value `None` represents nothing in Python
	- A function that **does not explicitly return a value** will return `None`
- Pure Functions & Non-Pure Functions
	- Pure functions just return values
	- Non-pure functions have side effects
### Lecture 3 Control
- Life Cycle of a User-Defined Function
	- Def statement
	- Call expression
	- Calling/Applying
- Multiple Environments in One Diagram
- Names Have No Meaning Without Environments
- Miscellaneous Python Features
	- Operators *note that `//` means `floordiv`* 
	- Multiple Return Values 
	- Docstrings *documentation about functions*
	- Doctests *test points within documentation*
	- Default Arguments
- Conditional Statements
	- Statements *A statement is executed by the interpreter to perform an action*
	- Compound statements *consist of clauses and suites*
	- Conditional Statements and Boolean Contexts
- While Statements