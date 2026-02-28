 [Module:: [[Software Design]]]
[Date Created:: 2025-05-03]

--- 
Standard Java libraries have many I/O classes, for reading and writing files/zip/buggers. 
```table-of-contents
```
---
- You can use **FileWriter** and **FileReader** for low level access
- Or **BufferedReader** for higher level access
- Or **Scanner** for parsing (splitting up) input
However, these files can throw an **IOException**, so make sure to use *try*/*catch*.
## File Writing
We need to:
- open the file (using e.g. **FileWriter**)
- write to the file
- close the file
```java
import java.io.File;  
import java.io.FileWriter;  
import java.io.IOException;  

/* … other stuff … */  

	File myFile = new File("myfile.txt");  
	if (myFile.exists())  
		return false;  
	try {  
		FileWriter writer = new FileWriter(myFile);  
		writer.write("Hello world in a file");  
		writer.close();  
	} catch (IOException ioe) {  
	/* TODO Deal with exception */  
	}
```
## File Reading
We need to:
- open the file (using e.g. **FileWriter**)
- make a *BufferedReader* object, to read data from the *FileReader* line by line
- read from the *BufferedReader*
- close the file

Why the *BufferedReader* object? It makes our lives easier! *FileReader* can only read a file character by character, so *BufferedReader* can read a file using *FileReader*, but line by line.