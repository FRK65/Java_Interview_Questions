
# 1. SOLID Principle names in Java.

**SOLID principles** by name only:

1. **S** – Single Responsibility Principle
2. **O** – Open/Closed Principle
3. **L** – Liskov Substitution Principle
4. **I** – Interface Segregation Principle
5. **D** – Dependency Inversion Principle
---

# 2. What is Stream in Java. 

- A Stream is an abstraction that represents a sequence of elements supporting functional-style operations to process data.
- A Stream in Java is a way to process a bunch of data step by step, using clean and simple code.
- A stream is not a collection – it just processes data from a collection.
- It does not change the original data.
- Operations can be chained together.
- Can run in parallel for better performance.
- It Introduced in Java 8, it allows for declarative, efficient, and parallel data manipulation (like filtering, mapping, and reducing) without modifying the source.
---

# 3. What is a Lambda in Java?

- A lambda in Java is a quick and clean way to pass behavior (code) as data, often used to simplify code that uses interfaces with one method
- A Lambda Expression in Java is a short way to write anonymous functions (functions without a name) that can be passed around as data.
- It introduced in java 8 has syntex as:  **(parameters) -> expression**
-  When to Use : It Mainly used with **functional interfaces** (interfaces with only one method)
-  Used in **stream, event handling, sorting and filtering**

Example without Lambda
```java
Runnable r = new Runnable() {  public void run() {  System.out.println("Hello")  }};
// Here we created a Runnable Object and passed a function in it.
```
Example with Lambda 
```java
Runnable r = () -> System.out.println("Hello");

```
---

# 4. What is Optional in Java 8?

- **`Optional` is a class** in Java 8 (`java.util.Optional`).
- It is used to **represent a value that may or may not be present**.
- It Helps **avoid `NullPointerException`** by explicitly handling possible absence of a value.
-  When is it used?

1. To **wrap return values** that might be `null`.
2. To **make your code more readable and safer** by forcing you to handle missing values explicitly instead of risking null checks everywhere.


### Key Methods of `Optional`:

| Method                | Description                                             |
| --------------------- | ------------------------------------------------------- |
| `empty()`             | Returns an empty `Optional` (no value)                  |
| `of(T value)`         | Returns an `Optional` with the specified non-null value |
| `ofNullable(T value)` | Returns an `Optional` with the value, or empty if null  |
| `isPresent()`         | Checks if a value is present                            |
| `get()`               | Gets the value if present, throws exception if empty    |
| `orElse(T other)`     | Returns value if present, otherwise returns `other`     |
| `ifPresent(Consumer)` | Executes action if value is present                     |

simple eaxmple :

```java
Optional<String> name = Optional.ofNullable(getName());

if (name.isPresent()) {
    System.out.println(name.get());
} else {
    System.out.println("Name not found");
}
```
Or using a cleaner approach:

```java
name.ifPresent(System.out::println);
```
---

# 5. What is a Functional Interface in Java?

- A **Functional Interface** is an interface that has **exactly one abstract method**. It can have multiple default or static methods, but only one abstract method.
- Why is it important?

1. Functional interfaces are the **target types for lambda expressions and method references** in Java.
2. They allow you to **pass behavior (code) as an argument** in a clean and concise way.

Example of Functional Interface:

```java
@FunctionalInterface
public interface MeraFunctionalInterface {
    void doSomething();
}
```
- The `@FunctionalInterface` annotation is optional but helps to enforce the rule of having exactly one abstract method.


**Common Built-in Functional Interfaces in Java:**

| Interface       | Method              | Purpose                                 |
| --------------- | ------------------- | --------------------------------------- |
| `Runnable`      | `void run()`        | Represents a task with no arguments     |
| `Callable<V>`   | `V call()`          | Represents a task that returns a result |
| `Supplier<T>`   | `T get()`           | Supplies a value                        |
| `Consumer<T>`   | `void accept(T t)`  | Consumes a value, returns nothing       |
| `Function<T,R>` | `R apply(T t)`      | Takes input and returns a result        |
| `Predicate<T>`  | `boolean test(T t)` | Tests a condition and returns boolean   |



**Simple Example using `Runnable`:**

Without Lambda:

```java
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Running");
    }
};
```

With Lambda:

```java
Runnable r = () -> System.out.println("Running");
```
---

