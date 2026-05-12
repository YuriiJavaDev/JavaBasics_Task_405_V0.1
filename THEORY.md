## Errors when declaring classes and objects.

### 1. Class Declaration Errors

#### Missing Access Modifiers (package-private by default)

In Java, if you don't explicitly specify an access modifier for a class, it is accessible only within the current package. This is called package-private or "default access." For example:

```java
// Book.java
class Book {
    String title;
}
```

Such a class cannot be used from another package. If you want the class to be accessible everywhere (and this is often the case for core models), use the **public** modifier:

```java
public class Book {
    String title;
}
```

**Why is this important?**

If you forget to include **public**, you'll be wondering why some **Library** from another package can't see your class.

#### Class Name and File Name Mismatch

In Java, the name of a class file **must match the name of a public class** within that file (case-sensitive!). For example:

```java
// Book.java File
public class Book {
    // ...
}
```

If you name the file **book.java** (without a capital letter) or, even worse, **BooK.java**, the compiler will throw an error. This is one of the reasons why the IDE is so fond of yelling at you if you rename a class but forget to rename the file.

#### Declaration Syntax Errors: Forgotten Curly Braces, Incorrectly Placed Methods and Fields

Java is a strict language. If you forget a curly brace or accidentally declare a method inside another method (you can't do that!), the compiler will immediately shame you.

**Example of an incorrect declaration:**

```java
public class User
    String name; // Oops! Missing class braces
    
    public void printName() {
        System.out.println(name);
    }
}
```

**Correct:**

```java
public class User {
    String name;
    
    public void printName() {
        System.out.println(name);
    }
}
```

**Remember:**

- All fields and methods are declared only within the class braces.
- Methods cannot be nested (in some languages, nested methods are allowed, but not in Java!).

### 2. Errors when creating objects

#### Attempting to use an object before it's initialized (**NullPointerException**)

The most common mistake of all time is trying to access an object that hasn't yet been created. In Java, reference type variables are null by default.

**Example:**

```java
User user;
System.out.println(user.name); // NullPointerException!
```

**Why?**

The **user** variable is declared but not initialized. If you try to access the field or method, you'll get an NPE (**NullPointerException**).

**Correct approach:**

```java
User user = new User();
System.out.println(user.name); // Now everything is fine (if the field isn't null)
```

#### Errors in constructor calls (mismatched parameters, missing default constructor)

If a class only has a parameterized constructor, attempting to create an object without parameters will result in a compilation error.

```java
public class Book {
    String title;
    
    public Book(String title) {
        this.title = title;
    }
}

    Book book = new Book(); // Error! No parameterless constructor
```

**Solution:** Either add a parameterless constructor or always pass the required values:

```java
Book book = new Book("Java for Dummies");
```

#### Multiple object creation instead of reuse

Sometimes beginners create a new object each time they need to access it, instead of using an existing one.

```java
Book book = new Book("Java for Dummies");
    System.out.println(book.title);

book = new Book("Java for Dummies"); // Why? There's already such an object!
    System.out.println(book.title);
```

This isn't a compilation error, but it's a sign of bad style—you're losing a reference to the old object and wasting unnecessary memory.

### 3. Best Practices: How to Avoid Making the Same Pitfall

#### Always Explicitly Specify Access Modifiers

Don't be lazy about writing **public**, **private**, or **protected**—this isn't just about security, it's also about code readability. The IDE will help, of course, but it's better to develop the habit right away.

**Example:**

```java
public class User {
    private String name;
    // ...
}
```

#### Watch your class naming

- Class name — capitalize, CamelCase: Book, LibraryUser, BookManager**.
- File name — exactly like the class name.

#### Use constructors to initialize required fields

If an object has fields that **required** to be filled in when created, add a constructor with parameters. This will prevent errors during use.

**Example:**

```java
public class User {
    private String name;
    
    public User(String name) {
        this.name = name;
    }
}
```

Now you can't create a **User** without a name — the compiler won't let you.

### 4. Applying What We've Learned: Building the Library Mini-App

Let's continue developing our tutorial app. Let's say we have a **Book** class and a **Library** class that manages books.

#### Example of a Correct Class Declaration

```java
// Book.java
public class Book {
    private String title;
    private String author;
    
    // Constructor with parameters
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
    
    // Getters
    public String getTitle() {
        return title;
    }
    
    public String getAuthor() {
        return author;
    }
}
```

#### Example of Correct Object Creation

```java
Book book = new Book("Java for Dummies", "John Doe");
    System.out.println(book.getTitle() + " - " + book.getAuthor());
```

#### Example of a manager class

```java
// File Library.java
import java.util.ArrayList;

public class Library { 
    private ArrayList<Book> books = new ArrayList<>(); 
    
    public void addBook(Book book) { 
        books.add(book); 
    } 
    
    public void printAllBooks() { 
        for (Book book : books) { 
            System.out.println(book.getTitle() + " - " + book.getAuthor()); 
        } 
    }
}
```

#### Use in main

```java
public class Main { 
    public static void main(String[] args) { 
        Library library = new Library(); 
        Book book1 = new Book("Java for Dummies", "John Doe");
        Book book2 = new Book("OOP in a Nutshell", "Ivan Ivanov");
        
        library.addBook(book1);
        library.addBook(book2);
        
        library.printAllBooks();
    }
}
```

### 5. Illustrations and Diagrams

#### Diagram: Where to Declare What?

```
+------------------------------+
| Book.java                    |
|------------------------------|
| public class Book {          |
| private String title;        | <--- fields (only within the class)
| ...                          |
| public Book(...) {...}       | <--- constructor (within the class)
| public String getTitle()     | <--- methods (within the class)
| }                            |
+------------------------------+

+------------------------------+
| Main.java                    |
|------------------------------|
| public class Main {          |
| public static void main      |
| // Creating objects          |
| Book book = new Book         |
| }                            |
+------------------------------+
```

### 6. Analyzing Common Errors

**Error №1: Class name and file name mismatch**

```java
// File: Libraryuser.java
public class LibraryUser { // Class name with a capital U, file with a lowercase U!
    // ...
}
```

**class LibraryUser is public, should be declared in a file named LibraryUser.java**

**Error №2: Attempt to use an uninitialized object**

```java
Book book;
System.out.println(book.getTitle()); // NullPointerException!
```

**Error №3: Forgotten curly braces**

```java
public class Book
private String title; // Fields are usually made private for encapsulation
    // ...
}
```

**';' expected**

**Error №4: Method declaration within a method**

```java
public class User {
    public void printName() {
        void sayHello() {
            System.out.println("Hello!"); // Cannot declare a method within a method!
        }
    }
}
```

**illegal start of type**
