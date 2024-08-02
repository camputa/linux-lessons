## Understanding Design Patterns in C#

Design patterns are reusable solutions to common problems in software design. They provide a template for how to solve a problem that can be used in many different situations. The "Gang of Four" (GoF) design patterns are widely recognized and provide a solid foundation for object-oriented design. In this wiki, we will explore these design patterns, provide common options, and offer code examples to illustrate how they can be applied in C#. Our aim is to present these concepts in a motivational and happy tone, making them accessible to those who are new to technology.

### 1. Creational Patterns

Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable for the situation. They help in making the system independent of how objects are created, composed, and represented.

#### Singleton Pattern

**Definition:**
The Singleton Pattern ensures that a class has only one instance and provides a global point of access to it.

**Explanation:**
Imagine you have a logging class that writes messages to a file. If multiple instances of this class exist, they might try to write to the file simultaneously, causing errors. The Singleton Pattern ensures that only one instance of the logging class exists, avoiding these issues.

**Example:**

```csharp
public class Singleton
{
    private static Singleton _instance;

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = new Singleton();
            }
            return _instance;
        }
    }

    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}
```

In this example, the `Singleton` class ensures that only one instance of the class can exist, and provides a global access point through the `Instance` property.

#### Factory Method Pattern

**Definition:**
The Factory Method Pattern defines an interface for creating an object but lets subclasses alter the type of objects that will be created.

**Explanation:**
Imagine you are developing a document editor that can create different types of documents, such as Word documents and PDFs. The Factory Method Pattern allows you to define a method for creating a document and let subclasses specify which document type to create.

**Example:**

```csharp
public abstract class Document
{
    public abstract void Print();
}

public class WordDocument : Document
{
    public override void Print()
    {
        Console.WriteLine("Printing Word document...");
    }
}

public class PdfDocument : Document
{
    public override void Print()
    {
        Console.WriteLine("Printing PDF document...");
    }
}

public abstract class DocumentCreator
{
    public abstract Document CreateDocument();
}

public class WordDocumentCreator : DocumentCreator
{
    public override Document CreateDocument()
    {
        return new WordDocument();
    }
}

public class PdfDocumentCreator : DocumentCreator
{
    public override Document CreateDocument()
    {
        return new PdfDocument();
    }
}
```

In this example, the `DocumentCreator` class defines the `CreateDocument` method, and the subclasses `WordDocumentCreator` and `PdfDocumentCreator` specify which document type to create.

### 2. Structural Patterns

Structural patterns deal with object composition, helping to ensure that if one part of a system changes, the entire system doesn't need to change as a result.

#### Adapter Pattern

**Definition:**
The Adapter Pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces.

**Explanation:**
Imagine you have a graphics library that draws shapes using a specific interface, but you need to use a new library with a different interface. The Adapter Pattern allows you to create an adapter class that makes the new library compatible with the existing code.

**Example:**

```csharp
public interface IShape
{
    void Draw();
}

public class LegacyRectangle
{
    public void DrawRectangle()
    {
        Console.WriteLine("Drawing rectangle...");
    }
}

public class RectangleAdapter : IShape
{
    private readonly LegacyRectangle _legacyRectangle;

    public RectangleAdapter(LegacyRectangle legacyRectangle)
    {
        _legacyRectangle = legacyRectangle;
    }

    public void Draw()
    {
        _legacyRectangle.DrawRectangle();
    }
}
```

In this example, the `RectangleAdapter` class makes the `LegacyRectangle` class compatible with the `IShape` interface.

#### Composite Pattern

**Definition:**
The Composite Pattern allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.

**Explanation:**
Imagine you are developing a file system where files and directories can be represented in a tree structure. The Composite Pattern allows you to treat both files and directories uniformly, making it easier to manage the file system.

**Example:**

```csharp
public abstract class FileSystemComponent
{
    public abstract void Display();
}

public class File : FileSystemComponent
{
    private readonly string _name;

    public File(string name)
    {
        _name = name;
    }

    public override void Display()
    {
        Console.WriteLine(_name);
    }
}

public class Directory : FileSystemComponent
{
    private readonly string _name;
    private readonly List<FileSystemComponent> _components = new List<FileSystemComponent>();

    public Directory(string name)
    {
        _name = name;
    }

    public void Add(FileSystemComponent component)
    {
        _components.Add(component);
    }

    public override void Display()
    {
        Console.WriteLine(_name);
        foreach (var component in _components)
        {
            component.Display();
        }
    }
}
```

In this example, the `Directory` class can contain both files and other directories, allowing for a tree structure representation.

### 3. Behavioral Patterns

Behavioral patterns deal with object collaboration and the delegation of responsibilities between objects.

#### Observer Pattern

**Definition:**
The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Explanation:**
Imagine you have a stock market application where multiple displays need to be updated whenever stock prices change. The Observer Pattern allows you to create a subject (the stock data) and observers (the displays) that get notified when the stock data changes.

**Example:**

```csharp
public interface IObserver
{
    void Update();
}

public class StockData
{
    private readonly List<IObserver> _observers = new List<IObserver>();

    public void Attach(IObserver observer)
    {
        _observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        _observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in _observers)
        {
            observer.Update();
        }
    }
}

public class StockDisplay : IObserver
{
    public void Update()
    {
        Console.WriteLine("Stock data updated");
    }
}
```

In this example, the `StockData` class notifies all attached observers when the stock data changes.

#### Strategy Pattern

**Definition:**
The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the algorithm vary independently from clients that use it.

**Explanation:**
Imagine you are developing a sorting application that needs to support multiple sorting algorithms (e.g., quicksort, mergesort). The Strategy Pattern allows you to define each algorithm separately and switch between them at runtime.

**Example:**

```csharp
public interface ISortingStrategy
{
    void Sort(List<int> list);
}

public class QuickSort : ISortingStrategy
{
    public void Sort(List<int> list)
    {
        Console.WriteLine("QuickSort algorithm");
    }
}

public class MergeSort : ISortingStrategy
{
    public void Sort(List<int> list)
    {
        Console.WriteLine("MergeSort algorithm");
    }
}

public class SortContext
{
    private ISortingStrategy _strategy;

    public void SetStrategy(ISortingStrategy strategy)
    {
        _strategy = strategy;
    }

    public void SortList(List<int> list)
    {
        _strategy.Sort(list);
    }
}
```

In this example, the `SortContext` class can use different sorting strategies interchangeably, allowing for flexible sorting options.

### Conclusion

Design patterns are powerful tools in a developer's toolkit, providing tried-and-true solutions to common problems. By understanding and implementing these patterns in C#, you can create code that is more modular, maintainable, and scalable. Whether you are using creational patterns to manage object creation, structural patterns to organize your system, or behavioral patterns to manage object interactions, design patterns help you build better software. Embrace these patterns, practice them in your projects, and watch your coding skills soar!

For further reading and examples, you can explore the following resources:
- [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/dp/0201633612) by the Gang of Four
- [Refactoring.Guru: Design Patterns](https://refactoring.guru/design-patterns)
- [Microsoft C# Design Patterns](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/design-patterns)

Happy coding!