## 1. Explanation of the Flocking Algorithm
The program implements the three rules of a flocking algorithm, as described by Craig Reynolds in his 1987 Boids model[^1], using a programmable turtle's `move()` and `turn()` methods. These rules are:
- separation, where turtles steer away from nearby turtles;
- alignment, where turtles steer towards the average angle of nearby turtles;
- and cohesion, where turtles steer towards the average position of nearby turtles.
The effect of each rule on the rotation is calculated, summated together for each turtle, and is appropriately updated per update cycle. Each turtle constantly moves forward at a steady speed, and is able to have a random rotation, to give more natural deviations in each turtle's path. Collision has been implemented as well, where each turtle tracks the nearest edge of an obstacle, calculates its normal angle, and then reflects the turtle based off its incident angle. Finally, the canvas itself is wrapped toroidally, allowing the turtles to stay on the canvas.

The combined effect of all of these implementations creates a simulation of emergent flocking behaviour, where turtles collectively form fluid groups that dynamically respond to each other, and their environment. 
# 2. Explanation of the Design
The program is written in Java, and structured with object-oriented design. Major aspects of the program are separated in packages, and classes incorporate inheritance, composition, interfacing and polymorphism principles. (The `drawing` package has been omitted, as its class `Canvas` is provided).
### 2.1 Turtle
The `turtle` package holds all the objects associated with turtles, based off Seymour Papert's Logo[^2] system:
- `Turtle` is the base class and implements the base moves of Papert's turtle, providing basic movement, and drawing logic;
- `DynamicTurtle` *extends* `Turtle`, which allows the turtle to move on its own. It adds speed, and handles reflections when it collides with an obstacle;
- `RandomTurtleC` *extends* `DynamicTurtle`, which allows the turtle to rotate randomly, based off a random angular velocity;
- and `FlockingTurtle` *extends* `RandomTurtleC`, which implements the three rules to create the flocking behaviour, with a maximum turn angle to make rotations smoother.
An `update()` method is overridden in each subclass starting from `DynamicTurtle`, allowing each turtle to have custom behaviour every update step.
### 2.2 Geometry
The `geometry` package holds all the objects to do with geometry, giving a basis for positioning and lines:
- `CartesianCoordinate` holds two integers, one for the x-coordinate, and one for the y-coordinate;
- `LineSegment` holds two `CartesianCoordinates`, defining a line;
- `NormalAngle` is an enum, and holds/calculates the normal angle when given two `CartesianCoordinates`. If the lines are grid-aligned (when the angle is a multiple of $90\degree$), the enum instead holds the predefined constants `RIGHT, DOWN, LEFT` and `UP`, to aid with code readability.
- `CollisionSegment` *extends* `LineSegment`, and holds the point nearest to a turtle, as well as the `NormalAngle`.
### 2.3 Obstacle
The `obstacle` packages holds all the objects to do with obstacles, and is designed in order to be easily expandable for more shapes of obstacle.
- `Obstacle` is an interface, and defines abstract methods for drawing the obstacle with `CollisionSegments`, getting its edges and centre of mass, as well as testing if a point is inside the object.
- `RectangleObstacle` *implements* `Obstacle`, and defines a rectangular obstacle based on its top-left coordinate, width and height. 
### 2.4 Flocking Program
The `flockingprogram` package has the `FlockingProgram` class, which is the top-level of the program. It holds the main method, which creates the GUI, and initialises an array of turtles and obstacles.   
### 2.5 Tools
The `tools` package holds the provided `Debug` and `SystemProperties` classes, but as well as a `Debug` enum. It holds multiple predefined boolean constants for different aspects of the program such as creating turtles, their position, flocking angles, etc. which centralises debug control for the entire program.
## 3. Explanation of the Program Implementation 
### 3.1 Top-level
![[image-3.png|Figure 2: FlockingProgram Class Diagram|273x238]]

The main method is contained in the `FlockingProgram` class [See Figure 2], which also has the high-level implementation of the flocking algorithm, and uses the `javax.swing` package for the GUI elements. The constructor initialises a new `JFrame`, and then calls three methods which set up the GUI, turtles and obstacles:
- The GUI consists of:
	- an upper `JPanel`, which holds three `JButtons`. One to add a new `FlockingTurtle` in a random position and rotation (with protections to prevent it spawning inside an obstacle), another button to remove a turtle, and another button to show/hide the trail behind each turtle;
	- a `Canvas` in the centre which displays the turtles and obstacles;
	-  and a lower `JPanel` which holds 8 `JSliders` and corresponding `JLabels` to control all the turtle's parameters. The parameters being: the turtle speed, the three flocking rules' strength, the random rotation, separation radius, perception radius, and the max turn angle. Each `JSlider's` spacing is automatically calculated using the `createSlider()` method.
- The turtle setup creates an array which holds `FlockingTurtles`, and adds an initial turtle.
- The obstacle setup creates an array which holds all of the obstacles, and adds the 3 required obstacles with the appropriate positions and widths.

