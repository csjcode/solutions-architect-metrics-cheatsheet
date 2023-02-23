
#  ⚡️ 150+ Solutions Architect metrics/calculations cheatsheet

150+ Solutions Architect metrics and calculations for systems design, technology comparisons, planning and projects. btw, If there is interest, I'll make this into tables, I made a few but haven't had time to do it all yet.

Categories: User, Network, Reliability, Compute, Storage, Database, Queues/Events, Security, Cost.

Thanks for checking it out... if you have ideas for improvements, feel free to comment or make a PR on my github repo: https://github.com/csjcode/solutions-architect-metrics-cheatsheet


### ⭐️ User

* **Daily Active Users (DAU)**
  * Unique active users / day 
  * Performance and capacity needs, daily, projections.
* **Monthly Active Users (MAU)**
  * Unique active users / month
  * Performance and capacity over longer time periods, projections.
* **Concurrent Users, Avg/Max** 
  * Number of users at same time, average and peaks
  * Reliability, server capacity, quotas, service bottlenecks
* **Actions Per User (APU): Average actions per user**
  * Actions performed by all unique users / by the number of unique users.
  * Performance, bandwidth, concurrency, cost optimization for high/low microservices.
* **Actions Per User delta (APU Δ)**
  * Change in actions per user over a given time period
  * Speed of scalability, concurrency, performance.
* **Daily User Actions (DUA)**
  * Total actions performed by all users in a day.
  * System load, performance, cost and capacity growth needs.
* **Requests Per Second (RPS)**
  * Service requests per second
  * Reliability in high traffic, quotas, performance.
* **User Delta**
  * Change in the number of users over a given time period
  * Speed of scalability, capacity planning, concurrency, performance, cost..
* **Session length**
  * Average duration of user session
  * Server resources, cost, performance, concurrency planning.



### ⭐️ Network 



* **CIDR/Subnet Calculation**
  * IP address and network mask calculation, 
  * Number of IPs = 2<sup>32</sup>-2<sup>prefix</sup>
  * 10.0.0.0/24 = 2<sup>32</sup>-2<sup>24</sup> = 2<sup>8</sup> = 256
  * For network sizing and planning
* **Bandwidth Consumed/Utilization**
  * (Bandwidth used / Total available bandwidth) x 100%
  * Network resource usage, potential bottlenecks, cost, quotas, performance
* **Available Bandwidth**
  * Total available bandwidth - bandwidth used.
  * Cost, performance, quotas, adequate resources for network traffic and avoiding slowdowns.
* **Data Transmission Rate**
  * Amount of data transferred / time taken
  * Data transfer speed and network efficiency.
* **Link Capacity**
  * Maximum bandwidth capacity of a link.
  * Reliability - determines maximum bandwidth available for a link to ensure it can handle traffic.
* **Network Throughput**
  * (Amount of data transferred / Total time) x 100%
  * Performance, operations, network efficiency and data transfer speed.
* **Network Latency**
  * Delay between sending and receiving data.  Round-trip time (RTT)
  * Performance, delay in data transfer and network responsiveness.
* **Network I/O**
  * Input/output rate of network data.
  * Warning of network bottlenecks, performance, cost.
* **Request Error rate**
  * Percentage of failed requests,  (Number of failed requests / Total requests) x 100%
  * Identifies issues in the network or application that need to be addressed.
* **Packet Loss Rate**
  * Percentage of lost packets.
  * Identifies potential vulnerabilities or issues in the network or application.