# 6. What is Multithreading in Java?
- Multithreading in Java means running multiple threads simultaneously to make programs faster and more efficient.
- Multithreading is a feature in Java that allows multiple threads (smallest units of a process) to run concurrently within a single program.
- Why we use : To perform multiple tasks at the same time, Improves the performance and responsiveness of applications.
- Each thread runs independently but shares the same memory space.
- Threads can be created by:
1. Extending the Thread class, or
2. Implementing the Runnable interface
Ex. Runnable
```java
class Car implements Runnable {
    public void run() {
        System.out.println("Thread is running");
    }
}

In main class :
        Thread t = new Thread(new Car());
        t.start();  // starts the new thread
  
}
```   
---

# 7. what is synchronized and asynchronized means

🔒 **Synchronized**

* **Synchronized** means **only one thread can access a block of code or method at a time**.
* It is used to **prevent race conditions** when multiple threads try to change shared data.
* Ensures **thread safety** by **locking** the resource while a thread is using it.


```java
public synchronized void increment() {
    count++;
}
```
**ASynchronized**

* **Asynchronized** means tasks or methods run **independently and concurrently**, without waiting for others.
* No locking is involved; multiple threads can access code simultaneously.
* Can lead to **race conditions** if shared data isn’t handled carefully.
---

# 8. What is volatile in Java?
- In Java, the volatile keyword is used to mark a variable so that every read and write operation happens directly in main memory, not in a thread's local cache.
- volatile in Java ensures that changes to a variable are always visible to all threads. It’s a lightweight way to ensure visibility in multithreaded code.
- Why needed : In multithreading, threads may cache variables, that leading to stale values.
- volatile ensures visibility: when one thread updates a variable, other threads immediately see the change.
- It Guarantees visibility, not atomicity
- With volatile Caching is disabled for that variable and Threads always **read the latest value**

Ex. 
```java
public class Example {

private volatile boolean running = true;

    public void run() {
        while (running) {
            // do some work
        }
    }

    public void stop() {
        running = false;
    }
}
```
Without volatile, another thread might never see the updated false value and keep running the loop forever.

# 9. What is ExecutorService in Java?

`ExecutorService` is a **powerful tool for managing multiple threads** in Java, making concurrent programming easier, more scalable, and less error-prone than using raw threads.

- **`ExecutorService`** is an **interface** in Java (from `java.util.concurrent`) that provides a **high-level way to manage and control threads**.
- Why use `ExecutorService` : Instead of manually creating and starting threads with `new Thread()` ExecutorService handle this for us.
- `ExecutorService` does below things :
1. Handles **thread creation**, **scheduling**, and **pooling**
2. Allows you to **submit tasks** and get **results** or **exceptions**
3. Helps manage **concurrency efficiently**

- 🔑 Key Features:

1. Executes **`Runnable` and `Callable`** tasks
2. Returns **`Future`** objects to track task results
3. Supports shutting down and controlling the thread pool


🧪 Simple Example:

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

executor.submit(() -> {
    System.out.println("Task running in thread: " + Thread.currentThread().getName());
});

executor.shutdown(); // Always shut down the executor
```

🛠️ Common Methods:

| Method               | Description                                                |
| -------------------- | ---------------------------------------------------------- |
| `submit(task)`       | Submits a task (Runnable or Callable)                      |
| `shutdown()`         | Gracefully shuts down the executor                         |
| `shutdownNow()`      | Attempts to stop all running tasks                         |
| `invokeAll()`        | Executes a list of tasks and waits for all                 |
| `invokeAny()`        | Executes a list, returns result of one that finishes first |
| `awaitTermination()` | Waits for tasks to finish after shutdown                   |


🧵 Common Implementations:

```java
Executors.newFixedThreadPool(4);    // Fixed number of threads
Executors.newSingleThreadExecutor(); // One thread only
Executors.newCachedThreadPool();     // Grows as needed, reuses idle threads
```

# 10. How to Design custom exceptions with a short real life example 

Custom exceptions make your code easier to understand, debug, and maintain by clearly naming and handling specific error situations.

Steps :
- Extend the Exception (for checked) or RuntimeException (for unchecked) class.
- Add constructors to pass error messages or causes.
- Optionally, add custom fields or methods.

 🎯 **Scenario**:

We’ll simulate an ATM system that:

* Throws a **checked exception** if someone tries to withdraw without inserting a card.
* Throws an **unchecked exception** if the withdrawal amount is negative.

✅ **1. Custom Exceptions**

```java
// Checked Exception

class CardNotInsertedException extends Exception {

    public CardNotInsertedException(String message) {
        super(message);
    }
}

