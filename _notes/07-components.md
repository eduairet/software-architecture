# Components

- Software components (sometimes called services) are pieces of software that are designed to be reusable and do only one thing.
- A distributed system is a system that consists of multiple components that communicate with each other over a network.

## Levels of Software Architecture

- **Component's Architecture:** It deals with the internal components of a system and how they interact with each other.
- **System's Architecture:** This has the big picture of the system and needs to be scalable, reliable, fast, and easy to maintain.

## Layers

- A good architecture is layered. Each layer has a specific responsibility and communicates with the layers above and below it.
- They represent the horizontal functionalities of the system.
  - **UI (user interface) or SI (system interface):** Expose the user interface or API
    - Exposes the API
    - Handles the data objects (JSON, XML, etc.)
    - Authentication and authorization
  - **BL (Business logic):** Handle the logic of the system to achieve the business goals
    - Validation
    - Enrichment
    - Computation
  - **DAL (Data Access Layer):** Save and retrieve data
    - Connect to the database
    - Query the database and save the data
    - Handles transactions
- Separating the system into layers allows us to change the implementation of one layer without affecting the others, for example, we can change the database without affecting the business logic or the user interface.
- The layers can only communicate with the layers above and below them, not with the layers that are not directly connected to them.
- Loose coupling is a design goal that aims to reduce the dependencies between components, making them easier to change and maintain.
- Dependency injection is a design pattern that allows us to inject the dependencies of a component at runtime, making it easier to change the implementation of a component without affecting the rest of the system.
- The exception handling between layers should keep the inner exception within the layer and not expose it to the outer layers, instead of that, we should throw a custom exception that is meaningful to the outer layer.

## Layers vs. Tiers

- Layers are logical divisions of the system, while tiers are physical divisions of the system.
- A system can have multiple layers in a single tier or multiple tiers for a single layer.
- A tier is a physical separation of the system, for example, a web server, an application server, and a database server.

## Interfaces

- An interface is a contract that defines the methods and properties that a component must implement.
- Using interfaces allows us to keep the code decoupled and makes it easier to change the implementation of a component without affecting the rest of the system.
  ```C#
  public Main()
  {
    ICalculator calculator = GetInstance(); // The contract here is the interface
    // Always prefer to use interfaces instead of concrete classes
    double result = calculator.Add(1, 2);
    Console.WriteLine(result);
  }
  ```

## Dependency Injection

- Is a technique that allows us to supply the dependencies of a component to another component at runtime.

  ```C#
  // Factory Method
  private ICalculator GetInstance(CalculatorType type) // Can be set from the configuration manager as well
  {
    ICalculator calculator = null;

    switch (type)
    {
      case CalculatorType.Regular:
        calculator = new RegularCalculator();
        break;
      case CalculatorType.Scientific:
        calculator = new ScientificCalculator();
        break;
      case CalculatorType.Financial:
        calculator = new FinancialCalculator();
        break;
      default:
        throw new ArgumentException("Invalid calculator type");
  }
  ```

  ```C#
  // Constructor Injection

  public class HomeController : Controller
  {
    ILogger _logger;

    public HomeController(ILogger logger)
    {
      _logger = logger;
    }
  }

  // This approach is better since it makes the code more testable and decoupled
  [TestMethod]
  public void TestControllerInitialization()
  {
    // Arrange
    var logger = new Mock<ILogger>();
    var controller = new HomeController(logger.Object);

    // Act
    controller.Index();

    // Assert
    logger.Verify(l => l.Log(It.IsAny<string>()), Times.Once);
  }
  ```

## SOLID Principles

- **S**: Single Responsibility Principle (SRP)
  - A class should have only one reason to change.
  - A class should have only one responsibility.
  - A class should do only one thing.
- **O**: Open/Closed Principle (OCP)
  - A class should be open for extension but closed for modification.
  - A class should be able to add new functionality without changing the existing code.
- **L**: Liskov Substitution Principle (LSP)
  - A derived class should be substitutable for its base class.
  - A derived class should be able to replace its base class without affecting the correctness of the program.
- **I**: Interface Segregation Principle (ISP)
  - A class should not be forced to implement interfaces it does not use.
  - A class should have only the methods it needs.
- **D**: Dependency Inversion Principle (DIP)
  - High-level modules should not depend on low-level modules. Both should depend on abstractions.
  - Abstractions should not depend on details. Details should depend on abstractions.
  - This principle is the basis of dependency injection.

## Naming conventions

- It depends on the language, it defines the format of the code and should be followed by all the developers in the team.

  ```
  // Pascal case
  MyClass

  // Camel case
  myClass

  // Snake case
  my_class

  // Kebab case
  my-class

  // Upper case
  MY_CLASS -> Usually used for constants
  ```

- The naming conventions should be followed by all the developers in the team to keep the code consistent and readable.

  ```
  // Methods
  def get_user_name(self): # It has a verb and a noun
    pass

  // Variables
  user_name = "John Doe" # It has a noun
  is_active = True # It has a noun and indicates it's a boolean value

  // Constants
  MAX_USERS = 100 # It has a noun
  ```

## Exception Handling

- Only catch exceptions if you have something to do with them (logging does not count).
- Only catch specific exceptions, like DatabaseException, and handle them correctly.
- Use try catch only in small pieces of code

## Logging

- Logging can help to spot problems pretty quickly.
- It doesn't matter if the system is small or big, logging is always a good idea.
- The main purposes of logging are:
  - Track Errors: This will give us a start point to investigate the problem.
  - Gather Data: This will help us to understand how the system is being used (most visited components) and what are the most common problems (performance, errors, etc.).
  - User's Flow: This will help us to understand how the user is using the system and find patterns that can be improved.
- Make sure to store it in a safe place, like a database or a file that is not accessible to the user and you can consult later.
- It's usually a good idea to use battle-tested libraries for logging, like NLog, Serilog, or Log4Net.
