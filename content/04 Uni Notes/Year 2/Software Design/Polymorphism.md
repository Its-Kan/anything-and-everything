 [Module:: [[Software Design]]]
[Date Created:: 2025-05-02]

--- 
Let's say we have a student, Jane, who plays football.
- Jane *is-a* **Student**, which extends **Person**
- Jane *is-a* **FootballPlayer**, which also extends **Person**
However, we can't assign her both. What do we do?
```table-of-contents
```
---
## Overloading
### Method
In a math library we may define an add method for adding:  
- Two int’s  
- Two float’s  
- Two double’s  

In C, we can only have one method called **add**. We would need to give a unique name to each one

In Java, we can do something called **method overloading**. They can all share the name, but have different inputs.
```java
public class MathLibrary {  
	public static int add(int a, int b) {  
		return a + b;  
	}  
	public static float add(float a, float b) {  
		return a + b;  
	}  
	public static double add(double a, double b) {  
		return a + b;  
	}  
}
```
### Constructor
We can do the same with constructors, which mean we can define a new object in multiple ways, depending on what we want
```java
public class Turtle {  
	private Canvas canvas;  
	private double direction; 
		 
	public Turtle(Canvas canvas) {  
		this.canvas = canvas;  
		direction = 0.0;  
		// or this(canvas, 0.0);
	}  
	public Turtle(Canvas canvas, double angle) {  
		this.canvas = canvas;  
		direction = angle;  
	}  
}
```
## Overriding
### Method
In [[Inheritance, Is-A Relationships]], a class extends another class. What if a method inherited by the subclass doesn't do the appropriate thing for the subclass? For example in **Person**, let's have a method that says "I am mortal". But if we extend **Person** for **Superperson**, this method doesn't make sense any more. We need to *override* this behaviour for **Superperson**.
## Polymorphism
A variable is allowed to refer to different object types.