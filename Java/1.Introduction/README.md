<div id="top"></div>

# Introduction

<details>

<summary>Table of contents</summary>

- [JDK Architecture](#jdk-structure)
- [Compilation Flow](#compilation-flow)
- [Reading Input from Keyboard](#reading-input-from-keyboard)
- [Common CMD Commands](#common-cmd-commands)
- [JVM Architecture](#jvm-architecture)
- [Reference Types](#reference-types)
- [OOP Concepts](#oops-concepts)
- [Abstract Classes](#abstract-classes)
- [Interfaces in Java](#interfaces-in-java)

</details>

## JDK Architecture

<table>
    <tr>
        <th>JDK Architecture</th>
        <th>Representation</th>
    </tr>
    <tr>
        <td>
            JDK (Development + tools)
             [-> [JRE(Java Class Library ) -> JVM(Java Virtual Machine)]]
        </td>
        <td>
            <img src="https://github.com/user-attachments/assets/78b59b0f-cfae-4454-a918-79c50274472a" width="100%" title="JDK Architecture"/>
        </td>
    </tr>
</table>

<hr/>

## Compilation Flow

```
First.java ----> Java c (Compiler) (from jdk) ---> First.class (byte code)
```

<hr/>

## Reading Input from Keyboard
```
  import java.lang.*;   #default package
  import java.util.*;   # for scanner class

  Scanner sc = new Scanner(System.in); // We provide input stream as param - System.in

  nextInt()
  nextFloat()
  nextDouble()
  next()
  nextLine()

  useRadix()
```

<hr/>

## Common CMD Commands

```
javac file_name.java  #to compile
java file_name #to execute
javap java.util.Scanner # to get all the methods in the specified package
```
<hr/>

## JVM Architecture

-> Memory
  - **Heap** - where objects are created (dynamic)
  - **stack** - where local variables and references are created
  - **code section** - contains the code (class Loader loads the code, - **Interpreter/JIT** - just in time compilation will interpret the code)

<hr/>

## Reference Types

- parent reference, child reference
- Reference Type decides which variables are accessible.
- Object Type decides which methods are executed at runtime (polymorphism).
- Variables are shadowed, methods are overridden.

<hr/>

## OOP Concepts

- **abstraction**
- **encapsulation**
- **inheritance** : single, multilevel, hierarchical, multiple(through interface), hybrid
- **polymorphism** : static compile time (method overloading) , dynamic run time (method overriding)

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

## Abstract Classes

- concrete class -> general class ex: class Parent {}
- abstract class - uses abstract keyword ex: abstract class Parent {}
- we cannot create an instance(object) of abstract class
- class that extends (inherits) abstract class will also be abstract 
- class to overcome abstract class then every method should be override
- abstract method - method which is not having body (undefined method)
    ex: abstract void meth2();
- abstract class - class that having atleast one abstract method (that means class is also not completely defined)

- abstract class set some standards like ex:
    
```
abstract class Hospital {
  abstract void emergency();
  abstract void appointment();
  abstract void admit();
  abstract void billing();
  ...
} 

class MyHospital extends Hospital {
  MyHospital() {}
  void emergency() {}
  void appointment() {}
  ...
}

Hospital h = new MyHospital();
// we make sure MyHospital only follow the standards that are set by Hospital as it can access the methods only defined in Hospital
```

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

## Interfaces in Java

- by default every method is abstract 
- classes are extends
- interfaces are implements
- we cannot create object for interface
- In java a class can be exteded only from single class (multiple inheritance is not possible) but in interfances it can implements from so many interfaces
- interface is defined for achieving runtime polymorphism and dynamic method dispatch
- it can have static methods with body

- ex

```
interface Parent1 {
  void meth1();
}

interface Parent2 {
  void meth1();
}
  
class Child1 implements Parent1,Parent2 {
  public void meth1() {
    System.out.println("Child meth2");
  } 
}

public class MyFirst {

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    Child1 p = new Child1();
    p.meth1();
  }
}
```

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

