[Module:: [[Software Design]]]
[Date Created:: 2025-05-05]

--- 
In Java, we can only extend from one class. If a class inherits from two classes, and both have overridden methods, the class doesn't know which method to inherit. We use **interfaces** to get the same functionality, but without the danger.
```table-of-contents
```
---
## Interface
These are a type of class, similar to [[Inheritance, Is-A Relationships#Abstract Classes|abstract classes]], they cannot be instantiated, and the only methods they can contain are:
- method signatures (abstract methods)
- static methods
- default methods

The *only* fields they can contain are effectively `static final` fields, but we can implement an unlimited number of interfaces in a single class
```java
public interface SuperHero {  
	public abstract void activateSuperPower();  
	public abstract void deactivateSuperPower();  
	public abstract void beAwesome();  
}
```

```java
public class Hulk extends Person implements SuperHero {  
	private int angry = 0;  
	public Hulk() {  
		super("Dr. Robert Bruce Banner");  
	}  
	@Override  
	public void activateSuperPower() {  
		angry = 9001; // OVER 9000!  
	}  
	@Override  
	public void deactivateSuperPower() {  
		angry = 0;  
	}  
}
``` 

If a class implements an interface, it must provide an implementation for all the abstract methods, which can be provided by either the class itself, or the super class. If two interfaces define the same abstract method, you need to provide *one* implementation to satisfy both of them. We don't choose which one to use.

```java
public class BilingualPerson extends Person implements French, Spanish {  
	public BilingualPerson(String name) {  
		super(name);  
	}  
	public void bonjour() {  
		System.out.println("Bonjour, mon nom est " + name);  
	}  
	public void auRevoir() {  
		System.out.println("Au Revoir!");  
	}  
	public void hola() {  
		System.out.println("Hola mi nombre es " + name);  
	}  
	public void adios() {  
		System.out.println("Adios!");  
	}  
}
```

We don't have to combine **FrenchPerson** and **SpanishPerson** classes to make a **BilingualPerson.** The interfaces provide a middle man.