# Caching

---

## **1️⃣ Basics of Caching**
- What is Caching?
Caching is an optimization technique that stores frequently accessed data in fast-access memory (RAM, SSD, or distributed cache) to reduce latency and improve application performance. Instead of making expensive calls to a database, API, or disk storage, applications first check the cache.

### **Importance & Benefits of Caching**  

Caching plays a **critical role** in modern software systems by **reducing latency, improving performance, and enabling scalability**. It helps applications run faster and handle more users efficiently.  

#### **1️⃣ Performance Improvement 🚀**  
🔹 **Faster Data Retrieval**: Instead of repeatedly fetching data from a slow database or external API, caching stores frequently used data in **RAM or SSD**, making access nearly **instantaneous**.  
🔹 **Optimized Computation**: Expensive operations (e.g., complex queries, ML model inference) can be cached to **avoid redundant processing**.  
🔹 **Example:** A **product listing page** in an e-commerce site loads much faster when product details are cached instead of being fetched from a relational database every time. 

#### **2️⃣ Latency Reduction ⏳**  
🔹 **Minimizing Network Calls**: A cache keeps data closer to the user, reducing **round-trip time (RTT)** between the client and the server.  
🔹 **Avoiding Slow Disk I/O**: Accessing data from **RAM** is much faster than reading from a disk-based database.  
🔹 **Example:** A **social media feed** loads faster because posts and comments are cached, reducing database lookups.  

#### **3️⃣ Scalability & High Availability 📈**  
🔹 **Reduced Server Load**: Offloading database and API calls to a cache means servers can handle **more concurrent requests** without slowing down.  
🔹 **Handling Traffic Spikes**: Helps manage **sudden bursts** in user activity (e.g., Black Friday sales, viral content).  
🔹 **Distributed Caching**: Systems like **Redis, Memcached, Hazelcast** enable **horizontal scaling**, distributing cache across multiple servers.  
🔹 **Example:** **Netflix & YouTube** cache popular videos at **edge locations (CDNs)** to serve millions of users with minimal delay.  

#### 4️⃣ Cost Savings 💰**  
🔹 **Fewer Database Queries** = **Lower Infrastructure Costs**  
🔹 **Efficient Resource Utilization** = Avoids unnecessary CPU and memory usage  
🔹 **Example:** A **news website** caches trending articles, reducing expensive database reads and lowering cloud costs.  

### **When to Use Caching?**  
Caching is most effective in scenarios where **data is frequently accessed but changes infrequently**. Here are the key use cases:


#### **1️⃣ Read-Heavy Workloads 📖**  
🔹 **Definition:** Workloads where **read operations far outnumber write operations**.  
🔹 **Why Cache?** Fetching data from a database or API every time is slow and inefficient. Caching stores **precomputed results** in memory for fast retrieval.  
🔹 **Examples:**  
- **Product catalogs** in e-commerce (Amazon caches product details).  
- **User profile data** in social media apps (Facebook caches user profiles).  
- **News articles or blog posts** (Medium caches frequently read articles).  

📌 **Best Practice:** Use a **Cache-Aside** strategy to fetch from cache first and only query the database if needed.  

#### **2️⃣ Stateless Data & Session Management ⚡**  
🔹 **Definition:** Stateless data doesn’t change frequently and can be stored in a cache without consistency issues.  
🔹 **Why Cache?** Improves **scalability and performance** by offloading session storage from databases.  
🔹 **Examples:**  
- **Session storage** in distributed apps (e.g., storing user sessions in Redis for authentication).  
- **JWT token validation** (reducing repetitive database lookups).  
- **Feature flagging** (caching enabled/disabled status for features).  

📌 **Best Practice:** Use **TTL (Time-to-Live)** to automatically expire session data. 

#### **3️⃣ Idempotent Operations ✅**  
🔹 **Definition:** An **idempotent operation** returns the same result **regardless of how many times it is executed**.  
🔹 **Why Cache?** Reduces redundant processing and speeds up response times.  
🔹 **Examples:**  
- **API response caching** (e.g., caching weather API responses).  
- **Database query caching** (e.g., caching analytics reports).  
- **Search result caching** (Google caches frequent searches for instant results).  

