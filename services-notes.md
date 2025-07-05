**Amazon CloudFront** - CDN, edges, caching, origin failover

**Amazon Global Accelerator** - network layer service that directs traffic to optimal endpoints over the AWS global network,
this improves the availability and performance of your internet applications. It provides two static anycast IP addresses
that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers,
Network Load Balancers, Elastic IP addresses or Amazon EC2 instances, in a single or in multiple AWS regions. 
UDP, IoT (MQTT), Voice Over IP, HTTP. CloudFront is better for improving application resiliency to handle spikes in traffic.

**Amazon Aurora** - if the writer instance in a cluster with read replicas becomes unavailable, Aurora automatically 
promotes one of the reader instances to take place as a new writer. Up to 15 Replicas can be distributed across the Availability Zones (AZs)

**Amazon Kinesis Data Streams** - Amazon Kinesis Data Streams is useful for rapidly moving data off data producers and 
then continuously processing the data, be it to transform the data before emitting to a data store, run real-time metrics 
and analytics, or derive more complex data streams for further processing. Kinesis data streams can continuously capture 
gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, 
financial transactions, social media feeds, IT logs, and location-tracking events.
- **Enhanced Fan-Out** - With enhanced fan-out developers can register stream consumers to use enhanced fan-out and 
receive their own 2MB/second pipe of read throughput per shard, and this throughput automatically scales with the number of shards in a stream.
![img.png](diagrams/amazon-kinesis-data-streams-enhanced-fan-out-diagram.png)

![img.png](diagrams/amazon-kinesis-data-streams-diagram.png)

**Amazon Kinesis Data Firehose** - Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores 
and analytics tools. Kinesis Firehose cannot be used to process and analyze the streaming data in custom applications. 
It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, 
and Splunk, enabling near real-time analytics.
![img.png](diagrams/amazon-kinesis-data-firehose-diagram.png)

**Amazon S3 (Simple Storage Service)** - Object storage, data lake, static website hosting, versioning, lifecycle policies, cross-region replication,
S3 Glacier for archiving. Strong read-after-write consistency. Always returns the latest version of an object.
- **Amazon S3 Transfer Acceleration (Amazon S3TA)** - speeds up content uploads to S3 by routing traffic through the AWS global network.
- **Amazon multipart upload** - allows you to upload large objects in parts, improving upload speed and reliability. 
If object size is greater than 100 MB, multipart upload is recommended.
- Storage classes:
  - **S3 Standard** - General-purpose storage for frequently accessed data.
  - **S3 Intelligent-Tiering** - Automatically moves data between two access tiers when access patterns change.
  - **S3 Standard-IA (Infrequent Access)** - For long-lived but infrequently accessed data.
  - **S3 One Zone-IA** - Lower-cost option for infrequently accessed data that does not require multiple AZ resilience.
  - **S3 Glacier** - Low-cost storage for archival data with retrieval times ranging from minutes to hours.
  - **S3 Glacier Deep Archive** - Lowest-cost storage class for long-term archival data with retrieval times of up to 12 hours.
  ![img.png](diagrams/amazon-s3-transitions-diagram.png)
- **S3 Object Lock** - Allows you to store objects using a write-once-read-many (WORM) model. It can help you prevent objects
from being deleted or overwritten for a fixed amount of time or indefinitely.
- **S3 Object Versioning** - Enables you to keep multiple versions of an object in the same bucket. It helps protect against accidental deletions
- **Amazon S3 File Gateway** - seamlessly connects on-premises applications to the cloud to store and access archive repositories,
  application data, and database backups as durable objects in Amazon S3. S3 File Gateway is used for on-premises data 
  intensive applications that need file protocol access to objects in S3. For online data migrations, you can use. 
  To migrate data offline, you can use AWS Snow Family.

**Amazon EC2 (Elastic Compute Cloud)** - Virtual servers, auto-scaling, load balancing, security groups, EBS volumes.
Max 7 instances per AZ per group.

- Placement techniques for EC2 instances:
  - **Spread Placement** - Distributes instances across underlying hardware to reduce correlated failures.
  - **Cluster Placement** - Packs instances close together (inside AZ) for high throughput and low latency.
  - **Partition Placement** - Distributes instances across logical partitions to isolate failures.

