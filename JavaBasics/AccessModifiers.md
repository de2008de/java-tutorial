![category](https://img.shields.io/badge/Category-Java%20Basics-brightgreen)

![logo](../logo.png)

- [Access Modifiers](#access-modifiers)
  * [Private](#private)
  * [Default](#default)
  * [Protected](#protected)
  * [Public](#public)
  * [Overriding Methods](#overriding-methods)

# Access Modifiers

There are four types of access modifiers in Java which put access restriction on fields and methods to protect them:

- Private

- Default

- Protected

- Public

## Private

When a field or a method has been defined as private, they can only be accessed within the class.

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

As can be seen from the above codes, title is a private field in class Book so it can only be accessed within class Book. The method open is within the class; therefore, it can use title directly.

However, if we try to access title outside the class, we will get an error.

```java
class Pen {

    public void static main(String[] args) {

        Book book = new Book("My Book");

        // error: The field Book.title is not visible
        System.out.println(book.title);
        
    }

}
```

If we try to call a private method outside of its class, we will get an error.

```java
class Pen {

    public static void main(String[] args) {

        Book book = new book("My Book");

        // error: The method open() from the type Book is not visible
        book.open();

    }

}

```

A class can be defined as private as well. A private class can only be accessed within the enclosing class.

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

If we do not specify access modifiers, then the access modifier will be default.

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

If we try to access title outside package A, we will get an error.

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

However, we can access title within the same package even if we access it within different class.

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

Default can be applied to class as well. A default class can only be acessed within the same package.

## Protected

A protected field or method can be accessed within or outside the same package. If they are accessed outside the same package, they can only be accessed through **inheritance**.

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
        // it here
        System.out.println(mb.title);

        Book book = new Book();
    
        // Error because this title field belongs to Book since this is an object of Book.
        // Therefore, MyBook does not inherit this specific
        // title here
        System.out.println(book.title);

    }

}

class Table {

    public static void main(String[] args) {

        Mybook mb = new MyBook();

        // Error because Table is neither a child class of Book nor a child class of MyBook
        // so it cannot access the protected field title
        System.out.println(mb.title);

    }
    
}
```

Although MyBook inherits title from Book, the field title is still protected. Therefore, class Table cannot access the protected field title of MyBook.

In addition, the keyword protected cannot be applied to class.

## Public

Public is an access modifier that allows access from anywhere and can be applied to class.

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

        // Ok because title is public
        System.out.println(book.title);

    }

}
```

## Overriding Methods

If we are overriding a method, the overridden method cannot be more restrictive.

For example, a protected method cannot be overriden as a private method.

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
