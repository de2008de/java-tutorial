# Encapsulation

Encapsulation is a concept that we put all relevant data and methods in one place as a single unit - class. By doing this way, we can easily access all relevant data and methods, and protect them from illegal access.

## Access Modifiers

There are four types of access modifiers in Java which put access restriction on fields and methods to protect them:

- Private

- Default

- Protected

- Public

### Private

When a field or a method has been defined as private, they can only be accessed within the class.

```java
public class Book {
    private String title;
    
    public Book(String title) {
        this.title = title;
    }

    private void open() {
        // open() can access private field title
        System.out.println("Open book with title " + title);
    }
}
```

As can be seen from the above codes, title is a private field in class Book so it can only be accessed within class Book. The method open is within the class; therefore, it can use title directly.

However, if we try to access title outside the class, we will get an error.

```java
Book book = new Book();

// error: The field Book.title is not visible
System.out.println(book.title);
```
