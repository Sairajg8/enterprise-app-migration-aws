# Enterprise Application Migration & Cloud-Native Refactoring

## 📌 Project Overview
This project demonstrates the architectural migration and re-engineering of a local multi-tier monolithic application into a highly resilient, fully managed, and scalable cloud-native ecosystem on AWS. 

By moving away from on-premise style administration (hosting everything on raw virtual machines), this architecture leverages AWS managed services to improve elasticity, security boundaries, and operational efficiency.

## 🏗️ Architecture Design
The incoming web traffic flows through the following secure topology:
`User ➔ Route 53 ➔ Elastic Load Balancer (ALB) ➔ Elastic Beanstalk (EC2 Auto-Scaling Group) ➔ Private Data Subnets (RDS / ElastiCache / Amazon MQ)`

## 🛠️ Infrastructure Mapping (Local vs. Cloud-Native)
To minimize administrative overhead and achieve high availability, the underlying components were refactored as follows:
* **Application Tier:** Migrated from a standalone Tomcat Server to **AWS Elastic Beanstalk**, configuring automated rolling deployments, health monitoring, and scaling policies.
* **Database Layer:** Replaced a self-hosted MySQL instance with multi-AZ **Amazon RDS (MySQL)** for built-in replication, automated failover, and automated patching.
* **Caching Layer:** Replaced a local Memcached service with **Amazon ElastiCache (Memcached)** to decouple application state and deliver sub-millisecond data retrieval.
* **Asynchronous Messaging:** Replaced a local RabbitMQ server with **Amazon MQ (Managed RabbitMQ)** to ensure decoupled, reliable messaging without broker overhead.
* **DNS & Traffic Routing:** Configured **Amazon Route 53** for private DNS resolution to seamlessly bridge the application components together securely.

## 🚀 Key Implementation Milestones
1. **Network & Security Boundary Isolation:** Formulated tight AWS Security Group rules adhering to the principle of least privilege, explicitly shielding database, caching, and messaging tiers from direct public internet exposure.
2. **Managed Data Stores Provisioning:** Deployed multi-AZ relational databases and distributed cache networks inside dedicated subnets.
3. **Environment Property Mapping:** Updated `application.properties` to cleanly direct database connections, cache nodes, and broker wire endpoints to the live AWS service endpoints.
4. **Automated Application Assembly:** Leveraged Maven to compile and package the source files into a unified deployable `.war` artifact for automated execution via Elastic Beanstalk.

