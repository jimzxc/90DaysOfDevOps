# Day 15 — Networking concepts
## DNS (`dig`)
### Full query
```bash
dig google.com
```

### Answers only
```bash
dig google.com +noall +answer
```

### Interfaces & addresses
```bash
ip addr show
```

## Private IP vs public IP
### Private IP
```bash
Used inside a VPC, LAN, or lab network (Docker/K8s networking is related but has extra concepts).
Not globally unique on the public internet like provider public space.
Outbound internet access usually goes through NAT (home router, NAT gateway, cloud NAT).
Helps avoid exposing workloads directly on the public internet.
```

### Public IP
```bash
Globally routable on the internet (assigned by an ISP or cloud provider).
Often used for ingress (load balancer, bastion, NAT gateway) and can be what a DNS A record points to.
```

## CIDR
```bash
CIDR defines an IPv4 network block and how large it is using address/prefix (example: 10.0.0.0/16).

The prefix length (/24, /16, …) tells you how many addresses exist in that subnet (and therefore how you carve subnets for routing and security boundaries).
Quick sizing (typical IPv4 LAN subnets)
Let h = 32 − prefix.

Total IPs: 2^h
Usable hosts (network + broadcast reserved): 2^h − 2
```