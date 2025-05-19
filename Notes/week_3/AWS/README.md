# AWS Notes

## Cloud Computing Definition

### **What is Cloud Computing?**

Cloud computing is the delivery of computing services—such as servers, storage, databases, networking, software, analytics, and intelligence—over the internet (“the cloud”) to provide faster innovation, flexible resources, and economies of scale. Instead of owning and maintaining physical data centers or servers, organizations rent access to these resources from cloud providers.

### **Key Characteristics of Cloud Computing**:

1. **On-Demand Self-Service**: Users can provision computing resources as needed without requiring human intervention from the provider.
2. **Broad Network Access**: Services are accessible over the internet through standard devices like laptops, smartphones, or tablets.
3. **Resource Pooling**: Resources are pooled to serve multiple customers, with the ability to dynamically allocate and reallocate resources based on demand.
4. **Rapid Elasticity**: Resources can scale up or down quickly, often automatically, to meet workload demands.
5. **Measured Service**: Cloud usage is metered, and customers only pay for what they use.

### **Benefits of Cloud Computing**:

- Reduced operational and capital costs.
- Scalability and flexibility to adapt to changing business needs.
- Enhanced collaboration through remote accessibility.
- Built-in security and compliance measures by major providers.

## Cloud Computing Model Types

### **1. Service Models**

Service models define the scope of cloud services provided by a vendor.

### **a) Infrastructure as a Service (IaaS)**

- **Definition**: Provides virtualized computing resources over the internet. Users rent infrastructure like servers, storage, and networks.
- **Responsibilities**: Users manage operating systems, applications, and data, while the provider handles hardware and virtualization.
- **Examples**: Amazon EC2, Microsoft Azure VMs, Google Compute Engine.
- **Use Cases**:
    - Hosting websites and applications.
    - Storage and backup solutions.
    - Development and testing environments.

### **b) Platform as a Service (PaaS)**

- **Definition**: Provides a platform and environment to build, deploy, and manage applications without managing the underlying infrastructure.
- **Responsibilities**: The provider manages the infrastructure and runtime, while users focus on application development.
- **Examples**: Heroku, Google App Engine, Microsoft Azure App Service.
- **Use Cases**:
    - Developing scalable web applications.
    - Simplifying application lifecycle management.

### **c) Software as a Service (SaaS)**

- **Definition**: Provides fully managed software applications accessible through a web browser. Users interact directly with the application without worrying about the underlying platform or infrastructure.
- **Responsibilities**: The provider manages everything—applications, runtime, OS, servers, and storage.
- **Examples**: Google Workspace, Salesforce, Dropbox.
- **Use Cases**:
    - Email and collaboration tools.
    - CRM and ERP systems.

---

### **2. Deployment Models**

Deployment models define how cloud services are accessed and managed based on the needs of the organization.

### **a) Public Cloud**

- **Definition**: Resources are owned and operated by third-party cloud service providers and shared among multiple tenants.
- **Benefits**: Cost-effective, scalable, easy to set up.
- **Examples**: Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform.
- **Use Cases**:
    - Startups needing low-cost scalability.
    - Test and development environments.

### **b) Private Cloud**

- **Definition**: Cloud infrastructure dedicated exclusively to a single organization, either hosted on-premises or by a third-party provider.
- **Benefits**: Enhanced security, control, and compliance.
- **Examples**: VMware vSphere, OpenStack Private Cloud.
- **Use Cases**:
    - Financial institutions or healthcare organizations with strict data regulations.
    - Organizations with high-security requirements.

### **c) Hybrid Cloud**

- **Definition**: Combines private and public clouds, allowing data and applications to move between them as needed for flexibility and optimization.
- **Benefits**: Balances cost-efficiency with security and flexibility.
- **Examples**: Microsoft Azure Stack, AWS Outposts.
- **Use Cases**:
    - Organizations with varying workloads, requiring scalability for some parts of the business while keeping sensitive data private.
    - Disaster recovery solutions.

