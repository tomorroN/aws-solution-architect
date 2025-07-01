**VPC NAT Gateway** - A managed NAT service that allows instances in a private subnet in your VPC to access the 
internet (IPv4) while preventing inbound traffic from the internet.

**VPC NAT Instance** - An EC2 instance configured to perform NAT for instances in a private subnet. 
It requires manual management and scaling. NAT Gateway is preferred for production use due to its managed nature and scalability.
Full comparison: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html


