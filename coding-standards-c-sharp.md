# C# Coding Standards and Naming Conventions

Welcome to our team! As a new junior developer, you're embarking on an exciting journey of learning and growth. To help you succeed, we've established a set of C# coding standards and naming conventions that will guide you in writing clean, maintainable, and efficient code. Adhering to these standards not only ensures consistency across our projects but also fosters a collaborative and productive work environment. Let's explore these standards and conventions, focusing on clarity, readability, and best practices, with specific tips for Visual Studio IDE and VS Code IDE users.

## General Coding Standards

### Consistency and Readability

Consistency in code style is crucial for maintaining readability and ease of maintenance. Our coding standards are designed to promote these principles across all our projects.

### Formatting Guidelines

Proper formatting improves code readability and maintainability. Here are some key formatting guidelines:

**Indentation:**
Use tabs for indentation. This ensures that your code is uniformly indented, making it easier to read and maintain.

```csharp
public void ProcessData() {
    if (data == null) {
        throw new ArgumentNullException(nameof(data));
    }
    // Process data
}
```

**Braces:**
Place opening braces on a new line, and closing braces on a new line to match the opening statement.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

**Spacing:**
Use a single space before and after operators, and after commas.

```csharp
int sum = a + b;
Console.WriteLine("Sum: " + sum);
```

### Code Structure and Organization

Organizing your code effectively is crucial for maintainability. Here are some tips:

**Namespace Organization:**
Organize your classes into namespaces to group related functionalities.

```csharp
namespace Company.Project.Module {
    public class Employee {
        // Class logic
    }
}
```

**Class Structure:**
Structure your classes logically, starting with fields, followed by properties, constructors, methods, and event handlers.

```csharp
public class Employee {
    // Fields
    private int employeeId;
    private string firstName;

    // Properties
    public int EmployeeId { get; set; }
    public string FirstName { get; set; }

    // Constructor
    public Employee(int id, string name) {
        EmployeeId = id;
        FirstName = name;
    }

    // Methods
    public void DisplayEmployeeDetails() {
        Console.WriteLine($"ID: {EmployeeId}, Name: {FirstName}");
    }
}
```

**File Organization:**
Place each class in its own file and name the file after the class. This makes it easier to locate and manage classes.

```csharp
// File: Employee.cs
public class Employee {
    // Class logic
}

// File: Department.cs
public class Department {
    // Class logic
}
```

---

## Naming Conventions

Naming conventions are essential for readability and maintaining a clean codebase. Follow these principles to ensure consistency.

- **Clarity and Descriptiveness**: Choose names that clearly describe the purpose and use of the variable, method, or class. Avoid abbreviations and single-letter names, except for loop counters.
- **Pascal Case and Camel Case**: Use PascalCase for class names, method names, and properties. Use camelCase for variables and parameters.

### Why Naming Conventions Matter

Naming conventions are like the grammar rules of coding. They provide a common language that helps developers understand and navigate the codebase easily. Consistent naming makes your code more readable and reduces the cognitive load for anyone who reads or maintains it. When everyone on the team follows the same conventions, it becomes easier to collaborate, review code, and catch errors. Naming conventions also make automated tools and IDEs more effective, as they can more reliably predict and assist with your coding patterns.

### Variable Naming Conventions

Here's a table to illustrate various naming conventions:

| Type| Convention | Example |
|---|---|---|
| Class| PascalCase | `Customer`, `OrderProcessor` |
| Method | PascalCase | `CalculateTotal`, `ProcessOrder` |
| Property | PascalCase | `CustomerName`, `OrderDate` |
| Variable | camelCase | `customerName`, `orderDate` |
| Constant | PascalCase | `MaxRetryCount`, `DefaultTimeout` |
| Private Field | _camelCase | `_logger`, `_currentRetryCount` |
| Parameter | camelCase | `customerName`, `orderId` |

### Classes and Methods

Class and method names should convey their responsibilities and behaviors.

- **Classes**: Use nouns or noun phrases. For example, `Customer`, `OrderProcessor`, `InvoiceService`.
- **Methods**: Use verbs or verb phrases. For example, `CalculateTotal`, `ProcessOrder`, `GenerateInvoice`.

```csharp
public class InvoiceService
{
    public void GenerateInvoice(Customer customer)
    {
        // Implementation
    }
}
```

### Variables and Constants

Variables and constants should be named based on their purpose and scope.

- **Variables**: Use camelCase for local variables and parameters. Ensure the name is descriptive and contextually meaningful.
- **Constants**: Use PascalCase for constants and prefix them with a descriptive term. For example, `MaxRetryCount`, `DefaultTimeout`.

```csharp
public class RetryPolicy
{
    private const int MaxRetryCount = 5;
    private int currentRetryCount;

    public bool ShouldRetry()
    {
        return currentRetryCount < MaxRetryCount;
    }
}
```

