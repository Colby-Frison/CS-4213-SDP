# Assignment Instructions
1. Group Task:  
    - Think about a system you developed in the past (course project, internship, or personal project).  
    - OR recall a system you’ve used/encountered that you believe applied (or could have benefited from) the Singleton Pattern. 
    - OR find an online system applied (or could have benefited from) the Singleton Pattern.
2. Identify:  
    - What was the problem in that system?  
    - Why would a single shared instance be the right solution?  
3. Explain:  
    - If the system used Singleton: How was it implemented?  
    - If it did not use Singleton: How would you redesign part of it to use Singleton?    
4. Prepare to Share:  In your group presentation (3–4 minutes):  
    1. Briefly describe the system.  
    2. Show the problem and why Singleton fits.  
    3. Summarize your reasoning in a way other students can understand.

---
# Assignment
## System explanation

**System Description:**
	The project is a web application that utilizes Firebase for backend services. It involves both client-side and server-side components. The client-side is responsible for user interactions and directly initializes a Firebase app instance for each user session. The server-side, using Firebase Cloud Functions, manages server-side operations and initializes the Firebase Admin SDK.

**Problem and Why Singleton Fits:**
	The current design initializes a new Firebase app instance for each client-side user session. This means that every user creates their own connection to the database, leading to multiple simultaneous connections. This can cause performance bottlenecks and resource exhaustion, especially when the number of users increases. The Singleton pattern is ideal here because it allows us to centralize database access. By maintaining a single shared instance of the database connection on the server-side, we can reduce the overhead of establishing multiple connections and ensure consistent access to the database.

**Proposed Solution with Singleton:**

To address this issue, we propose implementing a backend service that acts as an intermediary between the client and the database. This service would maintain a single instance of the database connection using the Singleton pattern. Here's how it would work:

1. **Backend Service:** 
   - The backend service would be responsible for all database interactions. It would maintain a single connection to the database, ensuring that all client requests are funneled through this single point of access.

2. **Client-Server Communication:**
   - Clients would communicate with the backend service using WebSockets or RESTful APIs. Instead of each client directly connecting to the database, they would send requests to the backend service.

3. **Singleton Implementation:**
   - The backend service would implement the Singleton pattern to manage the database connection. It would check if a connection already exists and reuse it, rather than creating a new one for each request. This ensures that only one connection is maintained, reducing load and improving performance.

**Benefits of Using Singleton:**
- **Reduced Load:** By centralizing the database connection, we reduce the load on the database server, as it only has to manage a single connection.
- **Improved Performance:** This approach can significantly improve performance, as the overhead of establishing new connections is eliminated.
- **Scalability:** It makes the system more scalable, as the backend can handle multiple client requests through a single connection.

This solution not only addresses the current performance issues but also sets the foundation for a more scalable and efficient system. By using the Singleton pattern, we ensure that our database interactions are optimized and sustainable as the user base grows.

---
## System analysis
### Question 2: Identify the Problem and Why a Singleton is the Right Solution

- **Problem in the System:**
	- The current system initializes a new Firebase app instance for each client-side user session. This results in multiple database connections being established, which can lead to performance bottlenecks and resource exhaustion, especially with a high number of concurrent users.

- **Why a Single Shared Instance is the Right Solution:**
	- A single shared instance of the database connection, managed on the server-side, would centralize database interactions. This reduces the overhead of establishing multiple connections and ensures consistent access to the database. By using a Singleton pattern, the server can maintain a single connection that all client requests go through, improving efficiency and scalability.

### Question 3: Explanation of Singleton Implementation

- If the System Did Not Use Singleton:
	- The current client-side implementation does not fully utilize the Singleton pattern across user sessions. Each user session creates its own instance, leading to multiple connections.

- How to Redesign with Singleton:
	- Implement a backend service that acts as a mediator between the client and the database. This service would maintain a single instance of the database connection using the Singleton pattern.
	- Use WebSockets or RESTful APIs for client-server communication. Clients would send requests to the backend service, which would then interact with the database on their behalf.
	- The backend service would check if a database connection already exists and reuse it, rather than creating a new one for each request. This ensures that only one connection is maintained, reducing load and improving performance.
