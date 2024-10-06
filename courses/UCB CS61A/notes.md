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
### Lecture 15 Mutability
- Object `<object_name>.<attribute_name>` *dot expression*
	- Objects represent information
	- Objects consist of data and behavior, bundled together to create abstractions
	- Objects can represent things, but also properties, interactions & processes
	- A type of object is called a class; classes are first-class values in Python
	- Object-oriented programming
		- A metaphor for organizing large programs
		- Special syntax that can improve the composition of programs
	- In Python, every value is an object
		- All objects have attributes
		- A lot of data manipulation happens object methods
		- Functions do one thing; objects do many related things
	- Example: Strings
- Representing Strings
	- the ASCII Standard
	- the Unicode Standard
- Mutation Operations
	- Some Objects Can Change
		- The same object can change in value throughout the course of computation
		- All names that refer to the same object are affected by a mutation
		- Only objects of mutable types can change: `lists & dictionaries`
	- Mutation Can Happen Within a Function Call
		- A function can change the value of any object **in its scope**
```Python
def mystery1(s):
	s.pop()
	s.pop()

def mystery2(s):
	s[2:] = []

def mystery3():
	four.pop()
	four.pop()

four = [1, 2, 3, 4]

```
- Tuples are *immutable sequences*
	- Immutable values are protected from mutation
	- An immutable sequence may still change if it contains a mutable value as an element
- Mutation
	- Sameness and Change
		- As long as we never modify objects, a compound object is just the totality of its pieces
		- A compound data object has an "identity" in addition to the pieces of which it is composed
	- **Identity** Operators `is & is not`
	- Mutable Default Arguments are Dangerous
		- A default argument value is **part of a function value**, not generated by a call
- Mutable Function
	- A Function with Behavior That Varies Over Time
	- Mutable Values & Persistent Local State
### Lecture 16 Iterators
- Iterators
	- A container can provide an iterator that provides access to its elements in some order
	- `iter(iterable)` returns an iterator over the elements of an iterable value
	- `next(iterator)` returns the next element in an iterator
- Dictionary Iteration
	- An *iterable* value is any value that can be passed to `iter` to produce an iterator
	- An *iterator* is returned from `iter` and can be passed to `next`
	- All iterators are mutable
	- A dictionary, its keys, its values, and its items are iterable values
- For statement
- Built-in Functions for Iteration
	- Many built-in sequence operations return iterators that compute results lazily
	- The Zip Function
		- The built-in `zip` function returns an iterator over co-indexed tuples
		- If one iterable is longer than the other, `zip` only iterates over matches and skips extras
		- More than two iterable can be passed to `zip`
```Python
def palindrome(s):
	''' Return whether s is the same backward and forward '''
	return all([a == b for a, b in zip(s, reversed(s))])
```
- Reasons for Using Iterators
	- Code that processes an iterator or iterable makes few assumptions about the data itself
		- Changing the data representation doesn't require rewriting code
		- Others are more likely to be able to use your code on their data
	- An iterator bundles together a sequence and a position within that sequence as one object
		- Passing that object to another function always retains the position
		- Useful for ensuring that each element of a sequence is processed only once
		- Limits the operations that can be performed on the sequence to only requesting `next`
### Lecture 17 Generators
- Generators and Generator Functions
	- A generator function is a function that yields values instead of returning them
	- A normal function returns once; a generator function can yield multiple times
	- A generator is an iterator created automatically by calling a generator function
	- When a generator function is called, it returns a generator that iterates over its yields
-  Generators can Yield from Iterators
	- A yield from statement yields all values from an iterator or iterable
- Example: Partitions
	- Yielding Partitions
```Python
def countPartitions(n, m):
	if n < 0 or m == 0:
		return 0
	else:
		exactMatch = 0
		if n == m:
			exactMatch = 1
		withM = countPartitions(n-m, m)
		withoutM = countPartitions(n, m-1)
		# exactMatch, withM and withoutM are three basic cases for partition
		return exactMatch + withM + withoutM

def listPartitions(n, m):
	if n < 0 or m == 0:
		return []
	else:
		exactMatch = []
		if n == m:
			exactMatch = [[m]]
		withM = [p + [m] for p in listPartitions(n-m, m)]
		withoutM = listPartitions(n, m-1)
		return exactMatch + withM + withoutM

def partitions(n, m):
	if n < 0 or m == 0:
		return []
	else:
		exactMatch = []
		if n == m:
			exactMatch = [str(m)]
		withM = [p + ' + ' + str(m) for p in partitions(n-m, m)]
		withoutM = partitions(n, m-1)
		return exactMatch + withM + withoutM

def yieldPartitions(n, m):
	if n > 0 and m > 0:
		if n == m:
			yield str(m)
		for p in partitions(n-m, m):
			yield p + ' + ' + str(m)
		yield from partitions(n, m-1)
```
### Lecture 18 Objects
- Object-Oriented Programming
	- A method for organizing programs
		- Extends data abstraction
		- Bundles together information and related behavior
	- A metaphor for computation using distributed state
		- Each **object** has its own local state
		- Each object also knows how to manage its own local state
		- Interact with an object using its **methods**
		- Several objects may all be instances of a common **class**
		- Different classes may relate to each other
	- Specialized syntax & vocabulary to support this metaphor
		- A **class** defines how objects of a particular type behave
		- An **object** is an instance of a class; the class is its type
		- A **method** is a function called on an object using a dot expression: `array.append(5)`
