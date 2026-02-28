 [Module:: [[Software Design]]]
[Date Created:: 2025-03-21]

--- 
In the [[Objects and Classes]] lecture, we created a class called *Person*, that stored:
- an age of type *int*
- a name of type *String*
However, we can store references to other objects too!
```table-of-contents
```
---
## A Motorbike
A motorbike is made of multiple parts. It has:

- **Wheels**:
```js
public class Wheel {  
	private float radius;  
	private float pressure;  
	
	public Wheel(float radius, float pressure) {  
		this.radius = radius;  
		this.pressure = pressure;  
	}  
	
	public float getRadius() {  
	return radius;  
	}  
	
	public float getPressure() {  
	return pressure;  
	}  
}
```
- **An engine**:
```js
public class Engine {  
	private int gear;  
	
	public Engine() {  
	gear = 1;  
	}  
	
	public void shiftUp() {  
	gear++;  
	}  
	
	public void shiftDown() {  
	gear--;  
	}
}
```

So, a *MotoBike* class is **composed** of both *Wheel* objects and an *Engine* object.

```js
public class MotoBike {  
	private Wheel frontWheel;  
	private Wheel backWheel;  
	private Engine engine;  
	
	public MotoBike() {  
		frontWheel = new Wheel(10, 100);  
		backWheel = new Wheel(10, 100);  
		engine = new Engine();  
	}  
}
```
## "Has-A" Relationships
Another name for composition.
- The *MotoBike* class **has-a** *Engine*
- The *MotoBike* class **has-a** *Wheel*

It's much better to build complex classes out of simple classes, rather than having a "flat" structure with a lot of primitives. It can get bulky. We can **encapsulate** the functionality of a wheel in its own class, so the *MotoBike* class becomes simpler.

> [!note]
> Instance variables (or the fields in the class) are always initialised. They're set to 0 for base types, and objects are set to *null*.
> Method variables (local) however are never automatically initialised, so they aren't assigned any value when created. We need to initialise a value to it, before we can use it.