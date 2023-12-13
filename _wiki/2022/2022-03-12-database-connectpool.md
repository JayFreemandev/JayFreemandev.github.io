---
layout  : wiki
title   : Find the optimal number of connections with DBCP
date    : 2022-03-12 21:35:00 +0900
updated : 2022-03-12 21:35:00 +0900
resource: CE/7B98C2-F86D-46A9-949B-56BAA0135AF6
toc     : true
public  : true
parent  : [[/2022]]
latex   : true
---
* TOC
{:toc}

When an API request comes from the backend server and accesses the DB, there is a process that receives the DB request 
and response. This communication uses the TCP network because of its high reliability. The part that should be noted is 
the operation process of TCP.

![image](https://user-images.githubusercontent.com/72185011/220371260-745afabd-f204-47f6-802b-6be185321ad4.png)

### **Connection Lifecycle**  
Before diving into Database Connection Pooling (DBCP), it's crucial to understand the typical connection lifecycle. 
Connections are opened before a query is requested and closed after the response is received. However, the traditional 
3-way and 4-way methods of opening and closing connections for each request are not efficient, leading to increased 
server costs and slower response times.

To solve this problem, the DBCP concept exists.

### **Introduction to DBCP**  
Database Connection Pooling (DBCP) is a solution designed to address the inefficiencies of the traditional connection 
methods. Instead of repeatedly opening and closing connections, DBCP involves accessing and allocating pre-made 
connections, reusing them, and returning them to a connection pool when closed. This significantly reduces the time and 
resources required for connection management.

### **max_connection**  
The term "max_connection" refers to the maximum number of connections that can be established with the database 
simultaneously. If the max_connection is already in use and a new server is added, it cannot be distributed efficiently. 
Properly setting max_connection is essential for optimal performance.

### **wait_timeout**  
To prevent idle connections from occupying resources indefinitely, a "wait_timeout" can be set. 
This timeout determines how long a connection will wait before being closed if it remains idle. For example, 
if set to 60 seconds, the connection will be closed if not used within that timeframe.

You can set a wait_timeout to avoid the weird phenomenon of a connection being occupied but not used. 
If you set it to 60 seconds, it will wait 60 seconds before deciding whether to close. 
If a timed request occurs before the end of the wait_timeout, the request will be received, processed, initialized to 0,
and returned after waiting 60 seconds.

### **Setting up DBCP on the server**  
It is recommended to set "minimumIdle" and "maximumPoolSize" to the same value. This ensures that there are enough 
connections available, avoiding the need to create new connections during heavy traffic, which incurs additional costs.

### **Finding the right number of connections**  
To determine the optimal number of connections, it's crucial to set up a monitoring environment and conduct 
load stress tests. Metrics such as Request per second and Avg response time provide insights into server performance 
under different loads.

you can use such tools ngrinder or jmeter 

- Request per second
   - How many requests can be processed per unit second
- avg response time
   - How long is the average response time for a request

### **Expected scenario**

1. Check the CPU and MEM utilization of your backend server and DB server.

If the resource usage of the server goes up when the traffic load goes up to a certain level, 
you can add more servers to distribute it, and if the DB server's utilization goes up and most of it is due to READ, 
you can increase the DB's SECONDARY because it is using replication. There are other methods such as sharding.

2. check thread per request

If the resource utilization of the backend server and DB server is stable under traffic load, 
but the graphs of Request per second and Avg response time are slowly declining, I would check the thread per request. 
This is because the response may be delayed due to insufficient number of active threads.

3. maximumPoolSize

If the thread count is slow even though there are 100/50 active, check the number of active connections in DBCP and see 
if all 5 of the maximumPoolSize are being used. If so, increase the maximumPoolSize. Note that the max_connections of the 
DB server should be more than that, so that you can respond to additional servers (adding spare servers) in a leisurely manner.

## **conclusion**  
Determine the max pool size of DBCP based on the number of backend servers to be used. This ensures that the connection 
pool can effectively handle the expected load, providing optimal performance and resource utilization.