- Root device types:
  - **EBS-backed** - Uses Amazon EBS volumes as root devices (Linux and Windows AMIs). Supports features like snapshots, 
  resizing, and encryption.
  - **Instance Store-backed** - Uses instance store volumes as root devices (Linux AMIs only). Provides temporary storage
- Dedicated Hosts and Dedicated Instances:
  - **Dedicated Host** - Physical server dedicated to your use, allowing you to run multiple instances on it. Useful for 
  compliance and licensing requirements.
  - **Dedicated Instance** - Instances that run on hardware dedicated to a single customer, but do not provide visibility into 
  the underlying host.
- A **launch template** is similar to a **launch configuration**, in that it specifies instance configuration information. 
  It includes the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and other parameters 
  used to launch EC2 instances. However, defining a launch template instead of a launch configuration allows you to have 
  multiple versions of a launch template.
- Using **Amazon CloudWatch** alarm actions, you can create alarms that automatically stop, terminate, reboot, or recover 
  your EC2 instances

**Amazon EBS (Elastic Block Store)** - high-performance block storage service designed for use with EC2 for both throughput
and transaction-intensive workloads at any scale. By default, the root volume for an AMI backed by Amazon EBS is deleted
when the instance terminates. When you create an encrypted Amazon EBS volume and attach it to a supported instance type, 
data stored at rest on the volume, data moving between the volume and the instance, snapshots created from the volume and
volumes created from those snapshots are all encrypted. It uses AWS Key Management Service (AWS KMS) customer master keys (CMK)
when creating encrypted volumes and snapshots. Encryption operations occur on the servers that host Amazon EC2 instances,
ensuring the security of both data-at-rest and data-in-transit between an instance and its attached Amazon EBS storage.

**Network Load Balancer** - functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle
millions of requests per second. After the load balancer receives a connection request, it selects a target from the target
group for the default rule. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.
- Request Routing and IP Addresses
  - If you specify targets using an instance ID, traffic is routed to instances using the primary private IP address specified
    in the primary network interface for the instance. The load balancer rewrites the destination IP address from the data packet
    before forwarding it to the target instance.
  - If you specify targets using IP addresses, you can route traffic to an instance using any private IP address from one 
    or more network interfaces. This enables multiple applications on an instance to use the same port. Note that each
    network interface can have its security group. The load balancer rewrites the destination IP address before 
    forwarding it to the target.

**Gateway Load Balancer** - new type of load balancer that operates at layer 3 of the OSI model and is built on Hyperplane,
which is capable of handling several thousands of connections per second. Gateway Load Balancer endpoints are configured
in spoke VPCs originating or receiving traffic from the Internet. This architecture allows you to perform inline inspection
of traffic from multiple spoke VPCs in a simplified and scalable fashion while still centralizing your virtual appliances.

