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
- The Anonymous Factorial
```Python
from operator import sub, mul

def make_anonymous_factorial():
    """Return the value of an expression that computes factorial.
   
    >>> make_anonymous_factorial()(5)
    120
    >>> from construct_check import check
    >>> # ban any assignments or recursion
    >>> check(HW_SOURCE_FILE, 'make_anonymous_factorial',
    ...     ['Assign', 'AnnAssign', 'AugAssign', 'NamedExpr', 'FunctionDef', 'Recursion'])
    True
    """
    return (lambda f : (lambda n : f(f, n)))(
        lambda f, n : 1 if n == 0 else mul(n, f(f, sub(n, 1)))
    )
```
### Lecture 10 Tree Recursion
- Order of Recursive Calls
	- The Cascade Function *the nested call expression need to return before whatever statements happens next*
	- Two Definitions of Cascade
		- `cascade1()` is shorter
		- `cascade2()` is more clear and has typical structure
	- Inverse Cascade
```Python
def cascade1(n):
	if n < 10:
		print(n)
	else:
		print(n)
		cascade1(n // 10)
		print(n)
		
def cascade2(n):
	print(n)
	if n > 10:
		cascade2(n // 10)
		print(n)

def inverseCascade(n):
	grow = lambda n : f1Thenf2(grow, print, n // 10)
	shrink = lambda n : f1Thenf2(print, shrink, n // 10)
	
	grow(n)
	print(n)
	shrink(n)

def f1Thenf2(f1, f2, n):
	if n:
		f1(n)
		f2(n)
```
- Tree Recursion
	- Tree-shaped processes arise whenever executing the body of a recursive function makes more than one call to that function
	- Tree-Recursive Process
	- Repetition in Tree-Recursive Computation
	- Example: Counting Partitions `countPartitions(6, 4)`
		- Recursive decomposition: finding simpler instances of the problem.
		- Explore two possibilities
			- Use at least one 4
			- Don't use any 4
		- Solve two simpler problems
			- `countPartitions(2, 4)`
			- `countPartitions(6, 3)`
		- Tree recursion often involves exploring different choices
```Python
# Fibonacci Numbers
def fib(n):
	if n == 0:
		return 0
	elif n == 1:
		return 1
	else:
		return fib(n - 2) + fib(n - 1)

# Counting Partitions
def countPartitions(n, m):
	''' Count the ways to partition n using parts up to m '''
	if n == 0:
		return 1
	elif n < 0:
		return 0
	elif m == 0:
		return 0
	else:
		withm = countPartitions(n - m, m)
		withoutm = countPartitions(n, m - 1)
		return withm + withoutm
```
### Lecture 11 Sequences
- Lists
	- The number of elements `len(<list>)`
	- An element selected by its index `<list>[<index>]`
	- Concatenation and repetition `<list1> + <list2> * 2`
	- Nested lists `[<list1>, <list2>, <list3>]`
- Containers
	- Built-in operators for testing whether an element appears in a compound value `<element> in <list>` or `<element> not in <list>`
- For Statements
	- Execution Procedure
		- Evaluate the header `<expression>`, which must yield an iterable value (a sequence)
		- For each element in that sequence, in order
			- Bind `<name>` to that element in the current frame
			- Execute the `<suite>`
	- Sequence Iteration
	- Sequence Unpacking
```
for <name> in <expression>:
	<suite>
```

```Python
# Sequence Iteration
def count(s, value):
	''' Count the number of times that value in sequence s '''
	total = 0
	for iterElement in s:
		if iterElement == value:
			total += 1
	return total

# Sequence Unpacking
def countSamePair(pairs):
	''' Count the number of the same pairs in sequence pairs '''
	sameCount = 0
	for x, y in s:
		if x == y:
			sameCount += 1
	return sameCount

pairs = [[1, 2], [2, 2], [3, 2], [4, 4]]
print(countSamePain(pairs))
```
- Ranges
	- *A range is a sequence of consecutive integers*
	- Including the starting value but excluding the ending value
	- **Length**: ending value - starting value
	- **Element selection**: starting value + index
```Python
def sumBelow(n):
	total = 0
	for i in range(n):
		total += i
	return total

def cheer():
	for _ in range(3):
		pritn('Go Bears! ')
```
- List Comprehensions
```Python
odds = [1, 3, 5, 7, 9]
evens = [x + 1 for x in odds]
evensWithCond = [x + 1 for x in odds if 25%x == 0]
def divisors(n):
	return [1] + [x for x in range(2, n) if n%x == 0]
```
### Lecture 12 Containers
- Box-and-Pointer Notation
	- The Closure Property of Data Types
		- A method for combining data values satisfies the *closure property* if the result of combination can itself be combined using the same method
		- Closure is powerful because it permits us to create hierarchical structures
		- Hierarchical structures are made up of parts, which themselves are made up of parts, and so on
		- **Lists can contain lists as elements (in addition to anything else)**
	- Box-and-Pointer Notation in Environment Diagrams
		- Lists are represented as a row of index-labeled adjacent boxes, one per element
		- Each box either contains a primitive value or points to a compound value
- Slicing
	- Slicing Creates New Values
