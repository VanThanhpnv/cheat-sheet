# Presenting new Java 8 features

In James we love Java 8 because it helps us write much more readable code. In this document, I will present the features we commonly use.

## Equals and hash code

Writing equals and hashCode is subject to errors, is long and hard to read.

You can use Objects helper for getting this easier : 

```
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

```
Function<String, String> function = new Function<String, String>() {
   @Override
   public String apply(String input) {
       return input.toUpperCase(Locale.US);
   }
};
```

Now : 

```
Function<String, String> function = string -> string.toUpperCase(Locale.US);
```

We will use it later with streams and optionals.

## Optional

An optional represents a value that can be null.

I have to specify my operations knowing that the value can be absent.

Creating an Optional :

```
Optional<String> example = Optional.empty();
Optional<String> example = Optional.of("This string will never be null");
Optional<String> example = Optional.ofNullable(aStringThatCanBeNull);
```

Getting the value of an optional :

```
optional.orElse("Replacement value. Will be returned if empty.");
optional.orElseThrow(new Exception("Will be thrown if empty"));
```

I can also do some more work with optionals :

```
optional.map(string -> string.toLowerCase(Locale.US))
    ...
optional.ifPresent(string -> doSomething(string));
```

With optionals, we can completly avoid null checks.

## Stream

### Creating a stream

### Operating on a stream

### Getting the result of a stream calculation
