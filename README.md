# Advanced Networking Cert Study

## DNS

DNS resolver runs on a reserved IP address for the VPC network range, plus 2. For example, the DNS Server on a 10.0.0.0/16 network is located at 10.0.0.2.

Route 53 Resolver is also available at 169.254.169.2**53**

**enableDnsHostnames** - the default for this attribute is false, unless the VPC is default or the VPC was created usign the VPC console wizard

**enableDnsSupport** - Queries to the Amazon provided DNS server succeed, default is true no matter how the VPC was created

If both set to `true`: 

* instances with public IP addresses recieve corresponding public DNS hostnames
* The Amazon Route 53 Resolver server can resolve Amazon-provided private DNS hostnames

If at least one set to `false`: 

* Intsances with public IP addresses do not recieve public DNS hostnames
* Route53 Resolver cannot resolve Amazon-provided private DNS hostnames
* Instances recieve custom private DNS hostnames if there is a custom domain name in the DHCP options set

If you use custom DNS hostnames defined in private hosted zone, or private DNS with interface VPC endpoints, you must set both attributes to `true`

**Route53 Resolver listens** - .2 of subnets and 169.254.169.253. IPV6: fd00:ec2::253

### DHCP Options Set 

**domain-name-servers** - IP addresses for up to four IPv4 dns servers and four IPv6 dns servers

**domain-name** - custom domain name for your instances

**ntp-servers** - the ip addresses of up to eight NTP servers 

**netbios-name-servers** - the ips of up to four NetBIOS name servers 

**netbios-node-type** - the NetBIOS node type (1,2,4,8) 

## Routing priority 

Order of BGP path selection from MOST preferred to LEAST preferred:

1. Longest prefix 

1. BGP propagated routes from an AWS Direct Connect connection.

1. Manually added static routes for a Site-to-Site VPN connection.

1. BGP propagated routes from a Site-to-Site VPN connection.

1. For matching prefixes where each Site-to-Site VPN connection uses BGP, the AS PATH is compared and the prefix with the shortest AS PATH is preferred. Alternatively, you can prepend AS_PATH, so that the path is less preferred.

1. When the AS PATHs are the same length and if the first AS in the AS_SEQUENCE is the same across multiple paths, multi-exit discriminators (MEDs) are compared. The path with the lowest MED value is preferred.

## Load Balancers

### General notes 

You can only specify one protocol and port number per target group.

### GLB

Gateway Load Balancer (GLB) - designed for security appliances

Integrates with auto scaling

### ALB

OSI Layer 7

Protocol Listeners HTTP, HTTPS, gRPC

No PrivateLink support

No static IP address

HTTP header based routing

Source IP preservation with `x-forwarded-for`

SSL termination at load balancer

### NLB

OSI layer 4

Protocol Listeners TCP, UDP, TLS

Private Link support over TCP/TLS

Yes static IP address

No HTTP header based routing

Source IP preservation is native

SSL Termination at load balancer or target

## ECS Networking

**awsvpc** - The task is allocated its own elastic network interface (ENI) and a primary private IPv4 address

**bridge** - The task utilizes Docker's built-in virtual network which runs inside each Amazon EC2 instance hosting the task

**host** - The task bypassess Docker's built-in virtual network and maps container ports directly to the ENI of the Amazon EC2 instance hosting the task

**none** - no external networking 

## EKS Networking

### Pod Networking

Amazon EKS supports native VPC networking with the Amazon VPC Container Network Interface (CNI) plugin for Kubernetes that assigns private IPv4 or IPv6 from VPC to each pod









