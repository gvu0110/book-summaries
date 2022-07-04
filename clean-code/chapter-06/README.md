# Chapter06
## Objects and Data Structures

### 1. Data Abstraction
- Abstraction means hiding implementation.
- Hiding implementation isn't means making the variables private and using `getter` and `setter` to access these variables.
- It means providing abstract interfaces that allow its users to manipulate the data, without having to know its implementation.
- This is not **Abstraction**:
```java
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```
- The following code doesn't represent **Abstraction** either. But, it uses concrete terms to communicate the fuel level of a vehicle, because these methods sure are just accessors (getters) of variables.
```java
public interface Vehicle {
    double getFuelTankCapacityInGallons();
    double getGallonsOfGasoline();
}
```
- The following code represents **Abstraction**. Which it does is the same purpose of the previous code, but with the abstraction of percentage. So, in this abstract case you do not at all know anything about internal details of data.
```java
public interface Vehicle {
    double getPercentFuelRemaining();
}
```

### 2. Data/Object Anti-Symmetry
- The difference between objects and data structures:
    + Objects: hide the data (be private) and have functions to operate on that data.
    + Data Structures: show the data (be public) and have no functions.

- The following code is using **data structures**. The `Geometry` class operates on the three shape classes. The shape classes are simple data structures without any behavior (function). All the behavior is in the Geometry class.
- If we add a `perimeter()` function to `Geometry`, the shape classes would be unaffected. But, if we add a new shape (new data structure), we must change all the functions in `Geometry` to deal with it.
```java
public class Square {
    public Point topLeft;
    public double side;
}

public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
}

public class Circle {
    public Point center;
    public double radius;
}

public class Geometry {
    public final double PI = 3.141592653589793;

    public double area(Object shape) throws NoSuchShapeException {
        if (shape instanceof Square) {
            Square s = (Square)shape;
            return s.side * s.side;
        }
        else if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle)shape;
            return r.height * r.width;
        }
        else if (shape instanceof Circle) {
            Circle c = (Circle)shape;
            return PI * c.radius * c.radius;
        }
        throw new NoSuchShapeException();
    }
}
```
- The following code is using **object oriented**. The `area()` function is polymorphic.
- If we add a new shape, none of the existing functions are affected. But, if I add a new function in `Shape` interface, all of the shapes must be changed.
```java
public interface Shape {
    public double area();
}

public class Square implements Shape {
    private Point topLeft;
    private double side;

    public double area() {
        return side*side;
    }
}

public class Rectangle implements Shape {
    private Point topLeft;
    private double height;
    private double width;

    public double area() {
        return height * width;
    }
}

public class Circle implements Shape {
    private Point center;
    private double radius;
    public final double PI = 3.141592653589793;

    public double area() {
        return PI * radius * radius;
    }
}
```
- Conclusion:
    + Procedural code (code using data structures) makes it easy to add new functions without changing the existing data structures. OO codode, on the other hand, makes it easy to add new classes without changing existing functions.
    + Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change.

### 3. The Law of Demeter
- A software component or an object should not have the knowledge of the internal working of other objects or components.
- The method `f` of a class `C` should only call the methods of these:
    + `C`
    + An object created by `f`
    + An object passed as an arguments to `f`
    + An object held in an instance variable of `C`
- The method should not invoke methods on objects that are returned by any of allowed functions. 
- The following code violates the Law of Demeter. It calls the `getScratchDir()` function on the return value of `getOptions()` and then calls `getAbsolutePath()` on the return value of `getScratchDir()`.
```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```
**Train Wrecks**
- The following "refactored" code is better, but, it still violates the Law:
```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```
- If `ctxt`, `Options`, and `ScratchDir` are just data structures with no behavior, then they naturally expose their internal structure, and so the Law does not apply. And the code had been written as follows
```java
final String outputDir = ctxt.options.scratchDir.absolutePath;
```

**Hybrids**
- Hybrid structures that are half object and half data structure.
- Avoid creating them. They are indicative of a muddled design whose authors are unsure of whether they need protection from functions or types.

**Hiding Structure**
- What if `ctxt`, `options`, and `scratchDir` are objects with real behavior? How then would we get the absolute path of the scratch directory?
- Assume that the intent of getting the absolute path of the scratch directory was to create a scratch file of a given name.
```java
String outFile = outputDir + "/" + className.replace('.', '/') + ".class";
FileOutputStream fout = new FileOutputStream(outFile);
BufferedOutputStream bos = new BufferedOutputStream(fout);
```
- So this following code allows `ctxt` to hide its internals
```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

### 4. Data Transfer Objects
- A form of a data structure which is a class with public variables and no functions.
- DTOs are very useful structures, especially when communicating with databases or parsing messages from sockets.
- There is another more common form called the ***bean*** form. Beans have private variables manipulated by getters and setters.
```java
public class Address {
    private String street;
    private String streetExtra;
    private String city;
    private String state;
    private String zip;

    public Address(String street, String streetExtra, String city, String state, String zip) {
        this.street = street;
        this.streetExtra = streetExtra;
        this.city = city;
        this.state = state;
        this.zip = zip;
    }

    public String getStreet() {
        return street;
    }

    public String getStreetExtra() {
        return streetExtra;
    }

    public String getCity() {
        return city;
    }

    public String getState() {
        return state;
    }

    public String getZip() {
        return zip;
    }
}
```