### **d) Multi-Cloud**

- **Definition**: Involves using multiple cloud service providers for different services to avoid dependency on a single vendor.
- **Benefits**: Avoids vendor lock-in, optimizes service selection based on features and pricing.
- **Examples**: Combining AWS for compute with Google Cloud for AI/ML services.
- **Use Cases**:
    - Global organizations leveraging best-of-breed solutions.
    - Businesses with geographically distributed operations.

---

### **Comparison Table: Cloud Service Models**

| Feature | IaaS | PaaS | SaaS |
| --- | --- | --- | --- |
| **Control** | Full control over VMs and OS | Application development | End-user software access |
| **Managed By** | Provider: Hardware | Provider: Hardware + OS | Provider: Everything |
| **Scalability** | High | Moderate | Limited by application |
| **Examples** | AWS EC2, Google Compute | Google App Engine, Heroku | Google Docs, Salesforce |
| **Use Cases** | Hosting, storage, testing | App development | Collaboration, CRM |

---

### **Summary**

Understanding cloud computing and its models is essential for leveraging its full potential. The **service models** (IaaS, PaaS, SaaS) provide flexibility in managing workloads, while the **deployment models** (public, private, hybrid, multi-cloud) cater to various organizational needs. Together, they offer unparalleled adaptability and innovation opportunities for businesses in all industries.

## AWS

## AWS Introduction

Cloud Computing: a service model in which users can access and use shared computing resources, such as servers, storage, and applications, over the internet on a pay-as-you-go basis, rather than owning and maintaining them locally

AWS, or Amazon Web Services, is a collection of cloud computing services owned by Amazon. Amazon is the leader in cloud computing in terms of market-share and currently holds the lead in terms of the number of services it offers. Cloud computing is such an important and relatively recent development in the world of technology, and yet it has already become a very important and integral part of many companies' IT systems. Small startups all the way to large enterprises are able to leverage the power of cloud computing, oftentimes through AWS.

## Benefits of AWS

- Scalability: resources can be scaled out (more) or in (less) as needed, so that you only pay for what you really need to use
- Reliability: AWS's infrastructure is designed to be highly available and fault-tolerant
- Cost-effectiveness: Pay only for what you use, with no upfront costs or long-term commitments
- Global reach: AWS has a global infrastructure with multiple regions and availablility zones, making it easy to deploy and run applications worldwide
- Flexibility: AWS offers a wide range of services, including virtual computing (AWS EC2), storage (S3, EBS, database services, etc.), allowing you to build and run virtually any application or service
- Security: AWS provides a variety of security features and compliance to regulations to help protect your data and applications

## Vertical v. Horizontal Scaling

- A major advantage of cloud computing is the ability to scale quickly based on the growth in the number of customers using the application
- Types of scaling
    - Vertical: Adding more power and resources to a single server (ex. adding more RAM, adding more CPU cores, etc.)
    - Horizontal: Adding more servers (ex. scaling from 1 server to 1000 servers)
- Horizontal scaling is virtually unlimited, while vertical scaling has an upper limit (constrained by physical limitations to what you can add to a single server)
- Horizontal scaling has challenges compared to virtual scaling in terms of how we design our infrastructure. With horizontal scaling, because we're making use of multiple servers, we need some way to distribute traffic out to different servers and deploy the application to all of those servers

## Cloud Computing Service Types

Cloud computing services are categorized based on the level of control, abstraction, and functionality they provide. These types help organizations choose the right solution for their specific needs.

---

### **1. Infrastructure as a Service (IaaS)**

**Definition**:

IaaS provides virtualized computing resources over the internet, such as virtual machines (VMs), storage, and networks. It allows organizations to avoid the complexities of maintaining physical servers.

**Key Features**:

- Full control over the operating system and applications.
- Highly scalable and flexible.
- Pay-as-you-go pricing for resources like CPU, RAM, and disk space.

