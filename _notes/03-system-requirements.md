# System Requirements

- Requirements are always in high level, so it's our job as architects and developers to translate them into low level requirements.

## Non-Functional Requirements

- These requirements are related to what the system should deal with, not how it should do it, some examples are:

  - Performance
    - It should always be measured in time so we can compare it, and make it as fast as possible within its limits
    - Latency is the time it takes to process a request, and it should be as low as possible
    - Throughput is the number of requests processed in a given time, and it should be as high as possible
  - Load
    - It's the quantity of work the system can handle without crashing, for example the number of requests an API can handle concurrently
  - Data volume
    - This refers to how much data will the system accumulate over time
    - Here we'll need to decide which database to use and design optimized queries to make it more efficient
    - We'll need to calculate the size of the database on day 1, and how much it will grow over time
  - Concurrent users
    - This is the number of users that will be using the system at the same time
    - This is important to calculate the load and performance of the system
    - The rule of thumb is to multiply the number of users by 10, so if we have 1000 users, we should be able to handle 10,000 requests per second
  - SLA (Service Level Agreement)
    - This is the required uptime for the system, it varies across different providers, but it can guarantee >99.9% uptime
    - It's usually calculated from the expectative of the business

- The architect role for these requirements is to frame the requirement boundaries, estimating realistic numbers and making sure the system can handle the load
- Making good decisions choosing these will save us headaches in the future, like overpricing, overengineering, and underperformance

## Functional Requirements

- These requirements are related to what the system should do, some examples are:
  - User stories
  - Use cases
  - Business rules
  - Data model
  - User interface
  - API
  - Security
  - Integration
  - Deployment
- These are usually defined by the system analyst
