[Year:: [[Year 2]] #uni/year2]

---

> [!uninotes] Software Design
> ```dataview
list
from "04 Uni Notes/Year 2/Software Design"
where file.name != regexreplace(file.folder, ".*/", "") 
sort regexreplace(file.folder, ".*/", "") asc

```meta-bind-button
label: Create New Note
icon: plus
style: primary
class: ""
cssStyle: ""
backgroundImage: ""
tooltip: ""
id: ""
hidden: false
actions:
  - type: templaterCreateNote
    templateFile: 02 Templates/Uni Notes Template.md
    folderPath: 04 Uni Notes/Year 2/Software Design
    fileName: Untitled
    openNote: true
    openIfAlreadyExists: true

```

Will be using Java. Concept of "write once, run anywhere!"
## Comparing C and Java
Source files are compiled into Java bytecode
The Java virtual machine (JVM)

Has real strings, Booleans, datatypes.

**Class**: blueprints that hold variables, and operations on those variables
**Objects**: instances of classes, that hold fields and methods
**Composition**: a class that holds other objects in it's fields
**Inheritance**: a class that borrows fields and methods from a class 
**Polymorphism**: different classes can call the same method, and do different things
**Interfaces**: abstractly defines a class's methods, without implementing it 