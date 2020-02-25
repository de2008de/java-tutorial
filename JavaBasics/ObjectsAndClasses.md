# Java Objects and Classes

Java is an object-oriented programming language. That means we will use a lot of objects in Java so it is very important to learn about them.

## Constructors: Create an Object

To create an object, we need to call a constructor with keyword **new**. For example:

```Java
// mb is an object of MyObject
MyObject mb = new MyObject();
```

Use dot . to access object's fields and methods.

```Java
MyObject mb = new MyObject();

mb.name; // access field
mb.sleep(); // access method
```

Constructor has the same name as the class name and it does not have a return type defined in code. 

However, that does not mean constructors return nothing. In fact, the constructor returns an instance of the class (object) so we can say that the return type of the constructors is the object type itself. 

In addition, a class can have many constructors as long as they have different lists of parameter types.

```java
public class MyObject {
    // Default Constructor: has no parameters
    public MyObject() {}

    // Constructor 2
    public MyObject(int id) {}

    // Constructor 3
    public MyObject(long id) {}

    // This is not a constructor as it has void return type defined
    public void MyObject() {}
}
```

## Classes: Blueprint for Objects

Class is a blueprint for objects. We need to write a class to define skeleton of the object.

For example, we want to create a cat object. This cat should have a name and age, and can walk and sleep. Therefore, we need to define those properties as class fields and behaviors as class methods in our Cat class.

```java
public class Cat {
    // Fields
    private String name;
    private int age;

    public Cat(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Methods
    public void walk() {
        System.out.println(name + " is walking");
    }

    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}
```

Once we have the class Cat defined, we can create a Cat object.

```java
public static void main(String[] args) {
    Cat cat = new Cat("Tigger", 2);

    cat.walk();
    cat.sleep();
}
```

The output will be:

```
Tigger is walking
Tigger is sleeping
```