**Examples**:

- **AWS**: Elastic Compute Cloud (EC2), Elastic Block Store (EBS).
- **Azure**: Virtual Machines, Blob Storage.
- **Google Cloud**: Compute Engine.

**Use Cases**:

- Hosting websites or applications.
- Test and development environments.
- Data storage and backup.

### **2. Platform as a Service (PaaS)**

**Definition**:

PaaS offers a platform with tools and frameworks for developers to build, deploy, and manage applications. It abstracts the underlying infrastructure, enabling faster development without managing servers.

**Key Features**:

- Pre-configured environments for development and deployment.
- Scalability and high availability managed by the provider.
- Supports popular programming languages and frameworks.

**Examples**:

- **AWS**: Elastic Beanstalk, AWS Lambda (Serverless PaaS).
- **Azure**: App Service, Azure Functions.
- **Google Cloud**: App Engine, Cloud Functions.

**Use Cases**:

- Rapid development of scalable web and mobile applications.
- Streamlined application lifecycle management.
- Serverless computing for event-driven workloads.

---

### **3. Software as a Service (SaaS)**

**Definition**:

SaaS provides fully functional software applications over the internet, eliminating the need for installation, maintenance, or updates. Users access these applications via web browsers or APIs.

**Key Features**:

- Managed by the provider (including software updates and security).
- Subscription-based pricing model.
- Accessible from any device with an internet connection.

**Examples**:

- **AWS**: Amazon WorkSpaces, AWS QuickSight.
- **General Examples**: Google Workspace, Microsoft 365, Salesforce.

**Use Cases**:

- Collaboration tools (e.g., Google Docs, Microsoft Teams).
- Customer Relationship Management (CRM) software.
- Enterprise Resource Planning (ERP) software.

## Aws Regions And Availability Zones

**AWS Regions and Availability Zones**

1. **AWS Regions**
    - AWS Regions are geographical locations where AWS data centers are located.
    - Each Region is a separate geographic area, such as "us-east-1" (N. Virginia), "eu-west-1" (Ireland), etc.
    - AWS Regions are completely isolated from each other.
2. **Availability Zones (AZs)**
    - Within each AWS Region, there are multiple Availability Zones.
    - Availability Zones are essentially data centers or clusters of data centers.
    - They are physically separate and isolated from each other but are connected through low-latency, high-throughput networking.
3. **High Availability and Fault Tolerance**
    - Availability Zones within a Region are designed to provide redundancy and high availability.
    - Deploying resources across multiple AZs ensures that if one AZ experiences an issue, your application can continue running in another AZ.
4. **Choosing Regions and AZs**
    - When creating AWS resources, you can select the AWS Region and specify the Availability Zone if necessary.
    - Example JavaScript code to list Availability Zones in a specific Region using the AWS SDK for JavaScript (Node.js):
5. **Benefits of Multiple Regions**
    - Multiple AWS Regions allow you to deploy applications closer to your end-users for lower latency.
    - It also provides disaster recovery options, as you can replicate resources and data across Regions.
6. **Data Transfer Costs**
    - Data transfer between Regions and Availability Zones may incur additional costs, so it's essential to consider this when designing your architecture.
7. **Global Services**
    - Some AWS services are global and not bound to a specific Region, such as AWS IAM (Identity and Access Management) and AWS Route 53 (DNS service).
8. **Region Naming Convention**
    - AWS Region names typically consist of the area name (e.g., "us" for United States) and a description (e.g., "east" or "west").


## Overview of AWS Services

Amazon Web Services (AWS) is the leading cloud platform, offering a comprehensive range of services for compute, storage, networking, machine learning, IoT, and more.

---

### **1. Compute**

Services that provide on-demand computing power.

- **Amazon EC2**: Virtual servers for hosting applications.
- **AWS Lambda**: Serverless compute for event-driven tasks.
- **Amazon ECS/EKS**: Container orchestration using Docker (ECS) or Kubernetes (EKS).
- **AWS Elastic Beanstalk**: Simplified application deployment and management.