- Class Statements
	- Classes *A class describes the behavior of its instances*
	- Example: The Account Class
```Python
class Account:
	def __init__(self, accountHolder):
		self.balance = 0
		self.holder = accoutHolder
	
	def deposit(self, amount):
		self.balance = self.balance + amount
		return self.balance
	def withdraw(self, amount):
		if amount > self.balance:
			return 'Insufficient funds'
		self.balance = self.balance - amount
		return self.balance
```
- Creating Instance
	- Object Construction *When a class is called*
		- A new instance of that class is created
		- The `__init__` method of the class is called with the new object as its first argument (named `self`), along with any additional arguments provided in the call expression
		- The `__init__` method is sometimes called a constructor
	- Instance Attributes
		- An object's attributes are accessed and modified using dot expressions
		- Any attribute can be assigned any value
	- Object Identity
		- Every object that is an instance of a user-defined class has a unique identity
		- Identity operators `is` and `is not` test if two expressions evaluate to the same object
		- Binding an object to a new name using assignment does not create a new object
- Method
	- Invoking Methods
		- All invoked methods have access to the object via the self parameter, and so they can all access and manipulate the object's attributes
		- Dot notation automatically supplies the first argument to a method
### Lecture 19 Attributes
- Class Attributes
	- The Class Statement
		- A class statements creates a new class and binds that class to `<name>` in the first frame of the current environment
		- Assignment & def statements in `<suite>` create attributes of the class (not names in frames)
	- *Class Attributes*
		- Class attributes are "shared" across all instances of a class because they are attributes of the class, not the instance
```
class <name>:
	<suite>
```
- Attribute Lookup
	- Looking Up Attributes by Name
		- Both instances and classes have attributes that can be looked up by dot expressions
		- To evaluate a dot expression
			- Evaluate the `<expression>` to the left of the dot, which yields the object of the dot expression
			- `<name>` is matched against the instance attributes of that object; if an attribute with that name exists, its value is returned
			- If not, `<name>` is looked up in the class, which yields a class attribute value
			- That value is returned unless it is a function, ,in which case a bound method is returned instead
	- *Accessing Attributes* Looking up an attribute name in an object may return
		- One of its instance attributes, or
		- One of the attribute of its class
- Attribute Assignment
	- Assignment to Attributes
		- Assignment statements with a dot expression on their left-hand side affect attributes for the object of that dot expression
			- If the object is an instance, then assignment sets an instance attribute (which overwrites the class attribute! )
			- If the object is a class, then assignment sets a class attribute
	- Attribute Assignment Statements
- Method Calls
	- Dot Expressions
		- Methods are invoked using dot notation
		- Evaluates to the value of the attribute looked up by `<name>` in the object that is the value of the `<expression>`
- Bound Methods
	- Terminology: Attributes, Functions, and Methods
		- All objects have attributes, which are name-value pairs
		- A class is a type (or category) of objects
		- Classes are objects too, so they have attributes
		- Instance attribute: attribute of an instance
		- Class attribute: attribute of the class of an instance
		- Python object system
			- Functions are objects
			- Bound methods are also objects: a function that has its first parameter "self" already bound to an instance
			- Dot expressions evaluate to bound methods for class attributes that are functions
	- Methods and Functions *Python distinguishes between*
		- *Functions*, which we have been creating since the beginning of the course
		- *Bound methods*, which couple together a function and the object on which that method will be invoked
### Lecture 20 Inheritance
- Inheritance
	- Inheritance is a method for relating classes together.
	- A common use: Two similar classes differ in their degree of specialization.
	- The specialized class may have the same attributes as the general class, along with some special-case behavior.
	- Conceptually, the new subclass "shares" attributes with its base class.
	- The subclass may override certain inherited attributes.
	- Using inheritance, we implement a subclass by specifying its differences from the base class.
- Inheritance Example *A CheckingAccount is a specialized type of Account*
- Looking Up Attribute Names on Classes
	- If it names an attribute in the class, return the attribute value.
	- Otherwise, look up the name in the base class, if there is one.
- Object-Oriented Design
	- Designing for Inheritance
		- Don't repeat yourself; use existing implementations
		- Attributes that have been overridden are still accessible via class objects. 
		- Look up attributes on instances whenever possible. 
	- Inheritance and Composition
		- Inheritance is best for representing 'is-a' relationships. 
		- Composition is best for representing 'has-a' relationships.