After this, the `main()` method calls the `gameLoop()` method, to start the turtle's movement logic. First the obstacles are drawn using a for loop which calls each obstacle's `draw()` method, and then a while loop runs for the turtle logic, which is broken down into three steps: 
- `undrawTurtles()`, which removes all the turtles from the canvas;
- `updateTurtles()`, which calculates the new movement and rotation for every turtle;
- and `drawTurtles()`, which shows all the turtles in their new orientations.
`undrawTurtles()` and `drawTurtles()` simply calls their corresponding method for each turtle (also using the `synchronized` keyword to ensure only one thread has access to the turtle array). `updateTurtles()` however, is what gives the turtle's their dynamic movement. This is also broken down into three steps:
- `turtle.reflectNearest(turtle, obstacles)`, which turns the turtle, based on its angle of incidence, if the edge of an obstacle is within the turtle's collision radius.
- `turtle.update(deltaTime, turtles)`, which updates the turtles position and rotation, based off its speed, random rotation and the three flocking rules.
- `turtle.wrapPosition(canvas.getWidth(), canvas.getHeight())`, which wraps the turtle toroidally, whenever the turtle leaves the confines of the window.
### 3.2 Turtles
![[image-2.png|Figure 3: Turtle Class Diagram|469x294]]

The turtle package uses an inheritance hierarchy [See Figure 3] to iteratively add upon itself, gradually building to the `FlockingTurtle`, which exhibits the complex flocking behaviours. The modular approach to these classes makes the code easy to read, as well as making extensions to the class in the future easier too.
#### 3.2.1 Turtle
This is the fundamental object, and implements the basic, manual moves of Papert's turtle. It has `CartesidanCoordinate` and `double` fields to store position and orientation respectively, what `Canvas` to render the turtle on, `booleans` storing if the turtle should draw it's path and if the turtle itself has been drawn, as well as an `integer` for the turtle's size. In terms of methods:
- `turn(angle)` adds the angle to the current angle, and `move(distance)` moves the turtle forwards, by using trigonometry to calculate the new coordinate, and then updating the current position to the new position.
- `turnTo(position)` and `moveTo(position)` makes the turtle point or move to a specified point
- `putPenUp()` and `putPenDown()` dictate whether the turtle draws its path on the canvas.
- `draw()` and `undraw()` creates a visual representation of the turtle in the shape of a bird, or removing it from the canvas.
#### 3.2.2 DynamicTurtle
`DynamicTurtle` extends `Turtle`, and introduces autonomous behaviour, including movement based on its speed, as well as collision detection. The new movement is calculated every time its `update(deltaTime)` method is called, based on the time between updates, and its `speed`. 

Collisions with realistic reflections were a complex aspect to implement, as we only have cartesian coordinates, and the `move()` and `turn()` methods to use. Before that, the turtle filters out most of the obstacles on the canvas, only focusing on the nearest edge to the turtle using the `nearestLine()` method. The `reflect()` method then calculates what angle to turn the turtle based on its angle of incidence, and the normal angle of the edge. The `reflectNearest()` method brings these two together, and reflects the turtle whenever its `collisionRadius` intersects with the `CollisionSegment`.  

There are multiple safeguards in place to prevent unwanted behaviour with the collisions. There is a `COLLISION_COOLDOWN`, which prevents a collision from occurring before the cooldown ends, decrementing whenever the `update()` method is called, and is resetting once a collision occurs. This prevented the turtle from getting stuck on an edge if the incident angle is too shallow. Another safeguard is in the `reflect()` method. If the turtle's angle and normal angle are roughly facing in the same direction (where their difference is $< \pm 90$), the reflection angle is set to $0$. This prevents the turtle getting stuck if it's near a corner, and the `collisionRadius` intersects the other edge while facing away from it.
#### 3.2.3 RandomTurtleC
`RandomTurtleC` extends `DynamicTurtle`, introducing random rotation, using angular velocity to make the rotation smoother.

The randomised rotation uses a counter to dictate when a new randomised angular velocity should be selected, however the counter's size changes randomly from 1 to `MAX_COUNTER` every time it completes its countdown. The `update()` method implements the functionality in `DynamicTurtle` and adds the random angular velocity.
#### 3.2.4 FlockingTurtle
Finally, `FlockingTurtle` extends `RandomTurtleC`, and fully implements the three flocking rules: separation, alignment and cohesion. All three rules require the perception of turtles near it, within the `separationRadius` for separation, and `perceptionRadius` for alignment and cohesion. When given the array holding all the turtles, it counts all the turtles within the radius, and calculates either the average repulsion force, angle, or coordinate for the separation, alignment and cohesion rules respectively. The angle to rotate according to these rules are different for each rule:
- separation uses trigonometry to calculate the angle of the repulsion force;
- alignment simple takes away the average angle with the current angle;
- and cohesion utilises the `turnTo()` method to make the turtle turn towards a point.

The `update()` method again implements the functionality in `FlockingTurtle` and adds the cumulative effects each flocking rule has on the angle. Each rule is capped to a `maxTurnAngle` to make the turning smoother, as well as a multiplier variable associated with them, which can increase/decrease the strength of each rule on the overall behaviour.
### 3.3 Geometry
![[image.png|Figure 4: Geometry Class Diagram|530x203]]

