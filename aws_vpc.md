# Freedom on the Move - AWS Infrastructure Documentation

## Networking Configuration

### VPC (Virtual Private Cloud)

- **VPC ID:** vpc-0a3db9b844c9f214c
- This VPC hosts all the infrastructure components for the Freedom on the Move project.

### Security Groups

#### Main Production Security Group

- **Security Group Name:** FOTM Prod SG
- **Security Group ID:** sg-0bdeb19338cc30509
- **Description:** Production FOTM SG
- **Owner AWS Account:** 928084024497

#### Inbound Rules

The security group has the following inbound rules allowing traffic to the application:

1. **PostgreSQL Access Rules:**
   - Port: 5432 (PostgreSQL)
   - Protocol: TCP
   - Sources:
     - 128.84.116.208/32 - Cornell
     - 128.253.0.0/16 - Cornell

2. **Web Traffic Rules:**
   - Port: 80 (HTTP)
   - Protocol: TCP
   - Source: 0.0.0.0/0 (open to all IPv4 addresses)
   
   - Port: 443 (HTTPS)
   - Protocol: TCP
   - Source: 0.0.0.0/0 (open to all IPv4 addresses)
   
   - IPv6 HTTP (Port 80) and HTTPS (Port 443) are also configured

3. **SSH Access Rules:**
   - Port: 22 (SSH)
   - Protocol: TCP
   - Sources:
     - 128.253.0.0/16 - Cornell
     - 128.84.0.0/16 - Cornell

4. **Self-referencing Rule:**
   - Type: All traffic
   - Protocol: All
   - Source: sg-0bdeb19338cc30509 (self-reference to allow all traffic between resources using this security group)

#### Outbound Rules

   - Allow-all rule (0.0.0.0/0) for outbound traffic

### Network Security Comments

1. **Database Access:** PostgreSQL access is restricted to specific IP addresses/ranges, which appears to include Cornell University networks (128.84.x.x, 128.253.x.x) and possibly specific developer or administrator IP addresses.

2. **Web Access:** HTTP and HTTPS access is open to the world (0.0.0.0/0), allowing public access to the web application.

3. **SSH Access:** SSH access is limited to specific IP addresses/ranges, providing administrative access from trusted locations only.

4. **Internal Communication:** Resources using this security group can communicate freely with each other through the self-referencing rule.
