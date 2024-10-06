
---

### Exceptions in Java

**Definition:**

- An exception in Java is an event that occurs during the execution of a program, disrupting the normal flow of instructions.
- Exceptions can occur due to various reasons, such as invalid input, resource unavailability, or programming errors.

**Types of Exceptions:**

1. **Checked Exceptions**:
    
    - Checked exceptions are exceptions that the compiler forces you to handle explicitly.
    - They are subclasses of `Exception` but not subclasses of `RuntimeException`.
    - Examples: `IOException`, `SQLException`.
2. **Unchecked Exceptions** (Runtime Exceptions):
    
    - Unchecked exceptions are exceptions that do not need to be handled explicitly by the programmer.
    - They are subclasses of `RuntimeException`.
    - Examples: `NullPointerException`, `ArrayIndexOutOfBoundsException`.

**Handling Exceptions:**

- **Try-Catch Block**:
    
```java
try {
    // Code that may throw an exception
} catch (ExceptionType1 e1) {
    // Handler for ExceptionType1
} catch (ExceptionType2 e2) {
    // Handler for ExceptionType2
} finally {
    // Optional block always executed, regardless of whether an exception occurred
}

```
    
- **Throwing Exceptions**:
    
```java
void method() throws SomeException {
    if (/* condition */) {
        throw new SomeException("Error message");
    }
}

```
- **Finally Block**:
    
    - The `finally` block is used to execute cleanup code that should always run, regardless of whether an exception occurs or not.

**Try-With-Resources (Java 7+):**

- A try-with-resources statement automatically closes resources opened within its parentheses.
- Resources must implement the `AutoCloseable` interface.
- Example:
    
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // Use BufferedReader
} catch (IOException e) {
    // Handle IOException
}

```

**Custom Exceptions:**

- Custom exceptions can be created by extending existing exception classes or the `Exception` class.
- Example:
```java
class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

```

**Best Practices:**

1. Handle exceptions gracefully rather than allowing the program to crash.
2. Use specific exception types whenever possible to provide meaningful error messages and enable targeted error handling.
3. Close resources properly to prevent resource leaks.
4. Log exceptions to aid in debugging and troubleshooting.

**Example:**
```java
public class Main {
    public static void main(String[] args) {
        try {
            int result = divide(10, 0);
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.err.println("Division by zero!");
        }
    }

    static int divide(int dividend, int divisor) {
        if (divisor == 0) {
            throw new ArithmeticException("Division by zero");
        }
        return dividend / divisor;
    }
}

```