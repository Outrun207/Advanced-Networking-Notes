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

You can only specify one protocol and port number per target group.
