# Writing clean code

Please observe the following rules during your work :

 - Never write a method that is more than 10 lines
 - Never write a method with more than 2 level of indentation
 - Names should be explicit.

```java
Mail m;    // Bad name
Mail mail; // Way better
```

 - All the code we write should be tested
 - Running tests before  submitting a review
 - Always taking time to read again before submitting a review
 - No comments. Code should be self describing
 - Respect the SOLID principals. Avoid side effects. Avoid sharing objects.
 - Don't realoccate variables : 

```java
// NOT OK
Mail mail = something;
//...
if (condition) {
    mail = otherMail;
}

// OK
Mail mail;
if (condition) {
    mail = something;
} else {
    mail = otherMail;
}

// Even better
Mail mail = retrieveMail()
//And
private Mail retrieveMail() {
    if (condition) {
        return something;
    } else {
        return otherMail;
    }
}
```

 - Class should ideally be small and do one thing well
 - Always prefer composition over inheritance

We will not use most of these recommandations. But please pay attention to the names you are using. And spend time to make it easy to read.
