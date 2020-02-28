![category](https://img.shields.io/badge/Category-Java%20Basics-brightgreen)

![logo](../logo.png)

![cover](img/access_modifiers_cover.png)

- [Access Modifiers](#access-modifiers)
  * [Private](#private)
  * [Default](#default)
  * [Protected](#protected)
  * [Public](#public)
  * [Overriding Methods](#overriding-methods)

# Access Modifiers

There are four types of access modifiers in Java which put access restriction on fields and methods, and we can apply some of the access modifiers to a class:

- Private

- Default

- Protected

- Public

## Private

When we define a field or a method as private, we can only access them within the same class.

```java
class Book {

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

As can be seen from the above codes, the title is a private field in class Book, so we can only access it within the class Book. For example, the method open() is within the class Book, so it can use the field title directly.

However, if we try to access the private field title or the private method open() outside the class Book, we get errors.

```java
class Pen {

    public void static main(String[] args) {

        Book book = new Book("My Book");

        // error: The field Book.title is not visible
        System.out.println(book.title);

        // error: The method open() from the type Book is not visible
        book.open();
        
    }

}
```

We can define a class as private, and we can only access a private class within the class that encloses it.

```java
class Book {
    
    Book book = new Book();

    // Ok because class Pen is enclosed by class Book
    Pen pen = book.new Pen();
    pen.print();

    private class Pen {
        public void print() {
            System.out.println("I am a pen");
        }
    }
}

class Water {

    public static void main(String[] args) {

        Book book = new Book();
        // error: Pen is not visible
        Pen pen = book.new Pen();

    }

}
```

## Default

If we do not specify access modifiers, then it is a default access modifier. We can only access a default field, method, or class within the same package that defines them.

```java
package A;

class Book {

    // Default access modifier
    String title;

    public Book(String title) {
        this.title = title;
    }

}
```

If we try to access the default field title outside package A, we get an error.

```java
package B;

class Pen {
    
    public static void main(String[] args) {

        Book book = new Book("My Book");

        // error
        String title = book.title;

    }
}
```

However, we can access the field title within the same package even if we access it within a different class.

```java
package A;

class Pen {

    public static void main(String[] args) {

        Book book = new Book("My Book");

        // Ok because they are within the same package A
        String title = book.title;

    }

}

```

We can apply the default access modifier to a class as well. A class with a default access modifier can only be accessed within the same package.

## Protected

If we define a field or a method with a protected access modifier, we can access them within the same package. However, if we want to access them outside the same package, we need to access them through **inheritance**.

We can access an **inherited** protected field or method within a child class.

```java
package A;

class Book {
    protected String title = "I am a book";
}
```

```java
package A;

class Pen {
    public static void main(String[] args) {

        Book book = new Book();

        // Ok because they are within the same package A
        System.out.println(book.title);

    }
}
```

```java
package B;

class MyBook extends Book {

    public static void main(String[] args) {
        
        MyBook mb = new MyBook();

        // Ok because MyBook is a child class of Book
        // Therefore, MyBook inherits title so we can access
        // the inherited field title here
        System.out.println(mb.title);

        Book book = new Book();
    
        // Error because this field title belongs to Book since this is an object of Book
        // Therefore, MyBook does not inherit this particular
        // title here so we cannot access it here
        System.out.println(book.title);

    }

}

class Table {

    public static void main(String[] args) {

        MyBook mb = new MyBook();

        // Error because Table is not a child class of MyBook
        // so it cannot access the protected field title
        System.out.println(mb.title);

    }
    
}
```

Although the class MyBook inherits the field title from the class Book, the access modifier is still protected. Therefore, the class Table cannot access the protected field title of MyBook since the class Table is not a child class of MyBook.

Also, we cannot apply the protected access modifier to a class.

## Public

The access modifier public allows access from anywhere, and we can apply it to a class.

```java
package A;

public class Book {
    public String title = "My Book";
}
```

```java
package B;

class Table {

    public static void main(String[] args) {

        // Ok because class Book is public
        Book book = new Book();

        // Ok because the field title is public
        System.out.println(book.title);

    }

}
```

## Overriding Methods

If we are overriding a method, the overridden method cannot be defined with a more restrictive access modifier.

For example, we cannot override a protected method to a private method.

```java
class Book {
    protected void read() {}
}

class MyBook extends Book {
    
    // Ok because public is less restrictive than protected
    public void read() {}

    // Error because private is more restrictive than protected
    private void read() {}
}
```
