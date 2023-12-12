---
layout  : wiki
title   : Why you can't use Redis as your main DB
date    : 2022-04-21 19:52:40 +0900
updated : 2022-04-21 19:52:40 +0900
resource: 64/2F57A9-C9EC-49D8-B99E-9183DECBBE4D
toc     : true
public  : true
parent  : [[2022]]
latex   : true
---
* TOC
{:toc}

Redis is an In-Memory Database (DB) that stores data in memory rather than on disk, making it faster than disk-based DBs.
Disk-based databases read data from disk to memory, introducing delays and slower performance. In-Memory DBs, like Redis,
directly access data from memory, eliminating this bottleneck.

However, there are drawbacks to in-memory databases. RAM, where data is stored, is volatile and lacks persistence guarantees.
Also, RAM has limited space, e.g., 8GB, making it unsuitable for storing large amounts of data without causing memory swaps,
leading to performance issues.

### **Why Disk-based Databases are Slower Compared to Redis**
Disk-based databases face inherent limitations due to their reliance on external storage, introducing latency in data
retrieval and updates. When data is stored on disk, a read operation involves fetching the data from the disk into memory
before it can be used.

Additionally, disk-based databases typically read data in pages, leading to inefficiencies.
For instance, if the desired data is on page 2 and page 1 has already been read, the system may reread page 2,
causing delays and reducing performance.

### **Why Redis is Unsuitable as the Main Database**
Redis, being an In-Memory Database (DB) with data stored primarily in RAM, offers unparalleled speed compared to
disk-based databases. However, several factors limit its viability as the main database

- Wide Data Structure Support:
  Redis distinguishes itself by supporting various data structures such as Strings, Bitmaps, Hashes, Lists, Sets, 
  and Sorted-Sets. This versatility simplifies development and reduces barriers to entry.

- Persistence Mechanisms:
  While in-memory databases lack persistence by default, Redis provides methods to ensure data durability:

- Snapshotting: Takes a snapshot of the entire in-memory data and writes it to disk.
  Append On File (AOF): Logs every write/update operation to a file.

Despite Redis addressing persistence concerns, it is not ideal as a main DB for several reasons

### **Storage Capacity Constraints**
In-memory databases like Redis rely on RAM for storage, imposing a severe limitation on the amount of data they can handle.
With RAM being volatile and typically constrained (e.g., 8GB), Redis is unsuitable for serving as the primary database
for large-scale applications that require extensive data storage.

### **Performance Degradation under Heavy Loads**
In scenarios where a significant volume of data is received, the limited storage space in RAM can lead to memory swapping.
This results in decreased performance as the system struggles to manage data in and out of memory. The trade-off between
high performance and cost becomes impractical for sustained heavy traffic.

### **Cost and Persistence Trade-offs**
While Redis provides mechanisms like Snapshotting and Append On File (AOF) to ensure data persistence,
the cost of maintaining high-performance, in-memory capabilities might not be justified when compared to other disk-based
databases. The advantage of Redis in terms of speed diminishes when the need for persistent storage is prioritized.

### **Optimal Use as a Cache**
Redis is commonly employed as a cache for data from disk-based databases rather than as the primary storage solution.
Its in-memory retrieval speed proves beneficial for caching frequently accessed or time-sensitive data,
enhancing performance without the limitations associated with serving as the main database.

## **conclusion**
In practice, Redis is commonly used not as the main database but for caching data from other main databases.
Its fast in-memory retrieval is leveraged to enhance performance in scenarios where the limitations of storage
capacity and cost-effectiveness are acceptable trade-offs.

In summary, while Redis excels in certain applications due to its in-memory nature and support for various data structures,
its limitations in storage capacity, potential performance issues during high traffic, and the cost-effectiveness of
maintaining persistence make it better suited as a cache for data from more traditional disk-based main databases.