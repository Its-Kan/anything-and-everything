 [Module:: [[Software Design]]]
[Date Created:: 2025-04-21]

--- 
In [[Composition, Has-A Relationships]], we saw how classes (objects) can contain other classes (objects).  Now we'll see inheritance, which can be thought of as an *is-a* relationship, where classes are directly related to other classes. 
- E.g. Student *is a* Person 
- Student is a *special type* of Person
- Student's are a subset of Person's  
```table-of-contents
```
---
## Class Diagrams
We can describe these relationships with a diagram.

| **Dog** <br>animal                                        | **Class name**<br>Package name |
| --------------------------------------------------------- | ------------------------------ |
| -size:int                                                 | Fields/attributes              |
| +Dog()<br>+bark():void<br>+eat():void<br>+chaseCat():void | Constructors<br>Methods        |
Access modifiers:
- `private`, "-"
- `public`, "+"
- `default` (or `package`), "~"
- `protected`, "#"

So for example, our person class will have:

| **Person** <br>person                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------- |
| -name: String<br>-age: int                                                                                                                      |
| +Person(String,int)<br>+getName():String<br>+setName(String):void<br>+getAge():int<br>+setAge(int):void<br>+sayHello():void<br>-checkAge():void |
## Inheritance

| [[Composition, Has-A Relationships]]                           | [[Inheritance, Is-A Relationships]]                         |
| -------------------------------------------------------------- | ----------------------------------------------------------- |
| Can store lots of appropriate objects, e.g. Car, House, Phone. | Some objects are a type of Person, e.g. Student, Footballer |
| A Person **"has-a"** Car                                       | A Student **is-a** Person                                   |
Let's suppose we want to make a **Superman** class. It would be similar to the **Person** class, but with some extra super-power methods. He's not a type of person, he's an *individual* person. It wouldn't make sense to make it a class, as we aren't going to have multiple Supermen. He's more like an object. 

If it was **Superperson**, then we have a special *type* of person, hence suitable for a class. We can *inherit* the functionality of **person**, and then *extend* it with superpowers.

| **Person** <br>person                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------- |
| -name: String<br>-age: int                                                                                                                      |
| +Person(String,int)<br>+getName():String<br>+setName(String):void<br>+getAge():int<br>+setAge(int):void<br>+sayHello():void<br>-checkAge():void |
⬆

| **Superperson**<br>person                             |
| ----------------------------------------------------- |
| -isFlying:boolean                                     |
| +Superperson()<br>+useLaserEyes():void<br>+fly():void |
**Implementation:**
```java
public class Superperson extends Person {  
	private boolean isFlying; 
	 
	public Superperson() {  
		super("Superman", 35);  
		isFlying = false;  
	}  
	public void useLaserEyes() {  
		System.out.println("Laser eyes activated!");  
	}  
	public void fly() {  
		isFlying = true;  
	}  
}
```

**Usage**:
```java
public void userSuperperson() {  
	// Instantiate a new Superperson object  
	Superperson ken = new Superperson();  
	
	// Can call methods defined in Person  
	int kenAge = ken.getAge();  
	
	// Can call methods defined in Superperson  
	ken.fly();  
}
```

![[Inheritance, Is-A Relationships.png]]
## Abstract Classes
Sometimes there's a class that doesn't need to be instantiated. For example, it wouldn't make sense to instantiate an **Animal** class, as it *needs* to be a type. In this case, we can make it an abstract class. They can't be instantiated, but can:
- Be inherited from (extended)  
- Contain normal fields and methods  
- Contain abstract methods  
- That must be implemented by any classes that inherit from it  
	- Subclasses, sub-subclasses, etc
```js
	public abstract class Animal {  
	// Fields (all classes) common to all animals  
	private Picture picture;  
	private Food food;  
	private Hunger hunger;  
	private Boundaries boundaries;  
	private Location location;  
	
	// Non-abstract methods  
	public Picture getPicture() {  
		return picture;  
	}  
	
	// Abstract methods – with no method body  
	public abstract void makeNoise();  
	/* Other stuff… */
```

- If an inheritance redefines a method in the superclass, use @Override 
- The `protected` keyword applies to fields and methods, and can only be accessed by either from within their own package, or from classes that inherit from that class.

```js
// Won’t compile  
// Animal animal = new Animal();  

Cat cat = new Cat();  
Dog dog = new Dog();  

cat.makeNoise(); // prints Meow  
dog.makeNoise(); // prints Woof  

Hunger catHunger = cat.getHunger();  
Hunger dogHunger = dog.getHunger();
```