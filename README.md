# Advanced Networking Cert Study

## DNS

DNS resolver runs on a reserved IP address for the VPC network range, plus 2. For example, the DNS Server on a 10.0.0.0/16 network is located at 10.0.0.2.

Route 53 Resolver is also available at 169.254.169.2**53**

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


