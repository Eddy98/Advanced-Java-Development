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
