# Case Study

## ASCII Type Generator

- A website that generates lettering artworks from users' inputs, it uses ASCII art alphabets created by other users to map the characters provided by the user.
- Users need to register to create their own ASCII artworks or upload their own alphabets, all their content is accessible via an user dashboard.
- The latest 10 artworks are initially displayed on the homepage but scrolling down will make more and more elements appear.
- Words can be searched by their name or by the name of the user who created them.

## Requirements

- **Functional Requirements**

  - Allow users to register, login, create/edit/delete ASCII artworks, and upload/delete their own ASCII alphabets.
  - Store the artworks and alphabets in a database, and show the artworks to other users, allowing them to search for them.
  - Add a revenue model to the website, allowing users to donate to the project by sending to a crypto Address, and by adding adds to the website.

- **Non-Functional Requirements**

  - Details:
    - Messages are created by the users, so the amount of data depends on the popularity of the website.
    - Since ASCII art is a nerdy topic from the old days of the internet, the website will probably not be very popular, so we can assume that the amount of data will be small.
    - Peak usage estimation: 100 users, 3 artworks per user, 1 alphabet per user since they can take a long time to create.
    - Expected artworks per month: 100×3×30=9000, where each artwork is approximately 1KB, giving us a total of 9MB of data per month.
    - Expected alphabets per month: 100×1×30=3000, where each alphabet is approximately 10KB, giving us a total of 150MB of data per month.
    - Yearly data:
      - Artworks: 9MB×12=108MB
      - Alphabets: 150MB×12=1.8GB
      - Total: 1.9GB
    - We need to ensure that the artworks and alphabets are stored to avoid data loss, so when there's an upload failure, the user should stay in the loop to try again.
    - Concurrent artworks and alphabets are expected to be less than 500, so we can assume that the database will be able to handle the load.
    - Concurrent users are expected to be less than 100
    - Total number of users is expected to be less than 1000
    - The SLA (Service Level Agreement) Level of the website should be Platinum:
      - Fully stateless
      - Easily scalable
      - Logged and monitored
  - Summary:
    - Data Volume: 1.9GB annually
    - Less than 100 concurrent requests
    - No data loss, keep the user in the loop
    - Less than 1000 users registered
    - SLA Level: Platinum

## Mapping the Components

- Receiver
  - User:
    - User ID
    - Registration date
    - Last update
    - Username
    - Password (hashed)
    - Email
    - Profile picture
    - GitHub id
  - The artworks and alphabets are stored in a database as text strings with their metadata.
    - Artworks:
      - Artwork ID
      - User ID
      - Creation date
      - Last update
      - Text
      - Art
    - Alphabets:
      - Alphabet ID
      - User ID
      - Creation date
      - Last update
      - Name
      - Description
      - Alphabet
  - Logging:
    - Request ID
    - Correlation ID
    - User ID
    - Request date
    - Request type
    - Message
- Handler:
  - Register:
    - It creates a new user in the database:
      - It can be done via GitHub without a password and account activation.
      - It can be done via email with a password and account activation.
  - Login:
    - It checks the credentials provided by the user and returns a token to be used in the next requests.
  - Artworks:
    - It processes and validates the text from an input provided by the user:
      - Authentication.
      - Invisible captcha.
      - The text is validated by just accepting ASCII characters.
      - The length of the text is limited to 20 characters.
  - Alphabets:
    - TXT files uploaded by the user:
      - Authentication
      - Invisible captcha
      - Validation:
        - They have only valid ASCII characters.
        - They are TXT files (prevent attacks).
        - They are les than 50kB.
        - They have the alphabet structure.
- Information provider
  - Artworks:
    - User Artworks: It returns the artworks of a user.
    - Latest Artworks: It returns the latest 10 artworks allowing pagination.
    - Artwork by name: It returns the artworks by their name.
    - Artwork by user name: It returns the artworks by their user name.
  - Alphabets:
    - User Alphabets: It returns the alphabets of a user.
    - Alphabets: It returns a catalog with all the alphabets.
    - Alphabet by name: It returns the alphabets by their name.
    - Alphabet by user name: It returns the alphabets by their user name.
- Logger:
  - Logs the requests made by the users to the database.
  - Logs the successful requests to the database.
  - Logs the request errors to the database.

## Choosing Messaging Methods

- Receiver
  - The receiver will be the rest API, it will be the entry point for the users to interact with the system.
  - Rest API is the best option here because it needs to respond to simple request and response messages to map the UI and to handle the user requests and the data.
  - It will use JWT tokens to authenticate the users and to authorize the requests.
- Handler
  - The data won't be very big, so transport it through JSON and TEXT responses wil be more than enough.
- Info
  - The UI is the is the info layer, it will be a web application that will be used by the users to create their artworks and alphabets.
- Data store
  - An SQL database will be used to store the data, we need this kind to make easier relations between the artworks, alphabets and users.
  - The database will be hosted in a cloud provider to make it easier to scale and to avoid data loss.
- Logger
  - The system can handle the logs in a database, because of the low volume of data it will be the same as the rest of the system just in a different table.
  - When a message is logged, a notification will be sent to a discord channel to notify the developers about the error.
