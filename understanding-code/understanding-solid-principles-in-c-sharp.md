# Understanding SOLID Principles in C#

SOLID principles are a set of five design principles that help software developers design and build maintainable, scalable, and robust software systems. These principles were introduced by Robert C. Martin and are considered essential for object-oriented programming and design. In this wiki, we will explore each SOLID principle in depth, provide common options, and offer code examples to illustrate how these principles can be applied in C#. Our goal is to make these concepts clear and accessible, ensuring you feel confident and motivated to implement them in your projects.

## S - Single Responsibility Principle (SRP)

The Single Responsibility Principle states that a class should have only one reason to change, meaning it should have only one job or responsibility. This principle helps in achieving a high level of cohesion within a class and ensures that each class has a well-defined purpose.

Imagine you have a class that handles both the logic for processing orders and the logic for sending notifications. If the notification logic changes, the order processing class will need to be modified, violating SRP. By separating these responsibilities into distinct classes, you ensure that changes in one area do not affect the other, making your code more modular and easier to maintain.

**Example:**

```csharp
public class OrderProcessor
{
    public void Process(Order order)
    {
        // Order processing logic
    }
}

public class NotificationService
{
    public void SendNotification(string message)
    {
        // Notification sending logic
    }
}
```

In this example, `OrderProcessor` is responsible for processing orders, and `NotificationService` is responsible for sending notifications, adhering to the SRP.

## O - Open/Closed Principle (OCP)

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means you should be able to add new functionality without changing existing code.

To adhere to OCP, you can use inheritance, interfaces, and abstract classes to allow behavior to be extended without modifying existing code. This reduces the risk of introducing bugs when new features are added.

**Example:**

```csharp
public abstract class Shape
{
    public abstract double CalculateArea();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public override double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```

Here, the `Shape` class is open for extension by creating new shapes (e.g., `Circle`, `Rectangle`), but closed for modification as the `Shape` class itself does not need to change when new shapes are added.

## L - Liskov Substitution Principle (LSP)

The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In other words, subclasses should be able to replace their superclass without causing errors.

LSP ensures that a subclass can stand in for its superclass, guaranteeing that the subclass maintains the behavior and expectations of the superclass. This promotes the use of polymorphism and encourages the creation of interchangeable components.

**Example:**

```csharp
public class Bird
{
    public virtual void Fly()
    {
        Console.WriteLine("Flying");
    }
}

public class Eagle : Bird
{
    public override void Fly()
    {
        Console.WriteLine("Eagle flying");
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException("Penguins cannot fly");
    }
}
```

In this example, `Penguin` violates LSP because it cannot fly, which contradicts the behavior expected from the `Bird` class. To adhere to LSP, we should refactor the hierarchy to separate flying birds from non-flying birds.

## I - Interface Segregation Principle (ISP)

The Interface Segregation Principle states that no client should be forced to depend on methods it does not use. This means interfaces should be small and specific to the needs of their clients, rather than being large and general.

By adhering to ISP, you create more focused and manageable interfaces, reducing the likelihood of implementing unnecessary methods in a class. This leads to more maintainable and understandable code.

**Example:**

```csharp
public interface IOrderProcessor
{
    void ProcessOrder(Order order);
}

public interface INotificationService
{
    void SendNotification(string message);
}

public class OrderProcessor : IOrderProcessor
{
    public void ProcessOrder(Order order)
    {
        // Order processing logic
    }
}

public class NotificationService : INotificationService
{
    public void SendNotification(string message)
    {
        // Notification sending logic
    }
}
```

In this example, `IOrderProcessor` and `INotificationService` are small, focused interfaces that adhere to ISP, ensuring that clients only implement the methods they need.

## D - Dependency Inversion Principle (DIP)

The Dependency Inversion Principle states that high-level modules should not depend on low-level modules. Both should depend on abstractions. Additionally, abstractions should not depend on details. Details should depend on abstractions.

DIP encourages the use of dependency injection and interfaces to decouple high-level and low-level components. This leads to more flexible and testable code, as dependencies can be easily swapped or mocked.

**Example:**

```csharp
public interface IDataAccess
{
    void SaveData(string data);
}

public class DataAccess : IDataAccess
{
    public void SaveData(string data)
    {
        // Save data logic
    }
}

public class DataManager
{
    private readonly IDataAccess _dataAccess;

    public DataManager(IDataAccess dataAccess)
    {
        _dataAccess = dataAccess;
    }

    public void Save(string data)
    {
        _dataAccess.SaveData(data);
    }
}
```

In this example, `DataManager` depends on the `IDataAccess` abstraction, not the `DataAccess` implementation. This adheres to DIP by decoupling the high-level `DataManager` class from the low-level `DataAccess` class.

## Conclusion

Understanding and implementing SOLID principles in C# can significantly improve the quality and maintainability of your code. These principles provide a strong foundation for building robust and scalable software systems. By following SRP, OCP, LSP, ISP, and DIP, you can create code that is easier to read, maintain, and extend. Remember, the goal is to write code that is not only functional but also elegant and resilient. Happy coding!

For further reading and examples, you can explore the following resources:
- [Microsoft C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [SOLID Principles: The Definitive Guide](https://solidprinciples.com/)
- [Refactoring.Guru: SOLID Principles](https://refactoring.guru/design-patterns/solid-principles)
