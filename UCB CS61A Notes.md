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
### Lecture 4 Higher-Order Functions
- Iteration Example
	- The Fibonacci Sequence
```Python
def fib(n):
	'''compute the n-th Fibonacci number, for n >= 1'''
	previousNum, currentNum = 1, 0
	k = 0
	while k < n:
		previousNum, currentNum = currentNum, previousNum + currentNum
		k = k + 1
	return currentNum
```
- If Statements and Call Expressions
	- If statements
		- Evaluate the header's expression
		- Execute the right clause and skip the remaining ones
	- Call expressions *can be implemented manually*
		- Evaluate **all subexpressions**, first the operator and then the operand
		- Apply the function which is the value of the call expression
```Python
def if_(condition, ifTrue, ifFalse):
	if condition:
		return ifTrue
	else:
		return ifFalse
```
- Control Expressions
	- Logical Operators  `and` `or`
- Higher-Order Functions
	- Generalizing Patterns with Arguments
	- Generalizing Over Computational Processes
	- Functions as Return Values
	- The Purpose of Higher-Order Functions *take functions as argument/return values*
		- Express general methods of computation
		- Remove repetition from programs
		- Separate concerns among functions
```Python
# Generalization with arguments
from math import pi

def area(leng, shapeCoef):
	'''calculate the area'''
	assert leng > 0, 'A length must be positive'
	return leng * leng * shapeCoef

def areaSquare(leng):
	'''calculate the area of a square'''
	return area(leng, 1)

def areaCircle(leng):
	'''calculate the area of a circle'''
	return area(leng, pi)

def aeaHexagon(leng):
	'''calculate the area of a hexagon'''
	return area(leng,3 * sqrt(3) / 2)
```

```Python
# Generalization over computational processes

def calSum(n, poly):
	'''sum the given polynomials'''
	k, total = 1, 0
	while k <= n:
		total, k = total + poly(k), k + 1
	return total

def calSumNaturals(n):
	'''sum naturals'''
	return calSum(n, lambda x : x)

def calSumCubes(n):
	'''sum cubes'''
	return calSum(n, lambda x : x ** 3)
```

```Python
# Functions as return values

def makeAdder(n):
	def adder(k):
		return k + n
	return adder

# call expressions as operator expressions

print(makeAdder(15)(15))
```
### Lecture 5 Environments
- Environments Enable Higher-Order Functions
	- Higher-order function: A function that takes functions as argument/return values
	- Names can be Bound to Functional Arguments
- Environments for Nested Definitions
	- Environment Diagrams for Nested Def Statements
	- How to Draw an Environment Diagram
- Local Names
	- Local Names are Invisible to Other (Non-Nested) Functions
- Function Composition
	- The Environment Diagram for Function Composition
- Lambda Expression
	- Comparison between Lambda Expressions and Def Statements
- Currying
	- Function Currying: Transforming a multi-argument function into a single-argument, higher-order function
```Python
# Environments for Nested Definitions
def makeAdder(n):
	def adder(k):
		return k + n
	return adder

addThree = makeAdder(3)
addFour = makeAdder(4)
```

```Python
# Local Names
def parentFunc(x, y):
	return g(x)
	# y is a local name in the parentFunc's frame

def (a):
	return a + y
	# y is a local name in the 

result = f(1, 2)
```

```Python
# Function Composition & Lambda Expression
def square(x):
	return x ** 2

def triple(x)
	return x * 3

def compose(f, g):
	return lambda x : f(g(x))

squiple = compose(square, triple)
tripare = compose(triple, square)
```

```Python
# Function Currying
def curry(f):
	def g(x):
		def h(y):
			return f(x, y)
		return h
	return g
```
### Lecture 7 Functional Abstraction
- Lambda Function Environments
	- Environment Diagrams with Lambda *A lambda function's parent is the current frame in which the lambda expression is evaluated*
```Python
# Lambda Function Environments
a = 1
def f(g):
	a = 2
	return lambda y : a * g(y) # a == 2
	f(lambda y : a + y)(a) # a == 1
```
- Return
	- Return Statements *A return statement completes the evaluation of a call expression and provides its value*
		- call expression
			- switch to the new environment which the called function belongs to
			- execute the function's body
		- return statement
			- switch back to the previous environment
			- the function now has a value
- Abstraction
	- Functional Abstractions: necessary interface properties
		- Arguments
		- Return values
	- Choosing Names
		- Names should convey the meaning or purpose of the values to which they are bound
		- The type of value bound to the name is best documented in a function's docstring
		- Function names typically convey their effect, their behavior, or the value returned
		- Which Values Deserve a Name
			- Repeated compound expressions
			- Meaningful parts of complex expressions
		- Extra Tips
			- Names can be long if they help document your code
			- Names can be short if necessary