**Amazon Relational Database Service (Amazon RDS)** - managed service that makes it easy to set up, operate, and scale a relational database
in the cloud. It provides cost-efficient and resizable capacity, while managing time-consuming database administration tasks,
freeing you to focus on your applications and business. [Amazon RDS FAQs](https://aws.amazon.com/rds/faqs)

**Amazon Aurora** - MySQL and PostgreSQL-compatible relational database built for the cloud, that combines 
the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open 
source databases. Amazon Aurora features a distributed, fault-tolerant, self-healing storage system that auto-scales up to 64 terabytes 
per database instance.
- **Amazon Aurora DB cluster** - An Amazon Aurora DB cluster consists of one or more DB instances and a cluster volume 
that manages the data for those DB instances.
  - **Primary (writer) DB instance** - Supports read and write operations, and performs all of the data modifications to the cluster volume. 
  Each Aurora DB cluster has one primary DB instance.
  - **Aurora Replica (reader DB instance)** – Connects to the same storage volume as the primary DB instance but supports only read operations.
  Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance.
- Types of Aurora Endpoints:
  - **Cluster endpoint** - The primary endpoint for the Aurora DB cluster. It connects to the primary DB instance.
  - **Reader endpoint** - A load-balanced endpoint that distributes connections to all available Aurora Replicas in the cluster.
  - **Custom endpoint** - Allows you to create a custom endpoint that connects to a specific set of instances in the cluster.
- A high-performance storage solution with reliable throughput and minimal latency is PIOPS SSD storage. Workloads like 
  insert operations, which demand high I/O performance, are ideally suited for it.

**Amazon DynamoDB** - NoSQL database, key-value and document store, global tables, on-demand capacity,  multi-region, 
multi-master, durable database with built-in security, backup and restore, and in-memory caching. 
- **DAX** is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance for 
demanding applications. DAX does not support SQL query caching.

**Amazon Neptune** - Amazon Neptune is a fast, reliable, fully managed graph database service that makes it easy to build
and run applications that work with highly connected datasets. Amazon Neptune is highly available, with read replicas, 
point-in-time recovery, continuous backup to Amazon S3, and replication across Availability Zones. Neptune is secure with 
support for HTTPS encrypted client connections and encryption at rest.
![img.png](diagrams/amazon-neptune-diagram.png)

**Amazon OpenSearch Service** - managed service that makes it easy for you to perform interactive log analytics, real-time
application monitoring, website search, and more. OpenSearch is an open source, distributed search and analytics suite derived from Elasticsearch.

**Amazon Redshift** - fully-managed petabyte-scale cloud-based data warehouse product designed for large scale data set 
storage and analysis. The given use-case is not about data warehousing, so this is not a correct option.
- **Redshift Spectrum** - allows you to run queries against exabytes of data in S3 without having to load or transform the data.
![img.png](diagrams/redshift-spectrum-diagram.png)

**AWS Database Migration Service** - helps you migrate databases to AWS quickly and securely. The source database remains fully
operational during the migration, minimizing downtime to applications that rely on the database. With AWS Database Migration Service,
you can continuously replicate your data with high availability and consolidate databases into a petabyte-scale data warehouse
by streaming data to Amazon Redshift and Amazon S3. 
![img.png](diagrams/aws-database-migration-service.png)

**AWS Schema Conversion Tool (AWS SCT)** - tool to convert your existing database schema from one database engine to another.

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

**Amazon FSx for Lustre** - fully managed service that provides high-performance, cost-effective, and scalable storage 
powered by Lustre, the world’s most popular high-performance file system. FSx for Lustre provides the fastest storage 
performance for GPU instances in the cloud with up to terabytes per second of throughput, millions of IOPS, sub-millisecond 
latencies, and virtually unlimited storage capacity. It delivers up to 34% better price performance compared to on-premises 
HDD file storage and up to 70% better price performance compared to other cloud-based Lustre storage. Use cases include
high-performance computing (HPC), machine learning, financial modeling, seismic reservoir simulations, and media data processing.

**Amazon FSx for Windows File Server** -  provides fully managed, highly reliable, and scalable file storage that is accessible
over the industry-standard Service Message Block (SMB) protocol. It is built on Windows Server, delivering a wide range of 
administrative features such as user quotas, end-user file restore, and Microsoft Active Directory (AD) integration.

**Amazon EMR** - industry-leading cloud big data platform for processing vast amounts of data using open 
source tools such as Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto. Amazon EMR uses Hadoop,
an open-source framework, to distribute your data and processing across a resizable cluster of Amazon EC2 instances.
You can deploy your workloads to EMR using Amazon EC2, Amazon Elastic Kubernetes Service (EKS), or on-premises AWS Outposts.

**AWS Glue** - AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to 
prepare and load their data for analytics. AWS Glue job is meant to be used for batch ETL data processing.

**AWS Elastic Beanstalk** - easy-to-use service for deploying and scaling web applications and services developed with Java,
.NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.

You can simply upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, 
load balancing, auto-scaling to application health monitoring. At the same time, you retain full control over the AWS resources
powering your application and can access the underlying resources at any time.

When you create an AWS Elastic Beanstalk environment, you can specify an Amazon Machine Image (AMI) to use instead of the
standard Elastic Beanstalk AMI included in your platform version. A custom AMI can improve provisioning times when instances
are launched in your environment if you need to install a lot of software that isn't included in the standard AMIs.

**Amazon Simple Notification Service (Amazon SNS)** - is a highly available, durable, secure, fully managed pub/sub messaging 
service that enables you to decouple microservices, distributed systems, and serverless applications. SNS cannot be used 
to decouple the producers and consumers for the real-time data processor as described in the given use-case.

**Amazon Simple Queue Service (Amazon SQS)** - offers a secure, durable, and available hosted queue that lets you integrate and
decouple distributed software systems and components. SQS cannot be used to decouple the producers and consumers for the 
real-time data processor as described in the given use-case.
- Amazon SQS offers two types of message queues. 
  - **Standard** queues offer maximum throughput, best-effort ordering, and at-least-once delivery. 
  - **FIFO** queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent. 
    By default, FIFO queues support up to 3,000 messages per second with batching, or up to 300 messages per second 
    (300 send, receive, or delete operations per second) without batching. Therefore, using batching you can meet a throughput
    requirement of upto 3,000 messages per second. The name of a FIFO queue must end with the .fifo suffix. 
    The suffix counts towards the 80-character queue name limit. To determine whether a queue is FIFO, you can check whether
    the queue name ends with the suffix.

**AWS DataSync** - online data transfer service that simplifies, automates, and accelerates copying large amounts of data
between on-premises storage systems and AWS Storage services, as well as between AWS Storage services. You can use AWS DataSync
to migrate data located on-premises, at the edge, or in other clouds to Amazon S3, Amazon EFS, Amazon FSx for Windows File Server,
Amazon FSx for Lustre, Amazon FSx for OpenZFS, and Amazon FSx for NetApp ONTAP.
![img.png](diagrams/aws-data-sync-diagram.png)

**Amazon Elastic Container Service (Amazon ECS)** - fully managed container orchestration service. 
ECS allows you to easily run, scale, and secure Docker container applications on AWS.
![img.png](diagrams/amazon-ecs-diagram.png)

**AWS Lambda** - With AWS Lambda, you can run code without provisioning or managing servers. You pay only for the compute time
that you consume—there’s no charge when your code isn’t running. You can run code for virtually any type of application or
backend service—all with zero administration.
- [Best practices for AWS Lambda](https://aws.amazon.com/blogs/architecture/best-practices-for-developing-on-aws-lambda/)
- **Lambda layers** - distribution mechanism for libraries, custom runtimes, and other dependencies that you can use in your Lambda functions.

![img.png](diagrams/aws-lambda-layer-diagram.png)

**AWS Config** - provides a detailed view of the configuration of AWS resources in your AWS account. This includes how the
resources are related to one another and how they were configured in the past so that you can see how the configurations 
and relationships change over time. An AWS resource is an entity you can work with in AWS, such as an 
Amazon Elastic Compute Cloud (EC2) instance, an Amazon Elastic Block Store (EBS) volume, a security group, or an 
Amazon Virtual Private Cloud (VPC). For a complete list of AWS resources supported by AWS Config, see [Supported 
Resource Types for AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html).
![img.png](diagrams/aws-config-diagram.png)

**Amazon Cognito** - user identity and access management service that scales to hundreds of millions of users.
User pools are for authentication. Your app users can sign in through the user pool, or federate through a third-party 
identity provider (IdP). Identity pools are for authorization. You can use identity pools to create unique identities
for users, and give them access to other AWS services.
- Use a user pool in the following scenarios:
  - Design sign-up and sign-in webpages for your app.
  - Access and manage user data.
  - Track your user device, location, and IP address, and adapt to sign-in requests of different risk levels.
  - Use a custom authentication flow for your app.
- Use an identity pool in the following scenarios:
  - Give your users access to AWS resources, such as an Amazon Simple Storage Service (Amazon S3) bucket or an Amazon DynamoDB table.
  - Generate temporary AWS credentials for unauthenticated users.

**CloudWatch** - service that monitors applications, responds to performance changes, optimizes resource use, and provides
insights into operational health. By collecting data across AWS resources, CloudWatch gives visibility into system-wide 
performance and allows users to set alarms, automatically react to changes, and gain a unified view of operational health.
- **CloudWatch Shared Dashboards** - allows you to share dashboards with people who do not have direct access to your AWS account.
  This enables you to share dashboards across teams, with stakeholders, and with people external to your organization. 
  You can even display dashboards on big screens in team areas, or embed them in Wikis and other webpages.

**Amazon AppFlow** - fully-managed integration service that enables you to securely exchange data between software as a 
service (SaaS) applications, such as Salesforce, and AWS services, such as Amazon Simple Storage Service (Amazon S3) and Amazon Redshift.
The use of Appflow helps to remove the ec2 as the middle layer which slows down the process of data transmission and introduce an additional variable.
Appflow is also a fully managed AWS service, thus reducing the operational overhead.
