**Amazon CloudFront** - CDN, edges, caching, origin failover

**Amazon Global Accelerator** - Improve availability and performance globally. UDP, IoT (MQTT), Voice Over IP, HTTP. 
CloudFront is better for improving application resiliency to handle spikes in traffic.

**Amazon Aurora** - if the writer instance in a cluster with read replicas becomes unavailable, Aurora automatically 
promotes one of the reader instances to take place as a new writer. Up to 15 Replicas can be distributed across the Availability Zones (AZs)

**Amazon Kinesis Data Streams** - Amazon Kinesis Data Streams is useful for rapidly moving data off data producers and 
then continuously processing the data, be it to transform the data before emitting to a data store, run real-time metrics 
and analytics, or derive more complex data streams for further processing. Kinesis data streams can continuously capture 
gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, 
financial transactions, social media feeds, IT logs, and location-tracking events.

![img.png](diagrams/amazon-kinesis-data-streams-diagram.png)

**Amazon Kinesis Data Firehose** - Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores 
and analytics tools. Kinesis Firehose cannot be used to process and analyze the streaming data in custom applications. 
It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, 
and Splunk, enabling near real-time analytics.
![img.png](diagrams/amazon-kinesis-data-firehose-diagram.png)

**Amazon S3 (Simple Storage Service)** - Object storage, data lake, static website hosting, versioning, lifecycle policies, cross-region replication,
S3 Glacier for archiving. Strong read-after-write consistency. Always returns the latest version of an object.
- Amazon S3 Transfer Acceleration (Amazon S3TA) - speeds up content uploads to S3 by routing traffic through the AWS global network.
- Amazon multipart upload - allows you to upload large objects in parts, improving upload speed and reliability. 
If object size is greater than 100 MB, multipart upload is recommended.

**Amazon EC2 (Elastic Compute Cloud)** - Virtual servers, auto-scaling, load balancing, security groups, EBS volumes.
Max 7 instances per AZ per group.

Placement techniques for EC2 instances:
- **Spread Placement** - Distributes instances across underlying hardware to reduce correlated failures.
- **Cluster Placement** - Packs instances close together (inside AZ) for high throughput and low latency.
- **Partition Placement** - Distributes instances across logical partitions to isolate failures.

**Amazon DynamoDB** - NoSQL database, key-value and document store, global tables, on-demand capacity,  multi-region, 
multi-master, durable database with built-in security, backup and restore, and in-memory caching.

**Amazon GuardDuty** - Threat detection service that continuously monitors for malicious activity and unauthorized behavior.
GuardDuty analyzes continuous streams of meta-data generated from your account and network activity found in AWS CloudTrail Events, 
Amazon VPC Flow Logs, and DNS Logs. It also uses integrated threat intelligence such as known malicious IP addresses, 
anomaly detection, and machine learning to identify threats more accurately. Review findings in the GuardDuty console,
or integrate into event management, workflow systems or trigger AWS Lambda.
![img.png](diagrams/amazon-guard-duty-diagram.png)

**Amazon Macie** - Security service that uses machine learning and pattern matching to discover, classify, and protect 
sensitive data and PII in Amazon S3. Send results to Amazon CloudWatch Events for alerting and remediation.
![img.png](diagrams/amazon-macie-diagram.png)

**AWS Compute Optimizer** - Get recommendations to optimize the performance and cost of your AWS resources. EC2, EC2 Auto Scaling, and RDS