The `geometry` package [See Figure 4] defines complex data types which build the foundations of the 2D plane. The most basic elements are the data-types `CartesianCoordinate` which holds an x and y-coordinate, and a `LineSegment` which holds two `CartesianCoordinates`, representing the two endpoints of a line.

To assign a `LineSegment` to be a collision object for a turtle, a `CollisionSegment` class extends its functionality. This stores an enum `NormalAngle`, which holds the predefined constants `RIGHT(0), DOWN(90), LEFT(180)` and `UP(270)`, making code more readable as the current obstacles are always grid-aligned. The enum has a method which calculates the integer normal angle when given two points, and throws an `IllegalArgumentException` if any of the lines are diagonal. It also allows easy extension to diagonal lines, if it were implemented in the future.

It also stores the `closestPoint` to a turtle, using vector math, projection and the shortest distance between a line and a point to calculate the point on the line which is closest to a given point. If the point is outside the range of the line, it snaps to the start or end point. This feature was used to have a point to discretely move the turtle to if a turtle were to clip inside an obstacle. 
### 3.4 Obstacles
![[Obstacle Class Diagram.png|Figure 5: Obstacle Class Diagram|309x270]]

The `obstacle` package [See Figure 5] defines the static barriers the turtles can interact with, drawn with any number of `CollisionSegments`. As there are multiple shapes an obstacle could be, an interface `Obstacle` was used to define a set of abstract methods any shape of obstacle must implement. These include:
- `draw()` to render the obstacle;
- `getEdges()` returns the array of all the `CollisionSegments`;
- `getCentre()` returns the centre of mass of the obstacle;
- and `containsPoint()` checks if a given point is within the obstacle.

The `RectangleObstacle` is the primary implementation of the `Obstacle` interface, and is easily defined by its top-left coordinate, as well as its width and height. As its such a simple shape, many of the abstract methods were easily implemented, as the centre is half the width and height, and the bounds of the top left and bottom right coordinates can easily check if a point is within this range. 
## 4. Summary of Test Procedures and Results
As mentioned before, a `Debug` enum was created, which was used to have centralised control over whether certain aspects of the program printed debugging information to the console, or other behaviour to stress test the code. 
```java
public class Debug {
	public static final boolean CREATE_TURTLES = false;
	public static final boolean RANDOM_TURTLE = false;
	public static final boolean FLOCKING_TURTLE = false;
	public static final boolean POSITION = false;
	public static final boolean COLLISION = false;
	public static final boolean GUI = false;
	public static final boolean OBSTACLES = false;
}
```

This means an if statement can be placed within the appropriate parts of the code and will only run if the corresponding boolean was true. This aided in code readability, as it was more readable than an array of booleans for example. 
- `Debug.CREATE_TURTLES` runs a for loop that creates 100 turtles at the same time. At a certain point, a `ConcurrentModificationException` is thrown, as the size of the array changes when a turtle is added in the middle of a loop. This was amended by using a `synchronizedList` over the `ListArray`. Some flickering in the turtles is seen if there are too many turtles, however this seemed to be a hardware issue, as every turtle has to be individually drawn, updated and undrawn every 20 milliseconds. 
- `Debug.RANDOM_TURTLE` prints a `DynamicTurtles` angle turned, and counter whenever  is updated. No issues were found with this implementation.
- `Debug.FLOCKING_TURTLE` prints the turning angle of each of the three rules in a `FlockingTurtles`. Some turning angles turned
- `Debug.POSITION` merely outputs the average position of all the turtles on the canvas in a label.
- `Debug.COLLISION` prints a collision message whenever a turtle collides with a `CollisionSegment`. It also prints the difference between the turtle's current angle, and the angle of the `CollisionSegment's` normal, the angle of incidence, the total turn the turtle makes, as well as the collision cooldown. The angle difference and collision cooldown were implemented after unwanted behaviour when the turtle angle with the edge was shallow, where the turtle would get stuck on the edge. This was due to the collision radius still intersecting with the edge even after reflecting. The angle difference prevents bounces if the turtle and normal angle are in the same direction, and the collision cooldown prevents multiple rapid bounces with the same edge.
- `Debug.GUI` prints the major and minor spacing of each slider, which are automatically calculated based off the upper and lower bound of the slider. The thresholds for what dictates the spacing had to be adjusted, as if they were set wrong, there were too many spacing lines between the two bounds.
- `Debug.OBSTACLES` prints the location of all the obstacles on the frame.
## 5. References
[^1]: [1]
	
	C. W. Reynolds, “Flocks, herds and schools: A distributed behavioral model,” _Proceedings of the 14th annual conference on Computer graphics and interactive techniques - SIGGRAPH ’87_, vol. 21, no. 4, 1987, doi: https://doi.org/10.1145/37401.37406.

[^2]: [2]
	
	H. Abelson, N. Goodman, and L. Rudolph, “LOGO Manual,” _Mit.edu_, 2025, doi: https://doi.org/AIM-313.
