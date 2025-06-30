
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






