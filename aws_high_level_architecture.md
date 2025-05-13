## Complete Infrastructure Architecture

1. **Web Layer:**
   - Two internet-facing Application Load Balancers (ALBs) handle incoming traffic
   - SSL/TLS termination at the load balancer level
   - Automatic HTTP to HTTPS redirection

2. **Application Layer:**
   - ECS Fargate cluster with four containerized services:
     - fotm-database-service: Handles database operations
     - fotm-database-search-service: Provides search functionality (likely MeiliSearch)
     - fotm-legacy-api-service: Provides API endpoints
     - fotm-link-redirector-service: Manages URL redirections

3. **Database Layer:**
   - PostgreSQL RDS instance (fotm-prod): Main application database
   - MySQL RDS instance (fotm-ghost-mysql): Ghost CMS database

4. **Content (Websites / Images / Assets)**
   - Websites, advertisement images and other assets all live in S3 buckets
   - Content held in S3 Buckets is served via Cloudfront for caching and SSL

5. **Networking:**
   - Dedicated VPC (vpc-0a3db9b844c9f214c)
   - Security groups controlling access to different components

6. **Security:**
   - HTTPS enforced for all web traffic
   - Restricted SSH and database access
   - AWS KMS for database encryption
