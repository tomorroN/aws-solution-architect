Leverage **AWS Database Migration Service (AWS DMS)** as a bridge between **Amazon S3** and **Amazon Kinesis Data Streams**
![img.png](diagrams/aws-dms-as-a-bridge-diagram.png)

**Amazon VPC** provides the facility to create an IPsec VPN connection (also known as AWS site-to-site VPN) between remote customer networks and their Amazon VPC over the internet. The following are the key concepts for a site-to-site VPN:
- Virtual private gateway: A virtual private gateway (VGW), also known as a VPN Gateway is the endpoint on the AWS VPC side of your VPN connection.
- VPN connection: A secure connection between your on-premises equipment and your VPCs.
- VPN tunnel: An encrypted link where data can pass from the customer network to or from AWS.
- Customer Gateway: An AWS resource that provides information to AWS about your Customer Gateway device.
- Customer Gateway device: A physical device or software application on the customer side of the Site-to-Site VPN connection.

![img.png](diagrams/amazon-ipsec-vpn-connection-diagram.png)

**Throttling** is the process of limiting the number of requests an authorized program can submit to a given operation in a given amount of time.
- Services that supports throttling: **Amazon API Gateway, Amazon Simple Queue Service (Amazon SQS) and Amazon Kinesis**
- To prevent your API from being overwhelmed by too many requests, Amazon API Gateway throttles requests to your API 
  using the token bucket algorithm, where a token counts for a request. Specifically, API Gateway sets a limit on a 
  steady-state rate and a burst of request submissions against all APIs in your account. In the token bucket algorithm,
  the burst is the maximum bucket size. 
- Amazon Simple Queue Service (Amazon SQS) - Amazon Simple Queue Service (SQS) is a fully managed message queuing service
  that enables you to decouple and scale microservices, distributed systems, and serverless applications. Amazon SQS offers 
  buffer capabilities to smooth out temporary volume spikes without losing messages or increasing latency.
- Amazon Kinesis - Amazon Kinesis is a fully managed, scalable service that can ingest, buffer, and process streaming data in real-time.