### Case Styles

Different programming languages and contexts use different case styles. Here are some of the most common ones:

- **PascalCase**: Each word in the identifier starts with an uppercase letter. Commonly used for class names, method names, and public properties. Example: `CustomerOrder`, `CalculateTotal`.
- **camelCase**: The first word starts with a lowercase letter, and subsequent words start with an uppercase letter. Often used for variables, function parameters, and private methods. Example: `customerName`, `processOrder`.
- **snake_case**: Words are separated by underscores, with all letters in lowercase. Frequently used in scripting languages and for file names. Example: `customer_name`, `process_order`.
- **kebab-case**: Similar to snake_case, but uses hyphens instead of underscores. Typically used for URLs and CSS class names. Example: `customer-name`, `process-order`.

#### PascalCase

Each word in the identifier starts with an uppercase letter. Commonly used for class names, method names, and public properties.

Pascal case is similar to camel case, but the first letter of the first word is also capitalized. This style was popularized by the Pascal programming language, which emphasized readability and structured programming.

**Example:**

- Class: `CustomerOrder`
- Method: `CalculateTotal`
- Property: `CustomerName`

#### camelCase

The first word starts with a lowercase letter, and subsequent words start with an uppercase letter. Often used for variables, function parameters, and private methods.

Camel case is a naming convention where the first letter of the first word is lowercase, and the first letter of each subsequent word is capitalized. It originated from the practice of abbreviating long names in early programming languages like C.

**Example:**

- Variable: `customerName`
- Parameter: `orderId`
- Private Method: `processOrder`

#### snake_case

Words are separated by underscores, with all letters in lowercase. Frequently used in scripting languages and for file names.

Snake case uses underscores to separate words and all letters are lowercase. This style comes from early programming practices in languages like Python and C, where underscores were used to improve readability in lowercase-only text environments.

**Example:**

- Variable: `customer_name`
- Function: `process_order`
- File Name: `customer_data.txt`

#### kebab-case

Similar to snake_case, but uses hyphens instead of underscores. Typically used for URLs and CSS class names.

**Example:**

- URL: `customer-name`
- CSS Class: `process-order`

---

### Special Considerations

#### Avoiding Ambiguity

Choose names that are unambiguous and clearly convey their purpose. Avoid using single-letter names, except for loop counters like `i`, `j`, and `k`. Instead of using vague names like `data` or `info`, be specific about what the variable represents, such as `customerData` or `orderInfo`.

#### Length and Descriptiveness

While names should be descriptive, they shouldn't be excessively long. Strive for a balance between clarity and brevity. For instance, `calculateOrderTotal` is more descriptive than `calcTotal`, but not unnecessarily verbose like `calculateTotalOfAllOrdersInSystem`.

#### Prefixes and Suffixes

Using prefixes and suffixes can add context to names, especially for distinguishing between different types of entities. For example, `is` or `has` for boolean variables (`isAvailable`, `hasPermission`), `min` or `max` for range values (`minLength`, `maxHeight`), and `list` or `array` for collections (`customerList`, `orderArray`).

Naming conventions are the foundation of readable and maintainable code. Consistent naming makes it easier for everyone on the team to understand and navigate the codebase. In C#, we use PascalCase and camelCase naming conventions to distinguish between different types of identifiers.

PascalCase capitalizes the first letter of each word and is used for naming classes, methods, and properties. For example, `Customer`, `CalculateTotal`, and `OrderDate` are all written in PascalCase. On the other hand, camelCase starts with a lowercase letter and capitalizes the first letter of each subsequent word. This convention is used for local variables, parameters, and private fields. Examples include `customerName`, `orderId`, and `_logger`.

### Tips for Consistent Naming Conventions

1. **Consistency is Key:** Stick to the chosen naming convention throughout your project.
2. **Descriptive Names:** Use clear, descriptive names that convey the purpose of the variable, function, or method.
3. **Avoid Abbreviations:** Abbreviations can be confusing; prefer full words unless they're widely understood.
4. **Context Matters:** Ensure names provide context about the data they hold or the function they perform.

---

### Class Naming

Class names should be clear and descriptive, reflecting the purpose or role of the class. They should be written in PascalCase and typically consist of a noun or noun phrase. For instance, a class representing a customer might be named `Customer`, while a class responsible for processing orders could be named `OrderProcessor`.

```csharp
public class OrderProcessor
{
	// Class implementation
}
```

When creating specialized versions of a base class, use a descriptive prefix or suffix to indicate the relationship. For example, `Customer` could be a base class, with `PremiumCustomer` and `RegularCustomer` as derived classes.

### Method Naming

Method names should clearly describe the action or behavior they perform. Use PascalCase for method names, and start each name with a verb. For example, `CalculateTotal`, `ProcessOrder`, and `GenerateInvoice` are all effective method names.

