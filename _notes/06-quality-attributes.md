# Quality Attributes

- Technical capabilities that should fulfill the non-functional requirements of the system.

## Scalability

- Is the capacity of a system to grow without interrupting its current operations.
  - For example, a system that can handle 1000 users today should be able to handle 2000 users tomorrow without any issues, just by increasing computing resources, a good example of this is a Kubernetes cluster, where you can add more nodes to the cluster and the system will automatically distribute the load between them through a load balancer.
  - This is a concept called scaling out, the anti-pattern of this is scaling up, where you have to increase the capacity of a single node, for example, by adding more RAM or CPU to it. This is not a good practice because if that node goes down, the whole system goes down with it.

## Manageability

- Is the capacity to know the state of the system and to be able to take actions on it.
  - For example, a system that has a good logging system and monitoring system, where you can see the state of the system and quickly identify issues to fix them.
  - A bad system is one that needs the users to report the issues.

## Modularity

- Modularity makes the system more flexible for changes.
- A system that is modular is one that has a clear separation of concerns, where each module has a single responsibility and can be changed independently of the others.
  - For example, a system that has a clear separation between the UI and the business logic, where the UI can be changed without affecting the business logic and vice versa.
  - A bad example of this is a system that has a lot of dependencies between the modules, where changing one module requires changing all the others.

## Extensibility

- An extensible system is one that can be extended without changing the existing code.
  - For example, an endpoint that parses JSON and XML, and later on you want to add support for CSV, you can do that by adding a new parser without changing the existing code.
  - A bad example of this is a system that has a lot of if statements to handle different types of requests, where you have to change the existing code to add support for a new type of request.

## Testability

- This is the capacity of a system to be tested, the easier it is to test, the better.
- There are several ways to test a system, the worst one is to test it manually, where you have to go through the system and check if everything is working as expected, this is a bad practice because it is time consuming and error prone.
- A better way to test a system is to use automated tests, unit tests, integration tests, and end-to-end tests.
  - Unit tests: Test a single unit of code, for example, a function or a class.
  - Integration tests: Test the interaction between different units of code, for example, a function that calls another function.
  - End-to-end tests: Test the whole system, for example, a test that simulates a user interacting with the system.
