# Advanced-Java-Development

Java course

## Generics

Generics make your code safer and clearer to read. Generics can be useful to provide contrains and flexibilty, depending on how they are used.

For example, you can use them to specify that a list will be contianing only Strings

```

List<String> shapes = new ArrayList<>();

shapes.add("Circle");

```

Here, we can see how we specify that the List will be contianing Strings

You can also use it to provice flexibility

```

//This should work with lists containing any type of object

    static <T> List<T> flattenList(List<List<T>> nestedList) {



        List<T> flattenedList = new ArrayList<>();

        nestedList.forEach(flattenedList::addAll);

        return flattenedList;



    }

```

Here we can see how we use the generic T Type to allow for any type of object to be passed in the method. We could pas a List of Lists of Strings, or Integers for example.

You can also be more specific by using the `extends` key word.

```

private static <T extends Number> List<T> convertArrayToList(T[] array) {

        return Arrays.asList(array);

    }

```

Here the methos will only return Number types like a doble or an int. This is called **Bounded Generics**

There are also "Wildcards"

```

static void checkoutAllItems(List<? extends ClothingItem> clothingItems) {



        for (ClothingItem clothingItem : clothingItems) {

            checkoutItem(clothingItem);

        }



    }



```

This method will take a List of any subtype of clothingItems

## Functional Programming

Lambda or functional interfaces were introduced on Java 8 to allow for writing of concise and neat code.

It's an interface with only one single method.

E.g.

```
@FunctionalInterface
public interface Greeting {
    void printMessage();
}
```

and they can be implemented like this:

```
public class HelloWorldGreeting implements Greeting {
    @Override
    public void printMessage() {
        System.out.println("Hello World");
    }
}
```

This can be shortened by using lambda functions, which are like anonymous functions in JS

The functional interface can be initialized like this

```
 Greeting helloWorldGreeting = () -> System.out.println("Hello World");
helloWorldGreeting.printMessage();

Greeting goodMorningGreeting = () -> System.out.println("Good morning");
goodMorningGreeting.printMessage();
```

Allowing for less code, similar to passing a callback function.

### Stream in Java

You can perform intermediate operations which return another stream, or you could also perform terminal operations, which return void.

Stream is not the same as a collection, streams are only used to perform operation on data, and do not store the data like a collection does.

## Concurrency

You can use multiple threads to perform multiple tasks at the same time.

### When to use threads

- Blocking I/O operations, such as user input
- GUI interfaces
- Large applications performing independent tasks

### What is a thread

It's a lightweight process, it's an independent path of execution. They have their own stack and local variables.

A process requires more resources, and threads inside the same process share memory. They can easily communicate with each other.

Threads all have access to global variables.

You can make functions `synchronized` so that multiple threads are not able to call it at the same time. This is important to avoid race conditions

```
static synchronized void purchase(StockChecker stockChecker, int amount) {
    int stock = stockChecker.getStock();
    if(stock - amount < 0) {
        System.out.println("Out of stock");
    } else {
        System.out.println("Item is in stock");
        stockChecker.updateStock(amount);
        System.out.println(amount + " items purchased");
    }
    System.out.println("Current stock: " + stockChecker.getStock());
}
```

You can use Executive service to handle threads for you

```

public static void main(String[] args) {

    // Create a new StockChecker object.
    StockChecker stockChecker = new StockChecker();

    // Create an ExecutorService with a fixed thread pool of 4 threads
    ExecutorService executorService = Executors.newFixedThreadPool(4);

    // Submit 4 tasks to the executor service.
    executorService.submit(() -> purchase(stockChecker, 20));
    executorService.submit(() -> purchase(stockChecker, 20));
    executorService.submit(() -> purchase(stockChecker, 20));
    executorService.submit(() -> purchase(stockChecker, 20));

    // In each task you should call the purchase method and pass in 20,
    // to represent a customer purchasing 20 items.
    executorService.shutdown();
    // Shut down the executor service.

}
```