```csharp
public class InvoiceService
{
	public void GenerateInvoice(Customer customer)
	{
		// Method implementation
	}
}
```

Methods that return a boolean value should be named to indicate a yes/no or true/false condition. Common prefixes include `Is`, `Can`, `Has`, and `Should`, such as `IsAvailable`, `CanExecute`, `HasPermission`, and `ShouldRetry`.

### Property Naming

Properties represent the characteristics or data of a class. They should be named using PascalCase and should be descriptive of the value they represent. For instance, `CustomerName`, `OrderDate`, and `TotalAmount` are clear and descriptive property names.

```csharp
public class Order
{
	public string CustomerName { get; set; }
	public DateTime OrderDate { get; set; }
	public decimal TotalAmount { get; set; }
}
```

Avoid using abbreviations or acronyms unless they are widely recognized and commonly used in the domain of the application.

### Variable Naming

Variables are used to store data and should be named using camelCase. The name should be descriptive enough to convey the purpose or content of the variable. For example, `customerName`, `orderId`, and `totalAmount` are clear and descriptive variable names.

```csharp
public class OrderProcessor
{
	private readonly ILogger _logger;
	private int currentRetryCount;

	public OrderProcessor(ILogger logger)
	{
		_logger = logger;
		currentRetryCount = 0;
	}
}
```

For loop variables, it's acceptable to use short names like `i`, `j`, and `k`, especially in short loops. However, for longer or nested loops, use more descriptive names.

### Constant Naming

Constants represent fixed values that do not change during the execution of a program. They should be named using PascalCase and should be prefixed with a descriptive term if necessary. For example, `MaxRetryCount` and `DefaultTimeout` are good constant names.

```csharp
public class RetryPolicy
{
	private const int MaxRetryCount = 5;
	private const int DefaultTimeout = 30; // in seconds
}
```

Using descriptive names for constants helps in understanding their purpose and usage within the code.

### Private Field Naming

Private fields are used to store data within a class. They should be named using camelCase and prefixed with an underscore (_) to distinguish them from local variables and method parameters. This helps in quickly identifying private fields in the code.

```csharp
public class OrderProcessor
{
	private readonly ILogger _logger;
	private int _currentRetryCount;

	public OrderProcessor(ILogger logger)
	{
		_logger = logger;
		_currentRetryCount = 0;
	}
}
```

### Parameter Naming

Parameters are variables passed to methods to provide input data. They should be named using camelCase and should be descriptive of their purpose. For example, `customerName`, `orderId`, and `totalAmount` are appropriate parameter names.

```csharp
public void ProcessOrder(int orderId, string customerName, decimal totalAmount)
{
	// Method implementation
}
```

Avoid using single-letter parameter names, except for very short and commonly understood abbreviations like `x` and `y` in mathematical computations.

---

## Code Comments

Effective comments are essential for maintaining clear and understandable code. They provide context and explanations for complex or non-obvious parts of your code. Comments should be concise yet informative, focusing on the "why" rather than the "what."

### Single-line Comments

Use `//` for short, single-line comments. Place them above the code they refer to, or at the end of the line if they are brief.

```csharp
public int CalculateFactorial(int number)
{
	if (number <= 1)
	{
		return 1; // Base case: factorial of 0 or 1 is 1.
	}
	return number * CalculateFactorial(number - 1); // Recursive case.
}
```

### Multi-line Comments

For longer, multi-line comments, use `/* */`. These comments can span multiple lines and are useful for explaining more complex logic.

```csharp
/*
 * This method calculates the factorial of a given number.
 * It uses a recursive approach to compute the result.
 * Base case: factorial of 0 or 1 is 1.
 * Recursive case: number * factorial of (number - 1).
 */
public int CalculateFactorial(int number)
{
	if (number <= 1)
	{
		return 1;
	}
	return number * CalculateFactorial(number - 1);
}
```

### XML Documentation Comments

Use `///` to create XML documentation comments. These comments can be used by tools like IntelliSense in Visual Studio to provide documentation for your code.

```csharp
/// <summary>
/// Calculates the factorial of a given number.
/// </summary>
/// <param name="number">The number to calculate the factorial for.</param>
/// <returns>The factorial of the specified number.</returns>
public int CalculateFactorial(int number)
{
	if (number <= 1)
	{
		return 1;
	}
	return number * CalculateFactorial(number - 1);
}
```

---

For further reading and best practices, check out the following resources:
- [C# Coding Standards](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)
- [PHP: The Right Way](https://phptherightway.com/)
- [JavaScript Style Guide](https://github.com/airbnb/javascript)
- [CSS Naming Conventions](https://css-tricks.com/naming-conventions-in-css/)
- [SQL Naming Conventions](https://www.sqlshack.com/sql-naming-conventions/)
