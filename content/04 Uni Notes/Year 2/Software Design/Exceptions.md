 [Module:: [[Software Design]]]
[Date Created:: 2025-05-03]

--- 
Though both **exceptions** and **errors** are warnings that something goes wrong, however they are distinct. 
- **Errors** are something has gone wrong, and we can't recover, *e.g. hardware fault, VM error, out of memory*
- **Exceptions** are something has gone wrong, but we can deal with the problem and recover, *e.g. divide by 0, null pointer, array index out of bounds, file not found*.
	- We can plan for and deal with these problems

In Java, when something goes wrong, an **exception** is **thrown**. These exceptions can be **caught**, and dealt with elsewhere in the program. **Uncaught** exceptions show up in the command prompt, and/or crash the program.
```table-of-contents
```
---
## Exceptions in Java
- If we divide by zero, an *ArithmeticException* would be thrown. We can catch it and deal with it, or ignore it and let the program crash! Let's not do that.
- If we overrun an array, an *ArrayIndexOutOfBoundsException* would be thrown. We can catch it and deal with it, or ignore it and let the program crash! Let's not do that.
- If a file doesn't exist when trying to open it, an *FileNotFoundException* would be thrown. We can catch it and deal with it, or ignore it and let the program crash! Let's not do that.
### Dealing with Exceptions
Java provides *try*, *catch*, and *finally* to catch **exceptions**
```java
try {  
	/* Code that could throw an exception */  
} catch (<Exception type> <reference>) {  
	/* Code that deals with the exception */  
} finally {  
	/* Optional, but if present always executes */  
}
```

```java
int a;  
int userInput = getUserInput();  
try {  
	a = 30 / userInput; // Could cause an exception  
} catch (ArithmeticException e) {  
	a = 0; // Deal with the exception  
}
```

```java
int[] array = new int[10];  
try {  
	for (int i = 0; i <= 10; i++) {  
		array[i] = 0; // Causes an exception at i=10  
	}  
} catch (ArrayIndexOutOfBoundsException aioobe) {  
	// TODO Deal with the exception  
}
```
## Exceptions We Can't Deal With
Sometimes we can't sensibly deal with the exception, and not know the best action to take to recover. In this case, we can **re-throw** the exception. We can *throw* the exception from the method where the exception occurred, to the method that called the method. A higher method is often *better placed* to make a sensible decision, and to decide who's responsible. 
```java
public class MyClass {  
	// If an exception happens in MethodA, it re-throws it  
	public int methodA(int i) throws ArithmeticException {  
		return 5 / i;  
	}  
	// MethodB catches the exception re-thrown by methodA  
	public void methodB() {  
		int z;  
		try {  
			z = methodA(0);  
		} catch (ArithmeticException ae) {  
			z = 0;  
		}
	}  
}
```
## Defining Our Own [[Exceptions]] 
We can extend the standard Java *Exception* class.
```java
public class MyClass {  
	public void methodA() throws CustomException {  
		if ( /* Something has gone wrong */ ) {  
			throw new CustomException();  
		}  
	}  
	public void methodB() {  
		try {  
			methodA();  
		} catch (CustomException ce) {  
			/* TODO Deal with CustomException */  
		}  
	}  
}
```