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












