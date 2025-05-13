# Freedom on the Move - AWS Infrastructure Documentation

## ECS (Elastic Container Service)

The project uses Amazon ECS with Fargate for containerized applications:

### Cluster Configuration

- **Cluster Name:** fotm
- **Status:** Active
- **ARN:** arn:aws:ecs:us-east-1:928084024497:cluster/fotm
- **CloudWatch Monitoring:** Default

### Services Overview

The cluster contains 4 active services, all running on Fargate:

1. **fotm-database-search-service**
   - **Status:** Active
   - **Service Type:** REPLICA
   - **Launch Type:** FARGATE
   - **Task Definition:** fotm-mellisearch:2
   - **Deployments:** 1/1 Tasks running

2. **fotm-database-service**
   - **Status:** Active
   - **Service Type:** REPLICA
   - **Launch Type:** FARGATE
   - **Task Definition:** fotm-database:8
   - **Deployments:** 1/1 Tasks running

3. **fotm-legacy-api-service**
   - **Status:** Active
   - **Service Type:** REPLICA
   - **Launch Type:** FARGATE
   - **Task Definition:** fotm-legacy-api-td:2
   - **Deployments:** 1/1 Tasks running

4. **fotm-link-redirector-service**
   - **Status:** Active
   - **Service Type:** REPLICA
   - **Launch Type:** FARGATE
   - **Task Definition:** fotm-link-redirector:1
   - **Deployments:** 1/1 Tasks running

### Service Architecture

Based on the service names, the application architecture appears to consist of:

1. **Database Search Service** - Provides search functionality using MeiliSearch, a search engine optimized for fast, relevant search results.

2. **Database Service** - Handles database operations and interactions with the RDS PostgreSQL instance. API powers database.freedomonthemove.org

3. **Legacy API Service** - Provides API endpoints for the crowdsourcing application.

4. **Link Redirector Service** - Manages URL redirections for the fotm.link redirection service.

### ECS/Fargate Configuration Notes

- All services are using the REPLICA service type, which maintains the desired count of tasks and restarts tasks if they fail.
- All visible services are using the Fargate launch type, which is serverless and eliminates the need to provision and manage servers.
