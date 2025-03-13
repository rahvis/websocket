# websocket
Notes on websocket

<img width="700" alt="image" src="https://github.com/user-attachments/assets/4641acbf-8656-4bb0-aaab-496b5a43d4ac" />

<img width="700" alt="image" src="https://github.com/user-attachments/assets/c162201b-2594-4584-991c-eba110278a16" />

The WebSocket technology includes two core building blocks:

• The WebSocket protocol. Enables communication between clients and servers over
the web, and supports transmission of binary data and text strings. 

• The WebSocket API. Allows you to perform necessary actions, like managing the
WebSocket connection, sending and receiving messages, and listening for events
triggered by the server.

<img width="700" alt="image" src="https://github.com/user-attachments/assets/5456b943-61a2-4d6e-9bfc-d6d8d05cf244" />

<img width="649" alt="image" src="https://github.com/user-attachments/assets/2321c5c3-5305-4c2f-b4a7-768fb1f8ef10" />

## Use cases and benefits

# WebSocket Technology Overview

WebSocket technology has broad applicability. It can be used for various purposes, such as:

- Streaming data between backend services.  
- Connecting a backend with a frontend via long-lasting, full-duplex connections.  

In essence, WebSockets are an excellent choice for architecting **event-driven systems** and building **realtime apps and services** where immediate data delivery is essential.

## WebSocket Use Cases

We can broadly group WebSocket use cases into two categories:

### 1. **Realtime Updates**
- Communication is **unidirectional**, where the server streams low-latency (and often frequent) updates to the client.  
- Examples include:  
  - Live sports updates  
  - Alerts  
  - Realtime dashboards  
  - Location tracking  

### 2. **Bidirectional Communication**
- Both the client and the server can **send and receive messages**.  
- Examples include:  
  - Chat applications  
  - Virtual events  
  - Virtual classrooms (often with features like polls, quizzes, and Q&As)  
- WebSockets can also support **multi-user synchronized collaboration**, such as multiple people editing the same document simultaneously.

## Key Benefits of Using WebSockets

### Improved Performance
- Compared to HTTP, WebSockets eliminate the need for a new connection with every request.  
- Each message is significantly smaller since WebSocket messages lack HTTP headers.  
- This improves latency, reduces bandwidth consumption, and makes WebSockets more scalable than HTTP.  
- While scaling WebSockets can be challenging, they are **less taxing on server resources** at scale.

### Extensibility
- WebSockets offer flexibility through **subprotocols** (application-level protocols) and **extensions** for additional functionality.  

### Fast Reaction Times
- As an **event-driven technology**, WebSockets allow data to be transferred without the client explicitly requesting it.  
- This makes WebSockets ideal for scenarios where the client must react quickly to unpredictable events, such as **fraud alerts**.

WebSocket technology is powerful for building fast, efficient, and scalable real-time applications with dynamic data flow.

<img width="649" alt="image" src="https://github.com/user-attachments/assets/205ff861-8a41-4b1f-b04f-384362f98df2" />

<img width="534" alt="image" src="https://github.com/user-attachments/assets/15f45ff0-9efb-4a26-bae6-32784dc32201" />

<img width="699" alt="image" src="https://github.com/user-attachments/assets/27a8179f-fd39-45ba-9a23-cad4b37c52eb" />


https://github.com/ably-labs/react-websockets-tutorial.git


