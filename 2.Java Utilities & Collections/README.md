<div id="top"></div>

# Java Utilities & Collections


<details>
<summary>Table of contents</summary>

- [Common Utility Methods](#common-utility-methods)
- [Java Arrays](#java-arrays)
- [Collections](#collections)
    - [ArrayList](#arraylist)
    - [Vector](#vector)
    - [HashMap](#hashmap)

</details>

## Common Utility Methods

- String Class

```
"0".repeat(9); // Repeats "0" 9 times → "000000000"
```

- Integer Class

```
Integer.toBinaryString(1) // "1" convert integer to binary string 
Integer.parseInt("1101", 2) // 13 binary to decimal
```


## Java Arrays
-   **declaration**
```
int[] ans = new int [5];
int[] ans = {1,3,34,5};
int ans[] = {1,3,34,5};
```

- **static return**
```
return new int[] {1,2,3};
```


## Collections

### ArrayList
-   dynamic array, not synchronized not suitable when multiple threads are accessing it simultaneously

- **declaration**
```
ArrayList<int[]> ans = new ArrayList<int[]>(); we should pass non primitive data type
ArrayList<Integer> al = new ArrayList<>(10); we added 10 as capacity
ArrayList <Integer> al2 = new ArrayList<>(Arrays.asList(1,2,3));
```

- **methods**
<table border="1" cellspacing="0" cellpadding="8">
  <thead>
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>add(val)</td>
      <td>Adds element to end of list</td>
      <td>al.add(10);</td>
    </tr>
    <tr>
      <td>add(index, val)</td>
      <td>Inserts element at specified index</td>
      <td>al.add(1, 20);</td>
    </tr>
    <tr>
      <td>get(index)</td>
      <td>Returns element at index</td>
      <td>al.get(0);</td>
    </tr>
    <tr>
      <td>set(index, val)</td>
      <td>Updates element at index</td>
      <td>al.set(0, 99);</td>
    </tr>
    <tr>
      <td>remove(index)</td>
      <td>Removes element at index</td>
      <td>al.remove(2);</td>
    </tr>
    <tr>
      <td>contains(val)</td>
      <td>Checks if list contains element</td>
      <td>al.contains(50);</td>
    </tr>
    <tr>
      <td>size()</td>
      <td>Returns number of elements</td>
      <td>al.size();</td>
    </tr>
    <tr>
      <td>clear()</td>
      <td>Removes all elements</td>
      <td>al.clear();</td>
    </tr>
    <tr>
      <td>toArray()</td>
      <td>Converts to array</td>
      <td>al.toArray();</td>
    </tr>
    <tr>
      <td>isEmpty()</td>
      <td>Checks if list is empty</td>
      <td>al.isEmpty();</td>
    </tr>
    <tr>
      <td>indexOf(val)</td>
      <td>Returns index of first occurrence</td>
      <td>al.indexOf(99);</td>
    </tr>
    <tr>
      <td>lastIndexOf(val)</td>
      <td>Returns index of last occurrence</td>
      <td>al.lastIndexOf(99);</td>
    </tr>
  </tbody>
</table>


- **Complexity of Java ArrayList**
<table>
    <tr>
        <th>Operation</th>
        <th>Time Complexity</th>
        <th>Space Complexity</th>
    </tr>
    <tr>
        <td>Inserting Element in ArrayList</td>
        <td>O(1)</td>
        <td>O(N)</td>
    </tr>
    <tr>
        <td>Removing Element from ArrayList</td>
        <td>O(N)</td>
        <td>O(1)</td>
    </tr>
    <tr>
        <td>Traversing Elements in ArrayList</td>
        <td>O(N)</td>
        <td>O(N)</td>
    </tr>
    <tr>
        <td>Replacing Elements in ArrayList</td>
        <td>O(1)</td>
        <td>O(1)</td>
    </tr>
</table>

<p align="right">(<a href="#top">back to top</a>)</p>


### Vector
-   synchronized, thread-safe, but slower than ArrayList

-   **declaration**
```
Vector<Integer> v = new Vector<Integer>();
```

- **Methods**
<h3>📘 Vector – Useful Methods</h3>

<table border="1" cellspacing="0" cellpadding="6">
  <thead>
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Code Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>add(val)</code></td>
      <td>Adds element to end</td>
      <td><code>v.add(10);</code></td>
    </tr>
    <tr>
      <td><code>add(index, val)</code></td>
      <td>Inserts element at index</td>
      <td><code>v.add(1, 20);</code></td>
    </tr>
    <tr>
      <td><code>get(index)</code></td>
      <td>Gets element at index</td>
      <td><code>v.get(0);</code></td>
    </tr>
    <tr>
      <td><code>set(index, val)</code></td>
      <td>Updates element at index</td>
      <td><code>v.set(0, 50);</code></td>
    </tr>
    <tr>
      <td><code>remove(index)</code></td>
      <td>Removes element at index</td>
      <td><code>v.remove(2);</code></td>
    </tr>
    <tr>
      <td><code>size()</code></td>
      <td>Returns number of elements</td>
      <td><code>int n = v.size();</code></td>
    </tr>
    <tr>
      <td><code>contains(val)</code></td>
      <td>Checks if value exists</td>
      <td><code>v.contains(100);</code></td>
    </tr>
    <tr>
      <td><code>clear()</code></td>
      <td>Removes all elements</td>
      <td><code>v.clear();</code></td>
    </tr>
    <tr>
      <td><code>addAll(Collection)</code></td>
      <td>Adds all elements from another collection</td>
      <td><code>v.addAll(list);</code></td>
    </tr>
    <tr>
      <td><code>elementAt(index)</code></td>
      <td>Gets element at index (legacy method)</td>
      <td><code>v.elementAt(0);</code></td>
    </tr>
    <tr>
      <td><code>firstElement()</code></td>
      <td>Returns first element</td>
      <td><code>v.firstElement();</code></td>
    </tr>
    <tr>
      <td><code>lastElement()</code></td>
      <td>Returns last element</td>
      <td><code>v.lastElement();</code></td>
    </tr>
  </tbody>
</table>

<p align="right">(<a href="#top">back to top</a>)</p>


### HashMap
- A HashMap is a data structure that stores key-value pairs.

- **declaration**
```
HashMap<Integer,Integer> store = new HashMap<>();
```

- **methods**
<table border="1" cellspacing="0" cellpadding="8">
  <thead>
    <tr>
      <th>Method</th>
      <th>Description</th>
      <th>Example Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>put(key, value)</td>
      <td>Inserts or updates a key-value pair</td>
      <td>map.put(1, 100);</td>
    </tr>
    <tr>
      <td>get(key)</td>
      <td>Returns the value for the key, or null if not found</td>
      <td>map.get(1);</td>
    </tr>
    <tr>
      <td>containsKey(key)</td>
      <td>Checks if the map contains the key</td>
      <td>map.containsKey(1);</td>
    </tr>
    <tr>
      <td>remove(key)</td>
      <td>Removes key-value pair for the given key</td>
      <td>map.remove(1);</td>
    </tr>
    <tr>
      <td>size()</td>
      <td>Returns the number of key-value pairs</td>
      <td>map.size();</td>
    </tr>
    <tr>
      <td>clear()</td>
      <td>Removes all mappings</td>
      <td>map.clear();</td>
    </tr>
    <tr>
      <td>isEmpty()</td>
      <td>Checks if map is empty</td>
      <td>map.isEmpty();</td>
    </tr>
    <tr>
      <td>keySet()</td>
      <td>Returns a Set view of the keys</td>
      <td>map.keySet();</td>
    </tr>
    <tr>
      <td>values()</td>
      <td>Returns a Collection view of values</td>
      <td>map.values();</td>
    </tr>
    <tr>
      <td>entrySet()</td>
      <td>Returns a Set of key-value pairs</td>
      <td>map.entrySet();</td>
    </tr>
    <tr>
      <td>for-each loop</td>
      <td>Iterate over entries</td>
      <td>
        for (Map.Entry&lt;Integer, Integer&gt; e : map.entrySet()) {<br>
        &nbsp;&nbsp;// use e.getKey(), e.getValue()<br>
        }
      </td>
    </tr>
  </tbody>
</table>