// Unchecked Exception
class InvalidAmountException extends RuntimeException {

    public InvalidAmountException(String message) {
        super(message);
    }
}
```

✅ **2. ATM Class Using Both**

```java
public class ATM {

    private boolean cardInserted = false;
    private double balance = 1000;

    public void insertCard() {
        cardInserted = true;
        System.out.println("Card inserted.");
    }

    public void withdraw(double amount) throws CardNotInsertedException {
        if (!cardInserted) {
            throw new CardNotInsertedException("Please insert your card before withdrawing.");
        }

        if (amount <= 0) {
            throw new InvalidAmountException("Withdrawal amount must be positive.");
        }

        if (amount > balance) {
            System.out.println("Insufficient funds.");
            return;
        }

        balance -= amount;
        System.out.println("Withdrawal successful. Remaining balance: $" + balance);
    }
}
```

✅ 3. **Main Method (Using the ATM)**

```java
public class Main {
    public static void main(String[] args) {

      ATM atm = new ATM();

        try {
            // Will throw checked exception (card not inserted)
            atm.withdraw(100);
        } catch (CardNotInsertedException e) {
            System.out.println("Checked Exception: " + e.getMessage());
        }

        atm.insertCard();

        // Will throw unchecked exception (invalid amount)
        atm.withdraw(-50);  // No try-catch needed, but may crash if not handled
    }
}
```

✅ **Summary Table**

| Exception Type | Exception Class            | When It Happens                            | Needs Handling? |
| -------------- | -------------------------- | ------------------------------------------ | --------------- |
| **Checked**    | `CardNotInsertedException` | Withdraw attempted before card is inserted | ✅ Yes           |
| **Unchecked**  | `InvalidAmountException`   | Withdrawal amount is zero or negative      | ❌ Optional      |

---

# 11. What is Stack Memory ?

* **Stack Memory** = Your **to-do list** (each method call is a task on the list).
* **Heap Memory** = A **storage room** where you put things (objects) you might need across multiple tasks.

In Java, memory is mainly divided into two important areas Stack and Heap :

🗂️ **Stack Memory**

* Used for: **Method execution and local variables**
* Every time a method is called, a **"stack frame"** is created.
* When the method finishes, the stack frame is removed.
* **Faster** access and **automatically managed**.
* Memory is **limited**, but very efficient.

 ✅ Characteristics:

* Stores **local variables** and **method calls**.
* **Last-In, First-Out (LIFO)** structure.
* Automatically cleaned when methods return.
* Each thread has its own **stack** (it’s thread-safe).

 📌 Example:

```java
public void add() {
    int a = 5; // 'a' stored in stack
}
```
---
# 12. What is **Heap Memory**

** 🧳 Heap Memory**

* Used for: **Objects and instance variables**
* Objects are created using `new` are stored in heap.
* Heap memory is **shared across threads**.
* **Garbage Collector** cleans unused objects.

✅ Characteristics:

* Stores all **objects** created via `new`.
* **Slower** than stack due to more complex management.
* **Shared** among all threads.

📌 Example:

```java
Person p = new Person(); // 'p' is a reference in the stack, object is in the heap
```

🔍 Visual Summary:

| Feature      | Stack                         | Heap                              |
| ------------ | ----------------------------- | --------------------------------- |
| Stores       | Local variables, method calls | Objects, instance variables       |
| Access Speed | Fast                          | Slower                            |
| Size         | Small                         | Large                             |
| Scope        | Per thread                    | Shared among all threads          |
| Lifetime     | Until method ends             | Until object is garbage collected |
| Managed By   | Java automatically            | Garbage Collector                 |

---

# 13. what is String Constant Pool?

The String Constant Pool is a special memory area inside the Heap where Java stores string literals to save memory and improve performance.
-Instead of creating a new String object every time, Java reuses existing literals from the pool.

**String Constant Pool** = String Intern Pool

✅ Example:

```java
String s1 = "Java";
String s2 = "Java";

