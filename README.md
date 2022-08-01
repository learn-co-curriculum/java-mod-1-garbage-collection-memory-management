# Garbage Collection and Memory Management

## Learning Goals

- Understand how Java manages memory
- Introduce the garbage collector

## Memory Management

In Java, objects live in **memory**. When we start the JVM, some memory from the operating system (OS) will be
allocated to the JVM. Once the memory is allocated, we can use that memory to run our Java program. Memory is an
important concept because it helps us create new objects and remove them. 

Think of a sandbox. We can build a castle with the sand inside the sandbox. When we are done, we can destroy the
castle, and it returns that sand used to the rest of the sandbox. Memory in Java works a lot like playing in a sandbox!
We have a finite amount of memory to create objects and when those objects are no longer useful to us, we can return
that memory to create new objects. 

When talking about memory in programming languages, we will often talk about the **stack** and the **heap**. 

### The Stack

The **stack** is where all primitive type variables are stored (think of `int` and `double`) and pointers for all
reference type variables (such as `String`). 

Remember that a **reference** is a strongly typed handle for an object. We can use the reference to access the object's
value in memory. All objects in Java, except for primitive types, are accessed through references. 

### The Heap

The **heap** is where the Java objects live. This is where new objects are created and stored and where they will be
cleaned up. 

Consider the following example:
![memory map](https://curriculum-content.s3.amazonaws.com/java-mod-1/garbage-collection-and-memory-management/Memory-1.png)

Within this example, we have our code sitting in the left block, the stack is in the center block, and the heap is the
right block in this diagram. Let's break up how this program would run and map it to the stack and heap!

- When the program starts, we will enter the `main` method.
- Then we will look at the line that states `int x = 18;`. Since x is a primitive type, the data will be allocated
within the stack.
- The next line we are creating a new `Cat` object called `tom`. Notice that when the program runs this line, it creates
the reference `tom` in the stack and points it to a `Cat` object that lives on the heap.
- The last line within the `main` method is very similar to the line above it. We are creating another `Cat` object but
this time it is being assigned the variable `garfield`. The reference variable, `garfield`, will be placed on the stack
and point to a new `Cat` object on the heap. 

## Garbage Collection

Now that we can see how objects are created within memory in Java, we can look at how that memory is cleaned up!

Java has something called **garbage collection** that will remove objects that are no longer needed. When an object is
no longer useful, the garbage collector will free those objects from memory to make space for new ones that may be
created. This process happens automatically in the background, so us, programmers, do not have to worry too much about
deleting unused objects within their code. Pretty cool, huh? 

Let's look at an example of how the garbage collection works!
![garbage collection eligibility](https://curriculum-content.s3.amazonaws.com/java-mod-1/garbage-collection-and-memory-management/Memory-2.png)

Our `Cat` objects `tom` and `garfield` are back at it to show us how memory is managed! Let's break down the example
above to see what happens with this program.

- When the program starts, we will enter the `main` method.
- Then we will create a new `Cat` object called `tom`. When this line runs, it will create a reference `tom` in the
stack to point to a `Cat` object within the heap.
- Afterwards, we create a new `Cat` object called `garfield`. This will create a reference `garfield` in the stack and
point it to another `Cat` object on the heap space.
- Now we are going to re-assign `garfield` to `tom` so both our references are pointing to the same `Cat` object. Note
that the other `Cat` object no longer has a reference pointing to it. This object is now **eligible for garbage**
**collection**. Since the other cat object is no longer useful to us in the program,

## Resources

- [Learning Java, 5th Edition](https://learning.oreilly.com/library/view/learning-java-5th/9781492056263/ch01.html#learnjava5-CHP-1-SECT-4.3)
- [Head First Java, 3rd Edition](https://learning.oreilly.com/library/view/head-first-java/9781492091646/ch09.html#the_stack_and_the_heap_where_things_live)