📌 **Best Practice:** Use **Write-Through Cache** to ensure data consistency while leveraging cache for performance.  


### **Caching vs Buffering vs Memoization**  

Caching, buffering, and memoization **optimize performance** but serve **different purposes**. Let’s break them down:

#### **1️⃣ Caching 🏎️ (Speeding Up Repeated Data Access)**  
**📌 What is it?**  
- Caching **stores frequently accessed data in a fast storage layer** (RAM, SSD, or distributed cache).  
- It **reduces latency** by avoiding expensive operations like database queries or network calls.  

**🔹 Example Use Cases:**  
✅ Web Browsers store **CSS, JS, images** for faster page loads.  
✅ APIs cache **frequent responses** (e.g., weather API).  
✅ Databases cache **query results** (e.g., Redis caching MySQL queries).  

**🚀 Best for:** Read-heavy workloads, reducing database or API load.  

#### **2️⃣ Buffering ⏳ (Handling Data Flow Efficiently)**  
**📌 What is it?**  
- Buffering **temporarily stores incoming data before processing it**.  
- It helps **smooth out fluctuations** in data flow, ensuring consistent performance.  

**🔹 Example Use Cases:**  
✅ **Video Streaming (Netflix, YouTube):** Videos are **buffered** so playback remains smooth.  
✅ **Network Packets (TCP Buffer):** Network data is stored in a buffer before transmission.  
✅ **Logging Systems (Kafka, Elasticsearch):** Logs are buffered before being written to storage.  

**🚀 Best for:** Handling **continuous data streams, network transmission, or I/O operations**.  

#### **3️⃣ Memoization 🔄 (Optimizing Function Calls in Code)**  
**📌 What is it?**  
- Memoization **stores function results** to avoid redundant calculations.  
- Works within the **same program execution** (unlike caching, which persists across requests).  

**🔹 Example Use Cases:**  
✅ **Recursive Algorithms (Fibonacci Sequence, Dynamic Programming):** Avoid recomputing results.  
✅ **Heavy Computations (Machine Learning, Graphics Processing):** Cache expensive function calls.  
✅ **Web Frontend Optimization:** React uses **memoization** (`useMemo`, `useCallback`) to avoid unnecessary renders.  

**🚀 Best for:** Optimizing **CPU-heavy computations inside a program**.  

#### **📌 Key Differences**
| Feature      | **Caching** | **Buffering** | **Memoization** |
|-------------|------------|--------------|----------------|
| **Purpose**  | Store frequently used data for fast retrieval. | Temporarily hold data before processing. | Store function results to avoid recomputation. |
| **Scope**    | System-wide (database, API, web) | I/O operations (disk, network, video) | Within a single program execution. |
| **Persistence** | Can persist across sessions. | Temporary (cleared after processing). | Limited to program runtime. |
| **Best Used For** | Reducing API calls, database queries. | Streaming, log handling, TCP packets. | Recursion, dynamic programming, frontend rendering. |

---
---

## **2️⃣ Types of Caching**
### **Client-Side Caching: Browser Caching (HTTP Cache, Service Workers)**

Client-side caching helps reduce **page load times, bandwidth usage, and server load** by storing frequently accessed resources in the user's browser.  

#### **1️⃣ Browser Caching (HTTP Cache) 🏎️**  
📌 **What is it?**  
- Stores web assets like **HTML, CSS, JavaScript, images, and fonts** in the browser.  
- Prevents unnecessary network requests, making websites load **faster**.  

📌 **How Does It Work?**  
- The browser first checks its **cache** before requesting data from the server.  
- If the resource is **fresh (valid cache)**, it loads from the cache instead of making an HTTP request.  
- If it’s **expired (stale cache)**, the browser requests a fresh copy from the server.  

📌 **Key HTTP Cache Headers:**  
- **`Cache-Control`**: Defines caching behavior (`max-age=3600`, `no-cache`, `public`, `private`).  
- **`Expires`**: Specifies an expiration date for cached content.  
- **`ETag`**: Helps check if a resource has changed; if not, the cached version is used.  
- **`Last-Modified`**: Stores the last modified timestamp to validate cache freshness.  