- Attributes Lookup Practice
```Python
class A:
	z = -1
	def f(self, x):
		return B(x - 1)

class B:
	n = 4
	z = -1
	
	def __init__(self, y):
		if y:
			self.z = self.f(y)
		else:
			self.z = C(y+1)
	
	def f(self, x):
		return B(x - 1)

class C:
	n = 4
	z = -1
	
	def __init__(self, y):
		if y:
			self.z = self.f(y)
		else:
			self.z = C(y+1)
	
	def f(self, x):
		return x

a = A()
b = B(1)
b.n = 5

>>> C(2).n
4
>>> a.z == C.z
True
>>> a.z == b.z
False
```
- Multiple Inheritance
	- A class may inherit from multiple base classes in Python.
	- Resolving Ambiguous Class Attribute Names
```Python
class Account:
	'''A bank account.'''
	interest = 0.02
	
	def __init__(self, account_holder):
		self.holder = account_holder
		self.balance = 0
	
	def deposit(self, amount):
		''' Add amount to balance. '''
		self.balance = self.balance + amount
		return self.balance
	
	def withdraw(self, amount):
		''' Subtract amount from balance. '''
		if amount > self.balance:
			return 'Insufficient funds'
		else:
			self.balance = self.balance - amount
			return self.balance
	
class CheckingAccount(Account):
	'''A bank account that charges for withdrawals. '''
	withdrawFee = 1
	interest = 0.01
	def withdraw(self, amount):
		return Account.withdraw(self, amount + self.withdrawFee)

class AsSeenOnTVAccount(CheckingAccount, SavingsAccount):
	def __init__(self, accountHolder):
		self.holder = accountHolder
		self.balance = 1 # A free dollar! 

class Bank:
	''' A bank *has* accounts. '''
	def __init__(self):
		self.accounts = []
	
	def openAccount(self, holder, amount, kind = Account):
		account = kind(holder)
		account.deposit(amount)
		self.accounts.append(account)
		return account
	
	def payInterest(self):
		for a in self.accounts:
			a.deposit(a.balance * a.interest)
	
	def tooBigtoFail(self):
		return len(self.accounts) > 1
```
### Lecture 21 Representation
- String Representations
	- An object value should behave like the kind of data it is meant to represent
	- For instance, by producing a string representation of itself
	- Strings are important: they represent language and programs
	- In Python, all objects produce two string representations
		- The `str` is legible to humans
		- The `repr` is legible to the Python interpreter
	- The `str` and `repr` strings are often the same, but not always
- The `repr` String for an Object
	- The `repr` function returns a Python expression (a string) that evaluates to an equal object
	- The result of calling `repr` on a value is what Python prints in an interactive session
	- Some objects do not have a simple Python-readable string
- The `str` String for an Object
	- Human interpretable strings are useful as well
	- The result of calling `str` on the value of an expression is what Python prints using the `print` function
- F-Strings String Interpolation in Python
		- String interpolation involves evaluating a string literal that contains expressions. 
		- The result of evaluating an f-string literal contains the str string of the value of each sub-expression. 
		- Sub-expressions are evaluated in the current environment. 
- Polymorphic Functions
	- Polymorphic function: A function that applies to many (ploy) different forms (morph) of data
	- `str` and `repr` are both polymorphic, and they invokes according zero-argument method on its argument
- Implementing `repr` and `str`
	- The behavior of `repr` is slightly more complicated than invoking `__repr__`on its argument
		- An instance attribute called `__repr__`  is ignored! Only class attributes are found. 
		- `type(x).__repr__(x)`
	- The behavior of `str` is also complicated
		- An instance attribute called `__str__` is ignored
		- If no `__str__` attribute is found, uses `repr` string
	- Interfaces
		- **Message passing**: Objects interact by looking up attributes on each other (passing messages)
		- The attribute look-up rules allow different data types to respond to the same message
		- A **shared message** (attribute name) that elicits similar behavior from different object classes is a powerful method of abstraction
		- An interface is a set of shared messages, along with a specification of what they mean
- Special Method Names
	- Special Method Names in Python
		- Certain names are special because they have built-in behavior
		- These names always start and end with two underscores
	- Special Methods
```Python
def gcd(n, d):
	while n != d:
		n, d = min(n, d), abs(n - d)

class Ratio:
	def __init__(self, n, d):
		self.numer = n
		self.denom = d

	def __repr__(self):
		return 'Ratio{0}, {1}'.format(self.numer, self.denom)

	def __str__(self):
		return '{0}/{1}'.format(self.numer, self.denom)

	def __add__(self, other):
		# type dispatching
		if isinstance(other, int):
			n = self.numer + self.denom * other
			d = self.denom
		elif isinstance(other, Ratio):
			n = self.numer * other.donom + self.donom * other.numer
			d = self.denom * other.denom
		elif isinstance(other, float):
			# type coercion
			return float(self) + other
		g = gcd(n, d)
		return Ratio(n // g, d // g)

	__radd__ = __add__

	def __float__(self):
		return self.numer/self.denom
```
### Lecture 22 Composition
- Linked List
	- Linked List Structure
		- A linked list is either empty **or** a first value and the rest of the linked list
		- Example `Link(3, Link(4, Link(5, Link.empty)))`