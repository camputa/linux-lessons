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

### Special Considerations

#### Avoiding Ambiguity

Choose names that are unambiguous and clearly convey their purpose. Avoid using single-letter names, except for loop counters like `i`, `j`, and `k`. Instead of using vague names like `data` or `info`, be specific about what the variable represents, such as `customerData` or `orderInfo`.

#### Length and Descriptiveness

While names should be descriptive, they shouldn't be excessively long. Strive for a balance between clarity and brevity. For instance, `calculateOrderTotal` is more descriptive than `calcTotal`, but not unnecessarily verbose like `calculateTotalOfAllOrdersInSystem`.

#### Prefixes and Suffixes

Using prefixes and suffixes can add context to names, especially for distinguishing between different types of entities. For example, `is` or `has` for boolean variables (`isAvailable`, `hasPermission`), `min` or `max` for range values (`minLength`, `maxHeight`), and `list` or `array` for collections (`customerList`, `orderArray`).

Naming conventions are the foundation of readable and maintainable code. Consistent naming makes it easier for everyone on the team to understand and navigate the codebase. In C#, we use PascalCase and camelCase naming conventions to distinguish between different types of identifiers.

PascalCase capitalizes the first letter of each word and is used for naming classes, methods, and properties. For example, `Customer`, `CalculateTotal`, and `OrderDate` are all written in PascalCase. On the other hand, camelCase starts with a lowercase letter and capitalizes the first letter of each subsequent word. This convention is used for local variables, parameters, and private fields. Examples include `customerName`, `orderId`, and `_logger`.

### Case Styles

Understanding different case styles is essential for writing clear and maintainable code. Each style has its history and typical use cases in various programming languages. Here's a detailed look at the most common case styles, their origins, and their applications.

- **PascalCase**: Each word in the identifier starts with an uppercase letter. Commonly used for class names, method names, and public properties. Example: `CustomerOrder`, `CalculateTotal`.
- **camelCase**: The first word starts with a lowercase letter, and subsequent words start with an uppercase letter. Often used for variables, function parameters, and private methods. Example: `customerName`, `processOrder`.
- **snake_case**: Words are separated by underscores, with all letters in lowercase. Frequently used in scripting languages and for file names. Example: `customer_name`, `process_order`.
- **kebab-case**: Similar to snake_case, but uses hyphens instead of underscores. Typically used for URLs and CSS class names. Example: `customer-name`, `process-order`.

| Case Style | Description | Common Uses | Examples |
|---|---|---|---|
| PascalCase | Capitalizes the first letter of each word | Classes, Methods, Public Properties | `CustomerOrder`, `ProcessOrder` |
| camelCase | Starts with a lowercase letter, capitalizes subsequent words | Variables, Parameters, Private Methods | `customerName`, `orderId` |
| snake_case | Uses underscores to separate words, all lowercase | Variables, Functions, File Names | `customer_name`, `process_order` |
| kebab-case | Uses hyphens to separate words | URLs, CSS Class Names, HTML Attributes | `customer-info`, `order-history` |
| UPPER_CASE_SNAKE_CASE  | Uses underscores to separate words, all uppercase | Constants, Macro Definitions, Environment Variables | `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`|

#### PascalCase

PascalCase, also known as UpperCamelCase, capitalizes the first letter of each word in the identifier. It is named after the Pascal programming language, which was developed in the late 1960s and early 1970s by Niklaus Wirth. PascalCase became popular due to its readability and has been widely adopted in many modern programming languages.

Pascal was designed as a teaching language, emphasizing structured programming and data structuring. The use of PascalCase was intended to make code more readable and to help new programmers quickly understand the structure and purpose of identifiers.

**Common Uses:**

- **Classes:** `CustomerOrder`, `OrderProcessor`
- **Methods:** `CalculateTotal`, `ProcessOrder`
- **Public Properties:** `CustomerName`, `OrderDate`

```csharp
public class OrderProcessor
{
    public void ProcessOrder(int orderId)
    {
        // C# example
    }
}
```

**Pros:**

- **Readability:** PascalCase improves readability by clearly separating words, making it easier to understand the purpose of the identifier.
- **Standardization:** Widely used for naming classes, methods, and public properties in languages like C#, Java, and Swift, providing a consistent look across the codebase.
- **Professional Appearance:** The use of capital letters gives a formal and structured appearance, suitable for professional codebases.

**Cons:**

- **Length:** PascalCase can lead to longer identifiers, which may be cumbersome in contexts where brevity is preferred.
- **Initial Capital:** The initial capital letter may be less intuitive for variables or parameters, where lowercase is often expected.

PascalCase is ideal for naming classes, methods, and public properties, where readability and professional appearance are crucial. It helps distinguish these elements from variables and parameters, enhancing the overall structure of the code.

#### camelCase

