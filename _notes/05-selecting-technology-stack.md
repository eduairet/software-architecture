# Selecting Technology Stack

- It's very important because it's irreversible, if you choose the wrong technology stack it's most likely that you will have to rewrite the entire application if you want to change it.
- This should be done without emotion, it should be done with a lot of research and analysis, considering the team, the project, the budget, the time, the resources, choosing the trendier technology is not always the best option.

## Considerations

- You must be sure the technology can perform the task you want it to
- You must be sure the technology is well documented and maintained, and has a large community that can help you with unexpected issues
- You must find a technology that's popular but's not only hype, this will allow to make it easier to find more team members when the project scales

## Backend

- Some of the most popular backend technologies are:
  - Java
    - It was founded in 1995 by Sun Microsystems
    - It's very popular, and it's used by a lot of big companies
    - It's general purpose, object oriented, static typed
    - It's cross platform, it can run on any OS
    - It's great for web applications and web APIs
  - Python
    - It was founded in 1991 by Guido van Rossum
    - It quickly became the most popular scripting language and eventually the most popular programming language
    - It's general purpose, object oriented, dynamic typed
    - It's cross platform, it can run on any OS
    - It's great for web applications and web APIs but you can create any type of application with it
    - Since its performance is not the best, it's not the best option for CPU intensive tasks
  - Node.js
    - It was founded in 2009 by Ryan Dahl
    - It's a JavaScript runtime built on Chrome's V8 JavaScript engine
    - It's optimized for highly-concurrent Web Apps
    - It's dynamically typed but it can be statically typed with TypeScript
    - It's not targeted for long running applications, it's not the best option for CPU intensive tasks
    - It's great for I/O (input/output) intensive tasks
  - PHP
    - It was founded in 1994 by Rasmus Lerdorf
    - It's a server-side scripting language
    - It's dynamically typed but it can be statically typed with PHP 7
    - It's not a very clean language and it can easily lead to spaghetti code
    - It's not the best option for new projects, but it's still very popular and has a large community
    - It's great for web applications and web APIs and it's very popular for CMS (Content Management Systems) like WordPress
  - .NET
    - ASP.NET
      - Founded in 2001 by microsoft to use C# instead Java
      - It's general purpose, object oriented, static typed
      - It needs an IDE to work like Visual Studio or Rider
      - It's windows only
      - It's performance it's acceptable but not the best
      - It's very mature but it's not the best option for new projects since it's being replaced by .NET Core
    - Core
      - It's cross platform
      - It has a great performance
      - It has reached a maturity level that makes it a great option for new projects
      - It can be run without an IDE with any text editor

## Frontend

- The frontend is the part of the software the user interacts with (the User Interface or UI)
- It's used in web applications, mobile applications, desktop applications, and games (someone would argue that console as well but it is not the case)
- Some of the most popular frontend technologies are:
  - Web Applications (HTML, JavaScript, CSS):
    - Angular
      - It's a full framework (it includes everything you need to create a web application)
      - It has a long learning curve
    - React
      - It's a library and it needs a framework like Next.js to add capabilities like routing, server side rendering, etc.
      - It has a short learning curve
  - Mobile applications:
    - Native development
      - Swift with Xcode & iOS SDK
      - Java with Android Studio & Android SDK
      - It gives you the best performance and the best user experience
      - It takes a lot of time and effort, so it's just ideal for big companies with a lot of resources
    - Hybrid
      - It's a wrapper around a web application
      - It uses web technologies like HTML, JavaScript, and CSS
      - It has a very limited access to the device's hardware which derives in a limited performance and user experience
    - Cross-Platform
      - Xamarin (C# and Visual Studio)
      - React Native (JavaScript)
      - Flutter (Dart, C, C++ with Android Studio)
      - You write the code and compiles it into whatever platform you want to deploy it
      - It becomes bogus very quickly so we need to constantly updating versions
      - It doesn't work well with heavy graphics
  - Desktop applications:
    - Windows
      - WinForms: It's a wrapper around the Windows API and it uses C# and .NET and it's limited, the learning curve is short though
      - WPF: It uses XAML and the learning curve is long, but it gives more flexibility and power
      - UWP: It's used for PCs, XBox, IoT, etc. and it needs a Sandbox to run, which won't give you full OS access, the learning curve is long as well
    - MacOS
      - MacOS
        - AppKit: A framework for building native macOS applications using Objective-C or Swift. It provides a rich set of UI components and tools for creating macOS-specific user interfaces.
        - SwiftUI: A modern declarative framework introduced by Apple for building user interfaces across all Apple platforms, including macOS. It simplifies UI development and integrates seamlessly with Swift.
        - Catalyst: A framework that allows developers to bring their iPad applications to macOS with minimal changes. It enables code reuse between iPadOS and macOS.
        - Electron: A popular framework for building cross-platform desktop applications using web technologies like HTML, CSS, and JavaScript. While not macOS-specific, it is widely used for macOS apps.
        - Qt: A cross-platform application framework that supports macOS. It allows developers to write applications in C++ and deploy them on multiple platforms, including macOS.

## Data Store

- SQL
  - Relational databases (the databases relate together by foreign keys)
  - The most common are MySQL, Microsoft Server, Oracle, SQLite and Postgres
  - They store the data in tables, each table has columns, and each column has properties
  - They have the concept of transactions, which represent a set of actions and whether it's executed or not
    - Transactions are defined by the concept of ACID (Atomicity, Consistency, Isolation, and Durability)
  - They use the SQL language (Structured Query Language) to interact with the database
  - They're optimal for structured data (like a bank account) and not huge amounts of data (like the user data of a social network)
- NoSQL
  - They're called Non-Relational databases and they have a key/value structure (usually JSON)
  - Their emphasis is scale and performance
  - They don't have schemas
  - The most popular is MongoDB
  - Transactions here guarantee that it will be executed but not when which can temporarily lead to data inconsistencies
  - It has no specific querying language which can be difficult
  - They're optimal for a huge amount of data (posts from a social network) and non-structured data (like images, videos, etc.)
