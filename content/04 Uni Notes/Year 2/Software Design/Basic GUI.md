 [Module:: [[Software Design]]]
[Date Created:: 2025-05-05]

--- 
The `Swing` package can be used to implement GUI's. We've seen `Jframe` to hold GUI `Component`'s.
```table-of-contents
```
---
## `JLabel`
This extends `JComponent`, which extends `Container` which extends `Component`, and can contain text and/or images. 
**Text**
```java
JFrame frame = new JFrame();  

JLabel label = new JLabel("Hello!");  
frame.add(label);
```

**Images**
```java
JFrame frame = new JFrame();  

ImageIcon image = new ImageIcon("superman.png");  
JLabel label = new JLabel(image);  
frame.add(label);  
frame.pack();
```
## Layouts
To specify the position of a `Component`, we need to use `Layouts`