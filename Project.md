## Project-5- Client-Server-Architecture-with-MySQL ##

Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another. In their communication, each machine has its own role: the machine sending requests is usually referred as "Client" and the machine responding (serving) is called "Server"

![capture](./Images/Capture.JPG)

If we extend this concept further and add a Database Server to our architecture, it will be:

![capture1](./Images/Capture1.JPG)

In this case, our Web Server has a role of a "Client" that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network)

## Task ##
- Implement a Client Server Architecture using MySQL Database Management System (DBMS)

STEPS
- Create and configure two Linux-based virtual servers (EC2 instances in AWS).
```
Server A name - `mysql server`
Server B name - `mysql client`
```
![alt](./Images/Server%20naming.JPG)

