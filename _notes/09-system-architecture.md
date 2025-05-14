# System Architecture

- The system architecture is the big picture ot what the system is and how it works.
- It answers the following questions:
  - How will the system work under heavy load?
  - What will happen if the system will crash at this exact moment in the business flow?
  - How complicated can be the update process?
- It includes the following aspects:
  - Defining the Software Components (Services)
  - Defining the way the components communicate with each other
  - Designing the System's capabilities (Scalability, Redundancy, Performance, etc.)
- The main topics are:
  - **Loose Coupling:** The components should be as independent as possible. This means that if one component fails, the others should still work.
  - **Stateless:** The components should not store any state to prevent redundancy and to make the system more scalable.
  - **Caching:** The components should cache the data they need to prevent unnecessary calls to the database.
  - **Messaging:** The components should communicate with each other using messages that transfer data between them.
  - **Logging & Monitoring:** The components should log and monitor their activity to detect problems and to improve the system.

## Loose Coupling

- This means to be sure that the services are not strongly tied to each other.
- A service should not force another service to use a specific API
- Changing an URL in a service should not break the other services, in fact the impact should be minimal or none.
- A good way to handle this is through a **Gateway**
  - It's a middleman that orchestrates the communication between the services
  - It provides URLs to the services that won't change when the services change

## Stateless

- The application state (application data) is stored only in two places:
  - The database
  - The client
- The application should not store any state in the server because it will lead to:

  - A scale up problem
  - The system won't work if the resource is not available, for example if the server is down the stateful logic will be down as well, on the other hand, a stateless logic will work if we run it on another server.

    ```
    User Interface
    +----------------+
            |
    +----------------+
    Load Balancer    | -> It distributes the load between the servers and points only to live servers
    +----------------+
            |
    +----------------+
    Multiple servers
    running the API
    service
    +----------------+
            |
    +----------------+
    Database
    +----------------+
    ```

## Caching

- Caching brings the data closer to the consumer to reduce the latency and the load on the database.
- It's an intermediate layer between the database and the data access layer.
- It usually stores the data in the application memory which makes it extremely fast, especially if the data is stored in the same server.
- The cache should be updated when the data in the database is updated.
- The main tradeoff of caching is that the reliability is poor, so we need to use it wisely
  - Rule of thumb is to cache data that is frequently accessed and rarely modified (synchronization is expensive)
  - Each server has its own cache, so if we have multiple servers we need to make sure that the data is consistent across all of them to avoid staling
- When the architecture has scale, instead of in-memory service we might need a distributed cache:
  - There are battle tested libraries that handle this, usually with concurrent collection
  - It's an external product that stores the data in an external process and provides an interface to access that data with a virtually unlimited size
  - The size of the cache is limited to the process's memory
  - The main tradeoff is performance, and that it usually only stores primitives

## Messaging

- This refers to the means of communication between the services.
- When selecting our messaging method we'll need to consider:
  - Performance: always prefer a faster method
  - Message size: Most systems have a limit on the size of the message
  - Execution model: Some systems require request/response, while others are more flexible
  - Feedback and reliability: It ensures that the message was delivered and processed successfully, if it fails it performs corrective action
  - Complexity: We need to know if the implementation is simple or complex
- The most common messaging methods are:
  - REST API
    - It's a request/response model
    - Performance is very fast
    - Message size is limited to the HTTP protocol usually 2MB
    - Execution model is request/response
    - Feedback and reliability is immediate via HTTP status codes
    - Complexity is low
    - It's the most common method and it's ideal for web applications
  - HTTP push notification
    - It's a subscription (web socket / long polling) model where the client subscribes to an event and the server pushes the data to the client when it satisfies the event
    - It uses advanced web technologies like WebSockets
    - Performance is excellent
    - Message size is limited to a few KB
    - It usually has no feedback and reliability since it fires and forgets
    - It's a very popular model for chat and monitoring applications
  - Queue
    - A queue is a middleman that stores the messages until they are processed
    - It delivers the messages to one or more consumers and after it's processed it deletes the message
    - It can be used to decouple the services and to improve the performance
    - Its performance is not so good since it adds latency
    - Message size is practically unlimited but it's preferred to keep it small
    - Its execution model is polling
    - It has very good feedback and reliability
    - Complexity requires training and setup, it usually uses a queue engine like RabbitMQ or Kafka
    - It's a very popular model for complex systems with lots of data when order and reliability are top priority
  - File-Based & Database-Based messaging
    - Similar to queues but instead of using a queue engine it uses a file or a database
    - It has very poor performance
    - Message size is unlimited
    - Execution model is polling
    - Feedback and reliability is very good
    - Complexity requieres training and setup
    - It's a very popular model for complex systems with lots of data but it's recommended to use a queue engine instead
- You can use a combination of these methods to achieve the best performance and reliability, just make sure to use the right method for the right job

## Logging & Monitoring

- Central logging service
  - It collects the logs from all the services and stores them in a central location, usually a database
  - It allows us to search and analyze the logs in real time
  - It can be used to detect problems and to improve the system
- Correlation ID
  - It's a unique identifier that is assigned to each request and is used to track the request across all the services
  - It allows us to trace the request and to find the root cause of the problem instead of searching for it in all the logs
  - It uses a correlation ID that links all the related logs together
