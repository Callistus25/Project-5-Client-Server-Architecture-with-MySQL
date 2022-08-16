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

- On mysql server EC2, install MySQL Server software.
```
sudo apt install mysql-server
```
![alt](./Images/Install%20Mysql%20on%20Server.JPG)
- On mysql client EC2, install MySQL Client software.
```
sudo apt install mysql-client
```
![alt](./Images/Install%20Mysql%20on%20client.JPG)

- Need to use mysql server's local IP address to connect from mysql client but need to configure the connection port. MySQL server uses TCP port 3306 by default, have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

![alt](./Images/Sql%20Secuorty%20group%20port%20addition.JPG)

- You might need to configure mySQL server to allow connections from remote hosts.
```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
Replace ‘127.0.0.1’ to ‘0.0.0.0’

![alt](./Images/sudo%20vi-etc-mysql-mysql.conf.d-mysqld.JPG)

- Restart mysql server afterwards with below command;

```
sudo systemctl restart mysql
```
![alt](./Images/Restart%20Mysql%20server.JPG)

- From mysql server, login to mysql and create a remote user and database for the client user to access. Use the commands below:
```
sudo mysql
```
- Create remote user
```
CREATE USER '<remoteusername>'@'%' IDENTIFIED WITH mysql_native_password BY '<password>';
```
where *< remoteusername>* and *< password>* in the above scenario need to be replaced. In my case, sample is like below;
```
CREATE USER 'callistus'@'%' IDENTIFIED WITH mysql_native_password BY 'Fearless';
```
![alt](./Images/create%20user%20success.JPG)

- Create a new database for the remote user using the below command;
```
CREATE DATABASE Test_data;
```
where Test_data is the name of the sample database.

![alt](./Images/create%20database.JPG)

- Grant privilege of all the database to the remote user using the below command;
```
GRANT ALL ON <databasename>.* TO '<remoteusername>'@'%' WITH GRANT OPTION;
```
In my case, i used ;

```
GRANT ALL ON Test_data.* TO 'callistus'@'%' WITH GRANT OPTION;
```
![alt](./Images/Database%20access%20granted%20to%20remoteuser.JPG)

- Flush the privileges.
```
mysql> FLUSH PRIVILEGES;
```
![alt](./Images/Flush%20privileges.JPG)

Then exit mysql server.

- From *mysql client*,  connect remotely to mysql server Database Engine without using SSH. You must use the *mysql* utility to perform this action.
Login to the *mysql server* from *mysql client* using the below command and the previously set password;

```
sudo mysql -u <remoteusername> -h <mysql_server_IP> -p
```
![alt](./Images/Login%20from%20client%20to%20server.JPG)


- Check and confirm that you have successfully connected to MySQL server and can perform SQL queries. Run the below command to show the existing databases.

 `` Show databases;
 ``
  ![alt](./Images/database%20connection%20success.JPG)

Connection success!