camelCase, also known as lowerCamelCase, starts with a lowercase letter, and subsequent words start with an uppercase letter. It is commonly used for variable names and function parameters. The name camelCase comes from the "humps" of uppercase letters in the middle of the word, resembling the humps on a camel's back.

camelCase has been used since the early days of programming, but it gained significant popularity with the rise of object-oriented programming languages like Java and JavaScript in the 1990s. It offers a balance between readability and brevity, making it a favorite for identifiers that are frequently used.

**Common Uses:**

- **Variables:** `customerName`, `orderId`
- **Parameters:** `orderDate`, `productName`
- **Private Methods:** `processOrder`, `calculateDiscount`

```javascript
function processOrder(orderId, customerName) {
    // JavaScript example
}
```

**Pros:**

- **Readability:** Like PascalCase, camelCase improves readability by separating words with capital letters.
- **Conciseness:** Starting with a lowercase letter keeps identifiers shorter and more concise, especially for variables and parameters.
- **Common Usage:** Widely used for variable and parameter names in many programming languages, including JavaScript, Java, and Python.

**Cons:**

- **Mixed Usage:** The mix of lowercase and uppercase letters may be confusing for beginners who are not familiar with the style.
- **Less Formal:** camelCase may appear less formal compared to PascalCase, which might be a consideration for certain projects.

camelCase is ideal for naming variables, parameters, and private methods. Its concise and readable format makes it easy to follow, contributing to cleaner and more maintainable code.

#### snake_case

Words are separated by underscores, with all letters in lowercase. Frequently used in scripting languages and for file names.

Snake case uses underscores to separate words and all letters are lowercase. This style comes from early programming practices in languages like Python and C, where underscores were used to improve readability in lowercase-only text environments.

**Example:**

- Variable: `customer_name`
- Function: `process_order`
- File Name: `customer_data.txt`

```python
def process_order(order_id, customer_name):
    # Python example
```

**Pros:**

- **Readability:** The use of underscores clearly separates words, making it easy to read and understand.
- **Consistency:** Consistent lowercase letters enhance readability and reduce the risk of case-related errors.
- **History:** Widely used in languages like Python and Ruby, making it familiar to many developers.

**Cons:**

- **Verbosity:** The use of underscores can make identifiers longer, which might be cumbersome in certain contexts.
- **Inconsistent with Other Styles:** snake_case may look out of place in codebases that predominantly use camelCase or PascalCase.

snake_case is well-suited for variables, functions, and file names, particularly in languages where readability is prioritized. Its clear separation of words helps in understanding the purpose of identifiers.

#### kebab-case

Similar to snake_case, but uses hyphens instead of underscores. Typically used for URLs and CSS class names.

**Common Uses:**

- **URLs:** `customer-name`, `order-history`
- **CSS Class Names:** `customer-info`, `order-details`
- **HTML Attributes:** `data-customer-id`, `aria-label`

```css
.customer-info {
    /* CSS example */
}
```

**Pros:**

- **Readability:** Hyphens provide clear separation between words, enhancing readability.
- **Web Development:** Commonly used in web development for URLs, HTML attributes, and CSS class names, providing consistency across different web technologies.
- **SEO Friendly:** Hyphens in URLs improve search engine optimization (SEO) by making URLs more readable.

**Cons:**

- **Limited Use:** Not typically used in most programming languages for naming variables or functions.
- **Hyphen Confusion:** Hyphens can be mistaken for subtraction operators in some contexts, leading to potential confusion.

kebab-case is ideal for web development contexts, such as naming URLs, HTML attributes, and CSS class names. Its readability and SEO benefits make it a valuable choice for these scenarios.

#### UPPER_CASE_SNAKE_CASE

UPPER_CASE_SNAKE_CASE is a variant of snake_case where all letters are uppercase. It is commonly used for constants and macro definitions. The uppercase letters signal that the identifier represents a value that should not change.

This style has been used since the early days of C programming in the 1970s, where it was essential to distinguish constants and macros from variables. It remains widely used in many programming languages for its clarity and convention.

**Common Uses:**

- **Constants:** `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`
- **Macro Definitions:** `#define MAX_BUFFER_SIZE 1024`
- **Environment Variables:** `PATH`, `HOME`

**Example in C:**

```csharp
int MAX_RETRY_COUNT = 5
```

**Pros:**

- **Visibility:** Uppercase letters and underscores make constants and macros highly visible and distinguishable from other identifiers.
- **Clarity:** Clearly indicates that the value is a constant, reducing the risk of accidental modification.
- **History:** Long-standing convention in many programming languages, making it familiar to developers.

**Cons:**

- **Length:** Uppercase letters and underscores can result in lengthy identifiers, which might be cumbersome in some contexts.
- **Visual Noise:** The use of uppercase letters can create visual noise, making the code harder to read if overused.

UPPER_CASE_SNAKE_CASE is perfect for naming constants, macro definitions, and environment variables. Its clear and distinguishable format ensures that these values are easily recognizable and not accidentally modified.

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
