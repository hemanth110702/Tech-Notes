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

- Math Class

```
Math.max(1, 2) // 2
Math.floor()
Math.ceil()
```


## Java Arrays
-   **Declaration**
```
int[] ans = new int [5];
int[] ans = {1,3,34,5};
int ans[] = {1,3,34,5};
```

- **Static return**
```
return new int[] {1,2,3};
```

- **Methods**
<table border="1" cellspacing="0" cellpadding="8">
  <thead>
    <tr>
      <th>Method / Feature</th>
      <th>Description</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>array.length</code></td>
      <td>Returns size of array</td>
      <td><code>arr.length</code></td>
    </tr>
    <tr>
      <td><code>Arrays.sort(arr)</code></td>
      <td>Sorts array in ascending order</td>
      <td><code>Arrays.sort(arr)</code></td>
    </tr>
    <tr>
      <td><code>Arrays.equals(arr1, arr2)</code></td>
      <td>Checks if two arrays are equal</td>
      <td><code>Arrays.equals(a, b)</code></td>
    </tr>
    <tr>
      <td><code>Arrays.toString(arr)</code></td>
      <td>Converts array to string</td>
      <td><code>System.out.println(Arrays.toString(arr))</code></td>
    </tr>
    <tr>
      <td><code>Arrays.stream(arr)</code></td>
      <td>Streams array for functional ops (Java 8+)</td>
      <td><code>Arrays.stream(arr).sum()</code></td>
    </tr>
  </tbody>
</table>

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

## Collections

## ArrayList
-   dynamic array, not synchronized not suitable when multiple threads are accessing it simultaneously

- **Declaration**
```
ArrayList<int[]> ans = new ArrayList<int[]>(); we should pass non primitive data type
ArrayList<Integer> al = new ArrayList<>(10); we added 10 as capacity
ArrayList <Integer> al2 = new ArrayList<>(Arrays.asList(1,2,3));
```

- **Methods**
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
      <td><code>add(val)/code></td>
      <td>Adds element to end of list</td>
      <td><code>al.add(10);</code></td>
    </tr>
    <tr>
      <td><code>add(index, val)</code></td>
      <td>Inserts element at specified index</td>
      <td><code>al.add(1, 20);</code></td>
    </tr>
    <tr>
      <td><code>get(index)/code></td>
      <td>Returns element at index</td>
      <td><code>al.get(0);</code></td>
    </tr>
    <tr>
      <td><code>set(index, val)</code></td>
      <td>Updates element at index</td>
      <td><code>al.set(0, 99);</code></td>
    </tr>
    <tr>
      <td><code>remove(index)</code></td>
      <td>Removes element at index</td>
      <td><code>al.remove(2);</code></td>
    </tr>
    <tr>
      <td><code>contains(val)</code></td>
      <td>Checks if list contains element</td>
      <td><code>al.contains(50);</code></td>
    </tr>
    <tr>
      <td><code>size()/code></td>
      <td>Returns number of elements</td>
      <td><code>al.size();</code></td>
    </tr>
    <tr>
      <td><code>clear()</code></td>
      <td>Removes all elements</td>
      <td><code>al.clear();</code></td>
    </tr>
    <tr>
      <td><code>toArray()</code></td>
      <td>Converts to array</td>
      <td><code>al.toArray();</code></td>
    </tr>
    <tr>
      <td><code>isEmpty()</code></td>
      <td>Checks if list is empty</td>
      <td><code>al.isEmpty();</code></td>
    </tr>
    <tr>
      <td><code>indexOf(val)/code></td>
      <td>Returns index of first occurrence</td>
      <td><code>al.indexOf(99);</code></td>
    </tr>
    <tr>
      <td><code>lastIndexOf(val)/code></td>
      <td>Returns index of last occurrence</td>
      <td><code>al.lastIndexOf(99);</code></td>
    </tr>
    <tr>
      <td><code>addAll(Arrays.asList(arr)) <br> addAll(list)</code></td>
      <td>Adds all elements of array to an ArrayList</td>
      <td><code>ArrayList<Integer> list.addAll(Arrays.asList(arr)); <br> list.addAll(list2); </code></td>
    </tr>
    <tr>
      <td><code>al.stream().mapToInt(i -> i).toArray()</code></td>
      <td>Converts ArrayList <Integer> to int[] using streams</td>
      <td><code>int[] arr = al.stream().mapToInt(i -> i).toArray();</code></td>
  </tr>
    <tr>
      <td><code>Collections.reverse(list_name)</code></td>
      <td>reverses the list</td>
      <td><code>Collections.reverse(list);</code></td>
  </tr>
  </tbody>
</table>

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

## Vector
-   synchronized, thread-safe, but slower than ArrayList

-   **Declaration**
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

<hr/>


## HashMap
- A HashMap is a data structure that stores key-value pairs.

- **Declaration**
```
HashMap<Integer,Integer> store = new HashMap<>();
```

- **Methods**
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
      <td><code>put(key, value)</code></td>
      <td>Inserts or updates a key-value pair</td>
      <td><code>map.put(1, 100);</code></td>
    </tr>
    <tr>
      <td><code>get(key)/code></td>
      <td>Returns the value for the key, or null if not found</td>
      <td><code>map.get(1);</code></td>
    </tr>
    <tr>
      <td><code>containsKey(key)/code></td>
      <td>Checks if the map contains the key</td>
      <td><code>map.containsKey(1);</code></td>
    </tr>
    <tr>
      <td><code>remove(key)</code></td>
      <td>Removes key-value pair for the given key</td>
      <td><code>map.remove(1);</code></td>
    </tr>
    <tr>
      <td><code>size()/code></td>
      <td>Returns the number of key-value pairs</td>
      <td><code>map.size();</code></td>
    </tr>
    <tr>
      <td><code>clear()</code></td>
      <td>Removes all mappings</td>
      <td><code>map.clear();</code></td>
    </tr>
    <tr>
      <td><code>isEmpty()</code></td>
      <td>Checks if map is empty</td>
      <td><code>map.isEmpty();</code></td>
    </tr>
    <tr>
      <td><code>keySet()/code></td>
      <td>Returns a Set view of the keys</td>
      <td><code>map.keySet();</code></td>
    </tr>
    <tr>
      <td><code>values()/code></td>
      <td>Returns a Collection view of values</td>
      <td><code>map.values();</code></td>
    </tr>
    <tr>
      <td><code>entrySet()/code></td>
      <td>Returns a Set of key-value pairs</td>
      <td><code>map.entrySet();</code></td>
    </tr>
    <tr>
      <td><code>for-each loop</code></td>
      <td>Iterate over entries</td>
      <td><code>
        for (Map.Entry&lt;Integer, Integer&gt; e : map.entrySet()) {<br>
        &nbsp;&nbsp;// use e.getKey(), e.getValue()<br>
        }</code>
      </td>
    </tr>
  </tbody>
</table>

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>
