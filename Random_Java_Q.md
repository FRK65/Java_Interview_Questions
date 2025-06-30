
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