* **HTTP response codes** 
  * Partial list, see [full list](https://en.wikipedia.org//wiki/List_of_HTTP_status_codes)
  * **1xx info**, processing
  * **2xx successful**: 200 OK
  * **3xx redirection**: 301 Moved Permanently, 302 Found, 304 Not Modified
  * **4xx client error**: 400 Bad Request (parameters missing?), 401 Unauthorized (API token missing?), 403 Forbidden (permissions?), 404 Not Found (url incorrect?), 405 Method Not Allowed (eg. POST not accepted on resource), 429 Too Many Requests (exceeded rate limits?), 499 Client Closed Request
  * **5xx server errors**:  500 Internal Server Error, 501 Not Implemented, 502 Bad Gateway, 503 Service Unavailable (overload?), 504 Gateway Timeout (upstream timeout?)
* **HTTP Header Fields**
  * List of [standard headers](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)



### ⭐️ Reliability


* **Recovery Time Objective (RTO)**
  * Maximum time window delay within which a service must be restored after a disaster.
* **Recovery Point Objective (RPO)**
  * Maximum amount of time before unacceptable amounts of data have been lost due to a disaster, failure, or comparable event
* **Single Point of Failure (SPOF)**
  * Component that can cause system failure.
  * 1 - (redundant components/total components).
* **Cloud Services Quotas**
  * Limits on usage of cloud services.
  * Possible SPOF, if quota reached, service unavailable/degraded.
* **Availability (% of time)**
  * proportion of time a system is operational
  * uptime / (uptime + downtime)
* * **Availability (% of requests)**
  * proportion of time a system is operational
  * successful requests / (valid requests)
* **Availability in 9s ("nines")**
  * Percentage of uptime in a year.
  * (total time - downtime) / total time
* **Maximum Availability with Dependencies**
  * Maximum Availability estimate for multiple services in a distributed system.
  * Availability of Service 1 * Availability of Service 2 * ... Availability of Service n
  * MTBF / MTBF + MTTR  
* **Maximum Availability with redundant components**
  * Maximum Availability estimate with duplicated components (higher reliability)
  * A = 1-F ≈ 1-f(1-a)<sup>s+1</sup>
  * where s = spare components, F= failure modes, a= availability (in %)
  * ex: 99.5% availability, with two spares the workload’s availability is A ≈ 1 − (1)(1−.995)3 = 99.9999875% availability
* **Mean Time to Failure (MTTF)**
  * Average time until a component fails.
  * total uptime / number of any failures.
* **Mean Time Between Critical Failures (MTBCF)**
  * total uptime / number of critical failures.
* **Mean Time to Data Loss (MTTDL)**
  * Average time before data loss.
  * MTTDL = (1 - Annualized Rate of Data Loss) / Annualized Rate of Data Loss
  * Annualized Rate of Data Loss = (Total Data Stored) x (Data Loss Rate)
* **Recovery Time (RT)**
  *  TTR + MTTD + MTTI + MTTRM, where TTR is Time to Respond.
* **Mean Recovery Time (MRT)**
  * Average time it takes to recover from a failure.
  * MRT = ∑RT / Number of incidents
* **Mean Time to Detect (MTTD)**
  * Average time it takes to detect a failure.
  * MTTD = ∑time taken to detect incidents / Number of incidents.
* **Mean Time to Identify (MTTI)**
  * Average time it takes to identify a failure.
  * MTTI = ∑time taken to identify incidents / Number of incidents.
* **Mean Time to Remediate (MTTRM)**
  * Average time it takes to fix a failure.
  * ∑time taken to remediate incidents / Number of incidents.
* **Mean Time to Resolve (MTTR)**
  * Average time it takes to resolve a failure.
  * MTTR = ∑time taken to resolve incidents / Number of incidents.
**Mean Time to Respond (MTTR)**
  * Average time it takes to respond to a failure.
  * MTTR = ∑time taken to respond to incidents / Number of incidents.
* **Change Failure Rate (CFR)**
  * Rate at which changes introduce failures.
  * CFR = Number of failed changes / Number of changes attempted.
* **Defect Escape Rate**
  * Rate at which defects escape detection.
  * DER = Number of defects found after release / Total number of defects.
* **Defect Density**
  * Number of defects per unit of code.
  * Number of defects / Size of the software.
* **Failure Rate**
  * Rate at which components fail.
  * Number of failures / Unit of time
* **Service restoration time**
  * Time taken to restore a failed system.
* **Redundancy**
  * (Number of redundant (backup) components / Total number of components) x 100%
* **Resiliency**
  * Ability to recover from a failure.
  * Availability x Reliability x Maintainability x Recoverability
  * Availability (% time), reliability (probability of working service), maintainability, and recoverability (MTTR)


### ⭐️ Compute


Many of the following metrics are available in analytics services of the cloud provider tools such as AWS Cloudwatch or service dashboards. Metrics are included here for awareness and a reminder when evaluating Compute resources.

* **CPU utilization**
  * CPU usage rate. Monitor performance & efficiency. Optimize performance.
  * Total CPU time / Elapsed time 
* **Disk I/O**
  * Disk input/output. Measure read/write speeds for the Compute device. Optimize throughput.
  * Total bytes read/written / Elapsed time 
* **Network I/O**
  * Network input/output. Measure bandwidth usage on the Compute device. Optimize connectivity. 
  * Total bytes sent/received / Elapsed time 
* **IOPS**
  * Input/Output operations/second. Assess data access performance. Optimize throughput.
  * Total operations / Elapsed time 
* **Memory utilization**
  * RAM usage rate. Assess RAM usage for performance.
  * Total RAM usage / Total RAM available 
* **Caching**
  * Data storage/retrieval. Improve data performance. 
  * Hits / Misses 
* **Cost**
  * Expense management. Estimate resource expenses. 
  * Actual cost/Estimated cost 
* **Container density**
  * Resource utilization. Optimize resource use. 
  * Used resources / Total resources 
* **Function duration vs. limits**
  * Execution time. Gauge execution time. 
  * Analytics or Start time - End time vs. quota
* **Function concurrency**
  * Simultaneous operations. Measure concurrency.
  * Analytics or Number of operations per lambda / Elapsed time
* **Function response time**
  * Execution time. Evaluate speed. Gauge execution time.

### ⭐️ Load Balancing
* **Load Balancing Algorithm**
  * Algorithm used by the load balancer to distribute traffic
  * Round Robin, Least Connections, Weighted Round Robin, Weighted Least Connections, Dynamic Least Connections, Source IP Hash, Least Time,  Least Packets, Agent-Based Load Balancing, URL Hash, Server Affinity (Sticky Sessions)
* **Request Success Rate**
  * Number of successful requests/Total number of requests
* **Latency**
  * Time taken to serve a request
* **Error Rate**
  * Number of failed requests/Total number of requests
* **Connection Count**
  * Number of connections between clients and servers
* **Active Connections**
  * Number of active connections between clients and servers
* **Backend Server Health**
  * Availability and response time of backend servers
* **SSL Handshake Time**
  * Time taken to establish a secure connection
* **Connection Rebalancing Time**
  * Time taken to rebalance connections across servers

### ⭐️ Autoscaling

* **Scaling metric**
  * A metric that determines when autoscaling should occur, such as CPU utilization or request count
* **Scaling policy**
  * A set of rules that define how autoscaling should occur, such as increasing or decreasing the number of instances based on the scaling metric
  * **Target Tracking Scaling**
    * Adjusts capacity based on target metrics.
  * **Step Scaling**
    * Adds or removes capacity based on specific thresholds.
  * **Simple Scaling**
    * Adds or removes capacity based on logging or cloudwatch alarms.
  * **Scheduled Scaling**
    * Changes capacity at specific times or dates.
  * **Predictive Scaling**
    * Uses ML to forecast demand and adjust capacity.
  * **Dynamic Scaling**
    * Resizes based on changing demand and traffic patterns.
  * **Capacity Optimized Scaling**
    * Provisions instances for optimal cost and performance.
* **Scale-out threshold**
  * The threshold value for the scaling metric that triggers scaling out (adding instances)
* **Scale-in threshold**
  * The threshold value for the scaling metric that triggers scaling in (removing instances)
* **Cool-down period**
  * The period of time after scaling has occurred during which autoscaling is suspended to prevent rapid scaling up and down

### ⭐️ Elasticity
* **Resource utilization**
  * The percentage of available resources (such as CPU or memory) that are currently in use
* **Capacity planning**
  * The process of estimating future resource needs based on historical usage patterns and growth projections
* **Time to Scale**
  * The time it takes to add or remove resources to meet demand changes
* **Cost Optimization**
  * The process of minimizing costs while maintaining the necessary level of elasticity and performance.

### ⭐️ Database

* **Throughput**
  * The amount of data transferred per unit of time
  * Data transferred / time
* **Latency**
  * The time it takes to process a request
  * Time to first byte + time to last byte
* **Response time**
  * The time it takes to respond to a request
  * Time to last byte - time to first byte
* **Concurrency**
  * The number of simultaneous users or connections
  * Simultaneous requests / time
* **Read-to-Write Ratio**
  * The ratio of read requests to write requests
  * Read requests / write requests
* **Cache Hit Rate**
  * The percentage of data that is retrieved from cache
  * cache hit rate = cache hits / (cache hits + cache misses)
* **Database Connections**
  * The number of active database connections
  * Measured using database monitoring tools.
* **Query performance**
  * Time to execute a database query
  * Execution time = end time - start time
* **Index usage**
  * How frequently an index is used to retrieve data
  * Index usage = (number of times index is used) / (total number of queries)
* **Lock waits**
  * Time spent waiting for a locked database object
  * Lock wait time = total time spent waiting for a lock
* **Deadlocks**
  * Occurrences of simultaneous locking conflicts in transactions
  * Deadlocks = number of occurrences of simultaneous locking conflicts
* **Data consistency**
  * Degree of uniformity and accuracy in data across systems
  * Data consistency = (number of errors detected / total number of checks) * 100
* **Backup and Recovery**
  * Time taken to backup and recover data in case of failure
  * Time taken to backup or recover / number of backups or recoveries
* **Database Size and Growth**
  * Total size of the database and its growth rate
  * Current size of database + (growth rate * time interval)
* **CAP Theorum**
  * Pick two of the following three properties:
  * **Consistency**: Each read request receives the most recent write or an error when consistency can’t be guaranteed.
  * **Availability**: Each request receives a non-error response, even when nodes are down or unavailable.
  * **Partition tolerance**: The system operates despite the loss of messages between nodes.
* **ACID**
  * **Atomicity**: All or nothing. Either all operations succeed or all operations fail.
  * **Consistency**: Data is consistent before and after the transaction.
  * **Isolation**: Transactions are isolated from each other.
  * **Durability**: Once a transaction has been committed, it will remain so, even in the event of power loss or system crash.
* **BASE**
  * Basically Available
  * Soft state (may be inconsistent for brief periods) 
  * Eventually consistent


### ⭐️ Storage


#### General Storage metrics
Applies to most storage mediums, including block, file, and object storage.

* **Data Durability**
  * Probability of data remaining intact over time
  * (1 - Annual Failure Rate) ^ Years
* **Latency**
  * Time for data to be accessed
  * Total time to read or write data
* **Replication Latency**
  * Time for replica data to be transferred or accessed
  * Total time to read or write data after transfer
* **IOPS (Input/Output Operations Per Second)**
  * Number of read/write operations per second
  * Total number of operations / time interval
* **Throughput**
  * Amount of data transferred per unit of time
  * Total data transferred / time interval
* **Maximum Throughput**
  * Amount of data transferred per unit of time
  * Total data transferred / time interval

#### Object storage

* **Object Storage Utilization**
  * Amount of object storage used versus total available object storage
  * Used object storage / Total object storage
* **Object Storage Tier Data Stored**
  * Length of time objects are stored in a tier before being transfered/deleted
  * Object transfer or deletion execution duration by tier
* **Object Storage API/request Calls**
  * API requests made to object storage service
  * API requests / Time interval
  * PUT, COPY, POST, LIST requests (pricing may be different)
  * GET, SELECT, and all other requests
  * Lifecycle Transition requests
  * Data Retrieval requests
* **Object Storage Latency**
  * Time taken for object storage service to process a request
  * Total time for requests / Number of requests
* **Data Transfer per time interval**
  * Total amount of data transferred
  * Data Transferred (in bytes) / time interval 
* **Object Storage Retention**
  * Length of time objects are stored before being deleted
  * Object transfer or deletion execution duration
* **Geographic Put/Get requests**
  * Latency of Put/Get requests
  * Latency (in milliseconds) / time interval 
* **Availability metrics**
  * Number of requests that fail
  * Requests that fail / total number of requests
* **Data Consistency metrics**
  * Number of objects that are successfully stored/retrieved
  * Number of objects successfully stored/retrieved / time interval
* **Bandwidth used in/out total, timeframe, region, internet, inside cloud provider**
  * Amount of data transferred in/out of object storage
  * Data transferred in/out / time interval
  * There may be different policies per cloud provider.


#### Disk storage

* **Disk Utilization**
  * Amount of disk space used versus total available disk space
  * Used disk space / Total disk space
* **Disk IOPS**
  * Number of read and write requests to a disk in a second
  * Number of requests / Time interval
* **Disk Latency**
  * Time taken for a disk to process a read/write request
  * Total time for read/write requests / Number of requests
* **Data Replication Latency**
  * Time taken to replicate data from one location to another
  * Time for replication completion - Time of data creation
* **Data Replication Bandwidth**
  * Amount of data replicated per second
  * Amount of data / Time interval
* **SSD Endurance**
  * Amount of data that can be written to an SSD before failure
  * Total bytes written / (Drive size in GB * Drive endurance)
* **Disk Utilization**
  * Percentage of disk space used
  * (Amount of space used / Total amount of space) x 100
* **RAID Reliability**
  * Probability that the RAID will remain operational
  * (1 - Probability of failure) ^ Number of disks
* **Storage Capacity**
  * Total amount of storage space available
  * Amount of space used + amount of space available
* **Block Storage IOPS**
  * Number of read and write requests to a block storage device in a second
  * Number of requests / Time interval
* **Block Storage Latency**
  * Time taken for a block storage device to process a read/write request
  * Total time for read/write requests / Number of requests

* Types of RAIDS


RAID Level | Description
-----------|------------
RAID 0 | Data is striped across multiple disks for increased performance, but offers no redundancy.
RAID 1 | Data is mirrored across two disks for fault tolerance, but offers no performance improvement.
RAID 5 | Data is striped across multiple disks with parity information stored on each disk for fault tolerance.
RAID 6 | Similar to RAID 5, but with two sets of parity information for even greater fault tolerance.
RAID 10 | A combination of RAID 1 and RAID 0, where data is mirrored and striped for both performance and fault tolerance.
RAID 50 | A combination of RAID 5 and RAID 0, where data is striped across multiple RAID 5 arrays for increased performance and fault tolerance.
RAID 60 | A combination of RAID 6 and RAID 0, where data is striped across multiple RAID 6 arrays for even greater performance and fault tolerance.


### ⭐️ Queues/Events

* **Queue Depth**
  * Number of events in a queue waiting to be processed.
  * Total events - Processed events
* **Queue Wait Time**
  * Amount of time an event spends waiting in a queue before being processed.
  * Total time events spend in queue / Number of events in queue
* **Event Arrival Rate**
  * Rate at which events are arriving at a queue.
  * Number of events arriving / Time interval
* **Event Processing Time**
  * Amount of time it takes to process an event.
  * Total time spent processing events / Number of events processed
* **Event Processing Rate**
  * Rate at which events are being processed.
  * Number of events processed / Time interval
* **Queue Processing Rate**
  * Rate at which events are being processed from a queue.
  * Number of events processed from queue / Time interval
* **Queue Time**
  * Total time that events spend in a queue, including both wait time and processing time.
  * Queue Wait Time + Event Processing Time
* **Queue Throughput**
  * The rate at which events are moving through a queue, including both incoming and outgoing events.
  * Incoming Event Rate + Outgoing Event Rate
* **Event Drop Rate**
  * the rate at which events are being dropped or lost, typically due to queue overflow.
  * Number of dropped events / Total number of events
* **Queue Latency**
  * the time it takes for an event to travel through a queue, including both wait time and pr**ocessing time.
  * Queue Time / Number of events


### ⭐️ Security
* Network Security Score: a metric that measures the security posture of a network, including factors such as the number of vulnerabilities, exposure to threats, and compliance with security standards.

* **Incident Response Time**
   * The amount of time it takes to respond to a security incident
   * Detection Time + Response Time + Mitigation Time
   * Time Detected - Time Reported
* **Risk Assessment Score**
   * A numerical score based on a risk assessment methodology such as the NIST Risk Management Framework
   * (risk rating x probability of risk) + (residual risk x probability of residual risk)
   * Number of Potential Risks / Number of Acceptable Risks
* **Attack Surface**
   * The total number of entry points or attack vectors available to attackers 
   * Attack surface = sum of (threats x vulnerabilities) 
* **Vulnerability Assessment Score**
   * A numerical score based on a vulnerability assessment methodology such as CVSS
   * Common Vulnerability Scoring System [CVSS calculator(https://www.first.org/cvss/calculator/3.1)
   * Potential Vulnerabilities/Number of Acceptable Vulnerabilities
   * CVSS: (Base Score + Temporal Score + Environmental Score)
* **Access Control Effectiveness**
   * The ability of the access control system to protect the system from unauthorized access
   * (Authenticated Access Attempts - Unauthorized Access Attempts) / Authenticated Access Attempts
   * Number of Access Control Rules/Number of Access Control Rules Enforced
* **Authentication Effectiveness**
   * The ability of the authentication system to accurately identify and authenticate users
   * Authentication Effectiveness = (Authenticated Users - Unauthenticated Users) / Authenticated Users
* **Authorization Effectiveness**
   * The ability of the authorization system to accurately authorize users to access resources
   * Number of Authorization Controls/Number of Authorization Controls Enforced
* **Security Audit Log Analysis**
   * The ability of the security audit system to detect, monitor, and analyze security events
   * (Audited Events - Unaudited Events) / Audited Events
   * Number of Security Events Detected/Number of Security Events Recorded
* **Security Incident Rate**
   * Rate of security incident per time interval
   * Security incidents / time  
* **Security Compliance Score**
   * Score of how well the system complies with security policies and best practices
   * Compliance score = (number of compliant components / total number of components) x 100
* **Security Training Effectiveness**
   * Measurement of how well users understand and adhere to security policies
   * Training effectiveness = (number of users who successfully complete security trainings / total number of users) x 100
* **Vulnerability Scanning Frequency**
   * Measurement of how often the system is tested for security vulnerabilities
   * Scanning frequency = (number of scans performed in a given time period / total time period)
* **Identity and Access Management (IAM) roles and permissions audit**
   * Measurement of the accuracy and security of IAM roles and permissions
   * IAM audit = (number of correct roles and permissions / total number of roles and permissions) x 100
* **Key Management Service (KMS) usage and audit**
   * Measurement of the accuracy and security of KMS usage
   * KMS audit = (number of correct KMS usage / total number of KMS usage) x 100
* **Security Information and Event Management (SIEM) alerts and monitoring**
   * Measurement of the accuracy and security of SIEM alerts
   * SIEM monitoring = (number of correctly triggered alerts / total number of alerts) x 100
* **Threat intelligence feeds integration and usage**
   * Measurement of how threat intelligence feeds are used to help identify and respond to security threats
   * Number of threat intelligence feeds used / total number of threat intelligence feeds available
* **Encryption key rotation frequency**
   * Measurement of how often cryptographic keys are changed
   * Time interval between key changes
* **Compliance posture**
   * Measurement of how well the system complies with a security standard
   * Number of security standards met / total number of security standards
* **Network traffic monitoring and analysis**
   * Measurement of the ability to monitor and analyze network traffic for suspicious activity
   * Amount of network traffic monitored / total network traffic
* **User behavior analytics (UBA) and anomaly detection**
   * Measurement of the ability to detect anomalous user behavior
   * Number of anomalies detected / total user behavior events
* **Data Loss Prevention (DLP)** 
   * The practice of preventing sensitive data from leaving the organization 
   * DLP = implementation of policies and technologies + monitoring of user activity 
* **Data Encryption** 
   * The practice of transforming sensitive data into an unreadable format 
   * Data encryption = implementation of encryption algorithms + encryption of data 

### ⭐️ Cost  

I am only going to give some brief metrics on Cost, because almost everything above can affect cost and it will vary a lot between providers. 

This is not to minimize cost, it's one of the most important factors!!! 

Just that cost should be considered on ALL the metrics above.

* **Total Cost of Ownership (TCO**) = (cost of acquisition + cost of operation + cost of maintenance) over the useful life of the asset
* **Cost per transaction** = total cost / number of transactions
* **Cost per unit of time** = total cost / time period
* **Cost per user** = total cost / number of users
* **Return on Investment (ROI)** = (gain from investment - cost of investment) / cost of investment
* **Cost of Downtime (CoD)** = (lost revenue + recovery costs + damage to brand reputation) / total downtime hours
* **Cost of Poor Quality (CoPQ)** = (internal failure costs + external failure costs + cost of appraisal + cost of prevention) / total number of units produced
* **Cost of Delay (CoD)** = (value of time saved by earlier release - cost of delay) / time saved

There are a ton of cloud cost tools but these are some of the popular ones on the biggest platforms (there are many more if you search on their sites):

* **AWS**
  * AWS Cost Explorer
  * AWS Budgets
  * AWS Trusted Advisor
* **Azure**
  * Azure Cost Management + Billing
  * Azure Advisor
  * Azure Service Health
* **GCP**
  * GCP Billing
  * GCP Pricing Calculator
  * GCP Cost Management
* **Third-party**
  * CloudCheckr
  * CloudHealth by VMware
  * Apptio Cloudability
  * CloudBolt
  * CloudZero

### ⭐️ References

* [Amazon AWS Well Architected](https://aws.amazon.com/architecture/well-architected/)
* [Microsoft Azure Well Architected](https://learn.microsoft.com/en-us/azure/architecture/framework/)
* [Google Cloud Architecture Framework](https://cloud.google.com/architecture/framework)
* [SystemsArchitect.io](https://systemsarchitect.io/)
* [The Site Reliability Engineering](https://sre.google/books/)
* [The Site Reliability Workbook](https://sre.google/books/)
* [System Design Primer](https://github.com/donnemartin/system-design-primer)
* [System Design Interview](https://github.com/checkcheckzz/system-design-interview)
  
  
Thanks for checking it out... if you have ideas for improvements, feel free to comment or make a PR on my github repo: https://github.com/csjcode/solutions-architect-metrics-cheatsheet