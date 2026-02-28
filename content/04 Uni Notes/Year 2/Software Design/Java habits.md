
> [!uninotes]- The **final** keyword
> With a variable, the final keyword indicates it cannot be changed after its initial definition:  
> 1. A final variable can only be assigned once.  
> 2. If it’s a primitive (int, float, etc), its value cannot change.  
> 3. If it’s an object reference, the reference cannot change (the object itself can be modified).  
> ## Code Conventions for **final** variables  
> Consider the following example (we could use it to create objects for different solar systems):  
> ```java
> public class SolarSystem {  
> public static final double MASS_OF_EARTH = 5.9722e24;  
> private final int numberOfPlanets = 8;  
> // Other stuff in this class...  
> }  
> ```
> For **MASS_OF_EARTH**, there is also a static keyword:  
> So, the class only has one copy of this "constant" – every object created from this class will see the same constant. The name should be all capitals with underscores. They are usually public.  
> 
> For **numberOfPlanets**, there is no static keyword (an instance variable):  
> So, every object created from this class has its own version of this instance variable, possibly with a different value in each object – but, the value cannot change once assigned. The name should be camelCase. They are often still kept private.  
> 
> In the example, the mass of the earth would not change even if we were talking about a different solar system – whereas different solar systems may have a different number of planets.  
> 
> Different **SolarSystem** objects would have:  
>4. the same access to the single MASS_OF_EARTH constant;  
>5. different copies of the **numberOfPlanets** instance variables.

> [!uninotes]- Classes, Objects, Fields & Local Variable **Naming Conventions**
> ## **Class** names 
> MUST start with upper case initial  
> -  E.g. “MyClassName” not “myClassName”  
> 
> ## **Fields/local variables** (hence objects) 
> MUST start with lower case initial  
> - E.g. “myVariableName” not “MyVariableName”  
>  
> ## **Constants** 
> MUST have all upper case with underscores  
> - E.g. “MY_CONSTANT” not “MYCONSTANT” or “My_Constant”

> [!uninotes]- Who should deal with **Exceptions**?
> It is often very bad practice to just pass a problem to someone else as an easy option for us. But in this case, the file name is passed in from the calling method, so it is reasonable to expect that the calling method should deal with the problem if the file doesn’t exist.  
>   ## Guideline
> An often-useful way of working out who should deal with the problem is to consider...  
> 1. If the problem is partly caused by the calling method, then it is sensible to throw the exception back out to the calling method to deal with.  
> 2. If the problem is mainly caused within our method, then we should deal with it there.  In the example of our turtle application, if the calling method gives us a file to read that doesn’t exist, then option 1) is a sensible choice – we are insisting that the calling method takes responsibility for ensuring that the file exists. (you should check the IO API as there is a nice class that allows us to do this efficiently)