System.out.println(s1 == s2); // true
```

> ✅ Both `s1` and `s2` refer to the **same object** in the **String pool**, not two separate ones.



🔧 But when you use `new String()`:

```java
String s3 = new String("Java");
System.out.println(s1 == s3); // false
```

> ❌ `s3` refers to a **new object** in the heap, even though the value is the same.


✅ Why is this useful?

* **Reduces memory usage** by reusing strings.
* **Improves performance** for string comparison using `==`.

🔁 You can manually add to the pool:

```java
String s4 = new String("Java").intern();
System.out.println(s1 == s4); // true
```

 ✅ Summary:

| Concept                  | Location    | Purpose                               |
| ------------------------ | ----------- | ------------------------------------- |
| **String Constant Pool** | Inside Heap | Stores unique string literals         |
| `==` works with literals | Yes         | Because they point to the same object |

---

# 14. Difference between == and equals() 

🗒️ Tip:

Always use `.equals()` when comparing **String content**.


🔍 `==` vs `.equals()` in Java

| Comparison Type | `==` operator                                        | `.equals()` method                                  |
| --------------- | ---------------------------------------------------- | --------------------------------------------------- |
| Compares        | **Memory reference (address)**                       | **Object content (value/data)**                     |
| Type            | Operator                                             | Method from `Object` class (overridden in `String`) |
| Use Case        | Check if two references point to the **same object** | Check if two objects have the **same value**        |



💡 Concept with **Heap** and **String Constant Pool**

Example 1: Using String Literals (String Constant Pool)

```java
String a = "Java";
String b = "Java";

System.out.println(a == b);        // true ✅ (same object in pool)
System.out.println(a.equals(b));   // true ✅ (same content)
```

✅ Both `"Java"` literals point to the **same memory location** in the **String Constant Pool** inside the **Heap**, so `==` is `true`.



Example 2: Using `new String()` (Heap objects)

```java
String x = new String("Frank");
String y = new String("Frank");

System.out.println(x == y);        // false ❌ (different objects in heap)
System.out.println(x.equals(y));   // true ✅ (same content)
```

🚫 `==` is `false` because `x` and `y` are **two different objects** in the **heap**, even though their values are the same.

✅ `.equals()` is `true` because it compares the **contents** of the strings.


Example 3: Mixing new and literal

```java
String p = "Java";
String q = new String("Java");

System.out.println(p == q);        // false ❌
System.out.println(p.equals(q));   // true ✅
```

🧠 Summary with Memory Concepts:

| Case                                       | Stored In    | `==` result | `.equals()` result | Why?                          |
| ------------------------------------------ | ------------ | ----------- | ------------------ | ----------------------------- |
| `"Java" == "Java"`                         | String Pool  | `true`      | `true`             | Same pool object              |
| `new String("Java") == new String("Java")` | Heap         | `false`     | `true`             | Different objects, same value |
| `"Java" == new String("Java")`             | Pool vs Heap | `false`     | `true`             | Different memory locations    |

---

# 15. what is Garbage Collection

**Garbage Collection** is the process by which **Java automatically frees memory** by removing objects that are **no longer reachable or used** by the program.

✅ Summary:

| Question                  | Answer                                                                     |
| ------------------------- | -------------------------------------------------------------------------- |
| What is GC?               | Automatic memory cleanup of unused objects                                 |
| Who invokes GC?           | JVM (automatic), programmer can request via `System.gc()` but no guarantee |
| When is GC invoked?       | When JVM detects low memory or on request                                  |
| What memory is collected? | Heap memory only                                                           |
| Can programmers force GC? | Can request but no guarantee; no direct control                            |
| Popular GC algorithms     | Serial, Parallel, CMS, G1, ZGC, Shenandoah                                 |


- When and Who Invokes Garbage Collection?

* **Invoked automatically** by the **JVM (Java Virtual Machine)** when it detects that memory is low or as needed.
* You **cannot control exactly when GC runs**, but you can **request** it by calling `System.gc()` (just a request, not guaranteed).
* **Programmers do NOT usually call GC directly.**

- 🧠 Which Memory Does Garbage Collector Clean?

* GC primarily collects objects in the **Heap memory** (where Java objects live).
* It **does NOT clean Stack memory**, which stores local variables and method calls.

🛠️ How to request Garbage Collection?

```java
System.gc();  // Suggest JVM to run GC, but it’s not guaranteed to run immediately
```

🔥 Famous and Latest Garbage Collection Algorithms in Java:

| Algorithm Name                  | Description                                                        | Java Version Introduced / Popular In               |
| ------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------- |
| **Serial GC**                   | Single-threaded GC, good for small apps                            | Early JVMs, simple but stops all threads during GC |
| **Parallel GC**                 | Multi-threaded GC, good for multi-core                             | Java 5+, default in many JDK versions              |
| **CMS (Concurrent Mark Sweep)** | Minimizes pause times by running concurrently                      | Java 5 - Java 8                                    |
| **G1 (Garbage-First GC)**       | Divides heap into regions, works concurrently, reduces pause times | Java 7+, became default in Java 9+                 |
| **ZGC (Z Garbage Collector)**   | Low-latency GC, designed for very large heaps                      | Java 11+, aims for sub-millisecond pauses          |
| **Shenandoah GC**               | Low-pause-time GC, similar to ZGC                                  | Java 12+, also targets large heaps and low pause   |

---

# 16. What is LocalDate and DayOfWeek ?

**LocalDate** is a class in the java.time package.
- It represents a date only (no time or timezone), like 2025-06-30.
- It is a final class, so it cannot be extended.
- Implements the Temporal, ChronoLocalDate, and Comparable interfaces.
- Use : When you only need the year, month, and day (e.g., birthdays, holidays, deadlines).
- For date calculations: adding/subtracting days, comparing dates, etc.
Ex :

```java
    import java.time.LocalDate;

    LocalDate today = LocalDate.now();
    System.out.println(today); // 25-06-30
    System.out.println(today.getDayOfWeek()); // Monday

    LocalDate date = LocalDate.of(1947,8,15);
    System.out.println(date);
    System.out.println(date.getDayOfWeek()); // Friday
    
