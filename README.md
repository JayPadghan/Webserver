# Web Server Project

This project demonstrates the implementation of three different Java-based server architectures, ranging from a basic single-threaded model to an efficient thread-pool-based system. Each implementation illustrates how Java handles socket connections and concurrency.

---

## Project Structure

The project is organized into three main packages representing different stages of server development:

### 1. SingleThreaded
- **Server.java**  
  A basic server that handles one connection at a time. It listens on port **8010**.
- **Client.java**  
  A simple client designed to connect to the server.  

### 2. Multithreaded
- **Server.java**  
  A server that spawns a new thread for every incoming client connection, allowing for concurrent processing.
- **Client.java**  
  A test client that spawns **100 threads** to simulate high concurrent load on the server.

### 3. ThreadPool
- **Server.java**  
  A scalable implementation using a **FixedThreadPool** (default size: **10**) to manage connections efficiently without the overhead of creating infinite threads.

---

## Getting Started

### Prerequisites
- Java Development Kit (JDK) **8 or higher**
- Apache **JMeter** (for performance testing)

---

## Testing with JMeter

Since these servers communicate over raw TCP sockets rather than HTTP, follow these steps to test performance using Apache JMeter.

### Configure the Test Plan

Open JMeter and create a new Thread Group.

Set:

- **Number of Threads (users):** 100 or higher
- **Ramp-up period:** 1 second

Right-click the Thread Group and select:

- **Add > Sampler > TCP Sampler**

Configure the TCP Sampler:

- **Server Name or IP:** localhost
- **Port Number:** 8010

### Add Listeners

To view the results, right-click the Thread Group and add:

- **View Results Tree** (to see individual responses like "Hello from server")
- **Summary Report** (to analyze throughput and latency)

### Run the Test

1. Start your desired server (e.g., `ThreadPool.Server`)
2. Click the Start button (green arrow) in JMeter
3. Observe how the Single-Threaded server struggles with high concurrency compared to the ThreadPool implementation

---

### Server Implementation Comparison

| Feature        | Single-Threaded Server        | Multi-Threaded Server                 | Thread Pool Server                   |
|---------------|------------------------------|--------------------------------------|-------------------------------------|
| Concurrency   | Handles one client at a time | Creates one thread per client        | Uses a fixed number of worker threads |
| Thread Usage  | No extra threads             | Unbounded thread creation            | Controlled thread creation           |
| Performance   | Poor under high load         | Better than single-threaded          | Stable and efficient                 |
| Resource Use  | Very low                     | High (risk under heavy load)         | Optimized and managed                |
| Scalability   | Not scalable                 | Limited scalability                  | Highly scalable                      |
| Best Use Case | Learning and debugging       | Moderate number of clients           | Production-like environments         |