- Errors & Tracebacks
	- Syntax error
	- Runtime error
	- Behavior error
### Lecture 8 Function Examples

```Python
# function delay
def delay(arg):
	print('delayed')
	def g():
		return arg
	return g

# Test01
delay(delay)()(6)()
# Evaluate
6
# Output
delayed
delayed
6

# Test02
print(delay(print)()(4))
# Evaluate
None
# Output
delayed
4
None
```

```Python
# function pirate
from operator import add, mul
def square(x):
	return mul(x, x)

def pirate(arggg):
	print('matey')
	def plunder(arggg):
		return arggg
	return plunder

# Test01
add(pirate(3)(square)(4), 1)
# Evaluate
17
# Output
matey
17

# Test02
pirate(pirate(pirate))(5)(7)
# Evaluate
# Output
matey
matey
error
```

```Python
# Draw environment diagram to understand this! 
def horse(mask):
	horse = mask
	def mask(horse):
		return horse
	return horse(mask)

mask = lambda horse : horse(2)

horse(mask)
```
- Implementing a Function
	- Read the description
	- Verify the examples & pick a simple one
	- Read the template
	- Implement without the template and fit your implementation to the template **OR** simply use the template
	- Annotate names with values from your chosen example
	- Write code to compute the result and check
	- Check other examples
```Python
def remove(n, digit):
	''' Return all digits of non-negative N that are not DIGIT, for some non-negative DIGIT less than 10
	>>> remove(231, 3)
	21
	>>> remove(243132, 2)
	4313
	'''
	kept, digits = 0, 0
	while n > 0:
		n, last = n // 10, n % 10
		if last != digit:
			kept = kept + last * (10 ** digits) 
			digits = digits + 1
		return kept
```
- Function Decorators
```Python
def trace(func):
	''' Return a version of func that first prints before it's called.
		func - a funciton of 1 argument
	'''
	def traced(x):
		print('Calling', func, 'on argument', x)
		return func(x)
	return traced

@trace
def square(x):
	return x * x

@trace
def sumSquaresUpTo(n):
	k, total = 1, 0
	while k <= n:
		k, total = k + 1, total + square(k)
	return total
```
### Lecture 9 Recursion
- Self-Reference
```Python
def printAll(x):
	print(x)
	return printAll

printAll(1)(3)(5)
```

```Python
def printSums(x):
	print(x)
	def nextSum(y):
		return printSums(x + y)
	return nextSum

printSums(1)(3)(5)
```
- Recursive Functions
	- **Definition**: A function is called recursive if the body of that function calls itself, either directly or indirectly
	- **Implication**: Executing the body of a recursive function may require applying that function again
	- **Instance**: Digit Sums
	- **Anatomy**
		- The **def statement header** is similar to other functions
		- Conditional statements check for **base cases**
		- Base cases are evaluated **without recursive calls**
		- Recursive cases are evaluated **with recursive calls**
```Python
# Digit Sums
def split(n):
	''' Split positive n into all but its last digit and its last digit '''
	return n // 10, n % 10

def sumDigits(n):
	''' Return the sum of the digits of positive integer n '''
	if n < 10:
		return n
	else:
		allButLast, last = split (n)
		return sumDigits(allButLast) + last
```
- Recursion in Environment Diagrams
	- The same function is called multiple times
	- Different frames keep track of the different arguments in each call
	- What arguments evaluate to depends upon which is the current environment
	- Each call to the function solves a simpler problem than the last
```Python
# The Factorial Function
def fact(n):
	if n == 0:
		return 1
	else:
		return fact(n - 1) * n
```
- Iteration vs Recursion
	- *Converting Recursion to Iteration*
		- **Can be tricky**: Iteration is a special case of recursion
		- **Idea**: Figure out what state must maintained by the iterative function
	- *Converting Iteration to Recursion*
		- **More formulaic**: Iteration is a special case of recursion
		- **Idea**: The state of an iteration can be passed as arguments
- Verifying Recursive Functions
	- Verify the base case
	- Treat the function as an abstraction
	- Assume that the function is correct for case `n - 1`
	- Verify that the function is correct for case `n` based on the assumption
- The Luhn Algorithm *Mutual Recursion*
```Python
# notice the flip flop between luhnSum() and luhnSumDouble()
def sumDigits(n):
	if n < 10:
		return n
	else:
		allButLast, last = n // 10, n % 10
		return sumDigits(allButLast) + last

def luhnSum(n):
	if n < 10:
		return n
	else:
		allButLast, last = n // 10, n % 10
		return lunSumDouble(allButLast) + last

def luhnSumDouble(n):
	allButLast, last = n // 10, n % 10
	luhnDigit = sumDigits(2 * last)
	if n < 10:
		return luhnDigit
	else:
		return luhnSum(allButLast) + luhnDigit
```