📌 **Example:**  
A web page includes a **logo.png**.  
- On first visit: The browser **downloads and caches** `logo.png`.  
- On refresh: If cache is valid, it **loads from cache** instead of re-downloading.  

📌 **Benefits:**  
✅ Reduces **page load time**.  
✅ Saves **bandwidth**.  
✅ Lowers **server requests**, improving scalability.

#### **2️⃣ Service Workers (Advanced Browser Caching) ⚡**  
📌 **What is it?**  
- A **JavaScript script** that runs in the background, intercepting network requests.  
- Enables **offline caching** and background sync for **Progressive Web Apps (PWAs)**.  

📌 **How It Works?**  
1. **Intercepts network requests** and serves cached data when offline.  
2. **Stores resources** (HTML, CSS, API responses) using the Cache API.  
3. **Refreshes cache** when the network is available.  

📌 **Example Code:** *(Caching API responses for offline use)*  
```javascript
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request).then(response => {
      return response || fetch(event.request);
    })
  );
});
```

📌 **Use Cases:**  
✅ **Offline Mode** (Gmail, Twitter Lite, Spotify Web)  
✅ **Faster Page Loads** (Caches API responses)  
✅ **Background Sync** (Syncs data when online)  


### **Application-Level Caching: Memory Cache in Frontend Apps**  

📌 **What is Application-Level Caching?**  
Application-level caching stores frequently used **data, API responses, or computed values** in memory within a frontend application. This reduces redundant processing and network requests, improving **performance and responsiveness**.  

#### **1️⃣ Memory Cache in Frontend Apps (Client-Side Caching)**
📌 **How It Works?**  
Instead of repeatedly fetching data from an API, the application **temporarily stores data in memory** (RAM, browser storage, or state management systems) to quickly serve repeated requests.  

📌 **Key Methods for Frontend Caching:**  
🔹 **In-Memory Caching**  
   - Stores data in **JavaScript objects, variables, or state management libraries** (e.g., React state, Vuex, Redux).  
   - **Pros:** Fast, reduces API calls. **Cons:** Data is lost on page refresh.  

🔹 **IndexedDB / LocalStorage / SessionStorage**  
   - Stores cached data persistently in the browser.  
   - **Pros:** Survives page reloads. **Cons:** Limited storage, slower than memory.  

🔹 **Service Worker Cache API**  
   - Caches API responses for offline use.  
   - **Pros:** Enables Progressive Web Apps (PWAs).  


#### **2️⃣ Example: Caching API Data in React with useState & useEffect**
```javascript
import { useState, useEffect } from "react";

const cache = {}; // Simple in-memory cache

function fetchData(url) {
  if (cache[url]) {
    return Promise.resolve(cache[url]); // Return cached data
  }
  return fetch(url)
    .then(response => response.json())
    .then(data => {
      cache[url] = data; // Store in cache
      return data;
    });
}

export default function App() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetchData("https://api.example.com/data").then(setData);
  }, []);

  return <div>{data ? JSON.stringify(data) : "Loading..."}</div>;
}
```
📌 **How This Works?**  
✅ First request → Data is **fetched from API** and stored in `cache`.  
✅ Subsequent requests → Data **served instantly from memory**.  
✅ Reduces **network requests** and improves **UI responsiveness**.  

#### **3️⃣ Use Cases for Frontend Caching**
✅ **Reducing API Calls:** Fetching user details, product lists, search results.  
✅ **Enhancing User Experience:** Caching user preferences, session data.  
✅ **Offline Support (PWA):** Storing data in Service Workers for offline access.  

---

### **Server-Side Caching: Application-Level Caching (In-Memory Caches like Redis, Memcached)**  

📌 **What is Application-Level Caching on the Server?**  
Application-level caching on the server stores frequently accessed **database queries, API responses, or computed results** in **fast, in-memory storage** (like **Redis, Memcached**) to **reduce database load and improve performance**.  

