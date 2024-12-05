# OOP Principles
- **Encapsulate**  is achieved by hiding the details of the web elements and providing only the necessary methods to interact with them.
  - Private Web Elements: Web elements are made private so that they are not accessible from outside the Page Object class.
  - Public Methods: Methods are provided to interact with these private elements. These methods are exposed to the test scripts, which can invoke them to interact with the web page.
- **Abstract** away the complexity of page interactions from the test scripts by creating high-level methods (e.g., login, logout).
- **Inheritance** is useful when there are common actions or utilities that can be shared between different page objects.
  - BasePage Class: A BasePage class can be created to contain common functionality such as navigating to different pages, waiting for elements, or performing common actions (e.g., clicking buttons, checking alerts).
  - The Page Object classes can then inherit from the BasePage class to reuse common methods.
- **Polymorphism** allows different page objects or actions to be handled using the same interface. This can be useful when you want to extend functionality or handle different page interactions in a unified way. Method overriding:
  - Redefine methods in the subclass
  - Define other methods with the same name, but different parameters
 
# SOLID principles
- **S - Single Responsibility Principle (SRP)**
  - Definition: A class should have only one reason to change, meaning it should only have one responsibility.
  - Example: A class that handles both user authentication and sending notifications should be refactored, so that each class focuses on a single task (one for authentication and another for notifications).
- **O - Open/Closed Principle (OCP)**
  - Definition: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
  - Example: Instead of modifying an existing class to add new functionality, you can extend it via inheritance or use interfaces and abstract classes to allow new behavior without altering existing code.
- **L - Liskov Substitution Principle (LSP)**
  - Definition: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
  - Example: If you have a base class Bird with a method fly(), and a subclass Penguin, the Penguin class should not override fly() to throw errors because penguins cannot fly.
- **I - Interface Segregation Principle (ISP)**
  - Definition: Clients should not be forced to depend on interfaces they do not use.
  - Example: Instead of having a large, monolithic interface with methods that don't make sense for certain classes, split it into smaller, more specific interfaces that are relevant to each class.
- **D - Dependency Inversion Principle (DIP)**
  - Definition: High-level modules should not depend on low-level modules. Both should depend on abstractions. Additionally, abstractions should not depend on details. Details should depend on abstractions.
  - Example: Instead of directly using a concrete class in your code, use an interface or abstract class. This makes your code more flexible and easier to test, as you can inject dependencies at runtime.

In summary:
- SRP keeps classes focused.
- OCP encourages extension without modification.
- LSP ensures that subclasses maintain the behavior of the superclass.
- ISP promotes smaller, more focused interfaces.
- DIP makes systems more modular and decoupled by depending on abstractions.
Together, these principles help in building robust and maintainable object-oriented systems.

# Compare Abstract and Interface
- Abstract:
  - Use an abstract class when you want to define a **template** for a group of related classes. Typically used when you want to provide a partial implementation of a class.
  - Used to provide a common base class with shared code and common behavior. Can define both fully implemented methods (with code) and abstract methods (without implementation).
  - The elements in the Abstract class can have an access level like a normal class
  - A regular class can only inherit from one Abstract class

```
abstract class Shape
{
    // Abstract method to be implemented by subclasses
    public abstract double CalculateArea();

    // Concrete method with shared implementation
    public void DisplayArea()
    {
        Console.WriteLine($"Area: {CalculateArea()}");
    }
}


class Circle : Shape
{
    public double Radius { get; set; }

    public Circle(double radius)
    {
        Radius = radius;
    }

    // Implementation of the abstract method
    public override double CalculateArea()
    {
        return Math.PI * Math.Pow(Radius, 2);
    }
}

```

- Interface:
  - Use an interface when you want to define a **contract** that classes must implement
  - By defining the general specifications of the methods, without implementing them, it requires the derived classes to **fully** implement those methods.
  - Interfaces do not have a constructor or a field, and no instance can be created from them.
  - Interfaces have the advantage of inheriting as many classes as they need.

```
public interface Scalable {
    void scale(double factor);
    void resetScale();
}

public class Circle implements Scalable {
    private double radius;
    private double scale = 1.0;

    public Circle(double radius) {
        this.radius = radius;
    }

    public void scale(double factor) {
        this.scale *= factor;
        this.radius *= factor;
    }

    public void resetScale() {
        this.scale = 1.0;
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```
