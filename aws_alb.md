# Freedom on the Move - AWS Infrastructure Documentation

## Load Balancing Configuration

The project uses Application Load Balancers (ALBs) to distribute traffic to the ECS services. There are two ALBs configured:

### 1. Legacy API Load Balancer (fotm-legacy-api-alb)

- **Status:** Active
- **Type:** Application Load Balancer (ALB)
- **Scheme:** Internet-facing
- **IP Address Type:** IPv4
- **VPC:** vpc-0a3db9b844c9f214c
- **Hosted Zone ID:** Z35SXDOTRQ7X7K
- **Created:** August 29, 2023, 11:24 (UTC-04:00)
- **DNS Name:** fotm-legacy-api-alb-861843054.us-east-1.elb.amazonaws.com (A Record)
- **ARN:** arn:aws:elasticloadbalancing:us-east-1:928084024497:loadbalancer/app/fotm-legacy-api-alb/46f75176a5c3a2be

**Availability Zones & Subnets:**
- us-east-1f (us1-az5): subnet-0b89eb6c205730a8
- us-east-1e (us1-az3): subnet-0785b18597b81715e
- us-east-1a (us1-az6): subnet-0b97ace067574da3b
- us-east-1b (us1-az1): subnet-0e0993c5f775b0ad9
- us-east-1c (us1-az2): subnet-06dbffca685f71724
- us-east-1d (us1-az4): subnet-0dc108532d9f03a0b

**Listeners and Rules:**
1. **HTTP:80**
   - Default Action: Redirect to HTTPS://#{host}:443/#{path}?#{query}
   - Status Code: HTTP_301
   - Rules: 1 rule

2. **HTTPS:443**
   - Default Action: Forward to target group
   - Target Group: ecs-fotm-legacy-api-tg (1 target, 100% traffic)
   - Target Group Stickiness: Off
   - Rules: 1 rule
   - Security Policy: ELBSecurityPolicy-TLS13-1-2-...
   - SSL/TLS Certificate: freedomonthemove.org (Certificate)
   - mTLS: Off

### 2. Database Load Balancer (fotm-database-alb)

- **Status:** Active
- **Type:** Application Load Balancer (ALB)
- **Scheme:** Internet-facing
- **IP Address Type:** IPv4
- **VPC:** vpc-0a3db9b844c9f214c
- **Hosted Zone ID:** Z35SXDOTRQ7X7K
- **Created:** November 10, 2023, 12:04 (UTC-05:00)
- **DNS Name:** fotm-database-alb-578528851.us-east-1.elb.amazonaws.com (A Record)
- **ARN:** arn:aws:elasticloadbalancing:us-east-1:928084024497:loadbalancer/app/fotm-database-alb/be2249bec36861d2

**Availability Zones & Subnets:**
- Same as the Legacy API ALB (all 6 AZs in us-east-1)

**Listeners and Rules:**
1. **HTTPS:443**
   - Default Action: Forward to target group
   - Target Group: ecs-fotm-database-tg (1 target, 100% traffic)
   - Target Group Stickiness: Off
   - Rules: 3 rules
   - Security Policy: ELBSecurityPolicy-TLS13-1-2-...
   - SSL/TLS Certificate: freedomonthemove.org (Certificate)
   - mTLS: Off

2. **HTTP:80**
   - Default Action: Redirect to HTTPS://#{host}:443/#{path}?#{query}
   - Status Code: HTTP_301
   - Rules: 1 rule

## Load Balancing Architecture

The load balancing configuration reveals the following architecture:

1. **Multi-AZ Deployment:** Both load balancers are deployed across all six availability zones in the us-east-1 region, providing high availability.

2. **SSL/TLS Termination:** Both load balancers handle SSL/TLS termination with certificates for freedomonthemove.org.

3. **HTTP to HTTPS Redirection:** Both load balancers redirect HTTP traffic to HTTPS, enforcing secure connections.

4. **Service Mapping:**
   - The Legacy API ALB routes traffic to the `fotm-legacy-api-service` running in ECS
   - The Database ALB routes traffic to the `fotm-database-service` running in ECS

5. **Target Groups:**
   - ecs-fotm-legacy-api-tg: Target group for the legacy API service
   - ecs-fotm-database-tg: Target group for the database service
