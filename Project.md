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

- On mysql server Linux Server install MySQL Server software.
```
sudo apt install mysql
```
![alt](./Images/Install%20Mysql%20on%20Server.JPG)
- On mysql client Linux Server install MySQL Client software.
```
sudo apt install mysql
```
![alt](./Images/Install%20Mysql%20on%20client.JPG)

- Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.
![alt](./Images/Sql%20Secuorty%20group%20port%20addition.JPG)

- You might need to configure MySQL server to allow connections from remote hosts.
```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
Replace ‘127.0.0.1’ to ‘0.0.0.0’

![alt](./Images/sudo%20vi-etc-mysql-mysql.conf.d-mysqld.JPG)

- From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH. You must use the mysql utility to perform this action.
next action will be to link the two Sql server and client.
 `` mysql -u username -h mysql_server_ip -p``
 ``sudo ufw allow from remote_ip_address to any port 3306``
 