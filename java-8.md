# Presenting new Java 8 features

In James we love Java 8 because it helps us write much more readable code. In this document, I will present the features we commonly use.

## Equals and hash code

Writing equals and hashCode is subject to errors, is long and hard to read.

You can use Objects helper for getting this easier : 

```java
private final String field1;
private final String field2;

public boolean equals(Object o) {
   if (o instanceOf MyClass.class) {
       MyClass that = (MyClass) o;
       
       return Objects.equal(this.field1, that.field1)
           && Objects.equal(this.field2, that.field2);
   }
   return false
}

public int hashCode() {
    return Objects.hashCode(field1, field2);
}
```

## Lambdas

Lambdas are a good way to inline functions :

Before : 

```java
Function<String, String> function = new Function<String, String>() {
   @Override
   public String apply(String input) {
       return input.toUpperCase(Locale.US);
   }
};
```

Now : 

```java
Function<String, String> function = string -> string.toUpperCase(Locale.US);
```

We will use it later with streams and optionals.

## Optional

An optional represents a value that can be null.

I have to specify my operations knowing that the value can be absent.

Creating an Optional :

```java
Optional<String> example = Optional.empty();
Optional<String> example = Optional.of("This string will never be null");
Optional<String> example = Optional.ofNullable(aStringThatCanBeNull);
```

Getting the value of an optional :

```java
optional.orElse("Replacement value. Will be returned if empty.");
optional.orElseThrow(new Exception("Will be thrown if empty"));
```

I can also do some more work with optionals :

```java
optional.map(string -> string.toLowerCase(Locale.US))
    .ifPresent(string -> doSomething(string));
```

With optionals, we can completly avoid null checks.

## Stream

A stream is a flaw of entity that you can operate on. It offers some functionnal transformations on stream data. You
can replace your **for** and **while** loop with this. It might be harder to write but it is way easier to read and reason about.

### Creating a stream

From a list :

```java
List<String> list;
list.stream();
```

Every collections offer this method.

From an array :

```java
Arrays.stream(myArray);
```

From an Iterator :

```java
Iterable<T> iterable = () -> sourceIterator;
return StreamSupport.stream(iterable.spliterator(), parallel);
```

James offers a utility for this :

```java
Iterators.toStream(iterator);
```

### Operating on a stream

The oerations we will need it the tickets are :

 - filer : only keep results that matches a conditions

```java
    peoples.stream()
        .filter(people -> people.getAge() > 18)
```

 - map : transform the result. The transformation will be applied to each element of the stream.

```java
    peoples.stream()
        .map(people -> people.getAge())
```

 - findFirst : get the first element of the stream. It is useful after a filter operation

```java
    peoples.stream()
        .filter(people -> people.isTeamLeader())
        .findFirst()
```

 - flatMap : If some transformation returns a stream, we might don't want a stream of stream, but a single stream.
 
```java
    employees.stream()
        .flapMap(employee -> employee.getChildren().stream())
        // Now we have the stream of all the children of the employees
```

 - sort (here on Comparable data)

```java
    employee.stream()
        .sort((employee1, employee2) -> employee1.compareTo(employee2))
```

### Getting the result of a stream calculation

We don't want to modify the result of the calculations we made hence we return Immutable datas.

Return a list :

```java
return initialCollection.stream()
    .filter(/*Some condition*/)
    .collect(Guavate.toImmutableList());
```

Return a map : 

```java
return initialCollection.stream()
    .filter(/*Some condition*/)
    .collect(Guavate.toImmutableMap(item -> item.extractKey()));
```

Or : 

```java
return initialCollection.stream()
    .filter(/*Some condition*/)
    .collect(Guavate.toImmutableMap(item -> item.extractKey(), item -> item.extractValue()));
```