🔹 **Why Use It?**  
- **Speeds up API responses** by serving cached data instead of querying the database.  
- **Reduces server load** by avoiding expensive computations.  
- **Handles high-traffic loads** efficiently.  

#### **1️⃣ In-Memory Caching with Redis & Memcached 🏎️**  
These caching systems **store key-value pairs in RAM** for **fast retrieval**.  

| Feature       | Redis | Memcached |
|--------------|-------|-----------|
| **Data Type Support** | Strings, Lists, Hashes, Sets, Sorted Sets | Only Strings |
| **Persistence** | Yes (AOF, RDB) | No (Memory-only) |
| **Eviction Policy** | LRU, LFU, TTL | LRU |
| **Replication & Clustering** | Yes | Limited |
| **Use Case** | **Database caching, session storage, message queues** | **Simple key-value caching** |

#### **2️⃣ Example: Caching Database Queries in Redis**
```python
import redis
import json
import sqlite3

# Connect to Redis
cache = redis.Redis(host='localhost', port=6379, db=0)

def get_user(user_id):
    cache_key = f"user:{user_id}"
    
    # Check cache first
    cached_user = cache.get(cache_key)
    if cached_user:
        return json.loads(cached_user)  # Return cached result
    
    # Query database if cache miss
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users WHERE id=?", (user_id,))
    user = cursor.fetchone()
    
    if user:
        cache.setex(cache_key, 3600, json.dumps(user))  # Cache result for 1 hour
    
    return user

print(get_user(1))  # Fetch from cache or DB
```
📌 **How This Works?**  
✅ **Cache Hit** → User data is served **instantly** from Redis.  
✅ **Cache Miss** → Data is **fetched from the database, cached, and served**.  
✅ **Expires after 1 hour (TTL)** to avoid stale data.  

#### **3️⃣ Use Cases for Application-Level Caching**
✅ **Reducing Database Load:** Cache **frequent queries** like product details.  
✅ **Session Storage:** Store **user sessions** in Redis for **stateless authentication**.  
✅ **API Rate Limiting:** Throttle requests by caching API usage counts.  

#### **💡 Takeaway**
✅ **In-memory caching (Redis, Memcached) is crucial for high-performance apps.**  
✅ **Ideal for database query caching, session storage, and API acceleration.**  
✅ **Prevents bottlenecks & scales applications efficiently.** 🚀


### **Database Caching: Query Caching, Result Caching, and Read Replicas**  

Database caching improves performance by reducing the load on databases, speeding up data retrieval, and enhancing scalability. Below are the key types of database caching:

#### **1️⃣ Query Caching**  
📌 **What is it?**  
Query caching stores the **results of SQL queries** so that when the same query is executed again, the result is fetched from the cache instead of querying the database. This avoids repeated processing of the same request.

📌 **How It Works:**  
- When a query is executed for the first time, the database engine stores the result in the cache (memory or disk).  
- On subsequent requests for the same query, the result is served from the cache, improving speed.

📌 **Example Use Case:**  
- A website that frequently displays **popular posts** with the same query. Query caching ensures that the same result is served from cache instead of querying the database repeatedly.  

📌 **Challenges:**  
- **Cache Invalidation**: If the data changes, the cached result must be invalidated to ensure fresh data.  
- **Limited Use**: Not ideal for highly dynamic data as cache can become stale quickly.


#### **2️⃣ Result Caching**  
📌 **What is it?**  
Result caching involves storing the **actual data** returned by queries (like user details, product information) in a fast-access cache (e.g., Redis or Memcached). This allows repeated access to the same data without querying the database.

📌 **How It Works:**  
- The data or query result is cached in a key-value store like **Redis**, **Memcached**, or **Hazelcast**.  
- When a request for the same data is made, the cached result is returned, bypassing the database query.

📌 **Example Use Case:**  
- **Product Catalog** in an e-commerce store: If product data is frequently requested, it’s cached so it doesn’t require repeated database lookups.

📌 **Benefits:**  
- **Reduced database load**: Frequently accessed data is fetched from the cache.  
- **Faster response times**: Data is retrieved from memory, which is much faster than querying a database.

