# Java

## Review of basic OOP

### Abstraction

`static` means that it's a class level attribute, meaning that it is one per class and not one per instance of the class

The `this` keyword as a reference provides a reference to the itself as an object

The `this` keyword as a method can be use to invoke matching constructors. For example:

```
private String message;

public Object() {
    this("hello");
}

public Object(String message) {
    this.message = message;
}
```

`this("hello");` is invoking the second constructor!

Similar to `this` as a method, `super()` invokes the constructor of the **parent** class.

You cannot instantiate abstract classes, however you can still make collections of them.

### Interfaces

Interfaces were added to get around the restriction of single inheritance.

For example, In a Task class, you can `implement` the Comparable interface, `overriding` the `compareTo` method. Then you can use a `Collections.sort(tasksList);` and it would know what method to use to compare and sort the classes. On top of that, Task can implement other interfaces if necessary.

### Exceptions

Example of creating your own exception class

```
public class MyException extends Exception {
    public MyException() {
        this("default message");
    }

    public MyException(String message) {
        super(message);
    }
}
```

One constructor that takes a message, and calls `super` to invoke the parent constructor. Also is good to create a default constructor, and you can use `this` to call the other constructor that takes in the message.

checked vs. unchecked exceptions. Problem with checked exceptions, lets say you have a chain of method calls like method A -> calls method B -> C -> D and so on, and method D throws an exception, and you would like to handle the exception in method A, then methods in between have to throw the same exception.

You can't recover from unchecked exceptions.
You can recover from checked exceptions.

## Generics

Example of a generic method

```
public static <T> void swap(Pair<T> pair) {
    T temp = pair.first;
    pair.first = pair.second;
    pair.second = temp;
}
```

The `<T>` syntax says that the method is a generic method.

## Concurrency

### Callables and Futures

The benefit of callables over runnables, is that callables return a value in the form of a `future`. Runnables return void.