```

**DayOfWeek** : DayOfWeek is an enum in java.time package.
- It represents the seven days of the week: MONDAY, TUESDAY, ..., SUNDAY
- It is an enum, not a class or interface.
- Each constant (MONDAY, TUESDAY, etc.) has an associated numeric value (1 to 7).
- When you want to find out the day of the week for a given date.
```java

LocalDate date = LocalDate.of(2025, 6, 30);

DayOfWeek myday = date.getDayOfWeek();  // MONDAY

System.out.println(myday);              // MONDAY
System.out.println(myday.getValue());   // 1 (Monday = 1, Sunday = 7)

```
---

# 17. What is Memory Leak in java ?
A **memory leak** in Java happens when the program allocates memory for objects but doesn’t release it when the objects are no longer needed. This prevents the garbage collector from cleaning them up, leading to increased memory usage over time.

Common causes include:

* Keeping unnecessary objects in collections.
* Not unregistering event listeners or callbacks.
* Holding objects in static fields.
* Failing to stop threads properly.

This can cause your application to slow down, crash, or run out of memory.

---

# 18. How to prevent memory leaks ?

To prevent memory leaks in Java:

1. **Nullify references** when done with objects.
2. **Remove objects** from collections when not needed.
3. **Unregister listeners/callbacks** when finished.
4. Use **WeakReferences** for infrequent or large objects.
5. Avoid **static references** to objects.
6. **Close resources** (files, DB connections) properly.
7. **Monitor memory usage** with profiling tools.

These steps help ensure objects are garbage collected when no longer needed.

# 19. How do you prevent memory leaks caused by event listeners? 
To prevent memory leaks caused by **event listeners** in Java:

1. **Unregister listeners** when they are no longer needed or when the object they are listening to is disposed of.

   ```java
   eventSource.removeListener(myListener);
   ```

2. **Use Weak References** for listeners, so they don’t prevent garbage collection when the listener object is no longer in use.

   ```java
   WeakReference<MyListener> weakListener = new WeakReference<>(myListener);
   ```

3. **Add and remove listeners properly** in lifecycle methods (like `addListener()` in `init()` and `removeListener()` in `dispose()`).

4. **Avoid holding strong references** to listeners in the objects they are attached to (like GUI components), as this will prevent garbage collection.

By unregistering listeners and using weak references, you ensure they don’t keep objects in memory unnecessarily.

---

# 20. What is the purpose of the PhantomReference class in Java?

The PhantomReference class in Java is part of the java.lang.ref package, and its purpose is to provide a way to track objects that are ready for garbage collection but haven't been collected yet. It is the most "advanced" type of reference in Java and is used in scenarios where you need to take action after an object has been garbage collected.

**Purpose**:
`PhantomReference` is used to track objects that are **about to be garbage collected**, allowing you to perform cleanup actions (like releasing resources) **after the object is collected** but before memory is reclaimed.

**Key Points**:

* **Doesn't prevent GC**: Unlike `WeakReference`, it doesn’t keep the object alive.
* **Works with `ReferenceQueue`**: The reference is placed in a `ReferenceQueue` when the object is about to be garbage collected.
* **Used for resource cleanup**: Typically used for managing native resources or memory outside the JVM.

**Use case**:
It's used in scenarios like custom memory management or releasing resources that are tied to objects but not managed by the JVM's garbage collector.

---

# 21. What are the advantages of using enum types over constant variables?

Enums are a more robust and flexible solution than constant variables, offering type safety, better organization, namespace encapsulation, additional functionality, and easier code maintenance.

Advantages of Enums over Constant Variables:
1. Type Safety: Enums ensure only valid values are used, whereas constants don’t.
2. Readability: Enums are more descriptive and easier to understand.
3. Namespace Organization: Enums group related constants, avoiding naming conflicts.
4. Extra Functionality: Enums can have methods and fields, offering more flexibility.
5. Built-in Methods: Enums provide useful methods like values(), valueOf(), and ordinal().
6. Extensibility: Enums are easier to extend if you need to add more values or logic.

In short, enums are safer, more organized, and flexible compared to constant variables.

---

# 22. difference between HashMap and TreeMap in terms of ordering and performance?

In short:

* **`HashMap`**: Unordered, faster for most operations.
* **`TreeMap`**: Ordered, but slower due to sorting.

comparison between **`HashMap`** and **`TreeMap`** in table form:

| Feature              | **`HashMap`**                                          | **`TreeMap`**                                            |
| -------------------- | ------------------------------------------------------ | -------------------------------------------------------- |
| **Ordering**         | No specific order, unordered                           | Sorted by natural ordering or custom comparator          |
| **Time Complexity**  | **`O(1)`** for `put()`, `get()`, `remove()` on average | **`O(log n)`** for `put()`, `get()`, `remove()`          |
| **Data Structure**   | Hash table                                             | Red-Black Tree (Self-balancing BST)                      |
| **Null Keys/Values** | Allows **one null key** and **multiple null values**   | Does not allow **null keys**, but allows **null values** |
| **Performance**      | Faster for most operations (on average)                | Slower due to tree balancing (logarithmic time)          |
| **Use Case**         | When you don’t need ordering, faster lookups           | When you need sorted order of keys                       |

---

# 23. Explain how the Stream.collect() method works with collectors

The `Stream.collect()` method in Java is a **terminal operation** used to transform a stream into a different form, usually a collection like a **List**, **Set**, or **Map**. It takes a **`Collector`** as an argument, which defines how the elements should be accumulated.

**Common Collectors:**

1. **`Collectors.toList()`**: Collects elements into a `List`.
2. **`Collectors.toSet()`**: Collects elements into a `Set`.
3. **`Collectors.toMap()`**: Collects elements into a `Map`.
4. **`Collectors.joining()`**: Concatenates elements into a single string.

 How it Works:

* **`collect()`** accumulates the elements of a stream into a result container, such as a collection or a custom object.
* **`Collector`** defines the **accumulation logic**, and it provides three important components:

  1. **Supplier**: Provides an empty container (e.g., a new list).
  2. **Accumulator**: Adds elements to the container.
  3. **Combiner**: Combines two partial results (used in parallel streams).

### Example:

```java
import java.util.*;
import java.util.stream.*;