#### **3️⃣ Read Replicas**  
📌 **What are Read Replicas?**  
Read replicas are **copies of the primary database** used for read operations. The main database handles **write operations**, and **replicas** handle **read operations**, distributing the load.

📌 **How It Works:**  
- The **primary database** (master) handles all **write operations** (insert, update, delete).  
- **Read replicas** replicate data from the master and serve **only read requests** (select queries).  
- This helps reduce the load on the primary database and **scales horizontally** by adding more replicas.

📌 **Example Use Case:**  
- An **online banking application** that needs to serve large numbers of account balance queries but wants to minimize the load on the main database. **Read replicas** can be used to serve read queries while the primary database focuses on transactions and updates.

📌 **Benefits:**  
- **Scalable performance**: Offload read-heavy operations to replicas.  
- **High availability**: Replicas can serve as backups in case the primary database fails.  
- **Reduced latency**: By placing read replicas close to users (in different geographic locations), you can reduce data access time.

#### **💡 Key Takeaways**  
✅ **Query Caching**: Cache SQL query results to avoid redundant execution of the same query.  
✅ **Result Caching**: Cache the actual data for frequently requested resources to speed up retrieval.  
✅ **Read Replicas**: Offload read queries from the main database to replicas for better scalability and performance.  


### **Distributed Caching: CDNs and Global Caches**  

Distributed caching improves the **scalability, performance, and availability** of web applications by storing data closer to the user, reducing latency and server load. **Content Delivery Networks (CDNs)** and **global caches** are two key components of distributed caching.

#### **1️⃣ Content Delivery Networks (CDNs)**  
📌 **What is a CDN?**  
- A **Content Delivery Network (CDN)** is a globally distributed network of servers that cache **static content** (images, videos, JavaScript, stylesheets, etc.) and **serve it from the nearest server** to the user.  
- CDNs reduce the time it takes to load content by serving data from locations that are physically closer to the user.

📌 **How It Works:**  
- When a user requests a resource (e.g., an image or webpage), the request is routed to the nearest **CDN edge server**. If the resource is cached on that server, it is served directly. If not, the CDN fetches it from the **origin server** and caches it for future requests.
- **Cache TTL (Time-to-Live)** is used to control how long the data remains in the CDN before being refreshed.

📌 **Example Use Case:**  
- **YouTube** uses CDNs to deliver video content to users based on their geographic location, reducing buffering times.  
- **E-commerce websites** cache product images and stylesheets in a CDN to improve loading times globally.  

📌 **Benefits:**  
- **Faster content delivery** by serving data from edge servers closer to the user.  
- **Reduced latency** as requests don’t need to travel long distances to the origin server.  
- **Reduced load on origin servers**, as the CDN caches and serves static content.

---

#### **2️⃣ Global Caches**  
📌 **What is a Global Cache?**  
- **Global caching** involves distributing cached data across multiple locations or data centers worldwide. This is done to provide **consistent, fast access to data** from any location, ensuring that users worldwide can access resources with minimal latency.  
- **Distributed caches** like **Redis**, **Hazelcast**, and **Memcached** can be set up in a **global, distributed manner** to store data across multiple regions.

📌 **How It Works:**  
- Data is cached in memory and is **replicated across different geographic locations** or data centers. 
- **Cache consistency** is maintained using **replication** and **sharding** techniques, ensuring that the most recent data is available across all nodes in the global cache.

📌 **Example Use Case:**  
- **Global e-commerce platforms** like Amazon use global caches to ensure that **product availability, prices, and user sessions** are quickly accessible from anywhere in the world, reducing server strain and improving user experience.  
- **Cloud applications** (AWS, Azure, Google Cloud) use global caches to distribute **user data, configuration settings, and session states** across multiple data centers for low-latency access.  

📌 **Benefits:**  
- **Low-latency access**: Data is always served from the nearest cache, ensuring fast response times.  
- **Improved scalability**: By distributing data, you can handle large volumes of traffic and avoid overloading any single data center.  
- **High availability**: Even if one data center goes down, other regions can serve the cached data, ensuring uninterrupted service.

