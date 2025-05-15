# Architecture Document

- This document is a high-level overview of the system architecture.
- It provides a summary of functional and non-functional requirements, design decisions, and technology stack.
- It's not a development document, and it should be defined in the early stages of the project.

## Goal of the Document

- The main goal is to describe what should be done and how it should be done and lay out the functional and non-functional requirements, here is the first time they're explained.
- The document should be a living document, and it should be updated as the project evolves.

## Audience

- This document is intended to be read by almost anyone involved in the project, including:
  - Project managers, CTO, CEO
    - They should be able to understand the high-level overview of the system architecture and trust that the project is on the right track and according to the business goals.
    - There should be a executive summary that describes the best practices and the patterns used in the project.
  - QA lead
    - This document will help them to be prepared for the testing phase, like preparing the servers, the tools, the environment, etc.
  - Developers
    - Developers should put special attention to the technology stack, components, services, communication, etc.

## Contents of the Document

- There is not just one right way to write an architecture document, but there are some common conventions.
- **UML (Unified Modeling Language)** is a standard way to visualize the design of a system.
  - This is a graphical language for visualizing, specifying, constructing, and documenting the artifacts of a software system.
  - It's good when most of the team is technical but it's not a good idea when the document is intended to be read by non-technical people.
- **Plain Text** is a good way to write the document when the audience is not technical.
  - It's easier to read and understand by the audience.
  - Try not to use too much technical jargon and try to explain the concepts in a simple way.
  - Use simple to understand graphs and diagrams to explain the concepts.
  - It can be written in the software you're most comfortable with, like Word, Google Docs, etc.

## Document Structure

- The document should be divided into sections, and each section should have a clear purpose.

### Background & Overview Section

- This should be short, one page maximum.
- The main audience is the team and the management.
- You should describe the system from a business perspective.
  - Which is going to be the system's role
  - Reasons to create or change the system
  - What is the expected business impact
- This section should validate the perspective of the system since the beginning because if it changes, the architecture should change too.

### Requirements Section

- This should also be short, one page maximum, and the main audience is the team and the management as well.
- Here we describe the various requirements for the system.
  - Functional requirements (always start with this and try to keep them below 5)
    - What the system should do
    - Use cases, user stories, etc.
  - Non-functional requirements (they should be extremely accurate because is the only place where they are described)
    - How the system will deal with
    - Performance, security, scalability, etc.
- All the requirements should be listed in a bulleted list and with no more than three lines per item.
- Including them in the document is important because they validate your understanding of the system and the business goals.
- They dictate the architecture and the technology stack.

### Executive Summary Section

- This section is a bit more extensive than the previous ones, usually two or three pages and its audience is the management.
- This section presents the system in a high-level overview, without technical detail.
- It is basically a summary of the system with simple to understand language, charts and diagrams that will make the management understand the system and why it was built this way.
- Even though this section is before the architecture overview and the components drill down, it should be written at the end of the document to have a better understanding of the system.
- Although this section is not technical, it should follow the DRY principle and the information should'nt be redundant with other sections.

### Architecture Overview Section

- This section should be written in a technical way without getting too deep into the details.
- It is the most extensive section of the document (usually 5-10 pages) and its audience is the development team and the QA lead.
- This section describes a high-level overview of the system architecture and presents it to the team.
- It doesn't deep dive into the components, but it describes the architecture and the technology stack.
- Its parts are:
  - General description of the system:
    - Type of system (web, mobile, etc.)
    - Major NF-Requirements (general performance, security, microservices, etc.)
  - High-Level Diagram:
    - A diagram that shows the components of the system and how they interact with each other.
    - It should be simple and easy to understand (just the logic behind the system, no technical details).
  - Walkthrough of the diagram:
    - A description of the diagram in text format with simple to understand language.
    - It includes the relevant details of the components only.
- Tech stack:
  - A list of the technology stack used in the system.
  - If the stack is single it can be included here, but if it has several stacks, it should be general here and then deep dive into each stack in the components drill down section.

### Components Drill Down Section

- This section is the most technical and important part of the document and it dives deep into the components of the system.
- It doesn't have an average length because is as extensive as the system requires, and its audience is the development team and the QA lead.
- This section goes through the various components of the system and describes them in detail in different subsections.
  - Component's role:
    - What is the component's role in the system.
    - Component's technology stack and the reasons to use this technology stack.
    - Component's Architecture (if it has one), for example:
      - For a REST API you might want to include a table with all the API endpoints, their role, response codes, comments, etc.
  - Not every component needs to be described in detail, if the child components are similar and the layer is already described, they can be grouped together.
  - Include important details like Dependency Injection, ORM, etc.
  - This part includes the development instructions for the component, like:
    - How to run the component
    - How to test it
    - How to deploy it
    - How to monitor it