![WebSocket Demo](https://github.com/ably-labs/react-websockets-tutorial/blob/master/media/demo.gif)

## Scaling the Web App  

When building a WebSocket-based web application, scaling is a crucial consideration to ensure performance, reliability, and seamless user experience as your user base grows.

### Understanding the Current Setup
In this context, the Node.js WebSocket server maintains **state information** about connected clients using a **Map**. This Map tracks each active WebSocket connection along with its associated metadata (e.g., user identity, session details, etc.).

### The Limitation of a Single Server
Since this state is stored directly in the WebSocket server, every client must remain connected to the **same WebSocket server** for the system to function correctly. This introduces a scalability limitation:

- The total number of users you can support depends on the available resources (CPU, memory, etc.) on that single server.
- While Node.js efficiently handles concurrent connections, the number of concurrent users will eventually hit a performance limit as the server's hardware capacity is exhausted.

### Vertical Scaling (Scaling Up)
One way to address this limitation is through **vertical scaling**, which involves upgrading the server's hardware:

- Increasing CPU cores  
- Expanding RAM  
- Improving network bandwidth  

Although vertical scaling can temporarily handle higher traffic, it has notable drawbacks:

- **Cost Inefficiency:** Upgrading to powerful hardware can become expensive.  
- **Limited Growth:** Even the most powerful hardware has a performance ceiling, restricting your ability to scale beyond that limit.  
- **Inflexibility:** Vertical scaling is not elastic — scaling must be done proactively, making it challenging to adapt to sudden traffic spikes.

### Horizontal Scaling (Scaling Out)
A more effective long-term solution is **horizontal scaling**, which involves distributing WebSocket connections across multiple servers:

- Instead of relying on one powerful server, multiple smaller servers (often called **nodes**) share the workload.  
- This strategy allows you to add or remove servers dynamically based on demand, making your system **elastic** and **cost-efficient**.  
- However, horizontal scaling introduces complexity because you must manage session data across multiple servers.

### Managing State in a Scaled Environment
Since WebSocket connections are stateful, distributing state information across multiple servers requires additional infrastructure:

- **Session Affinity (Sticky Sessions):** Ensures that a client’s requests are always routed to the same server.  
- **Centralized State Management:** Externalizing session data in systems like **Redis**, **MongoDB**, or **DynamoDB** allows multiple servers to access shared state data.  
- **Load Balancers:** Tools like **NGINX**, **HAProxy**, or **Azure Load Balancer** efficiently distribute incoming connections across multiple WebSocket servers.

### Choosing the Right Scaling Strategy
- **Start with Vertical Scaling** if your user base is small or your traffic patterns are predictable.  
- **Embrace Horizontal Scaling** if your app needs to support thousands of concurrent users, handle unpredictable spikes, or ensure high availability.

By designing your WebSocket infrastructure with scalability in mind, you can build a robust system capable of delivering real-time data efficiently while accommodating future growth.



# What Makes WebSockets Hard to Scale?

WebSockets are inherently challenging to scale due to the persistent nature of their connections and the complexity of managing state across multiple servers.

## Persistent Connections
Unlike traditional HTTP requests, WebSocket connections are **persistent**. This means that once a connection is established, it remains open for the duration of the session. As a result, each WebSocket server must maintain an active connection for every connected client. This persistence increases the complexity of scaling because:

- Each WebSocket connection consumes resources (memory, CPU, etc.).  
- Scaling your server layer involves ensuring new instances can handle additional persistent connections.  

## Managing Shared State
Even after scaling your WebSocket server layer, maintaining a **consistent view of state** across all nodes becomes a challenge. Since WebSocket servers only know about the clients connected to them, a mechanism for sharing state between nodes is essential.

### Solutions for Sharing State
To ensure all nodes have the same view of the connection state, data must be stored **out-of-process**. This is typically achieved using technologies such as:

- **Redis**: A fast, in-memory data store that efficiently manages session data across multiple nodes.  
- **Traditional Databases**: Useful for persisting session data but may introduce latency compared to Redis.  

## Broadcasting Challenges
When broadcasting messages to multiple clients:

- Each WebSocket server node only knows about the clients directly connected to it.  
- Broadcasting to **all connected clients** requires additional coordination between nodes.  

### Solutions for Broadcasting
There are two primary approaches to enable effective broadcasting across scaled WebSocket servers:

1. **Direct Node Communication:** Establishing direct communication channels between WebSocket server nodes to relay messages.  
2. **External Pub/Sub Mechanism:** Implementing a **publish/subscribe (pub/sub)** system that acts as a central message hub.  

## Adding a Backplane
Implementing a pub/sub system or direct node communication introduces another layer of complexity, often referred to as **"adding a backplane"** to your infrastructure. This backplane ensures that messages and state updates are efficiently distributed across multiple WebSocket nodes.  

While adding a backplane improves scalability, it introduces additional moving parts, increasing maintenance complexity and potential points of failure.

Scaling WebSockets requires careful planning, especially around managing persistent connections, synchronizing state across nodes, and broadcasting messages effectively. Leveraging solutions like Redis or pub/sub systems can mitigate these challenges, but they add complexity to the overall system design.

## Horizontal Scaling and Its Complexities

Horizontal scaling introduces additional complexities compared to vertical scaling. While it provides the ability to expand your system's capacity effectively, achieving this requires careful architectural planning and infrastructure management.

### Key Challenges of Horizontal Scaling
1. **Complex Architecture:**  
   Horizontal scaling demands a more sophisticated system design. Instead of relying on a single powerful server, multiple servers must be organized to handle incoming requests efficiently.

2. **Infrastructure Management:**  
   Managing multiple WebSocket servers requires tools and processes to monitor performance, ensure uptime, and manage deployments effectively.

3. **Load Balancing:**  
   To distribute traffic evenly across multiple servers, a load balancer is essential. This component ensures that no single server becomes overwhelmed, improving both performance and reliability.

4. **Data Synchronization:**  
   One of the biggest challenges in horizontal scaling is ensuring that message data and connection state are synchronized across all WebSocket servers. Since WebSocket connections are persistent, maintaining real-time consistency across servers must happen within milliseconds to prevent data loss or duplication.

Despite these complexities, horizontal scaling is highly beneficial. It offers the potential for **limitless scalability** (in theory), making it a more flexible and powerful solution than vertical scaling. Instead of focusing on **"How many connections can my server handle?"**, a better question is:  
**"How many servers can I distribute the workload to?"**

### Importance of Elasticity in Scaling
Beyond implementing horizontal scaling, **elasticity** is crucial to maintaining system stability under unpredictable traffic patterns. The public internet is inherently volatile, and traffic spikes can occur suddenly. If your server layer is **inelastic**, these sudden surges may overwhelm your system, causing downtime or performance degradation.

To address this, your system should be designed to:

- **Dynamically scale up** by adding more servers when traffic increases.  
- **Scale down** during low-traffic periods to optimize costs.  

By ensuring your WebSocket infrastructure is both **scalable** and **elastic**, you can build a robust system capable of handling real-time communication at scale with minimal disruption.