#### **💡 Key Takeaways**
✅ **CDNs** cache static content at the **edge of the network**, delivering fast content delivery with reduced latency.  
✅ **Global Caches** store data across multiple regions to provide **low-latency access** and **high availability** for distributed applications.  
✅ **Both CDNs and global caches** help scale applications by **offloading traffic**, reducing latency, and improving the user experience.  


### **Edge Caching: CDNs, CloudFront, Cloudflare, Akamai**  

Edge caching is a technique that improves performance by **storing content closer to the user**, at the **edge of the network**, typically in **Content Delivery Networks (CDNs)**. This reduces latency and accelerates content delivery. Let’s explore how edge caching works with popular CDNs like **CloudFront**, **Cloudflare**, and **Akamai**.

#### **1️⃣ What is Edge Caching?**  
📌 **Edge caching** stores data at geographically distributed servers called **edge locations**. These are closer to the user’s location than the origin server (usually a centralized data center).  
- **Content is cached at the "edge"**, reducing the distance the data must travel, leading to **faster load times** and **reduced latency**.  
- Common use cases for edge caching include **static resources** like images, videos, stylesheets, and web pages.

📌 **How It Works:**  
- When a user requests content (e.g., a webpage or image), the request is routed to the nearest **edge server**.
- If the content is cached at that edge server, it is served directly to the user.
- If the content is not cached (cache miss), the server fetches it from the **origin server**, caches it, and serves it to the user.

#### **2️⃣ CloudFront (AWS)**  
📌 **What is CloudFront?**  
Amazon **CloudFront** is AWS’s **content delivery network** that uses edge locations around the world to cache content and deliver it with **low latency**.

📌 **How It Works:**  
- CloudFront automatically caches content from an **origin server** (Amazon S3, EC2, or other HTTP sources).  
- CloudFront has **over 200 edge locations** globally, ensuring that users access content quickly.
- **Cache Control**: CloudFront respects HTTP headers like `Cache-Control` to determine how long content is cached and when it should expire.  
- **Customizable Cache**: CloudFront allows you to configure cache policies for **dynamic and static content**.

📌 **Example Use Case:**  
- A **video streaming platform** caches video files at CloudFront edge locations for faster playback and reduced buffering.

#### **3️⃣ Cloudflare**  
📌 **What is Cloudflare?**  
**Cloudflare** is a popular CDN and security service that provides **global edge caching** and performance optimization for websites and APIs.

📌 **How It Works:**  
- Cloudflare caches static content at **over 200 locations worldwide**.  
- Unlike traditional CDNs, Cloudflare offers **dynamic content caching** using its **"cache everything"** feature.
- **Automatic Content Optimization**: Cloudflare can automatically optimize images, minify scripts, and even cache HTML content to improve load times.  
- **Security**: Cloudflare also offers **DDoS protection** and **SSL encryption** as part of its CDN services.

📌 **Example Use Case:**  
- A **retail website** using Cloudflare can cache **product pages** and **images** at edge servers, improving response time for global users.

#### **4️⃣ Akamai**  
📌 **What is Akamai?**  
Akamai is one of the **largest and most established CDNs**, providing **edge caching** and content delivery solutions to enterprises worldwide.

📌 **How It Works:**  
- Akamai operates **over 300,000 servers** across the globe, ensuring that content is cached at **millions of edge locations**.  
- It supports **dynamic content delivery**, including the ability to cache not just static assets but also **API responses and dynamic HTML**.  
- **Intelligent Caching**: Akamai uses **AI and machine learning** to optimize caching and predict traffic patterns, ensuring the most efficient delivery.  

📌 **Example Use Case:**  
- A **media company** uses Akamai to deliver high-quality video streaming with **zero buffering** by caching content at global edge servers.

#### **💡 Key Benefits of Edge Caching**  
✅ **Faster Content Delivery**: Data is served from the **nearest edge server**, reducing latency and improving load times.  
✅ **Scalability**: By offloading requests to edge servers, CDNs reduce the load on the origin server, enabling the application to scale easily.  
✅ **Cost Reduction**: **Bandwidth costs** are reduced as requests are served from cached content at edge locations.  
✅ **Improved User Experience**: Faster load times and reduced latency **boost user satisfaction**, especially for global audiences.