---

### **2. Storage**

Scalable and reliable storage solutions.

- **Amazon S3**: Object storage for files, images, and backups.
- **Amazon EBS**: Block storage for EC2 instances.
- **Amazon Glacier**: Low-cost storage for long-term data archiving.
- **AWS Backup**: Centralized backup for AWS resources.

---

### **3. Database**

Managed database services for various use cases.

- **Amazon RDS**: Relational databases (MySQL, PostgreSQL, Oracle, SQL Server).
- **Amazon DynamoDB**: NoSQL database for high-performance applications.
- **Amazon Redshift**: Data warehousing for big data analytics.
- **Amazon ElastiCache**: In-memory caching for real-time applications.

---

### **4. Networking & Content Delivery**

Services to connect, secure, and deliver applications globally.

- **Amazon VPC**: Virtual Private Cloud for isolated network environments.
- **Amazon CloudFront**: Content Delivery Network (CDN) for fast content distribution.
- **AWS Direct Connect**: Dedicated network connections to AWS.
- **Elastic Load Balancing (ELB)**: Distributes traffic across multiple servers.

---

### **5. Security, Identity, and Compliance**

Tools to secure applications and manage access.

- **AWS IAM**: Identity and Access Management for secure access control.
- **AWS Shield**: DDoS protection for web applications.
- **AWS WAF**: Web Application Firewall for filtering malicious traffic.
- **AWS Key Management Service (KMS)**: Managed encryption key storage.

---

### **6. Machine Learning and AI**

Services for developers and data scientists.

- **Amazon SageMaker**: Build, train, and deploy machine learning models.
- **AWS Rekognition**: Image and video analysis.
- **AWS Lex**: Build conversational interfaces (chatbots).
- **Amazon Polly**: Text-to-speech service.

---

### **7. Analytics**

Tools for big data processing and analytics.

- **Amazon EMR**: Big data processing with Apache Spark, Hadoop, etc.
- **Amazon Athena**: Query data stored in S3 using SQL.
- **AWS Glue**: ETL (Extract, Transform, Load) service for data preparation.
- **Amazon QuickSight**: BI (Business Intelligence) and visualization.

---

### **8. Developer Tools**

Support for DevOps practices and automation.

- **AWS CodeCommit**: Managed Git repositories.
- **AWS CodePipeline**: Automate CI/CD workflows.
- **AWS CloudFormation**: Infrastructure as Code (IaC) for resource provisioning.
- **AWS X-Ray**: Debugging and performance analysis for applications.

---

### **9. Internet of Things (IoT)**

Services to connect and manage IoT devices.

- **AWS IoT Core**: Securely connect and manage IoT devices.
- **AWS Greengrass**: Run local compute, messaging, and data caching for IoT devices.

---

### **10. Monitoring and Management**

Tools for monitoring and managing resources.

- **Amazon CloudWatch**: Metrics and logging for AWS services.
- **AWS Trusted Advisor**: Recommendations for cost optimization and security.
- **AWS Config**: Resource configuration tracking.

---

### **Summary of AWS Services**

| **Category** | **Examples** | **Use Cases** |
| --- | --- | --- |
| **Compute** | EC2, Lambda, Elastic Beanstalk | Web hosting, batch processing, serverless applications |
| **Storage** | S3, Glacier, EBS | Backup, archiving, data storage |
| **Database** | RDS, DynamoDB, Redshift | Relational databases, NoSQL, big data analytics |
| **Networking** | VPC, CloudFront, ELB | Secure networks, global content delivery, load balancing |
| **AI/ML** | SageMaker, Rekognition, Polly | Predictive models, image analysis, voice synthesis |
| **Developer Tools** | CodePipeline, CodeBuild, X-Ray | CI/CD automation, application debugging |
