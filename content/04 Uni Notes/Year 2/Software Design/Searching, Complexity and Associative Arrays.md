 [Module:: [[Software Design]]]
[Date Created:: 2025-03-09]

--- 
```table-of-contents
```
---
## Linear Search
```js
public int linearSearch(int[] array, int target) {  
	for (int index = 0; index < array.length; index++) {  
		if (array[index] == target)  
		return index;  
	}  
	return -1;  
}  
```
 
 The time to complete a linear search is a function of the number of elements in the array, thus the time scales with the size of the array. **Complexity analysis** is concerned with this scaling.
- In the worst case, the search has to check *all n* elements
- In the best case, the search ahs to check *only 1* element 
- But on average, it has to check *n/2 (half)* elements 
	- If the input size *n* doubles, so does the time required to find the target value, hence a linear relationship
## Binary Search 
If we keep a random-access collection in order of the relevant component value (the key), we can search it efficiently breaking the problem in two. Essentially, having an ordered list in which we can access any element allows us to split the array into two.
### Algorithm
1. Calculate the middle array index from the average of the bottom and top indices
2. Check the value at this index
	- If **bigger** than needed, repeat the search in the lower half of the array
	- If **smaller** than needed, repeat the search in the upper half of the array

```js
public int binarySearch(int x, int[] array, int numInArray)  
{  
	int middle;  
	int start = 0;  
	int end = numInArray - 1;  
	
	while (end >= start) {  
		middle = (start + end) / 2;  
		if (array[middle] == x)  
			return middle;  
		if (array[middle] < x)  
			start = middle + 1;  
		else  
			end = middle - 1;  
	}  
	return -1;  
}  
```

This works, however if *x* appears multiple times or not at all, then it's unhelpful.
## Algorithm Analysis 
We can analyse an algorithm's space, but time is usually the key issue. We can:
- Count operations for a particular set of parameters
- Count operations as a function of the problem size, then generalise over all the possible inputs.
## RAM Model of Computation
To quantify the computation cost, we need to simplify some operations:
- **Simple operations** (+, -, \*, /, =) take **one** time step
- **Memory access** takes **one** time step
- Multiple number of operations in **loops** by the number of repeats.
	- Watch out for nested loops!
- **Function calls** add overheads, depending on the number of parameters

![[Searching, Complexity and Associative Arrays.png]]

So applying these rules gets is a total count of operations, $f(N)$, e.g.
$$f(N) = 2N^{2} + 254N + 9$$
- This is an approximation. The exponents and non-linear terms make all the difference.

However many algorithms are data-dependent, and their runtimes are not just dependent on $N$.
## Measures of Complexity 
- **Worse case**: *Maximum* number of steps require to complete algorithm 
- **Best case**: *Minimum* number of steps require to complete algorithm
- **Average case**: *Average* number of steps require to complete algorithm
## Associative Arrays
Also referred to as dictionaries, maps or symbol tables, these are an abstract data type used to store (key, value) pairs.
- Keys are used to access associated values, as indices are used to access items in an array 
$$\{ (\text{key}_0, \text{value}_{0),}(\text{key}_1, \text{value}_{1)}, \dots, (\text{key}_n, \text{value}_n) \}$$
### Operations
- **Constructor** – create a new associative array  
- **Destructor** – delete a associative array  
- **Insert** – insert a (key, value) pair  
- **Search** – search for the value paired with a given key  
- **Remove** – remove a (key, value) pair  
### Library Metaphor
In a library, should record who has borrowed each book currently on loan  
- Associative array could be used to store the name of the person who has borrowed each book  
- Where the person who has borrowed a given book (value) could be accessed using the book title (key)
### Hash Table
These are possible implementations of the associative array abstract data type. They used a *many-to-one* function for determining an array index from the key, called a **hash function**. Different keys can produce the same index. The size of the hash table is typically much smaller than the number of possible keys.