### Lecture 1 Introduction
- Welcome! 
	- 61B Overview
		- Writing code that runs efficiently
			- Good algorithms. 
			- Good data structures.
		- Writing code efficiently.
			- Designing, building, testing, and debugging large programs.
			- User of programming tools.
				- git, IntelliJ, JUnit, and various command line tools.
			- Java (not the focus of the course! )
	- Other great features of 61B:
		- The most popular topics for job interview questions in software engineering.
			- Examples : Hash tables, binary search trees, quick sort, graphs, Dijkstra's algorithm.
		- Some really cool math. Examples: 
			- Asymptotic analysis.
			- Resizing arrays.
			- The isometry between self-balancing 2-3 trees and self-balancing red black trees.
			- Graph theory.
			- P=NP
		- Once you're done : the confident sense that you can build any software.
	- Class Phase
		- Phase 1 (weeks 1 - 4) : Introduction to Java and Data Structures. 
		- Phase 2 (weeks 5 - 10) : Data Structures.
		- Phase 3 (weeks 12 - 14) : Algorithms.
- Our First Java Programs
	- Hello World
		- Reflections
			- In Java, all code must be part of a class.
			- Classes are defined with `public class CLASSNAME`
			- We use `{ }` to delineate the beginning and ending of things.
			- We must end lines with a semicolon.
			- The code we want to run must be inside `static void main(String[] args)`
		- Java is an object oriented language with strict requirements
			- Every Java file must contain a class declaration
			- **All code** lives inside a class, even helper functions, global constants, etc.
			- To run a Java program, you typically define a main method using `public static void main(String[] args)`
	- Hello Numbers
		- Reflections
			- Before Java variables can be used, they must be declared.
			- Java variables must have a specific type.
			- Java variable types can never change.
			- Types are verified before the code even runs! 
		- Java is statically typed
			- All variables, parameters, and methods must have a declared type.
			- That type can never change.
			- Expressions also have a type.
			- The compiler checks that all the types in your program are compatible **before the program ever runs**
	- Larger
		- Reflections
			- Functions must be declared as part of a class in Java. A function that is part of a class is called a "method". So in Java, all functions are methods.
			- To define a function in Java, we use "public static". We will see alternate ways of defining functions later.
			- All parameters of a function must have a declared type, and the return value of the function must have a declared type. Functions in Java return only one value! 
	- Reflections on Java
		- Compilation vs. Interpretation
			- In Java, compilation and interpretation are two separate steps.
			- Java source code is compiled into `.class` file, and then JVM interpreter the `.class` file
	- Object-Oriented Programming
		- A model for organizing programs
			- Modularity : Define each piece without worrying about other pieces, and they all work together
			- Allows for data abstraction : You can interact with an object without knowing how it's implemented
		- Objects
			- An object bundles together information and related behavior
			- Each object has its own local state
			- Several objects may all be instances of a common type
		- Classes
			- A class serves as a template for all of its instances
			- Each object is an *instance* of some class

```Java
public class helloWorld {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}

public class helloNumbers {
	public static void main(String[] args) {
		int x = 0;
		while(x < 10) {
			System.out.println(x);
			x = x + 1;
		}
		
		/*
		String x;
		x = "horse";
		System.out.println(x);
		*/
	}
}

public class larger {	
	public static int larger(int x, int y) {
		if (x > y) {
			return x;
		}
		else {
			return y;
		}
	}
	
	public static void main(string[] args) {
		System.out.println(larger(-5, 10))
	}
}

public class car {
	String model;
	int wheels;
	
	public car(String m) {
		this.model = m;
		this wheels = 4;
	}
	
	public drive() {
		if (this.wheels < 4) {
			System.out.println(this.model + "no go vroom");
			return;
		}
		System.out.println(this.model + "go vroom");
	}
	
	public int getNumWheels() {
		return this.wheels;
	}
	
	public void driveIntoDitch(int wheelslost) {
		this.wheels = this.wheels - wheelslost;
	}
}

public static void main(String[] args) {
	Car c1 = new Car("Civic Typr R");
	Car c2 = new Car("Toyota Camry");
	
	c1.drive();
	c1.driveIntoDitch(2);
	c1.drive();
	
	System.out.println(c2.getNumWheels());
}
```
### Lecture 2 Defining and Using Classes
- 