 [Module:: [[Software Design]]]
[Date Created:: 2025-03-08]

--- 
In C, data and functions are defined separately. We create objects that store some sort of customised data, and then we can manipulate this data outside of the object, using functions. 

```c
// Define a complex number data structure  
struct ComplexNumber {  
	float real;  
	float imaginary;  
};  
// Other code…  
// Define a function for conjugating a complex number  
ComplexNumber conjugate(ComplexNumber cn){  
	cn.imaginary = -cn.imaginary;  
	return cn;  
}
```

In Java, we can do both in one structure, called a **class**. We have data (real, imaginary) called fields, and methods (conjugate), which provides functionality to the data.

```js
public class ComplexNumber {  
	float real;  
	float imaginary;  
	
	void conjugate() {  
		imaginary = -imaginary;  
	}  
}
```

```table-of-contents
```
---
## Using Classes
### Objects
Using the *ComplexNumber* class as an example, we can use it to create an instance of the class, called an **object**. We can define a new object using the **new** keyword, called **instantiation**.

```js
ComplexNumber x = new ComplexNumber();
```

We now have an **object** called *x* which adopts the *ComplexNumber* data type. We can now use this object to do stuff! We can use a dot to change the fields, or call a method. 

```js
x.real = 1;
x.imaginary = 2;

x.conjugate();
```

> [!note] Habit
> It's good practice to name classes and objects as nouns, and methods as verbs.

> [!example]
> Create a virtual person in a game, described by a name and an age, and is able to say say "Hello!"
> 
> ```js
> public class Person { // Defines a new class 
> 	// Fields
> 	String name;
> 	int age;
> 
> 	// Methods
> 	void sayHello() {
> 		System.out.println("Hello, I'm " + name);
> 	}
> }
> 
> // Instantiate a Person object
> Person alice = new Person();
> 
> // Set the values of the fields
> alice.name = "Alice";
> alice.age = 32;
> 
> alice.sayHello();
> ```

However, if we call a method without properly setting up the object, we might get some errors. In this case, we're directly changing the fields inside. Instead, we can use **constructors**!
### Constructors
Using **constructors**, we can define the fields at the same time as instantiating the object.

```js
public class Person {
	String name;
	int age;
	
	// Constructor
	public Person(String name, int age) {
		this.name = name; // this allows us to refer to the class variable (field)
		this.age = age; // and not the method variable (local variable)
	}
	
	void sayHello() {
		System.out.println("Hello, I'm " + name);
	}
}

// We must now specify a name and age
Person alice = new Person("Alice", 32);
alice.sayHello();
```

We can force a name and age to be set (a behaviour) for *sayHello* to work. 
## Public vs. Private
What if we set age to a negative number? Of course that doesn't exist, so we can prevent the age being set to a negative number in the constructor:

```js
public Person(String name, int age) {
		this.name = name;
		if (age < 0) {
			age = Math.abs(age);
		}
		this.age = age; 
	}
```

But wait, if we bypass the constructor and set the field directly, the negative number can still be set! How do we fix this? Well, Java has keywords for controlling *access* from outside the class, for both the fields and methods. We've been using **public** for defining, however there's also:

- **public** - fields/methods *can* be accessed from outside the class
- **private** - fields/methods *cannot* be accessed from outside the class

| **Modifier** | **Class** | **Package** | **Subclass** | **World** |
| ------------ | --------- | ----------- | ------------ | --------- |
| *public*     | ✅         | ✅<br>       | ✅<br>        | ✅<br>     |
| *protected*  | ✅<br>     | ✅<br>       | ✅<br>        | ❌         |
| no modifier  | ✅         | ✅           | ❌            | ❌         |
| *private*    | ✅         | ❌           | ❌            | ❌         |

> [!NOTE]
> 
> | **Property**           | **Access Modifier** | **Inappropriate Access Modifier** | **Consequences of Wrong Access** |
> | ---------------------- | ------------------- | --------------------------------- | -------------------------------- |
> | Engine Management Unit | `private`           | `public`                          | Damage to engine                 |
> | Accelerator            | `public`            | `private`                         | Life very boring                 |
> | Brake                  | `public`            | `private`                         | Life too exciting                |
> | Steering Wheel         | `public`            | `private`                         | Life too exciting                |

We can now apply this to our person class:

```js
public class Person {
	private String name;
	private int age;
	
	public Person(String name, int age) {
		this.name = name;
		if (age < 0) {
			age = Math.abs(age);
		}
		this.age = age;
	}
	
	public void sayHello() {
		System.out.println("Hello, I'm " + name);
	}
}
```

We can now no longer edit the fields directly. But what if we want to view it without editing it? 
### Getters and Setters
If so, we can make certain methods for accessing object fields:
- a **getter** method allows us to *get* the value stored in a field
- a **setter** method allows us to *set* the value stored in a field

These methods *control how* fields can be accessed and changed. For example, we can return a value in meters even if the field is in inches. We can change the field from inches to miles without the user knowing. If you need to keep it completely private, just don't add getter and setter methods.

``` js
public int getAge() {
	//getter
	return age;
}

public void setName(string name) {
	//setter
	this.name = name;
}
```

So combining everything we have:

```js
Person alice = new Person("Alice", 32);  

// alice.age = 42; -- No longer compiles  
// alice.name = "Alicia"; -- No longer compiles  

// We can read the age, but not the name  
int age = alice.getAge();  

// We can change the name, but not the age  
alice.setName("Alicia");  

// Prints to the screen "Hello I’m, Alicia"  
alice.sayHello();  
```