#### **💡 Key Takeaways**  
✅ **CloudFront, Cloudflare, and Akamai** are **leading edge caching solutions** that store data at geographically distributed servers to **optimize content delivery**.  
✅ They are used to **cache static and dynamic content**, improving website performance and **reducing the load on origin servers**.  
✅ **Edge caching** is **critical for global websites and applications** to ensure fast, reliable, and scalable content delivery.


---
---

## **3️⃣ Caching Strategies**
- **Cache Invalidation Strategies**  
  - Write-Through Cache  
  - Write-Back (Lazy Write)  
  - Write-Around Cache  

---

- **Cache Expiration Policies**  
  - TTL (Time-To-Live)  
  - LRU (Least Recently Used)  
  - LFU (Least Frequently Used)  
  - FIFO (First-In, First-Out)  
  - MRU (Most Recently Used)  
  - ARC (Adaptive Replacement Cache)  

---

- **Cache Placement Strategies**  
  - Read-Through Cache  
  - Cache-Aside (Lazy Loading)  
  - Write-Through Cache  
  - Write-Back Cache  

---
---

## **4️⃣ HTTP Caching (Web Caching)**
- **HTTP Cache Headers**
  - `Cache-Control`, `Expires`, `ETag`, `Last-Modified`, `Pragma`
- **Browser Cache (Service Workers, LocalStorage, IndexedDB)**
- **Reverse Proxy Caching (Varnish, Nginx, Cloudflare, Squid)**
- **CDN Caching (Akamai, Cloudflare, AWS CloudFront)**

---
---

## **5️⃣ Database Caching**
- **Query Caching** (MySQL Query Cache, PostgreSQL Statement Cache)  
- **Row-Based Caching** (Caching individual rows in Redis, Memcached)  
- **Materialized Views** (Precomputed query results)  
- **Read Replicas & Sharding for Caching**  
- **Write-Through vs Write-Back Database Cache**  

---
---

## **6️⃣ In-Memory Caching Systems**
- **Redis**
  - Key-Value Storage, Pub/Sub, Expiry Mechanisms
  - Redis Eviction Policies (LRU, LFU, TTL)
  - Redis Persistence (RDB, AOF)
  - Redis Clustering & Replication

- **Memcached**
  - Use Cases, Differences from Redis
  - LRU Eviction Strategy

- **Comparison of Redis vs Memcached**

---
---

## **7️⃣ Distributed Caching & Scaling**
- **Consistent Hashing**  
- **Cache Partitioning & Sharding**  
- **Multi-Tier Caching (L1, L2, L3 Caches)**  
- **Cache Coherency & Synchronization in Distributed Systems**  
- **Challenges of Distributed Caching (Cache Stampede, Thundering Herd, Invalidation Delays)**  
- **Cache Replication & High Availability**  

---
---

## **8️⃣ Advanced**
- **Cache Warming (Preloading the Cache)**  
- **Cache Bypass & Soft Cache Misses**  
- **Bloom Filters for Efficient Caching**  
- **Cache Stampede Prevention (Locking, Request Collapsing)**  
- **Performance Tuning for Caching (Metrics & Benchmarking)**  
- **Hybrid Caching Strategies (Combining LRU + LFU, etc.)**  

---

## **9️⃣ Caching in Cloud & Microservices**
- **AWS ElastiCache (Redis & Memcached)**
- **Google Cloud Memorystore**
- **Azure Cache for Redis**
- **Microservices Caching (API Gateway Cache, Service Mesh Cache)**
- **Sidecar Caching (Envoy Proxy, Istio, Nginx Cache)**
- **GraphQL Query Caching & Response Caching**  

---
---

## **🔟 Real-World Use Cases**
- **Caching in Web Applications (Session Storage, Authentication Tokens)**
- **E-Commerce Caching (Product Catalog, Pricing, User Sessions)**
- **Social Media Caching (News Feed, User Profiles)**
- **Gaming & Real-Time Applications (Leaderboard, Matchmaking)**
- **Machine Learning Caching (Model Inference Caching, Feature Store)**  
