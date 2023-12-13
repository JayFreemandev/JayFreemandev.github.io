---
layout  : wiki
title   : How Springboot handle multiple requests(thread pool)
date    : 2023-01-29 20:44:40 +0900
updated : 2023-01-29 20:44:40 +0900
resource: A7/953B01-621E-4081-B40C-2BCDA2ECBBC3
toc     : true
public  : true
parent  : [[/2023]]
latex   : true
---
* TOC
  {:toc}

![img.png](../../resource/img/spring_boot/multiple_request.png)

Most of Server developer who use spring framework knew how spring dispatcher work flow started. However, 
Multiple request is far from their interest because spring framework handle it.
Servlet Container(Tomcat) in Spring handle multiple request. Default tomcat’s thread is 200. 
It work in one process and create thread pool to reuse when HttpRequest visit.

### **What is thread pool?**

The concept of Thread Pool is to generate the necessary Threads to run the program in earlier.

**Request per thread then multiple Servlet Context?**

How this thread can share one object in one controller? When we create a controller, Object saved in Heap but information 
about that class saved in Method Area(or Permenant Area) that mean whichever heap memory or method one every thread can 
share object’s information.

Therefore, we only need to call a method. no need to be synchronize. There are no problem 100,000 requests visit because
logic is shared already.

For example, Tomcat’s default thread is 200 but Hikari CP’s default is 10. Unless there is no state change. 200 thread can use 10 connection at the same time. that’s why stateless bean is singleton, not prototype.

**What is difference servlet container and spring container?**  
Servlet mean java based classes in Server. The container run multiple threads to process multiple requests to a single servlet.

**Isn't one thread assigned to one client? Each client operates on its own thread?**  
One thread per request. Container is not interested in who sent the request. New requests create new threads.

**Why is Thread-per-request preferred for Thread-per-connection?**  
It is advantageous for scalability. Java threads are expensive, with 1Mb memory segments attached one by one. 
It doesn't matter whether it's active or idle. If you attach it to one thread per connection, the thread will have to 
wait idle until the request continues.

Ultimately, the framework won't be able to make new connections because it can't make more trashThis means that the 
thread must be maintained while the connection is connected.

However, if you use thread-per-request, threads intervene only when the request is in progress, so even if tens of 
thousands of people use the service, it is economical because you can only put threads in the request currently in use.
Servlet Container (Web Container) is responsible for creating and managing Servlet Instances.

The Servlet Container we know representatively is Tomcat. ServletContainer is attached one WebApplication at a time. 
Tomcat, a servletContainer, is also a Java program, so a single JVM is attached. That is, **one WAS per one JVM.**

**What is the difference between Apache and Tomcat?**  
The Client sends a request according to a predetermined HTTP specification. After interpreting HTTP, 
it is the Web Server's job to send it in the appropriate data format

This process is called Static Web Server because it simply matches the request with the data and returns it to fit HTTP. 
However, this type of site will not be able to provide dynamic functionality. To solve this problem, 
a Web Application Server is used. WAS consists of the features of some Web Servers and Web Containers, 
where some Web Severs at the front receive HTTP requests and hand them over to Web Containers.

The Web Container processes internal program logic, creates data, and delivers it back to the Web server. 
Processing according to the Web Server is called Servlet Container in the Java camp. An example of a servlet container
is Tomcat, and when Tomcat Server receives a request, the Tomcat Engine finds a context that meets the request, 
and the context is processed by delivering the request delivered based on its web.xml to the servlet. (For reference, 
Spring Boot has an Embedded Tomcat, which can process data and affect the DB itself.)

Apache Web Server can use a multi-process and multi-threaded method together. There is always an idle number of 
processes and threads, so there is no need to wait for a new process or thread to be created when a request is made.
Usually, one request responds to one thread, but **when the user's access increases, the process is forked or allocated 
according to the Apache MPM method.**

**Apache is a multi-process, Tomcat is a multi-threaded. So why don't you just float multiple Tomcat Instances on one 
Apache web server?**  
Many tomcat instange == Many JVM. high probability of memory leak.  

To handle multiple requests, Tomcat creates a Thread Pool, a collection of threads, at boot time. When a user request 
(HttpServletRequest) is received, the Thread Pool assigns a Thread one by one. The corresponding Thread processes user
requests via the Dispatch Servlet created by the spring boot. After the operation is complete, the thread is returned 
to the thread pool.

**NIO (Non-Blocking I/O) Connector Introduces Tomcat 8.5 as a Default**  
The Connector imports socket connections, acquires data packets, converts them into HttpServletRequest objects, 
and forwards them to servlet objects.

**Why BIO connector is deprecated?**  
thread live till connection close. that mean other threads can’t work. NIO connection replace BIO. In the NIO Connector, 
a separate thread called Poler processes the connection. Poller reduces the amount of time a thread is wasted in idle 
state by holding sockets in cache and assigning threads only when data can be processed in that socket.

Apache Tomcat works as a process. Apache is a web server, Tomcat is ServletContext, and one Apache can have multiple 
Tomcat Instances as needed One Tomcat is a Single Servlet. Tomcat's Instance has one Acceptor Thread for each Instance
and has Dedicated Thread Pool. Tomcat basically advocates one thread per request, so it allocates one thread when one
HTTP request comes in. When the request is finished, return it to the Thread Pool so that the Thread can be reused.

## **Conclusion**
One Instance refers to a servletContainer shared by several Threads. When a servlet is created, it is created new if it 
is not already created in the servlet container. If you have already made a servlet, reuse it. Therefore, servlets must 
be implemented in a reusable form while being stateless.

A separate synchronization process is not required because it shares objects with no state. Therefore, there is no 
problem even if the controller receives dozens or tens of thousands of requests.