public class CollectExample {
    public static void main(String[] args) {

        List<String> words = Arrays.asList("apple", "banana", "cherry", "date");
        
        // Using Collectors.toList() to collect stream into a List

        List<String> collected = words.stream()
                                      .filter(w -> w.startsWith("a"))
                                      .collect(Collectors.toList());
        
        System.out.println(collected);  // Output: [apple]
    }
}
```

# 24. Diffrence between `map()` and `flatMap()` in Java Streams:

Summary:

* **`map()`**: One-to-one transformation.
* **`flatMap()`**: One-to-many transformation with flattening.
  
comparing **`map()`** and **`flatMap()`** in Java Streams:

| **Concept**              | **`map()`**                                       | **`flatMap()`**                                                                      |
| ------------------------ | ------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Purpose**              | Transforms each element into exactly one element. | Transforms each element into a stream of elements, then flattens the streams.        |
| **Function Output**      | A function that returns a single value.           | A function that returns a stream of values.                                          |
| **Result**               | Stream of transformed elements (one-to-one).      | Stream of flattened elements (one-to-many).                                          |
| **Use Case**             | When you need to modify or convert each element.  | When you need to flatten nested collections or generate multiple values per element. |
| **Example**              | `stream.map(String::length)`                      | `stream.flatMap(list -> list.stream())`                                              |
| **Handling Collections** | Each element maps to a single transformed value.  | Each element maps to a stream of values, and those are flattened.                    |
| **Performance**          | Operates on individual elements (simpler).        | Slightly more complex due to flattening.                                             |

---