```Python
# Slicing
odds = [3, 5, 7, 9, 11]
odds[1:3] # [5, 7]
odds[:3] # [3, 5, 7]
odds[1:] # [5, 7, 9, 11]
odds[:] # [3, 5, 7, 9, 11]
```
### Lecture 13 Data Abstraction
- Data Abstraction *Compound objects combine objects together*
	- An abstract data type lets us manipulate compound objects as units
	- Isolate two parts of any program that uses data
		- How data are represented
		- How data are manipulated
	- Data abstraction: A methodology by which functions enforce an abstraction barrier between **representation** and **use**
	- Rational Numbers
	- Rational Number Arithmetic Implementation
- Abstraction Barriers & Violation
- Reducing to Lowest Terms
- Data Representations *What is Data?*
	- We need to guarantee that constructor and selector functions work together to specify the right behavior
	- Behavior condition
	- Data abstraction uses selectors and constructors to define behavior
	- If behavior conditions are met, then the representation is valid
	- **You can recognize data abstraction by its behavior**
- Rational Data Abstraction Implemented as Functions
```Python
# Rational Numbers Implementation Version 1
from fractions import gcd

# Constructor and selectors implement the abstract data type
# Constructor is a higher-order function
def rational1(n, d):
	''' Construct a rational number that represents n/d '''
	# The function select() represents a rational number
	g = gcd(n, d)
	def select(name):
		if name == 'n':
			return n // g
		elif name == 'd':
			return d // g
	return select
# Selectors call the object itself
def numer1(x):
	''' Return the numerator of rational number x '''
	return x('n')

def demon1(x):
	''' Return the denominator of rational number x '''
	return x('d')
```

```Python
# Rational Numbers Implementation Version 2

def rational(n, d):
	''' Construct a rational number that represents n/d '''
	return [n, d]

def numer(x):
	''' Return the numerator of rational number x '''
	return x[0]

def denom(x):
	''' Return the denominator of rational number x '''
	return x[1]
```

```Python
# Rational Number Arithmetic Implementation
def mulRational(x, y):
	return rational(numer(x) * numer(y), denom(x) * denom(y))

def addRational(x, y):
	nx, dx = numer(x), denom(x)
	ny, dy = numer(y), denom(y)
	return rational(nx * dy + ny * dx, dx * dy)

def equalRational(x, y):
	return numer(x) * denom(y) == numer(y) * denom(x)

def printRational(x):
	print(numer(x), '/', denom(x))
```
### Lecture 14 Tree
- Trees
	- Tree Abstraction
		- Recursive description **(wooden trees)**
			- A **tree** has a root **label** and a list of **branches**
			- Each branch is a **tree**
			- A tree with zero branches is called a **leaf**
		- Relative description **(family trees)**
			- Each location in a tree is called a **node**
			- Each **node** has a **label** that can be any value
			- One node can be the **parent/child** of another
		- People often refer to labels by their location
	- Implementing the Tree Abstraction
- Tree Processing Uses Recursion
- Creating Trees
- Examples
	- Printing Tree
	- Summing Paths
- Count Paths that have a Total Label Sum
```Python
# Trees

def tree(label, branches = []):
	# Verifies the tree definition
	for branch in branches:
		assert isTree(branch)
	return [label] + list(branches)

def label(tree):
	return tree[0]

def branches(tree):
	return tree[1:]

def isTree(tree):
	result = True
	if type(tree) != list or len(tree) < 1:
		result = False
	for branch in branches(tree):
		if not isTree(branch):
			result = False
	return result

def isLeaf(tree):
	return not branches(tree)

def fibTree(n):
	if n <= 1:
		return tree(n)
	else:
		left, right = fibTree(n - 2), fibTree(n - 1)
		return tree(label(left) + label(right), [left, right])

# Tree processing Uses Recursion
def countLeaves(t):
	''' Count the leaves of tree t '''
	if isLeaf(t):
		return 1
	else:
		branchCounts = [countLeaves(b) for b in branches(t)]
		return sum(branchCounts)

def leaves(t):
	''' Return a list containing the leaf labels of tree t '''
	if isLeaf(t):
		return [label(t)]
	else:
		return sum ([leaves(b) for b in branches(t)], [])

def incrementLeaves(t):
	''' Return a tree like t but with leaf labels incremented '''
	if isLeaf(t):
		return tree(label(t) + 1)
	else:
		bs = [incrementLeaves(b) for b in branches(t)]
		return tree(label(t), bs)

def increment(t):
	''' Return a tree like t but with all labels incremented '''
	return tree(label(t) + 1, [increment(b) for b in branches(t)])

def printTree(t, indent = 0):
	print('    ' * indent + str(label(t)))
	for b in branches(t):
		printTree(b, indent + 1)

def printSums(t, currSum):
	currSum += label(t)
	if isLeaf(t):
		print(currSum)
	else:
		for b in branches(t):
			printSums(b, currSum)

def countPaths(t, total):
	''' Return the number of paths from the root to any node in tree t for which the labels along the path sum to total '''
	if label(t) == total:
		found = 1
	else:
		found = 0
	return found + sum([countPaths(b, total - label(t)) for b in branches(t)])
```
### Lecture 15